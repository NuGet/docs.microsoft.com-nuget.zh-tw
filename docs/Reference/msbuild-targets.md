---
title: "NuGet 封裝和還原為 MSBuild 目標 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。"
keywords: "NuGet 和 MSBuild、NuGet 封裝目標、NuGet 還原目標"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 798b3550718294072d86b6e4827ec5017178d2cc
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5159c-104">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="5159c-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5159c-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="5159c-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="5159c-106">利用 PackageReference 格式，NuGet 4.0+ 可以在專案檔內直接儲存所有資訊清單中繼資料，而非使用個別的 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5159c-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="5159c-107">使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。</span><span class="sxs-lookup"><span data-stu-id="5159c-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5159c-108">這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。</span><span class="sxs-lookup"><span data-stu-id="5159c-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5159c-109">(在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令)。</span><span class="sxs-lookup"><span data-stu-id="5159c-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="5159c-110">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="5159c-110">Target build order</span></span>

<span data-ttu-id="5159c-111">因為 `pack` 和 `restore` 是 MSBuild 目標，所以您可以存取它們，以加強工作流程。</span><span class="sxs-lookup"><span data-stu-id="5159c-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5159c-112">例如，假設您想要在封裝套件之後，將套件複製至網路共用。</span><span class="sxs-lookup"><span data-stu-id="5159c-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5159c-113">做法是在專案檔中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="5159c-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="5159c-114">同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，以及在 MSBuild 工作中使用 NuGet 屬性。</span><span class="sxs-lookup"><span data-stu-id="5159c-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5159c-115">封裝目標</span><span class="sxs-lookup"><span data-stu-id="5159c-115">pack target</span></span>

<span data-ttu-id="5159c-116">使用封裝目標 (即 `msbuild /t:pack`) 時，MSBuild 會從專案檔獲得其輸入。</span><span class="sxs-lookup"><span data-stu-id="5159c-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="5159c-117">下表描述可新增至第一個 `<PropertyGroup>` 節點內之專案檔的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="5159c-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5159c-118">以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。</span><span class="sxs-lookup"><span data-stu-id="5159c-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5159c-119">為了方便起見，資料表是依 [`.nuspec` 檔案](../reference/nuspec.md)中的對等屬性進行組織。</span><span class="sxs-lookup"><span data-stu-id="5159c-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="5159c-120">請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5159c-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="5159c-121">屬性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="5159c-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5159c-122">MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="5159c-122">MSBuild Property</span></span> | <span data-ttu-id="5159c-123">預設</span><span class="sxs-lookup"><span data-stu-id="5159c-123">Default</span></span> | <span data-ttu-id="5159c-124">注意</span><span class="sxs-lookup"><span data-stu-id="5159c-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5159c-125">ID</span><span class="sxs-lookup"><span data-stu-id="5159c-125">Id</span></span> | <span data-ttu-id="5159c-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="5159c-126">PackageId</span></span> | <span data-ttu-id="5159c-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5159c-127">AssemblyName</span></span> | <span data-ttu-id="5159c-128">MSBuild 中的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="5159c-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5159c-129">版本</span><span class="sxs-lookup"><span data-stu-id="5159c-129">Version</span></span> | <span data-ttu-id="5159c-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5159c-130">PackageVersion</span></span> | <span data-ttu-id="5159c-131">版本</span><span class="sxs-lookup"><span data-stu-id="5159c-131">Version</span></span> | <span data-ttu-id="5159c-132">這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="5159c-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5159c-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5159c-133">VersionPrefix</span></span> | <span data-ttu-id="5159c-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5159c-134">PackageVersionPrefix</span></span> | <span data-ttu-id="5159c-135">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-135">empty</span></span> | <span data-ttu-id="5159c-136">設定 PackageVersion 會覆寫 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5159c-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="5159c-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5159c-137">VersionSuffix</span></span> | <span data-ttu-id="5159c-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5159c-138">PackageVersionSuffix</span></span> | <span data-ttu-id="5159c-139">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-139">empty</span></span> | <span data-ttu-id="5159c-140">MSBuild 中的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="5159c-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5159c-141">設定 PackageVersion 會覆寫 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5159c-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="5159c-142">作者</span><span class="sxs-lookup"><span data-stu-id="5159c-142">Authors</span></span> | <span data-ttu-id="5159c-143">作者</span><span class="sxs-lookup"><span data-stu-id="5159c-143">Authors</span></span> | <span data-ttu-id="5159c-144">目前使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="5159c-144">Username of the current user</span></span> | |
| <span data-ttu-id="5159c-145">Owners</span><span class="sxs-lookup"><span data-stu-id="5159c-145">Owners</span></span> | <span data-ttu-id="5159c-146">N/A</span><span class="sxs-lookup"><span data-stu-id="5159c-146">N/A</span></span> | <span data-ttu-id="5159c-147">NuSpec 中沒有</span><span class="sxs-lookup"><span data-stu-id="5159c-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5159c-148">標題</span><span class="sxs-lookup"><span data-stu-id="5159c-148">Title</span></span> | <span data-ttu-id="5159c-149">標題</span><span class="sxs-lookup"><span data-stu-id="5159c-149">Title</span></span> | <span data-ttu-id="5159c-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="5159c-150">The PackageId</span></span>| |
| <span data-ttu-id="5159c-151">描述</span><span class="sxs-lookup"><span data-stu-id="5159c-151">Description</span></span> | <span data-ttu-id="5159c-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="5159c-152">PackageDescription</span></span> | <span data-ttu-id="5159c-153">"Package Description"</span><span class="sxs-lookup"><span data-stu-id="5159c-153">"Package Description"</span></span> | |
| <span data-ttu-id="5159c-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="5159c-154">Copyright</span></span> | <span data-ttu-id="5159c-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="5159c-155">Copyright</span></span> | <span data-ttu-id="5159c-156">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-156">empty</span></span> | |
| <span data-ttu-id="5159c-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5159c-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5159c-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5159c-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5159c-159">False</span><span class="sxs-lookup"><span data-stu-id="5159c-159">false</span></span> | |
| <span data-ttu-id="5159c-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-160">LicenseUrl</span></span> | <span data-ttu-id="5159c-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-161">PackageLicenseUrl</span></span> | <span data-ttu-id="5159c-162">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-162">empty</span></span> | |
| <span data-ttu-id="5159c-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-163">ProjectUrl</span></span> | <span data-ttu-id="5159c-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-164">PackageProjectUrl</span></span> | <span data-ttu-id="5159c-165">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-165">empty</span></span> | |
| <span data-ttu-id="5159c-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-166">IconUrl</span></span> | <span data-ttu-id="5159c-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-167">PackageIconUrl</span></span> | <span data-ttu-id="5159c-168">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-168">empty</span></span> | |
| <span data-ttu-id="5159c-169">Tags</span><span class="sxs-lookup"><span data-stu-id="5159c-169">Tags</span></span> | <span data-ttu-id="5159c-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5159c-170">PackageTags</span></span> | <span data-ttu-id="5159c-171">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-171">empty</span></span> | <span data-ttu-id="5159c-172">以分號來分隔標記。</span><span class="sxs-lookup"><span data-stu-id="5159c-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5159c-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5159c-173">ReleaseNotes</span></span> | <span data-ttu-id="5159c-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5159c-174">PackageReleaseNotes</span></span> | <span data-ttu-id="5159c-175">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-175">empty</span></span> | |
| <span data-ttu-id="5159c-176">儲存機制/Url</span><span class="sxs-lookup"><span data-stu-id="5159c-176">Repository/Url</span></span> | <span data-ttu-id="5159c-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-177">RepositoryUrl</span></span> | <span data-ttu-id="5159c-178">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-178">empty</span></span> | <span data-ttu-id="5159c-179">用來複製或擷取原始程式碼儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="5159c-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="5159c-180">範例： *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="5159c-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="5159c-181">儲存機制/類型</span><span class="sxs-lookup"><span data-stu-id="5159c-181">Repository/Type</span></span> | <span data-ttu-id="5159c-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5159c-182">RepositoryType</span></span> | <span data-ttu-id="5159c-183">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-183">empty</span></span> | <span data-ttu-id="5159c-184">儲存機制類型。</span><span class="sxs-lookup"><span data-stu-id="5159c-184">Repository type.</span></span> <span data-ttu-id="5159c-185">範例： *git*， *tfs*。</span><span class="sxs-lookup"><span data-stu-id="5159c-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="5159c-186">儲存機制/分支</span><span class="sxs-lookup"><span data-stu-id="5159c-186">Repository/Branch</span></span> | <span data-ttu-id="5159c-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5159c-187">RepositoryBranch</span></span> | <span data-ttu-id="5159c-188">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-188">empty</span></span> | <span data-ttu-id="5159c-189">選擇性的儲存機制分支的資訊。</span><span class="sxs-lookup"><span data-stu-id="5159c-189">Optional repository branch information.</span></span> <span data-ttu-id="5159c-190">*RepositoryUrl*也必須指定要包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="5159c-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5159c-191">範例：*主要*(NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="5159c-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5159c-192">儲存機制/認可</span><span class="sxs-lookup"><span data-stu-id="5159c-192">Repository/Commit</span></span> | <span data-ttu-id="5159c-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5159c-193">RepositoryCommit</span></span> | <span data-ttu-id="5159c-194">空白</span><span class="sxs-lookup"><span data-stu-id="5159c-194">empty</span></span> | <span data-ttu-id="5159c-195">選擇性的儲存機制認可或變更集，以表示其來源封裝已針對所建立。</span><span class="sxs-lookup"><span data-stu-id="5159c-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="5159c-196">*RepositoryUrl*也必須指定要包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="5159c-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5159c-197">範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="5159c-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5159c-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="5159c-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5159c-199">總結</span><span class="sxs-lookup"><span data-stu-id="5159c-199">Summary</span></span> | <span data-ttu-id="5159c-200">不支援</span><span class="sxs-lookup"><span data-stu-id="5159c-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="5159c-201">封裝目標輸入</span><span class="sxs-lookup"><span data-stu-id="5159c-201">pack target inputs</span></span>

- <span data-ttu-id="5159c-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="5159c-202">IsPackable</span></span>
- <span data-ttu-id="5159c-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5159c-203">PackageVersion</span></span>
- <span data-ttu-id="5159c-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="5159c-204">PackageId</span></span>
- <span data-ttu-id="5159c-205">作者</span><span class="sxs-lookup"><span data-stu-id="5159c-205">Authors</span></span>
- <span data-ttu-id="5159c-206">描述</span><span class="sxs-lookup"><span data-stu-id="5159c-206">Description</span></span>
- <span data-ttu-id="5159c-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="5159c-207">Copyright</span></span>
- <span data-ttu-id="5159c-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5159c-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5159c-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5159c-209">DevelopmentDependency</span></span>
- <span data-ttu-id="5159c-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="5159c-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-211">PackageProjectUrl</span></span>
- <span data-ttu-id="5159c-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-212">PackageIconUrl</span></span>
- <span data-ttu-id="5159c-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5159c-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="5159c-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5159c-214">PackageTags</span></span>
- <span data-ttu-id="5159c-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5159c-215">PackageOutputPath</span></span>
- <span data-ttu-id="5159c-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5159c-216">IncludeSymbols</span></span>
- <span data-ttu-id="5159c-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5159c-217">IncludeSource</span></span>
- <span data-ttu-id="5159c-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5159c-218">PackageTypes</span></span>
- <span data-ttu-id="5159c-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="5159c-219">IsTool</span></span>
- <span data-ttu-id="5159c-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-220">RepositoryUrl</span></span>
- <span data-ttu-id="5159c-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5159c-221">RepositoryType</span></span>
- <span data-ttu-id="5159c-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5159c-222">RepositoryBranch</span></span>
- <span data-ttu-id="5159c-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5159c-223">RepositoryCommit</span></span>
- <span data-ttu-id="5159c-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5159c-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="5159c-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5159c-225">MinClientVersion</span></span>
- <span data-ttu-id="5159c-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5159c-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="5159c-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5159c-227">IncludeContentInPack</span></span>
- <span data-ttu-id="5159c-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5159c-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5159c-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5159c-229">ContentTargetFolders</span></span>
- <span data-ttu-id="5159c-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="5159c-230">NuspecFile</span></span>
- <span data-ttu-id="5159c-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="5159c-231">NuspecBasePath</span></span>
- <span data-ttu-id="5159c-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="5159c-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5159c-233">封裝案例</span><span class="sxs-lookup"><span data-stu-id="5159c-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5159c-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5159c-234">PackageIconUrl</span></span>

<span data-ttu-id="5159c-235">隨著 [NuGet 問題 2582](https://github.com/NuGet/Home/issues/2582) 的變更，`PackageIconUrl` 最後會變更為 `PackageIconUri`，而且可以是圖示檔的相對路徑，而圖示檔包含在所產生套件的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="5159c-235">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5159c-236">輸出組件</span><span class="sxs-lookup"><span data-stu-id="5159c-236">Output assemblies</span></span>

<span data-ttu-id="5159c-237">`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="5159c-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5159c-238">所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。</span><span class="sxs-lookup"><span data-stu-id="5159c-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5159c-239">在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：</span><span class="sxs-lookup"><span data-stu-id="5159c-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5159c-240">`IncludeBuildOutput`：布林值，決定是否應該在套件中包含組建輸出組件。</span><span class="sxs-lookup"><span data-stu-id="5159c-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5159c-241">`BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5159c-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5159c-242">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5159c-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5159c-243">套件參考</span><span class="sxs-lookup"><span data-stu-id="5159c-243">Package references</span></span>

<span data-ttu-id="5159c-244">請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。</span><span class="sxs-lookup"><span data-stu-id="5159c-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5159c-245">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="5159c-245">Project to project references</span></span>

<span data-ttu-id="5159c-246">預設會將專案對專案參考視為 NuGet 套件參考，例如：</span><span class="sxs-lookup"><span data-stu-id="5159c-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5159c-247">您也可以將下列中繼資料新增至您的專案參考：</span><span class="sxs-lookup"><span data-stu-id="5159c-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5159c-248">在套件內包含內容</span><span class="sxs-lookup"><span data-stu-id="5159c-248">Including content in a package</span></span>

<span data-ttu-id="5159c-249">若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。</span><span class="sxs-lookup"><span data-stu-id="5159c-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5159c-250">除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：</span><span class="sxs-lookup"><span data-stu-id="5159c-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="5159c-251">除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="5159c-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5159c-252">如果您想要將所有內容都只複製至特定根資料夾 (而不是 `content` 和 `contentFiles`)，則可以使用 MSBuild 屬性 `ContentTargetFolders`，其預設為 "content;contentFiles"，但可以設定為任何其他資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="5159c-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5159c-253">請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。</span><span class="sxs-lookup"><span data-stu-id="5159c-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5159c-254">`PackagePath` 可以是以分號分隔的一組目標路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5159c-255">指定空的套件路徑會將檔案新增至套件的根目錄。</span><span class="sxs-lookup"><span data-stu-id="5159c-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5159c-256">例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：</span><span class="sxs-lookup"><span data-stu-id="5159c-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5159c-257">另有 MSBuild 屬性 `$(IncludeContentInPack)` 預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="5159c-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5159c-258">如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。</span><span class="sxs-lookup"><span data-stu-id="5159c-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5159c-259">您可在上述任何項目上設定的其他封裝特定中繼資料包含 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，其在輸出 nuspec 的 ```contentFiles``` 項目上設定 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="5159c-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="5159c-260">除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="5159c-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5159c-261">針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5159c-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5159c-262">IncludeSymbols</span></span>

<span data-ttu-id="5159c-263">使用 `MSBuild /t:pack /p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。</span><span class="sxs-lookup"><span data-stu-id="5159c-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5159c-264">請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。</span><span class="sxs-lookup"><span data-stu-id="5159c-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5159c-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5159c-265">IncludeSource</span></span>

<span data-ttu-id="5159c-266">這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5159c-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5159c-267">所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="5159c-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5159c-268">這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="5159c-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5159c-269">若類型為 Compile 的檔案位於專案資料夾之外，就只會將其新增至 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="5159c-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="5159c-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="5159c-270">IsTool</span></span>

<span data-ttu-id="5159c-271">使用 `MSBuild /t:pack /p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5159c-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5159c-272">請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。</span><span class="sxs-lookup"><span data-stu-id="5159c-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5159c-273">使用 .nuspec 封裝</span><span class="sxs-lookup"><span data-stu-id="5159c-273">Packing using a .nuspec</span></span>

<span data-ttu-id="5159c-274">您可以使用 `.nuspec` 檔案來封裝專案，前提是您讓專案檔匯入 `NuGet.Build.Tasks.Pack.targets`，以執行封裝工作。</span><span class="sxs-lookup"><span data-stu-id="5159c-274">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5159c-275">下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：</span><span class="sxs-lookup"><span data-stu-id="5159c-275">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5159c-276">`NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-276">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5159c-277">`NuspecProperties`：以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="5159c-277">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5159c-278">基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`/p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="5159c-278">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5159c-279">`NuspecBasePath`：`.nuspec` 檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-279">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5159c-280">如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="5159c-280">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5159c-281">如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="5159c-281">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="5159c-282">還原目標</span><span class="sxs-lookup"><span data-stu-id="5159c-282">restore target</span></span>

<span data-ttu-id="5159c-283">`MSBuild /t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5159c-283">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5159c-284">讀取所有專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="5159c-284">Read all project to project references</span></span>
1. <span data-ttu-id="5159c-285">讀取專案屬性來尋找中繼資料夾和目標架構</span><span class="sxs-lookup"><span data-stu-id="5159c-285">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5159c-286">將 msbuild 資料傳遞至 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="5159c-286">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5159c-287">執行還原</span><span class="sxs-lookup"><span data-stu-id="5159c-287">Run restore</span></span>
1. <span data-ttu-id="5159c-288">下載套件</span><span class="sxs-lookup"><span data-stu-id="5159c-288">Download packages</span></span>
1. <span data-ttu-id="5159c-289">撰寫資產檔案、目標和屬性</span><span class="sxs-lookup"><span data-stu-id="5159c-289">Write assets file, targets, and props</span></span>

> [!Note]
> <span data-ttu-id="5159c-290">`restore` MSBuild 目標只適用於使用專案`PackageReference`項目，且不會還原封裝使用參考`packages.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="5159c-290">The `restore` MSBuild target only works for projects using `PackageReference` items and does not restore packages referenced using a `packages.config` file.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="5159c-291">還原屬性</span><span class="sxs-lookup"><span data-stu-id="5159c-291">Restore properties</span></span>

<span data-ttu-id="5159c-292">其他還原設定可能來自專案檔中的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="5159c-292">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5159c-293">您也可以從命令列，使用 `/p:` 參數設定值 (請參閱下列＜範例＞)。</span><span class="sxs-lookup"><span data-stu-id="5159c-293">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5159c-294">屬性</span><span class="sxs-lookup"><span data-stu-id="5159c-294">Property</span></span> | <span data-ttu-id="5159c-295">描述</span><span class="sxs-lookup"><span data-stu-id="5159c-295">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5159c-296">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5159c-296">RestoreSources</span></span> | <span data-ttu-id="5159c-297">以分號分隔的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="5159c-297">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5159c-298">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5159c-298">RestorePackagesPath</span></span> | <span data-ttu-id="5159c-299">使用者套件資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-299">User packages folder path.</span></span> |
| <span data-ttu-id="5159c-300">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5159c-300">RestoreDisableParallel</span></span> | <span data-ttu-id="5159c-301">限制逐一進行下載。</span><span class="sxs-lookup"><span data-stu-id="5159c-301">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5159c-302">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5159c-302">RestoreConfigFile</span></span> | <span data-ttu-id="5159c-303">要套用之 `Nuget.Config` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-303">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5159c-304">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5159c-304">RestoreNoCache</span></span> | <span data-ttu-id="5159c-305">如果為 true，請避免使用 Web 快取。</span><span class="sxs-lookup"><span data-stu-id="5159c-305">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="5159c-306">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5159c-306">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5159c-307">如果為 true，請忽略失敗或遺漏的套件來源。</span><span class="sxs-lookup"><span data-stu-id="5159c-307">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5159c-308">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5159c-308">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5159c-309">`NuGet.Build.Tasks.dll` 的路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-309">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5159c-310">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5159c-310">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5159c-311">要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="5159c-311">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5159c-312">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="5159c-312">RestoreOutputPath</span></span> | <span data-ttu-id="5159c-313">輸出資料夾，預設為 `obj` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5159c-313">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="5159c-314">範例</span><span class="sxs-lookup"><span data-stu-id="5159c-314">Examples</span></span>

<span data-ttu-id="5159c-315">命令列：</span><span class="sxs-lookup"><span data-stu-id="5159c-315">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="5159c-316">專案檔：</span><span class="sxs-lookup"><span data-stu-id="5159c-316">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5159c-317">Restore outputs</span><span class="sxs-lookup"><span data-stu-id="5159c-317">Restore outputs</span></span>

<span data-ttu-id="5159c-318">還原會在組建 `obj` 資料夾中建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="5159c-318">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5159c-319">檔案</span><span class="sxs-lookup"><span data-stu-id="5159c-319">File</span></span> | <span data-ttu-id="5159c-320">描述</span><span class="sxs-lookup"><span data-stu-id="5159c-320">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5159c-321">先前是 `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="5159c-321">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5159c-322">套件中所含 MSBuild 屬性的參考</span><span class="sxs-lookup"><span data-stu-id="5159c-322">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5159c-323">套件中所含 MSBuild 目標的參考</span><span class="sxs-lookup"><span data-stu-id="5159c-323">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="5159c-324">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5159c-324">PackageTargetFallback</span></span>

<span data-ttu-id="5159c-325">`PackageTargetFallback` 項目可讓您指定一組要在還原套件時使用的相容目標。</span><span class="sxs-lookup"><span data-stu-id="5159c-325">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="5159c-326">其設計目的是要讓使用 dotnet [TxM](../reference/target-frameworks.md) 的套件可以與未宣告 dotnet TxM 的相容套件一起運作。</span><span class="sxs-lookup"><span data-stu-id="5159c-326">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5159c-327">也就是說，如果您的專案使用 dotnet TxM，除非您將 `<PackageTargetFallback>` 新增至專案，以讓非 dotnet 平台變成與 dotnet 相容，否則其相依的所有套件也必須要有 dotnet TxM。</span><span class="sxs-lookup"><span data-stu-id="5159c-327">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="5159c-328">例如，如果專案使用 `netstandard1.6` TxM，而且相依套件僅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，則無法建置專案。</span><span class="sxs-lookup"><span data-stu-id="5159c-328">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5159c-329">如果您想要匯入的是第二個 DLL，則可以如下新增 `PackageTargetFallback`，指出 `portable-net45+win81` DLL 相容：</span><span class="sxs-lookup"><span data-stu-id="5159c-329">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5159c-330">若要宣告專案中所有目標的後援，請省略 `Condition` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5159c-330">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5159c-331">您也可以包含 `$(PackageTargetFallback)` 來擴充任何現有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5159c-331">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5159c-332">取代還原圖形中的一個程式庫</span><span class="sxs-lookup"><span data-stu-id="5159c-332">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5159c-333">如果還原內含錯誤的組件，您可以排除該套件預設選項，並將其取代為您自己的選項。</span><span class="sxs-lookup"><span data-stu-id="5159c-333">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5159c-334">首先，會有最上層 `PackageReference`，但排除所有資產：</span><span class="sxs-lookup"><span data-stu-id="5159c-334">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5159c-335">接下來，新增您自己對 DLL 之適當本機複本的參考：</span><span class="sxs-lookup"><span data-stu-id="5159c-335">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
