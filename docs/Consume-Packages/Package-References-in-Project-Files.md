---
title: NuGet PackageReference 格式 (專案檔中的套件參考) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 4.0+ 和 VS2017 及 .NET Core 2.0 所支援之專案檔中的 NuGet PackageReference 詳細資料
keywords: NuGet 套件相依性, 套件參考, 專案檔, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e1880c9b294e19ef1b71c7b17b02df8ff1cf1b73
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="ffaab-104">專案檔中的套件參考 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="ffaab-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="ffaab-105">套件參考使用 `PackageReference` 節點，直接在專案檔中管理 NuGet 相依性 (而不是在個別的 `packages.config` 檔案中)。</span><span class="sxs-lookup"><span data-stu-id="ffaab-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="ffaab-106">使用 PackageReference 不會影響 NuGet 的其他方面；例如，仍會套用 `NuGet.Config` 檔案中的設定 (包括套件來源)，如[設定 NuGet 行為](configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="ffaab-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="ffaab-107">使用 PackageReference 也可讓您使用 MSBuild 條件，依目標 Framework、組態、平台或其他群組來選擇套件參考。</span><span class="sxs-lookup"><span data-stu-id="ffaab-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="ffaab-108">它也允許對相依性和內容流動進行細微控制。</span><span class="sxs-lookup"><span data-stu-id="ffaab-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="ffaab-109">(如需詳細資訊，請參閱 [NuGet pack and restore as MSBuild targetsNuGet](../reference/msbuild-targets.md) (NuGet 以 pack 與 restore 作為 MSBuild 目標)。)</span><span class="sxs-lookup"><span data-stu-id="ffaab-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="ffaab-110">根據預設，PackageReference 會用於以 Windows 10 組建 15063 (Creators Update) 及更新版本為目標的 .NET Core 專案、.NET Standard 專案和 UWP 專案 (C++ UWP 專案除外)。</span><span class="sxs-lookup"><span data-stu-id="ffaab-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="ffaab-111">.NET 完整 Framework 專案支援 PackageReference，但目前預設為 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="ffaab-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="ffaab-112">若要使用 PackageReference，請將相依性從 `packages.config` 移轉至您的專案檔，然後移除 packages.config。</span><span class="sxs-lookup"><span data-stu-id="ffaab-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="ffaab-113">新增 PackageReference</span><span class="sxs-lookup"><span data-stu-id="ffaab-113">Adding a PackageReference</span></span>

<span data-ttu-id="ffaab-114">使用下列語法在專案檔中新增相依性：</span><span class="sxs-lookup"><span data-stu-id="ffaab-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="ffaab-115">控制相依性版本</span><span class="sxs-lookup"><span data-stu-id="ffaab-115">Controlling dependency version</span></span>

<span data-ttu-id="ffaab-116">指定套件版本的慣例和使用 `packages.config` 時一樣：</span><span class="sxs-lookup"><span data-stu-id="ffaab-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ffaab-117">在上述範例中，3.6.0 表示 >=3.6.0 的任何版本，但偏好最低版本，如[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中所述。</span><span class="sxs-lookup"><span data-stu-id="ffaab-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="ffaab-118">浮動版本</span><span class="sxs-lookup"><span data-stu-id="ffaab-118">Floating Versions</span></span>

<span data-ttu-id="ffaab-119">[浮動版本](../consume-packages/dependency-resolution.md#floating-versions)支援 `PackageReference`：</span><span class="sxs-lookup"><span data-stu-id="ffaab-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="ffaab-120">控制相依性資產</span><span class="sxs-lookup"><span data-stu-id="ffaab-120">Controlling dependency assets</span></span>

<span data-ttu-id="ffaab-121">您可能純粹使用相依性作為開發載入器，不想要對取用套件的專案公開。</span><span class="sxs-lookup"><span data-stu-id="ffaab-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="ffaab-122">在此案例中，您可以使用 `PrivateAssets` 中繼資料控制這個行為。</span><span class="sxs-lookup"><span data-stu-id="ffaab-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ffaab-123">下列中繼資料標記控制相依性資產：</span><span class="sxs-lookup"><span data-stu-id="ffaab-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="ffaab-124">標記</span><span class="sxs-lookup"><span data-stu-id="ffaab-124">Tag</span></span> | <span data-ttu-id="ffaab-125">描述</span><span class="sxs-lookup"><span data-stu-id="ffaab-125">Description</span></span> | <span data-ttu-id="ffaab-126">預設值</span><span class="sxs-lookup"><span data-stu-id="ffaab-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffaab-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="ffaab-127">IncludeAssets</span></span> | <span data-ttu-id="ffaab-128">會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="ffaab-128">These assets will be consumed</span></span> | <span data-ttu-id="ffaab-129">全部</span><span class="sxs-lookup"><span data-stu-id="ffaab-129">all</span></span> |
| <span data-ttu-id="ffaab-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="ffaab-130">ExcludeAssets</span></span> | <span data-ttu-id="ffaab-131">不會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="ffaab-131">These assets will not be consumed</span></span> | <span data-ttu-id="ffaab-132">無</span><span class="sxs-lookup"><span data-stu-id="ffaab-132">none</span></span> |
| <span data-ttu-id="ffaab-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="ffaab-133">PrivateAssets</span></span> | <span data-ttu-id="ffaab-134">會取用這些資產，但不會流動至父專案</span><span class="sxs-lookup"><span data-stu-id="ffaab-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="ffaab-135">contentfiles;分析器;建置</span><span class="sxs-lookup"><span data-stu-id="ffaab-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="ffaab-136">這些標記的可允許值如下，使用分號隔開多個值，但 `all` 和 `none` 必須單獨出現：</span><span class="sxs-lookup"><span data-stu-id="ffaab-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="ffaab-137">值</span><span class="sxs-lookup"><span data-stu-id="ffaab-137">Value</span></span> | <span data-ttu-id="ffaab-138">描述</span><span class="sxs-lookup"><span data-stu-id="ffaab-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="ffaab-139">compile</span><span class="sxs-lookup"><span data-stu-id="ffaab-139">compile</span></span> | <span data-ttu-id="ffaab-140">`lib` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="ffaab-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="ffaab-141">執行階段</span><span class="sxs-lookup"><span data-stu-id="ffaab-141">runtime</span></span> | <span data-ttu-id="ffaab-142">`runtimes` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="ffaab-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="ffaab-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ffaab-143">contentFiles</span></span> | <span data-ttu-id="ffaab-144">`contentfiles` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="ffaab-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="ffaab-145">build</span><span class="sxs-lookup"><span data-stu-id="ffaab-145">build</span></span> | <span data-ttu-id="ffaab-146">`build` 資料夾中的 props 和目標</span><span class="sxs-lookup"><span data-stu-id="ffaab-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="ffaab-147">分析器</span><span class="sxs-lookup"><span data-stu-id="ffaab-147">analyzers</span></span> | <span data-ttu-id="ffaab-148">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="ffaab-148">.NET analyzers</span></span> |
| <span data-ttu-id="ffaab-149">native</span><span class="sxs-lookup"><span data-stu-id="ffaab-149">native</span></span> | <span data-ttu-id="ffaab-150">`native` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="ffaab-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="ffaab-151">無</span><span class="sxs-lookup"><span data-stu-id="ffaab-151">none</span></span> | <span data-ttu-id="ffaab-152">以上皆不使用。</span><span class="sxs-lookup"><span data-stu-id="ffaab-152">None of the above are used.</span></span> |
| <span data-ttu-id="ffaab-153">全部</span><span class="sxs-lookup"><span data-stu-id="ffaab-153">all</span></span> | <span data-ttu-id="ffaab-154">以上全部 (除了`none`)</span><span class="sxs-lookup"><span data-stu-id="ffaab-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="ffaab-155">在下列範例中，除來自套件的內容檔案之外的所有項目都會被專案取用，除內容檔案和分析器之外的所有項目都會流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="ffaab-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="ffaab-156">請注意，因為 `build` 不隨附於 `PrivateAssets`，所以目標與 props「會」流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="ffaab-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="ffaab-157">例如，考慮到上述參考會用在建置名為 AppLogger 之 NuGet 套件的專案中。</span><span class="sxs-lookup"><span data-stu-id="ffaab-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="ffaab-158">AppLogger 可從 `Contoso.Utility.UsefulStuff` 取用目標與 props，如同專案可以取用 AppLogger。</span><span class="sxs-lookup"><span data-stu-id="ffaab-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="ffaab-159">新增 PackageReference 條件</span><span class="sxs-lookup"><span data-stu-id="ffaab-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="ffaab-160">您可以使用條件來控制是否包含套件，這些條件可以使用任何 MSBuild 變數或在目標或 props 檔案中定義的變數。</span><span class="sxs-lookup"><span data-stu-id="ffaab-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="ffaab-161">但目前只支援 `TargetFramework` 變數。</span><span class="sxs-lookup"><span data-stu-id="ffaab-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="ffaab-162">例如，假設您的目標是 `netstandard1.4` 以及 `net452`，但所擁有的相依性只適用於 `net452`。</span><span class="sxs-lookup"><span data-stu-id="ffaab-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="ffaab-163">在此情況下，您不希望取用套件的 `netstandard1.4` 專案新增該項不必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="ffaab-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="ffaab-164">為避免這個問題，您要在 `PackageReference` 指定條件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ffaab-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ffaab-165">使用此專案的套件組建會顯示 Newtonsoft.json 隨附為相依性，但僅適用於 `net452` 目標：</span><span class="sxs-lookup"><span data-stu-id="ffaab-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![使用 VS2017 對 PackageReference 套用條件的結果](media/PackageReference-Condition.png)

<span data-ttu-id="ffaab-167">條件也可以套用在 `ItemGroup` 層級，並且套用至所有子系 `PackageReference` 項目：</span><span class="sxs-lookup"><span data-stu-id="ffaab-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
