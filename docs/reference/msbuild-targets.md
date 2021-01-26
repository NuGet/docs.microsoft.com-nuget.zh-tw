---
title: NuGet 封裝和還原為 MSBuild 目標
description: 使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777714"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="d4d60-103">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="d4d60-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="d4d60-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="d4d60-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="d4d60-105">使用 [PackageReference](../consume-packages/package-references-in-project-files.md) 格式時，NuGet 4.0 + 可以直接將所有資訊清單中繼資料儲存在專案檔中，而不是使用個別的檔案 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="d4d60-106">使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。</span><span class="sxs-lookup"><span data-stu-id="d4d60-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="d4d60-107">這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。</span><span class="sxs-lookup"><span data-stu-id="d4d60-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="d4d60-108">如需使用 MSBuild 建立 NuGet 套件的指示，請參閱 [使用 Msbuild 建立 nuget 套件](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="d4d60-109">(在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../reference/cli-reference/cli-ref-pack.md) 和 [restore](../reference/cli-reference/cli-ref-restore.md) 命令)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="d4d60-110">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="d4d60-110">Target build order</span></span>

<span data-ttu-id="d4d60-111">因為 `pack` 和 `restore` 是 MSBuild 目標，所以您可以存取它們，以加強工作流程。</span><span class="sxs-lookup"><span data-stu-id="d4d60-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="d4d60-112">例如，假設您想要在封裝套件之後，將套件複製至網路共用。</span><span class="sxs-lookup"><span data-stu-id="d4d60-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="d4d60-113">做法是在專案檔中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="d4d60-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="d4d60-114">同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，以及在 MSBuild 工作中使用 NuGet 屬性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="d4d60-115">`$(OutputPath)` 是相對的，且預期您是從專案根目錄執行命令。</span><span class="sxs-lookup"><span data-stu-id="d4d60-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="d4d60-116">封裝目標</span><span class="sxs-lookup"><span data-stu-id="d4d60-116">pack target</span></span>

<span data-ttu-id="d4d60-117">針對使用格式的 .NET 專案 `PackageReference` ，使用會 `msbuild -t:pack` 從專案檔繪製輸入，以用於建立 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="d4d60-118">下表描述可新增至第一個節點內之專案檔的 MSBuild 屬性 `<PropertyGroup>` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="d4d60-119">以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。</span><span class="sxs-lookup"><span data-stu-id="d4d60-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="d4d60-120">為了方便起見，資料表會依照檔案中的對等屬性進行[ `.nuspec` 組織。](../reference/nuspec.md)</span><span class="sxs-lookup"><span data-stu-id="d4d60-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="d4d60-121">請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="d4d60-122">屬性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="d4d60-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="d4d60-123">MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="d4d60-123">MSBuild Property</span></span> | <span data-ttu-id="d4d60-124">預設</span><span class="sxs-lookup"><span data-stu-id="d4d60-124">Default</span></span> | <span data-ttu-id="d4d60-125">備註</span><span class="sxs-lookup"><span data-stu-id="d4d60-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="d4d60-126">識別碼</span><span class="sxs-lookup"><span data-stu-id="d4d60-126">Id</span></span> | <span data-ttu-id="d4d60-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="d4d60-127">PackageId</span></span> | <span data-ttu-id="d4d60-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="d4d60-128">AssemblyName</span></span> | <span data-ttu-id="d4d60-129">MSBuild 中的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="d4d60-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="d4d60-130">版本</span><span class="sxs-lookup"><span data-stu-id="d4d60-130">Version</span></span> | <span data-ttu-id="d4d60-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d4d60-131">PackageVersion</span></span> | <span data-ttu-id="d4d60-132">版本</span><span class="sxs-lookup"><span data-stu-id="d4d60-132">Version</span></span> | <span data-ttu-id="d4d60-133">這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="d4d60-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="d4d60-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d4d60-134">VersionPrefix</span></span> | <span data-ttu-id="d4d60-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d4d60-135">PackageVersionPrefix</span></span> | <span data-ttu-id="d4d60-136">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-136">empty</span></span> | <span data-ttu-id="d4d60-137">設定 PackageVersion 會覆寫 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d4d60-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="d4d60-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d4d60-138">VersionSuffix</span></span> | <span data-ttu-id="d4d60-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d4d60-139">PackageVersionSuffix</span></span> | <span data-ttu-id="d4d60-140">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-140">empty</span></span> | <span data-ttu-id="d4d60-141">MSBuild 中的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="d4d60-142">設定 PackageVersion 會覆寫 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d4d60-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="d4d60-143">Authors</span><span class="sxs-lookup"><span data-stu-id="d4d60-143">Authors</span></span> | <span data-ttu-id="d4d60-144">Authors</span><span class="sxs-lookup"><span data-stu-id="d4d60-144">Authors</span></span> | <span data-ttu-id="d4d60-145">目前使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d4d60-145">Username of the current user</span></span> | <span data-ttu-id="d4d60-146">以分號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些會顯示在 nuget.org 的 NuGet 元件庫中，並用來交互參照相同作者的封裝。</span><span class="sxs-lookup"><span data-stu-id="d4d60-146">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="d4d60-147">擁有者</span><span class="sxs-lookup"><span data-stu-id="d4d60-147">Owners</span></span> | <span data-ttu-id="d4d60-148">N/A</span><span class="sxs-lookup"><span data-stu-id="d4d60-148">N/A</span></span> | <span data-ttu-id="d4d60-149">NuSpec 中沒有</span><span class="sxs-lookup"><span data-stu-id="d4d60-149">Not present in NuSpec</span></span> | |
| <span data-ttu-id="d4d60-150">標題</span><span class="sxs-lookup"><span data-stu-id="d4d60-150">Title</span></span> | <span data-ttu-id="d4d60-151">標題</span><span class="sxs-lookup"><span data-stu-id="d4d60-151">Title</span></span> | <span data-ttu-id="d4d60-152">PackageId</span><span class="sxs-lookup"><span data-stu-id="d4d60-152">The PackageId</span></span>| <span data-ttu-id="d4d60-153">套件的易記標題，通常會用於 UI 顯示，以及 nuget.org 和 Visual Studio 套件管理員中。</span><span class="sxs-lookup"><span data-stu-id="d4d60-153">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| <span data-ttu-id="d4d60-154">描述</span><span class="sxs-lookup"><span data-stu-id="d4d60-154">Description</span></span> | <span data-ttu-id="d4d60-155">描述</span><span class="sxs-lookup"><span data-stu-id="d4d60-155">Description</span></span> | <span data-ttu-id="d4d60-156">"Package Description"</span><span class="sxs-lookup"><span data-stu-id="d4d60-156">"Package Description"</span></span> | <span data-ttu-id="d4d60-157">組件的完整描述。</span><span class="sxs-lookup"><span data-stu-id="d4d60-157">A long description for the assembly.</span></span> <span data-ttu-id="d4d60-158">如果 `PackageDescription` 未指定，則此屬性也會用來做為封裝的描述。</span><span class="sxs-lookup"><span data-stu-id="d4d60-158">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="d4d60-159">著作權</span><span class="sxs-lookup"><span data-stu-id="d4d60-159">Copyright</span></span> | <span data-ttu-id="d4d60-160">著作權</span><span class="sxs-lookup"><span data-stu-id="d4d60-160">Copyright</span></span> | <span data-ttu-id="d4d60-161">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-161">empty</span></span> | <span data-ttu-id="d4d60-162">套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4d60-162">Copyright details for the package.</span></span> |
| <span data-ttu-id="d4d60-163">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d4d60-163">RequireLicenseAcceptance</span></span> | <span data-ttu-id="d4d60-164">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d4d60-164">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="d4d60-165">false</span><span class="sxs-lookup"><span data-stu-id="d4d60-165">false</span></span> | <span data-ttu-id="d4d60-166">布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。</span><span class="sxs-lookup"><span data-stu-id="d4d60-166">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="d4d60-167">授權</span><span class="sxs-lookup"><span data-stu-id="d4d60-167">license</span></span> | <span data-ttu-id="d4d60-168">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d4d60-168">PackageLicenseExpression</span></span> | <span data-ttu-id="d4d60-169">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-169">empty</span></span> | <span data-ttu-id="d4d60-170">對應至 `<license type="expression">`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-170">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="d4d60-171">請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-171">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="d4d60-172">授權</span><span class="sxs-lookup"><span data-stu-id="d4d60-172">license</span></span> | <span data-ttu-id="d4d60-173">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d4d60-173">PackageLicenseFile</span></span> | <span data-ttu-id="d4d60-174">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-174">empty</span></span> | <span data-ttu-id="d4d60-175">如果您使用自訂授權或未獲指派 SPDX 識別碼的授權，則為套件內的授權檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-175">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="d4d60-176">您必須明確地封裝參考的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-176">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="d4d60-177">對應至 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-177">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="d4d60-178">請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-178">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="d4d60-179">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-179">LicenseUrl</span></span> | <span data-ttu-id="d4d60-180">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-180">PackageLicenseUrl</span></span> | <span data-ttu-id="d4d60-181">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-181">empty</span></span> | <span data-ttu-id="d4d60-182">`PackageLicenseUrl` 已被取代。</span><span class="sxs-lookup"><span data-stu-id="d4d60-182">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="d4d60-183">請改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-183">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="d4d60-184">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-184">ProjectUrl</span></span> | <span data-ttu-id="d4d60-185">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-185">PackageProjectUrl</span></span> | <span data-ttu-id="d4d60-186">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-186">empty</span></span> | |
| <span data-ttu-id="d4d60-187">圖示</span><span class="sxs-lookup"><span data-stu-id="d4d60-187">Icon</span></span> | <span data-ttu-id="d4d60-188">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="d4d60-188">PackageIcon</span></span> | <span data-ttu-id="d4d60-189">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-189">empty</span></span> | <span data-ttu-id="d4d60-190">封裝中用來做為封裝圖示的影像路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-190">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="d4d60-191">您必須明確地封裝參考的圖示影像檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-191">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="d4d60-192">如需詳細資訊，請參閱[封裝圖示影像檔](#packing-an-icon-image-file)案和[ `icon` 中繼資料](/nuget/reference/nuspec#icon)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-192">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| <span data-ttu-id="d4d60-193">IconUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-193">IconUrl</span></span> | <span data-ttu-id="d4d60-194">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-194">PackageIconUrl</span></span> | <span data-ttu-id="d4d60-195">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-195">empty</span></span> | <span data-ttu-id="d4d60-196">`PackageIconUrl` 已被取代，改為使用 `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-196">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="d4d60-197">但是，為了獲得最佳的早期體驗，除了之外，您還應該指定 `PackageIconUrl` `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-197">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| <span data-ttu-id="d4d60-198">標籤</span><span class="sxs-lookup"><span data-stu-id="d4d60-198">Tags</span></span> | <span data-ttu-id="d4d60-199">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d4d60-199">PackageTags</span></span> | <span data-ttu-id="d4d60-200">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-200">empty</span></span> | <span data-ttu-id="d4d60-201">以分號分隔的標記清單，用以指定套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-201">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="d4d60-202">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d4d60-202">ReleaseNotes</span></span> | <span data-ttu-id="d4d60-203">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d4d60-203">PackageReleaseNotes</span></span> | <span data-ttu-id="d4d60-204">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-204">empty</span></span> | <span data-ttu-id="d4d60-205">套件的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d4d60-205">Release notes for the package.</span></span> |
| <span data-ttu-id="d4d60-206">存放庫/Url</span><span class="sxs-lookup"><span data-stu-id="d4d60-206">Repository/Url</span></span> | <span data-ttu-id="d4d60-207">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-207">RepositoryUrl</span></span> | <span data-ttu-id="d4d60-208">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-208">empty</span></span> | <span data-ttu-id="d4d60-209">用來複製或取出原始程式碼的儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="d4d60-209">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="d4d60-210">範例： *https://github.com/NuGet/NuGet.Client.git* 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-210">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="d4d60-211">存放庫/類型</span><span class="sxs-lookup"><span data-stu-id="d4d60-211">Repository/Type</span></span> | <span data-ttu-id="d4d60-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d4d60-212">RepositoryType</span></span> | <span data-ttu-id="d4d60-213">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-213">empty</span></span> | <span data-ttu-id="d4d60-214">存放庫類型。</span><span class="sxs-lookup"><span data-stu-id="d4d60-214">Repository type.</span></span> <span data-ttu-id="d4d60-215">範例： `git` (預設) ， `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-215">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="d4d60-216">存放庫/分支</span><span class="sxs-lookup"><span data-stu-id="d4d60-216">Repository/Branch</span></span> | <span data-ttu-id="d4d60-217">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d4d60-217">RepositoryBranch</span></span> | <span data-ttu-id="d4d60-218">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-218">empty</span></span> | <span data-ttu-id="d4d60-219">選用的存放庫分支資訊。</span><span class="sxs-lookup"><span data-stu-id="d4d60-219">Optional repository branch information.</span></span> <span data-ttu-id="d4d60-220">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="d4d60-220">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="d4d60-221">範例： *master* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-221">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="d4d60-222">儲存機制/認可</span><span class="sxs-lookup"><span data-stu-id="d4d60-222">Repository/Commit</span></span> | <span data-ttu-id="d4d60-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d4d60-223">RepositoryCommit</span></span> | <span data-ttu-id="d4d60-224">empty</span><span class="sxs-lookup"><span data-stu-id="d4d60-224">empty</span></span> | <span data-ttu-id="d4d60-225">選用的儲存機制認可或變更集，以指出建立封裝的來源。</span><span class="sxs-lookup"><span data-stu-id="d4d60-225">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="d4d60-226">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="d4d60-226">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="d4d60-227">範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-227">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="d4d60-228">PackageType</span><span class="sxs-lookup"><span data-stu-id="d4d60-228">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="d4d60-229">摘要</span><span class="sxs-lookup"><span data-stu-id="d4d60-229">Summary</span></span> | <span data-ttu-id="d4d60-230">不支援</span><span class="sxs-lookup"><span data-stu-id="d4d60-230">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="d4d60-231">封裝目標輸入</span><span class="sxs-lookup"><span data-stu-id="d4d60-231">pack target inputs</span></span>

| <span data-ttu-id="d4d60-232">屬性</span><span class="sxs-lookup"><span data-stu-id="d4d60-232">Property</span></span> | <span data-ttu-id="d4d60-233">描述</span><span class="sxs-lookup"><span data-stu-id="d4d60-233">Description</span></span> |
| - | - |
| <span data-ttu-id="d4d60-234">IsPackable</span><span class="sxs-lookup"><span data-stu-id="d4d60-234">IsPackable</span></span> | <span data-ttu-id="d4d60-235">布林值，指定是否可封裝專案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-235">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="d4d60-236">預設值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-236">The default value is `true`.</span></span> |
| <span data-ttu-id="d4d60-237">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="d4d60-237">SuppressDependenciesWhenPacking</span></span> | <span data-ttu-id="d4d60-238">設定為 `true` ，以從產生的 NuGet 套件抑制套件相依性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-238">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| <span data-ttu-id="d4d60-239">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d4d60-239">PackageVersion</span></span> | <span data-ttu-id="d4d60-240">指定所產生之套件的版本。</span><span class="sxs-lookup"><span data-stu-id="d4d60-240">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="d4d60-241">接受所有形式的 NuGet 版本字串。</span><span class="sxs-lookup"><span data-stu-id="d4d60-241">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="d4d60-242">預設為 `$(Version)` 的值，也就是專案中的屬性 `Version`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-242">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| <span data-ttu-id="d4d60-243">PackageId</span><span class="sxs-lookup"><span data-stu-id="d4d60-243">PackageId</span></span> | <span data-ttu-id="d4d60-244">指定所產生之套件的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4d60-244">Specifies the name for the resulting package.</span></span> <span data-ttu-id="d4d60-245">如果未指定，`pack` 作業會預設為使用 `AssemblyName` 或目錄名稱作為套件的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4d60-245">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| <span data-ttu-id="d4d60-246">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="d4d60-246">PackageDescription</span></span> | <span data-ttu-id="d4d60-247">UI 顯示中的套件詳細描述。</span><span class="sxs-lookup"><span data-stu-id="d4d60-247">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="d4d60-248">Authors</span><span class="sxs-lookup"><span data-stu-id="d4d60-248">Authors</span></span> | <span data-ttu-id="d4d60-249">以分號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些會顯示在 nuget.org 的 NuGet 元件庫中，並用來交互參照相同作者的封裝。</span><span class="sxs-lookup"><span data-stu-id="d4d60-249">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="d4d60-250">描述</span><span class="sxs-lookup"><span data-stu-id="d4d60-250">Description</span></span> | <span data-ttu-id="d4d60-251">組件的完整描述。</span><span class="sxs-lookup"><span data-stu-id="d4d60-251">A long description for the assembly.</span></span> <span data-ttu-id="d4d60-252">如果 `PackageDescription` 未指定，則此屬性也會用來做為封裝的描述。</span><span class="sxs-lookup"><span data-stu-id="d4d60-252">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="d4d60-253">著作權</span><span class="sxs-lookup"><span data-stu-id="d4d60-253">Copyright</span></span> | <span data-ttu-id="d4d60-254">套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4d60-254">Copyright details for the package.</span></span> |
| <span data-ttu-id="d4d60-255">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d4d60-255">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="d4d60-256">布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。</span><span class="sxs-lookup"><span data-stu-id="d4d60-256">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="d4d60-257">預設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-257">The default is `false`.</span></span> |
| <span data-ttu-id="d4d60-258">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="d4d60-258">DevelopmentDependency</span></span> | <span data-ttu-id="d4d60-259">布林值，指定封裝是否標記為僅限開發的相依性，這可防止封裝作為其他封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-259">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="d4d60-260">使用 `PackageReference` (NuGet 4.8 +) ，此旗標也表示編譯時期資產已從編譯中排除。</span><span class="sxs-lookup"><span data-stu-id="d4d60-260">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="d4d60-261">如需詳細資訊，請參閱 [PackageReference 的 DevelopmentDependency 支援](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-261">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| <span data-ttu-id="d4d60-262">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d4d60-262">PackageLicenseExpression</span></span> | <span data-ttu-id="d4d60-263">[SPDX 授權識別碼](https://spdx.org/licenses/)或運算式，例如 `Apache-2.0` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-263">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="d4d60-264">如需詳細資訊，請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-264">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="d4d60-265">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d4d60-265">PackageLicenseFile</span></span> | <span data-ttu-id="d4d60-266">如果您使用自訂授權或未獲指派 SPDX 識別碼的授權，則為套件內的授權檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-266">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| <span data-ttu-id="d4d60-267">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-267">PackageLicenseUrl</span></span> | <span data-ttu-id="d4d60-268">`PackageLicenseUrl` 已被取代。</span><span class="sxs-lookup"><span data-stu-id="d4d60-268">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="d4d60-269">請改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-269">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="d4d60-270">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-270">PackageProjectUrl</span></span> | |
| <span data-ttu-id="d4d60-271">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="d4d60-271">PackageIcon</span></span> | <span data-ttu-id="d4d60-272">指定封裝圖示路徑（相對於封裝的根目錄）。</span><span class="sxs-lookup"><span data-stu-id="d4d60-272">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="d4d60-273">如需詳細資訊，請參閱 [封裝圖示影像檔](#packing-an-icon-image-file)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-273">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| <span data-ttu-id="d4d60-274">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d4d60-274">PackageReleaseNotes</span></span>| <span data-ttu-id="d4d60-275">套件的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d4d60-275">Release notes for the package.</span></span> |
| <span data-ttu-id="d4d60-276">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d4d60-276">PackageTags</span></span> | <span data-ttu-id="d4d60-277">以分號分隔的標記清單，用以指定套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-277">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="d4d60-278">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="d4d60-278">PackageOutputPath</span></span> | <span data-ttu-id="d4d60-279">決定要置放所封裝之套件的輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-279">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="d4d60-280">預設為 `$(OutputPath)`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-280">Default is `$(OutputPath)`.</span></span> |
| <span data-ttu-id="d4d60-281">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d4d60-281">IncludeSymbols</span></span> | <span data-ttu-id="d4d60-282">此布林值會指出在封裝專案時，套件是否應該建立額外的符號套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-282">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="d4d60-283">符號套件的格式由 `SymbolPackageFormat` 屬性控制。</span><span class="sxs-lookup"><span data-stu-id="d4d60-283">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="d4d60-284">如需詳細資訊，請參閱 [IncludeSymbols](#includesymbols)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-284">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| <span data-ttu-id="d4d60-285">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d4d60-285">IncludeSource</span></span> | <span data-ttu-id="d4d60-286">此布林值會指出封裝處理序是否應該建立來源套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-286">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="d4d60-287">來源套件包含程式庫的原始程式碼及 PDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-287">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="d4d60-288">原始程式檔會放在所產生之套件檔案中的 `src/ProjectName` 目錄底下。</span><span class="sxs-lookup"><span data-stu-id="d4d60-288">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="d4d60-289">如需詳細資訊，請參閱 [IncludeSource](#includesource)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-289">For more information, see [IncludeSource](#includesource).</span></span> |
| <span data-ttu-id="d4d60-290">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="d4d60-290">PackageTypes</span></span>
| <span data-ttu-id="d4d60-291">IsTool</span><span class="sxs-lookup"><span data-stu-id="d4d60-291">IsTool</span></span> | <span data-ttu-id="d4d60-292">指定是否要將所有輸出檔複製到 *tools* 資料夾，而不是 *lib* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4d60-292">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="d4d60-293">如需詳細資訊，請參閱 [IsTool](#istool)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-293">For more information, see [IsTool](#istool).</span></span> |
| <span data-ttu-id="d4d60-294">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-294">RepositoryUrl</span></span> | <span data-ttu-id="d4d60-295">用來複製或取出原始程式碼的儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="d4d60-295">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="d4d60-296">範例： *https://github.com/NuGet/NuGet.Client.git* 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-296">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="d4d60-297">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d4d60-297">RepositoryType</span></span> | <span data-ttu-id="d4d60-298">存放庫類型。</span><span class="sxs-lookup"><span data-stu-id="d4d60-298">Repository type.</span></span> <span data-ttu-id="d4d60-299">範例： `git` (預設) ， `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-299">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="d4d60-300">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d4d60-300">RepositoryBranch</span></span> | <span data-ttu-id="d4d60-301">選用的存放庫分支資訊。</span><span class="sxs-lookup"><span data-stu-id="d4d60-301">Optional repository branch information.</span></span> <span data-ttu-id="d4d60-302">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="d4d60-302">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="d4d60-303">範例： *master* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-303">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="d4d60-304">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d4d60-304">RepositoryCommit</span></span> | <span data-ttu-id="d4d60-305">選用的儲存機制認可或變更集，以指出建立封裝的來源。</span><span class="sxs-lookup"><span data-stu-id="d4d60-305">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="d4d60-306">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="d4d60-306">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="d4d60-307">範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-307">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="d4d60-308">SymbolPackageFormat</span><span class="sxs-lookup"><span data-stu-id="d4d60-308">SymbolPackageFormat</span></span> | <span data-ttu-id="d4d60-309">指定符號套件的格式。</span><span class="sxs-lookup"><span data-stu-id="d4d60-309">Specifies the format of the symbols package.</span></span> <span data-ttu-id="d4d60-310">如果是 "nupkg"，則會使用包含 Pdb、Dll 和其他輸出檔的 *nupkg* 副檔名來建立舊版符號套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-310">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="d4d60-311">如果是 ".snupkg"，則會建立包含便攜 Pdb 的 .snupkg 符號套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-311">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="d4d60-312">預設值為 "nupkg"。</span><span class="sxs-lookup"><span data-stu-id="d4d60-312">The default is "symbols.nupkg".</span></span> |
| <span data-ttu-id="d4d60-313">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="d4d60-313">NoPackageAnalysis</span></span> | <span data-ttu-id="d4d60-314">指定 `pack` 在建立封裝之後，不應該執行套件分析。</span><span class="sxs-lookup"><span data-stu-id="d4d60-314">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="d4d60-315">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="d4d60-315">MinClientVersion</span></span> | <span data-ttu-id="d4d60-316">指定可安裝此套件的最低 NuGet 用戶端版本，此作業是由 nuget.exe 和 Visual Studio 套件管理員強制執行。</span><span class="sxs-lookup"><span data-stu-id="d4d60-316">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| <span data-ttu-id="d4d60-317">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d4d60-317">IncludeBuildOutput</span></span> | <span data-ttu-id="d4d60-318">這個布林值會指定是否應將組建輸出元件封裝至 *nupkg* 檔中。</span><span class="sxs-lookup"><span data-stu-id="d4d60-318">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| <span data-ttu-id="d4d60-319">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="d4d60-319">IncludeContentInPack</span></span> | <span data-ttu-id="d4d60-320">這個布林值會指定是否 `Content` 要自動在產生的封裝中包含類型為的任何專案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-320">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="d4d60-321">預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-321">The default is `true`.</span></span> |
| <span data-ttu-id="d4d60-322">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="d4d60-322">BuildOutputTargetFolder</span></span> | <span data-ttu-id="d4d60-323">指定要放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4d60-323">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="d4d60-324">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="d4d60-324">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="d4d60-325">如需詳細資訊，請參閱 [輸出元件](#output-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-325">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| <span data-ttu-id="d4d60-326">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="d4d60-326">ContentTargetFolders</span></span> | <span data-ttu-id="d4d60-327">如果未指定所有內容檔案，則指定其預設位置 `PackagePath` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-327">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="d4d60-328">預設值為 "content;contentFiles"。</span><span class="sxs-lookup"><span data-stu-id="d4d60-328">The default value is "content;contentFiles".</span></span> <span data-ttu-id="d4d60-329">如需詳細資訊，請參閱 [Including content in a package](#including-content-in-a-package) (在套件中包含內容)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-329">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| <span data-ttu-id="d4d60-330">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="d4d60-330">NuspecFile</span></span> | <span data-ttu-id="d4d60-331">正用於封裝之 *.nuspec* 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-331">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="d4d60-332">如果指定，則會 **專門** 用於封裝資訊，而不會使用專案中的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="d4d60-332">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="d4d60-333">如需詳細資訊，請參閱 [使用 Nuspec 封裝](#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-333">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="d4d60-334">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="d4d60-334">NuspecBasePath</span></span> | <span data-ttu-id="d4d60-335">*.nuspec* 檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-335">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="d4d60-336">如需詳細資訊，請參閱 [使用 Nuspec 封裝](#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-336">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="d4d60-337">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="d4d60-337">NuspecProperties</span></span> | <span data-ttu-id="d4d60-338">以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="d4d60-338">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="d4d60-339">如需詳細資訊，請參閱 [使用 Nuspec 封裝](#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-339">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="d4d60-340">封裝案例</span><span class="sxs-lookup"><span data-stu-id="d4d60-340">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="d4d60-341">隱藏相關性</span><span class="sxs-lookup"><span data-stu-id="d4d60-341">Suppress dependencies</span></span>

<span data-ttu-id="d4d60-342">若要從產生的 NuGet 套件抑制套件相依性，請將設定 `SuppressDependenciesWhenPacking` 為，以 `true` 允許略過產生的 nupkg 檔案中的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-342">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="d4d60-343">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d4d60-343">PackageIconUrl</span></span>

<span data-ttu-id="d4d60-344">`PackageIconUrl` 已被取代為屬性的使用方式 [`PackageIcon`](#packageicon) 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-344">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="d4d60-345">從 NuGet 5.3 開始，Visual Studio 2019 16.3 版， `pack` 如果套件中繼資料僅指定，則會引發 [NU5048](./errors-and-warnings/nu5048.md) 警告 `PackageIconUrl` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-345">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="d4d60-346">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="d4d60-346">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="d4d60-347">若要維持與尚未支援的用戶端和來源的回溯相容性 `PackageIcon` ，請同時指定 `PackageIcon` 和 `PackageIconUrl` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-347">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="d4d60-348">Visual Studio 支援 `PackageIcon` 來自以資料夾為基礎之來源的封裝。</span><span class="sxs-lookup"><span data-stu-id="d4d60-348">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="d4d60-349">封裝圖示影像檔案</span><span class="sxs-lookup"><span data-stu-id="d4d60-349">Packing an icon image file</span></span>

<span data-ttu-id="d4d60-350">封裝圖示影像檔案時，請使用 `PackageIcon` 屬性來指定圖示檔路徑（相對於封裝的根目錄）。</span><span class="sxs-lookup"><span data-stu-id="d4d60-350">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="d4d60-351">此外，請確定檔案包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="d4d60-351">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="d4d60-352">影像檔案大小限制為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="d4d60-352">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="d4d60-353">支援的檔案格式包括 JPEG 和 PNG。</span><span class="sxs-lookup"><span data-stu-id="d4d60-353">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="d4d60-354">我們建議使用128x128 的影像解析度。</span><span class="sxs-lookup"><span data-stu-id="d4d60-354">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="d4d60-355">例如：</span><span class="sxs-lookup"><span data-stu-id="d4d60-355">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="d4d60-356">[封裝圖示範例](https://github.com/NuGet/Samples/tree/master/PackageIconExample)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-356">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="d4d60-357">針對 nuspec 對等專案，請查看 [圖示的 nuspec 參考](nuspec.md#icon)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-357">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="d4d60-358">輸出組件</span><span class="sxs-lookup"><span data-stu-id="d4d60-358">Output assemblies</span></span>

<span data-ttu-id="d4d60-359">`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-359">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="d4d60-360">所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。</span><span class="sxs-lookup"><span data-stu-id="d4d60-360">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="d4d60-361">在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：</span><span class="sxs-lookup"><span data-stu-id="d4d60-361">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="d4d60-362">`IncludeBuildOutput`：布林值，決定是否應該在套件中包含組建輸出組件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-362">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="d4d60-363">`BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4d60-363">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="d4d60-364">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="d4d60-364">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="d4d60-365">套件參考</span><span class="sxs-lookup"><span data-stu-id="d4d60-365">Package references</span></span>

<span data-ttu-id="d4d60-366">請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-366">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="d4d60-367">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="d4d60-367">Project to project references</span></span>

<span data-ttu-id="d4d60-368">預設會將專案對專案參考視為 NuGet 套件參考，例如：</span><span class="sxs-lookup"><span data-stu-id="d4d60-368">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="d4d60-369">您也可以將下列中繼資料新增至您的專案參考：</span><span class="sxs-lookup"><span data-stu-id="d4d60-369">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="d4d60-370">在套件內包含內容</span><span class="sxs-lookup"><span data-stu-id="d4d60-370">Including content in a package</span></span>

<span data-ttu-id="d4d60-371">若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。</span><span class="sxs-lookup"><span data-stu-id="d4d60-371">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="d4d60-372">除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：</span><span class="sxs-lookup"><span data-stu-id="d4d60-372">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="d4d60-373">除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="d4d60-373">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="d4d60-374">如果您想要將所有內容都只複製至特定根資料夾 (而不是 `content` 和 `contentFiles`)，則可以使用 MSBuild 屬性 `ContentTargetFolders`，其預設為 "content;contentFiles"，但可以設定為任何其他資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="d4d60-374">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="d4d60-375">請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。</span><span class="sxs-lookup"><span data-stu-id="d4d60-375">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="d4d60-376">`PackagePath` 可以是以分號分隔的一組目標路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-376">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="d4d60-377">指定空的套件路徑會將檔案新增至套件的根目錄。</span><span class="sxs-lookup"><span data-stu-id="d4d60-377">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="d4d60-378">例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：</span><span class="sxs-lookup"><span data-stu-id="d4d60-378">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="d4d60-379">另有 MSBuild 屬性 `$(IncludeContentInPack)` 預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-379">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="d4d60-380">如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。</span><span class="sxs-lookup"><span data-stu-id="d4d60-380">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="d4d60-381">您可在上述任何項目上設定的其他封裝特定中繼資料包含 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，其在輸出 nuspec 的 ```contentFiles``` 項目上設定 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="d4d60-381">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="d4d60-382">除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d4d60-382">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="d4d60-383">針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-383">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="d4d60-384">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d4d60-384">IncludeSymbols</span></span>

<span data-ttu-id="d4d60-385">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-385">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="d4d60-386">請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-386">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="d4d60-387">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d4d60-387">IncludeSource</span></span>

<span data-ttu-id="d4d60-388">這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-388">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="d4d60-389">所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="d4d60-389">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="d4d60-390">這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-390">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="d4d60-391">若類型為 Compile 的檔案位於專案資料夾之外，就只會將其新增至 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-391">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="d4d60-392">封裝授權運算式或授權檔案</span><span class="sxs-lookup"><span data-stu-id="d4d60-392">Packing a license expression or a license file</span></span>

<span data-ttu-id="d4d60-393">使用授權運算式時，請使用 `PackageLicenseExpression` 屬性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-393">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="d4d60-394">如需範例，請參閱 [授權運算式範例](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-394">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="d4d60-395">若要深入瞭解 NuGet.org 所接受的授權運算式和授權，請參閱 [授權中繼資料](nuspec.md#license)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-395">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="d4d60-396">封裝授權檔案時，請使用 `PackageLicenseFile` 屬性來指定相對於封裝根目錄的封裝路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-396">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="d4d60-397">此外，請確定檔案包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="d4d60-397">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="d4d60-398">例如：</span><span class="sxs-lookup"><span data-stu-id="d4d60-398">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="d4d60-399">如需範例，請參閱 [授權檔案範例](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-399">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="d4d60-400">`PackageLicenseExpression`一次只能指定、和中的一個 `PackageLicenseFile` `PackageLicenseUrl` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-400">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="d4d60-401">封裝沒有副檔名的檔案</span><span class="sxs-lookup"><span data-stu-id="d4d60-401">Packing a file without an extension</span></span>

<span data-ttu-id="d4d60-402">在某些情況下，例如封裝授權檔案時，您可能會想要包含沒有副檔名的檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-402">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="d4d60-403">基於歷史原因，NuGet & MSBuild 會將沒有副檔名的路徑視為目錄。</span><span class="sxs-lookup"><span data-stu-id="d4d60-403">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="d4d60-404">[沒有副檔名範例的](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/)檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-404">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="d4d60-405">IsTool</span><span class="sxs-lookup"><span data-stu-id="d4d60-405">IsTool</span></span>

<span data-ttu-id="d4d60-406">使用 `MSBuild -t:pack -p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4d60-406">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="d4d60-407">請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。</span><span class="sxs-lookup"><span data-stu-id="d4d60-407">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="d4d60-408">使用 .nuspec 封裝</span><span class="sxs-lookup"><span data-stu-id="d4d60-408">Packing using a .nuspec</span></span>

<span data-ttu-id="d4d60-409">雖然建議您將通常是在檔案中的 [所有屬性包含](../reference/msbuild-targets.md#pack-target) 在 `.nuspec` 專案檔中，但您可以選擇使用檔案 `.nuspec` 來封裝專案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-409">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="d4d60-410">若為使用的非 SDK 樣式專案 `PackageReference` ，您必須匯入， `NuGet.Build.Tasks.Pack.targets` 才能執行封裝工作。</span><span class="sxs-lookup"><span data-stu-id="d4d60-410">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="d4d60-411">您仍然需要還原專案，才能封裝 nuspec 檔。</span><span class="sxs-lookup"><span data-stu-id="d4d60-411">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="d4d60-412"> (SDK 樣式專案預設會包含套件目標。 ) </span><span class="sxs-lookup"><span data-stu-id="d4d60-412">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="d4d60-413">專案檔的目標 framework 是不相關的，而且不會在封裝 nuspec 時使用。</span><span class="sxs-lookup"><span data-stu-id="d4d60-413">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="d4d60-414">下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：</span><span class="sxs-lookup"><span data-stu-id="d4d60-414">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="d4d60-415">`NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-415">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="d4d60-416">`NuspecProperties`：以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="d4d60-416">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="d4d60-417">基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`-p:NuspecProperties="key1=value1;key2=value2"`。</span><span class="sxs-lookup"><span data-stu-id="d4d60-417">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="d4d60-418">`NuspecBasePath`：`.nuspec` 檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-418">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="d4d60-419">如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="d4d60-419">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d4d60-420">如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="d4d60-420">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d4d60-421">請注意，使用 dotnet.exe 或 msbuild 封裝 nuspec 時，預設也會導致建立專案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-421">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="d4d60-422">將 ```--no-build``` 屬性傳遞給 dotnet.exe （這相當於專案檔中的設定 ```<NoBuild>true</NoBuild> ``` ，以及專案檔中的設定），即可避免此情況 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-422">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="d4d60-423">要封裝 nuspec 檔案的 *.csproj* 檔案範例如下：</span><span class="sxs-lookup"><span data-stu-id="d4d60-423">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="d4d60-424">用來建立自訂套件的 Advanced 擴充點</span><span class="sxs-lookup"><span data-stu-id="d4d60-424">Advanced extension points to create customized package</span></span>

<span data-ttu-id="d4d60-425">`pack`目標提供在內部、目標 framework 特定組建中執行的兩個擴充點。</span><span class="sxs-lookup"><span data-stu-id="d4d60-425">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="d4d60-426">擴充點支援在套件中包含目標 framework 特定內容和元件：</span><span class="sxs-lookup"><span data-stu-id="d4d60-426">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="d4d60-427">`TargetsForTfmSpecificBuildOutput` 目標：用於資料夾內的檔案 `lib` 或使用指定的資料夾 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-427">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="d4d60-428">`TargetsForTfmSpecificContentInPackage` 目標：用於以外的檔案 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-428">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="d4d60-429">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d4d60-429">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="d4d60-430">撰寫自訂目標，並將其指定為屬性的值 `$(TargetsForTfmSpecificBuildOutput)` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-430">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="d4d60-431">若為任何需要在預設情況下進入 `BuildOutputTargetFolder` (lib 的檔案) ，目標應該將這些檔案寫入 ItemGroup `BuildOutputInPackage` ，並設定下列兩個中繼資料值：</span><span class="sxs-lookup"><span data-stu-id="d4d60-431">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="d4d60-432">`FinalOutputPath`：檔案的絕對路徑;如果未提供，則會使用身分識別來評估來源路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-432">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="d4d60-433">`TargetPath`：當檔案需要移至內的子資料夾時， (選擇性的) 設定 `lib\<TargetFramework>` ，例如在其個別文化特性資料夾下的附屬元件。</span><span class="sxs-lookup"><span data-stu-id="d4d60-433">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="d4d60-434">預設為檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4d60-434">Defaults to the name of the file.</span></span>

<span data-ttu-id="d4d60-435">範例：</span><span class="sxs-lookup"><span data-stu-id="d4d60-435">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="d4d60-436">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="d4d60-436">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="d4d60-437">撰寫自訂目標，並將其指定為屬性的值 `$(TargetsForTfmSpecificContentInPackage)` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-437">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="d4d60-438">對於要包含在封裝中的任何檔案，目標應該將這些檔案寫入至 ItemGroup `TfmSpecificPackageFile` ，並設定下列選擇性中繼資料：</span><span class="sxs-lookup"><span data-stu-id="d4d60-438">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="d4d60-439">`PackagePath`：檔案應在封裝中輸出的路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-439">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="d4d60-440">如果有多個檔案加入至相同的封裝路徑，NuGet 會發出警告。</span><span class="sxs-lookup"><span data-stu-id="d4d60-440">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="d4d60-441">`BuildAction`：要指派給檔案的組建動作，只有在封裝路徑位於資料夾中時才需要 `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-441">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="d4d60-442">預設值為 "None"。</span><span class="sxs-lookup"><span data-stu-id="d4d60-442">Defaults to "None".</span></span>

<span data-ttu-id="d4d60-443">例如：</span><span class="sxs-lookup"><span data-stu-id="d4d60-443">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="d4d60-444">還原目標</span><span class="sxs-lookup"><span data-stu-id="d4d60-444">restore target</span></span>

<span data-ttu-id="d4d60-445">`MSBuild -t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d4d60-445">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="d4d60-446">讀取所有專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="d4d60-446">Read all project to project references</span></span>
1. <span data-ttu-id="d4d60-447">讀取專案屬性來尋找中繼資料夾和目標架構</span><span class="sxs-lookup"><span data-stu-id="d4d60-447">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="d4d60-448">將 MSBuild 資料傳遞給 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="d4d60-448">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="d4d60-449">執行還原</span><span class="sxs-lookup"><span data-stu-id="d4d60-449">Run restore</span></span>
1. <span data-ttu-id="d4d60-450">下載套件</span><span class="sxs-lookup"><span data-stu-id="d4d60-450">Download packages</span></span>
1. <span data-ttu-id="d4d60-451">撰寫資產檔案、目標和屬性</span><span class="sxs-lookup"><span data-stu-id="d4d60-451">Write assets file, targets, and props</span></span>

<span data-ttu-id="d4d60-452">`restore`目標適用于使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-452">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="d4d60-453">`MSBuild 16.5+` 也提供格式的 [選擇支援](#restoring-packagereference-and-packagesconfig-with-msbuild) `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-453">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="d4d60-454">`restore`目標[不應](#restoring-and-building-with-one-msbuild-command)與目標一起執行 `build` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-454">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="d4d60-455">還原屬性</span><span class="sxs-lookup"><span data-stu-id="d4d60-455">Restore properties</span></span>

<span data-ttu-id="d4d60-456">其他還原設定可能來自專案檔中的 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-456">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="d4d60-457">您也可以從命令列，使用 `-p:` 參數設定值 (請參閱下列＜範例＞)。</span><span class="sxs-lookup"><span data-stu-id="d4d60-457">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="d4d60-458">屬性</span><span class="sxs-lookup"><span data-stu-id="d4d60-458">Property</span></span> | <span data-ttu-id="d4d60-459">描述</span><span class="sxs-lookup"><span data-stu-id="d4d60-459">Description</span></span> |
|--------|--------|
| <span data-ttu-id="d4d60-460">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="d4d60-460">RestoreSources</span></span> | <span data-ttu-id="d4d60-461">以分號分隔的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="d4d60-461">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="d4d60-462">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="d4d60-462">RestorePackagesPath</span></span> | <span data-ttu-id="d4d60-463">使用者套件資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-463">User packages folder path.</span></span> |
| <span data-ttu-id="d4d60-464">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="d4d60-464">RestoreDisableParallel</span></span> | <span data-ttu-id="d4d60-465">限制逐一進行下載。</span><span class="sxs-lookup"><span data-stu-id="d4d60-465">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="d4d60-466">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="d4d60-466">RestoreConfigFile</span></span> | <span data-ttu-id="d4d60-467">要套用之 `Nuget.Config` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-467">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="d4d60-468">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="d4d60-468">RestoreNoCache</span></span> | <span data-ttu-id="d4d60-469">若為 true，則避免使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="d4d60-469">If true, avoids using cached packages.</span></span> <span data-ttu-id="d4d60-470">請參閱 [管理全域封裝和](../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4d60-470">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="d4d60-471">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="d4d60-471">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="d4d60-472">如果為 true，請忽略失敗或遺漏的套件來源。</span><span class="sxs-lookup"><span data-stu-id="d4d60-472">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="d4d60-473">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="d4d60-473">RestoreFallbackFolders</span></span> | <span data-ttu-id="d4d60-474">回溯資料夾，使用的方式與使用者套件資料夾相同。</span><span class="sxs-lookup"><span data-stu-id="d4d60-474">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="d4d60-475">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="d4d60-475">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="d4d60-476">還原期間要使用的其他來源。</span><span class="sxs-lookup"><span data-stu-id="d4d60-476">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="d4d60-477">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="d4d60-477">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="d4d60-478">還原期間要使用的其他回溯資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4d60-478">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="d4d60-479">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="d4d60-479">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="d4d60-480">排除指定的回溯資料夾 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="d4d60-480">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="d4d60-481">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="d4d60-481">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="d4d60-482">`NuGet.Build.Tasks.dll` 的路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-482">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="d4d60-483">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="d4d60-483">RestoreGraphProjectInput</span></span> | <span data-ttu-id="d4d60-484">要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="d4d60-484">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="d4d60-485">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="d4d60-485">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="d4d60-486">透過 MSBuild 收集項目時，它會決定是否使用優化進行收集 `SkipNonexistentTargets` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-486">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="d4d60-487">若未設定，則預設為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-487">When not set, defaults to `true`.</span></span> <span data-ttu-id="d4d60-488">當無法匯入專案的目標時，結果會是快速失敗的行為。</span><span class="sxs-lookup"><span data-stu-id="d4d60-488">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="d4d60-489">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="d4d60-489">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="d4d60-490">輸出檔案夾，預設為 `BaseIntermediateOutputPath` 和 `obj` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4d60-490">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="d4d60-491">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="d4d60-491">RestoreForce</span></span> | <span data-ttu-id="d4d60-492">在以 PackageReference 為基礎的專案中，即使上次還原成功，仍會強制解析所有相依性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-492">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="d4d60-493">指定此旗標與刪除檔案類似 `project.assets.json` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-493">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="d4d60-494">這不會略過 HTTP 快取。</span><span class="sxs-lookup"><span data-stu-id="d4d60-494">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="d4d60-495">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="d4d60-495">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="d4d60-496">選擇使用鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="d4d60-496">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="d4d60-497">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="d4d60-497">RestoreLockedMode</span></span> | <span data-ttu-id="d4d60-498">以鎖定模式執行還原。</span><span class="sxs-lookup"><span data-stu-id="d4d60-498">Run restore in locked mode.</span></span> <span data-ttu-id="d4d60-499">這表示還原將不會重新評估相依性。</span><span class="sxs-lookup"><span data-stu-id="d4d60-499">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="d4d60-500">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="d4d60-500">NuGetLockFilePath</span></span> | <span data-ttu-id="d4d60-501">鎖定檔案的自訂位置。</span><span class="sxs-lookup"><span data-stu-id="d4d60-501">A custom location for the lock file.</span></span> <span data-ttu-id="d4d60-502">預設位置是專案的旁邊，而且名為 `packages.lock.json` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-502">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="d4d60-503">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="d4d60-503">RestoreForceEvaluate</span></span> | <span data-ttu-id="d4d60-504">強制還原以重新計算相依性，並更新鎖定檔案而不發出任何警告。</span><span class="sxs-lookup"><span data-stu-id="d4d60-504">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="d4d60-505">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="d4d60-505">RestorePackagesConfig</span></span> | <span data-ttu-id="d4d60-506">可使用 packages.config 還原專案的加入宣告參數。僅支援 `MSBuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-506">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="d4d60-507">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="d4d60-507">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="d4d60-508">加入宣告參數以使用靜態圖形 MSBuild 評估，而不是標準評估。</span><span class="sxs-lookup"><span data-stu-id="d4d60-508">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="d4d60-509">靜態圖表評估是一項實驗性功能，對於大型存放庫和解決方案來說更快。</span><span class="sxs-lookup"><span data-stu-id="d4d60-509">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="d4d60-510">範例</span><span class="sxs-lookup"><span data-stu-id="d4d60-510">Examples</span></span>

<span data-ttu-id="d4d60-511">命令列：</span><span class="sxs-lookup"><span data-stu-id="d4d60-511">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="d4d60-512">專案檔：</span><span class="sxs-lookup"><span data-stu-id="d4d60-512">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="d4d60-513">Restore outputs</span><span class="sxs-lookup"><span data-stu-id="d4d60-513">Restore outputs</span></span>

<span data-ttu-id="d4d60-514">還原會在組建 `obj` 資料夾中建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="d4d60-514">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="d4d60-515">檔案</span><span class="sxs-lookup"><span data-stu-id="d4d60-515">File</span></span> | <span data-ttu-id="d4d60-516">描述</span><span class="sxs-lookup"><span data-stu-id="d4d60-516">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="d4d60-517">包含所有封裝參考的相依性圖形。</span><span class="sxs-lookup"><span data-stu-id="d4d60-517">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="d4d60-518">套件中所含 MSBuild 屬性的參考</span><span class="sxs-lookup"><span data-stu-id="d4d60-518">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="d4d60-519">套件中所含 MSBuild 目標的參考</span><span class="sxs-lookup"><span data-stu-id="d4d60-519">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="d4d60-520">使用一個 MSBuild 命令來還原和建立</span><span class="sxs-lookup"><span data-stu-id="d4d60-520">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="d4d60-521">由於 NuGet 可以還原可關閉 MSBuild 目標和 .props 的套件，因此會使用不同的全域屬性來執行還原和建立評估。</span><span class="sxs-lookup"><span data-stu-id="d4d60-521">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="d4d60-522">這表示下列將會有無法預測且通常不正確的行為。</span><span class="sxs-lookup"><span data-stu-id="d4d60-522">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="d4d60-523">建議的方法是：</span><span class="sxs-lookup"><span data-stu-id="d4d60-523">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="d4d60-524">相同的邏輯也適用于類似的其他目標 `build` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-524">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="d4d60-525">使用 MSBuild 還原 PackageReference 和 packages.config</span><span class="sxs-lookup"><span data-stu-id="d4d60-525">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="d4d60-526">使用 MSBuild 16.5 + 時，也支援的 packages.config `msbuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-526">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="d4d60-527">`packages.config` restore 僅適用于 `MSBuild 16.5+` 和 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="d4d60-527">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="d4d60-528">使用 MSBuild 靜態圖形評估還原</span><span class="sxs-lookup"><span data-stu-id="d4d60-528">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="d4d60-529">使用 MSBuild 16.6 版 +，NuGet 已新增實驗性功能，可從命令列使用靜態圖形評估，以大幅改善大型存放庫的還原時間。</span><span class="sxs-lookup"><span data-stu-id="d4d60-529">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="d4d60-530">或者，您可以藉由在 .Props 中設定屬性來啟用它。</span><span class="sxs-lookup"><span data-stu-id="d4d60-530">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="d4d60-531">自 Visual Studio 2019. x 和 NuGet 5.x 起，這項功能會被視為實驗性和加入宣告。</span><span class="sxs-lookup"><span data-stu-id="d4d60-531">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="d4d60-532">依照 [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) 的詳細資訊，以瞭解何時預設會啟用這項功能。</span><span class="sxs-lookup"><span data-stu-id="d4d60-532">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="d4d60-533">靜態圖形還原會變更還原的 msbuild 部分、專案讀取和評估，但不會變更還原演算法！</span><span class="sxs-lookup"><span data-stu-id="d4d60-533">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="d4d60-534">所有 NuGet 工具的還原演算法都相同 ( # A0、MSBuild.exe、dotnet.exe 和 Visual Studio) 。</span><span class="sxs-lookup"><span data-stu-id="d4d60-534">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="d4d60-535">在極少數的情況下，靜態圖形還原的行為可能會與目前的還原不同，而某些宣告的 PackageReferences 或 ProjectReferences 可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="d4d60-535">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="d4d60-536">為了簡化您的想法，請在遷移至靜態圖形還原時，考慮執行：</span><span class="sxs-lookup"><span data-stu-id="d4d60-536">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="d4d60-537">NuGet *不* 應報告任何變更。</span><span class="sxs-lookup"><span data-stu-id="d4d60-537">NuGet should *not* report any changes.</span></span> <span data-ttu-id="d4d60-538">如果您看不到差異，請在 [NuGet/Home](https://github.com/nuget/home/issues/new)提出問題。</span><span class="sxs-lookup"><span data-stu-id="d4d60-538">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="d4d60-539">取代還原圖形中的一個程式庫</span><span class="sxs-lookup"><span data-stu-id="d4d60-539">Replacing one library from a restore graph</span></span>

<span data-ttu-id="d4d60-540">如果還原內含錯誤的組件，您可以排除該套件預設選項，並將其取代為您自己的選項。</span><span class="sxs-lookup"><span data-stu-id="d4d60-540">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="d4d60-541">首先，會有最上層 `PackageReference`，但排除所有資產：</span><span class="sxs-lookup"><span data-stu-id="d4d60-541">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="d4d60-542">接下來，新增您自己對 DLL 之適當本機複本的參考：</span><span class="sxs-lookup"><span data-stu-id="d4d60-542">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
