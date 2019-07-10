---
title: 如何使用 NuGet 封裝 UI 控制項
description: 如何建立包含 UWP 或 WPF 控制項的 NuGet 套件，包含 Visual Studio 和 Blend 設計工具的必要中繼資料和支援檔案。
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 522dbbb2a39eb1cb6f0d23f39a48158b07c9076d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426858"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="c6071-103">建立 UI 控制項作為 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c6071-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="c6071-104">自 Visual Studio 2017 開始，您可利用 NuGet 套件所傳遞的 UWP 和 WPF 控制項新增功能。</span><span class="sxs-lookup"><span data-stu-id="c6071-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="c6071-105">本指南會使用 [ExtensionSDKasNuGetPackage 範例](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)，在 UWP 控制項內容中，逐步介紹這些功能。</span><span class="sxs-lookup"><span data-stu-id="c6071-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="c6071-106">除非另外提及，否則所述內容也適用於 WPF 控制項。</span><span class="sxs-lookup"><span data-stu-id="c6071-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6071-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="c6071-107">Prerequisites</span></span>

1. <span data-ttu-id="c6071-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6071-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="c6071-109">了解如何[建立 UWP 套件](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="c6071-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="c6071-110">產生程式庫配置</span><span class="sxs-lookup"><span data-stu-id="c6071-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="c6071-111">這僅適用於 UWP 控制項。</span><span class="sxs-lookup"><span data-stu-id="c6071-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="c6071-112">設定 `GenerateLibraryLayout` 屬性可確保專案建置輸出以可供封裝的配置來產生，而不需要 nuspec 中的個別檔案項目。</span><span class="sxs-lookup"><span data-stu-id="c6071-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="c6071-113">從專案屬性中，移至 [建置] 索引標籤並選取 [產生程式庫配置] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c6071-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="c6071-114">這將會修改專案檔，並將目前所選取的組建組態和平台的 `GenerateLibraryLayout` 旗標設定成 true。</span><span class="sxs-lookup"><span data-stu-id="c6071-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="c6071-115">或者，編輯專案檔，以將 `<GenerateLibraryLayout>true</GenerateLibraryLayout>` 新增至第一個無條件屬性群組。</span><span class="sxs-lookup"><span data-stu-id="c6071-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="c6071-116">這樣將會套用屬性，而不論組建組態和平台為何。</span><span class="sxs-lookup"><span data-stu-id="c6071-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="c6071-117">新增 XAML 控制項的工具箱/資產窗格支援</span><span class="sxs-lookup"><span data-stu-id="c6071-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="c6071-118">若要讓 XAML 控制項出現在 Visual Studio 的 XAML 設計工具工具箱中以及 Blend 的 [資產] 索引標籤中，請在套件專案的 `tools` 資料夾根中建立 `VisualStudioToolsManifest.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6071-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="c6071-119">如果您不需要控制項出現在工具箱或 [資產] 窗格中，則不需要此檔案。</span><span class="sxs-lookup"><span data-stu-id="c6071-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="c6071-120">該檔案的結構如下：</span><span class="sxs-lookup"><span data-stu-id="c6071-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="c6071-121">其中：</span><span class="sxs-lookup"><span data-stu-id="c6071-121">where:</span></span>

- <span data-ttu-id="c6071-122">*your_package_file*：您控制檔案的名稱，例如 `ManagedPackage.winmd` ("ManagedPackage" 是用於此範例的任意名稱，沒有任何其他意義)。</span><span class="sxs-lookup"><span data-stu-id="c6071-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="c6071-123">*vs_category*：群組標籤，Visual Studio 設計工具工具箱控制項應該出現在此群組中。</span><span class="sxs-lookup"><span data-stu-id="c6071-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="c6071-124">需要有 `VSCategory`，控制項才會出現在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="c6071-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="c6071-125">*blend_category*：群組標籤，Blend 設計工具 [資產] 窗格控制項應該出現在此群組。</span><span class="sxs-lookup"><span data-stu-id="c6071-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="c6071-126">需要有 `BlendCategory`，控制項才會出現在 [資產] 中。</span><span class="sxs-lookup"><span data-stu-id="c6071-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="c6071-127">*type_full_name_n*：每個控制項的完整名稱，包含命名空間，例如 `ManagedPackage.MyCustomControl`。</span><span class="sxs-lookup"><span data-stu-id="c6071-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="c6071-128">請注意，點格式適用於 Managed 和原生類型。</span><span class="sxs-lookup"><span data-stu-id="c6071-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="c6071-129">在更進階的情況下，您也可以在單一套件包含多個控制項組件時，於 `<FileList>` 內包含多個 `<File>` 項目。</span><span class="sxs-lookup"><span data-stu-id="c6071-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="c6071-130">如果您想要將您的控制項組織成不同的類別，則也可以在單一 `<File>` 內有多個 `<ToolboxItems>` 節點。</span><span class="sxs-lookup"><span data-stu-id="c6071-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="c6071-131">在下列範例中，`ManagedPackage.winmd` 中所實作的控制項會出現在 Visual Studio 和 Blend 的 [Managed Package] (Managed 套件) 群組中，而且 “MyCustomControl” 會出現在該群組中。</span><span class="sxs-lookup"><span data-stu-id="c6071-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="c6071-132">所有這些名稱都是任意的。</span><span class="sxs-lookup"><span data-stu-id="c6071-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="c6071-135">您必須明確指定想要在工具箱/[資產] 窗格中看到的每個控制項。</span><span class="sxs-lookup"><span data-stu-id="c6071-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="c6071-136">請確保以 `Namespace.ControlName` 格式指定它們。</span><span class="sxs-lookup"><span data-stu-id="c6071-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="c6071-137">將自訂圖示新增至控制項</span><span class="sxs-lookup"><span data-stu-id="c6071-137">Add custom icons to your controls</span></span>

<span data-ttu-id="c6071-138">若要在工具箱/資產窗格中顯示自訂圖示，請將影像新增至專案或名為 “Namespace.ControlName.extension” 的對應 `design.dll` 專案，並將建置動作新增至 [內嵌資源]。</span><span class="sxs-lookup"><span data-stu-id="c6071-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="c6071-139">您也必須確定關聯的 `AssemblyInfo.cs` 指定 ProvideMetadata 屬性 - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`。</span><span class="sxs-lookup"><span data-stu-id="c6071-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="c6071-140">請參閱此[範例](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)。</span><span class="sxs-lookup"><span data-stu-id="c6071-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="c6071-141">支援的格式為 `.png`、`.jpg`、`.jpeg`、`.gif` 和 `.bmp`。</span><span class="sxs-lookup"><span data-stu-id="c6071-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="c6071-142">建議的格式為 16 x 16 像素的 BMP24。</span><span class="sxs-lookup"><span data-stu-id="c6071-142">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![工具箱圖示範例](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="c6071-144">執行階段會更換粉紅色背景。</span><span class="sxs-lookup"><span data-stu-id="c6071-144">The pink background is replaced at runtime.</span></span> <span data-ttu-id="c6071-145">變更 Visual Studio 佈景主題時，圖示將會更換顏色，且應會出現背景顏色。</span><span class="sxs-lookup"><span data-stu-id="c6071-145">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="c6071-146">如需詳細資訊，請參考 [Visual Studio 的映像與圖示](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="c6071-146">For more information, please reference [Images and Icons for Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="c6071-147">在下列範例中，專案會包含名為 “ManagedPackage.MyCustomControl.png” 的影像檔。</span><span class="sxs-lookup"><span data-stu-id="c6071-147">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![在專案中設定自訂圖示](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="c6071-149">對於原生控制項，您必須將圖示當成資源放至 `design.dll` 專案中。</span><span class="sxs-lookup"><span data-stu-id="c6071-149">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="c6071-150">支援特定的 Windows 平台版本</span><span class="sxs-lookup"><span data-stu-id="c6071-150">Support specific Windows platform versions</span></span>

<span data-ttu-id="c6071-151">UWP 套件的 TargetPlatformVersion (TPV) 和 TargetPlatformMinVersion (TPMinV) 會定義可安裝應用程式之 OS 版本的上限和下限。</span><span class="sxs-lookup"><span data-stu-id="c6071-151">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="c6071-152">TPV 進一步指定用來建置應用程式的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="c6071-152">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="c6071-153">撰寫 UWP 套件時，請留意這些屬性：在應用程式中所定義平台版本界限外部使用 API，會導致組建失敗，或應用程式在執行階段失敗。</span><span class="sxs-lookup"><span data-stu-id="c6071-153">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="c6071-154">例如，假設您已將控制項套件的 TPMinV 設定為 Windows 10 Anniversary Edition (10.0；組建 14393)，因此想要確保只有符合該下限的 UWP 專案會取用該套件。</span><span class="sxs-lookup"><span data-stu-id="c6071-154">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="c6071-155">若要允許 UWP 專案使用您的套件，您必須使用下列資料夾名稱來封裝控制項：</span><span class="sxs-lookup"><span data-stu-id="c6071-155">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="c6071-156">NuGet 會自動檢查取用專案的 TPMinV。如果低於 Windows 10 Anniversary Edition (10.0；組建 14393)，將無法安裝</span><span class="sxs-lookup"><span data-stu-id="c6071-156">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="c6071-157">若為 WPF，假設想要讓 WPF 控制項套件供目標為 .NET Framework v4.6.1 或更高版本的專案取用。</span><span class="sxs-lookup"><span data-stu-id="c6071-157">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="c6071-158">若要強制這麼做，必須使用以下資料夾名稱來封裝控制項：</span><span class="sxs-lookup"><span data-stu-id="c6071-158">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="c6071-159">新增設計階段支援</span><span class="sxs-lookup"><span data-stu-id="c6071-159">Add design-time support</span></span>

<span data-ttu-id="c6071-160">若要設定在屬性偵測器中顯示控制項屬性、新增自訂裝飾項等等，請適當地將 `design.dll` 檔案放在目標平台的 `lib\uap10.0.14393\Design` 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="c6071-160">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="c6071-161">此外，為了確保 [[編輯範本] > [編輯複本]](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)  功能正常運作，您必須在 `<your_assembly_name>\Themes` 資料夾中包含 `Generic.xaml` 及其合併的任何資源目錄 (同樣使用您實際的組件名稱)。</span><span class="sxs-lookup"><span data-stu-id="c6071-161">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="c6071-162">(此檔案不會影響控制項的執行階段行為)。資料夾結構會因此出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c6071-162">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="c6071-163">對於 WPF，請從範例中想要讓 WPF 控制項套件供目標為 .NET Framework v4.6.1 或更高版本的專案取用之處，繼續進行範例：</span><span class="sxs-lookup"><span data-stu-id="c6071-163">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="c6071-164">控制屬性預設會顯示在屬性偵測器的 [其他] 類別下方。</span><span class="sxs-lookup"><span data-stu-id="c6071-164">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="c6071-165">使用字串和資源</span><span class="sxs-lookup"><span data-stu-id="c6071-165">Use strings and resources</span></span>

<span data-ttu-id="c6071-166">您可以在套件中內嵌控制項或取用 UWP 專案可使用的字串資源 (`.resw`)，並將 `.resw` 檔案的 [建置動作]  屬性設定為 [PRIResource]  。</span><span class="sxs-lookup"><span data-stu-id="c6071-166">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="c6071-167">如需範例，請參閱 ExtensionSDKasNuGetPackage 範例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。</span><span class="sxs-lookup"><span data-stu-id="c6071-167">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="c6071-168">這僅適用於 UWP 控制項。</span><span class="sxs-lookup"><span data-stu-id="c6071-168">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="c6071-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c6071-169">See also</span></span>

- [<span data-ttu-id="c6071-170">建立 UWP 套件</span><span class="sxs-lookup"><span data-stu-id="c6071-170">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="c6071-171">ExtensionSDKasNuGetPackage 範例</span><span class="sxs-lookup"><span data-stu-id="c6071-171">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
