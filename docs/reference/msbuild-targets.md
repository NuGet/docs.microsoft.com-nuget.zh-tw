---
title: NuGet 封裝和還原為 MSBuild 目標
description: 使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: d8d1b2ef0185381d16c1bb73035588fe90bcfd14
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959685"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="52b89-103">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="52b89-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="52b89-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="52b89-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="52b89-105">使用[PackageReference](../consume-packages/package-references-in-project-files.md)格式時, NuGet 4.0 + 可以直接在專案檔中儲存所有資訊清單中繼資料, 而不`.nuspec`是使用個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="52b89-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="52b89-106">使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。</span><span class="sxs-lookup"><span data-stu-id="52b89-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="52b89-107">這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。</span><span class="sxs-lookup"><span data-stu-id="52b89-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="52b89-108">如需使用 MSBuild 建立 NuGet 套件的指示, 請參閱[使用 Msbuild 建立 nuget 套件](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="52b89-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="52b89-109">(在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../reference/cli-reference/cli-ref-pack.md) 和 [restore](../reference/cli-reference/cli-ref-restore.md) 命令)。</span><span class="sxs-lookup"><span data-stu-id="52b89-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="52b89-110">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="52b89-110">Target build order</span></span>

<span data-ttu-id="52b89-111">因為 `pack` 和 `restore` 是 MSBuild 目標，所以您可以存取它們，以加強工作流程。</span><span class="sxs-lookup"><span data-stu-id="52b89-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="52b89-112">例如，假設您想要在封裝套件之後，將套件複製至網路共用。</span><span class="sxs-lookup"><span data-stu-id="52b89-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="52b89-113">做法是在專案檔中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="52b89-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="52b89-114">同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，以及在 MSBuild 工作中使用 NuGet 屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="52b89-115">`$(OutputPath)`是相對的, 而且預期您是從專案根目錄執行命令。</span><span class="sxs-lookup"><span data-stu-id="52b89-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="52b89-116">封裝目標</span><span class="sxs-lookup"><span data-stu-id="52b89-116">pack target</span></span>

<span data-ttu-id="52b89-117">對於使用 PackageReference 格式的 .NET Standard 專案, 使用`msbuild -t:pack`會從專案檔繪製輸入, 以用來建立 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="52b89-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="52b89-118">下表描述可新增至第一個 `<PropertyGroup>` 節點內之專案檔的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="52b89-119">以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。</span><span class="sxs-lookup"><span data-stu-id="52b89-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="52b89-120">為了方便起見，資料表是依 [`.nuspec` 檔案](../reference/nuspec.md)中的對等屬性進行組織。</span><span class="sxs-lookup"><span data-stu-id="52b89-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="52b89-121">請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="52b89-122">屬性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="52b89-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="52b89-123">MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="52b89-123">MSBuild Property</span></span> | <span data-ttu-id="52b89-124">預設</span><span class="sxs-lookup"><span data-stu-id="52b89-124">Default</span></span> | <span data-ttu-id="52b89-125">附註</span><span class="sxs-lookup"><span data-stu-id="52b89-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="52b89-126">ID</span><span class="sxs-lookup"><span data-stu-id="52b89-126">Id</span></span> | <span data-ttu-id="52b89-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="52b89-127">PackageId</span></span> | <span data-ttu-id="52b89-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="52b89-128">AssemblyName</span></span> | <span data-ttu-id="52b89-129">MSBuild 中的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="52b89-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="52b89-130">版本</span><span class="sxs-lookup"><span data-stu-id="52b89-130">Version</span></span> | <span data-ttu-id="52b89-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="52b89-131">PackageVersion</span></span> | <span data-ttu-id="52b89-132">版本</span><span class="sxs-lookup"><span data-stu-id="52b89-132">Version</span></span> | <span data-ttu-id="52b89-133">這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="52b89-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="52b89-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="52b89-134">VersionPrefix</span></span> | <span data-ttu-id="52b89-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="52b89-135">PackageVersionPrefix</span></span> | <span data-ttu-id="52b89-136">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-136">empty</span></span> | <span data-ttu-id="52b89-137">設定 PackageVersion 會覆寫 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="52b89-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="52b89-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="52b89-138">VersionSuffix</span></span> | <span data-ttu-id="52b89-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="52b89-139">PackageVersionSuffix</span></span> | <span data-ttu-id="52b89-140">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-140">empty</span></span> | <span data-ttu-id="52b89-141">MSBuild 中的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="52b89-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="52b89-142">設定 PackageVersion 會覆寫 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="52b89-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="52b89-143">作者</span><span class="sxs-lookup"><span data-stu-id="52b89-143">Authors</span></span> | <span data-ttu-id="52b89-144">作者</span><span class="sxs-lookup"><span data-stu-id="52b89-144">Authors</span></span> | <span data-ttu-id="52b89-145">目前使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="52b89-145">Username of the current user</span></span> | |
| <span data-ttu-id="52b89-146">Owners</span><span class="sxs-lookup"><span data-stu-id="52b89-146">Owners</span></span> | <span data-ttu-id="52b89-147">N/A</span><span class="sxs-lookup"><span data-stu-id="52b89-147">N/A</span></span> | <span data-ttu-id="52b89-148">NuSpec 中沒有</span><span class="sxs-lookup"><span data-stu-id="52b89-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="52b89-149">標題</span><span class="sxs-lookup"><span data-stu-id="52b89-149">Title</span></span> | <span data-ttu-id="52b89-150">標題</span><span class="sxs-lookup"><span data-stu-id="52b89-150">Title</span></span> | <span data-ttu-id="52b89-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="52b89-151">The PackageId</span></span>| |
| <span data-ttu-id="52b89-152">描述</span><span class="sxs-lookup"><span data-stu-id="52b89-152">Description</span></span> | <span data-ttu-id="52b89-153">描述</span><span class="sxs-lookup"><span data-stu-id="52b89-153">Description</span></span> | <span data-ttu-id="52b89-154">"Package Description"</span><span class="sxs-lookup"><span data-stu-id="52b89-154">"Package Description"</span></span> | |
| <span data-ttu-id="52b89-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="52b89-155">Copyright</span></span> | <span data-ttu-id="52b89-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="52b89-156">Copyright</span></span> | <span data-ttu-id="52b89-157">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-157">empty</span></span> | |
| <span data-ttu-id="52b89-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="52b89-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="52b89-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="52b89-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="52b89-160">False</span><span class="sxs-lookup"><span data-stu-id="52b89-160">false</span></span> | |
| <span data-ttu-id="52b89-161">執照</span><span class="sxs-lookup"><span data-stu-id="52b89-161">license</span></span> | <span data-ttu-id="52b89-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="52b89-162">PackageLicenseExpression</span></span> | <span data-ttu-id="52b89-163">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-163">empty</span></span> | <span data-ttu-id="52b89-164">對應至`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="52b89-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="52b89-165">執照</span><span class="sxs-lookup"><span data-stu-id="52b89-165">license</span></span> | <span data-ttu-id="52b89-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="52b89-166">PackageLicenseFile</span></span> | <span data-ttu-id="52b89-167">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-167">empty</span></span> | <span data-ttu-id="52b89-168">對應至 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="52b89-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="52b89-169">您可能需要明確地封裝參考的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="52b89-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="52b89-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-170">LicenseUrl</span></span> | <span data-ttu-id="52b89-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-171">PackageLicenseUrl</span></span> | <span data-ttu-id="52b89-172">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-172">empty</span></span> | <span data-ttu-id="52b89-173">`licenseUrl` 已被取代，使用 [PackageLicenseExpression] 或 PackageLicenseFile 屬性</span><span class="sxs-lookup"><span data-stu-id="52b89-173">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="52b89-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-174">ProjectUrl</span></span> | <span data-ttu-id="52b89-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-175">PackageProjectUrl</span></span> | <span data-ttu-id="52b89-176">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-176">empty</span></span> | |
| <span data-ttu-id="52b89-177">IconUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-177">IconUrl</span></span> | <span data-ttu-id="52b89-178">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-178">PackageIconUrl</span></span> | <span data-ttu-id="52b89-179">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-179">empty</span></span> | |
| <span data-ttu-id="52b89-180">Tags</span><span class="sxs-lookup"><span data-stu-id="52b89-180">Tags</span></span> | <span data-ttu-id="52b89-181">PackageTags</span><span class="sxs-lookup"><span data-stu-id="52b89-181">PackageTags</span></span> | <span data-ttu-id="52b89-182">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-182">empty</span></span> | <span data-ttu-id="52b89-183">以分號來分隔標記。</span><span class="sxs-lookup"><span data-stu-id="52b89-183">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="52b89-184">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="52b89-184">ReleaseNotes</span></span> | <span data-ttu-id="52b89-185">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="52b89-185">PackageReleaseNotes</span></span> | <span data-ttu-id="52b89-186">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-186">empty</span></span> | |
| <span data-ttu-id="52b89-187">存放庫/Url</span><span class="sxs-lookup"><span data-stu-id="52b89-187">Repository/Url</span></span> | <span data-ttu-id="52b89-188">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-188">RepositoryUrl</span></span> | <span data-ttu-id="52b89-189">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-189">empty</span></span> | <span data-ttu-id="52b89-190">用來複製或取出原始程式碼的存放庫 URL。</span><span class="sxs-lookup"><span data-stu-id="52b89-190">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="52b89-191">實例 *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="52b89-191">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="52b89-192">存放庫/類型</span><span class="sxs-lookup"><span data-stu-id="52b89-192">Repository/Type</span></span> | <span data-ttu-id="52b89-193">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="52b89-193">RepositoryType</span></span> | <span data-ttu-id="52b89-194">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-194">empty</span></span> | <span data-ttu-id="52b89-195">存放庫類型。</span><span class="sxs-lookup"><span data-stu-id="52b89-195">Repository type.</span></span> <span data-ttu-id="52b89-196">範例: *git*、 *tfs*。</span><span class="sxs-lookup"><span data-stu-id="52b89-196">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="52b89-197">存放庫/分支</span><span class="sxs-lookup"><span data-stu-id="52b89-197">Repository/Branch</span></span> | <span data-ttu-id="52b89-198">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="52b89-198">RepositoryBranch</span></span> | <span data-ttu-id="52b89-199">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-199">empty</span></span> | <span data-ttu-id="52b89-200">選擇性的存放庫分支資訊。</span><span class="sxs-lookup"><span data-stu-id="52b89-200">Optional repository branch information.</span></span> <span data-ttu-id="52b89-201">您也必須指定*RepositoryUrl* , 才能包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-201">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="52b89-202">範例: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="52b89-202">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="52b89-203">存放庫/認可</span><span class="sxs-lookup"><span data-stu-id="52b89-203">Repository/Commit</span></span> | <span data-ttu-id="52b89-204">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="52b89-204">RepositoryCommit</span></span> | <span data-ttu-id="52b89-205">空白</span><span class="sxs-lookup"><span data-stu-id="52b89-205">empty</span></span> | <span data-ttu-id="52b89-206">選擇性存放庫認可或變更集, 用來指出要建立封裝的來源。</span><span class="sxs-lookup"><span data-stu-id="52b89-206">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="52b89-207">您也必須指定*RepositoryUrl* , 才能包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="52b89-208">範例：*0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="52b89-208">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="52b89-209">PackageType</span><span class="sxs-lookup"><span data-stu-id="52b89-209">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="52b89-210">總結</span><span class="sxs-lookup"><span data-stu-id="52b89-210">Summary</span></span> | <span data-ttu-id="52b89-211">不支援</span><span class="sxs-lookup"><span data-stu-id="52b89-211">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="52b89-212">封裝目標輸入</span><span class="sxs-lookup"><span data-stu-id="52b89-212">pack target inputs</span></span>

- <span data-ttu-id="52b89-213">IsPackable</span><span class="sxs-lookup"><span data-stu-id="52b89-213">IsPackable</span></span>
- <span data-ttu-id="52b89-214">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="52b89-214">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="52b89-215">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="52b89-215">PackageVersion</span></span>
- <span data-ttu-id="52b89-216">PackageId</span><span class="sxs-lookup"><span data-stu-id="52b89-216">PackageId</span></span>
- <span data-ttu-id="52b89-217">作者</span><span class="sxs-lookup"><span data-stu-id="52b89-217">Authors</span></span>
- <span data-ttu-id="52b89-218">說明</span><span class="sxs-lookup"><span data-stu-id="52b89-218">Description</span></span>
- <span data-ttu-id="52b89-219">Copyright</span><span class="sxs-lookup"><span data-stu-id="52b89-219">Copyright</span></span>
- <span data-ttu-id="52b89-220">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="52b89-220">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="52b89-221">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="52b89-221">DevelopmentDependency</span></span>
- <span data-ttu-id="52b89-222">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="52b89-222">PackageLicenseExpression</span></span>
- <span data-ttu-id="52b89-223">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="52b89-223">PackageLicenseFile</span></span>
- <span data-ttu-id="52b89-224">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-224">PackageLicenseUrl</span></span>
- <span data-ttu-id="52b89-225">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-225">PackageProjectUrl</span></span>
- <span data-ttu-id="52b89-226">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-226">PackageIconUrl</span></span>
- <span data-ttu-id="52b89-227">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="52b89-227">PackageReleaseNotes</span></span>
- <span data-ttu-id="52b89-228">PackageTags</span><span class="sxs-lookup"><span data-stu-id="52b89-228">PackageTags</span></span>
- <span data-ttu-id="52b89-229">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="52b89-229">PackageOutputPath</span></span>
- <span data-ttu-id="52b89-230">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="52b89-230">IncludeSymbols</span></span>
- <span data-ttu-id="52b89-231">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="52b89-231">IncludeSource</span></span>
- <span data-ttu-id="52b89-232">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="52b89-232">PackageTypes</span></span>
- <span data-ttu-id="52b89-233">IsTool</span><span class="sxs-lookup"><span data-stu-id="52b89-233">IsTool</span></span>
- <span data-ttu-id="52b89-234">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-234">RepositoryUrl</span></span>
- <span data-ttu-id="52b89-235">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="52b89-235">RepositoryType</span></span>
- <span data-ttu-id="52b89-236">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="52b89-236">RepositoryBranch</span></span>
- <span data-ttu-id="52b89-237">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="52b89-237">RepositoryCommit</span></span>
- <span data-ttu-id="52b89-238">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="52b89-238">NoPackageAnalysis</span></span>
- <span data-ttu-id="52b89-239">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="52b89-239">MinClientVersion</span></span>
- <span data-ttu-id="52b89-240">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="52b89-240">IncludeBuildOutput</span></span>
- <span data-ttu-id="52b89-241">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="52b89-241">IncludeContentInPack</span></span>
- <span data-ttu-id="52b89-242">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="52b89-242">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="52b89-243">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="52b89-243">ContentTargetFolders</span></span>
- <span data-ttu-id="52b89-244">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="52b89-244">NuspecFile</span></span>
- <span data-ttu-id="52b89-245">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="52b89-245">NuspecBasePath</span></span>
- <span data-ttu-id="52b89-246">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="52b89-246">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="52b89-247">封裝案例</span><span class="sxs-lookup"><span data-stu-id="52b89-247">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="52b89-248">隱藏相依性</span><span class="sxs-lookup"><span data-stu-id="52b89-248">Suppress dependencies</span></span>

<span data-ttu-id="52b89-249">若要隱藏產生的 NuGet 套件中的套件`SuppressDependenciesWhenPacking`相依`true`性, 請將設定為, 允許從產生的 nupkg 檔略過所有相依性。</span><span class="sxs-lookup"><span data-stu-id="52b89-249">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="52b89-250">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="52b89-250">PackageIconUrl</span></span>

<span data-ttu-id="52b89-251">在[NuGet 問題 352](https://github.com/NuGet/Home/issues/352)的變更過程中, 最後`PackageIconUrl`將會變更為`PackageIconUri` , 而且可以是圖示檔案的相對路徑, 該檔案會包含在所產生套件的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="52b89-251">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="52b89-252">輸出組件</span><span class="sxs-lookup"><span data-stu-id="52b89-252">Output assemblies</span></span>

<span data-ttu-id="52b89-253">`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="52b89-253">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="52b89-254">所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。</span><span class="sxs-lookup"><span data-stu-id="52b89-254">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="52b89-255">在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：</span><span class="sxs-lookup"><span data-stu-id="52b89-255">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="52b89-256">`IncludeBuildOutput`：布林值, 判斷組建輸出元件是否應包含在封裝中。</span><span class="sxs-lookup"><span data-stu-id="52b89-256">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="52b89-257">`BuildOutputTargetFolder`：指定應該放置輸出元件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="52b89-257">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="52b89-258">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="52b89-258">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="52b89-259">套件參考</span><span class="sxs-lookup"><span data-stu-id="52b89-259">Package references</span></span>

<span data-ttu-id="52b89-260">請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。</span><span class="sxs-lookup"><span data-stu-id="52b89-260">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="52b89-261">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="52b89-261">Project to project references</span></span>

<span data-ttu-id="52b89-262">預設會將專案對專案參考視為 NuGet 套件參考，例如：</span><span class="sxs-lookup"><span data-stu-id="52b89-262">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="52b89-263">您也可以將下列中繼資料新增至您的專案參考：</span><span class="sxs-lookup"><span data-stu-id="52b89-263">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="52b89-264">在套件內包含內容</span><span class="sxs-lookup"><span data-stu-id="52b89-264">Including content in a package</span></span>

<span data-ttu-id="52b89-265">若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。</span><span class="sxs-lookup"><span data-stu-id="52b89-265">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="52b89-266">除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：</span><span class="sxs-lookup"><span data-stu-id="52b89-266">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="52b89-267">除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="52b89-267">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="52b89-268">如果您想要將所有內容都只複製至特定根資料夾 (而不是 `content` 和 `contentFiles`)，則可以使用 MSBuild 屬性 `ContentTargetFolders`，其預設為 "content;contentFiles"，但可以設定為任何其他資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="52b89-268">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="52b89-269">請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。</span><span class="sxs-lookup"><span data-stu-id="52b89-269">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="52b89-270">`PackagePath` 可以是以分號分隔的一組目標路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-270">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="52b89-271">指定空的套件路徑會將檔案新增至套件的根目錄。</span><span class="sxs-lookup"><span data-stu-id="52b89-271">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="52b89-272">例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：</span><span class="sxs-lookup"><span data-stu-id="52b89-272">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="52b89-273">另有 MSBuild 屬性 `$(IncludeContentInPack)` 預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="52b89-273">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="52b89-274">如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。</span><span class="sxs-lookup"><span data-stu-id="52b89-274">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="52b89-275">您可在上述任何項目上設定的其他封裝特定中繼資料包含 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，其在輸出 nuspec 的 ```contentFiles``` 項目上設定 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="52b89-275">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="52b89-276">除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="52b89-276">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="52b89-277">針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-277">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="52b89-278">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="52b89-278">IncludeSymbols</span></span>

<span data-ttu-id="52b89-279">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。</span><span class="sxs-lookup"><span data-stu-id="52b89-279">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="52b89-280">請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。</span><span class="sxs-lookup"><span data-stu-id="52b89-280">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="52b89-281">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="52b89-281">IncludeSource</span></span>

<span data-ttu-id="52b89-282">這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。</span><span class="sxs-lookup"><span data-stu-id="52b89-282">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="52b89-283">所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="52b89-283">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="52b89-284">這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="52b89-284">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="52b89-285">若類型為 Compile 的檔案位於專案資料夾之外，就只會將其新增至 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="52b89-285">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="52b89-286">封裝授權運算式或授權檔案</span><span class="sxs-lookup"><span data-stu-id="52b89-286">Packing a license expression or a license file</span></span>

<span data-ttu-id="52b89-287">使用授權運算式時, 應該使用 PackageLicenseExpression 屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-287">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="52b89-288">[授權運算式範例](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="52b89-288">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="52b89-289">[深入瞭解 NuGet.org 所接受的授權運算式和](nuspec.md#license)授權。</span><span class="sxs-lookup"><span data-stu-id="52b89-289">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="52b89-290">封裝授權檔案時, 您必須使用 PackageLicenseFile 屬性來指定相對於封裝根目錄的封裝路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-290">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="52b89-291">此外, 您必須確定檔案已包含在封裝中。</span><span class="sxs-lookup"><span data-stu-id="52b89-291">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="52b89-292">例如：</span><span class="sxs-lookup"><span data-stu-id="52b89-292">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="52b89-293">[授權檔案範例](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="52b89-293">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="52b89-294">IsTool</span><span class="sxs-lookup"><span data-stu-id="52b89-294">IsTool</span></span>

<span data-ttu-id="52b89-295">使用 `MSBuild -t:pack -p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="52b89-295">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="52b89-296">請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。</span><span class="sxs-lookup"><span data-stu-id="52b89-296">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="52b89-297">使用 .nuspec 封裝</span><span class="sxs-lookup"><span data-stu-id="52b89-297">Packing using a .nuspec</span></span>

<span data-ttu-id="52b89-298">雖然建議您改為在專案檔中包含檔案中的[所有屬性](../reference/msbuild-targets.md#pack-target) `.nuspec` , 但您可以`.nuspec`選擇使用檔案來封裝專案。</span><span class="sxs-lookup"><span data-stu-id="52b89-298">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="52b89-299">若為使用`PackageReference`的非 SDK 樣式專案, 您必須匯入`NuGet.Build.Tasks.Pack.targets` , 才能執行封裝工作。</span><span class="sxs-lookup"><span data-stu-id="52b89-299">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="52b89-300">您仍然需要還原專案, 才能封裝 nuspec 檔案。</span><span class="sxs-lookup"><span data-stu-id="52b89-300">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="52b89-301">(根據預設, SDK 樣式專案包含套件目標)。</span><span class="sxs-lookup"><span data-stu-id="52b89-301">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="52b89-302">專案檔的目標 framework 不相關, 也不會在封裝 nuspec 時使用。</span><span class="sxs-lookup"><span data-stu-id="52b89-302">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="52b89-303">下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：</span><span class="sxs-lookup"><span data-stu-id="52b89-303">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="52b89-304">`NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-304">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="52b89-305">`NuspecProperties`：以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="52b89-305">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="52b89-306">基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`-p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="52b89-306">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="52b89-307">`NuspecBasePath`：檔案的`.nuspec`基底路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-307">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="52b89-308">如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="52b89-308">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="52b89-309">如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="52b89-309">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="52b89-310">請注意, 使用 dotnet 封裝 nuspec 或 msbuild 也會導致預設建立專案。</span><span class="sxs-lookup"><span data-stu-id="52b89-310">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="52b89-311">藉由將屬性傳遞```--no-build```至 dotnet, 即可避免這種情況, 這相當於您專案檔中的設定```<NoBuild>true</NoBuild> ``` , 以及專案```<IncludeBuildOutput>false</IncludeBuildOutput> ```檔中的設定。</span><span class="sxs-lookup"><span data-stu-id="52b89-311">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="52b89-312">封裝 nuspec 檔案的 *.csproj*檔案範例如下:</span><span class="sxs-lookup"><span data-stu-id="52b89-312">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="52b89-313">用來建立自訂套件的先進擴充功能點</span><span class="sxs-lookup"><span data-stu-id="52b89-313">Advanced extension points to create customized package</span></span>

<span data-ttu-id="52b89-314">`pack`目標提供兩個擴充點, 可在內部、目標 framework 特定組建中執行。</span><span class="sxs-lookup"><span data-stu-id="52b89-314">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="52b89-315">擴充點支援將目標 framework 特定的內容和元件包含在封裝中:</span><span class="sxs-lookup"><span data-stu-id="52b89-315">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="52b89-316">`TargetsForTfmSpecificBuildOutput`設定用於資料夾內的`lib`檔案, 或使用`BuildOutputTargetFolder`指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="52b89-316">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="52b89-317">`TargetsForTfmSpecificContentInPackage`設定用於以外的`BuildOutputTargetFolder`檔案。</span><span class="sxs-lookup"><span data-stu-id="52b89-317">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="52b89-318">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="52b89-318">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="52b89-319">撰寫自訂目標, 並將它指定為`$(TargetsForTfmSpecificBuildOutput)`屬性的值。</span><span class="sxs-lookup"><span data-stu-id="52b89-319">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="52b89-320">對於需要移入的`BuildOutputTargetFolder`任何檔案 (預設為 lib), 目標應該將這些檔案寫入至 ItemGroup `BuildOutputInPackage` , 並設定下列兩個中繼資料值:</span><span class="sxs-lookup"><span data-stu-id="52b89-320">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="52b89-321">`FinalOutputPath`：檔案的絕對路徑;如果未提供, 則會使用身分識別來評估來源路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-321">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="52b89-322">`TargetPath`：選擇性當檔案需要進入中`lib\<TargetFramework>`的子資料夾時設定, 例如在其各自的文化特性資料夾下的附屬元件。</span><span class="sxs-lookup"><span data-stu-id="52b89-322">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="52b89-323">預設為檔案名。</span><span class="sxs-lookup"><span data-stu-id="52b89-323">Defaults to the name of the file.</span></span>

<span data-ttu-id="52b89-324">範例：</span><span class="sxs-lookup"><span data-stu-id="52b89-324">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="52b89-325">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="52b89-325">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="52b89-326">撰寫自訂目標, 並將它指定為`$(TargetsForTfmSpecificContentInPackage)`屬性的值。</span><span class="sxs-lookup"><span data-stu-id="52b89-326">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="52b89-327">針對要包含在封裝中的任何檔案, 目標應該將這些檔案寫入 ItemGroup `TfmSpecificPackageFile` , 並設定下列選擇性中繼資料:</span><span class="sxs-lookup"><span data-stu-id="52b89-327">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="52b89-328">`PackagePath`：封裝中應該輸出檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-328">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="52b89-329">如果將多個檔案新增至相同的封裝路徑, NuGet 就會發出警告。</span><span class="sxs-lookup"><span data-stu-id="52b89-329">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="52b89-330">`BuildAction`：要指派給檔案的組建動作, 只有在封裝路徑位於`contentFiles`資料夾中時才需要。</span><span class="sxs-lookup"><span data-stu-id="52b89-330">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="52b89-331">預設值為 "None"。</span><span class="sxs-lookup"><span data-stu-id="52b89-331">Defaults to "None".</span></span>

<span data-ttu-id="52b89-332">範例:</span><span class="sxs-lookup"><span data-stu-id="52b89-332">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="52b89-333">還原目標</span><span class="sxs-lookup"><span data-stu-id="52b89-333">restore target</span></span>

<span data-ttu-id="52b89-334">`MSBuild -t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="52b89-334">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="52b89-335">讀取所有專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="52b89-335">Read all project to project references</span></span>
1. <span data-ttu-id="52b89-336">讀取專案屬性來尋找中繼資料夾和目標架構</span><span class="sxs-lookup"><span data-stu-id="52b89-336">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="52b89-337">將 MSBuild 資料傳遞至 Nuget.exe。 .dll</span><span class="sxs-lookup"><span data-stu-id="52b89-337">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="52b89-338">執行還原</span><span class="sxs-lookup"><span data-stu-id="52b89-338">Run restore</span></span>
1. <span data-ttu-id="52b89-339">下載套件</span><span class="sxs-lookup"><span data-stu-id="52b89-339">Download packages</span></span>
1. <span data-ttu-id="52b89-340">撰寫資產檔案、目標和屬性</span><span class="sxs-lookup"><span data-stu-id="52b89-340">Write assets file, targets, and props</span></span>

<span data-ttu-id="52b89-341">目標僅適用于使用 PackageReference 格式的專案。 `restore`</span><span class="sxs-lookup"><span data-stu-id="52b89-341">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="52b89-342">其不適用於使用格式的`packages.config`專案; 請改用[nuget 還原](../reference/cli-reference/cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="52b89-342">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="52b89-343">還原屬性</span><span class="sxs-lookup"><span data-stu-id="52b89-343">Restore properties</span></span>

<span data-ttu-id="52b89-344">其他還原設定可能來自專案檔中的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-344">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="52b89-345">您也可以從命令列，使用 `-p:` 參數設定值 (請參閱下列＜範例＞)。</span><span class="sxs-lookup"><span data-stu-id="52b89-345">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="52b89-346">屬性</span><span class="sxs-lookup"><span data-stu-id="52b89-346">Property</span></span> | <span data-ttu-id="52b89-347">描述</span><span class="sxs-lookup"><span data-stu-id="52b89-347">Description</span></span> |
|--------|--------|
| <span data-ttu-id="52b89-348">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="52b89-348">RestoreSources</span></span> | <span data-ttu-id="52b89-349">以分號分隔的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="52b89-349">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="52b89-350">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="52b89-350">RestorePackagesPath</span></span> | <span data-ttu-id="52b89-351">使用者套件資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-351">User packages folder path.</span></span> |
| <span data-ttu-id="52b89-352">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="52b89-352">RestoreDisableParallel</span></span> | <span data-ttu-id="52b89-353">限制逐一進行下載。</span><span class="sxs-lookup"><span data-stu-id="52b89-353">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="52b89-354">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="52b89-354">RestoreConfigFile</span></span> | <span data-ttu-id="52b89-355">要套用之 `Nuget.Config` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-355">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="52b89-356">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="52b89-356">RestoreNoCache</span></span> | <span data-ttu-id="52b89-357">若為 true, 則避免使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="52b89-357">If true, avoids using cached packages.</span></span> <span data-ttu-id="52b89-358">請參閱[管理全域套件和](../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="52b89-358">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="52b89-359">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="52b89-359">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="52b89-360">如果為 true，請忽略失敗或遺漏的套件來源。</span><span class="sxs-lookup"><span data-stu-id="52b89-360">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="52b89-361">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="52b89-361">RestoreFallbackFolders</span></span> | <span data-ttu-id="52b89-362">回溯資料夾, 其使用方式與使用者套件資料夾相同。</span><span class="sxs-lookup"><span data-stu-id="52b89-362">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="52b89-363">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="52b89-363">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="52b89-364">還原期間要使用的其他來源。</span><span class="sxs-lookup"><span data-stu-id="52b89-364">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="52b89-365">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="52b89-365">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="52b89-366">還原期間要使用的其他 fallback 資料夾。</span><span class="sxs-lookup"><span data-stu-id="52b89-366">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="52b89-367">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="52b89-367">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="52b89-368">排除在中指定的 fallback 資料夾`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="52b89-368">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="52b89-369">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="52b89-369">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="52b89-370">`NuGet.Build.Tasks.dll` 的路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-370">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="52b89-371">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="52b89-371">RestoreGraphProjectInput</span></span> | <span data-ttu-id="52b89-372">要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="52b89-372">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="52b89-373">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="52b89-373">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="52b89-374">透過 MSBuild 收集項目時, 它會決定是否使用`SkipNonexistentTargets`優化進行收集。</span><span class="sxs-lookup"><span data-stu-id="52b89-374">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="52b89-375">[未設定] 時, `true`預設為。</span><span class="sxs-lookup"><span data-stu-id="52b89-375">When not set, defaults to `true`.</span></span> <span data-ttu-id="52b89-376">當無法匯入專案的目標時, 結果會是失敗快速的行為。</span><span class="sxs-lookup"><span data-stu-id="52b89-376">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="52b89-377">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="52b89-377">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="52b89-378">輸出檔案夾, 預設為`BaseIntermediateOutputPath` `obj`和資料夾。</span><span class="sxs-lookup"><span data-stu-id="52b89-378">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="52b89-379">範例</span><span class="sxs-lookup"><span data-stu-id="52b89-379">Examples</span></span>

<span data-ttu-id="52b89-380">命令列：</span><span class="sxs-lookup"><span data-stu-id="52b89-380">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="52b89-381">專案檔：</span><span class="sxs-lookup"><span data-stu-id="52b89-381">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="52b89-382">Restore outputs</span><span class="sxs-lookup"><span data-stu-id="52b89-382">Restore outputs</span></span>

<span data-ttu-id="52b89-383">還原會在組建 `obj` 資料夾中建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="52b89-383">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="52b89-384">檔案</span><span class="sxs-lookup"><span data-stu-id="52b89-384">File</span></span> | <span data-ttu-id="52b89-385">描述</span><span class="sxs-lookup"><span data-stu-id="52b89-385">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="52b89-386">包含所有封裝參考的相依性圖形。</span><span class="sxs-lookup"><span data-stu-id="52b89-386">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="52b89-387">套件中所含 MSBuild 屬性的參考</span><span class="sxs-lookup"><span data-stu-id="52b89-387">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="52b89-388">套件中所含 MSBuild 目標的參考</span><span class="sxs-lookup"><span data-stu-id="52b89-388">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="52b89-389">使用一個 MSBuild 命令還原和建立</span><span class="sxs-lookup"><span data-stu-id="52b89-389">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="52b89-390">因為 NuGet 可以還原會導致 MSBuild 目標和 .props 的封裝, 所以還原和組建評估會以不同的全域屬性執行。</span><span class="sxs-lookup"><span data-stu-id="52b89-390">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="52b89-391">這表示下列程式將會有無法預測且通常不正確的行為。</span><span class="sxs-lookup"><span data-stu-id="52b89-391">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="52b89-392">相反地, 建議的方法是:</span><span class="sxs-lookup"><span data-stu-id="52b89-392">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="52b89-393">相同的邏輯也適用于類似`build`的其他目標。</span><span class="sxs-lookup"><span data-stu-id="52b89-393">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="52b89-394">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="52b89-394">PackageTargetFallback</span></span>

<span data-ttu-id="52b89-395">`PackageTargetFallback` 項目可讓您指定一組要在還原套件時使用的相容目標。</span><span class="sxs-lookup"><span data-stu-id="52b89-395">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="52b89-396">其設計目的是要讓使用 dotnet [TxM](../reference/target-frameworks.md) 的套件可以與未宣告 dotnet TxM 的相容套件一起運作。</span><span class="sxs-lookup"><span data-stu-id="52b89-396">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="52b89-397">也就是說，如果您的專案使用 dotnet TxM，除非您將 `<PackageTargetFallback>` 新增至專案，以讓非 dotnet 平台變成與 dotnet 相容，否則其相依的所有套件也必須要有 dotnet TxM。</span><span class="sxs-lookup"><span data-stu-id="52b89-397">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="52b89-398">例如，如果專案使用 `netstandard1.6` TxM，而且相依套件僅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，則無法建置專案。</span><span class="sxs-lookup"><span data-stu-id="52b89-398">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="52b89-399">如果您想要匯入的是第二個 DLL，則可以如下新增 `PackageTargetFallback`，指出 `portable-net45+win81` DLL 相容：</span><span class="sxs-lookup"><span data-stu-id="52b89-399">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="52b89-400">若要宣告專案中所有目標的後援，請省略 `Condition` 屬性。</span><span class="sxs-lookup"><span data-stu-id="52b89-400">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="52b89-401">您也可以包含 `$(PackageTargetFallback)` 來擴充任何現有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="52b89-401">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="52b89-402">取代還原圖形中的一個程式庫</span><span class="sxs-lookup"><span data-stu-id="52b89-402">Replacing one library from a restore graph</span></span>

<span data-ttu-id="52b89-403">如果還原內含錯誤的組件，您可以排除該套件預設選項，並將其取代為您自己的選項。</span><span class="sxs-lookup"><span data-stu-id="52b89-403">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="52b89-404">首先，會有最上層 `PackageReference`，但排除所有資產：</span><span class="sxs-lookup"><span data-stu-id="52b89-404">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="52b89-405">接下來，新增您自己對 DLL 之適當本機複本的參考：</span><span class="sxs-lookup"><span data-stu-id="52b89-405">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
