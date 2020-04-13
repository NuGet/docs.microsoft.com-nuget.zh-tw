---
title: 建立通用 Windows 平台的 NuGet 套件
description: 使用 C# 中通用 Windows 平臺的 Windows 執行時元件創建 NuGet 套件的端到端演練。
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231802"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="2d457-103">建立 UWP 套件 (C#)</span><span class="sxs-lookup"><span data-stu-id="2d457-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="2d457-104">[通用 Windows 平台 (UWP)](/windows/uwp) 會為每個執行 Windows 10 的裝置提供通用應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="2d457-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="2d457-105">在此模型內，UWP 應用程式可以呼叫所有裝置通用的 WinRT API，也可以呼叫應用程式執行所在裝置系列特有的 API (包含 Win32 和 .NET)。</span><span class="sxs-lookup"><span data-stu-id="2d457-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="2d457-106">在本演練中,您將創建一個帶有 C# UWP 元件(包括 XAML 控制件)的 NuGet 套件,該元件可用於託管專案和本機專案。</span><span class="sxs-lookup"><span data-stu-id="2d457-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d457-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d457-107">Prerequisites</span></span>

1. <span data-ttu-id="2d457-108">Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="2d457-108">Visual Studio 2019.</span></span> <span data-ttu-id="2d457-109">安裝2019年社區版免費從[visualstudio.com;](https://www.visualstudio.com/)您也可以使用專業版和企業版。</span><span class="sxs-lookup"><span data-stu-id="2d457-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="2d457-110">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="2d457-110">NuGet CLI.</span></span> <span data-ttu-id="2d457-111">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 `nuget.exe`，並將它儲存至您選擇的位置 (直接下載為 `.exe`)。</span><span class="sxs-lookup"><span data-stu-id="2d457-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="2d457-112">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="2d457-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="2d457-113">[其他詳細資訊](/nuget/reference/nuget-exe-cli-reference#windows)。</span><span class="sxs-lookup"><span data-stu-id="2d457-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="2d457-114">建立 UWP Windows 執行階段元件</span><span class="sxs-lookup"><span data-stu-id="2d457-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="2d457-115">在可視化工作室中,選擇 **「檔>」新>專案**「,搜索」uwp c#",選擇**Windows 執行時元件(通用 Windows)** 樣本,按一下下一個,將名稱更改為 Image 增強器,然後單擊"創建"。</span><span class="sxs-lookup"><span data-stu-id="2d457-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="2d457-116">當系統出現提示時，請接受目標版本和最低版本的預設值。</span><span class="sxs-lookup"><span data-stu-id="2d457-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![建立新 UWP Windows 執行階段元件專案](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="2d457-118">右鍵按一下解決方案資源管理員的項目,選擇 **'新增>新專案**',選擇 **「樣本化控制件**」,將名稱更改為AwesomeImageControl.cs,然後按下「**新增**:</span><span class="sxs-lookup"><span data-stu-id="2d457-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![將新的 XAML 樣板化控制項項目新增至專案](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="2d457-120">右鍵單擊解決方案資源管理器中的專案並選擇 **「屬性」。**</span><span class="sxs-lookup"><span data-stu-id="2d457-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="2d457-121">在「屬性」 頁中,選擇 **「產生**」選項卡並開啟**XML 文件檔**:</span><span class="sxs-lookup"><span data-stu-id="2d457-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![將 [產生 XML 文件檔] 設定為 [是]](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="2d457-123">右鍵按一下*解決方案*,選擇**批次處理生成**,選擇對話框中的五個生成框,如下所示。</span><span class="sxs-lookup"><span data-stu-id="2d457-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="2d457-124">這確保當您執行建置時，會為 Windows 所支援的每個目標系統產生一組完整成品。</span><span class="sxs-lookup"><span data-stu-id="2d457-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![批次建置](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="2d457-126">在 [批次建置] 對話方塊中，按一下 [建置]\*\*\*\* 確認專案，並建立 NuGet 套件所需的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="2d457-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="2d457-127">在本逐步解說中，您將偵錯成品用於套件。</span><span class="sxs-lookup"><span data-stu-id="2d457-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="2d457-128">針對非偵錯套件，請改為檢查 [批次建置] 對話方塊中的 [發行] 選項，並參照所遵循步驟中產生的發行資料夾。</span><span class="sxs-lookup"><span data-stu-id="2d457-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="2d457-129">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="2d457-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="2d457-130">若要建立初始 `.nuspec` 檔案，請執行下列三個步驟。</span><span class="sxs-lookup"><span data-stu-id="2d457-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="2d457-131">下列各節接著會引導您完成其他必要更新。</span><span class="sxs-lookup"><span data-stu-id="2d457-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="2d457-132">開啟命令提示字元，並巡覽至包含 `ImageEnhancer.csproj` 的資料夾 (這是低於方案檔一階的子資料夾)。</span><span class="sxs-lookup"><span data-stu-id="2d457-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="2d457-133">執行要[`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec)產生`ImageEnhancer.nuspec`的指令(檔案的名稱取`.csroj`自 檔案的名稱):</span><span class="sxs-lookup"><span data-stu-id="2d457-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="2d457-134">在編輯器中開啟 `ImageEnhancer.nuspec`，更新它使符合下列內容，以適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="2d457-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="2d457-135">不要留下任何$propertyName$ 值。</span><span class="sxs-lookup"><span data-stu-id="2d457-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="2d457-136">尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="2d457-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="2d457-137">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="2d457-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="2d457-138">針對公眾使用而建置的套件，請特別注意 `<tags>` 項目，因為這些標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="2d457-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="2d457-139">將 Windows 中繼資料新增至套件</span><span class="sxs-lookup"><span data-stu-id="2d457-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="2d457-140">Windows 執行階段元件需要描述其所有公開可用類型的中繼資料，讓其他應用程式和程式庫可以使用元件。</span><span class="sxs-lookup"><span data-stu-id="2d457-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="2d457-141">此中繼資料包含在 .winmd 檔案中，而此檔案是在您編譯專案時建立，並且必須併入 NuGet 套件中。</span><span class="sxs-lookup"><span data-stu-id="2d457-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="2d457-142">具有 IntelliSense 資料的 XML 檔案也會在相同的時間建置，同時應該予以包含。</span><span class="sxs-lookup"><span data-stu-id="2d457-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="2d457-143">將下列 `<files>` 節點新增至 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="2d457-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="2d457-144">新增 XAML 內容</span><span class="sxs-lookup"><span data-stu-id="2d457-144">Adding XAML content</span></span>

<span data-ttu-id="2d457-145">若要包含 XAML 控制項與您的元件，您需要新增包含控制項的預設範本 (如專案範本所產生)。</span><span class="sxs-lookup"><span data-stu-id="2d457-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="2d457-146">在 `<files>` 區段中也包含這項內容：</span><span class="sxs-lookup"><span data-stu-id="2d457-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="2d457-147">新增原生實作程式庫</span><span class="sxs-lookup"><span data-stu-id="2d457-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="2d457-148">在元件中,Image增強器類型的核心邏輯位於本機代碼中,該代碼包含在為每個目標運行時生成的各種`ImageEnhancer.winmd`程式集(ARM、ARM64、x86 和 x64)中。</span><span class="sxs-lookup"><span data-stu-id="2d457-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="2d457-149">若要將這些併入套件中，請在 `<files>` 區段和其相關聯 .pri 資源檔中參考它們：</span><span class="sxs-lookup"><span data-stu-id="2d457-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="2d457-150">最終 .nuspec</span><span class="sxs-lookup"><span data-stu-id="2d457-150">Final .nuspec</span></span>

<span data-ttu-id="2d457-151">最終 `.nuspec` 檔案現在看起來應該如下所示，並且應該將 YOUR_NAME 取代為適當值：</span><span class="sxs-lookup"><span data-stu-id="2d457-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="2d457-152">封裝元件</span><span class="sxs-lookup"><span data-stu-id="2d457-152">Package the component</span></span>

<span data-ttu-id="2d457-153">完成`.nuspec`參考套件中需要包含的所有檔案後,即可執行[`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack)以下 指令:</span><span class="sxs-lookup"><span data-stu-id="2d457-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="2d457-154">這會產生 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="2d457-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="2d457-155">在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="2d457-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![顯示 ImageEnhancer 套件的 NuGet 套件總管](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="2d457-157">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="2d457-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="2d457-158">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="2d457-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="2d457-159">若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="2d457-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="2d457-160">相關主題</span><span class="sxs-lookup"><span data-stu-id="2d457-160">Related topics</span></span>

- [<span data-ttu-id="2d457-161">.nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="2d457-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="2d457-162">符號包</span><span class="sxs-lookup"><span data-stu-id="2d457-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="2d457-163">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="2d457-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="2d457-164">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="2d457-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2d457-165">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="2d457-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="2d457-166">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="2d457-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
