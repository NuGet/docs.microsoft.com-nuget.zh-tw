---
title: 使用 dotnet CLI 建立 NuGet 套件
description: NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類關鍵決策點。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462462"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="4d719-103">使用 dotnet CLI 建立 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="4d719-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="4d719-104">不論套件的功能或所含程式碼為何，您都可以使用其中一個 CLI 工具 (`nuget.exe` 或 `dotnet.exe`) 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。</span><span class="sxs-lookup"><span data-stu-id="4d719-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="4d719-105">此文章說明如何使用 dotnet CLI 建立套件。</span><span class="sxs-lookup"><span data-stu-id="4d719-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="4d719-106">若要安裝 `dotnet` CLI，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="4d719-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="4d719-107">從 Visual Studio 2017 開始，dotnet CLI 隨附於 .NET Core工作負載中。</span><span class="sxs-lookup"><span data-stu-id="4d719-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="4d719-108">針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，NuGet 會直接使用專案檔中的資訊來建立套件。</span><span class="sxs-lookup"><span data-stu-id="4d719-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="4d719-109">如需逐步教學課程，請參閱[使用 dotnet CLI 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)、[使用 Visual Studio 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="4d719-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="4d719-110">`msbuild -t:pack` 在功能上相當於 `dotnet pack`。</span><span class="sxs-lookup"><span data-stu-id="4d719-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="4d719-111">若要使用 MSBuild 進行建置，概念與此文章中所述相同，但是命令列命令會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="4d719-111">To build with MSBuild, the concepts are the same as described in this article, but the command line commands are slightly different.</span></span> <span data-ttu-id="4d719-112">同樣地，對於非 SDK 樣式的專案與 `<PackageReference>`，您可以使用 `msbuild /t:pack`。</span><span class="sxs-lookup"><span data-stu-id="4d719-112">Similarly, with a non-SDK-style project and `<PackageReference>`, you can use `msbuild /t:pack`.</span></span> <span data-ttu-id="4d719-113">在這些情節中，您需要將 NuGet.Build.Tasks.Pack 套件新增至其相依性。</span><span class="sxs-lookup"><span data-stu-id="4d719-113">In these scenarios, you need to add the NuGet.Build.Tasks.Pack package to their dependencies.</span></span> <span data-ttu-id="4d719-114">請參閱 [NuGet 套件和還原為 MSBuild 目標](../reference/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="4d719-114">See [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d719-115">此主題適用於 [SDK 樣式](../resources/check-project-format.md)的專案，這通常是 .NET Core 與 .NET Standard 專案。</span><span class="sxs-lookup"><span data-stu-id="4d719-115">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="4d719-116">設定屬性</span><span class="sxs-lookup"><span data-stu-id="4d719-116">Set properties</span></span>

<span data-ttu-id="4d719-117">建立套件時需要下列屬性。</span><span class="sxs-lookup"><span data-stu-id="4d719-117">The following properties are required to create a package.</span></span>

- <span data-ttu-id="4d719-118">`PackageId`，套件識別碼，這在裝載套件的資源庫內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4d719-118">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="4d719-119">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="4d719-119">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4d719-120">`Version`，*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="4d719-120">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="4d719-121">若未指定，則預設值為 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="4d719-121">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="4d719-122">主機上應該會出現套件標題 (例如 nuget.org)</span><span class="sxs-lookup"><span data-stu-id="4d719-122">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="4d719-123">`Authors`，作者與擁有者資訊。</span><span class="sxs-lookup"><span data-stu-id="4d719-123">`Authors`, author and owner information.</span></span> <span data-ttu-id="4d719-124">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="4d719-124">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4d719-125">`Company`，您的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="4d719-125">`Company`, your company name.</span></span> <span data-ttu-id="4d719-126">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="4d719-126">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="4d719-127">在 Visual Studio 中，您可以在專案屬性中設定這些值 (在 [方案總管] 中以滑鼠右鍵按一下專案，選擇 [屬性]  ，然後選取 [套件]  索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="4d719-127">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="4d719-128">您也可以直接在專案檔 (`.csproj`) 中設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="4d719-128">You can also set these properties directly in the project files (`.csproj`).</span></span>

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> <span data-ttu-id="4d719-129">為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何套件資源上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4d719-129">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="4d719-130">您還可以設定選擇性屬性，例如`Title`、`PackageDescription` 與 `PackageTags`，如 [MSBuild 套件目標](../reference/msbuild-targets.md#pack-target)、[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)，以及 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。</span><span class="sxs-lookup"><span data-stu-id="4d719-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="4d719-131">針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="4d719-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="4d719-132">如需宣告相依性以及指定版本號碼的詳細資料，請參閱[套件版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="4d719-132">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="4d719-133">使用 `<IncludeAssets>` 與 `<ExcludeAssets>` 屬性，也可以將來自相依性的資產直接用於套件中。</span><span class="sxs-lookup"><span data-stu-id="4d719-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="4d719-134">如需詳細資訊，請參閱[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="4d719-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="4d719-135">選擇唯一的套件識別碼並設定版本號碼</span><span class="sxs-lookup"><span data-stu-id="4d719-135">Choose a unique package identifier and set the version number</span></span>

<span data-ttu-id="4d719-136">套件識別碼與版本號碼是專案中的兩個最重要值，因為它們可以唯一識別套件中所含的確切程式碼。</span><span class="sxs-lookup"><span data-stu-id="4d719-136">The package identifier and the version number are the two most important values in the project because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="4d719-137">**套件識別碼的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="4d719-137">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="4d719-138">**唯一性**：在 nuget.org 內，或只要資源庫裝載套件時，識別碼就必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4d719-138">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="4d719-139">決定識別碼之前，請搜尋適用的資源庫，檢查是否已在使用名稱。</span><span class="sxs-lookup"><span data-stu-id="4d719-139">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="4d719-140">若要避免衝突，不錯的模式是使用您的公司名稱作為識別碼的第一個部分，例如 `Contoso.`。</span><span class="sxs-lookup"><span data-stu-id="4d719-140">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="4d719-141">**命名空間類似名稱**：遵循與 .NET 中命名空間類似的模式，即使用點標記法，而非連字號。</span><span class="sxs-lookup"><span data-stu-id="4d719-141">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="4d719-142">例如，使用 `Contoso.Utility.UsefulStuff`，而非 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。</span><span class="sxs-lookup"><span data-stu-id="4d719-142">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="4d719-143">套件識別碼符合程式碼中所使用的命名空間時，取用者也會發現它十分有用。</span><span class="sxs-lookup"><span data-stu-id="4d719-143">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="4d719-144">**範例套件**：如果您產生的範例程式碼套件示範如何使用另一個套件，請將 `.Sample` 附加為識別碼的尾碼，如 `Contoso.Utility.UsefulStuff.Sample` 所示</span><span class="sxs-lookup"><span data-stu-id="4d719-144">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="4d719-145">(範例套件當然會有與另一個套件的相依性)。建立範例套件時，請使用 `<IncludeAssets>` 中的 `contentFiles` 值。</span><span class="sxs-lookup"><span data-stu-id="4d719-145">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the `contentFiles` value in `<IncludeAssets>`.</span></span> <span data-ttu-id="4d719-146">在 `content` 資料夾中，於稱為 `\Samples\<identifier>` 的資料夾中排列範例程式碼，而這與 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相同。</span><span class="sxs-lookup"><span data-stu-id="4d719-146">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="4d719-147">**套件版本的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="4d719-147">**Best practices for the package version:**</span></span>

- <span data-ttu-id="4d719-148">一般而言，請設定套件版本，使其符合專案 (或組件)，但這不是絕對必要。</span><span class="sxs-lookup"><span data-stu-id="4d719-148">In general, set the version of the package to match the project (or assembly), though this is not strictly required.</span></span> <span data-ttu-id="4d719-149">當您將套件限制為單一組件時，這很簡單。</span><span class="sxs-lookup"><span data-stu-id="4d719-149">This is a simple matter when you limit a package to a single assembly.</span></span> <span data-ttu-id="4d719-150">整體來說，請記住，解析相依性時，NuGet 本身會處理套件版本，而非組件版本。</span><span class="sxs-lookup"><span data-stu-id="4d719-150">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="4d719-151">使用非標準版本方式時，請務必考慮使用 NuGet 版本控制規則，如[套件版本控制](../reference/package-versioning.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="4d719-151">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="4d719-152">NuGet 大多[符合 semver 2 規範](../reference/package-versioning.md#semantic-versioning-200)。</span><span class="sxs-lookup"><span data-stu-id="4d719-152">NuGet is mostly [semver 2 compliant](../reference/package-versioning.md#semantic-versioning-200).</span></span>

> <span data-ttu-id="4d719-153">如需相依性解析的相關資訊，請參閱[使用 PackageReference 的相依性解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)。</span><span class="sxs-lookup"><span data-stu-id="4d719-153">For information on dependency resolution, see [Dependency resolution with PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span></span> <span data-ttu-id="4d719-154">如需更深入了解版本控制的較舊資訊，請參閱這一系列的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="4d719-154">For older information that may also be helpful to better understand versioning, see this series of blog posts.</span></span>
>
> - <span data-ttu-id="4d719-155">[第 1 部分：接受 DLL 挑戰](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="4d719-155">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="4d719-156">[第 2 部分：核心演算法](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="4d719-156">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="4d719-157">[第 3 部分：透過繫結重新導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="4d719-157">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="4d719-158">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="4d719-158">Run the pack command</span></span>

<span data-ttu-id="4d719-159">若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `dotnet pack` 命令，該命令也會自動建置專案：</span><span class="sxs-lookup"><span data-stu-id="4d719-159">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="4d719-160">輸出將顯示 `.nupkg` 檔案的路徑：</span><span class="sxs-lookup"><span data-stu-id="4d719-160">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="4d719-161">建置時自動產生套件</span><span class="sxs-lookup"><span data-stu-id="4d719-161">Automatically generate package on build</span></span>

<span data-ttu-id="4d719-162">若要在您執行 `dotnet build` 時自動執行 `dotnet pack`，請將下列程式行加入專案檔的 `<PropertyGroup>` 中：</span><span class="sxs-lookup"><span data-stu-id="4d719-162">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="4d719-163">當您在方案上執行 `dotnet pack` 時，這會封裝方案中可封裝的所有專案 ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 屬性設定為 `true`)。</span><span class="sxs-lookup"><span data-stu-id="4d719-163">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="4d719-164">當您自動產生套件時，封裝的時間會增加專案的建置時間。</span><span class="sxs-lookup"><span data-stu-id="4d719-164">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="4d719-165">測試套件安裝</span><span class="sxs-lookup"><span data-stu-id="4d719-165">Test package installation</span></span>

<span data-ttu-id="4d719-166">發行套件之前，您通常會想要測試將套件安裝至專案的程序。</span><span class="sxs-lookup"><span data-stu-id="4d719-166">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="4d719-167">測試可確定必要檔案最後都在專案的正確位置。</span><span class="sxs-lookup"><span data-stu-id="4d719-167">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="4d719-168">您可以使用一般[套件安裝步驟](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)，以在 Visual Studio 中或命令列上手動測試安裝。</span><span class="sxs-lookup"><span data-stu-id="4d719-168">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d719-169">套件是不可變的。</span><span class="sxs-lookup"><span data-stu-id="4d719-169">Packages are immutable.</span></span> <span data-ttu-id="4d719-170">如果您更正了問題，請變更套件的內容並再次封裝，當您重新測試時，仍會使用舊版套件，直到您[清除全域套件](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)資料夾為止。</span><span class="sxs-lookup"><span data-stu-id="4d719-170">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="4d719-171">在測試每個組建上未使用唯一發行前版本標籤的套件時，這關係重大。</span><span class="sxs-lookup"><span data-stu-id="4d719-171">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d719-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d719-172">Next Steps</span></span>

<span data-ttu-id="4d719-173">建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="4d719-173">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="4d719-174">您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：</span><span class="sxs-lookup"><span data-stu-id="4d719-174">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="4d719-175">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="4d719-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4d719-176">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="4d719-176">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="4d719-177">原始程式檔和組態檔的轉換</span><span class="sxs-lookup"><span data-stu-id="4d719-177">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="4d719-178">當地語系化</span><span class="sxs-lookup"><span data-stu-id="4d719-178">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4d719-179">發行前版本</span><span class="sxs-lookup"><span data-stu-id="4d719-179">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="4d719-180">設定套件類型</span><span class="sxs-lookup"><span data-stu-id="4d719-180">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="4d719-181">建立包含 COM Interop 組件的套件</span><span class="sxs-lookup"><span data-stu-id="4d719-181">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="4d719-182">最後，請注意其他套件類型：</span><span class="sxs-lookup"><span data-stu-id="4d719-182">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="4d719-183">原生套件</span><span class="sxs-lookup"><span data-stu-id="4d719-183">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="4d719-184">符號套件</span><span class="sxs-lookup"><span data-stu-id="4d719-184">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
