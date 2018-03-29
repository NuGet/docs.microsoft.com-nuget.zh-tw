---
title: NuGet 封裝和還原為 MSBuild 目標 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。
keywords: NuGet 和 MSBuild、NuGet 封裝目標、NuGet 還原目標
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a9c2c2229d717dff8472dce0ba568e4a21900b19
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="49c0b-104">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="49c0b-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="49c0b-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="49c0b-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="49c0b-106">利用 PackageReference 格式，NuGet 4.0+ 可以在專案檔內直接儲存所有資訊清單中繼資料，而非使用個別的 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="49c0b-107">使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。</span><span class="sxs-lookup"><span data-stu-id="49c0b-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="49c0b-108">這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。</span><span class="sxs-lookup"><span data-stu-id="49c0b-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="49c0b-109">(在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令)。</span><span class="sxs-lookup"><span data-stu-id="49c0b-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="49c0b-110">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="49c0b-110">Target build order</span></span>

<span data-ttu-id="49c0b-111">因為 `pack` 和 `restore` 是 MSBuild 目標，所以您可以存取它們，以加強工作流程。</span><span class="sxs-lookup"><span data-stu-id="49c0b-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="49c0b-112">例如，假設您想要在封裝套件之後，將套件複製至網路共用。</span><span class="sxs-lookup"><span data-stu-id="49c0b-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="49c0b-113">做法是在專案檔中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="49c0b-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="49c0b-114">同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，以及在 MSBuild 工作中使用 NuGet 屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="49c0b-115">封裝目標</span><span class="sxs-lookup"><span data-stu-id="49c0b-115">pack target</span></span>

<span data-ttu-id="49c0b-116">PackageReference 格式，使用標準.NET 專案`msbuild /t:pack`繪製輸入来用來建立 NuGet 封裝的專案檔案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-116">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="49c0b-117">下表描述可新增至第一個 `<PropertyGroup>` 節點內之專案檔的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="49c0b-118">以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。</span><span class="sxs-lookup"><span data-stu-id="49c0b-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="49c0b-119">為了方便起見，資料表是依 [`.nuspec` 檔案](../reference/nuspec.md)中的對等屬性進行組織。</span><span class="sxs-lookup"><span data-stu-id="49c0b-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="49c0b-120">請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="49c0b-121">屬性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="49c0b-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="49c0b-122">MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="49c0b-122">MSBuild Property</span></span> | <span data-ttu-id="49c0b-123">預設</span><span class="sxs-lookup"><span data-stu-id="49c0b-123">Default</span></span> | <span data-ttu-id="49c0b-124">注意</span><span class="sxs-lookup"><span data-stu-id="49c0b-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="49c0b-125">ID</span><span class="sxs-lookup"><span data-stu-id="49c0b-125">Id</span></span> | <span data-ttu-id="49c0b-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="49c0b-126">PackageId</span></span> | <span data-ttu-id="49c0b-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="49c0b-127">AssemblyName</span></span> | <span data-ttu-id="49c0b-128">MSBuild 中的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="49c0b-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="49c0b-129">版本</span><span class="sxs-lookup"><span data-stu-id="49c0b-129">Version</span></span> | <span data-ttu-id="49c0b-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="49c0b-130">PackageVersion</span></span> | <span data-ttu-id="49c0b-131">版本</span><span class="sxs-lookup"><span data-stu-id="49c0b-131">Version</span></span> | <span data-ttu-id="49c0b-132">這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="49c0b-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="49c0b-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="49c0b-133">VersionPrefix</span></span> | <span data-ttu-id="49c0b-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="49c0b-134">PackageVersionPrefix</span></span> | <span data-ttu-id="49c0b-135">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-135">empty</span></span> | <span data-ttu-id="49c0b-136">設定 PackageVersion 會覆寫 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="49c0b-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="49c0b-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="49c0b-137">VersionSuffix</span></span> | <span data-ttu-id="49c0b-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="49c0b-138">PackageVersionSuffix</span></span> | <span data-ttu-id="49c0b-139">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-139">empty</span></span> | <span data-ttu-id="49c0b-140">MSBuild 中的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="49c0b-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="49c0b-141">設定 PackageVersion 會覆寫 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="49c0b-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="49c0b-142">作者</span><span class="sxs-lookup"><span data-stu-id="49c0b-142">Authors</span></span> | <span data-ttu-id="49c0b-143">作者</span><span class="sxs-lookup"><span data-stu-id="49c0b-143">Authors</span></span> | <span data-ttu-id="49c0b-144">目前使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="49c0b-144">Username of the current user</span></span> | |
| <span data-ttu-id="49c0b-145">Owners</span><span class="sxs-lookup"><span data-stu-id="49c0b-145">Owners</span></span> | <span data-ttu-id="49c0b-146">N/A</span><span class="sxs-lookup"><span data-stu-id="49c0b-146">N/A</span></span> | <span data-ttu-id="49c0b-147">NuSpec 中沒有</span><span class="sxs-lookup"><span data-stu-id="49c0b-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="49c0b-148">標題</span><span class="sxs-lookup"><span data-stu-id="49c0b-148">Title</span></span> | <span data-ttu-id="49c0b-149">標題</span><span class="sxs-lookup"><span data-stu-id="49c0b-149">Title</span></span> | <span data-ttu-id="49c0b-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="49c0b-150">The PackageId</span></span>| |
| <span data-ttu-id="49c0b-151">描述</span><span class="sxs-lookup"><span data-stu-id="49c0b-151">Description</span></span> | <span data-ttu-id="49c0b-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="49c0b-152">PackageDescription</span></span> | <span data-ttu-id="49c0b-153">"Package Description"</span><span class="sxs-lookup"><span data-stu-id="49c0b-153">"Package Description"</span></span> | |
| <span data-ttu-id="49c0b-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="49c0b-154">Copyright</span></span> | <span data-ttu-id="49c0b-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="49c0b-155">Copyright</span></span> | <span data-ttu-id="49c0b-156">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-156">empty</span></span> | |
| <span data-ttu-id="49c0b-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="49c0b-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="49c0b-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="49c0b-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="49c0b-159">False</span><span class="sxs-lookup"><span data-stu-id="49c0b-159">false</span></span> | |
| <span data-ttu-id="49c0b-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-160">LicenseUrl</span></span> | <span data-ttu-id="49c0b-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-161">PackageLicenseUrl</span></span> | <span data-ttu-id="49c0b-162">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-162">empty</span></span> | |
| <span data-ttu-id="49c0b-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-163">ProjectUrl</span></span> | <span data-ttu-id="49c0b-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-164">PackageProjectUrl</span></span> | <span data-ttu-id="49c0b-165">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-165">empty</span></span> | |
| <span data-ttu-id="49c0b-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-166">IconUrl</span></span> | <span data-ttu-id="49c0b-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-167">PackageIconUrl</span></span> | <span data-ttu-id="49c0b-168">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-168">empty</span></span> | |
| <span data-ttu-id="49c0b-169">Tags</span><span class="sxs-lookup"><span data-stu-id="49c0b-169">Tags</span></span> | <span data-ttu-id="49c0b-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="49c0b-170">PackageTags</span></span> | <span data-ttu-id="49c0b-171">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-171">empty</span></span> | <span data-ttu-id="49c0b-172">以分號來分隔標記。</span><span class="sxs-lookup"><span data-stu-id="49c0b-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="49c0b-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="49c0b-173">ReleaseNotes</span></span> | <span data-ttu-id="49c0b-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="49c0b-174">PackageReleaseNotes</span></span> | <span data-ttu-id="49c0b-175">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-175">empty</span></span> | |
| <span data-ttu-id="49c0b-176">儲存機制/Url</span><span class="sxs-lookup"><span data-stu-id="49c0b-176">Repository/Url</span></span> | <span data-ttu-id="49c0b-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-177">RepositoryUrl</span></span> | <span data-ttu-id="49c0b-178">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-178">empty</span></span> | <span data-ttu-id="49c0b-179">用來複製或擷取原始程式碼儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="49c0b-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="49c0b-180">範例： *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="49c0b-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="49c0b-181">儲存機制/類型</span><span class="sxs-lookup"><span data-stu-id="49c0b-181">Repository/Type</span></span> | <span data-ttu-id="49c0b-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="49c0b-182">RepositoryType</span></span> | <span data-ttu-id="49c0b-183">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-183">empty</span></span> | <span data-ttu-id="49c0b-184">儲存機制類型。</span><span class="sxs-lookup"><span data-stu-id="49c0b-184">Repository type.</span></span> <span data-ttu-id="49c0b-185">範例： *git*， *tfs*。</span><span class="sxs-lookup"><span data-stu-id="49c0b-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="49c0b-186">儲存機制/分支</span><span class="sxs-lookup"><span data-stu-id="49c0b-186">Repository/Branch</span></span> | <span data-ttu-id="49c0b-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="49c0b-187">RepositoryBranch</span></span> | <span data-ttu-id="49c0b-188">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-188">empty</span></span> | <span data-ttu-id="49c0b-189">選擇性的儲存機制分支的資訊。</span><span class="sxs-lookup"><span data-stu-id="49c0b-189">Optional repository branch information.</span></span> <span data-ttu-id="49c0b-190">*RepositoryUrl*也必須指定要包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="49c0b-191">範例：*主要*(NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="49c0b-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="49c0b-192">儲存機制/認可</span><span class="sxs-lookup"><span data-stu-id="49c0b-192">Repository/Commit</span></span> | <span data-ttu-id="49c0b-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="49c0b-193">RepositoryCommit</span></span> | <span data-ttu-id="49c0b-194">空白</span><span class="sxs-lookup"><span data-stu-id="49c0b-194">empty</span></span> | <span data-ttu-id="49c0b-195">選擇性的儲存機制認可或變更集，以表示其來源封裝已針對所建立。</span><span class="sxs-lookup"><span data-stu-id="49c0b-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="49c0b-196">*RepositoryUrl*也必須指定要包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="49c0b-197">範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="49c0b-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="49c0b-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="49c0b-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="49c0b-199">總結</span><span class="sxs-lookup"><span data-stu-id="49c0b-199">Summary</span></span> | <span data-ttu-id="49c0b-200">不支援</span><span class="sxs-lookup"><span data-stu-id="49c0b-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="49c0b-201">封裝目標輸入</span><span class="sxs-lookup"><span data-stu-id="49c0b-201">pack target inputs</span></span>

- <span data-ttu-id="49c0b-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="49c0b-202">IsPackable</span></span>
- <span data-ttu-id="49c0b-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="49c0b-203">PackageVersion</span></span>
- <span data-ttu-id="49c0b-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="49c0b-204">PackageId</span></span>
- <span data-ttu-id="49c0b-205">作者</span><span class="sxs-lookup"><span data-stu-id="49c0b-205">Authors</span></span>
- <span data-ttu-id="49c0b-206">描述</span><span class="sxs-lookup"><span data-stu-id="49c0b-206">Description</span></span>
- <span data-ttu-id="49c0b-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="49c0b-207">Copyright</span></span>
- <span data-ttu-id="49c0b-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="49c0b-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="49c0b-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="49c0b-209">DevelopmentDependency</span></span>
- <span data-ttu-id="49c0b-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="49c0b-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-211">PackageProjectUrl</span></span>
- <span data-ttu-id="49c0b-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-212">PackageIconUrl</span></span>
- <span data-ttu-id="49c0b-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="49c0b-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="49c0b-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="49c0b-214">PackageTags</span></span>
- <span data-ttu-id="49c0b-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="49c0b-215">PackageOutputPath</span></span>
- <span data-ttu-id="49c0b-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="49c0b-216">IncludeSymbols</span></span>
- <span data-ttu-id="49c0b-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="49c0b-217">IncludeSource</span></span>
- <span data-ttu-id="49c0b-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="49c0b-218">PackageTypes</span></span>
- <span data-ttu-id="49c0b-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="49c0b-219">IsTool</span></span>
- <span data-ttu-id="49c0b-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-220">RepositoryUrl</span></span>
- <span data-ttu-id="49c0b-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="49c0b-221">RepositoryType</span></span>
- <span data-ttu-id="49c0b-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="49c0b-222">RepositoryBranch</span></span>
- <span data-ttu-id="49c0b-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="49c0b-223">RepositoryCommit</span></span>
- <span data-ttu-id="49c0b-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="49c0b-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="49c0b-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="49c0b-225">MinClientVersion</span></span>
- <span data-ttu-id="49c0b-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="49c0b-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="49c0b-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="49c0b-227">IncludeContentInPack</span></span>
- <span data-ttu-id="49c0b-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="49c0b-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="49c0b-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="49c0b-229">ContentTargetFolders</span></span>
- <span data-ttu-id="49c0b-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="49c0b-230">NuspecFile</span></span>
- <span data-ttu-id="49c0b-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="49c0b-231">NuspecBasePath</span></span>
- <span data-ttu-id="49c0b-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="49c0b-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="49c0b-233">封裝案例</span><span class="sxs-lookup"><span data-stu-id="49c0b-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="49c0b-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="49c0b-234">PackageIconUrl</span></span>

<span data-ttu-id="49c0b-235">一部分的變更[NuGet 問題 352](https://github.com/NuGet/Home/issues/352)，`PackageIconUrl`最終將會變更為`PackageIconUri`而且可以是圖示檔案以將包含在產生的封裝根目錄的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-235">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="49c0b-236">輸出組件</span><span class="sxs-lookup"><span data-stu-id="49c0b-236">Output assemblies</span></span>

<span data-ttu-id="49c0b-237">`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="49c0b-238">所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。</span><span class="sxs-lookup"><span data-stu-id="49c0b-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="49c0b-239">在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：</span><span class="sxs-lookup"><span data-stu-id="49c0b-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="49c0b-240">`IncludeBuildOutput`：布林值，決定是否應該在套件中包含組建輸出組件。</span><span class="sxs-lookup"><span data-stu-id="49c0b-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="49c0b-241">`BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="49c0b-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="49c0b-242">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="49c0b-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="49c0b-243">套件參考</span><span class="sxs-lookup"><span data-stu-id="49c0b-243">Package references</span></span>

<span data-ttu-id="49c0b-244">請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。</span><span class="sxs-lookup"><span data-stu-id="49c0b-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="49c0b-245">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="49c0b-245">Project to project references</span></span>

<span data-ttu-id="49c0b-246">預設會將專案對專案參考視為 NuGet 套件參考，例如：</span><span class="sxs-lookup"><span data-stu-id="49c0b-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="49c0b-247">您也可以將下列中繼資料新增至您的專案參考：</span><span class="sxs-lookup"><span data-stu-id="49c0b-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="49c0b-248">在套件內包含內容</span><span class="sxs-lookup"><span data-stu-id="49c0b-248">Including content in a package</span></span>

<span data-ttu-id="49c0b-249">若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。</span><span class="sxs-lookup"><span data-stu-id="49c0b-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="49c0b-250">除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：</span><span class="sxs-lookup"><span data-stu-id="49c0b-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="49c0b-251">除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="49c0b-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="49c0b-252">如果您想要將所有內容都只複製至特定根資料夾 (而不是 `content` 和 `contentFiles`)，則可以使用 MSBuild 屬性 `ContentTargetFolders`，其預設為 "content;contentFiles"，但可以設定為任何其他資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="49c0b-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="49c0b-253">請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。</span><span class="sxs-lookup"><span data-stu-id="49c0b-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="49c0b-254">`PackagePath` 可以是以分號分隔的一組目標路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="49c0b-255">指定空的套件路徑會將檔案新增至套件的根目錄。</span><span class="sxs-lookup"><span data-stu-id="49c0b-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="49c0b-256">例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：</span><span class="sxs-lookup"><span data-stu-id="49c0b-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="49c0b-257">另有 MSBuild 屬性 `$(IncludeContentInPack)` 預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="49c0b-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="49c0b-258">如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。</span><span class="sxs-lookup"><span data-stu-id="49c0b-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="49c0b-259">您可在上述任何項目上設定的其他封裝特定中繼資料包含 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，其在輸出 nuspec 的 ```contentFiles``` 項目上設定 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="49c0b-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="49c0b-260">除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="49c0b-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="49c0b-261">針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="49c0b-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="49c0b-262">IncludeSymbols</span></span>

<span data-ttu-id="49c0b-263">使用 `MSBuild /t:pack /p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。</span><span class="sxs-lookup"><span data-stu-id="49c0b-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="49c0b-264">請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。</span><span class="sxs-lookup"><span data-stu-id="49c0b-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="49c0b-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="49c0b-265">IncludeSource</span></span>

<span data-ttu-id="49c0b-266">這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="49c0b-267">所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="49c0b-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="49c0b-268">這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="49c0b-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="49c0b-269">若類型為 Compile 的檔案位於專案資料夾之外，就只會將其新增至 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="49c0b-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="49c0b-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="49c0b-270">IsTool</span></span>

<span data-ttu-id="49c0b-271">使用 `MSBuild /t:pack /p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="49c0b-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="49c0b-272">請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。</span><span class="sxs-lookup"><span data-stu-id="49c0b-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="49c0b-273">使用 .nuspec 封裝</span><span class="sxs-lookup"><span data-stu-id="49c0b-273">Packing using a .nuspec</span></span>

<span data-ttu-id="49c0b-274">您可以使用`.nuspec`檔案來封裝您的專案，前提是有 SDK 專案檔匯入`NuGet.Build.Tasks.Pack.targets`，這樣可以執行組件工作。</span><span class="sxs-lookup"><span data-stu-id="49c0b-274">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="49c0b-275">您仍需要將專案還原之前，您可以壓縮 nuspec 檔案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-275">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="49c0b-276">專案檔的目標 framework 不相關及 nuspec 封裝作業時，不使用。</span><span class="sxs-lookup"><span data-stu-id="49c0b-276">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="49c0b-277">下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：</span><span class="sxs-lookup"><span data-stu-id="49c0b-277">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="49c0b-278">`NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-278">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="49c0b-279">`NuspecProperties`：以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="49c0b-279">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="49c0b-280">基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`/p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="49c0b-280">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="49c0b-281">`NuspecBasePath`：`.nuspec` 檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-281">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="49c0b-282">如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="49c0b-282">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="49c0b-283">如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="49c0b-283">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="49c0b-284">請注意，封裝 nuspec 使用 dotnet.exe 或 msbuild 也會使預設建置專案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-284">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="49c0b-285">這可以避免藉由傳遞```--no-build```dotnet.exe，相當於設定的屬性```<NoBuild>true</NoBuild> ```專案檔，以及設定中```<IncludeBuildOutput>false</IncludeBuildOutput> ```專案檔中</span><span class="sxs-lookup"><span data-stu-id="49c0b-285">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="49c0b-286">組件 nuspec 檔案 csproj 檔案的範例是：</span><span class="sxs-lookup"><span data-stu-id="49c0b-286">An example of a csproj file to pack a nuspec file is:</span></span>

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="49c0b-287">進階擴充點來建立自訂的套件</span><span class="sxs-lookup"><span data-stu-id="49c0b-287">Advanced extension points to create customized package</span></span>

<span data-ttu-id="49c0b-288">`pack`目標提供兩個內部的目標 framework 特定組建中執行的擴充點。</span><span class="sxs-lookup"><span data-stu-id="49c0b-288">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="49c0b-289">包括特定內容的目標 framework 和到封裝的組件，支援的擴充點：</span><span class="sxs-lookup"><span data-stu-id="49c0b-289">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="49c0b-290">`TargetsForTfmSpecificBuildOutput` 目標： 用於內部檔案`lib`資料夾或使用指定的資料夾`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="49c0b-290">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="49c0b-291">`TargetsForTfmSpecificContentInPackage` 目標： 以外的檔案使用`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="49c0b-291">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="49c0b-292">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="49c0b-292">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="49c0b-293">撰寫自訂的目標，並指定做為值`$(TargetsForTfmSpecificBuildOutput)`屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-293">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="49c0b-294">需要進入的任何檔案`BuildOutputTargetFolder`(依預設 lib)，目標應該將這些檔案複製到 ItemGroup`BuildOutputInPackage`並設定下列兩個中繼資料值：</span><span class="sxs-lookup"><span data-stu-id="49c0b-294">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="49c0b-295">`FinalOutputPath`： 絕對路徑的檔案。如果未提供，身分識別用來評估來源路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-295">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="49c0b-296">`TargetPath`: （選擇性) 需要移入的子資料夾中的檔案時，設定`lib\<TargetFramework>`，像在其各自的文化特性資料夾下，移至附屬組件。</span><span class="sxs-lookup"><span data-stu-id="49c0b-296">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="49c0b-297">預設值是檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="49c0b-297">Defaults to the name of the file.</span></span>

<span data-ttu-id="49c0b-298">範例：</span><span class="sxs-lookup"><span data-stu-id="49c0b-298">Example:</span></span>

```
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="49c0b-299">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="49c0b-299">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="49c0b-300">撰寫自訂的目標，並指定做為值`$(TargetsForTfmSpecificContentInPackage)`屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-300">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="49c0b-301">若要在封裝中包含任何檔案，目標應該寫入這些檔案 ItemGroup`TfmSpecificPackageFile`並設定下列選擇性中繼資料：</span><span class="sxs-lookup"><span data-stu-id="49c0b-301">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="49c0b-302">`PackagePath`： 在封裝中的輸出檔案應該的儲存路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-302">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="49c0b-303">如果多個檔案加入至相同的封裝路徑，NuGet 就會發出警告。</span><span class="sxs-lookup"><span data-stu-id="49c0b-303">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="49c0b-304">`BuildAction`： 建置動作指派給檔，才是必要的封裝路徑是否在`contentFiles`資料夾。</span><span class="sxs-lookup"><span data-stu-id="49c0b-304">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="49c0b-305">預設值是"None"。</span><span class="sxs-lookup"><span data-stu-id="49c0b-305">Defaults to "None".</span></span>

<span data-ttu-id="49c0b-306">範例：</span><span class="sxs-lookup"><span data-stu-id="49c0b-306">An example:</span></span>
```
<PropertyGroup>
    <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
    <ItemGroup>
      <TfmSpecificPackageFile Include=""abc.txt"">
        <PackagePath>mycontent/$(TargetFramework)</PackagePath>
      </TfmSpecificPackageFile>
      <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
        <PackagePath>net46content</PackagePath>
      </TfmSpecificPackageFile>  
    </ItemGroup>
  </Target>  
```

## <a name="restore-target"></a><span data-ttu-id="49c0b-307">還原目標</span><span class="sxs-lookup"><span data-stu-id="49c0b-307">restore target</span></span>

<span data-ttu-id="49c0b-308">`MSBuild /t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49c0b-308">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="49c0b-309">讀取所有專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="49c0b-309">Read all project to project references</span></span>
1. <span data-ttu-id="49c0b-310">讀取專案屬性來尋找中繼資料夾和目標架構</span><span class="sxs-lookup"><span data-stu-id="49c0b-310">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="49c0b-311">將 msbuild 資料傳遞至 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="49c0b-311">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="49c0b-312">執行還原</span><span class="sxs-lookup"><span data-stu-id="49c0b-312">Run restore</span></span>
1. <span data-ttu-id="49c0b-313">下載套件</span><span class="sxs-lookup"><span data-stu-id="49c0b-313">Download packages</span></span>
1. <span data-ttu-id="49c0b-314">撰寫資產檔案、目標和屬性</span><span class="sxs-lookup"><span data-stu-id="49c0b-314">Write assets file, targets, and props</span></span>

<span data-ttu-id="49c0b-315">`restore`目標 works**只**使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-315">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="49c0b-316">它會**不**工作的專案使用`packages.config`格式; 使用[nuget 還原](../tools/cli-ref-restore.md)改為。</span><span class="sxs-lookup"><span data-stu-id="49c0b-316">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="49c0b-317">還原屬性</span><span class="sxs-lookup"><span data-stu-id="49c0b-317">Restore properties</span></span>

<span data-ttu-id="49c0b-318">其他還原設定可能來自專案檔中的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-318">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="49c0b-319">您也可以從命令列，使用 `/p:` 參數設定值 (請參閱下列＜範例＞)。</span><span class="sxs-lookup"><span data-stu-id="49c0b-319">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="49c0b-320">屬性</span><span class="sxs-lookup"><span data-stu-id="49c0b-320">Property</span></span> | <span data-ttu-id="49c0b-321">描述</span><span class="sxs-lookup"><span data-stu-id="49c0b-321">Description</span></span> |
|--------|--------|
| <span data-ttu-id="49c0b-322">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="49c0b-322">RestoreSources</span></span> | <span data-ttu-id="49c0b-323">以分號分隔的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="49c0b-323">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="49c0b-324">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="49c0b-324">RestorePackagesPath</span></span> | <span data-ttu-id="49c0b-325">使用者套件資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-325">User packages folder path.</span></span> |
| <span data-ttu-id="49c0b-326">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="49c0b-326">RestoreDisableParallel</span></span> | <span data-ttu-id="49c0b-327">限制逐一進行下載。</span><span class="sxs-lookup"><span data-stu-id="49c0b-327">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="49c0b-328">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="49c0b-328">RestoreConfigFile</span></span> | <span data-ttu-id="49c0b-329">要套用之 `Nuget.Config` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-329">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="49c0b-330">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="49c0b-330">RestoreNoCache</span></span> | <span data-ttu-id="49c0b-331">如果為 true，可避免使用快取的套件。</span><span class="sxs-lookup"><span data-stu-id="49c0b-331">If true, avoids using cached packages.</span></span> <span data-ttu-id="49c0b-332">請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="49c0b-332">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="49c0b-333">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="49c0b-333">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="49c0b-334">如果為 true，請忽略失敗或遺漏的套件來源。</span><span class="sxs-lookup"><span data-stu-id="49c0b-334">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="49c0b-335">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="49c0b-335">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="49c0b-336">`NuGet.Build.Tasks.dll` 的路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-336">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="49c0b-337">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="49c0b-337">RestoreGraphProjectInput</span></span> | <span data-ttu-id="49c0b-338">要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="49c0b-338">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="49c0b-339">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="49c0b-339">RestoreOutputPath</span></span> | <span data-ttu-id="49c0b-340">輸出資料夾，預設為 `obj` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="49c0b-340">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="49c0b-341">範例</span><span class="sxs-lookup"><span data-stu-id="49c0b-341">Examples</span></span>

<span data-ttu-id="49c0b-342">命令列：</span><span class="sxs-lookup"><span data-stu-id="49c0b-342">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="49c0b-343">專案檔：</span><span class="sxs-lookup"><span data-stu-id="49c0b-343">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="49c0b-344">Restore outputs</span><span class="sxs-lookup"><span data-stu-id="49c0b-344">Restore outputs</span></span>

<span data-ttu-id="49c0b-345">還原會在組建 `obj` 資料夾中建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="49c0b-345">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="49c0b-346">檔案</span><span class="sxs-lookup"><span data-stu-id="49c0b-346">File</span></span> | <span data-ttu-id="49c0b-347">描述</span><span class="sxs-lookup"><span data-stu-id="49c0b-347">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="49c0b-348">包含封裝的所有參考的相依性圖形。</span><span class="sxs-lookup"><span data-stu-id="49c0b-348">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="49c0b-349">套件中所含 MSBuild 屬性的參考</span><span class="sxs-lookup"><span data-stu-id="49c0b-349">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="49c0b-350">套件中所含 MSBuild 目標的參考</span><span class="sxs-lookup"><span data-stu-id="49c0b-350">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="49c0b-351">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="49c0b-351">PackageTargetFallback</span></span>

<span data-ttu-id="49c0b-352">`PackageTargetFallback` 項目可讓您指定一組要在還原套件時使用的相容目標。</span><span class="sxs-lookup"><span data-stu-id="49c0b-352">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="49c0b-353">其設計目的是要讓使用 dotnet [TxM](../reference/target-frameworks.md) 的套件可以與未宣告 dotnet TxM 的相容套件一起運作。</span><span class="sxs-lookup"><span data-stu-id="49c0b-353">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="49c0b-354">也就是說，如果您的專案使用 dotnet TxM，除非您將 `<PackageTargetFallback>` 新增至專案，以讓非 dotnet 平台變成與 dotnet 相容，否則其相依的所有套件也必須要有 dotnet TxM。</span><span class="sxs-lookup"><span data-stu-id="49c0b-354">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="49c0b-355">例如，如果專案使用 `netstandard1.6` TxM，而且相依套件僅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，則無法建置專案。</span><span class="sxs-lookup"><span data-stu-id="49c0b-355">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="49c0b-356">如果您想要匯入的是第二個 DLL，則可以如下新增 `PackageTargetFallback`，指出 `portable-net45+win81` DLL 相容：</span><span class="sxs-lookup"><span data-stu-id="49c0b-356">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="49c0b-357">若要宣告專案中所有目標的後援，請省略 `Condition` 屬性。</span><span class="sxs-lookup"><span data-stu-id="49c0b-357">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="49c0b-358">您也可以包含 `$(PackageTargetFallback)` 來擴充任何現有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49c0b-358">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="49c0b-359">取代還原圖形中的一個程式庫</span><span class="sxs-lookup"><span data-stu-id="49c0b-359">Replacing one library from a restore graph</span></span>

<span data-ttu-id="49c0b-360">如果還原內含錯誤的組件，您可以排除該套件預設選項，並將其取代為您自己的選項。</span><span class="sxs-lookup"><span data-stu-id="49c0b-360">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="49c0b-361">首先，會有最上層 `PackageReference`，但排除所有資產：</span><span class="sxs-lookup"><span data-stu-id="49c0b-361">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="49c0b-362">接下來，新增您自己對 DLL 之適當本機複本的參考：</span><span class="sxs-lookup"><span data-stu-id="49c0b-362">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
