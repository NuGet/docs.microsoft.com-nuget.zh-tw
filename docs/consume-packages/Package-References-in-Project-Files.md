---
title: NuGet PackageReference 格式 (專案檔中的套件參考)
description: NuGet 4.0+ 和 VS2017 及 .NET Core 2.0 所支援之專案檔中的 NuGet PackageReference 詳細資料
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: e4df15be1f29e2c611876aaa49e16ac7d1823938
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248451"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="d272a-103">專案檔中的套件參考 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d272a-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="d272a-104">套件參考使用 `PackageReference` 節點，直接在專案檔中管理 NuGet 相依性 (而不是在個別的 `packages.config` 檔案中)。</span><span class="sxs-lookup"><span data-stu-id="d272a-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="d272a-105">使用 PackageReference 不會影響 NuGet 的其他方面；例如，仍會套用 `NuGet.config` 檔案中的設定 (包括套件來源)，如[設定 NuGet 行為](configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="d272a-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="d272a-106">使用 PackageReference 也可讓您使用 MSBuild 條件，依目標 Framework、組態、平台或其他群組來選擇套件參考。</span><span class="sxs-lookup"><span data-stu-id="d272a-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="d272a-107">它也允許對相依性和內容流動進行細微控制。</span><span class="sxs-lookup"><span data-stu-id="d272a-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="d272a-108">(如需詳細資訊，請參閱 [NuGet pack and restore as MSBuild targetsNuGet](../reference/msbuild-targets.md) (NuGet 以 pack 與 restore 作為 MSBuild 目標)。)</span><span class="sxs-lookup"><span data-stu-id="d272a-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="d272a-109">根據預設，PackageReference 會用於以 Windows 10 組建 15063 (Creators Update) 及更新版本為目標的 .NET Core 專案、.NET Standard 專案和 UWP 專案 (C++ UWP 專案除外)。</span><span class="sxs-lookup"><span data-stu-id="d272a-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="d272a-110">.NET Framework 專案支援 PackageReference，但目前預設為 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="d272a-110">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="d272a-111">若要使用 PackageReference，請將相依性從 `packages.config` 移轉至您的專案檔，然後移除 packages.config。</span><span class="sxs-lookup"><span data-stu-id="d272a-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="d272a-112">新增 PackageReference</span><span class="sxs-lookup"><span data-stu-id="d272a-112">Adding a PackageReference</span></span>

<span data-ttu-id="d272a-113">使用下列語法在專案檔中新增相依性：</span><span class="sxs-lookup"><span data-stu-id="d272a-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="d272a-114">控制相依性版本</span><span class="sxs-lookup"><span data-stu-id="d272a-114">Controlling dependency version</span></span>

<span data-ttu-id="d272a-115">指定套件版本的慣例和使用 `packages.config` 時一樣：</span><span class="sxs-lookup"><span data-stu-id="d272a-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="d272a-116">在上述範例中，3.6.0 表示 >=3.6.0 的任何版本，但偏好最低版本，如[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中所述。</span><span class="sxs-lookup"><span data-stu-id="d272a-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="d272a-117">針對沒有任何 PackageReference 的專案使用 PackageReference</span><span class="sxs-lookup"><span data-stu-id="d272a-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="d272a-118">進階：如果專案中未安裝任何套件 (專案檔中沒有 PackageReference，也沒有 packages.config 檔案)，但希望專案能還原為 PackageReference 樣式，您可以在您的專案檔中將專案屬性 RestoreProjectStyle 設定為 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="d272a-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="d272a-119">如果您的參考專案為 PackageReference 樣式 (現有的 csproj 或 SDK 樣式專案)，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="d272a-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="d272a-120">這會讓這些專案參考的套件成為您專案「過渡性」參考的套件。</span><span class="sxs-lookup"><span data-stu-id="d272a-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="d272a-121">浮動版本</span><span class="sxs-lookup"><span data-stu-id="d272a-121">Floating Versions</span></span>

<span data-ttu-id="d272a-122">[浮動版本](../consume-packages/dependency-resolution.md#floating-versions)支援 `PackageReference`：</span><span class="sxs-lookup"><span data-stu-id="d272a-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="d272a-123">控制相依性資產</span><span class="sxs-lookup"><span data-stu-id="d272a-123">Controlling dependency assets</span></span>

<span data-ttu-id="d272a-124">您可能純粹使用相依性作為開發載入器，不想要對取用套件的專案公開。</span><span class="sxs-lookup"><span data-stu-id="d272a-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="d272a-125">在此案例中，您可以使用 `PrivateAssets` 中繼資料控制這個行為。</span><span class="sxs-lookup"><span data-stu-id="d272a-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="d272a-126">下列中繼資料標記控制相依性資產：</span><span class="sxs-lookup"><span data-stu-id="d272a-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="d272a-127">標記</span><span class="sxs-lookup"><span data-stu-id="d272a-127">Tag</span></span> | <span data-ttu-id="d272a-128">說明</span><span class="sxs-lookup"><span data-stu-id="d272a-128">Description</span></span> | <span data-ttu-id="d272a-129">預設值</span><span class="sxs-lookup"><span data-stu-id="d272a-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d272a-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="d272a-130">IncludeAssets</span></span> | <span data-ttu-id="d272a-131">會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="d272a-131">These assets will be consumed</span></span> | <span data-ttu-id="d272a-132">全部</span><span class="sxs-lookup"><span data-stu-id="d272a-132">all</span></span> |
| <span data-ttu-id="d272a-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="d272a-133">ExcludeAssets</span></span> | <span data-ttu-id="d272a-134">不會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="d272a-134">These assets will not be consumed</span></span> | <span data-ttu-id="d272a-135">無</span><span class="sxs-lookup"><span data-stu-id="d272a-135">none</span></span> |
| <span data-ttu-id="d272a-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="d272a-136">PrivateAssets</span></span> | <span data-ttu-id="d272a-137">會取用這些資產，但不會流動至父專案</span><span class="sxs-lookup"><span data-stu-id="d272a-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="d272a-138">contentfiles;分析器;建置</span><span class="sxs-lookup"><span data-stu-id="d272a-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="d272a-139">這些標記的可允許值如下，使用分號隔開多個值，但 `all` 和 `none` 必須單獨出現：</span><span class="sxs-lookup"><span data-stu-id="d272a-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="d272a-140">值</span><span class="sxs-lookup"><span data-stu-id="d272a-140">Value</span></span> | <span data-ttu-id="d272a-141">說明</span><span class="sxs-lookup"><span data-stu-id="d272a-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="d272a-142">compile</span><span class="sxs-lookup"><span data-stu-id="d272a-142">compile</span></span> | <span data-ttu-id="d272a-143">`lib` 資料夾的內容，以及專案是否能對該資料夾內的組件進行編譯的控制項</span><span class="sxs-lookup"><span data-stu-id="d272a-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="d272a-144">執行階段</span><span class="sxs-lookup"><span data-stu-id="d272a-144">runtime</span></span> | <span data-ttu-id="d272a-145">`lib` 與 `runtimes` 資料夾的內容，以及是否能將這些組件複製到組建輸出目錄的控制項</span><span class="sxs-lookup"><span data-stu-id="d272a-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="d272a-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d272a-146">contentFiles</span></span> | <span data-ttu-id="d272a-147">`contentfiles` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="d272a-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="d272a-148">build</span><span class="sxs-lookup"><span data-stu-id="d272a-148">build</span></span> | <span data-ttu-id="d272a-149">`build` 資料夾中的 props 和目標</span><span class="sxs-lookup"><span data-stu-id="d272a-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="d272a-150">分析器</span><span class="sxs-lookup"><span data-stu-id="d272a-150">analyzers</span></span> | <span data-ttu-id="d272a-151">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="d272a-151">.NET analyzers</span></span> |
| <span data-ttu-id="d272a-152">native</span><span class="sxs-lookup"><span data-stu-id="d272a-152">native</span></span> | <span data-ttu-id="d272a-153">`native` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="d272a-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="d272a-154">無</span><span class="sxs-lookup"><span data-stu-id="d272a-154">none</span></span> | <span data-ttu-id="d272a-155">以上皆不使用。</span><span class="sxs-lookup"><span data-stu-id="d272a-155">None of the above are used.</span></span> |
| <span data-ttu-id="d272a-156">全部</span><span class="sxs-lookup"><span data-stu-id="d272a-156">all</span></span> | <span data-ttu-id="d272a-157">以上全部 (除了`none`)</span><span class="sxs-lookup"><span data-stu-id="d272a-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="d272a-158">在下列範例中，除來自套件的內容檔案之外的所有項目都會被專案取用，除內容檔案和分析器之外的所有項目都會流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="d272a-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="d272a-159">請注意，因為 `build` 不隨附於 `PrivateAssets`，所以目標與 props「會」流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="d272a-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="d272a-160">例如，考慮到上述參考會用在建置名為 AppLogger 之 NuGet 套件的專案中。</span><span class="sxs-lookup"><span data-stu-id="d272a-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="d272a-161">AppLogger 可從 `Contoso.Utility.UsefulStuff` 取用目標與 props，如同專案可以取用 AppLogger。</span><span class="sxs-lookup"><span data-stu-id="d272a-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="d272a-162">新增 PackageReference 條件</span><span class="sxs-lookup"><span data-stu-id="d272a-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="d272a-163">您可以使用條件來控制是否包含套件，這些條件可以使用任何 MSBuild 變數或在目標或 props 檔案中定義的變數。</span><span class="sxs-lookup"><span data-stu-id="d272a-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="d272a-164">但目前只支援 `TargetFramework` 變數。</span><span class="sxs-lookup"><span data-stu-id="d272a-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="d272a-165">例如，假設您的目標是 `netstandard1.4` 以及 `net452`，但所擁有的相依性只適用於 `net452`。</span><span class="sxs-lookup"><span data-stu-id="d272a-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="d272a-166">在此情況下，您不希望取用套件的 `netstandard1.4` 專案新增該項不必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="d272a-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="d272a-167">為避免這個問題，您要在 `PackageReference` 指定條件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d272a-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="d272a-168">使用此專案的套件組建會顯示 Newtonsoft.Json 隨附為相依性，但僅適用於 `net452` 目標：</span><span class="sxs-lookup"><span data-stu-id="d272a-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![使用 VS2017 對 PackageReference 套用條件的結果](media/PackageReference-Condition.png)

<span data-ttu-id="d272a-170">條件也可以套用在 `ItemGroup` 層級，並且套用至所有子系 `PackageReference` 項目：</span><span class="sxs-lookup"><span data-stu-id="d272a-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="d272a-171">鎖定相依性</span><span class="sxs-lookup"><span data-stu-id="d272a-171">Locking dependencies</span></span>
<span data-ttu-id="d272a-172">*NuGet **4.9** 或更新版本搭配 Visual Studio 2017 **15.9** 或更新版本提供此功能。*</span><span class="sxs-lookup"><span data-stu-id="d272a-172">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="d272a-173">對 NuGet 還原的輸入是一組來自專案檔 (頂層或直接相依性) 的套件參考，而輸出是完整的套件相依性終止，包括可轉移相依性。</span><span class="sxs-lookup"><span data-stu-id="d272a-173">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="d272a-174">若輸入 PackageReference 清單未變更，NuGet 會嘗試一律產生相同的完整套件相依性終止。</span><span class="sxs-lookup"><span data-stu-id="d272a-174">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="d272a-175">不過，在一些情況下，無法這樣做。</span><span class="sxs-lookup"><span data-stu-id="d272a-175">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="d272a-176">例如：</span><span class="sxs-lookup"><span data-stu-id="d272a-176">For example:</span></span>

* <span data-ttu-id="d272a-177">當您使用如 `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 的浮動版本時。</span><span class="sxs-lookup"><span data-stu-id="d272a-177">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="d272a-178">雖然這裡的目的是在次套件還原時浮動到最新版本，在某些案例中，使用者在收到明確手勢時需要圖形鎖定為特定最新版本並浮動到更新的版本 (如果可用)。</span><span class="sxs-lookup"><span data-stu-id="d272a-178">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="d272a-179">會發行符合 PackageReference 版本需求的的較新套件版本。</span><span class="sxs-lookup"><span data-stu-id="d272a-179">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="d272a-180">例如，</span><span class="sxs-lookup"><span data-stu-id="d272a-180">E.g.</span></span> 

  * <span data-ttu-id="d272a-181">第 1 天：若您指定 `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`，但 NuGet 存放庫上可用的版本是 4.1.0、4.2.0 與 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="d272a-181">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="d272a-182">在此案例中，NuGet would 將會解析為 4.1.0 (最接近的最小版本)</span><span class="sxs-lookup"><span data-stu-id="d272a-182">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="d272a-183">第 2 天：版本 4.0.0 發行。</span><span class="sxs-lookup"><span data-stu-id="d272a-183">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="d272a-184">NuGet 現在將會尋找精確相符項目並開始解析為 4.0.0</span><span class="sxs-lookup"><span data-stu-id="d272a-184">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="d272a-185">給定套件版本會從存放庫移除。</span><span class="sxs-lookup"><span data-stu-id="d272a-185">A given package version is removed from the repository.</span></span> <span data-ttu-id="d272a-186">雖然 nuget.org 不允許套件刪除，但並非所有套件存放庫都有此限制式。</span><span class="sxs-lookup"><span data-stu-id="d272a-186">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="d272a-187">這會導致 NuGet 在無法解析為已刪除版本時尋找最佳相符項目。</span><span class="sxs-lookup"><span data-stu-id="d272a-187">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="d272a-188">啟用鎖定檔案</span><span class="sxs-lookup"><span data-stu-id="d272a-188">Enabling lock file</span></span>
<span data-ttu-id="d272a-189">若要保存完整的套件相依性終止，您可以透過設定專案的 MSBuild 屬性 `RestorePackagesWithLockFile` 來選擇啟用鎖定檔案功能：</span><span class="sxs-lookup"><span data-stu-id="d272a-189">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="d272a-190">若已設定此屬性，NuGet 還原將會產生鎖定檔案，也就是專案根目錄中列出所有套件相依性的 `packages.lock.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d272a-190">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="d272a-191">一旦專案的根目錄中有 `packages.lock.json` 檔案，就一律會使用鎖定檔案來進行還原，即使是未設定 `RestorePackagesWithLockFile` 屬性也一樣。</span><span class="sxs-lookup"><span data-stu-id="d272a-191">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="d272a-192">因此，選擇啟用此功能的另一個方式在專案根目錄中建立虛設空白 `packages.lock.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d272a-192">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="d272a-193">具有鎖定檔案的 `restore` 行為</span><span class="sxs-lookup"><span data-stu-id="d272a-193">`restore` behavior with lock file</span></span>
<span data-ttu-id="d272a-194">若專案有鎖定檔案存在，NuGet 會使用此所鎖定檔案來執行 `restore`。</span><span class="sxs-lookup"><span data-stu-id="d272a-194">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="d272a-195">NuGet 會執行快速檢查以查看套件相依性中是否有變更，如專案檔 (或相依專案的檔案) 所述，而且若沒有變更，它只會還原鎖定檔案中所述的套件。</span><span class="sxs-lookup"><span data-stu-id="d272a-195">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="d272a-196">不會重新評估套件相依性。</span><span class="sxs-lookup"><span data-stu-id="d272a-196">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="d272a-197">若 NuGet 偵測到定義相依性中的變更 (如專案檔中所述)，它會重新評估套件圖表並更新鎖定檔案以反映專案的新套件終止。</span><span class="sxs-lookup"><span data-stu-id="d272a-197">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="d272a-198">針對 CI/CD 與其他案例，若不想即時變更套件相依性，您可以將 `lockedmode` 設定為 `true`：</span><span class="sxs-lookup"><span data-stu-id="d272a-198">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="d272a-199">針對 dotnet.exe，請執行：</span><span class="sxs-lookup"><span data-stu-id="d272a-199">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="d272a-200">針對 msbuild.exe，請執行：</span><span class="sxs-lookup"><span data-stu-id="d272a-200">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="d272a-201">您也可以在您的專案檔中設定此條件式 MSBuild 屬性：</span><span class="sxs-lookup"><span data-stu-id="d272a-201">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="d272a-202">若鎖定模式是 `true`，還原將會還原鎖定檔案中所列的精確套件；若您在鎖定檔案建立之後更新專案的已定義套件相依性，則會失敗。</span><span class="sxs-lookup"><span data-stu-id="d272a-202">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="d272a-203">讓鎖定檔案成為您來源存放庫的一部分</span><span class="sxs-lookup"><span data-stu-id="d272a-203">Make lock file part of your source repository</span></span>
<span data-ttu-id="d272a-204">若您要建置應用程式，可執行檔與討論的專案是相依性鏈結的開頭，則請將鎖定檔案存回原始程式碼存放庫，讓 NuGet 可以在還原期間使用。</span><span class="sxs-lookup"><span data-stu-id="d272a-204">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="d272a-205">不過，若您的專案是您不會發行的程式庫專案，或是其他專案所相依的一般程式碼專案，您**不應該**將鎖定檔案存回為您原始程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="d272a-205">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="d272a-206">保留鎖定檔案並不會造成傷害，但在還原/建置相依於此一般程式碼專案的專案時，無法使用一般程式碼專案的鎖定套件相依性，如鎖定檔案中所列。</span><span class="sxs-lookup"><span data-stu-id="d272a-206">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="d272a-207">例如：</span><span class="sxs-lookup"><span data-stu-id="d272a-207">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="d272a-208">若 `ProjectA` 有對 `PackageX` 版本 `2.0.0` 的相依性，而且也參考相依於 `PackageX` 版本 `1.0.0` 的 `ProjectB`，則 `ProjectB` 的鎖定檔案將會列出對 `PackageX` 版本 `1.0.0` 的相依性。</span><span class="sxs-lookup"><span data-stu-id="d272a-208">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="d272a-209">不過，當建置 `ProjectA` 時，其鎖定檔案將會包含對 `PackageX` 版本 **`2.0.0`** 的相依性，而**非** `1.0.0` (如 `ProjectB` 的鎖定檔案所列)。</span><span class="sxs-lookup"><span data-stu-id="d272a-209">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="d272a-210">因此，一般程式碼專案的鎖定檔案對於相依於它之專案的解析套件沒有多大決定權。</span><span class="sxs-lookup"><span data-stu-id="d272a-210">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="d272a-211">鎖定檔案擴充性</span><span class="sxs-lookup"><span data-stu-id="d272a-211">Lock file extensibility</span></span>
<span data-ttu-id="d272a-212">您使用鎖定檔案來控制還原的各種行為，如下所述：</span><span class="sxs-lookup"><span data-stu-id="d272a-212">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="d272a-213">選項</span><span class="sxs-lookup"><span data-stu-id="d272a-213">Option</span></span> | <span data-ttu-id="d272a-214">MSBuild 同等選項</span><span class="sxs-lookup"><span data-stu-id="d272a-214">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="d272a-215">專案的鎖定檔案啟動程序使用。</span><span class="sxs-lookup"><span data-stu-id="d272a-215">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="d272a-216">或者，您可以在專案檔中設定 `RestorePackagesWithLockFile` 屬性</span><span class="sxs-lookup"><span data-stu-id="d272a-216">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="d272a-217">針對還原啟用鎖定模式。</span><span class="sxs-lookup"><span data-stu-id="d272a-217">Enables locked mode for restore.</span></span> <span data-ttu-id="d272a-218">這在您想要取得可重複組建的 CI/CD 案例中非常實用。</span><span class="sxs-lookup"><span data-stu-id="d272a-218">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="d272a-219">透過將 `RestoreLockedMode` MSBuild 屬性設定為 `true`，就可以達到這個目的</span><span class="sxs-lookup"><span data-stu-id="d272a-219">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="d272a-220">對於專案中已定義浮動版本的套件而言，此選項非常實用。</span><span class="sxs-lookup"><span data-stu-id="d272a-220">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="d272a-221">根據預設，NuGet 還原將不會在每次還原時自動更新套件版本，除非您搭配 `--force-evaluate` 選項執行還原。</span><span class="sxs-lookup"><span data-stu-id="d272a-221">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="d272a-222">為專案定義自訂鎖定檔案位置。</span><span class="sxs-lookup"><span data-stu-id="d272a-222">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="d272a-223">這也可以透過設定 MSBuild 屬性 `NuGetLockFilePath` 來完成。</span><span class="sxs-lookup"><span data-stu-id="d272a-223">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="d272a-224">根據預設，NuGet 支援根目錄的 `packages.lock.json`。</span><span class="sxs-lookup"><span data-stu-id="d272a-224">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="d272a-225">若您在相同的目錄中有多個專案，NuGet 支援專案特定鎖定檔案 `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="d272a-225">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
