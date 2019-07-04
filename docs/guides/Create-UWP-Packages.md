---
title: 建立通用 Windows 平台的 NuGet 套件
description: 有關如何使用適用於通用 Windows 平台之 Windows 執行階段元件來建立 NuGet 套件的端對端逐步解說。
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 52f2057f7d1012b75bba9e8730eacffd99adacfa
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426868"
---
# <a name="create-uwp-packages"></a>建立 UWP 套件

[通用 Windows 平台 (UWP)](https://developer.microsoft.com/windows) 會為每個執行 Windows 10 的裝置提供通用應用程式平台。 在此模型內，UWP 應用程式可以呼叫所有裝置通用的 WinRT API，也可以呼叫應用程式執行所在裝置系列特有的 API (包含 Win32 和 .NET)。

在本逐步解說中，您將使用可在受控和原生專案中使用的原生 UWP 元件 (包含 XAML 控制項) 來建立 NuGet 套件。

## <a name="prerequisites"></a>必要條件

1. Visual Studio 2017 或 Visual Studio 2015. 從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2017 Community Edition，也可以使用 Professional Edition 和 Enterprise Edition。

1. NuGet CLI。 從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 `nuget.exe`，並將它儲存至您選擇的位置 (直接下載為 `.exe`)。 如果尚未新增，則請將該位置新增至您的 PATH 環境變數。

## <a name="create-a-uwp-windows-runtime-component"></a>建立 UWP Windows 執行階段元件

1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]  ，並展開 [Visual C++] > [Windows] > [通用]  節點，然後選取 [Windows 執行階段元件 (通用 Windows)]  範本，並將名稱變更為 ImageEnhancer，然後按一下 [確定]。 當系統出現提示時，請接受目標版本和最低版本的預設值。

    ![建立新 UWP Windows 執行階段元件專案](media/UWP-NewProject.png)

1. 以滑鼠右鍵按一下方案總管中的專案，選取 [新增] > [新增項目]  、按一下 [Visual C++] > [XAML]  節點、選取 [樣板化控制項]  、將名稱變更為 AwesomeImageControl.cpp，然後按一下 [新增]  ：

    ![將新的 XAML 樣板化控制項項目新增至專案](media/UWP-NewXAMLControl.png)

1. 以滑鼠右鍵按一下方案總管，然後選取 [屬性]  。 在 [屬性] 頁面中，展開 [組態屬性] > [C/C++]  ，然後按一下 [輸出檔案]  。 在右窗格中，將 [產生 XML 文件檔]  的值變更為 [是]：

    ![將 [產生 XML 文件檔] 設定為 [是]](media/UWP-GenerateXMLDocFiles.png)

1. 現在以滑鼠右鍵按一下「方案」  ，並選取 [批次建置]  ，然後核取對話方塊中的三個 [偵錯] 方塊，如下顯示。 這確保當您執行建置時，會為 Windows 所支援的每個目標系統產生一組完整成品。

    ![批次建置](media/UWP-BatchBuild.png)

1. 在 [批次建置] 對話方塊中，按一下 [建置]  確認專案，並建立 NuGet 套件所需的輸出檔案。

> [!Note]
> 在本逐步解說中，您將偵錯成品用於套件。 針對非偵錯套件，請改為檢查 [批次建置] 對話方塊中的 [發行] 選項，並參照所遵循步驟中產生的發行資料夾。

## <a name="create-and-update-the-nuspec-file"></a>建立和更新 .nuspec 檔案

若要建立初始 `.nuspec` 檔案，請執行下列三個步驟。 下列各節接著會引導您完成其他必要更新。

1. 開啟命令提示字元，並巡覽至包含 `ImageEnhancer.vcxproj` 的資料夾 (這是低於方案檔一階的子資料夾)。
1. 執行 NuGet `spec` 命令來產生 `ImageEnhancer.nuspec` (檔案名稱取自 `.vcxproj` 檔案的名稱)：

    ```cli
    nuget spec
    ```

1. 在編輯器中開啟 `ImageEnhancer.nuspec`，然後進行更新使其符合下列內容，並使用適當的值取代 YOUR_NAME。 尤其是在整個 nuget.org 中，`<id>` 值必須為唯一 (請參閱[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。 另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> 針對公眾使用而建置的套件，請特別注意 `<tags>` 項目，因為這些標籤可協助其他人找到您的套件，並了解其用途。

### <a name="adding-windows-metadata-to-the-package"></a>將 Windows 中繼資料新增至套件

Windows 執行階段元件需要描述其所有公開可用類型的中繼資料，讓其他應用程式和程式庫可以使用元件。 此中繼資料包含在 .winmd 檔案中，而此檔案是在您編譯專案時建立，並且必須併入 NuGet 套件中。 具有 IntelliSense 資料的 XML 檔案也會在相同的時間建置，同時應該予以包含。

將下列 `<files>` 節點新增至 `.nuspec` 檔案：

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>新增 XAML 內容

若要包含 XAML 控制項與您的元件，您需要新增包含控制項的預設範本 (如專案範本所產生)。 在 `<files>` 區段中也包含這項內容：

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>新增原生實作程式庫

在您的元件內，ImageEnhancer 類型的核心邏輯是原生程式碼，包含在為每個目標執行階段 (ARM、x86 和 x64) 產生的各種 `ImageEnhancer.dll` 組件。 若要將這些併入套件中，請在 `<files>` 區段和其相關聯 .pri 資源檔中參考它們：

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>新增 .targets

接下來，可能使用 NuGet 套件的 C++ 和 JavaScript 專案需要有 .targets 檔案，才能識別必要組件和 winmd 檔案 (C# 和 Visual Basic 專案會自動執行這項作業)。將下方文字複製到 `ImageEnhancer.targets` 以建立此檔案，然後將其儲存到與 `.nuspec` 檔案相同的資料夾中。 _注意_：此 `.targets` 檔案的名稱必須與套件識別碼相同 (例如 `.nupspec` 檔案中的 `<Id>` 元素)：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

然後在 `.nuspec` 檔案中參照 `ImageEnhancer.targets`：

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>最終 .nuspec

最終 `.nuspec` 檔案現在看起來應該如下所示，並且應該將 YOUR_NAME 取代為適當值：

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>封裝元件

只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：

```cli
nuget pack ImageEnhancer.nuspec
```

這會產生 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`。 在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：

![顯示 ImageEnhancer 套件的 NuGet 套件總管](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。 然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。

若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)上的指示。

## <a name="related-topics"></a>相關主題

- [.nuspec 參考](../reference/nuspec.md)
- [符號套件](../create-packages/symbol-packages.md)
- [套件版本控制](../reference/package-versioning.md)
- [支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [在套件中包含 MSBuild 屬性和目標](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)
