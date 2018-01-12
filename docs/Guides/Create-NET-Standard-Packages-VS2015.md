---
title: "使用 Visual Studio 2015 建立 .NET Standard NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "使用 NuGet 3.x 和 Visual Studio 2015 建立 .NET Standard NuGet 套件的端對端逐步解說。"
keywords: "建立套件, .NET Standard 套件, .NET Standard 對應表"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>使用 Visual Studio 2015 建立 .NET Standard 套件

*適用於 NuGet 3.x。請參閱[使用 Visual Studio 2017 建立 .NET Standard 套件](../guides/create-net-standard-packages-vs2017.md)，以使用 NuGet 4.x+。*

[.NET Standard 程式庫](/dotnet/articles/standard/library)是計劃提供所有 .NET 執行階段使用的 .NET API 正式規格，因此在 .NET 生態系統中能建立較強的一致性。 .NET Standard 程式庫定義一致的 BCL (基底類別庫) API 集合，以供所有 .NET 平台實作，而不論工作負載為何。 它可讓開發人員產生可跨所有 .NET 執行階段使用的 PCL，並減少 (如果無法消除) 共用程式碼中的平台專屬條件式編譯指示詞。

本指南將引導您建立以 .NET Standard 程式庫 1.4 為目標的 NuGet 套件。 這對 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 都適用。 如需詳細資料，請參閱本主題下文中的 [.NET Standard 對應表](#net-standard-mapping-table)。

1. [必要條件](#pre-requisites)
1. [建立類別庫專案](#create-the-class-library-project)
1. [建立和更新 .nuspec 檔案](#create-and-update-the-nuspec-file)
1. [封裝元件](#package-the-component)
1. [其他選項](#additional-options)
1. [.NET Standard 對應表](#net-standard-mapping-table)
1. [相關主題](#related-topics)


## <a name="pre-requisites"></a>必要條件

1. Visual Studio 2015。 從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，當然也可以使用 Professional Edition 和 Enterprise Edition。
1. .NET Core：從 [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849) 安裝 .NET Core 以及適用於 Visual Studio 2015 的範本和其他工具。
1. NuGet CLI。 從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。 如果尚未新增，則請將該位置新增至您的 PATH 環境變數。

> [!Note]
> nuget.exe 本身是 CLI 工具，不是安裝程式，所以請務必從瀏覽器儲存下載的檔案，而不是執行它。



## <a name="create-the-class-library-project"></a>建立類別庫專案

1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [Windows] 節點、選取 [類別庫 (可攜式)]、將名稱變更為 AppLogger，然後按一下 [確定]。

    ![建立新的類別庫專案](media/NetStandard-NewProject.png)

1. 在出現的 [新增可攜式類別庫] 對話方塊中，選取 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 選項。
1. 以滑鼠右鍵按一下方案總管中的 `AppLogger (Portable)`，依序選取 [屬性] 和 [程式庫] 索引標籤，然後按一下 [目標鎖定] 區段的 [目標 .NET 平台標準]。 這會提示您進行確認，然後就可以從下拉式清單中選取 [`.NET Standard 1.4`]：

    ![將目標設定為 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. 按一下 [組建] 索引標籤，將 [組態] 變更為 `Release`，並核取 [XML 文件檔] 方塊。
1. 將程式碼新增至元件，例如：

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. (使用版本組態) 建置專案，並確認 DLL 和 XML 檔案已產生在 bin\Release 資料夾內。

## <a name="create-and-update-the-nuspec-file"></a>建立和更新 .nuspec 檔案

1. 開啟命令提示字元，巡覽至包含 `AppLogg.csproj` 資料夾的資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `AppLogger.nuspec` 檔案：

```
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
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. 將參考組件新增至 `.nuspec` 檔案，也就是程式庫的 DLL 和 IntelliSense XML 檔案：

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. 以滑鼠右鍵按一下解決方案，然後選取 [組建方案] 產生套件的所有檔案。


## <a name="package-the-component"></a>封裝元件

只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：

```
nuget pack AppLogger.nuspec
```

這會產生 `AppLogger.YOUR_NAME.1.0.0.nupkg`。 在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：

![顯示 AppLogger 套件的 NuGet 套件總管](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。 然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。

若要讓其他開發人員使用您的套件，請遵循[發行套件](../create-packages/publish-a-package.md)上的指示。

請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。 在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。

## <a name="additional-options"></a>其他選項

下列各節會進入建立 NuGet 套件的其他選項：

- [宣告相依性](#declaring-dependencies)
- [支援多個目標 Framework](#supporting-multiple-target-frameworks)
- [新增 MSBuild 的目標與 props](#adding-targets-and-props-for-msbuild)
- [建立當地語系化的套件](#creating-localized-packages)
- [新增讀我檔案](#adding-a-readme)

### <a name="declaring-dependencies"></a>宣告相依性

如有其他 NuGet 套件的任何相依性，請使用 `<group>` 項目在 `<dependencies>` 項目中列出它們。 例如，若要宣告對 NewtonSoft.Json 8.0.3 或更新版本的相依性，請新增下列內容：

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

*version* 屬性的語法在此表示接受該版本 8.0.3 或更新版本。 若要指定不同的版本範圍，請參閱[套件版本控制](../reference/package-versioning.md)。

### <a name="supporting-multiple-target-frameworks"></a>支援多個目標 Framework

假設您想要利用 .NET Standard 1.4 不提供的 .NET Framework 4.6.2 API。 您需要先使用條件式編譯或共用專案，確定程式庫相容於 .NET 4.6.2，才能執行此作業。 (在 Visual Studio 中，您可以建立 NetCore 專案、將 Framework 選項新增至多個 Framework 區段，然後建置。)然後使用簡單的慣例式工作目錄技巧建立套件，如下所示：

1. 在包含 `.nuspec` 檔案的專案根資料夾中，建立名為 `lib` 的資料夾。
1. 在 `lib` 中，為您想要支援的每個平台建立資料夾：

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. 在 `.nuspec` 檔案中，在 `package` 節點下新增 `files` 節點，並使用萬用字元參考 `lib` 中的檔案。 **注意：**不支援以慣例型工作目錄方法取代權杖，所以請使用常值取代它們：

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. 使用 `nuget pack AppLogger.spec` 再次建立套件。

如需使用這項技術的詳細資料，請參閱[支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)

### <a name="adding-targets-and-props-for-msbuild"></a>新增 MSBuild 的目標與 props

在某些情況下，您可能想要在取用您套件的專案中新增自訂組建目標或屬性，例如在建置期間執行自訂工具或程序。 執行此作業，只要依下列步驟所述，將檔案新增至 `\build` 資料夾即可。 當 NuGet 使用 \build 檔案安裝套件時，會在指向 .targets 和 .props 檔案的專案檔中新增 MSBuild 項目。

> [!Note]
> 當使用 `project.json` 時，目標不會新增至專案，但可透過 `project.lock.json` 提供。


1. 在包含 `.nuspec` 檔案的專案資料夾中，建立名為 `build` 的資料夾。
1. 在 `build` 內，為每個受支援的 `build` 建立資料夾，並在這些資料夾內放置您的 `.targets` 和 `.props` 檔案：

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. 在 `.nuspec` 檔案中，在 `package` 節點下新增 `files` 節點，並使用萬用字元參考 `build` 中的檔案。

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. 使用 `nuget pack AppLogger.nuspec` 再次建立套件。

如需其他詳細資料，請參閱[在套件中包含 MSBuild props 和目標](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)。


### <a name="creating-localized-packages"></a>建立當地語系化的套件

若要建立程式庫的當地語系化版本，您可以為不同的地區設定建立個別的套件，或在單一套件內包含當地語系化資源組件。 以下示範以第二種方法建立德文和義大利文的版本：

1. 在 `lib` 下的每個目標 Framework 資料夾內，建立每種受支援語言的資料夾，英文預設值除外。 您可以在這些資料夾中放置資源組件和當地語系化 IntelliSense XML 檔案。 例如: 

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. 在 `.nuspec` 檔案中，參考 `<files>` 節點中的這些檔案：

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. 使用 `nuget pack AppLogger.nuspec` 再次建立套件。


### <a name="adding-a-readme"></a>新增讀我檔案

當您在套件的根目錄中包含 `readme.txt` 檔案時，Visual Studio 會在直接安裝套件時顯示它。

> [!Note]
> 已安裝為相依性的套件或 .NET Core 專案不會顯示讀我檔案。


若要這樣做，請建立您的 `readme.txt` 檔案，將它放在專案根資料夾中，並在 `.nuspec` 檔案中參考它：

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


## <a name="net-standard-mapping-table"></a>.NET Standard 對應表

|平台名稱 |Alias|
|--------------|-----|
|.NET Standard | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET 核心 | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Mono/Xamarin 平台| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|通用 Windows 平台| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>相關主題

- [Nuspec 參考](../schema/nuspec.md)
- [符號套件](../create-packages/symbol-packages.md)
- [套件版本控制](../reference/package-versioning.md)
- [支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [在套件中包含 MSBuild 屬性和目標](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)
- [.NET Standard 程式庫文件](/dotnet/articles/standard/library)
- [從 .NET Framework 移轉到 .NET Core](/dotnet/articles/core/porting/index)
