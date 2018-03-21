---
title: "使用 Visual Studio 2015 建立 .NET Standard NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "使用 NuGet 3.x 和 Visual Studio 2015 建立 .NET Standard NuGet 套件的端對端逐步解說。"
keywords: "建立套件, .NET Standard 套件, .NET Standard 對應表"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="d4bc2-104">使用 Visual Studio 2015 建立 .NET Standard 套件</span><span class="sxs-lookup"><span data-stu-id="d4bc2-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="d4bc2-105">*適用於 NuGet 3.x。請參閱[使用 Visual Studio 2017 建立和發佈套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)，以使用 NuGet 4.x+。*</span><span class="sxs-lookup"><span data-stu-id="d4bc2-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="d4bc2-106">[.NET Standard 程式庫](/dotnet/articles/standard/library)是計劃提供所有 .NET 執行階段使用的 .NET API 正式規格，因此在 .NET 生態系統中能建立較強的一致性。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="d4bc2-107">.NET Standard 程式庫定義一致的 BCL (基底類別庫) API 集合，以供所有 .NET 平台實作，而不論工作負載為何。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="d4bc2-108">其可讓開發人員產生可跨所有 .NET 執行階段使用的程式碼，並減少 (如果無法消除) 共用程式碼中的平台專屬條件式編譯指示詞。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="d4bc2-109">本指南將引導您建立以 .NET Standard 程式庫 1.4 為目標的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="d4bc2-110">這類程式庫對 .NET Framework 4.6.1、通用 Windows 平台 10、.NET Core 和 Mono/Xamarin 都適用。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="d4bc2-111">如需詳細資料，請參閱本主題下文中的 [.NET Standard 對應表](#net-standard-mapping-table)。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4bc2-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4bc2-112">Prerequisites</span></span>

1. <span data-ttu-id="d4bc2-113">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="d4bc2-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="d4bc2-114">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="d4bc2-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="d4bc2-115">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-115">NuGet CLI.</span></span> <span data-ttu-id="d4bc2-116">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="d4bc2-117">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="d4bc2-118">nuget.exe 本身是 CLI 工具，不是安裝程式，所以請務必從瀏覽器儲存下載的檔案，而不是執行它。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="d4bc2-119">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="d4bc2-119">Create the class library project</span></span>

1. <span data-ttu-id="d4bc2-120">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [Windows] 節點、選取 [類別庫 (可攜式)]、將名稱變更為 AppLogger，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![建立新的類別庫專案](media/NetStandard-NewProject.png)

1. <span data-ttu-id="d4bc2-122">在出現的 [新增可攜式類別庫] 對話方塊中，選取 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 選項。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="d4bc2-123">以滑鼠右鍵按一下方案總管中的 `AppLogger (Portable)`，依序選取 [屬性] 和 [程式庫] 索引標籤，然後按一下 [目標鎖定] 區段的 [目標 .NET 平台標準]。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="d4bc2-124">這會提示您進行確認，然後就可以從下拉式清單中選取 [`.NET Standard 1.4`]：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![將目標設定為 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="d4bc2-126">按一下 [組建] 索引標籤，將 [組態] 變更為 `Release`，並核取 [XML 文件檔] 方塊。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="d4bc2-127">將程式碼新增至元件，例如：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-127">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="d4bc2-128">將組態設定為發行、建置專案，並確認 DLL 和 XML 檔案已產生在 `bin\Release` 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="d4bc2-129">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="d4bc2-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="d4bc2-130">開啟命令提示字元，巡覽至包含 `AppLogger.csproj` 資料夾的資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `AppLogger.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="d4bc2-131">在編輯器中開啟 `AppLogger.nuspec`，更新它使符合下列內容，以適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="d4bc2-132">尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="d4bc2-133">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="d4bc2-134">將參考組件新增至 `.nuspec` 檔案，也就是程式庫的 DLL 和 IntelliSense XML 檔案：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="d4bc2-135">以滑鼠右鍵按一下解決方案，然後選取 [組建方案] 產生套件的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="d4bc2-136">宣告相依性</span><span class="sxs-lookup"><span data-stu-id="d4bc2-136">Declaring dependencies</span></span>

<span data-ttu-id="d4bc2-137">如有其他 NuGet 套件的任何相依性，請使用 `<group>` 項目在資訊清單的 `<dependencies>` 項目中加以列出。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="d4bc2-138">例如，若要宣告對 NewtonSoft.Json 8.0.3 或更新版本的相依性，請新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="d4bc2-139">*version* 屬性的語法在此表示接受該版本 8.0.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="d4bc2-140">若要指定不同的版本範圍，請參閱[套件版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="d4bc2-141">新增讀我檔案</span><span class="sxs-lookup"><span data-stu-id="d4bc2-141">Adding a readme</span></span>

<span data-ttu-id="d4bc2-142">請建立您的 `readme.txt` 檔案，將其置於專案根資料夾中，並在 `.nuspec` 檔案中加以參考：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="d4bc2-143">當套件安裝至專案中時，Visual Studio 會顯示 `readme.txt`。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="d4bc2-144">安裝至 .NET Core 專案時，或對於已安裝為相依性的套件，檔案則不會顯示。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="d4bc2-145">封裝元件</span><span class="sxs-lookup"><span data-stu-id="d4bc2-145">Package the component</span></span>

<span data-ttu-id="d4bc2-146">只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="d4bc2-147">這會產生 `AppLogger.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="d4bc2-148">在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="d4bc2-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![顯示 AppLogger 套件的 NuGet 套件總管](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="d4bc2-150">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="d4bc2-151">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="d4bc2-152">若要讓其他開發人員使用您的套件，請遵循[發佈套件](../create-packages/publish-a-package.md)上的指示。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="d4bc2-153">請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="d4bc2-154">在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。</span><span class="sxs-lookup"><span data-stu-id="d4bc2-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="d4bc2-155">.NET Standard 對應表</span><span class="sxs-lookup"><span data-stu-id="d4bc2-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="d4bc2-156">平台名稱</span><span class="sxs-lookup"><span data-stu-id="d4bc2-156">Platform Name</span></span> | <span data-ttu-id="d4bc2-157">Alias</span><span class="sxs-lookup"><span data-stu-id="d4bc2-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="d4bc2-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="d4bc2-158">.NET Standard</span></span> | <span data-ttu-id="d4bc2-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="d4bc2-159">netstandard</span></span> | <span data-ttu-id="d4bc2-160">1.0</span><span class="sxs-lookup"><span data-stu-id="d4bc2-160">1.0</span></span> | <span data-ttu-id="d4bc2-161">1.1</span><span class="sxs-lookup"><span data-stu-id="d4bc2-161">1.1</span></span> | <span data-ttu-id="d4bc2-162">1.2</span><span class="sxs-lookup"><span data-stu-id="d4bc2-162">1.2</span></span> | <span data-ttu-id="d4bc2-163">1.3</span><span class="sxs-lookup"><span data-stu-id="d4bc2-163">1.3</span></span> | <span data-ttu-id="d4bc2-164">1.4</span><span class="sxs-lookup"><span data-stu-id="d4bc2-164">1.4</span></span> | <span data-ttu-id="d4bc2-165">1.5</span><span class="sxs-lookup"><span data-stu-id="d4bc2-165">1.5</span></span> | <span data-ttu-id="d4bc2-166">1.6</span><span class="sxs-lookup"><span data-stu-id="d4bc2-166">1.6</span></span> |
| <span data-ttu-id="d4bc2-167">.NET 核心</span><span class="sxs-lookup"><span data-stu-id="d4bc2-167">.NET Core</span></span> | <span data-ttu-id="d4bc2-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="d4bc2-168">netcoreapp</span></span> | <span data-ttu-id="d4bc2-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-169">&#x2192;</span></span> | <span data-ttu-id="d4bc2-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-170">&#x2192;</span></span> | <span data-ttu-id="d4bc2-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-171">&#x2192;</span></span> | <span data-ttu-id="d4bc2-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-172">&#x2192;</span></span> | <span data-ttu-id="d4bc2-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-173">&#x2192;</span></span> | <span data-ttu-id="d4bc2-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-174">&#x2192;</span></span> | <span data-ttu-id="d4bc2-175">1.0</span><span class="sxs-lookup"><span data-stu-id="d4bc2-175">1.0</span></span> |
| <span data-ttu-id="d4bc2-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d4bc2-176">.NET Framework</span></span> | <span data-ttu-id="d4bc2-177">net</span><span class="sxs-lookup"><span data-stu-id="d4bc2-177">net</span></span> | <span data-ttu-id="d4bc2-178">4.5</span><span class="sxs-lookup"><span data-stu-id="d4bc2-178">4.5</span></span> | <span data-ttu-id="d4bc2-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="d4bc2-179">4.5.1</span></span> | <span data-ttu-id="d4bc2-180">4.6</span><span class="sxs-lookup"><span data-stu-id="d4bc2-180">4.6</span></span> | <span data-ttu-id="d4bc2-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="d4bc2-181">4.6.1</span></span> | <span data-ttu-id="d4bc2-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="d4bc2-182">4.6.2</span></span> | <span data-ttu-id="d4bc2-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="d4bc2-183">4.6.3</span></span> |
| <span data-ttu-id="d4bc2-184">Mono/Xamarin 平台</span><span class="sxs-lookup"><span data-stu-id="d4bc2-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="d4bc2-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-185">&#x2192;</span></span> | <span data-ttu-id="d4bc2-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-186">&#x2192;</span></span> | <span data-ttu-id="d4bc2-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-187">&#x2192;</span></span> | <span data-ttu-id="d4bc2-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-188">&#x2192;</span></span> | <span data-ttu-id="d4bc2-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-189">&#x2192;</span></span> | <span data-ttu-id="d4bc2-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-190">&#x2192;</span></span> |
| <span data-ttu-id="d4bc2-191">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="d4bc2-191">Universal Windows Platform</span></span> | <span data-ttu-id="d4bc2-192">uap</span><span class="sxs-lookup"><span data-stu-id="d4bc2-192">uap</span></span> | <span data-ttu-id="d4bc2-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-193">&#x2192;</span></span> | <span data-ttu-id="d4bc2-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-194">&#x2192;</span></span> | <span data-ttu-id="d4bc2-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-195">&#x2192;</span></span> | <span data-ttu-id="d4bc2-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-196">&#x2192;</span></span> |<span data-ttu-id="d4bc2-197">10.0</span><span class="sxs-lookup"><span data-stu-id="d4bc2-197">10.0</span></span> |
| <span data-ttu-id="d4bc2-198">Windows</span><span class="sxs-lookup"><span data-stu-id="d4bc2-198">Windows</span></span> | <span data-ttu-id="d4bc2-199">win</span><span class="sxs-lookup"><span data-stu-id="d4bc2-199">win</span></span>| <span data-ttu-id="d4bc2-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-200">&#x2192;</span></span> | <span data-ttu-id="d4bc2-201">8.0</span><span class="sxs-lookup"><span data-stu-id="d4bc2-201">8.0</span></span> | <span data-ttu-id="d4bc2-202">8.1</span><span class="sxs-lookup"><span data-stu-id="d4bc2-202">8.1</span></span> |
| <span data-ttu-id="d4bc2-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="d4bc2-203">Windows Phone</span></span> | <span data-ttu-id="d4bc2-204">wpa</span><span class="sxs-lookup"><span data-stu-id="d4bc2-204">wpa</span></span>| <span data-ttu-id="d4bc2-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-205">&#x2192;</span></span>| <span data-ttu-id="d4bc2-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="d4bc2-206">&#x2192;</span></span> | <span data-ttu-id="d4bc2-207">8.1</span><span class="sxs-lookup"><span data-stu-id="d4bc2-207">8.1</span></span> |
| <span data-ttu-id="d4bc2-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d4bc2-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="d4bc2-209">wp</span><span class="sxs-lookup"><span data-stu-id="d4bc2-209">wp</span></span> | <span data-ttu-id="d4bc2-210">8.0</span><span class="sxs-lookup"><span data-stu-id="d4bc2-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="d4bc2-211">相關主題</span><span class="sxs-lookup"><span data-stu-id="d4bc2-211">Related topics</span></span>

- [<span data-ttu-id="d4bc2-212">.nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="d4bc2-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="d4bc2-213">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="d4bc2-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d4bc2-214">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="d4bc2-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="d4bc2-215">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="d4bc2-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="d4bc2-216">符號套件</span><span class="sxs-lookup"><span data-stu-id="d4bc2-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="d4bc2-217">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="d4bc2-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="d4bc2-218">.NET Standard 程式庫文件</span><span class="sxs-lookup"><span data-stu-id="d4bc2-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="d4bc2-219">從 .NET Framework 移轉到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="d4bc2-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
