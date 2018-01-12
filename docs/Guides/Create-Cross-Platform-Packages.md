---
title: "建立跨平台 NuGet 套件 (適用於 iOS、Android 和 Windows) | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: "有關如何為 Xamarin 建立 NuGet 套件的端對端逐步解說，而這些套件在 iOS、Android 和 Windows 上使用原生 API。"
keywords: "建立套件, Xamarin 的套件, 跨平台套件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f372856232f151efcf972881cffbe7d4bb7ed6ee
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="create-cross-platform-packages"></a>建立跨平台套件

跨平台套件包含在 iOS、Android 和 Windows 上使用原生 API 的程式碼 (視執行階段作業系統而定)。 雖然這十分簡單，但最好是讓開發人員使用 PCL 中的套件，或透過通用 API 介面區的 .NET Standard 程式庫。

在本逐步解說中，您將建立可在 iOS、Android 和 Windows 上之行動專案中使用的跨平台 NuGet 套件。

1. [必要條件](#pre-requisites)
1. [建立專案結構和抽象程式碼](#create-the-project-structure-and-abstraction-code)
1. [撰寫平台特定程式碼](#write-your-platform-specific-code)
1. [建立和更新 .nuspec 檔案](#create-and-update-the-nuspec-file)
1. [封裝元件](#package-the-component)
1. [相關主題](#related-topics)

## <a name="pre-requisites"></a>必要條件

1. 含通用 Windows 平台 (UWP) 和 Xamarin 的 Visual Studio 2015。 從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，當然也可以使用 Professional Edition 和 Enterprise Edition。 若要包含 UWP 和 Xamarin 工具，請選取 [自訂安裝] 並檢查適當的選項。
1. NuGet CLI。 從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。 如果尚未新增，則請將該位置新增至您的 PATH 環境變數。

> [!Note]
> nuget.exe 本身是 CLI 工具，不是安裝程式，因此請務必從瀏覽器儲存下載的檔案，而不是執行它。


## <a name="create-the-project-structure-and-abstraction-code"></a>建立專案結構和抽象程式碼

1. 針對 Visual Studio，下載並執行 [ Xamarin 範本延伸模組外掛程式](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)。 這些範本可讓您輕鬆建立此逐步解說的必要專案結構。
1. 在 Visual Studio 中，選取 [檔案] > [新增] > [專案]、搜尋 `Plugin`、選取 [Plugin for Xamarin ] (Xamarin 的外掛程式) 範本、將名稱變更為 LoggingLibrary，然後按一下 [確定]。

    ![Visual Studio 中的新空白應用程式 (Xamarin.Forms 可攜式) 專案](media/CrossPlatform-NewProject.png)

所產生的方案包含兩個 PCL 專案，以及各種平台特定專案：

- 名為 `Plugin.LoggingLibrary.Abstractions (Portable)` 的 PCL 會定義元件的公用介面 (API 介面區)；在此情況下，ILoggingLibrary.cs 檔案中包含 `ILoggingLibrary` 介面。 這是您在其中定義程式庫介面的位置。
- 其他 PCL `Plugin.LoggingLibrary (Portable)` 會在 CrossLoggingLibrary.cs 中包含程式碼，以找出執行階段之抽象介面的平台特定實作。 您通常不需要修改這個檔案。
- 平台特定專案 (例如 `Plugin.LoggingLibrary.Android`)，每個專案都會在其個別 LoggingLibraryImplementation.cs 檔案中包含原生介面實作。 這是您建置程式庫程式碼的位置。

Abstractions 專案的 ILoggingLibrary.cs 檔案預設會包含介面定義，但沒有任何方法。 基於本逐步解說的目的，新增 `Log` 方法，如下所示：

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

1. 開啟每個平台專案的 `LoggingLibraryImplementation.cs` 檔案，並新增必要程式碼。 例如 (使用 `Plugin.LoggingLibrary.Android` 專案)：

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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
1. 以滑鼠右鍵按一下 iOS 專案、選取 [屬性]、按一下 [建置] 索引標籤，然後從 [輸出路徑] 和 [XML 文件檔案] 設定中移除 "\iPhone"。 在本逐步解說中，這只是方便之後使用。 在完成時儲存檔案。
1. 以滑鼠右鍵按一下方案，並選取 [組態管理員]，然後為 PCL 和每個所支援的平台核取 [建置] 方塊。
1. 以滑鼠右鍵按一下方案，然後選取 [建置方案] 檢查您的工作，並產生之後將封裝的成品。 如果您收到有關遺漏參考的錯誤，請以滑鼠右鍵按一下方案，然後選取 [還原 NuGet 套件] 以安裝相依性並重建。

> [!Note]
> 若要針對 iOS 建置，您需要連線至 Visual Studio 的網路 Mac，如　[Xamarin.iOS for Visual Studio 簡介](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)上所述。 如果您沒有可用的 Mac，請在組態管理員中清除 iOS 專案 (上述步驟 3)。


## <a name="create-and-update-the-nuspec-file"></a>建立和更新 .nuspec 檔案

1. 開啟命令提示字元，並巡覽至 `LoggingLibrary` 資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `Package.nuspec` 檔案：

```
nuget spec
```

1. 將這個檔案重新命名為 `LoggingLibrary.nuspec`，並在編輯器中予以開啟。
1. 更新檔案使其符合下列內容，並使用適當的值取代 YOUR_NAME。 尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。 另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。

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
        <copyright>Copyright 2016</copyright>
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
    <copyright>Copyright 2016</copyright>
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

```
nuget pack LoggingLibrary.nuspec
```

這會產生 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`。 在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：

![顯示 LoggingLibrary 套件的 NuGet 套件總管](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。 然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。


若要讓其他開發人員使用您的套件，請遵循[發行套件](../create-packages/publish-a-package.md)上的指示。

## <a name="related-topics"></a>相關主題

- [Nuspec 參考](../schema/nuspec.md)
- [符號套件](../create-packages/symbol-packages.md)
- [套件版本控制](../reference/package-versioning.md)
- [支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [在套件中包含 MSBuild 屬性和目標](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)