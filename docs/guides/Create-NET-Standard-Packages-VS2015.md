---
title: 使用 Visual Studio 2015 建立 .NET Standard 和 .NET Framework NuGet 套件
description: 使用 NuGet 3.x 和 Visual Studio 2015 建立 .NET Standard 和 NuGet 套件的逐步解說。
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: af0c42853a9e407557a010ff2793406499b4b2ef
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426872"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>使用 Visual Studio 2015 建立 .NET Standard 和 .NET Framework 套件

**注意：** 建議使用 Visual Studio 2017 來開發 .NET Standard 程式庫。 可以使用 Visual Studio 2015，但 .NET Core 工具僅提供為「預覽」階段。 如需使用 NuGet 4.x+ 和 Visual Studio 2017 的資訊，請參閱[使用 Visual Studio 2017 建立和發佈套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)。

[.NET Standard 程式庫](/dotnet/articles/standard/library)是計劃提供所有 .NET 執行階段使用的 .NET API 正式規格，因此在 .NET 生態系統中能建立較強的一致性。 .NET Standard 程式庫定義一致的 BCL (基底類別庫) API 集合，以供所有 .NET 平台實作，而不論工作負載為何。 其可讓開發人員產生可跨所有 .NET 執行階段使用的程式碼，並減少 (如果無法消除) 共用程式碼中的平台專屬條件式編譯指示詞。

本指南引導您建立以 .NET Standard Library 1.4 為目標的 NuGet 套件，或是以 .NET Framework 4.6 為目標的套件。 .NET Standard 1.4 程式庫可用於 .NET Framework 4.6.1、Universal Windows Platform 10、.NET Core 和 Mono/Xamarin。 如需詳細資訊，請參閱 [.NET Standard 對應表](/dotnet/standard/net-standard#net-implementation-support) (.NET 文件)。 您可以依需求選擇其他版本的 .NET Standard 程式庫。

## <a name="prerequisites"></a>必要條件

1. Visual Studio 2015 Update 3
1. (僅限 .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/) \(英文\)
1. NuGet CLI。 從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。 如果尚未新增，則請將該位置新增至您的 PATH 環境變數。

    > [!Note]
    > nuget.exe 本身是 CLI 工具，不是安裝程式，所以請務必從瀏覽器儲存下載的檔案，而不是執行它。

## <a name="create-the-class-library-project"></a>建立類別庫專案

1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]  ，依序展開 [Visual C#] > [Windows]  節點，選取 [類別庫 (可攜式)]  將名稱變更為 AppLogger，然後選取 [確定]  。

    ![建立新的類別庫專案](media/NetStandard-NewProject.png)

1. 在顯示的 [加入可攜式類別庫]  對話方塊中，選取 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 的選項。 (如果目標是 .NET Framework，您可以選取任何適當的選項。)

1. 如果目標是 .NET Standard，在 [方案總管] 中，以滑鼠右鍵按一下 [`AppLogger (Portable)`]，選取 [屬性]  ，選取 [程式庫]  索引標籤，然後在 [目標]  區段中選取 [目標 .NET 平台標準]  。 此動作會提示您確認，之後您就可以從下拉式清單中選取 `.NET Standard 1.4` (或其他可用版本)：

    ![將目標設定為 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. 按一下 [組建]  索引標籤，將 [組態]  變更為 `Release`，並核取 [XML 文件檔]  方塊。

1. 將程式碼新增至元件，例如：

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. 將組態設定為發行、建置專案，並確認 DLL 和 XML 檔案已產生在 `bin\Release` 資料夾內。

## <a name="create-and-update-the-nuspec-file"></a>建立和更新 .nuspec 檔案

1. 開啟命令提示字元，巡覽至包含 `AppLogger.csproj` 資料夾的資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `AppLogger.nuspec` 檔案：

    ```cli
    nuget spec
    ```

1. 在編輯器中開啟 `AppLogger.nuspec`，更新它使符合下列內容，以適當的值取代 YOUR_NAME。 尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。 另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. 將參考組件新增至 `.nuspec` 檔案，也就是程式庫的 DLL 和 IntelliSense XML 檔案：

    如果目標是 .NET Standard，項目會顯示如下：

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    如果目標是 .NET Framework，項目會顯示如下：

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. 以滑鼠右鍵按一下解決方案，然後選取 [組建方案]  產生套件的所有檔案。

### <a name="declaring-dependencies"></a>宣告相依性

如有其他 NuGet 套件的任何相依性，請使用 `<group>` 項目在資訊清單的 `<dependencies>` 項目中加以列出。 例如，若要宣告對 NewtonSoft.Json 8.0.3 或更新版本的相依性，請新增下列內容：

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

*version* 屬性的語法在此表示接受該版本 8.0.3 或更新版本。 若要指定不同的版本範圍，請參閱[套件版本控制](../reference/package-versioning.md)。

### <a name="adding-a-readme"></a>新增讀我檔案

請建立您的 `readme.txt` 檔案，將其置於專案根資料夾中，並在 `.nuspec` 檔案中加以參考：

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

當套件安裝至專案中時，Visual Studio 會顯示 `readme.txt`。 安裝至 .NET Core 專案時，或對於已安裝為相依性的套件，檔案則不會顯示。

## <a name="package-the-component"></a>封裝元件

只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：

```cli
nuget pack AppLogger.nuspec
```

這會產生 `AppLogger.YOUR_NAME.1.0.0.nupkg`。 在 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) \(英文\) 之類的工具中開啟此檔案，並展開所有節點，您會看到以下內容 (顯示的是 .NET Standard)：

![顯示 AppLogger 套件的 NuGet 套件總管](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。 然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。

若要讓其他開發人員使用您的套件，請遵循[發佈套件](../nuget-org/publish-a-package.md)上的指示。

請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。 在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。

## <a name="related-topics"></a>相關主題

- [.nuspec 參考](../reference/nuspec.md)
- [支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [在套件中包含 MSBuild 屬性和目標](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)
- [符號套件](../create-packages/symbol-packages.md)
- [套件版本控制](../reference/package-versioning.md)
- [.NET Standard 程式庫文件](/dotnet/articles/standard/library)
- [從 .NET Framework 移轉到 .NET Core](/dotnet/articles/core/porting/index)
