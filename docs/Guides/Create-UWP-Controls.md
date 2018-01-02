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
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="c1016-104">建立 UWP 控制項作為 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c1016-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="c1016-105">使用 Visual Studio 2017，您可以利用以 NuGet 套件傳遞之 UWP 控制項的新增功能。</span><span class="sxs-lookup"><span data-stu-id="c1016-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="c1016-106">本指南會逐步引導您使用 [ExtensionSDKasNuGetPackage 範例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)來使用這些功能。</span><span class="sxs-lookup"><span data-stu-id="c1016-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="c1016-107">必要條件：</span><span class="sxs-lookup"><span data-stu-id="c1016-107">Pre-requisites:</span></span>

1.  <span data-ttu-id="c1016-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c1016-108">Visual Studio 2017</span></span>
1.  <span data-ttu-id="c1016-109">了解如何[建立 UWP 套件](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="c1016-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="c1016-110">新增 XAML 控制項的工具箱/資產窗格支援</span><span class="sxs-lookup"><span data-stu-id="c1016-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="c1016-111">若要讓 XAML 控制項出現在 Visual Studio 的 XAML 設計工具工具箱中以及 Blend 的 [資產] 索引標籤中，請在套件專案的 `tools` 資料夾根中建立 `VisualStudioToolsManifest.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c1016-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="c1016-112">如果您不需要控制項出現在工具箱或 [資產] 窗格中，則不需要此檔案。</span><span class="sxs-lookup"><span data-stu-id="c1016-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

<span data-ttu-id="c1016-113">該檔案的結構如下：</span><span class="sxs-lookup"><span data-stu-id="c1016-113">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="c1016-114">其中：</span><span class="sxs-lookup"><span data-stu-id="c1016-114">where:</span></span>

- <span data-ttu-id="c1016-115">*your_package_file*：您控制檔案的名稱，例如 `ManagedPackage.winmd` ("ManagedPackage" 是用於此範例的任意名稱，沒有任何其他意義)。</span><span class="sxs-lookup"><span data-stu-id="c1016-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="c1016-116">*vs_category*：Visual Studio 設計工具工具箱中控制項應該出現在其中的群組標籤。</span><span class="sxs-lookup"><span data-stu-id="c1016-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="c1016-117">需要有 `VSCategory`，控制項才會出現在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="c1016-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="c1016-118">*blend_category*：Blend 設計工具 [資產] 窗格中控制項應該出現在其中的群組標籤。</span><span class="sxs-lookup"><span data-stu-id="c1016-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="c1016-119">需要有 `BlendCategory`，控制項才會出現在 [資產] 中。</span><span class="sxs-lookup"><span data-stu-id="c1016-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="c1016-120">*type_full_name_n*：每個控制項的完整名稱，包含命名空間 (例如 `ManagedPackage.MyCustomControl`)。</span><span class="sxs-lookup"><span data-stu-id="c1016-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="c1016-121">請注意，點格式適用於 Managed 和原生類型。</span><span class="sxs-lookup"><span data-stu-id="c1016-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="c1016-122">在更進階的情況下，您也可以在單一套件包含多個控制項組件時，於 `<FileList>` 內包含多個 `<File>` 項目。</span><span class="sxs-lookup"><span data-stu-id="c1016-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="c1016-123">如果您想要將您的控制項組織成不同的類別，則也可以在單一 `<File>` 內有多個 `<ToolboxItems>` 節點。</span><span class="sxs-lookup"><span data-stu-id="c1016-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="c1016-124">在下列範例中，`ManagedPackage.winmd` 中所實作的控制項會出現在 Visual Studio 和 Blend 的 [Managed Package] (Managed 套件) 群組中，而且 “MyCustomControl” 會出現在該群組中。</span><span class="sxs-lookup"><span data-stu-id="c1016-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="c1016-125">所有這些名稱都是任意的。</span><span class="sxs-lookup"><span data-stu-id="c1016-125">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="c1016-128">您必須明確指定想要在工具箱/[資產] 窗格中看到的每個控制項。</span><span class="sxs-lookup"><span data-stu-id="c1016-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="c1016-129">請確保以 `Namespace.ControlName` 格式指定它們。</span><span class="sxs-lookup"><span data-stu-id="c1016-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="c1016-130">將自訂圖示新增至控制項</span><span class="sxs-lookup"><span data-stu-id="c1016-130">Add custom icons to your controls</span></span>

<span data-ttu-id="c1016-131">若要在工具箱/資產窗格中顯示自訂圖示，請將影像新增至專案或名為 “Namespace.ControlName.extension” 的對應 `design.dll` 專案，並將建置動作新增至 [內嵌資源]。</span><span class="sxs-lookup"><span data-stu-id="c1016-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="c1016-132">支援的格式為 `.png`、`.jpg`、`.jpeg`、`.gif` 和 `.bmp`。</span><span class="sxs-lookup"><span data-stu-id="c1016-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="c1016-133">建議的影像大小為 64 x 64 個像素。</span><span class="sxs-lookup"><span data-stu-id="c1016-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="c1016-134">在下列範例中，專案會包含名為 “ManagedPackage.MyCustomControl.png” 的影像檔。</span><span class="sxs-lookup"><span data-stu-id="c1016-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![在專案中設定自訂圖示](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="c1016-136">對於原生控制項，您必須將圖示當成資源放至 `design.dll` 專案中。</span><span class="sxs-lookup"><span data-stu-id="c1016-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="c1016-137">支援特定的 Windows 平台版本</span><span class="sxs-lookup"><span data-stu-id="c1016-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="c1016-138">UWP 套件的 TargetPlatformVersion (TPV) 和 TargetPlatformMinVersion (TPMinV) 會定義可安裝應用程式之 OS 版本的上限和下限。</span><span class="sxs-lookup"><span data-stu-id="c1016-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="c1016-139">TPV 進一步指定用來建置應用程式的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="c1016-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="c1016-140">撰寫 UWP 套件時，請留意這些屬性：在應用程式中所定義平台版本界限外部使用 API，會導致組建失敗，或應用程式在執行階段失敗。</span><span class="sxs-lookup"><span data-stu-id="c1016-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="c1016-141">例如，假設您已將控制項套件的 TPMinV 設定為 Windows 10 Anniversary Edition (10.0；組建 14393)，因此想要確保符合該下限的 UWP 專案僅使用該套件。</span><span class="sxs-lookup"><span data-stu-id="c1016-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="c1016-142">若要允許 `project.json` UWP 專案使用您的套件，您必須使用下列資料夾名稱來封裝控制項：</span><span class="sxs-lookup"><span data-stu-id="c1016-142">To allow your package to be consumed by `project.json` based UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0\*
\ref\uap10.0\*
```

<span data-ttu-id="c1016-143">若要強制執行適當的 TPMinV 檢查，請建立 [MSBuild 目標檔案](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)，並將它封裝在組建資料夾下方 (將 "your_assembly_name" 取代為特定組件的名稱)：</span><span class="sxs-lookup"><span data-stu-id="c1016-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

<span data-ttu-id="c1016-144">以下範例是目標檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="c1016-144">Here is an example of what the targets file should look like:</span></span>

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

## <a name="add-design-time-support"></a><span data-ttu-id="c1016-145">新增設計階段支援</span><span class="sxs-lookup"><span data-stu-id="c1016-145">Add design-time support</span></span>

<span data-ttu-id="c1016-146">若要設定在屬性偵測器中顯示控制項屬性、新增自訂裝飾項等等，請適當地將 `design.dll` 檔案放在目標平台的 `lib\<platform>\Design` 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="c1016-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="c1016-147">此外，為了確保**[編輯範本 > 編輯複本](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**功能正常運作，您必須包含 `Generic.xaml` 以及它在 `<AssemblyName>\Themes` 資料夾中所合併的任何資源字典 </span><span class="sxs-lookup"><span data-stu-id="c1016-147">Also, to ensure that the **[Edit Template > Edit a Copy](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="c1016-148">(此檔案不會影響控制項的執行階段行為)。</span><span class="sxs-lookup"><span data-stu-id="c1016-148">(This file has no impact on the runtime behavior of a control.)</span></span>


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
> <span data-ttu-id="c1016-149">控制屬性預設會顯示在屬性偵測器的 [其他] 類別下方。</span><span class="sxs-lookup"><span data-stu-id="c1016-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>


## <a name="use-strings-and-resources"></a><span data-ttu-id="c1016-150">使用字串和資源</span><span class="sxs-lookup"><span data-stu-id="c1016-150">Use strings and resources</span></span>

<span data-ttu-id="c1016-151">您可以在套件中內嵌控制項或取用 UWP 專案可使用的字串資源 (`.resw`)，並將 `.resw` 檔案的 [建置動作] 屬性設定為 [PRIResource]。</span><span class="sxs-lookup"><span data-stu-id="c1016-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="c1016-152">如需範例，請參閱 ExtensionSDKasNuGetPackage 範例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。</span><span class="sxs-lookup"><span data-stu-id="c1016-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="c1016-153">套件內容 (例如影像)</span><span class="sxs-lookup"><span data-stu-id="c1016-153">Package content such as images</span></span>

<span data-ttu-id="c1016-154">封裝控制項或取用 UWP 專案可使用的內容 (例如影像)。</span><span class="sxs-lookup"><span data-stu-id="c1016-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="c1016-155">如下在 `lib\uap10.0.14393.0` 資料夾中新增這些檔案 ("your_assembly_name" 應該再次符合您的特定控制項)：</span><span class="sxs-lookup"><span data-stu-id="c1016-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

<span data-ttu-id="c1016-156">您也可以編寫 [MSBuild 目標檔案](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)，以確保將資產複製至取用專案的輸出資料夾：</span><span class="sxs-lookup"><span data-stu-id="c1016-156">You may also author an[MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="c1016-157">請參閱</span><span class="sxs-lookup"><span data-stu-id="c1016-157">See also</span></span>

- [<span data-ttu-id="c1016-158">建立 UWP 套件</span><span class="sxs-lookup"><span data-stu-id="c1016-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="c1016-159">ExtensionSDKasNuGetPackage 範例</span><span class="sxs-lookup"><span data-stu-id="c1016-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
