---
title: 建立通用 Windows 平台的 NuGet 套件
description: 使用中C#通用 Windows 平臺的 Windows 執行階段元件建立 NuGet 套件的端對端逐步解說。
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231802"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="fe325-103">建立 UWP 套件（C#）</span><span class="sxs-lookup"><span data-stu-id="fe325-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="fe325-104">[通用 Windows 平台 (UWP)](/windows/uwp) 會為每個執行 Windows 10 的裝置提供通用應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="fe325-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="fe325-105">在此模型內，UWP 應用程式可以呼叫所有裝置通用的 WinRT API，也可以呼叫應用程式執行所在裝置系列特有的 API (包含 Win32 和 .NET)。</span><span class="sxs-lookup"><span data-stu-id="fe325-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="fe325-106">在本逐步解說中，您會使用可C#用於 Managed 和原生專案的 UWP 元件（包括 XAML 控制項）來建立 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="fe325-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe325-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fe325-107">Prerequisites</span></span>

1. <span data-ttu-id="fe325-108">Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="fe325-108">Visual Studio 2019.</span></span> <span data-ttu-id="fe325-109">從[visualstudio.com](https://www.visualstudio.com/)免費安裝2019社區版本;您也可以使用 Professional 和 Enterprise edition。</span><span class="sxs-lookup"><span data-stu-id="fe325-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="fe325-110">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="fe325-110">NuGet CLI.</span></span> <span data-ttu-id="fe325-111">從 `nuget.exe`nuget.org/downloads[ 下載最新版的 ](https://nuget.org/downloads)，並將它儲存至您選擇的位置 (直接下載為 `.exe`)。</span><span class="sxs-lookup"><span data-stu-id="fe325-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="fe325-112">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="fe325-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="fe325-113">[其他詳細資訊](/nuget/reference/nuget-exe-cli-reference#windows)。</span><span class="sxs-lookup"><span data-stu-id="fe325-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="fe325-114">建立 UWP Windows 執行階段元件</span><span class="sxs-lookup"><span data-stu-id="fe325-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="fe325-115">在 Visual Studio 中，選擇 [檔案 **> 新增 > 專案**]，搜尋 "uwp c #"，選取 [ **Windows 執行階段元件（通用 Windows）** ] 範本，按 [下一步]，將名稱變更為 ImageEnhancer，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="fe325-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="fe325-116">當系統出現提示時，請接受目標版本和最低版本的預設值。</span><span class="sxs-lookup"><span data-stu-id="fe325-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![建立新 UWP Windows 執行階段元件專案](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="fe325-118">以滑鼠右鍵按一下方案總管中的專案，選取 [**加入 > 新增專案**]，選取 [樣板**化控制項**]，將名稱變更為 AwesomeImageControl.cs，然後按一下 [**新增**]：</span><span class="sxs-lookup"><span data-stu-id="fe325-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![將新的 XAML 樣板化控制項項目新增至專案](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="fe325-120">以滑鼠右鍵按一下方案總管，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="fe325-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="fe325-121">在 [屬性] 頁面中，選擇 [**組建**] 索引標籤並啟用**XML 檔**檔：</span><span class="sxs-lookup"><span data-stu-id="fe325-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![將 [產生 XML 文件檔] 設定為 [是]](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="fe325-123">以滑鼠右鍵按一下*方案*，選取 [**批次組建**]，檢查對話方塊中的五個組建方塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fe325-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="fe325-124">這確保當您執行建置時，會為 Windows 所支援的每個目標系統產生一組完整成品。</span><span class="sxs-lookup"><span data-stu-id="fe325-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![批次建置](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="fe325-126">在 [批次建置] 對話方塊中，按一下 [建置] 確認專案，並建立 NuGet 套件所需的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="fe325-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="fe325-127">在本逐步解說中，您將偵錯成品用於套件。</span><span class="sxs-lookup"><span data-stu-id="fe325-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="fe325-128">針對非偵錯套件，請改為檢查 [批次建置] 對話方塊中的 [發行] 選項，並參照所遵循步驟中產生的發行資料夾。</span><span class="sxs-lookup"><span data-stu-id="fe325-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="fe325-129">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="fe325-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="fe325-130">若要建立初始 `.nuspec` 檔案，請執行下列三個步驟。</span><span class="sxs-lookup"><span data-stu-id="fe325-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="fe325-131">下列各節接著會引導您完成其他必要更新。</span><span class="sxs-lookup"><span data-stu-id="fe325-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="fe325-132">開啟命令提示字元，並巡覽至包含 `ImageEnhancer.csproj` 的資料夾 (這是低於方案檔一階的子資料夾)。</span><span class="sxs-lookup"><span data-stu-id="fe325-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="fe325-133">執行[`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec)命令以產生 `ImageEnhancer.nuspec` （檔案的名稱取自 `.csroj` 檔案的名稱）：</span><span class="sxs-lookup"><span data-stu-id="fe325-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="fe325-134">在編輯器中開啟 `ImageEnhancer.nuspec`，然後進行更新使其符合下列內容，並使用適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="fe325-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="fe325-135">請勿保留任何 $propertyName $ 值。</span><span class="sxs-lookup"><span data-stu-id="fe325-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="fe325-136">尤其是在整個 nuget.org 中，`<id>` 值必須為唯一 (請參閱[建立套件](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="fe325-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="fe325-137">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fe325-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="fe325-138">針對公眾使用而建置的套件，請特別注意 `<tags>` 項目，因為這些標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="fe325-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="fe325-139">將 Windows 中繼資料新增至套件</span><span class="sxs-lookup"><span data-stu-id="fe325-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="fe325-140">Windows 執行階段元件需要描述其所有公開可用類型的中繼資料，讓其他應用程式和程式庫可以使用元件。</span><span class="sxs-lookup"><span data-stu-id="fe325-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="fe325-141">此中繼資料包含在 .winmd 檔案中，而此檔案是在您編譯專案時建立，並且必須併入 NuGet 套件中。</span><span class="sxs-lookup"><span data-stu-id="fe325-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="fe325-142">具有 IntelliSense 資料的 XML 檔案也會在相同的時間建置，同時應該予以包含。</span><span class="sxs-lookup"><span data-stu-id="fe325-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="fe325-143">將下列 `<files>` 節點新增至 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="fe325-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="fe325-144">新增 XAML 內容</span><span class="sxs-lookup"><span data-stu-id="fe325-144">Adding XAML content</span></span>

<span data-ttu-id="fe325-145">若要包含 XAML 控制項與您的元件，您需要新增包含控制項的預設範本 (如專案範本所產生)。</span><span class="sxs-lookup"><span data-stu-id="fe325-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="fe325-146">在 `<files>` 區段中也包含這項內容：</span><span class="sxs-lookup"><span data-stu-id="fe325-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="fe325-147">新增原生實作程式庫</span><span class="sxs-lookup"><span data-stu-id="fe325-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="fe325-148">在您的元件中，ImageEnhancer 類型的核心邏輯是在機器碼中，此程式碼包含在針對每個目標執行時間（ARM、ARM64、x86 和 x64）產生的各種 `ImageEnhancer.winmd` 元件中。</span><span class="sxs-lookup"><span data-stu-id="fe325-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="fe325-149">若要將這些併入套件中，請在 `<files>` 區段和其相關聯 .pri 資源檔中參考它們：</span><span class="sxs-lookup"><span data-stu-id="fe325-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="fe325-150">最終 .nuspec</span><span class="sxs-lookup"><span data-stu-id="fe325-150">Final .nuspec</span></span>

<span data-ttu-id="fe325-151">最終 `.nuspec` 檔案現在看起來應該如下所示，並且應該將 YOUR_NAME 取代為適當值：</span><span class="sxs-lookup"><span data-stu-id="fe325-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="fe325-152">封裝元件</span><span class="sxs-lookup"><span data-stu-id="fe325-152">Package the component</span></span>

<span data-ttu-id="fe325-153">透過完整的 `.nuspec` 參考您需要包含在封裝中的所有檔案，您就可以執行[`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack)命令：</span><span class="sxs-lookup"><span data-stu-id="fe325-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="fe325-154">這會產生 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="fe325-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="fe325-155">在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="fe325-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![顯示 ImageEnhancer 套件的 NuGet 套件總管](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="fe325-157">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="fe325-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="fe325-158">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="fe325-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="fe325-159">若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="fe325-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="fe325-160">相關主題</span><span class="sxs-lookup"><span data-stu-id="fe325-160">Related topics</span></span>

- [<span data-ttu-id="fe325-161">.nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="fe325-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="fe325-162">符號套件</span><span class="sxs-lookup"><span data-stu-id="fe325-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="fe325-163">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="fe325-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="fe325-164">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="fe325-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fe325-165">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="fe325-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="fe325-166">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="fe325-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
