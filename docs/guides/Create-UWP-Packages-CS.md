---
title: '建立 UWP 平臺的 NuGet 套件 (c # ) '
description: '使用 c # 中通用 Windows 平臺的 Windows 執行階段元件來建立 NuGet 套件的端對端逐步解說。'
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 22df2cd6dc374ba265c79a019747191e797b774c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774288"
---
# <a name="create-uwp-packages-c"></a> (c # ) 建立 UWP 套件

[通用 Windows 平台 (UWP)](/windows/uwp) 會為每個執行 Windows 10 的裝置提供通用應用程式平台。 在此模型內，UWP 應用程式可以呼叫所有裝置通用的 WinRT API，也可以呼叫應用程式執行所在裝置系列特有的 API (包含 Win32 和 .NET)。

在這個逐步解說中，您會使用 c # UWP 元件建立 NuGet 套件， (包括可在 Managed 和原生專案中使用的 XAML 控制項) 。

## <a name="prerequisites"></a>Prerequisites

1. Visual Studio 2019。 從 [visualstudio.com](https://www.visualstudio.com/)免費安裝2019版的社區版;您也可以使用 Professional edition 和 Enterprise edition。

1. NuGet CLI。 從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 `nuget.exe`，並將它儲存至您選擇的位置 (直接下載為 `.exe`)。 如果尚未新增，則請將該位置新增至您的 PATH 環境變數。 [更多詳細資料](../reference/nuget-exe-cli-reference.md#windows)。

## <a name="create-a-uwp-windows-runtime-component"></a>建立 UWP Windows 執行階段元件

1. 在 Visual Studio 中，選擇 [檔案] **> [新的 > 專案**]，搜尋 [uwp c #]，選取 **Windows 執行階段元件 (通用 Windows)** 範本，按一下 [下一步]，將名稱變更為 ImageEnhancer，然後按一下 [建立]。 當系統出現提示時，請接受目標版本和最低版本的預設值。

    ![建立新 UWP Windows 執行階段元件專案](media/UWP-NewProject-CS.png)

1. 以滑鼠右鍵按一下方案總管中的專案，選取 [ **加入 > 新專案**]，選取 [樣板 **化控制項**]，將名稱變更為 AwesomeImageControl.cs，然後按一下 [ **新增**]：

    ![將新的 XAML 樣板化控制項項目新增至專案](media/UWP-NewXAMLControl-CS.png)

1. 以滑鼠右鍵按一下方案總管中的專案，然後選取 [ **屬性]。** 在 [屬性] 頁面中，選擇 [ **組建** ] 索引標籤，並啟用 **XML 檔** 檔：

    ![將 [產生 XML 文件檔] 設定為 [是]](media/UWP-GenerateXMLDocFiles-CS.png)

1. 以滑鼠右鍵按一下 *方案* ，選取 [ **批次組建**]，然後在對話方塊中檢查五個組建方塊，如下所示。 這確保當您執行建置時，會為 Windows 所支援的每個目標系統產生一組完整成品。

    ![批次建置](media/UWP-BatchBuild-CS.png)

1. 在 [批次建置] 對話方塊中，按一下 [建置] 確認專案，並建立 NuGet 套件所需的輸出檔案。

> [!Note]
> 在本逐步解說中，您將偵錯成品用於套件。 針對非偵錯套件，請改為檢查 [批次建置] 對話方塊中的 [發行] 選項，並參照所遵循步驟中產生的發行資料夾。

## <a name="create-and-update-the-nuspec-file"></a>建立和更新 .nuspec 檔案

若要建立初始 `.nuspec` 檔案，請執行下列三個步驟。 下列各節接著會引導您完成其他必要更新。

1. 開啟命令提示字元，並巡覽至包含 `ImageEnhancer.csproj` 的資料夾 (這是低於方案檔一階的子資料夾)。
1. 執行 [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) 命令以產生 (檔案的名稱 `ImageEnhancer.nuspec` 取自) 的檔案名 `.csroj` ：

    ```cli
    nuget spec
    ```

1. 在編輯器中開啟 `ImageEnhancer.nuspec`，更新它使符合下列內容，以適當的值取代 YOUR_NAME。 請勿保留任何 $propertyName $ 值。 尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。 另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。

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
        <copyright>Copyright 2020</copyright>
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
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
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

在您的元件中，ImageEnhancer 類型的核心邏輯是在機器碼中，它包含在 `ImageEnhancer.winmd` 針對每個目標執行時間產生的各種元件中， (ARM、ARM64、x86 和 x64) 。 若要將這些併入套件中，請在 `<files>` 區段和其相關聯 .pri 資源檔中參考它們：

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>封裝元件

完成 `.nuspec` 參考您需要包含在套件中的所有檔案之後，您就可以開始執行 [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) 命令：

```cli
nuget pack ImageEnhancer.nuspec
```

這會產生 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`。 在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：

![顯示 ImageEnhancer 套件的 NuGet 套件總管](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。 然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。

若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)的指示。

## <a name="related-topics"></a>相關主題

- [nuspec 參考](../reference/nuspec.md)
- [符號套件](../create-packages/symbol-packages-snupkg.md)
- [套件版本控制](../concepts/package-versioning.md)
- [支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)
- [在套件中包含 MSBuild 屬性和目標](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)