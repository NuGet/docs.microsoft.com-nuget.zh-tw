---
title: "NuGet 封裝和還原為 MSBuild 目標 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。"
keywords: "NuGet 和 MSBuild、NuGet 封裝目標、NuGet 還原目標"
ms.reviewer: karann-msft
ms.openlocfilehash: def01380e5bc3bf878e72dd437f52cd033641ca5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="3e1ff-104">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="3e1ff-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="3e1ff-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="3e1ff-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="3e1ff-106">NuGet 4.0+ 可以直接與 `.csproj` 檔案中的資訊搭配運作，而不需要個別的 `.nuspec` 或 `project.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="3e1ff-107">所有先前儲存在這些組態檔中的中繼資料都可以改為直接儲存在 `.csproj` 檔案中，如這裡所述。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="3e1ff-108">使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="3e1ff-109">這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="3e1ff-110">(在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令)。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="3e1ff-111">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-111">In this topic:</span></span>

- [<span data-ttu-id="3e1ff-112">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="3e1ff-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="3e1ff-113">封裝目標</span><span class="sxs-lookup"><span data-stu-id="3e1ff-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="3e1ff-114">封裝案例</span><span class="sxs-lookup"><span data-stu-id="3e1ff-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="3e1ff-115">還原目標</span><span class="sxs-lookup"><span data-stu-id="3e1ff-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="3e1ff-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3e1ff-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="3e1ff-117">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="3e1ff-117">Target build order</span></span>

<span data-ttu-id="3e1ff-118">因為 `pack` 和 `restore` 是 MSBuild 目標，所以您可以存取它們，以加強工作流程。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="3e1ff-119">例如，假設您想要在封裝套件之後，將套件複製至網路共用。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="3e1ff-120">做法是在專案檔中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="3e1ff-121">同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，以及在 MSBuild 工作中使用 NuGet 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="3e1ff-122">封裝目標</span><span class="sxs-lookup"><span data-stu-id="3e1ff-122">pack target</span></span>

<span data-ttu-id="3e1ff-123">使用封裝目標 (即 `msbuild /t:pack`) 時，MSBuild 會從 `.csproj` 檔案獲得其輸入，而不是從 `project.json` 或 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="3e1ff-124">下表描述第一個 `<PropertyGroup>` 節點內可新增至 `.csproj` 檔案的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="3e1ff-125">以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="3e1ff-126">為了方便起見，資料表是依 [`.nuspec` 檔案](../schema/nuspec.md)中的對等屬性進行組織。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="3e1ff-127">請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="3e1ff-128">屬性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="3e1ff-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="3e1ff-129">MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="3e1ff-129">MSBuild Property</span></span> | <span data-ttu-id="3e1ff-130">預設</span><span class="sxs-lookup"><span data-stu-id="3e1ff-130">Default</span></span> | <span data-ttu-id="3e1ff-131">注意</span><span class="sxs-lookup"><span data-stu-id="3e1ff-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="3e1ff-132">ID</span><span class="sxs-lookup"><span data-stu-id="3e1ff-132">Id</span></span> | <span data-ttu-id="3e1ff-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="3e1ff-133">PackageId</span></span> | <span data-ttu-id="3e1ff-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="3e1ff-134">AssemblyName</span></span> | <span data-ttu-id="3e1ff-135">MSBuild 中的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="3e1ff-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="3e1ff-136">版本</span><span class="sxs-lookup"><span data-stu-id="3e1ff-136">Version</span></span> | <span data-ttu-id="3e1ff-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3e1ff-137">PackageVersion</span></span> | <span data-ttu-id="3e1ff-138">版本</span><span class="sxs-lookup"><span data-stu-id="3e1ff-138">Version</span></span> | <span data-ttu-id="3e1ff-139">這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="3e1ff-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="3e1ff-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3e1ff-140">VersionPrefix</span></span> | <span data-ttu-id="3e1ff-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3e1ff-141">PackageVersionPrefix</span></span> | <span data-ttu-id="3e1ff-142">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-142">empty</span></span> | <span data-ttu-id="3e1ff-143">設定 PackageVersion 將會覆寫 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3e1ff-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="3e1ff-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3e1ff-144">VersionSuffix</span></span> | <span data-ttu-id="3e1ff-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3e1ff-145">PackageVersionSuffix</span></span> | <span data-ttu-id="3e1ff-146">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-146">empty</span></span> | <span data-ttu-id="3e1ff-147">MSBuild 中的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="3e1ff-148">設定 PackageVersion 將會覆寫 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3e1ff-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="3e1ff-149">作者</span><span class="sxs-lookup"><span data-stu-id="3e1ff-149">Authors</span></span> | <span data-ttu-id="3e1ff-150">作者</span><span class="sxs-lookup"><span data-stu-id="3e1ff-150">Authors</span></span> | <span data-ttu-id="3e1ff-151">目前使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="3e1ff-151">Username of the current user</span></span> | |
| <span data-ttu-id="3e1ff-152">Owners</span><span class="sxs-lookup"><span data-stu-id="3e1ff-152">Owners</span></span> | <span data-ttu-id="3e1ff-153">N/A</span><span class="sxs-lookup"><span data-stu-id="3e1ff-153">N/A</span></span> | <span data-ttu-id="3e1ff-154">NuSpec 中沒有</span><span class="sxs-lookup"><span data-stu-id="3e1ff-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="3e1ff-155">標題</span><span class="sxs-lookup"><span data-stu-id="3e1ff-155">Title</span></span> | <span data-ttu-id="3e1ff-156">標題</span><span class="sxs-lookup"><span data-stu-id="3e1ff-156">Title</span></span> | <span data-ttu-id="3e1ff-157">PackageId</span><span class="sxs-lookup"><span data-stu-id="3e1ff-157">The PackageId</span></span>| |
| <span data-ttu-id="3e1ff-158">說明</span><span class="sxs-lookup"><span data-stu-id="3e1ff-158">Description</span></span> | <span data-ttu-id="3e1ff-159">說明</span><span class="sxs-lookup"><span data-stu-id="3e1ff-159">Description</span></span> | <span data-ttu-id="3e1ff-160">"Package Description"</span><span class="sxs-lookup"><span data-stu-id="3e1ff-160">"Package Description"</span></span> | |
| <span data-ttu-id="3e1ff-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="3e1ff-161">Copyright</span></span> | <span data-ttu-id="3e1ff-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="3e1ff-162">Copyright</span></span> | <span data-ttu-id="3e1ff-163">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-163">empty</span></span> | |
| <span data-ttu-id="3e1ff-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3e1ff-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="3e1ff-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3e1ff-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="3e1ff-166">false</span><span class="sxs-lookup"><span data-stu-id="3e1ff-166">false</span></span> | |
| <span data-ttu-id="3e1ff-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-167">LicenseUrl</span></span> | <span data-ttu-id="3e1ff-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-168">PackageLicenseUrl</span></span> | <span data-ttu-id="3e1ff-169">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-169">empty</span></span> | |
| <span data-ttu-id="3e1ff-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-170">ProjectUrl</span></span> | <span data-ttu-id="3e1ff-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-171">PackageProjectUrl</span></span> | <span data-ttu-id="3e1ff-172">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-172">empty</span></span> | |
| <span data-ttu-id="3e1ff-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-173">IconUrl</span></span> | <span data-ttu-id="3e1ff-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-174">PackageIconUrl</span></span> | <span data-ttu-id="3e1ff-175">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-175">empty</span></span> | |
| <span data-ttu-id="3e1ff-176">Tags</span><span class="sxs-lookup"><span data-stu-id="3e1ff-176">Tags</span></span> | <span data-ttu-id="3e1ff-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3e1ff-177">PackageTags</span></span> | <span data-ttu-id="3e1ff-178">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-178">empty</span></span> | <span data-ttu-id="3e1ff-179">以分號來分隔標記。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="3e1ff-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3e1ff-180">ReleaseNotes</span></span> | <span data-ttu-id="3e1ff-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3e1ff-181">PackageReleaseNotes</span></span> | <span data-ttu-id="3e1ff-182">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-182">empty</span></span> | |
| <span data-ttu-id="3e1ff-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-183">RepositoryUrl</span></span> | <span data-ttu-id="3e1ff-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-184">RepositoryUrl</span></span> | <span data-ttu-id="3e1ff-185">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-185">empty</span></span> | |
| <span data-ttu-id="3e1ff-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3e1ff-186">RepositoryType</span></span> | <span data-ttu-id="3e1ff-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3e1ff-187">RepositoryType</span></span> | <span data-ttu-id="3e1ff-188">空白</span><span class="sxs-lookup"><span data-stu-id="3e1ff-188">empty</span></span> | |
| <span data-ttu-id="3e1ff-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="3e1ff-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="3e1ff-190">總結</span><span class="sxs-lookup"><span data-stu-id="3e1ff-190">Summary</span></span> | <span data-ttu-id="3e1ff-191">不支援</span><span class="sxs-lookup"><span data-stu-id="3e1ff-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="3e1ff-192">封裝目標輸入</span><span class="sxs-lookup"><span data-stu-id="3e1ff-192">pack target inputs</span></span>

- <span data-ttu-id="3e1ff-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="3e1ff-193">IsPackable</span></span>
- <span data-ttu-id="3e1ff-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3e1ff-194">PackageVersion</span></span>
- <span data-ttu-id="3e1ff-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="3e1ff-195">PackageId</span></span>
- <span data-ttu-id="3e1ff-196">作者</span><span class="sxs-lookup"><span data-stu-id="3e1ff-196">Authors</span></span>
- <span data-ttu-id="3e1ff-197">說明</span><span class="sxs-lookup"><span data-stu-id="3e1ff-197">Description</span></span>
- <span data-ttu-id="3e1ff-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="3e1ff-198">Copyright</span></span>
- <span data-ttu-id="3e1ff-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3e1ff-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="3e1ff-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="3e1ff-200">DevelopmentDependency</span></span>
- <span data-ttu-id="3e1ff-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="3e1ff-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-202">PackageProjectUrl</span></span>
- <span data-ttu-id="3e1ff-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-203">PackageIconUrl</span></span>
- <span data-ttu-id="3e1ff-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3e1ff-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="3e1ff-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3e1ff-205">PackageTags</span></span>
- <span data-ttu-id="3e1ff-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="3e1ff-206">PackageOutputPath</span></span>
- <span data-ttu-id="3e1ff-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3e1ff-207">IncludeSymbols</span></span>
- <span data-ttu-id="3e1ff-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3e1ff-208">IncludeSource</span></span>
- <span data-ttu-id="3e1ff-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="3e1ff-209">PackageTypes</span></span>
- <span data-ttu-id="3e1ff-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="3e1ff-210">IsTool</span></span>
- <span data-ttu-id="3e1ff-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-211">RepositoryUrl</span></span>
- <span data-ttu-id="3e1ff-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3e1ff-212">RepositoryType</span></span>
- <span data-ttu-id="3e1ff-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="3e1ff-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="3e1ff-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="3e1ff-214">MinClientVersion</span></span>
- <span data-ttu-id="3e1ff-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3e1ff-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="3e1ff-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="3e1ff-216">IncludeContentInPack</span></span>
- <span data-ttu-id="3e1ff-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="3e1ff-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="3e1ff-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="3e1ff-218">ContentTargetFolders</span></span>
- <span data-ttu-id="3e1ff-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="3e1ff-219">NuspecFile</span></span>
- <span data-ttu-id="3e1ff-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="3e1ff-220">NuspecBasePath</span></span>
- <span data-ttu-id="3e1ff-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="3e1ff-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="3e1ff-222">封裝案例</span><span class="sxs-lookup"><span data-stu-id="3e1ff-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="3e1ff-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3e1ff-223">PackageIconUrl</span></span>

<span data-ttu-id="3e1ff-224">隨著 [NuGet 問題 2582](https://github.com/NuGet/Home/issues/2582) 的變更，`PackageIconUrl` 最後會變更為 `PackageIconUri`，而且可以是圖示檔的相對路徑，而圖示檔包含在所產生套件的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="3e1ff-225">輸出組件</span><span class="sxs-lookup"><span data-stu-id="3e1ff-225">Output assemblies</span></span>

<span data-ttu-id="3e1ff-226">`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="3e1ff-227">所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="3e1ff-228">在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="3e1ff-229">`IncludeBuildOutput`：布林值，決定是否應該在套件中包含組建輸出組件。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="3e1ff-230">`BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="3e1ff-231">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="3e1ff-232">套件參考</span><span class="sxs-lookup"><span data-stu-id="3e1ff-232">Package references</span></span>

<span data-ttu-id="3e1ff-233">請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="3e1ff-234">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="3e1ff-234">Project to project references</span></span>

<span data-ttu-id="3e1ff-235">預設會將專案對專案參考視為 NuGet 套件參考，例如：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="3e1ff-236">您也可以將下列中繼資料新增至您的專案參考：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="3e1ff-237">在套件內包含內容</span><span class="sxs-lookup"><span data-stu-id="3e1ff-237">Including content in a package</span></span>

<span data-ttu-id="3e1ff-238">若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="3e1ff-239">除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="3e1ff-240">除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="3e1ff-241">如果您想要將所有內容都只複製至特定根資料夾 (而不是 `content` 和 `contentFiles`)，則可以使用 MSBuild 屬性 `ContentTargetFolders`，其預設為 "content;contentFiles"，但可以設定為任何其他資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="3e1ff-242">請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="3e1ff-243">`PackagePath` 可以是以分號分隔的一組目標路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="3e1ff-244">指定空的套件路徑會將檔案新增至套件的根目錄。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="3e1ff-245">例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="3e1ff-246">另有 MSBuild 屬性 `$(IncludeContentInPack)` 預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="3e1ff-247">如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="3e1ff-248">您可在上述任何項目上設定的其他封裝特定中繼資料包含 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，其在輸出 nuspec 的 ```contentFiles``` 項目上設定 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="3e1ff-249">除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="3e1ff-250">針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="3e1ff-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3e1ff-251">IncludeSymbols</span></span>

<span data-ttu-id="3e1ff-252">使用 `MSBuild /t:pack /p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="3e1ff-253">請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="3e1ff-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3e1ff-254">IncludeSource</span></span>

<span data-ttu-id="3e1ff-255">這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="3e1ff-256">所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="3e1ff-257">這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="3e1ff-258">如果 Compile 類型的檔案是在專案資料夾外部，則只會將它新增至 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-258">If a file of type Compile, is outside the project folder, then it is just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="3e1ff-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="3e1ff-259">IsTool</span></span>

<span data-ttu-id="3e1ff-260">使用 `MSBuild /t:pack /p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="3e1ff-261">請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="3e1ff-262">使用 .nuspec 封裝</span><span class="sxs-lookup"><span data-stu-id="3e1ff-262">Packing using a .nuspec</span></span>

<span data-ttu-id="3e1ff-263">您可以使用 `.nuspec` 檔案來封裝專案，前提是您讓專案檔匯入 `NuGet.Build.Tasks.Pack.targets`，以執行封裝工作。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="3e1ff-264">下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="3e1ff-265">`NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="3e1ff-266">`NuspecProperties`：以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="3e1ff-267">基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`/p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="3e1ff-268">`NuspecBasePath`：`.nuspec` 檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="3e1ff-269">如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3e1ff-270">如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="3e1ff-271">還原目標</span><span class="sxs-lookup"><span data-stu-id="3e1ff-271">restore target</span></span>

<span data-ttu-id="3e1ff-272">`MSBuild /t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="3e1ff-273">讀取所有專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="3e1ff-273">Read all project to project references</span></span>
1. <span data-ttu-id="3e1ff-274">讀取專案屬性來尋找中繼資料夾和目標架構</span><span class="sxs-lookup"><span data-stu-id="3e1ff-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="3e1ff-275">將 msbuild 資料傳遞至 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="3e1ff-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="3e1ff-276">執行還原</span><span class="sxs-lookup"><span data-stu-id="3e1ff-276">Run restore</span></span>
1. <span data-ttu-id="3e1ff-277">下載套件</span><span class="sxs-lookup"><span data-stu-id="3e1ff-277">Download packages</span></span>
1. <span data-ttu-id="3e1ff-278">撰寫資產檔案、目標和屬性</span><span class="sxs-lookup"><span data-stu-id="3e1ff-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="3e1ff-279">還原屬性</span><span class="sxs-lookup"><span data-stu-id="3e1ff-279">Restore properties</span></span>

<span data-ttu-id="3e1ff-280">其他還原設定可能來自專案檔中的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="3e1ff-281">您也可以從命令列，使用 `/p:` 參數設定值 (請參閱下列＜範例＞)。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="3e1ff-282">屬性</span><span class="sxs-lookup"><span data-stu-id="3e1ff-282">Property</span></span> | <span data-ttu-id="3e1ff-283">說明</span><span class="sxs-lookup"><span data-stu-id="3e1ff-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="3e1ff-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="3e1ff-284">RestoreSources</span></span> | <span data-ttu-id="3e1ff-285">以分號分隔的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="3e1ff-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="3e1ff-286">RestorePackagesPath</span></span> | <span data-ttu-id="3e1ff-287">使用者套件資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-287">User packages folder path.</span></span> |
| <span data-ttu-id="3e1ff-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="3e1ff-288">RestoreDisableParallel</span></span> | <span data-ttu-id="3e1ff-289">限制逐一進行下載。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="3e1ff-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="3e1ff-290">RestoreConfigFile</span></span> | <span data-ttu-id="3e1ff-291">要套用之 `Nuget.Config` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="3e1ff-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="3e1ff-292">RestoreNoCache</span></span> | <span data-ttu-id="3e1ff-293">如果為 true，請避免使用 Web 快取。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="3e1ff-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="3e1ff-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="3e1ff-295">如果為 true，請忽略失敗或遺漏的套件來源。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="3e1ff-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="3e1ff-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="3e1ff-297">`NuGet.Build.Tasks.dll` 的路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="3e1ff-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="3e1ff-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="3e1ff-299">要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="3e1ff-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="3e1ff-300">RestoreOutputPath</span></span> | <span data-ttu-id="3e1ff-301">輸出資料夾，預設為 `obj` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="3e1ff-302">**範例**</span><span class="sxs-lookup"><span data-stu-id="3e1ff-302">**Examples**</span></span>

<span data-ttu-id="3e1ff-303">命令列：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="3e1ff-304">專案檔：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="3e1ff-305">Restore outputs</span><span class="sxs-lookup"><span data-stu-id="3e1ff-305">Restore outputs</span></span>

<span data-ttu-id="3e1ff-306">還原會在組建 `obj` 資料夾中建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="3e1ff-307">檔案</span><span class="sxs-lookup"><span data-stu-id="3e1ff-307">File</span></span> | <span data-ttu-id="3e1ff-308">說明</span><span class="sxs-lookup"><span data-stu-id="3e1ff-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="3e1ff-309">先前是 `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="3e1ff-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="3e1ff-310">套件中所含 MSBuild 屬性的參考</span><span class="sxs-lookup"><span data-stu-id="3e1ff-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="3e1ff-311">套件中所含 MSBuild 目標的參考</span><span class="sxs-lookup"><span data-stu-id="3e1ff-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="3e1ff-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3e1ff-312">PackageTargetFallback</span></span> 

<span data-ttu-id="3e1ff-313">`PackageTargetFallback` 項目可讓您指定一組要在還原套件時使用的相容目標 ([`project.json` 中 `imports`](../schema/project-json.md#imports) 的對等項目)。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="3e1ff-314">其設計目的是要讓使用 dotnet [TxM](../schema/target-frameworks.md) 的套件可以與未宣告 dotnet TxM 的相容套件一起運作。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3e1ff-315">也就是說，如果您的專案使用 dotnet TxM，除非您將 `<PackageTargetFallback>` 新增至專案，以讓非 dotnet 平台變成與 dotnet 相容，否則其相依的所有套件也必須要有 dotnet TxM。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="3e1ff-316">例如，如果專案使用 `netstandard1.6` TxM，而且相依套件僅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，則無法建置專案。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="3e1ff-317">如果您想要匯入的是第二個 DLL，則可以如下新增 `PackageTargetFallback`，指出 `portable-net45+win81` DLL 相容：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="3e1ff-318">若要宣告專案中所有目標的後援，請省略 `Condition` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="3e1ff-319">您也可以包含 `$(PackageTargetFallback)` 來擴充任何現有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="3e1ff-320">取代還原圖形中的一個程式庫</span><span class="sxs-lookup"><span data-stu-id="3e1ff-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="3e1ff-321">如果還原內含錯誤的組件，則可能會排除該套件預設選項，並將它取代為您自己的選項。</span><span class="sxs-lookup"><span data-stu-id="3e1ff-321">If a restore is bringing the wrong assembly, it is possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="3e1ff-322">首先，會有最上層 `PackageReference`，但排除所有資產：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="3e1ff-323">接下來，新增您自己對 DLL 之適當本機複本的參考：</span><span class="sxs-lookup"><span data-stu-id="3e1ff-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
