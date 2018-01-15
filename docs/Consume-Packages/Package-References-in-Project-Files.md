---
title: "Visual Studio 專案檔中的 NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "NuGet 4.0+ 和 VS2017 所支援之專案檔中的 NuGet PackageReference 詳細資料"
keywords: "NuGet 套件相依性, 套件參考, 專案檔, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="49e42-104">專案檔中的套件參考 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="49e42-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="49e42-105">使用 `PackageReference` 節點的套件參考，可讓您直接在專案檔中管理 NuGet 相依性，不需要個別的 `packages.config` 或 `project.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="49e42-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="49e42-106">這個方法不會影響 NuGet 的其他方面，例如，仍會套用 `NuGet.Config` 檔案中的設定 (包括套件來源)，如[設定 NuGet 行為](Configuring-NuGet-Behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="49e42-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="49e42-107">目前，Visual Studio 2017 僅支援以 Windows 10 組建 15063 (Creators Update) 為目標的 .NET Core 專案、.NET Standard 專案和 UWP 專案套件參考。</span><span class="sxs-lookup"><span data-stu-id="49e42-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="49e42-108">`PackageReference` 方法可讓您使用 MSBuild 條件，依目標 Framework、組態、平台或其他分組來選擇套件參考。</span><span class="sxs-lookup"><span data-stu-id="49e42-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="49e42-109">它也允許對相依性和內容流動進行細微控制。</span><span class="sxs-lookup"><span data-stu-id="49e42-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="49e42-110">就行為和[相依性解析](Dependency-Resolution.md)而言，這和使用 `project.json` 相同。</span><span class="sxs-lookup"><span data-stu-id="49e42-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it's the same as using `project.json`.</span></span>

<span data-ttu-id="49e42-111">如需 MSBuild 與專案檔中套件參考整合的詳細資料，請參閱 [NuGet 套件與還原為 MSBuild 目標](../schema/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="49e42-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="49e42-112">新增 PackageReference</span><span class="sxs-lookup"><span data-stu-id="49e42-112">Adding a PackageReference</span></span>

<span data-ttu-id="49e42-113">使用下列語法在專案檔中新增相依性：</span><span class="sxs-lookup"><span data-stu-id="49e42-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="49e42-114">控制相依性版本</span><span class="sxs-lookup"><span data-stu-id="49e42-114">Controlling dependency version</span></span>

<span data-ttu-id="49e42-115">指定套件版本的慣例和使用 `packages.config` 或 `project.json` 一樣：</span><span class="sxs-lookup"><span data-stu-id="49e42-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="49e42-116">在上述範例中，3.6.0 表示 >=3.6.0 的任何版本，但偏好最低版本，如[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中所述。</span><span class="sxs-lookup"><span data-stu-id="49e42-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="49e42-117">浮動版本</span><span class="sxs-lookup"><span data-stu-id="49e42-117">Floating Versions</span></span>

<span data-ttu-id="49e42-118">[浮動版本](../consume-packages/dependency-resolution.md#floating-versions)支援 `PackageReference`：</span><span class="sxs-lookup"><span data-stu-id="49e42-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="49e42-119">控制相依性資產</span><span class="sxs-lookup"><span data-stu-id="49e42-119">Controlling dependency assets</span></span>

<span data-ttu-id="49e42-120">您可能純粹使用相依性作為開發載入器，不想要對取用套件的專案公開。</span><span class="sxs-lookup"><span data-stu-id="49e42-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="49e42-121">在此案例中，您可以使用 `PrivateAssets` 中繼資料控制這個行為。</span><span class="sxs-lookup"><span data-stu-id="49e42-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="49e42-122">下列中繼資料標記控制相依性資產：</span><span class="sxs-lookup"><span data-stu-id="49e42-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="49e42-123">標記</span><span class="sxs-lookup"><span data-stu-id="49e42-123">Tag</span></span> | <span data-ttu-id="49e42-124">描述</span><span class="sxs-lookup"><span data-stu-id="49e42-124">Description</span></span> | <span data-ttu-id="49e42-125">預設值</span><span class="sxs-lookup"><span data-stu-id="49e42-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49e42-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="49e42-126">IncludeAssets</span></span> | <span data-ttu-id="49e42-127">會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="49e42-127">These assets will be consumed</span></span> | <span data-ttu-id="49e42-128">全部</span><span class="sxs-lookup"><span data-stu-id="49e42-128">all</span></span> |
| <span data-ttu-id="49e42-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="49e42-129">ExcludeAssets</span></span> | <span data-ttu-id="49e42-130">不會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="49e42-130">These assets will not be consumed</span></span> | <span data-ttu-id="49e42-131">無</span><span class="sxs-lookup"><span data-stu-id="49e42-131">none</span></span> | 
| <span data-ttu-id="49e42-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="49e42-132">PrivateAssets</span></span> | <span data-ttu-id="49e42-133">會取用這些資產，但不會流動至父專案</span><span class="sxs-lookup"><span data-stu-id="49e42-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="49e42-134">contentfiles;分析器;建置</span><span class="sxs-lookup"><span data-stu-id="49e42-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="49e42-135">這些標記的可允許值如下，使用分號隔開多個值，但 `all` 和 `none` 必須單獨出現：</span><span class="sxs-lookup"><span data-stu-id="49e42-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="49e42-136">值</span><span class="sxs-lookup"><span data-stu-id="49e42-136">Value</span></span> | <span data-ttu-id="49e42-137">描述</span><span class="sxs-lookup"><span data-stu-id="49e42-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="49e42-138">compile</span><span class="sxs-lookup"><span data-stu-id="49e42-138">compile</span></span> | <span data-ttu-id="49e42-139">`lib` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="49e42-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="49e42-140">執行階段</span><span class="sxs-lookup"><span data-stu-id="49e42-140">runtime</span></span> | <span data-ttu-id="49e42-141">`runtime` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="49e42-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="49e42-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="49e42-142">contentFiles</span></span> | <span data-ttu-id="49e42-143">`contentfiles` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="49e42-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="49e42-144">組建</span><span class="sxs-lookup"><span data-stu-id="49e42-144">build</span></span> | <span data-ttu-id="49e42-145">`build` 資料夾中的 props 和目標</span><span class="sxs-lookup"><span data-stu-id="49e42-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="49e42-146">分析器</span><span class="sxs-lookup"><span data-stu-id="49e42-146">analyzers</span></span> | <span data-ttu-id="49e42-147">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="49e42-147">.NET analyzers</span></span> |
| <span data-ttu-id="49e42-148">native</span><span class="sxs-lookup"><span data-stu-id="49e42-148">native</span></span> | <span data-ttu-id="49e42-149">`native` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="49e42-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="49e42-150">無</span><span class="sxs-lookup"><span data-stu-id="49e42-150">none</span></span> | <span data-ttu-id="49e42-151">以上皆不使用。</span><span class="sxs-lookup"><span data-stu-id="49e42-151">None of the above are used.</span></span> |
| <span data-ttu-id="49e42-152">全部</span><span class="sxs-lookup"><span data-stu-id="49e42-152">all</span></span> | <span data-ttu-id="49e42-153">以上全部 (除了`none`)</span><span class="sxs-lookup"><span data-stu-id="49e42-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="49e42-154">在下列範例中，除來自套件的內容檔案之外的所有項目都會被專案取用，除內容檔案和分析器之外的所有項目都會流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="49e42-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="49e42-155">請注意，因為 `build` 不隨附於 `PrivateAssets`，所以目標與 props「會」流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="49e42-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="49e42-156">例如，考慮到上述參考會用在建置名為 AppLogger 之 NuGet 套件的專案中。</span><span class="sxs-lookup"><span data-stu-id="49e42-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="49e42-157">AppLogger 可從 `Contoso.Utility.UsefulStuff` 取用目標與 props，如同專案可以取用 AppLogger。</span><span class="sxs-lookup"><span data-stu-id="49e42-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="49e42-158">新增 PackageReference 條件</span><span class="sxs-lookup"><span data-stu-id="49e42-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="49e42-159">您可以使用條件來控制是否包含套件，這些條件可以使用任何 MSBuild 變數或在目標或 props 檔案中定義的變數。</span><span class="sxs-lookup"><span data-stu-id="49e42-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="49e42-160">但目前只支援 `TargetFramework` 變數。</span><span class="sxs-lookup"><span data-stu-id="49e42-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="49e42-161">例如，假設您的目標是 `netstandard1.4` 以及 `net452`，但所擁有的相依性只適用於 `net452`。</span><span class="sxs-lookup"><span data-stu-id="49e42-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="49e42-162">在此情況下，您不希望取用套件的 `netstandard1.4` 專案新增該項不必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="49e42-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="49e42-163">為避免這個問題，您要在 `PackageReference` 指定條件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49e42-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="49e42-164">使用此專案的套件組建會顯示 Newtonsoft.json 隨附為相依性，但僅適用於 `net452` 目標：</span><span class="sxs-lookup"><span data-stu-id="49e42-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![使用 VS2017 對 PackageReference 套用條件的結果](media/PackageReference-Condition.png)

<span data-ttu-id="49e42-166">條件也可以套用在 `ItemGroup` 層級，並且套用至所有子系 `PackageReference` 項目：</span><span class="sxs-lookup"><span data-stu-id="49e42-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
