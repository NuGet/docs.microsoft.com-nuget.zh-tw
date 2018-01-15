---
title: "如何使用 NuGet 封裝 UWP 控制項 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "如何建立包含 UWP 控制項的 NuGet 套件，包含 Visual Studio 和 Blend 設計工具的必要中繼資料和支援檔案。"
keywords: "NuGet UWP 控制項、Visual Studio XAML 設計工具、Blend 設計工具、自訂控制項"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8756ce472c11a05370914841245295361b3f179b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>建立 UWP 控制項作為 NuGet 套件

使用 Visual Studio 2017，您可以利用以 NuGet 套件傳遞之 UWP 控制項的新增功能。 本指南會逐步引導您使用 [ExtensionSDKasNuGetPackage 範例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)來使用這些功能。 

## <a name="pre-requisites"></a>必要條件：

1.  Visual Studio 2017
1.  了解如何[建立 UWP 套件](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>新增 XAML 控制項的工具箱/資產窗格支援

若要讓 XAML 控制項出現在 Visual Studio 的 XAML 設計工具工具箱中以及 Blend 的 [資產] 索引標籤中，請在套件專案的 `tools` 資料夾根中建立 `VisualStudioToolsManifest.xml` 檔案。 如果您不需要控制項出現在工具箱或 [資產] 窗格中，則不需要此檔案。

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

該檔案的結構如下：

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

其中：

- *your_package_file*：您控制檔案的名稱，例如 `ManagedPackage.winmd` ("ManagedPackage" 是用於此範例的任意名稱，沒有任何其他意義)。
- *vs_category*：Visual Studio 設計工具工具箱中控制項應該出現在其中的群組標籤。 需要有 `VSCategory`，控制項才會出現在工具箱中。
- *blend_category*：Blend 設計工具 [資產] 窗格中控制項應該出現在其中的群組標籤。 需要有 `BlendCategory`，控制項才會出現在 [資產] 中。
- *type_full_name_n*：每個控制項的完整名稱，包含命名空間 (例如 `ManagedPackage.MyCustomControl`)。 請注意，點格式適用於 Managed 和原生類型。

在更進階的情況下，您也可以在單一套件包含多個控制項組件時，於 `<FileList>` 內包含多個 `<File>` 項目。 如果您想要將您的控制項組織成不同的類別，則也可以在單一 `<File>` 內有多個 `<ToolboxItems>` 節點。

在下列範例中，`ManagedPackage.winmd` 中所實作的控制項會出現在 Visual Studio 和 Blend 的 [Managed Package] \(Managed 套件) 群組中，而且 “MyCustomControl” 會出現在該群組中。 所有這些名稱都是任意的。

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![在 Visual Studio 中出現的範例控制項](media/UWP-control-vs-toolbox.png)

![在 Blend 中出現的範例控制項](media/UWP-control-blend-assets.png)

> [!Note]
> 您必須明確指定想要在工具箱/[資產] 窗格中看到的每個控制項。 請確保以 `Namespace.ControlName` 格式指定它們。

## <a name="add-custom-icons-to-your-controls"></a>將自訂圖示新增至控制項

若要在工具箱/資產窗格中顯示自訂圖示，請將影像新增至專案或名為 “Namespace.ControlName.extension” 的對應 `design.dll` 專案，並將建置動作新增至 [內嵌資源]。 支援的格式為 `.png`、`.jpg`、`.jpeg`、`.gif` 和 `.bmp`。 建議的影像大小為 64 x 64 個像素。

在下列範例中，專案會包含名為 “ManagedPackage.MyCustomControl.png” 的影像檔。

![在專案中設定自訂圖示](media/UWP-control-custom-icon.png)

> [!Note]
> 對於原生控制項，您必須將圖示當成資源放至 `design.dll` 專案中。

## <a name="support-specific-windows-platform-versions"></a>支援特定的 Windows 平台版本

UWP 套件的 TargetPlatformVersion (TPV) 和 TargetPlatformMinVersion (TPMinV) 會定義可安裝應用程式之 OS 版本的上限和下限。 TPV 進一步指定用來建置應用程式的 SDK 版本。 撰寫 UWP 套件時，請留意這些屬性：在應用程式中所定義平台版本界限外部使用 API，會導致組建失敗，或應用程式在執行階段失敗。

例如，假設您已將控制項套件的 TPMinV 設定為 Windows 10 Anniversary Edition (10.0；組建 14393)，因此想要確保符合該下限的 UWP 專案僅使用該套件。 若要允許 `project.json` UWP 專案使用您的套件，您必須使用下列資料夾名稱來封裝控制項：

```
\lib\uap10.0\*
\ref\uap10.0\*
```

若要強制執行適當的 TPMinV 檢查，請建立 [MSBuild 目標檔案](/visualstudio/msbuild/msbuild-targets)，並將它封裝在組建資料夾下方 (將 "your_assembly_name" 取代為特定組件的名稱)：

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

以下範例是目標檔案的內容：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>新增設計階段支援

若要設定在屬性偵測器中顯示控制項屬性、新增自訂裝飾項等等，請適當地將 `design.dll` 檔案放在目標平台的 `lib\<platform>\Design` 資料夾內。 此外，為了確保**[編輯範本 > 編輯複本](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**功能正常運作，您必須包含 `Generic.xaml` 以及它在 `<AssemblyName>\Themes` 資料夾中所合併的任何資源字典  (此檔案不會影響控制項的執行階段行為)。


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> 控制屬性預設會顯示在屬性偵測器的 [其他] 類別下方。


## <a name="use-strings-and-resources"></a>使用字串和資源

您可以在套件中內嵌控制項或取用 UWP 專案可使用的字串資源 (`.resw`)，並將 `.resw` 檔案的 [建置動作] 屬性設定為 [PRIResource]。

如需範例，請參閱 ExtensionSDKasNuGetPackage 範例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。

## <a name="package-content-such-as-images"></a>套件內容 (例如影像)

封裝控制項或取用 UWP 專案可使用的內容 (例如影像)。 如下在 `lib\uap10.0.14393.0` 資料夾中新增這些檔案 ("your_assembly_name" 應該再次符合您的特定控制項)：

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

您也可以編寫 [MSBuild 目標檔案](/visualstudio/msbuild/msbuild-targets)，以確保將資產複製至取用專案的輸出資料夾：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>另請參閱

- [建立 UWP 套件](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage 範例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
