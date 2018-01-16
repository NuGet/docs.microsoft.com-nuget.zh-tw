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
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="cecbf-104">使用 Visual Studio 2015 建立 .NET Standard 套件</span><span class="sxs-lookup"><span data-stu-id="cecbf-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="cecbf-105">*適用於 NuGet 3.x。請參閱[使用 Visual Studio 2017 建立 .NET Standard 套件](../guides/create-net-standard-packages-vs2017.md)，以使用 NuGet 4.x+。*</span><span class="sxs-lookup"><span data-stu-id="cecbf-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="cecbf-106">[.NET Standard 程式庫](/dotnet/articles/standard/library)是計劃提供所有 .NET 執行階段使用的 .NET API 正式規格，因此在 .NET 生態系統中能建立較強的一致性。</span><span class="sxs-lookup"><span data-stu-id="cecbf-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="cecbf-107">.NET Standard 程式庫定義一致的 BCL (基底類別庫) API 集合，以供所有 .NET 平台實作，而不論工作負載為何。</span><span class="sxs-lookup"><span data-stu-id="cecbf-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="cecbf-108">它可讓開發人員產生可跨所有 .NET 執行階段使用的 PCL，並減少 (如果無法消除) 共用程式碼中的平台專屬條件式編譯指示詞。</span><span class="sxs-lookup"><span data-stu-id="cecbf-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="cecbf-109">本指南將引導您建立以 .NET Standard 程式庫 1.4 為目標的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="cecbf-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="cecbf-110">這對 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 都適用。</span><span class="sxs-lookup"><span data-stu-id="cecbf-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="cecbf-111">如需詳細資料，請參閱本主題下文中的 [.NET Standard 對應表](#net-standard-mapping-table)。</span><span class="sxs-lookup"><span data-stu-id="cecbf-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="cecbf-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="cecbf-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="cecbf-113">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="cecbf-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="cecbf-114">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="cecbf-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="cecbf-115">封裝元件</span><span class="sxs-lookup"><span data-stu-id="cecbf-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="cecbf-116">其他選項</span><span class="sxs-lookup"><span data-stu-id="cecbf-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="cecbf-117">.NET Standard 對應表</span><span class="sxs-lookup"><span data-stu-id="cecbf-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="cecbf-118">相關主題</span><span class="sxs-lookup"><span data-stu-id="cecbf-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="cecbf-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="cecbf-119">Pre-requisites</span></span>

1. <span data-ttu-id="cecbf-120">Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="cecbf-120">Visual Studio 2015.</span></span> <span data-ttu-id="cecbf-121">從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，當然也可以使用 Professional Edition 和 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="cecbf-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="cecbf-122">.NET Core：從 [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849) 安裝 .NET Core 以及適用於 Visual Studio 2015 的範本和其他工具。</span><span class="sxs-lookup"><span data-stu-id="cecbf-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="cecbf-123">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="cecbf-123">NuGet CLI.</span></span> <span data-ttu-id="cecbf-124">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="cecbf-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="cecbf-125">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="cecbf-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="cecbf-126">nuget.exe 本身是 CLI 工具，不是安裝程式，所以請務必從瀏覽器儲存下載的檔案，而不是執行它。</span><span class="sxs-lookup"><span data-stu-id="cecbf-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="cecbf-127">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="cecbf-127">Create the class library project</span></span>

1. <span data-ttu-id="cecbf-128">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [Windows] 節點、選取 [類別庫 (可攜式)]、將名稱變更為 AppLogger，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cecbf-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![建立新的類別庫專案](media/NetStandard-NewProject.png)

1. <span data-ttu-id="cecbf-130">在出現的 [新增可攜式類別庫] 對話方塊中，選取 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 選項。</span><span class="sxs-lookup"><span data-stu-id="cecbf-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="cecbf-131">以滑鼠右鍵按一下方案總管中的 `AppLogger (Portable)`，依序選取 [屬性] 和 [程式庫] 索引標籤，然後按一下 [目標鎖定] 區段的 [目標 .NET 平台標準]。</span><span class="sxs-lookup"><span data-stu-id="cecbf-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="cecbf-132">這會提示您進行確認，然後就可以從下拉式清單中選取 [`.NET Standard 1.4`]：</span><span class="sxs-lookup"><span data-stu-id="cecbf-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![將目標設定為 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="cecbf-134">按一下 [組建] 索引標籤，將 [組態] 變更為 `Release`，並核取 [XML 文件檔] 方塊。</span><span class="sxs-lookup"><span data-stu-id="cecbf-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="cecbf-135">將程式碼新增至元件，例如：</span><span class="sxs-lookup"><span data-stu-id="cecbf-135">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="cecbf-136">(使用版本組態) 建置專案，並確認 DLL 和 XML 檔案已產生在 bin\Release 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="cecbf-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="cecbf-137">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="cecbf-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="cecbf-138">開啟命令提示字元，巡覽至包含 `AppLogg.csproj` 資料夾的資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `AppLogger.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="cecbf-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="cecbf-139">在編輯器中開啟 `AppLogger.nuspec`，更新它使符合下列內容，以適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="cecbf-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="cecbf-140">尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="cecbf-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="cecbf-141">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="cecbf-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

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

1. <span data-ttu-id="cecbf-142">將參考組件新增至 `.nuspec` 檔案，也就是程式庫的 DLL 和 IntelliSense XML 檔案：</span><span class="sxs-lookup"><span data-stu-id="cecbf-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="cecbf-143">以滑鼠右鍵按一下解決方案，然後選取 [組建方案] 產生套件的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="cecbf-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="cecbf-144">封裝元件</span><span class="sxs-lookup"><span data-stu-id="cecbf-144">Package the component</span></span>

<span data-ttu-id="cecbf-145">只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="cecbf-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="cecbf-146">這會產生 `AppLogger.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="cecbf-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="cecbf-147">在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="cecbf-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![顯示 AppLogger 套件的 NuGet 套件總管](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="cecbf-149">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="cecbf-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="cecbf-150">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="cecbf-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="cecbf-151">若要讓其他開發人員使用您的套件，請遵循[發行套件](../create-packages/publish-a-package.md)上的指示。</span><span class="sxs-lookup"><span data-stu-id="cecbf-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="cecbf-152">請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。</span><span class="sxs-lookup"><span data-stu-id="cecbf-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="cecbf-153">在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。</span><span class="sxs-lookup"><span data-stu-id="cecbf-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="cecbf-154">其他選項</span><span class="sxs-lookup"><span data-stu-id="cecbf-154">Additional options</span></span>

<span data-ttu-id="cecbf-155">下列各節會進入建立 NuGet 套件的其他選項：</span><span class="sxs-lookup"><span data-stu-id="cecbf-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="cecbf-156">宣告相依性</span><span class="sxs-lookup"><span data-stu-id="cecbf-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="cecbf-157">支援多個目標 Framework</span><span class="sxs-lookup"><span data-stu-id="cecbf-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="cecbf-158">新增 MSBuild 的目標與 props</span><span class="sxs-lookup"><span data-stu-id="cecbf-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="cecbf-159">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="cecbf-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="cecbf-160">新增讀我檔案</span><span class="sxs-lookup"><span data-stu-id="cecbf-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="cecbf-161">宣告相依性</span><span class="sxs-lookup"><span data-stu-id="cecbf-161">Declaring dependencies</span></span>

<span data-ttu-id="cecbf-162">如有其他 NuGet 套件的任何相依性，請使用 `<group>` 項目在 `<dependencies>` 項目中列出它們。</span><span class="sxs-lookup"><span data-stu-id="cecbf-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="cecbf-163">例如，若要宣告對 NewtonSoft.Json 8.0.3 或更新版本的相依性，請新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="cecbf-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="cecbf-164">*version* 屬性的語法在此表示接受該版本 8.0.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cecbf-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="cecbf-165">若要指定不同的版本範圍，請參閱[套件版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="cecbf-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="cecbf-166">支援多個目標 Framework</span><span class="sxs-lookup"><span data-stu-id="cecbf-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="cecbf-167">假設您想要利用 .NET Standard 1.4 不提供的 .NET Framework 4.6.2 API。</span><span class="sxs-lookup"><span data-stu-id="cecbf-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="cecbf-168">您需要先使用條件式編譯或共用專案，確定程式庫相容於 .NET 4.6.2，才能執行此作業。</span><span class="sxs-lookup"><span data-stu-id="cecbf-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="cecbf-169">(在 Visual Studio 中，您可以建立 NetCore 專案、將 Framework 選項新增至多個 Framework 區段，然後建置。)然後使用簡單的慣例式工作目錄技巧建立套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cecbf-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="cecbf-170">在包含 `.nuspec` 檔案的專案根資料夾中，建立名為 `lib` 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="cecbf-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="cecbf-171">在 `lib` 中，為您想要支援的每個平台建立資料夾：</span><span class="sxs-lookup"><span data-stu-id="cecbf-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="cecbf-172">在 `.nuspec` 檔案中，在 `package` 節點下新增 `files` 節點，並使用萬用字元參考 `lib` 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="cecbf-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="cecbf-173">**注意：**不支援以慣例型工作目錄方法取代權杖，所以請使用常值取代它們：</span><span class="sxs-lookup"><span data-stu-id="cecbf-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

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

1. <span data-ttu-id="cecbf-174">使用 `nuget pack AppLogger.spec` 再次建立套件。</span><span class="sxs-lookup"><span data-stu-id="cecbf-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="cecbf-175">如需使用這項技術的詳細資料，請參閱[支援多個 .NET Framework 版本](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="cecbf-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="cecbf-176">新增 MSBuild 的目標與 props</span><span class="sxs-lookup"><span data-stu-id="cecbf-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="cecbf-177">在某些情況下，您可能想要在取用您套件的專案中新增自訂組建目標或屬性，例如在建置期間執行自訂工具或程序。</span><span class="sxs-lookup"><span data-stu-id="cecbf-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="cecbf-178">執行此作業，只要依下列步驟所述，將檔案新增至 `\build` 資料夾即可。</span><span class="sxs-lookup"><span data-stu-id="cecbf-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="cecbf-179">當 NuGet 使用 \build 檔案安裝套件時，會在指向 .targets 和 .props 檔案的專案檔中新增 MSBuild 項目。</span><span class="sxs-lookup"><span data-stu-id="cecbf-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="cecbf-180">當使用 `project.json` 時，目標不會新增至專案，但可透過 `project.lock.json` 提供。</span><span class="sxs-lookup"><span data-stu-id="cecbf-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="cecbf-181">在包含 `.nuspec` 檔案的專案資料夾中，建立名為 `build` 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="cecbf-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="cecbf-182">在 `build` 內，為每個受支援的 `build` 建立資料夾，並在這些資料夾內放置您的 `.targets` 和 `.props` 檔案：</span><span class="sxs-lookup"><span data-stu-id="cecbf-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="cecbf-183">在 `.nuspec` 檔案中，在 `package` 節點下新增 `files` 節點，並使用萬用字元參考 `build` 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="cecbf-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

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

1. <span data-ttu-id="cecbf-184">使用 `nuget pack AppLogger.nuspec` 再次建立套件。</span><span class="sxs-lookup"><span data-stu-id="cecbf-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="cecbf-185">如需其他詳細資料，請參閱[在套件中包含 MSBuild props 和目標](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)。</span><span class="sxs-lookup"><span data-stu-id="cecbf-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="cecbf-186">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="cecbf-186">Creating localized packages</span></span>

<span data-ttu-id="cecbf-187">若要建立程式庫的當地語系化版本，您可以為不同的地區設定建立個別的套件，或在單一套件內包含當地語系化資源組件。</span><span class="sxs-lookup"><span data-stu-id="cecbf-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="cecbf-188">以下示範以第二種方法建立德文和義大利文的版本：</span><span class="sxs-lookup"><span data-stu-id="cecbf-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="cecbf-189">在 `lib` 下的每個目標 Framework 資料夾內，建立每種受支援語言的資料夾，英文預設值除外。</span><span class="sxs-lookup"><span data-stu-id="cecbf-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="cecbf-190">您可以在這些資料夾中放置資源組件和當地語系化 IntelliSense XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="cecbf-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="cecbf-191">例如: </span><span class="sxs-lookup"><span data-stu-id="cecbf-191">For example:</span></span>

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

1. <span data-ttu-id="cecbf-192">在 `.nuspec` 檔案中，參考 `<files>` 節點中的這些檔案：</span><span class="sxs-lookup"><span data-stu-id="cecbf-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

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

1. <span data-ttu-id="cecbf-193">使用 `nuget pack AppLogger.nuspec` 再次建立套件。</span><span class="sxs-lookup"><span data-stu-id="cecbf-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="cecbf-194">新增讀我檔案</span><span class="sxs-lookup"><span data-stu-id="cecbf-194">Adding a readme</span></span>

<span data-ttu-id="cecbf-195">當您在套件的根目錄中包含 `readme.txt` 檔案時，Visual Studio 會在直接安裝套件時顯示它。</span><span class="sxs-lookup"><span data-stu-id="cecbf-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="cecbf-196">已安裝為相依性的套件或 .NET Core 專案不會顯示讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="cecbf-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="cecbf-197">若要這樣做，請建立您的 `readme.txt` 檔案，將它放在專案根資料夾中，並在 `.nuspec` 檔案中參考它：</span><span class="sxs-lookup"><span data-stu-id="cecbf-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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


## <a name="net-standard-mapping-table"></a><span data-ttu-id="cecbf-198">.NET Standard 對應表</span><span class="sxs-lookup"><span data-stu-id="cecbf-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="cecbf-199">平台名稱</span><span class="sxs-lookup"><span data-stu-id="cecbf-199">Platform Name</span></span> |<span data-ttu-id="cecbf-200">Alias</span><span class="sxs-lookup"><span data-stu-id="cecbf-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="cecbf-201">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="cecbf-201">.NET Standard</span></span> | <span data-ttu-id="cecbf-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="cecbf-202">netstandard</span></span>| <span data-ttu-id="cecbf-203">1.0</span><span class="sxs-lookup"><span data-stu-id="cecbf-203">1.0</span></span>| <span data-ttu-id="cecbf-204">1.1</span><span class="sxs-lookup"><span data-stu-id="cecbf-204">1.1</span></span>| <span data-ttu-id="cecbf-205">1.2</span><span class="sxs-lookup"><span data-stu-id="cecbf-205">1.2</span></span>| <span data-ttu-id="cecbf-206">1.3</span><span class="sxs-lookup"><span data-stu-id="cecbf-206">1.3</span></span>| <span data-ttu-id="cecbf-207">1.4</span><span class="sxs-lookup"><span data-stu-id="cecbf-207">1.4</span></span>| <span data-ttu-id="cecbf-208">1.5</span><span class="sxs-lookup"><span data-stu-id="cecbf-208">1.5</span></span>| <span data-ttu-id="cecbf-209">1.6</span><span class="sxs-lookup"><span data-stu-id="cecbf-209">1.6</span></span>|
|<span data-ttu-id="cecbf-210">.NET 核心</span><span class="sxs-lookup"><span data-stu-id="cecbf-210">.NET Core</span></span> | <span data-ttu-id="cecbf-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="cecbf-211">netcoreapp</span></span>| <span data-ttu-id="cecbf-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-212">&#x2192;</span></span>| <span data-ttu-id="cecbf-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-213">&#x2192;</span></span>| <span data-ttu-id="cecbf-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-214">&#x2192;</span></span>| <span data-ttu-id="cecbf-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-215">&#x2192;</span></span>| <span data-ttu-id="cecbf-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-216">&#x2192;</span></span>| <span data-ttu-id="cecbf-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-217">&#x2192;</span></span>| <span data-ttu-id="cecbf-218">1.0</span><span class="sxs-lookup"><span data-stu-id="cecbf-218">1.0</span></span>|
|<span data-ttu-id="cecbf-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="cecbf-219">.NET Framework</span></span>| <span data-ttu-id="cecbf-220">net</span><span class="sxs-lookup"><span data-stu-id="cecbf-220">net</span></span>| <span data-ttu-id="cecbf-221">4.5</span><span class="sxs-lookup"><span data-stu-id="cecbf-221">4.5</span></span>| <span data-ttu-id="cecbf-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="cecbf-222">4.5.1</span></span>| <span data-ttu-id="cecbf-223">4.6</span><span class="sxs-lookup"><span data-stu-id="cecbf-223">4.6</span></span>| <span data-ttu-id="cecbf-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="cecbf-224">4.6.1</span></span>| <span data-ttu-id="cecbf-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="cecbf-225">4.6.2</span></span>| <span data-ttu-id="cecbf-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="cecbf-226">4.6.3</span></span>|
|<span data-ttu-id="cecbf-227">Mono/Xamarin 平台</span><span class="sxs-lookup"><span data-stu-id="cecbf-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="cecbf-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-228">&#x2192;</span></span>| <span data-ttu-id="cecbf-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-229">&#x2192;</span></span>| <span data-ttu-id="cecbf-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-230">&#x2192;</span></span>| <span data-ttu-id="cecbf-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-231">&#x2192;</span></span>| <span data-ttu-id="cecbf-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-232">&#x2192;</span></span>| <span data-ttu-id="cecbf-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-233">&#x2192;</span></span>|
|<span data-ttu-id="cecbf-234">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="cecbf-234">Universal Windows Platform</span></span>| <span data-ttu-id="cecbf-235">uap</span><span class="sxs-lookup"><span data-stu-id="cecbf-235">uap</span></span>| <span data-ttu-id="cecbf-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-236">&#x2192;</span></span>| <span data-ttu-id="cecbf-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-237">&#x2192;</span></span>| <span data-ttu-id="cecbf-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-238">&#x2192;</span></span>| <span data-ttu-id="cecbf-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-239">&#x2192;</span></span>|<span data-ttu-id="cecbf-240">10.0</span><span class="sxs-lookup"><span data-stu-id="cecbf-240">10.0</span></span>|
|<span data-ttu-id="cecbf-241">Windows</span><span class="sxs-lookup"><span data-stu-id="cecbf-241">Windows</span></span>| <span data-ttu-id="cecbf-242">win</span><span class="sxs-lookup"><span data-stu-id="cecbf-242">win</span></span>| <span data-ttu-id="cecbf-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-243">&#x2192;</span></span>| <span data-ttu-id="cecbf-244">8.0</span><span class="sxs-lookup"><span data-stu-id="cecbf-244">8.0</span></span>| <span data-ttu-id="cecbf-245">8.1</span><span class="sxs-lookup"><span data-stu-id="cecbf-245">8.1</span></span>|
|<span data-ttu-id="cecbf-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="cecbf-246">Windows Phone</span></span>| <span data-ttu-id="cecbf-247">wpa</span><span class="sxs-lookup"><span data-stu-id="cecbf-247">wpa</span></span>| <span data-ttu-id="cecbf-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-248">&#x2192;</span></span>| <span data-ttu-id="cecbf-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="cecbf-249">&#x2192;</span></span>|<span data-ttu-id="cecbf-250">8.1</span><span class="sxs-lookup"><span data-stu-id="cecbf-250">8.1</span></span>|
|<span data-ttu-id="cecbf-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="cecbf-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="cecbf-252">wp</span><span class="sxs-lookup"><span data-stu-id="cecbf-252">wp</span></span>| <span data-ttu-id="cecbf-253">8.0</span><span class="sxs-lookup"><span data-stu-id="cecbf-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="cecbf-254">相關主題</span><span class="sxs-lookup"><span data-stu-id="cecbf-254">Related topics</span></span>

- [<span data-ttu-id="cecbf-255">Nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="cecbf-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="cecbf-256">符號套件</span><span class="sxs-lookup"><span data-stu-id="cecbf-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="cecbf-257">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="cecbf-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="cecbf-258">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="cecbf-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="cecbf-259">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="cecbf-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="cecbf-260">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="cecbf-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="cecbf-261">.NET Standard 程式庫文件</span><span class="sxs-lookup"><span data-stu-id="cecbf-261">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="cecbf-262">從 .NET Framework 移轉到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="cecbf-262">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
