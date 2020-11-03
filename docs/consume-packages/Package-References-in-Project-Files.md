---
title: NuGet PackageReference 格式 (專案檔中的套件參考)
description: NuGet 4.0+ 和 VS2017 及 .NET Core 2.0 所支援之專案檔中的 NuGet PackageReference 詳細資料
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237636"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="043a3-103">專案檔中的套件參考 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="043a3-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="043a3-104">套件參考使用 `PackageReference` 節點，直接在專案檔中管理 NuGet 相依性 (而不是在個別的 `packages.config` 檔案中)。</span><span class="sxs-lookup"><span data-stu-id="043a3-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="043a3-105">使用 PackageReference 不會影響 NuGet 的其他方面；例如，仍會套用 `NuGet.config` 檔案中的設定 (包括套件來源)，如[常用的 NuGet 組態](configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="043a3-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="043a3-106">使用 PackageReference，您也可以使用 MSBuild 條件來選擇每個目標 framework 的套件參考，或其他群組。</span><span class="sxs-lookup"><span data-stu-id="043a3-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="043a3-107">它也允許對相依性和內容流動進行細微控制。</span><span class="sxs-lookup"><span data-stu-id="043a3-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="043a3-108">(如需詳細資訊，請參閱 [NuGet pack and restore as MSBuild targetsNuGet](../reference/msbuild-targets.md) (NuGet 以 pack 與 restore 作為 MSBuild 目標)。)</span><span class="sxs-lookup"><span data-stu-id="043a3-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="043a3-109">專案類型支援</span><span class="sxs-lookup"><span data-stu-id="043a3-109">Project type support</span></span>

<span data-ttu-id="043a3-110">根據預設，PackageReference 會用於以 Windows 10 組建 15063 (Creators Update) 及更新版本為目標的 .NET Core 專案、.NET Standard 專案和 UWP 專案 (C++ UWP 專案除外)。</span><span class="sxs-lookup"><span data-stu-id="043a3-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="043a3-111">.NET Framework 專案支援 PackageReference，但目前預設為 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="043a3-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="043a3-112">若要使用 PackageReference，請將相依性從 `packages.config`[移轉](../consume-packages/migrate-packages-config-to-package-reference.md)至您的專案檔，然後移除 packages.config。</span><span class="sxs-lookup"><span data-stu-id="043a3-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="043a3-113">以完整的 .NET Framework 為目標的 ASP.NET 應用程式僅包含 PackageReference 的[有限支援](https://github.com/NuGet/Home/issues/5877) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="043a3-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="043a3-114">不支援 C++ 和 JavaScript 專案類型。</span><span class="sxs-lookup"><span data-stu-id="043a3-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="043a3-115">新增 PackageReference</span><span class="sxs-lookup"><span data-stu-id="043a3-115">Adding a PackageReference</span></span>

<span data-ttu-id="043a3-116">使用下列語法在專案檔中新增相依性：</span><span class="sxs-lookup"><span data-stu-id="043a3-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="043a3-117">控制相依性版本</span><span class="sxs-lookup"><span data-stu-id="043a3-117">Controlling dependency version</span></span>

<span data-ttu-id="043a3-118">指定套件版本的慣例和使用 `packages.config` 時一樣：</span><span class="sxs-lookup"><span data-stu-id="043a3-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="043a3-119">在上述範例中，3.6.0 表示 >=3.6.0 的任何版本，但偏好最低版本，如[套件版本控制](../concepts/package-versioning.md#version-ranges)中所述。</span><span class="sxs-lookup"><span data-stu-id="043a3-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="043a3-120">針對沒有任何 PackageReference 的專案使用 PackageReference</span><span class="sxs-lookup"><span data-stu-id="043a3-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="043a3-121">進階：如果專案中未安裝任何套件 (專案檔中沒有 PackageReference，也沒有 packages.config 檔案)，但希望專案能還原為 PackageReference 樣式，您可以在您的專案檔中將專案屬性 RestoreProjectStyle 設為 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="043a3-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="043a3-122">如果您的參考專案為 PackageReference 樣式 (現有的 csproj 或 SDK 樣式專案)，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="043a3-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="043a3-123">這會讓這些專案參考的套件成為您專案「過渡性」參考的套件。</span><span class="sxs-lookup"><span data-stu-id="043a3-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="043a3-124">PackageReference 和來源</span><span class="sxs-lookup"><span data-stu-id="043a3-124">PackageReference and sources</span></span>

<span data-ttu-id="043a3-125">在 PackageReference 專案中，可轉移的相依性版本會在還原時進行解析。</span><span class="sxs-lookup"><span data-stu-id="043a3-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="043a3-126">因此，在 PackageReference 專案中，所有來源都必須可用於所有還原。</span><span class="sxs-lookup"><span data-stu-id="043a3-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="043a3-127">浮動版本</span><span class="sxs-lookup"><span data-stu-id="043a3-127">Floating Versions</span></span>

<span data-ttu-id="043a3-128">[浮動版本](../concepts/dependency-resolution.md#floating-versions)支援 `PackageReference`：</span><span class="sxs-lookup"><span data-stu-id="043a3-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="043a3-129">控制相依性資產</span><span class="sxs-lookup"><span data-stu-id="043a3-129">Controlling dependency assets</span></span>

<span data-ttu-id="043a3-130">您可能純粹使用相依性作為開發載入器，不想要對取用套件的專案公開。</span><span class="sxs-lookup"><span data-stu-id="043a3-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="043a3-131">在此案例中，您可以使用 `PrivateAssets` 中繼資料控制這個行為。</span><span class="sxs-lookup"><span data-stu-id="043a3-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="043a3-132">下列中繼資料標記控制相依性資產：</span><span class="sxs-lookup"><span data-stu-id="043a3-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="043a3-133">標籤</span><span class="sxs-lookup"><span data-stu-id="043a3-133">Tag</span></span> | <span data-ttu-id="043a3-134">描述</span><span class="sxs-lookup"><span data-stu-id="043a3-134">Description</span></span> | <span data-ttu-id="043a3-135">預設值</span><span class="sxs-lookup"><span data-stu-id="043a3-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="043a3-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="043a3-136">IncludeAssets</span></span> | <span data-ttu-id="043a3-137">會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="043a3-137">These assets will be consumed</span></span> | <span data-ttu-id="043a3-138">all</span><span class="sxs-lookup"><span data-stu-id="043a3-138">all</span></span> |
| <span data-ttu-id="043a3-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="043a3-139">ExcludeAssets</span></span> | <span data-ttu-id="043a3-140">不會取用這些資產</span><span class="sxs-lookup"><span data-stu-id="043a3-140">These assets will not be consumed</span></span> | <span data-ttu-id="043a3-141">無</span><span class="sxs-lookup"><span data-stu-id="043a3-141">none</span></span> |
| <span data-ttu-id="043a3-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="043a3-142">PrivateAssets</span></span> | <span data-ttu-id="043a3-143">會取用這些資產，但不會流動至父專案</span><span class="sxs-lookup"><span data-stu-id="043a3-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="043a3-144">contentfiles;分析器;建置</span><span class="sxs-lookup"><span data-stu-id="043a3-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="043a3-145">這些標記的可允許值如下，使用分號隔開多個值，但 `all` 和 `none` 必須單獨出現：</span><span class="sxs-lookup"><span data-stu-id="043a3-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="043a3-146">值</span><span class="sxs-lookup"><span data-stu-id="043a3-146">Value</span></span> | <span data-ttu-id="043a3-147">描述</span><span class="sxs-lookup"><span data-stu-id="043a3-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="043a3-148">compile</span><span class="sxs-lookup"><span data-stu-id="043a3-148">compile</span></span> | <span data-ttu-id="043a3-149">`lib` 資料夾的內容，以及專案是否能對該資料夾內的組件進行編譯的控制項</span><span class="sxs-lookup"><span data-stu-id="043a3-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="043a3-150">執行階段</span><span class="sxs-lookup"><span data-stu-id="043a3-150">runtime</span></span> | <span data-ttu-id="043a3-151">`lib` 與 `runtimes` 資料夾的內容，以及是否能將這些組件複製到組建輸出目錄的控制項</span><span class="sxs-lookup"><span data-stu-id="043a3-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="043a3-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="043a3-152">contentFiles</span></span> | <span data-ttu-id="043a3-153">`contentfiles` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="043a3-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="043a3-154">build</span><span class="sxs-lookup"><span data-stu-id="043a3-154">build</span></span> | <span data-ttu-id="043a3-155">`build` 資料夾中的 `.props` 與 `.targets`</span><span class="sxs-lookup"><span data-stu-id="043a3-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="043a3-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="043a3-156">buildMultitargeting</span></span> | <span data-ttu-id="043a3-157">用於跨架構目標的 *(4.0)* `.props` 與 `buildMultitargeting` 資料夾中的 `.targets`</span><span class="sxs-lookup"><span data-stu-id="043a3-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="043a3-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="043a3-158">buildTransitive</span></span> | <span data-ttu-id="043a3-159">*(5.0+)`buildTransitive` 資料夾中的* `.props` 與 `.targets`，用於可傳遞至任何取用專案的資產。</span><span class="sxs-lookup"><span data-stu-id="043a3-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="043a3-160">請參閱[功能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)頁面 \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="043a3-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="043a3-161">analyzers</span><span class="sxs-lookup"><span data-stu-id="043a3-161">analyzers</span></span> | <span data-ttu-id="043a3-162">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="043a3-162">.NET analyzers</span></span> |
| <span data-ttu-id="043a3-163">native</span><span class="sxs-lookup"><span data-stu-id="043a3-163">native</span></span> | <span data-ttu-id="043a3-164">`native` 資料夾的內容</span><span class="sxs-lookup"><span data-stu-id="043a3-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="043a3-165">無</span><span class="sxs-lookup"><span data-stu-id="043a3-165">none</span></span> | <span data-ttu-id="043a3-166">以上皆不使用。</span><span class="sxs-lookup"><span data-stu-id="043a3-166">None of the above are used.</span></span> |
| <span data-ttu-id="043a3-167">all</span><span class="sxs-lookup"><span data-stu-id="043a3-167">all</span></span> | <span data-ttu-id="043a3-168">以上全部 (除了`none`)</span><span class="sxs-lookup"><span data-stu-id="043a3-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="043a3-169">在下列範例中，除來自套件的內容檔案之外的所有項目都會被專案取用，除內容檔案和分析器之外的所有項目都會流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="043a3-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="043a3-170">請注意，因為 `build` 不隨附於 `PrivateAssets`，所以目標與 props「會」  流動至父專案。</span><span class="sxs-lookup"><span data-stu-id="043a3-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="043a3-171">例如，考慮到上述參考會用在建置名為 AppLogger 之 NuGet 套件的專案中。</span><span class="sxs-lookup"><span data-stu-id="043a3-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="043a3-172">AppLogger 可從 `Contoso.Utility.UsefulStuff` 取用目標與 props，如同專案可以取用 AppLogger。</span><span class="sxs-lookup"><span data-stu-id="043a3-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="043a3-173">在 `.nuspec` 檔案中，當 `developmentDependency` 設定為 `true` 時可讓套件成為僅限開發相依性，這可防止套件被包含為其他套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="043a3-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="043a3-174">使用 PackageReference *(NuGet 4.8+)* 時，此旗標也表示它在編譯時會排除編譯時間資產。</span><span class="sxs-lookup"><span data-stu-id="043a3-174">With PackageReference *(NuGet 4.8+)* , this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="043a3-175">如需詳細資訊，請參閱 [PackageReference 的 DevelopmentDependency 支援](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="043a3-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="043a3-176">新增 PackageReference 條件</span><span class="sxs-lookup"><span data-stu-id="043a3-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="043a3-177">您可以使用條件來控制是否包含套件，這些條件可以使用任何 MSBuild 變數或在目標或 props 檔案中定義的變數。</span><span class="sxs-lookup"><span data-stu-id="043a3-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="043a3-178">但目前只支援 `TargetFramework` 變數。</span><span class="sxs-lookup"><span data-stu-id="043a3-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="043a3-179">例如，假設您的目標是 `netstandard1.4` 以及 `net452`，但所擁有的相依性只適用於 `net452`。</span><span class="sxs-lookup"><span data-stu-id="043a3-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="043a3-180">在此情況下，您不希望取用套件的 `netstandard1.4` 專案新增該項不必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="043a3-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="043a3-181">為避免這個問題，您要在 `PackageReference` 指定條件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="043a3-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="043a3-182">使用此專案的套件組建會顯示 Newtonsoft.Json 隨附為相依性，但僅適用於 `net452` 目標：</span><span class="sxs-lookup"><span data-stu-id="043a3-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![使用 VS2017 對 PackageReference 套用條件的結果](media/PackageReference-Condition.png)

<span data-ttu-id="043a3-184">條件也可以套用在 `ItemGroup` 層級，並且套用至所有子系 `PackageReference` 項目：</span><span class="sxs-lookup"><span data-stu-id="043a3-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="043a3-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="043a3-185">GeneratePathProperty</span></span>

<span data-ttu-id="043a3-186">這項功能適用于 NuGet **5.0** 或更新版本，以及 Visual Studio 2019 **16.0** 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="043a3-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="043a3-187">有時候，最好從 MSBuild 目標參考封裝中的檔案。</span><span class="sxs-lookup"><span data-stu-id="043a3-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="043a3-188">在以專案 `packages.config` 為基礎的專案中，套件會安裝在相對於專案檔的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="043a3-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="043a3-189">不過，在 PackageReference 中，封裝 [會從](../concepts/package-installation-process.md)*全域套件* 資料夾取用，而這可能會因電腦而異。</span><span class="sxs-lookup"><span data-stu-id="043a3-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="043a3-190">為了橋接該間距，NuGet 引進了一個屬性，該屬性指向將取用封裝的位置。</span><span class="sxs-lookup"><span data-stu-id="043a3-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="043a3-191">範例：</span><span class="sxs-lookup"><span data-stu-id="043a3-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="043a3-192">此外，NuGet 會自動為包含 tools 資料夾的套件產生屬性。</span><span class="sxs-lookup"><span data-stu-id="043a3-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="043a3-193">MSBuild 屬性和套件身分識別沒有相同的限制，因此必須將套件身分識別變更為 MSBuild 易記名稱，並在前面加上文字 `Pkg` 。</span><span class="sxs-lookup"><span data-stu-id="043a3-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="043a3-194">若要確認所產生屬性的確切名稱，請查看產生的 [.props](../reference/msbuild-targets.md#restore-outputs) 檔案。</span><span class="sxs-lookup"><span data-stu-id="043a3-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="043a3-195">NuGet 警告和錯誤</span><span class="sxs-lookup"><span data-stu-id="043a3-195">NuGet warnings and errors</span></span>

<span data-ttu-id="043a3-196">*這項功能適用于 NuGet **4.3** 或更新版本，以及 Visual Studio 2017 **15.3** 或更新版本。*</span><span class="sxs-lookup"><span data-stu-id="043a3-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="043a3-197">在許多套件和還原案例中，所有的 NuGet 警告和錯誤都會進行編碼，並從開始 `NU****` 。</span><span class="sxs-lookup"><span data-stu-id="043a3-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="043a3-198">所有 NuGet 警告和錯誤都會列在 [參考](../reference/errors-and-warnings.md) 檔中。</span><span class="sxs-lookup"><span data-stu-id="043a3-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="043a3-199">NuGet 會觀察下列警告屬性：</span><span class="sxs-lookup"><span data-stu-id="043a3-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="043a3-200">`TreatWarningsAsErrors`，將所有警告視為錯誤</span><span class="sxs-lookup"><span data-stu-id="043a3-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="043a3-201">`WarningsAsErrors`，將特定警告視為錯誤</span><span class="sxs-lookup"><span data-stu-id="043a3-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="043a3-202">`NoWarn`，隱藏特定的警告，可能是整個專案或整個套件。</span><span class="sxs-lookup"><span data-stu-id="043a3-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="043a3-203">範例：</span><span class="sxs-lookup"><span data-stu-id="043a3-203">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="043a3-204">隱藏 NuGet 警告</span><span class="sxs-lookup"><span data-stu-id="043a3-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="043a3-205">雖然建議您在封裝和還原作業期間解決所有的 NuGet 警告，但在某些情況下，這些警告仍有保證。</span><span class="sxs-lookup"><span data-stu-id="043a3-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="043a3-206">若要隱藏警告專案範圍，請考慮執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="043a3-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="043a3-207">有時警告只適用于圖形中的特定套件。</span><span class="sxs-lookup"><span data-stu-id="043a3-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="043a3-208">我們可以選擇 `NoWarn` 在 PackageReference 專案上加入，以更有選擇性地隱藏該警告。</span><span class="sxs-lookup"><span data-stu-id="043a3-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="043a3-209">隱藏 Visual Studio 中的 NuGet 套件警告</span><span class="sxs-lookup"><span data-stu-id="043a3-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="043a3-210">當 Visual Studio 時，您也可以透過 IDE [隱藏警告](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) 。</span><span class="sxs-lookup"><span data-stu-id="043a3-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="043a3-211">鎖定相依性</span><span class="sxs-lookup"><span data-stu-id="043a3-211">Locking dependencies</span></span>

<span data-ttu-id="043a3-212">*NuGet **4.9** 或更新版本搭配 Visual Studio 2017 **15.9** 或更新版本提供此功能。*</span><span class="sxs-lookup"><span data-stu-id="043a3-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="043a3-213">對 NuGet 還原的輸入是一組來自專案檔 (頂層或直接相依性) 的套件參考，而輸出是完整的套件相依性終止，包括可轉移相依性。</span><span class="sxs-lookup"><span data-stu-id="043a3-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="043a3-214">若輸入 PackageReference 清單未變更，NuGet 會嘗試一律產生相同的完整套件相依性終止。</span><span class="sxs-lookup"><span data-stu-id="043a3-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="043a3-215">不過，在一些情況下，無法這樣做。</span><span class="sxs-lookup"><span data-stu-id="043a3-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="043a3-216">例如：</span><span class="sxs-lookup"><span data-stu-id="043a3-216">For example:</span></span>

* <span data-ttu-id="043a3-217">當您使用如 `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 的浮動版本時。</span><span class="sxs-lookup"><span data-stu-id="043a3-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="043a3-218">雖然這裡的目的是在次套件還原時浮動到最新版本，在某些案例中，使用者在收到明確手勢時需要圖形鎖定為特定最新版本並浮動到更新的版本 (如果可用)。</span><span class="sxs-lookup"><span data-stu-id="043a3-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="043a3-219">會發行符合 PackageReference 版本需求的的較新套件版本。</span><span class="sxs-lookup"><span data-stu-id="043a3-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="043a3-220">例如</span><span class="sxs-lookup"><span data-stu-id="043a3-220">E.g.</span></span> 

  * <span data-ttu-id="043a3-221">第 1 天：若您指定 `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`，但 NuGet 存放庫上可用的版本是 4.1.0、4.2.0 與 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="043a3-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="043a3-222">在此案例中，NuGet would 將會解析為 4.1.0 (最接近的最小版本)</span><span class="sxs-lookup"><span data-stu-id="043a3-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="043a3-223">第 2 天：版本 4.0.0 發行。</span><span class="sxs-lookup"><span data-stu-id="043a3-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="043a3-224">NuGet 現在將會尋找精確相符項目並開始解析為 4.0.0</span><span class="sxs-lookup"><span data-stu-id="043a3-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="043a3-225">給定套件版本會從存放庫移除。</span><span class="sxs-lookup"><span data-stu-id="043a3-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="043a3-226">雖然 nuget.org 不允許套件刪除，但並非所有套件存放庫都有此限制式。</span><span class="sxs-lookup"><span data-stu-id="043a3-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="043a3-227">這會導致 NuGet 在無法解析為已刪除版本時尋找最佳相符項目。</span><span class="sxs-lookup"><span data-stu-id="043a3-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="043a3-228">啟用鎖定檔案</span><span class="sxs-lookup"><span data-stu-id="043a3-228">Enabling lock file</span></span>

<span data-ttu-id="043a3-229">若要保存完整的套件相依性終止，您可以透過設定專案的 MSBuild 屬性 `RestorePackagesWithLockFile` 來選擇啟用鎖定檔案功能：</span><span class="sxs-lookup"><span data-stu-id="043a3-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="043a3-230">若已設定此屬性，NuGet 還原將會產生鎖定檔案，也就是專案根目錄中列出所有套件相依性的 `packages.lock.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="043a3-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="043a3-231">一旦專案的根目錄中有 `packages.lock.json` 檔案，就一律會使用鎖定檔案來進行還原，即使是未設定 `RestorePackagesWithLockFile` 屬性也一樣。</span><span class="sxs-lookup"><span data-stu-id="043a3-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="043a3-232">因此，選擇啟用此功能的另一個方式在專案根目錄中建立虛設空白 `packages.lock.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="043a3-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="043a3-233">具有鎖定檔案的 `restore` 行為</span><span class="sxs-lookup"><span data-stu-id="043a3-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="043a3-234">若專案有鎖定檔案存在，NuGet 會使用此所鎖定檔案來執行 `restore`。</span><span class="sxs-lookup"><span data-stu-id="043a3-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="043a3-235">NuGet 會執行快速檢查以查看套件相依性中是否有變更，如專案檔 (或相依專案的檔案) 所述，而且若沒有變更，它只會還原鎖定檔案中所述的套件。</span><span class="sxs-lookup"><span data-stu-id="043a3-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="043a3-236">不會重新評估套件相依性。</span><span class="sxs-lookup"><span data-stu-id="043a3-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="043a3-237">若 NuGet 偵測到定義相依性中的變更 (如專案檔中所述)，它會重新評估套件圖表並更新鎖定檔案以反映專案的新套件終止。</span><span class="sxs-lookup"><span data-stu-id="043a3-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="043a3-238">針對 CI/CD 與其他案例，若不想即時變更套件相依性，您可以將 `lockedmode` 設定為 `true`：</span><span class="sxs-lookup"><span data-stu-id="043a3-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="043a3-239">針對 dotnet.exe，請執行：</span><span class="sxs-lookup"><span data-stu-id="043a3-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="043a3-240">針對 msbuild.exe，請執行：</span><span class="sxs-lookup"><span data-stu-id="043a3-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="043a3-241">您也可以在您的專案檔中設定此條件式 MSBuild 屬性：</span><span class="sxs-lookup"><span data-stu-id="043a3-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="043a3-242">若鎖定模式是 `true`，還原將會還原鎖定檔案中所列的精確套件；若您在鎖定檔案建立之後更新專案的已定義套件相依性，則會失敗。</span><span class="sxs-lookup"><span data-stu-id="043a3-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="043a3-243">讓鎖定檔案成為您來源存放庫的一部分</span><span class="sxs-lookup"><span data-stu-id="043a3-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="043a3-244">若您要建置應用程式，可執行檔與討論的專案是相依性鏈結的開頭，則請將鎖定檔案存回原始程式碼存放庫，讓 NuGet 可以在還原期間使用。</span><span class="sxs-lookup"><span data-stu-id="043a3-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="043a3-245">不過，若您的專案是您不會發行的程式庫專案，或是其他專案所相依的一般程式碼專案，您 **不應該** 將鎖定檔案存回為您原始程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="043a3-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="043a3-246">保留鎖定檔案並不會造成傷害，但在還原/建置相依於此一般程式碼專案的專案時，無法使用一般程式碼專案的鎖定套件相依性，如鎖定檔案中所列。</span><span class="sxs-lookup"><span data-stu-id="043a3-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="043a3-247">例如：</span><span class="sxs-lookup"><span data-stu-id="043a3-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="043a3-248">若 `ProjectA` 有對 `PackageX` 版本 `2.0.0` 的相依性，而且也參考相依於 `PackageX` 版本 `1.0.0` 的 `ProjectB`，則 `ProjectB` 的鎖定檔案將會列出對 `PackageX` 版本 `1.0.0` 的相依性。</span><span class="sxs-lookup"><span data-stu-id="043a3-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="043a3-249">不過，當 `ProjectA` 建立時，其鎖定檔案將會包含版本的相依性， `PackageX` **`2.0.0`** 而 **不** 會包含 `1.0.0` 的鎖定檔案中所列 `ProjectB` 的相依性。</span><span class="sxs-lookup"><span data-stu-id="043a3-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="043a3-250">因此，一般程式碼專案的鎖定檔案對於相依於它之專案的解析套件沒有多大決定權。</span><span class="sxs-lookup"><span data-stu-id="043a3-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="043a3-251">鎖定檔案擴充性</span><span class="sxs-lookup"><span data-stu-id="043a3-251">Lock file extensibility</span></span>

<span data-ttu-id="043a3-252">您使用鎖定檔案來控制還原的各種行為，如下所述：</span><span class="sxs-lookup"><span data-stu-id="043a3-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="043a3-253">NuGet.exe 選項</span><span class="sxs-lookup"><span data-stu-id="043a3-253">NuGet.exe option</span></span> | <span data-ttu-id="043a3-254">dotnet 選項</span><span class="sxs-lookup"><span data-stu-id="043a3-254">dotnet option</span></span> | <span data-ttu-id="043a3-255">MSBuild 同等選項</span><span class="sxs-lookup"><span data-stu-id="043a3-255">MSBuild equivalent option</span></span> | <span data-ttu-id="043a3-256">Description</span><span class="sxs-lookup"><span data-stu-id="043a3-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="043a3-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="043a3-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="043a3-258">選擇使用鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="043a3-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="043a3-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="043a3-259">RestoreLockedMode</span></span> | <span data-ttu-id="043a3-260">針對還原啟用鎖定模式。</span><span class="sxs-lookup"><span data-stu-id="043a3-260">Enables locked mode for restore.</span></span> <span data-ttu-id="043a3-261">這在您想要可重複組建的 CI/CD 案例中很有用。</span><span class="sxs-lookup"><span data-stu-id="043a3-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="043a3-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="043a3-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="043a3-263">對於專案中已定義浮動版本的套件而言，此選項非常實用。</span><span class="sxs-lookup"><span data-stu-id="043a3-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="043a3-264">根據預設，除非您使用此選項執行還原，否則 NuGet 還原不會在每次還原時自動更新套件版本。</span><span class="sxs-lookup"><span data-stu-id="043a3-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="043a3-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="043a3-265">NuGetLockFilePath</span></span> | <span data-ttu-id="043a3-266">為專案定義自訂鎖定檔案位置。</span><span class="sxs-lookup"><span data-stu-id="043a3-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="043a3-267">根據預設，NuGet 支援根目錄的 `packages.lock.json`。</span><span class="sxs-lookup"><span data-stu-id="043a3-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="043a3-268">若您在相同的目錄中有多個專案，NuGet 支援專案特定鎖定檔案 `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="043a3-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
