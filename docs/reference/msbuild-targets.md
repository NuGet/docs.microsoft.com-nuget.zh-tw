---
title: NuGet 封裝和還原為 MSBuild 目標
description: 使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7b3fc72ddd3ad6c9185c2bd0f2563df59e77f1c8
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453542"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="c96ec-103">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="c96ec-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="c96ec-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="c96ec-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="c96ec-105">利用 PackageReference 格式，NuGet 4.0+ 可以在專案檔內直接儲存所有資訊清單中繼資料，而非使用個別的 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="c96ec-106">使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。</span><span class="sxs-lookup"><span data-stu-id="c96ec-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="c96ec-107">這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。</span><span class="sxs-lookup"><span data-stu-id="c96ec-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="c96ec-108">(在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="c96ec-109">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="c96ec-109">Target build order</span></span>

<span data-ttu-id="c96ec-110">因為 `pack` 和 `restore` 是 MSBuild 目標，所以您可以存取它們，以加強工作流程。</span><span class="sxs-lookup"><span data-stu-id="c96ec-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="c96ec-111">例如，假設您想要在封裝套件之後，將套件複製至網路共用。</span><span class="sxs-lookup"><span data-stu-id="c96ec-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="c96ec-112">做法是在專案檔中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="c96ec-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="c96ec-113">同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，以及在 MSBuild 工作中使用 NuGet 屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="c96ec-114">封裝目標</span><span class="sxs-lookup"><span data-stu-id="c96ec-114">pack target</span></span>

<span data-ttu-id="c96ec-115">.NET Standard 專案使用 PackageReference 格式，請使用`msbuild -t:pack`獲得從要用來建立 NuGet 套件的專案檔的輸入。</span><span class="sxs-lookup"><span data-stu-id="c96ec-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="c96ec-116">下表描述可新增至第一個 `<PropertyGroup>` 節點內之專案檔的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="c96ec-117">以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。</span><span class="sxs-lookup"><span data-stu-id="c96ec-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="c96ec-118">為了方便起見，資料表是依 [`.nuspec` 檔案](../reference/nuspec.md)中的對等屬性進行組織。</span><span class="sxs-lookup"><span data-stu-id="c96ec-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="c96ec-119">請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="c96ec-120">屬性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="c96ec-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="c96ec-121">MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="c96ec-121">MSBuild Property</span></span> | <span data-ttu-id="c96ec-122">預設</span><span class="sxs-lookup"><span data-stu-id="c96ec-122">Default</span></span> | <span data-ttu-id="c96ec-123">注意</span><span class="sxs-lookup"><span data-stu-id="c96ec-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="c96ec-124">ID</span><span class="sxs-lookup"><span data-stu-id="c96ec-124">Id</span></span> | <span data-ttu-id="c96ec-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="c96ec-125">PackageId</span></span> | <span data-ttu-id="c96ec-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="c96ec-126">AssemblyName</span></span> | <span data-ttu-id="c96ec-127">MSBuild 中的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="c96ec-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="c96ec-128">版本</span><span class="sxs-lookup"><span data-stu-id="c96ec-128">Version</span></span> | <span data-ttu-id="c96ec-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c96ec-129">PackageVersion</span></span> | <span data-ttu-id="c96ec-130">版本</span><span class="sxs-lookup"><span data-stu-id="c96ec-130">Version</span></span> | <span data-ttu-id="c96ec-131">這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="c96ec-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="c96ec-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c96ec-132">VersionPrefix</span></span> | <span data-ttu-id="c96ec-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c96ec-133">PackageVersionPrefix</span></span> | <span data-ttu-id="c96ec-134">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-134">empty</span></span> | <span data-ttu-id="c96ec-135">設定 PackageVersion 會覆寫 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c96ec-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="c96ec-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c96ec-136">VersionSuffix</span></span> | <span data-ttu-id="c96ec-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c96ec-137">PackageVersionSuffix</span></span> | <span data-ttu-id="c96ec-138">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-138">empty</span></span> | <span data-ttu-id="c96ec-139">MSBuild 中的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="c96ec-140">設定 PackageVersion 會覆寫 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c96ec-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="c96ec-141">作者</span><span class="sxs-lookup"><span data-stu-id="c96ec-141">Authors</span></span> | <span data-ttu-id="c96ec-142">作者</span><span class="sxs-lookup"><span data-stu-id="c96ec-142">Authors</span></span> | <span data-ttu-id="c96ec-143">目前使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="c96ec-143">Username of the current user</span></span> | |
| <span data-ttu-id="c96ec-144">Owners</span><span class="sxs-lookup"><span data-stu-id="c96ec-144">Owners</span></span> | <span data-ttu-id="c96ec-145">N/A</span><span class="sxs-lookup"><span data-stu-id="c96ec-145">N/A</span></span> | <span data-ttu-id="c96ec-146">NuSpec 中沒有</span><span class="sxs-lookup"><span data-stu-id="c96ec-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="c96ec-147">標題</span><span class="sxs-lookup"><span data-stu-id="c96ec-147">Title</span></span> | <span data-ttu-id="c96ec-148">標題</span><span class="sxs-lookup"><span data-stu-id="c96ec-148">Title</span></span> | <span data-ttu-id="c96ec-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="c96ec-149">The PackageId</span></span>| |
| <span data-ttu-id="c96ec-150">描述</span><span class="sxs-lookup"><span data-stu-id="c96ec-150">Description</span></span> | <span data-ttu-id="c96ec-151">描述</span><span class="sxs-lookup"><span data-stu-id="c96ec-151">Description</span></span> | <span data-ttu-id="c96ec-152">"Package Description"</span><span class="sxs-lookup"><span data-stu-id="c96ec-152">"Package Description"</span></span> | |
| <span data-ttu-id="c96ec-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="c96ec-153">Copyright</span></span> | <span data-ttu-id="c96ec-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="c96ec-154">Copyright</span></span> | <span data-ttu-id="c96ec-155">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-155">empty</span></span> | |
| <span data-ttu-id="c96ec-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c96ec-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="c96ec-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c96ec-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="c96ec-158">False</span><span class="sxs-lookup"><span data-stu-id="c96ec-158">false</span></span> | |
| <span data-ttu-id="c96ec-159">授權</span><span class="sxs-lookup"><span data-stu-id="c96ec-159">license</span></span> | <span data-ttu-id="c96ec-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c96ec-160">PackageLicenseExpression</span></span> | <span data-ttu-id="c96ec-161">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-161">empty</span></span> | <span data-ttu-id="c96ec-162">對應至 `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="c96ec-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="c96ec-163">授權</span><span class="sxs-lookup"><span data-stu-id="c96ec-163">license</span></span> | <span data-ttu-id="c96ec-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c96ec-164">PackageLicenseFile</span></span> | <span data-ttu-id="c96ec-165">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-165">empty</span></span> | <span data-ttu-id="c96ec-166">對應至 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="c96ec-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="c96ec-167">您可能需要明確組件參考的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="c96ec-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-168">LicenseUrl</span></span> | <span data-ttu-id="c96ec-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-169">PackageLicenseUrl</span></span> | <span data-ttu-id="c96ec-170">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-170">empty</span></span> | <span data-ttu-id="c96ec-171">`licenseUrl` 已被取代，使用 [PackageLicenseExpression] 或 PackageLicenseFile 屬性</span><span class="sxs-lookup"><span data-stu-id="c96ec-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="c96ec-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-172">ProjectUrl</span></span> | <span data-ttu-id="c96ec-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-173">PackageProjectUrl</span></span> | <span data-ttu-id="c96ec-174">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-174">empty</span></span> | |
| <span data-ttu-id="c96ec-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-175">IconUrl</span></span> | <span data-ttu-id="c96ec-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-176">PackageIconUrl</span></span> | <span data-ttu-id="c96ec-177">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-177">empty</span></span> | |
| <span data-ttu-id="c96ec-178">Tags</span><span class="sxs-lookup"><span data-stu-id="c96ec-178">Tags</span></span> | <span data-ttu-id="c96ec-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c96ec-179">PackageTags</span></span> | <span data-ttu-id="c96ec-180">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-180">empty</span></span> | <span data-ttu-id="c96ec-181">以分號來分隔標記。</span><span class="sxs-lookup"><span data-stu-id="c96ec-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="c96ec-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c96ec-182">ReleaseNotes</span></span> | <span data-ttu-id="c96ec-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c96ec-183">PackageReleaseNotes</span></span> | <span data-ttu-id="c96ec-184">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-184">empty</span></span> | |
| <span data-ttu-id="c96ec-185">存放庫/Url</span><span class="sxs-lookup"><span data-stu-id="c96ec-185">Repository/Url</span></span> | <span data-ttu-id="c96ec-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-186">RepositoryUrl</span></span> | <span data-ttu-id="c96ec-187">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-187">empty</span></span> | <span data-ttu-id="c96ec-188">用來複製或擷取原始程式碼存放庫 URL。</span><span class="sxs-lookup"><span data-stu-id="c96ec-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="c96ec-189">範例： *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="c96ec-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="c96ec-190">存放庫/類型</span><span class="sxs-lookup"><span data-stu-id="c96ec-190">Repository/Type</span></span> | <span data-ttu-id="c96ec-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c96ec-191">RepositoryType</span></span> | <span data-ttu-id="c96ec-192">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-192">empty</span></span> | <span data-ttu-id="c96ec-193">存放庫類型。</span><span class="sxs-lookup"><span data-stu-id="c96ec-193">Repository type.</span></span> <span data-ttu-id="c96ec-194">範例： *git*， *tfs*。</span><span class="sxs-lookup"><span data-stu-id="c96ec-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="c96ec-195">存放庫/分支</span><span class="sxs-lookup"><span data-stu-id="c96ec-195">Repository/Branch</span></span> | <span data-ttu-id="c96ec-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="c96ec-196">RepositoryBranch</span></span> | <span data-ttu-id="c96ec-197">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-197">empty</span></span> | <span data-ttu-id="c96ec-198">選擇性的存放庫分支資訊。</span><span class="sxs-lookup"><span data-stu-id="c96ec-198">Optional repository branch information.</span></span> <span data-ttu-id="c96ec-199">*RepositoryUrl*也必須指定要包含此屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c96ec-200">範例：*主要*(NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="c96ec-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c96ec-201">存放庫/認可</span><span class="sxs-lookup"><span data-stu-id="c96ec-201">Repository/Commit</span></span> | <span data-ttu-id="c96ec-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="c96ec-202">RepositoryCommit</span></span> | <span data-ttu-id="c96ec-203">空白</span><span class="sxs-lookup"><span data-stu-id="c96ec-203">empty</span></span> | <span data-ttu-id="c96ec-204">選擇性的儲存機制認可或變更集，以表示其來源的套件建置。</span><span class="sxs-lookup"><span data-stu-id="c96ec-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="c96ec-205">*RepositoryUrl*也必須指定要包含此屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c96ec-206">範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="c96ec-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c96ec-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="c96ec-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="c96ec-208">總結</span><span class="sxs-lookup"><span data-stu-id="c96ec-208">Summary</span></span> | <span data-ttu-id="c96ec-209">不支援</span><span class="sxs-lookup"><span data-stu-id="c96ec-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="c96ec-210">封裝目標輸入</span><span class="sxs-lookup"><span data-stu-id="c96ec-210">pack target inputs</span></span>

- <span data-ttu-id="c96ec-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="c96ec-211">IsPackable</span></span>
- <span data-ttu-id="c96ec-212">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c96ec-212">PackageVersion</span></span>
- <span data-ttu-id="c96ec-213">PackageId</span><span class="sxs-lookup"><span data-stu-id="c96ec-213">PackageId</span></span>
- <span data-ttu-id="c96ec-214">作者</span><span class="sxs-lookup"><span data-stu-id="c96ec-214">Authors</span></span>
- <span data-ttu-id="c96ec-215">描述</span><span class="sxs-lookup"><span data-stu-id="c96ec-215">Description</span></span>
- <span data-ttu-id="c96ec-216">Copyright</span><span class="sxs-lookup"><span data-stu-id="c96ec-216">Copyright</span></span>
- <span data-ttu-id="c96ec-217">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c96ec-217">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="c96ec-218">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="c96ec-218">DevelopmentDependency</span></span>
- <span data-ttu-id="c96ec-219">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c96ec-219">PackageLicenseExpression</span></span>
- <span data-ttu-id="c96ec-220">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c96ec-220">PackageLicenseFile</span></span>
- <span data-ttu-id="c96ec-221">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-221">PackageLicenseUrl</span></span>
- <span data-ttu-id="c96ec-222">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-222">PackageProjectUrl</span></span>
- <span data-ttu-id="c96ec-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-223">PackageIconUrl</span></span>
- <span data-ttu-id="c96ec-224">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c96ec-224">PackageReleaseNotes</span></span>
- <span data-ttu-id="c96ec-225">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c96ec-225">PackageTags</span></span>
- <span data-ttu-id="c96ec-226">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="c96ec-226">PackageOutputPath</span></span>
- <span data-ttu-id="c96ec-227">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c96ec-227">IncludeSymbols</span></span>
- <span data-ttu-id="c96ec-228">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c96ec-228">IncludeSource</span></span>
- <span data-ttu-id="c96ec-229">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="c96ec-229">PackageTypes</span></span>
- <span data-ttu-id="c96ec-230">IsTool</span><span class="sxs-lookup"><span data-stu-id="c96ec-230">IsTool</span></span>
- <span data-ttu-id="c96ec-231">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-231">RepositoryUrl</span></span>
- <span data-ttu-id="c96ec-232">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c96ec-232">RepositoryType</span></span>
- <span data-ttu-id="c96ec-233">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="c96ec-233">RepositoryBranch</span></span>
- <span data-ttu-id="c96ec-234">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="c96ec-234">RepositoryCommit</span></span>
- <span data-ttu-id="c96ec-235">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c96ec-235">NoPackageAnalysis</span></span>
- <span data-ttu-id="c96ec-236">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c96ec-236">MinClientVersion</span></span>
- <span data-ttu-id="c96ec-237">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c96ec-237">IncludeBuildOutput</span></span>
- <span data-ttu-id="c96ec-238">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="c96ec-238">IncludeContentInPack</span></span>
- <span data-ttu-id="c96ec-239">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="c96ec-239">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="c96ec-240">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="c96ec-240">ContentTargetFolders</span></span>
- <span data-ttu-id="c96ec-241">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="c96ec-241">NuspecFile</span></span>
- <span data-ttu-id="c96ec-242">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="c96ec-242">NuspecBasePath</span></span>
- <span data-ttu-id="c96ec-243">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="c96ec-243">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="c96ec-244">封裝案例</span><span class="sxs-lookup"><span data-stu-id="c96ec-244">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="c96ec-245">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c96ec-245">PackageIconUrl</span></span>

<span data-ttu-id="c96ec-246">一部分的變更[NuGet 問題 352](https://github.com/NuGet/Home/issues/352)，`PackageIconUrl`最後會變更為`PackageIconUri`而且可以是圖示檔會包含在產生的封裝根目錄的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-246">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="c96ec-247">輸出組件</span><span class="sxs-lookup"><span data-stu-id="c96ec-247">Output assemblies</span></span>

<span data-ttu-id="c96ec-248">`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-248">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="c96ec-249">所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。</span><span class="sxs-lookup"><span data-stu-id="c96ec-249">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="c96ec-250">在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：</span><span class="sxs-lookup"><span data-stu-id="c96ec-250">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="c96ec-251">`IncludeBuildOutput`：布林值，決定是否應該在套件中包含組建輸出組件。</span><span class="sxs-lookup"><span data-stu-id="c96ec-251">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="c96ec-252">`BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c96ec-252">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="c96ec-253">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c96ec-253">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="c96ec-254">套件參考</span><span class="sxs-lookup"><span data-stu-id="c96ec-254">Package references</span></span>

<span data-ttu-id="c96ec-255">請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-255">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="c96ec-256">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="c96ec-256">Project to project references</span></span>

<span data-ttu-id="c96ec-257">預設會將專案對專案參考視為 NuGet 套件參考，例如：</span><span class="sxs-lookup"><span data-stu-id="c96ec-257">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="c96ec-258">您也可以將下列中繼資料新增至您的專案參考：</span><span class="sxs-lookup"><span data-stu-id="c96ec-258">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="c96ec-259">在套件內包含內容</span><span class="sxs-lookup"><span data-stu-id="c96ec-259">Including content in a package</span></span>

<span data-ttu-id="c96ec-260">若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。</span><span class="sxs-lookup"><span data-stu-id="c96ec-260">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="c96ec-261">除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：</span><span class="sxs-lookup"><span data-stu-id="c96ec-261">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="c96ec-262">除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="c96ec-262">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="c96ec-263">如果您想要將所有內容都只複製至特定根資料夾 (而不是 `content` 和 `contentFiles`)，則可以使用 MSBuild 屬性 `ContentTargetFolders`，其預設為 "content;contentFiles"，但可以設定為任何其他資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="c96ec-263">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="c96ec-264">請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。</span><span class="sxs-lookup"><span data-stu-id="c96ec-264">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="c96ec-265">`PackagePath` 可以是以分號分隔的一組目標路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-265">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="c96ec-266">指定空的套件路徑會將檔案新增至套件的根目錄。</span><span class="sxs-lookup"><span data-stu-id="c96ec-266">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="c96ec-267">例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：</span><span class="sxs-lookup"><span data-stu-id="c96ec-267">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="c96ec-268">另有 MSBuild 屬性 `$(IncludeContentInPack)` 預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="c96ec-268">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="c96ec-269">如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。</span><span class="sxs-lookup"><span data-stu-id="c96ec-269">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="c96ec-270">您可在上述任何項目上設定的其他封裝特定中繼資料包含 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，其在輸出 nuspec 的 ```contentFiles``` 項目上設定 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="c96ec-270">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="c96ec-271">除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c96ec-271">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="c96ec-272">針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-272">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="c96ec-273">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c96ec-273">IncludeSymbols</span></span>

<span data-ttu-id="c96ec-274">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-274">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="c96ec-275">請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。</span><span class="sxs-lookup"><span data-stu-id="c96ec-275">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="c96ec-276">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c96ec-276">IncludeSource</span></span>

<span data-ttu-id="c96ec-277">這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-277">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="c96ec-278">所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="c96ec-278">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="c96ec-279">這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="c96ec-279">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="c96ec-280">若類型為 Compile 的檔案位於專案資料夾之外，就只會將其新增至 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="c96ec-280">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="c96ec-281">封裝授權運算式或授權檔案</span><span class="sxs-lookup"><span data-stu-id="c96ec-281">Packing a license expression or a license file</span></span>

<span data-ttu-id="c96ec-282">使用授權運算式時，應該使用 PackageLicenseExpression 屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-282">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="c96ec-283">[授權運算式範例](# https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-283">[License expression sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

<span data-ttu-id="c96ec-284">當封裝的授權檔案，您需要使用 PackageLicenseFile 屬性來指定封裝路徑，相對於封裝根目錄。</span><span class="sxs-lookup"><span data-stu-id="c96ec-284">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="c96ec-285">此外，您需要確定在封裝中包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-285">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="c96ec-286">例如: </span><span class="sxs-lookup"><span data-stu-id="c96ec-286">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
<span data-ttu-id="c96ec-287">[授權生命週期範例](# https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-287">[License life sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="c96ec-288">IsTool</span><span class="sxs-lookup"><span data-stu-id="c96ec-288">IsTool</span></span>

<span data-ttu-id="c96ec-289">使用 `MSBuild -t:pack -p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c96ec-289">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="c96ec-290">請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。</span><span class="sxs-lookup"><span data-stu-id="c96ec-290">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="c96ec-291">使用 .nuspec 封裝</span><span class="sxs-lookup"><span data-stu-id="c96ec-291">Packing using a .nuspec</span></span>

<span data-ttu-id="c96ec-292">您可以使用`.nuspec`檔案來封裝您的專案，前提是您要匯入的 SDK 專案檔案`NuGet.Build.Tasks.Pack.targets`，這樣可以執行封裝工作。</span><span class="sxs-lookup"><span data-stu-id="c96ec-292">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="c96ec-293">您仍然需要先還原專案，才可以 pack nuspec 檔案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-293">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="c96ec-294">專案檔的目標 framework 無關，不使用封裝 nuspec 時。</span><span class="sxs-lookup"><span data-stu-id="c96ec-294">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="c96ec-295">下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：</span><span class="sxs-lookup"><span data-stu-id="c96ec-295">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="c96ec-296">`NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-296">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="c96ec-297">`NuspecProperties`：以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="c96ec-297">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="c96ec-298">基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`-p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="c96ec-298">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="c96ec-299">`NuspecBasePath`：`.nuspec` 檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-299">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="c96ec-300">如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="c96ec-300">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c96ec-301">如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="c96ec-301">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c96ec-302">請注意，封裝 nuspec 使用 dotnet.exe 或 msbuild 也會導致建置預設的專案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-302">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="c96ec-303">可以避免此一傳遞```--no-build```屬性就相當於設定的 dotnet.exe```<NoBuild>true</NoBuild> ```在您的專案檔，以及設定```<IncludeBuildOutput>false</IncludeBuildOutput> ```專案檔中</span><span class="sxs-lookup"><span data-stu-id="c96ec-303">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="c96ec-304">Csproj 檔案組件 nuspec 檔案的範例為：</span><span class="sxs-lookup"><span data-stu-id="c96ec-304">An example of a csproj file to pack a nuspec file is:</span></span>

```xml
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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="c96ec-305">進階延伸模組點來建立自訂的套件</span><span class="sxs-lookup"><span data-stu-id="c96ec-305">Advanced extension points to create customized package</span></span>

<span data-ttu-id="c96ec-306">`pack`目標會提供在內部的目標 framework 特定組建中執行的兩個擴充點。</span><span class="sxs-lookup"><span data-stu-id="c96ec-306">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="c96ec-307">包含特定內容的目標 framework 和組件載入封裝，支援的擴充點：</span><span class="sxs-lookup"><span data-stu-id="c96ec-307">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="c96ec-308">`TargetsForTfmSpecificBuildOutput` 目標： 檔案內使用`lib`資料夾或使用指定的資料夾`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="c96ec-308">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="c96ec-309">`TargetsForTfmSpecificContentInPackage` 目標： 用於外部檔案`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="c96ec-309">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="c96ec-310">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c96ec-310">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="c96ec-311">撰寫自訂目標，並將其指定的值為`$(TargetsForTfmSpecificBuildOutput)`屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-311">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="c96ec-312">針對需要進入的任何檔案`BuildOutputTargetFolder`（預設程式庫），目標應該寫入 ItemGroup 的那些檔案`BuildOutputInPackage`並設定下列兩個中繼資料值：</span><span class="sxs-lookup"><span data-stu-id="c96ec-312">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="c96ec-313">`FinalOutputPath`: 檔案中; 的絕對路徑如果未提供，身分識別用來評估來源路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-313">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="c96ec-314">`TargetPath`: （選擇性) 設定時必須將檔案移至的子資料夾內`lib\<TargetFramework>`，例如在其各自的文化特性資料夾底下，移至附屬組件。</span><span class="sxs-lookup"><span data-stu-id="c96ec-314">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="c96ec-315">預設值是檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="c96ec-315">Defaults to the name of the file.</span></span>

<span data-ttu-id="c96ec-316">範例：</span><span class="sxs-lookup"><span data-stu-id="c96ec-316">Example:</span></span>

```xml
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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="c96ec-317">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="c96ec-317">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="c96ec-318">撰寫自訂目標，並將其指定的值為`$(TargetsForTfmSpecificContentInPackage)`屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="c96ec-319">要包含在封裝中的任何檔案，目標應該寫入這些檔案的 ItemGroup`TfmSpecificPackageFile`並設定下列選擇性的中繼資料：</span><span class="sxs-lookup"><span data-stu-id="c96ec-319">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="c96ec-320">`PackagePath`： 在封裝中的輸出檔案應該的儲存路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-320">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="c96ec-321">如果多個檔案新增至相同的封裝路徑，NuGet 就會發出警告。</span><span class="sxs-lookup"><span data-stu-id="c96ec-321">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="c96ec-322">`BuildAction`： 建置動作將指派給該檔案，才需要的封裝路徑是否在`contentFiles`資料夾。</span><span class="sxs-lookup"><span data-stu-id="c96ec-322">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="c96ec-323">預設為 「 無 」。</span><span class="sxs-lookup"><span data-stu-id="c96ec-323">Defaults to "None".</span></span>

<span data-ttu-id="c96ec-324">範例：</span><span class="sxs-lookup"><span data-stu-id="c96ec-324">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="c96ec-325">還原目標</span><span class="sxs-lookup"><span data-stu-id="c96ec-325">restore target</span></span>

<span data-ttu-id="c96ec-326">`MSBuild -t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c96ec-326">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="c96ec-327">讀取所有專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="c96ec-327">Read all project to project references</span></span>
1. <span data-ttu-id="c96ec-328">讀取專案屬性來尋找中繼資料夾和目標架構</span><span class="sxs-lookup"><span data-stu-id="c96ec-328">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="c96ec-329">將 msbuild 資料傳遞至 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="c96ec-329">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="c96ec-330">執行還原</span><span class="sxs-lookup"><span data-stu-id="c96ec-330">Run restore</span></span>
1. <span data-ttu-id="c96ec-331">下載套件</span><span class="sxs-lookup"><span data-stu-id="c96ec-331">Download packages</span></span>
1. <span data-ttu-id="c96ec-332">撰寫資產檔案、目標和屬性</span><span class="sxs-lookup"><span data-stu-id="c96ec-332">Write assets file, targets, and props</span></span>

<span data-ttu-id="c96ec-333">`restore`目標 works**只有**對於使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-333">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="c96ec-334">它會**未**工作使用的專案`packages.config`格式; 請改用[nuget 還原](../tools/cli-ref-restore.md)改為。</span><span class="sxs-lookup"><span data-stu-id="c96ec-334">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="c96ec-335">還原屬性</span><span class="sxs-lookup"><span data-stu-id="c96ec-335">Restore properties</span></span>

<span data-ttu-id="c96ec-336">其他還原設定可能來自專案檔中的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-336">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="c96ec-337">您也可以從命令列，使用 `-p:` 參數設定值 (請參閱下列＜範例＞)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-337">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="c96ec-338">屬性</span><span class="sxs-lookup"><span data-stu-id="c96ec-338">Property</span></span> | <span data-ttu-id="c96ec-339">描述</span><span class="sxs-lookup"><span data-stu-id="c96ec-339">Description</span></span> |
|--------|--------|
| <span data-ttu-id="c96ec-340">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="c96ec-340">RestoreSources</span></span> | <span data-ttu-id="c96ec-341">以分號分隔的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="c96ec-341">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="c96ec-342">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="c96ec-342">RestorePackagesPath</span></span> | <span data-ttu-id="c96ec-343">使用者套件資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-343">User packages folder path.</span></span> |
| <span data-ttu-id="c96ec-344">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="c96ec-344">RestoreDisableParallel</span></span> | <span data-ttu-id="c96ec-345">限制逐一進行下載。</span><span class="sxs-lookup"><span data-stu-id="c96ec-345">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="c96ec-346">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="c96ec-346">RestoreConfigFile</span></span> | <span data-ttu-id="c96ec-347">要套用之 `Nuget.Config` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-347">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="c96ec-348">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="c96ec-348">RestoreNoCache</span></span> | <span data-ttu-id="c96ec-349">如果為 true，可避免使用快取的套件。</span><span class="sxs-lookup"><span data-stu-id="c96ec-349">If true, avoids using cached packages.</span></span> <span data-ttu-id="c96ec-350">請參閱[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="c96ec-350">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c96ec-351">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="c96ec-351">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="c96ec-352">如果為 true，請忽略失敗或遺漏的套件來源。</span><span class="sxs-lookup"><span data-stu-id="c96ec-352">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="c96ec-353">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="c96ec-353">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="c96ec-354">`NuGet.Build.Tasks.dll` 的路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-354">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="c96ec-355">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="c96ec-355">RestoreGraphProjectInput</span></span> | <span data-ttu-id="c96ec-356">要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="c96ec-356">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="c96ec-357">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="c96ec-357">RestoreOutputPath</span></span> | <span data-ttu-id="c96ec-358">輸出資料夾，預設為 `obj` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c96ec-358">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="c96ec-359">範例</span><span class="sxs-lookup"><span data-stu-id="c96ec-359">Examples</span></span>

<span data-ttu-id="c96ec-360">命令列：</span><span class="sxs-lookup"><span data-stu-id="c96ec-360">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="c96ec-361">專案檔：</span><span class="sxs-lookup"><span data-stu-id="c96ec-361">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="c96ec-362">Restore outputs</span><span class="sxs-lookup"><span data-stu-id="c96ec-362">Restore outputs</span></span>

<span data-ttu-id="c96ec-363">還原會在組建 `obj` 資料夾中建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="c96ec-363">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="c96ec-364">檔案</span><span class="sxs-lookup"><span data-stu-id="c96ec-364">File</span></span> | <span data-ttu-id="c96ec-365">描述</span><span class="sxs-lookup"><span data-stu-id="c96ec-365">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="c96ec-366">包含封裝的所有參考的相依性圖形。</span><span class="sxs-lookup"><span data-stu-id="c96ec-366">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="c96ec-367">套件中所含 MSBuild 屬性的參考</span><span class="sxs-lookup"><span data-stu-id="c96ec-367">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="c96ec-368">套件中所含 MSBuild 目標的參考</span><span class="sxs-lookup"><span data-stu-id="c96ec-368">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="c96ec-369">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="c96ec-369">PackageTargetFallback</span></span>

<span data-ttu-id="c96ec-370">`PackageTargetFallback` 項目可讓您指定一組要在還原套件時使用的相容目標。</span><span class="sxs-lookup"><span data-stu-id="c96ec-370">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="c96ec-371">其設計目的是要讓使用 dotnet [TxM](../reference/target-frameworks.md) 的套件可以與未宣告 dotnet TxM 的相容套件一起運作。</span><span class="sxs-lookup"><span data-stu-id="c96ec-371">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="c96ec-372">也就是說，如果您的專案使用 dotnet TxM，除非您將 `<PackageTargetFallback>` 新增至專案，以讓非 dotnet 平台變成與 dotnet 相容，否則其相依的所有套件也必須要有 dotnet TxM。</span><span class="sxs-lookup"><span data-stu-id="c96ec-372">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="c96ec-373">例如，如果專案使用 `netstandard1.6` TxM，而且相依套件僅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，則無法建置專案。</span><span class="sxs-lookup"><span data-stu-id="c96ec-373">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="c96ec-374">如果您想要匯入的是第二個 DLL，則可以如下新增 `PackageTargetFallback`，指出 `portable-net45+win81` DLL 相容：</span><span class="sxs-lookup"><span data-stu-id="c96ec-374">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="c96ec-375">若要宣告專案中所有目標的後援，請省略 `Condition` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c96ec-375">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="c96ec-376">您也可以包含 `$(PackageTargetFallback)` 來擴充任何現有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c96ec-376">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="c96ec-377">取代還原圖形中的一個程式庫</span><span class="sxs-lookup"><span data-stu-id="c96ec-377">Replacing one library from a restore graph</span></span>

<span data-ttu-id="c96ec-378">如果還原內含錯誤的組件，您可以排除該套件預設選項，並將其取代為您自己的選項。</span><span class="sxs-lookup"><span data-stu-id="c96ec-378">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="c96ec-379">首先，會有最上層 `PackageReference`，但排除所有資產：</span><span class="sxs-lookup"><span data-stu-id="c96ec-379">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="c96ec-380">接下來，新增您自己對 DLL 之適當本機複本的參考：</span><span class="sxs-lookup"><span data-stu-id="c96ec-380">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
