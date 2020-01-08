---
title: 建立適用于 Xamarin （適用于 iOS、Android 和 Windows）的 NuGet 套件（含 Visual Studio 2017 或2019）
description: 有關如何為 Xamarin 建立 NuGet 套件的端對端逐步解說，而這些套件在 iOS、Android 和 Windows 上使用原生 API。
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fce3c9a92dfee325f9e914bf3d6444601fb38b6c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385667"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>建立具有 Visual Studio 2017 或2019之 Xamarin 的套件

適用於 Xamarin 的套件包含使用 iOS、Android 和 Windows (視執行階段作業系統而定) 上原生 API 的程式碼。 雖然這十分簡單，但最好是讓開發人員使用 PCL 中的套件，或透過通用 API 介面區的 .NET Standard 程式庫。

在本逐步解說中，您會使用 Visual Studio 2017 或2019來建立可在 iOS、Android 和 Windows 上的行動專案中使用的跨平臺 NuGet 套件。

1. [必要條件](#prerequisites)
1. [建立專案結構和抽象程式碼](#create-the-project-structure-and-abstraction-code)
1. [撰寫平台特定程式碼](#write-your-platform-specific-code)
1. [建立和更新 .nuspec 檔案](#create-and-update-the-nuspec-file)
1. [封裝元件](#package-the-component)
1. [相關主題](#related-topics)

## <a name="prerequisites"></a>必要條件：

1. 使用通用 Windows 平臺（UWP）和 Xamarin Visual Studio 2017 或2019。 從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，當然也可以使用 Professional Edition 和 Enterprise Edition。 若要包含 UWP 和 Xamarin 工具，請選取 [自訂安裝] 並檢查適當的選項。
1. NuGet CLI。 從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。 如果尚未新增，則請將該位置新增至您的 PATH 環境變數。

> [!Note]
> nuget.exe 本身是 CLI 工具，不是安裝程式，因此請務必從瀏覽器儲存下載的檔案，而不是執行它。

## <a name="create-the-project-structure-and-abstraction-code"></a>建立專案結構和抽象程式碼

1. 下載並執行適用于 Visual Studio 的[跨平臺 .NET Standard 外掛程式範本延伸模組](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)。 這些範本可讓您輕鬆建立此逐步解說的必要專案結構。
1. 在 Visual Studio 2017，檔案 **> 新增 > 專案**中，搜尋 `Plugin`，選取 [**跨平臺 .NET Standard 程式庫外掛程式**] 範本，將名稱變更為 LoggingLibrary，然後按一下 [確定]。

    ![VS 2017 中的新空白應用程式（Xamarin. 表單可攜）專案](media/CrossPlatform-NewProject.png)

    在 Visual Studio 2019，檔案 **> 新增 > 專案**中，搜尋 `Plugin`，選取 [**跨平臺 .NET Standard 程式庫外掛程式**] 範本，然後按 [下一步]。

    ![VS 2019 中的新空白應用程式（Xamarin. 表單可攜）專案](media/CrossPlatform-NewProject19-Part1.png)

    將名稱變更為 LoggingLibrary，然後按一下 [建立]。

    ![VS 2019 中的新空白應用程式（Xamarin 形式可攜）設定](media/CrossPlatform-NewProject19-Part2.png)

產生的方案包含兩個共用的專案，以及各種不同的平臺特定專案：

- `ILoggingLibrary` 專案（包含在 `ILoggingLibrary.shared.cs` 檔案中）會定義元件的公用介面（API 表面區域）。 這是您在其中定義程式庫介面的位置。
- 另一個共用專案包含 `CrossLoggingLibrary.shared.cs` 中的程式碼，可在執行時間找出抽象介面的平臺特定執行。 您通常不需要修改這個檔案。
- 平臺特定專案（例如 `LoggingLibrary.android.cs`）每個包含在其各自的 `LoggingLibraryImplementation.cs` （VS 2017）或 `LoggingLibrary.<PLATFORM>.cs` （VS 2019）檔案中都包含介面的原生執行。 這是您建置程式庫程式碼的位置。

根據預設，`ILoggingLibrary` 專案的 ILoggingLibrary.shared.cs 檔包含介面定義，但沒有方法。 基於本逐步解說的目的，新增 `Log` 方法，如下所示：

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>撰寫平台特定程式碼

若要實作 `ILoggingLibrary` 介面的平台特定實作和其方法，請執行下列動作：

1. 開啟每個平臺專案的 `LoggingLibraryImplementation.cs` （VS 2017）或 `LoggingLibrary.<PLATFORM>.cs` （VS 2019）檔案，並新增必要的程式碼。 例如（使用 `Android` 平臺專案）：

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. 針對每個您想要支援的平台，重複專案中的這個實作。
1. 以滑鼠右鍵按一下方案，然後選取 [建置方案] 檢查您的工作，並產生之後將封裝的成品。 如果您收到有關遺漏參考的錯誤，請以滑鼠右鍵按一下方案，然後選取 [還原 NuGet 套件] 以安裝相依性並重建。

> [!Note]
> 如果您使用 Visual Studio 2019，在選取 [**還原 NuGet 套件**] 並嘗試重建之前，您必須將 `MSBuild.Sdk.Extras` 的版本變更為 `LoggingLibrary.csproj`中的 `2.0.54`。 只有先以滑鼠右鍵按一下專案（在方案底下），然後選取 [`Unload Project`]，然後在已卸載的專案上按一下滑鼠右鍵，然後選取 [`Edit LoggingLibrary.csproj`]，才能存取這個檔案。

> [!Note]
> 若要針對 iOS 建置，您需要連線至 Visual Studio 的網路 Mac，如　[Xamarin.iOS for Visual Studio 簡介](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)上所述。 如果您沒有可用的 Mac，請在組態管理員中清除 iOS 專案 (上述步驟 3)。

## <a name="create-and-update-the-nuspec-file"></a>建立和更新 .nuspec 檔案

1. 開啟命令提示字元，並巡覽至 `LoggingLibrary` 資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `Package.nuspec` 檔案：

    ```cli
    nuget spec
    ```

1. 將這個檔案重新命名為 `LoggingLibrary.nuspec`，並在編輯器中予以開啟。
1. 更新檔案使其符合下列內容，並使用適當的值取代 YOUR_NAME。 尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。 另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> 您的套件版本可以加上 `-alpha`、`-beta` 或 `-rc` 後置詞，以將套件標示為發行前版本，如需發行前版本的詳細資訊，請檢查[發行前版本](../create-packages/prerelease-packages.md)。

### <a name="add-reference-assemblies"></a>新增參考組件

若要包含平台特定參考組件，請針對您的支援平台適當地將下列新增至 `LoggingLibrary.nuspec` 的 `<files>` 項目：

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> 若要縮短 DLL 和 XML 檔案的名稱，請以滑鼠右鍵按一下任何指定的專案，並選取 [程式庫] 索引標籤，然後變更組件名稱。

### <a name="add-dependencies"></a>新增相依性

如果您有原生實作的特定相依性，請搭配使用 `<dependencies>` 項目與 `<group>` 項目來指定它們，例如：

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

例如，下列會將 iTextSharp 設定為 UAP 目標的相依性：

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>最終 .nuspec

最終 `.nuspec` 檔案現在看起來應該如下所示，並且應該將 YOUR_NAME 取代為適當值：

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>封裝元件

只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：

```cli
nuget pack LoggingLibrary.nuspec
```

這會產生 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`。 在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：

![顯示 LoggingLibrary 套件的 NuGet 套件總管](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。 然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。

若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)的指示。

## <a name="related-topics"></a>相關主題

- [Nuspec 參考](../reference/nuspec.md)
- [符號套件](../create-packages/symbol-packages.md)
- [套件版本控制](../concepts/package-versioning.md)
- [支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [在套件中包含 MSBuild 屬性和目標](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)