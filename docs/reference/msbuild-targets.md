---
title: NuGet 套件和還原為 MSBuild 目標
description: NuGet pack 和 restore 可以直接做為 MSBuild 4.0 + 的目標使用 NuGet 。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067306"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="ed45e-103">NuGet 套件和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="ed45e-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="ed45e-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="ed45e-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="ed45e-105">使用 [PackageReference](../consume-packages/package-references-in-project-files.md) 格式， NuGet 4.0 + 可以直接將所有資訊清單中繼資料儲存在專案檔中，而不是使用個別的檔案 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="ed45e-106">使用 MSBuild 15.1 + NuGet 時，也是 MSBuild 具有和目標的第一級公民， `pack` `restore` 如下所述。</span><span class="sxs-lookup"><span data-stu-id="ed45e-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="ed45e-107">這些目標可讓您與 NuGet 任何其他工作或目標一樣使用 MSBuild 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="ed45e-108">如需使用建立 NuGet 封裝的指示 MSBuild ，請參閱[ NuGet 使用 MSBuild 建立封裝](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="ed45e-109"> (3.x NuGet 及更早版本，您可以改為使用 [套件](../reference/cli-reference/cli-ref-pack.md) 並透過 CLI [還原](../reference/cli-reference/cli-ref-restore.md) 命令 NuGet 。 ) </span><span class="sxs-lookup"><span data-stu-id="ed45e-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="ed45e-110">目標組建順序</span><span class="sxs-lookup"><span data-stu-id="ed45e-110">Target build order</span></span>

<span data-ttu-id="ed45e-111">因為 `pack` 和 `restore` 是  MSBuild 目標，所以您可以存取它們來增強您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="ed45e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="ed45e-112">例如，假設您想要在封裝之後將套件複製到網路共用。</span><span class="sxs-lookup"><span data-stu-id="ed45e-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="ed45e-113">做法是在專案檔中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="ed45e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="ed45e-114">同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，並使用 NuGet 工作中的屬性 MSBuild 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="ed45e-115">`$(OutputPath)` 是相對的，且預期您是從專案根目錄執行命令。</span><span class="sxs-lookup"><span data-stu-id="ed45e-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="ed45e-116">封裝目標</span><span class="sxs-lookup"><span data-stu-id="ed45e-116">pack target</span></span>

<span data-ttu-id="ed45e-117">針對使用格式的 .NET 專案 `PackageReference` ，使用會 `msbuild -t:pack` 從專案檔繪製輸入，以用於建立 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="ed45e-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="ed45e-118">下表說明 MSBuild 可以加入至第一個節點內之專案檔的屬性 `<PropertyGroup>` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="ed45e-119">以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。</span><span class="sxs-lookup"><span data-stu-id="ed45e-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="ed45e-120">為了方便起見，資料表會依照檔案中的對等屬性進行[ `.nuspec` 組織。](../reference/nuspec.md)</span><span class="sxs-lookup"><span data-stu-id="ed45e-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ed45e-121">`Owners``Summary`不支援的和屬性 `.nuspec` MSBuild 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="ed45e-122">屬性/ nuspec 值</span><span class="sxs-lookup"><span data-stu-id="ed45e-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="ed45e-123">MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="ed45e-123">MSBuild Property</span></span> | <span data-ttu-id="ed45e-124">預設</span><span class="sxs-lookup"><span data-stu-id="ed45e-124">Default</span></span> | <span data-ttu-id="ed45e-125">備註</span><span class="sxs-lookup"><span data-stu-id="ed45e-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="ed45e-126">來自 MSBuild 的 `$(AssemblyName)`</span><span class="sxs-lookup"><span data-stu-id="ed45e-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="ed45e-127">版本</span><span class="sxs-lookup"><span data-stu-id="ed45e-127">Version</span></span> | <span data-ttu-id="ed45e-128">這是 semver 相容的，例如 `1.0.0` ， `1.0.0-beta` 或 `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="ed45e-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="ed45e-129">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-129">empty</span></span> | <span data-ttu-id="ed45e-130">設定 `PackageVersion` 覆寫 `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="ed45e-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="ed45e-131">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-131">empty</span></span> | <span data-ttu-id="ed45e-132">`$(VersionSuffix)` from MSBuild 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="ed45e-133">設定 `PackageVersion` 覆寫 `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="ed45e-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="ed45e-134">目前使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="ed45e-134">Username of the current user</span></span> | <span data-ttu-id="ed45e-135">以分號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些會顯示在 nuget.org 的資源 NuGet 庫中，並用來交互參照相同作者的封裝。</span><span class="sxs-lookup"><span data-stu-id="ed45e-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="ed45e-136">N/A</span><span class="sxs-lookup"><span data-stu-id="ed45e-136">N/A</span></span> | <span data-ttu-id="ed45e-137">不存在於 nuspec</span><span class="sxs-lookup"><span data-stu-id="ed45e-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="ed45e-138">`PackageId`</span><span class="sxs-lookup"><span data-stu-id="ed45e-138">The `PackageId`</span></span> | <span data-ttu-id="ed45e-139">套件的易記標題，通常會用於 UI 顯示，以及 nuget.org 和 Visual Studio 套件管理員中。</span><span class="sxs-lookup"><span data-stu-id="ed45e-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="ed45e-140">"Package Description"</span><span class="sxs-lookup"><span data-stu-id="ed45e-140">"Package Description"</span></span> | <span data-ttu-id="ed45e-141">組件的完整描述。</span><span class="sxs-lookup"><span data-stu-id="ed45e-141">A long description for the assembly.</span></span> <span data-ttu-id="ed45e-142">如果 `PackageDescription` 未指定，則此屬性也會用來做為封裝的描述。</span><span class="sxs-lookup"><span data-stu-id="ed45e-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="ed45e-143">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-143">empty</span></span> | <span data-ttu-id="ed45e-144">套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ed45e-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="ed45e-145">布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。</span><span class="sxs-lookup"><span data-stu-id="ed45e-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="ed45e-146">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-146">empty</span></span> | <span data-ttu-id="ed45e-147">對應至 `<license type="expression">`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="ed45e-148">請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="ed45e-149">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-149">empty</span></span> | <span data-ttu-id="ed45e-150">如果您使用自訂授權或未獲指派 SPDX 識別碼的授權，則為套件內的授權檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="ed45e-151">您必須明確地封裝參考的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="ed45e-152">對應至 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="ed45e-153">請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="ed45e-154">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-154">empty</span></span> | <span data-ttu-id="ed45e-155">`PackageLicenseUrl` 已被取代。</span><span class="sxs-lookup"><span data-stu-id="ed45e-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="ed45e-156">請改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="ed45e-157">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="ed45e-158">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-158">empty</span></span> | <span data-ttu-id="ed45e-159">封裝中用來做為封裝圖示的影像路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="ed45e-160">您必須明確地封裝參考的圖示影像檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="ed45e-161">如需詳細資訊，請參閱[封裝圖示影像檔](#packing-an-icon-image-file)案和[ `icon` 中繼資料](./nuspec.md#icon)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="ed45e-162">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-162">empty</span></span> | <span data-ttu-id="ed45e-163">`PackageIconUrl` 已被取代，改為使用 `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="ed45e-164">但是，為了獲得最佳的早期體驗，除了之外，您還應該指定 `PackageIconUrl` `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="ed45e-165">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-165">empty</span></span> | <span data-ttu-id="ed45e-166">您必須明確地封裝參考的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="ed45e-167">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-167">empty</span></span> | <span data-ttu-id="ed45e-168">以分號分隔的標記清單，用以指定套件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="ed45e-169">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-169">empty</span></span> | <span data-ttu-id="ed45e-170">套件的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="ed45e-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="ed45e-171">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-171">empty</span></span> | <span data-ttu-id="ed45e-172">用來複製或取出原始程式碼的儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="ed45e-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="ed45e-173">範例： *https://github.com/ NuGet / NuGet 。用戶端. git*。</span><span class="sxs-lookup"><span data-stu-id="ed45e-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="ed45e-174">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-174">empty</span></span> | <span data-ttu-id="ed45e-175">存放庫類型。</span><span class="sxs-lookup"><span data-stu-id="ed45e-175">Repository type.</span></span> <span data-ttu-id="ed45e-176">範例： `git` (預設) ， `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="ed45e-177">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-177">empty</span></span> | <span data-ttu-id="ed45e-178">選用的存放庫分支資訊。</span><span class="sxs-lookup"><span data-stu-id="ed45e-178">Optional repository branch information.</span></span> <span data-ttu-id="ed45e-179">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="ed45e-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="ed45e-180">範例： *master* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="ed45e-181">empty</span><span class="sxs-lookup"><span data-stu-id="ed45e-181">empty</span></span> | <span data-ttu-id="ed45e-182">選用的儲存機制認可或變更集，以指出建立封裝的來源。</span><span class="sxs-lookup"><span data-stu-id="ed45e-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="ed45e-183">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="ed45e-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="ed45e-184">範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | <span data-ttu-id="ed45e-185">指出封裝的預定用途。</span><span class="sxs-lookup"><span data-stu-id="ed45e-185">Indicates the package's intended use.</span></span> <span data-ttu-id="ed45e-186">封裝類型使用與封裝識別碼相同的格式，並以分隔 `;` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-186">Package types use the same format as package IDs and are delimited by `;`.</span></span> <span data-ttu-id="ed45e-187">封裝類型可透過附加 `,` 和字串來建立版本 [`Version`](/dotnet/api/system.version) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-187">Package types may be versioned by appending a `,` and a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="ed45e-188">請參閱 [設定 NuGet 套件類型](../create-packages/set-package-type.md) (NuGet 3.5.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-188">See [Set a NuGet package type](../create-packages/set-package-type.md) (NuGet 3.5.0+).</span></span> |
| `Summary` | <span data-ttu-id="ed45e-189">不支援</span><span class="sxs-lookup"><span data-stu-id="ed45e-189">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="ed45e-190">封裝目標輸入</span><span class="sxs-lookup"><span data-stu-id="ed45e-190">pack target inputs</span></span>

| <span data-ttu-id="ed45e-191">屬性</span><span class="sxs-lookup"><span data-stu-id="ed45e-191">Property</span></span> | <span data-ttu-id="ed45e-192">描述</span><span class="sxs-lookup"><span data-stu-id="ed45e-192">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="ed45e-193">布林值，指定是否可封裝專案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-193">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="ed45e-194">預設值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-194">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="ed45e-195">設定為， `true` 以從產生的封裝中隱藏封裝相依性 NuGet 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-195">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="ed45e-196">指定所產生之套件的版本。</span><span class="sxs-lookup"><span data-stu-id="ed45e-196">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="ed45e-197">接受所有形式的 NuGet 版本字串。</span><span class="sxs-lookup"><span data-stu-id="ed45e-197">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="ed45e-198">預設為 `$(Version)` 的值，也就是專案中的屬性 `Version`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-198">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="ed45e-199">指定所產生之套件的名稱。</span><span class="sxs-lookup"><span data-stu-id="ed45e-199">Specifies the name for the resulting package.</span></span> <span data-ttu-id="ed45e-200">如果未指定，`pack` 作業會預設為使用 `AssemblyName` 或目錄名稱作為套件的名稱。</span><span class="sxs-lookup"><span data-stu-id="ed45e-200">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="ed45e-201">UI 顯示中的套件詳細描述。</span><span class="sxs-lookup"><span data-stu-id="ed45e-201">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="ed45e-202">以分號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些會顯示在 nuget.org 的資源 NuGet 庫中，並用來交互參照相同作者的封裝。</span><span class="sxs-lookup"><span data-stu-id="ed45e-202">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="ed45e-203">組件的完整描述。</span><span class="sxs-lookup"><span data-stu-id="ed45e-203">A long description for the assembly.</span></span> <span data-ttu-id="ed45e-204">如果 `PackageDescription` 未指定，則此屬性也會用來做為封裝的描述。</span><span class="sxs-lookup"><span data-stu-id="ed45e-204">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="ed45e-205">套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ed45e-205">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="ed45e-206">布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。</span><span class="sxs-lookup"><span data-stu-id="ed45e-206">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="ed45e-207">預設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-207">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="ed45e-208">布林值，指定封裝是否標記為僅限開發的相依性，這可防止封裝作為其他封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="ed45e-208">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="ed45e-209">在 `PackageReference` (NuGet 4.8 +) 中，此旗標也表示編譯時期資產已從編譯中排除。</span><span class="sxs-lookup"><span data-stu-id="ed45e-209">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="ed45e-210">如需詳細資訊，請參閱 [PackageReference 的 DevelopmentDependency 支援](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-210">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="ed45e-211">[SPDX 授權識別碼](https://spdx.org/licenses/)或運算式，例如 `Apache-2.0` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-211">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="ed45e-212">如需詳細資訊，請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-212">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="ed45e-213">如果您使用自訂授權或未獲指派 SPDX 識別碼的授權，則為套件內的授權檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-213">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="ed45e-214">`PackageLicenseUrl` 已被取代。</span><span class="sxs-lookup"><span data-stu-id="ed45e-214">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="ed45e-215">請改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-215">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="ed45e-216">指定封裝圖示路徑（相對於封裝的根目錄）。</span><span class="sxs-lookup"><span data-stu-id="ed45e-216">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="ed45e-217">如需詳細資訊，請參閱 [封裝圖示影像檔](#packing-an-icon-image-file)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-217">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="ed45e-218">套件的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="ed45e-218">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="ed45e-219">封裝的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-219">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="ed45e-220">以分號分隔的標記清單，用以指定套件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-220">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="ed45e-221">決定要置放所封裝之套件的輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-221">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="ed45e-222">預設為 `$(OutputPath)`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-222">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="ed45e-223">此布林值會指出在封裝專案時，套件是否應該建立額外的符號套件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-223">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="ed45e-224">符號套件的格式由 `SymbolPackageFormat` 屬性控制。</span><span class="sxs-lookup"><span data-stu-id="ed45e-224">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="ed45e-225">如需詳細資訊，請參閱 [IncludeSymbols](#includesymbols)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-225">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="ed45e-226">此布林值會指出封裝處理序是否應該建立來源套件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-226">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="ed45e-227">來源套件包含程式庫的原始程式碼及 PDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-227">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="ed45e-228">原始程式檔會放在所產生之套件檔案中的 `src/ProjectName` 目錄底下。</span><span class="sxs-lookup"><span data-stu-id="ed45e-228">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="ed45e-229">如需詳細資訊，請參閱 [IncludeSource](#includesource)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-229">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="ed45e-230">指定是否要將所有輸出檔複製到 *tools* 資料夾，而不是 *lib* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed45e-230">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="ed45e-231">如需詳細資訊，請參閱 [IsTool](#istool)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-231">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="ed45e-232">用來複製或取出原始程式碼的儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="ed45e-232">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="ed45e-233">範例： *https://github.com/ NuGet / NuGet 。用戶端. git*。</span><span class="sxs-lookup"><span data-stu-id="ed45e-233">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="ed45e-234">存放庫類型。</span><span class="sxs-lookup"><span data-stu-id="ed45e-234">Repository type.</span></span> <span data-ttu-id="ed45e-235">範例： `git` (預設) ， `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-235">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="ed45e-236">選用的存放庫分支資訊。</span><span class="sxs-lookup"><span data-stu-id="ed45e-236">Optional repository branch information.</span></span> <span data-ttu-id="ed45e-237">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="ed45e-237">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="ed45e-238">範例： *master* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-238">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="ed45e-239">選用的儲存機制認可或變更集，以指出建立封裝的來源。</span><span class="sxs-lookup"><span data-stu-id="ed45e-239">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="ed45e-240">`RepositoryUrl` 也必須指定此屬性才能包含。</span><span class="sxs-lookup"><span data-stu-id="ed45e-240">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="ed45e-241">範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-241">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="ed45e-242">指定符號套件的格式。</span><span class="sxs-lookup"><span data-stu-id="ed45e-242">Specifies the format of the symbols package.</span></span> <span data-ttu-id="ed45e-243">如果是 "nupkg"，則會使用包含 Pdb、Dll 和其他輸出檔的 *nupkg* 副檔名來建立舊版符號套件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-243">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="ed45e-244">如果是 ".snupkg"，則會建立包含便攜 Pdb 的 .snupkg 符號套件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-244">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="ed45e-245">預設值為 "nupkg"。</span><span class="sxs-lookup"><span data-stu-id="ed45e-245">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="ed45e-246">指定 `pack` 在建立封裝之後，不應該執行套件分析。</span><span class="sxs-lookup"><span data-stu-id="ed45e-246">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="ed45e-247">指定 NuGet 可安裝此封裝的最小用戶端版本，由 nuget.exe 和 Visual Studio 封裝管理員強制執行。</span><span class="sxs-lookup"><span data-stu-id="ed45e-247">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="ed45e-248">這個布林值會指定是否應將組建輸出元件封裝至 *nupkg* 檔中。</span><span class="sxs-lookup"><span data-stu-id="ed45e-248">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="ed45e-249">這個布林值會指定是否 `Content` 要自動在產生的封裝中包含類型為的任何專案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-249">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="ed45e-250">預設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-250">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="ed45e-251">指定要放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed45e-251">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="ed45e-252">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ed45e-252">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="ed45e-253">如需詳細資訊，請參閱 [輸出元件](#output-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-253">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="ed45e-254">如果未指定所有內容檔案，則指定其預設位置 `PackagePath` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-254">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="ed45e-255">預設值為 "content;contentFiles"。</span><span class="sxs-lookup"><span data-stu-id="ed45e-255">The default value is "content;contentFiles".</span></span> <span data-ttu-id="ed45e-256">如需詳細資訊，請參閱 [Including content in a package](#including-content-in-a-package) (在套件中包含內容)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-256">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="ed45e-257">用於封裝之檔案的相對或絕對路徑 *.nuspec* 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-257">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="ed45e-258">如果指定，則會 **專門** 用於封裝資訊，而不會使用專案中的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="ed45e-258">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="ed45e-259">如需詳細資訊，請參閱[使用 .nuspec 封裝](#packing-using-a-nuspec-file)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="ed45e-260">檔案的基底路徑 *.nuspec* 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-260">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="ed45e-261">如需詳細資訊，請參閱[使用 .nuspec 封裝](#packing-using-a-nuspec-file)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-261">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="ed45e-262">以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="ed45e-262">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="ed45e-263">如需詳細資訊，請參閱[使用 .nuspec 封裝](#packing-using-a-nuspec-file)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-263">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="ed45e-264">封裝案例</span><span class="sxs-lookup"><span data-stu-id="ed45e-264">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="ed45e-265">隱藏相關性</span><span class="sxs-lookup"><span data-stu-id="ed45e-265">Suppressing dependencies</span></span>

<span data-ttu-id="ed45e-266">若要從產生的封裝隱藏封裝相依性 NuGet ，請將設定 `SuppressDependenciesWhenPacking` 為，以 `true` 允許略過產生的 nupkg 檔中的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="ed45e-266">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="ed45e-267">`PackageIconUrl` 已被取代為屬性的使用方式 [`PackageIcon`](#packageicon) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-267">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="ed45e-268">從5.3 開始， NuGet Visual Studio 2019 16.3 版， `pack` 如果封裝中繼資料僅指定，則會引發 [NU5048](./errors-and-warnings/nu5048.md) 警告 `PackageIconUrl` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-268">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="ed45e-269">若要維持與尚未支援的用戶端和來源的回溯相容性 `PackageIcon` ，請同時指定 `PackageIcon` 和 `PackageIconUrl` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-269">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="ed45e-270">Visual Studio 支援 `PackageIcon` 來自以資料夾為基礎之來源的封裝。</span><span class="sxs-lookup"><span data-stu-id="ed45e-270">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="ed45e-271">封裝圖示影像檔案</span><span class="sxs-lookup"><span data-stu-id="ed45e-271">Packing an icon image file</span></span>

<span data-ttu-id="ed45e-272">封裝圖示影像檔案時，請使用 `PackageIcon` 屬性來指定圖示檔路徑（相對於封裝的根目錄）。</span><span class="sxs-lookup"><span data-stu-id="ed45e-272">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="ed45e-273">此外，請確定檔案包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="ed45e-273">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="ed45e-274">影像檔案大小限制為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="ed45e-274">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="ed45e-275">支援的檔案格式包括 JPEG 和 PNG。</span><span class="sxs-lookup"><span data-stu-id="ed45e-275">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="ed45e-276">我們建議使用128x128 的影像解析度。</span><span class="sxs-lookup"><span data-stu-id="ed45e-276">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="ed45e-277">例如：</span><span class="sxs-lookup"><span data-stu-id="ed45e-277">For example:</span></span>

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

<span data-ttu-id="ed45e-278">[封裝圖示範例](https://github.com/NuGet/Samples/tree/main/PackageIconExample)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-278">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="ed45e-279">針對 nuspec 相等的，請查看圖示的[ nuspec 參考](nuspec.md#icon)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-279">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="ed45e-280">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="ed45e-280">PackageReadmeFile</span></span>

<span data-ttu-id="ed45e-281">*支援 **NuGet 5.10.0 preview 2**  /  **.net SDK 5.0.300** 和更新版本*</span><span class="sxs-lookup"><span data-stu-id="ed45e-281">*Supported with **NuGet 5.10.0 preview 2** / **.NET SDK 5.0.300** and above*</span></span>

<span data-ttu-id="ed45e-282">封裝讀我檔案時，您必須使用 `PackageReadmeFile` 屬性來指定封裝路徑（相對於封裝的根目錄）。</span><span class="sxs-lookup"><span data-stu-id="ed45e-282">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ed45e-283">此外，您必須確定檔案包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="ed45e-283">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="ed45e-284">支援的檔案格式只包含 Markdown (*md*) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-284">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="ed45e-285">例如：</span><span class="sxs-lookup"><span data-stu-id="ed45e-285">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="ed45e-286">如 nuspec 需對等專案，請參閱[ nuspec 讀我檔案的參考](nuspec.md#readme)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-286">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="ed45e-287">輸出組件</span><span class="sxs-lookup"><span data-stu-id="ed45e-287">Output assemblies</span></span>

<span data-ttu-id="ed45e-288">`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-288">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="ed45e-289">複製的輸出檔案取決於 MSBuild 從目標提供的內容 `BuiltOutputProjectGroup` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-289">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="ed45e-290">您 MSBuild  可以在專案檔或命令列中使用兩個屬性來控制輸出元件的位置：</span><span class="sxs-lookup"><span data-stu-id="ed45e-290">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="ed45e-291">`IncludeBuildOutput`：布林值，決定是否應該在套件中包含組建輸出組件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-291">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="ed45e-292">`BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed45e-292">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="ed45e-293">輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ed45e-293">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="ed45e-294">套件參考</span><span class="sxs-lookup"><span data-stu-id="ed45e-294">Package references</span></span>

<span data-ttu-id="ed45e-295">請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-295">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="ed45e-296">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="ed45e-296">Project to project references</span></span>

<span data-ttu-id="ed45e-297">專案對專案的參考預設會被視為 NuGet 封裝參考。</span><span class="sxs-lookup"><span data-stu-id="ed45e-297">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="ed45e-298">例如：</span><span class="sxs-lookup"><span data-stu-id="ed45e-298">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="ed45e-299">您也可以將下列中繼資料新增至您的專案參考：</span><span class="sxs-lookup"><span data-stu-id="ed45e-299">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="ed45e-300">在套件內包含內容</span><span class="sxs-lookup"><span data-stu-id="ed45e-300">Including content in a package</span></span>

<span data-ttu-id="ed45e-301">若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。</span><span class="sxs-lookup"><span data-stu-id="ed45e-301">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="ed45e-302">除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：</span><span class="sxs-lookup"><span data-stu-id="ed45e-302">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="ed45e-303">除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="ed45e-303">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="ed45e-304">如果您想要將所有內容複寫到僅 (s 的特定根資料夾)  (而非 `content` 和 `contentFiles` 兩者) ，您可以使用 MSBuild 屬性 `ContentTargetFolders` （預設為 "content; contentFiles"），但可以設定為任何其他資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="ed45e-304">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="ed45e-305">請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。</span><span class="sxs-lookup"><span data-stu-id="ed45e-305">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="ed45e-306">`PackagePath` 可以是以分號分隔的一組目標路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-306">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="ed45e-307">指定空的套件路徑會將檔案新增至套件的根目錄。</span><span class="sxs-lookup"><span data-stu-id="ed45e-307">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="ed45e-308">例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：</span><span class="sxs-lookup"><span data-stu-id="ed45e-308">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="ed45e-309">另外還有一個 MSBuild 屬性 `$(IncludeContentInPack)` ，預設為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-309">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="ed45e-310">如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。</span><span class="sxs-lookup"><span data-stu-id="ed45e-310">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="ed45e-311">您可以在上述任何專案上設定的其他封裝特定中繼資料，包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` 輸出中專案的集合和值 nuspec 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-311">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="ed45e-312">除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ed45e-312">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="ed45e-313">針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-313">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="ed45e-314">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="ed45e-314">IncludeSymbols</span></span>

<span data-ttu-id="ed45e-315">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-315">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="ed45e-316">請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-316">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="ed45e-317">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="ed45e-317">IncludeSource</span></span>

<span data-ttu-id="ed45e-318">這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-318">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="ed45e-319">所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="ed45e-319">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="ed45e-320">這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-320">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="ed45e-321">若類型為 Compile 的檔案位於專案資料夾之外，就只會將其新增至 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="ed45e-321">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="ed45e-322">封裝授權運算式或授權檔案</span><span class="sxs-lookup"><span data-stu-id="ed45e-322">Packing a license expression or a license file</span></span>

<span data-ttu-id="ed45e-323">使用授權運算式時，請使用 `PackageLicenseExpression` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ed45e-323">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="ed45e-324">如需範例，請參閱 [授權運算式範例](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-324">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="ed45e-325">若要深入瞭解由 org 接受的授權運算式和授權 NuGet ，請參閱 [授權中繼資料](nuspec.md#license)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-325">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="ed45e-326">封裝授權檔案時，請使用 `PackageLicenseFile` 屬性來指定相對於封裝根目錄的封裝路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-326">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ed45e-327">此外，請確定檔案包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="ed45e-327">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="ed45e-328">例如：</span><span class="sxs-lookup"><span data-stu-id="ed45e-328">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="ed45e-329">如需範例，請參閱 [授權檔案範例](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-329">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="ed45e-330">`PackageLicenseExpression`一次只能指定、和中的一個 `PackageLicenseFile` `PackageLicenseUrl` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-330">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="ed45e-331">封裝沒有副檔名的檔案</span><span class="sxs-lookup"><span data-stu-id="ed45e-331">Packing a file without an extension</span></span>

<span data-ttu-id="ed45e-332">在某些情況下，例如封裝授權檔案時，您可能會想要包含沒有副檔名的檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-332">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="ed45e-333">基於歷史原因，請 NuGet  &  MSBuild 將沒有副檔名的路徑視為目錄。</span><span class="sxs-lookup"><span data-stu-id="ed45e-333">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="ed45e-334">[沒有副檔名範例的](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-334">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="ed45e-335">IsTool</span><span class="sxs-lookup"><span data-stu-id="ed45e-335">IsTool</span></span>

<span data-ttu-id="ed45e-336">使用 `MSBuild -t:pack -p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed45e-336">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="ed45e-337">請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。</span><span class="sxs-lookup"><span data-stu-id="ed45e-337">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="ed45e-338">使用 `.nuspec` 檔案進行封裝</span><span class="sxs-lookup"><span data-stu-id="ed45e-338">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="ed45e-339">雖然建議您將通常是在檔案中的 [所有屬性包含](../reference/msbuild-targets.md#pack-target) 在 `.nuspec` 專案檔中，但您可以選擇使用檔案 `.nuspec` 來封裝專案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-339">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="ed45e-340">若為使用的非 SDK 樣式專案 `PackageReference` ，您必須匯入， `NuGet.Build.Tasks.Pack.targets` 才能執行封裝工作。</span><span class="sxs-lookup"><span data-stu-id="ed45e-340">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="ed45e-341">您仍然需要還原專案，才能封裝檔案 nuspec 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-341">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="ed45e-342"> (SDK 樣式專案預設會包含套件目標。 ) </span><span class="sxs-lookup"><span data-stu-id="ed45e-342">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="ed45e-343">專案檔的目標 framework 是不相關的，而且不會在封裝時使用 nuspec 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-343">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="ed45e-344">下列三個 MSBuild 屬性與使用的封裝有關 `.nuspec` ：</span><span class="sxs-lookup"><span data-stu-id="ed45e-344">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="ed45e-345">`NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-345">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="ed45e-346">`NuspecProperties`：以分號分隔的索引鍵=值組清單。</span><span class="sxs-lookup"><span data-stu-id="ed45e-346">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="ed45e-347">由於 MSBuild 命令列剖析的運作方式，必須指定多個屬性，如下所示： `-p:NuspecProperties="key1=value1;key2=value2"` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-347">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="ed45e-348">`NuspecBasePath`：`.nuspec` 檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-348">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="ed45e-349">如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="ed45e-349">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ed45e-350">如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：</span><span class="sxs-lookup"><span data-stu-id="ed45e-350">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ed45e-351">請注意， nuspec 使用 dotnet.exe 或 msbuild 封裝，預設也會導致建立專案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-351">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="ed45e-352">將 ```--no-build``` 屬性傳遞給 dotnet.exe （這相當於專案檔中的設定 ```<NoBuild>true</NoBuild> ``` ，以及專案檔中的設定），即可避免此情況 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-352">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="ed45e-353">封裝檔案的 *.csproj* 檔案範例 nuspec 如下：</span><span class="sxs-lookup"><span data-stu-id="ed45e-353">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="ed45e-354">用來建立自訂套件的 Advanced 擴充點</span><span class="sxs-lookup"><span data-stu-id="ed45e-354">Advanced extension points to create customized package</span></span>

<span data-ttu-id="ed45e-355">`pack`目標提供在內部、目標 framework 特定組建中執行的兩個擴充點。</span><span class="sxs-lookup"><span data-stu-id="ed45e-355">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="ed45e-356">擴充點支援在套件中包含目標 framework 特定內容和元件：</span><span class="sxs-lookup"><span data-stu-id="ed45e-356">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="ed45e-357">`TargetsForTfmSpecificBuildOutput` 目標：用於資料夾內的檔案 `lib` 或使用指定的資料夾 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-357">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="ed45e-358">`TargetsForTfmSpecificContentInPackage` 目標：用於以外的檔案 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-358">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="ed45e-359">撰寫自訂目標，並將其指定為屬性的值 `$(TargetsForTfmSpecificBuildOutput)` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-359">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="ed45e-360">若為任何需要在預設情況下進入 `BuildOutputTargetFolder` (lib 的檔案) ，目標應該將這些檔案寫入 ItemGroup `BuildOutputInPackage` ，並設定下列兩個中繼資料值：</span><span class="sxs-lookup"><span data-stu-id="ed45e-360">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="ed45e-361">`FinalOutputPath`：檔案的絕對路徑;如果未提供，則會使用身分識別來評估來源路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-361">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="ed45e-362">`TargetPath`：當檔案需要移至內的子資料夾時， (選擇性的) 設定 `lib\<TargetFramework>` ，例如在其個別文化特性資料夾下的附屬元件。</span><span class="sxs-lookup"><span data-stu-id="ed45e-362">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="ed45e-363">預設為檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="ed45e-363">Defaults to the name of the file.</span></span>

<span data-ttu-id="ed45e-364">範例：</span><span class="sxs-lookup"><span data-stu-id="ed45e-364">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="ed45e-365">撰寫自訂目標，並將其指定為屬性的值 `$(TargetsForTfmSpecificContentInPackage)` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-365">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="ed45e-366">對於要包含在封裝中的任何檔案，目標應該將這些檔案寫入至 ItemGroup `TfmSpecificPackageFile` ，並設定下列選擇性中繼資料：</span><span class="sxs-lookup"><span data-stu-id="ed45e-366">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="ed45e-367">`PackagePath`：檔案應在封裝中輸出的路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-367">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="ed45e-368">NuGet 如果有多個檔案加入至相同的封裝路徑，則會發出警告。</span><span class="sxs-lookup"><span data-stu-id="ed45e-368">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="ed45e-369">`BuildAction`：要指派給檔案的組建動作，只有在封裝路徑位於資料夾中時才需要 `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-369">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="ed45e-370">預設值為 "None"。</span><span class="sxs-lookup"><span data-stu-id="ed45e-370">Defaults to "None".</span></span>

<span data-ttu-id="ed45e-371">例如：</span><span class="sxs-lookup"><span data-stu-id="ed45e-371">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="ed45e-372">還原目標</span><span class="sxs-lookup"><span data-stu-id="ed45e-372">restore target</span></span>

<span data-ttu-id="ed45e-373">`MSBuild -t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ed45e-373">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="ed45e-374">讀取所有專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="ed45e-374">Read all project to project references</span></span>
1. <span data-ttu-id="ed45e-375">讀取專案屬性來尋找中繼資料夾和目標架構</span><span class="sxs-lookup"><span data-stu-id="ed45e-375">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="ed45e-376">MSBuild將資料傳遞給 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="ed45e-376">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="ed45e-377">執行還原</span><span class="sxs-lookup"><span data-stu-id="ed45e-377">Run restore</span></span>
1. <span data-ttu-id="ed45e-378">下載套件</span><span class="sxs-lookup"><span data-stu-id="ed45e-378">Download packages</span></span>
1. <span data-ttu-id="ed45e-379">撰寫資產檔案、目標和屬性</span><span class="sxs-lookup"><span data-stu-id="ed45e-379">Write assets file, targets, and props</span></span>

<span data-ttu-id="ed45e-380">`restore`目標適用于使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-380">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="ed45e-381">`MSBuild 16.5+` 也提供格式的 [選擇支援](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-381">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="ed45e-382">`restore`目標[不應](#restoring-and-building-with-one-msbuild-command)與目標一起執行 `build` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-382">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="ed45e-383">還原屬性</span><span class="sxs-lookup"><span data-stu-id="ed45e-383">Restore properties</span></span>

<span data-ttu-id="ed45e-384">其他還原設定可能來自 MSBuild 專案檔中的屬性。</span><span class="sxs-lookup"><span data-stu-id="ed45e-384">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="ed45e-385">您也可以從命令列，使用 `-p:` 參數設定值 (請參閱下列＜範例＞)。</span><span class="sxs-lookup"><span data-stu-id="ed45e-385">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="ed45e-386">屬性</span><span class="sxs-lookup"><span data-stu-id="ed45e-386">Property</span></span> | <span data-ttu-id="ed45e-387">描述</span><span class="sxs-lookup"><span data-stu-id="ed45e-387">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="ed45e-388">以分號分隔的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="ed45e-388">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="ed45e-389">使用者套件資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-389">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="ed45e-390">限制逐一進行下載。</span><span class="sxs-lookup"><span data-stu-id="ed45e-390">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="ed45e-391">要套用之 `Nuget.Config` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-391">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="ed45e-392">若為 true，則避免使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="ed45e-392">If true, avoids using cached packages.</span></span> <span data-ttu-id="ed45e-393">請參閱 [管理全域封裝和](../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed45e-393">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="ed45e-394">如果為 true，請忽略失敗或遺漏的套件來源。</span><span class="sxs-lookup"><span data-stu-id="ed45e-394">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="ed45e-395">回溯資料夾，使用的方式與使用者套件資料夾相同。</span><span class="sxs-lookup"><span data-stu-id="ed45e-395">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="ed45e-396">還原期間要使用的其他來源。</span><span class="sxs-lookup"><span data-stu-id="ed45e-396">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="ed45e-397">還原期間要使用的其他回溯資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed45e-397">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="ed45e-398">排除指定的回溯資料夾 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="ed45e-398">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="ed45e-399">`NuGet.Build.Tasks.dll` 的路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-399">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="ed45e-400">要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="ed45e-400">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="ed45e-401">透過它收集項目時，會 MSBuild 決定是否使用優化來收集項目 `SkipNonexistentTargets` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-401">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="ed45e-402">若未設定，則預設為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-402">When not set, defaults to `true`.</span></span> <span data-ttu-id="ed45e-403">當無法匯入專案的目標時，結果會是快速失敗的行為。</span><span class="sxs-lookup"><span data-stu-id="ed45e-403">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="ed45e-404">輸出檔案夾，預設為 `BaseIntermediateOutputPath` 和 `obj` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ed45e-404">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="ed45e-405">在以 PackageReference 為基礎的專案中，即使上次還原成功，仍會強制解析所有相依性。</span><span class="sxs-lookup"><span data-stu-id="ed45e-405">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="ed45e-406">指定此旗標與刪除檔案類似 `project.assets.json` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-406">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="ed45e-407">這不會略過 HTTP 快取。</span><span class="sxs-lookup"><span data-stu-id="ed45e-407">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="ed45e-408">選擇使用鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="ed45e-408">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="ed45e-409">以鎖定模式執行還原。</span><span class="sxs-lookup"><span data-stu-id="ed45e-409">Run restore in locked mode.</span></span> <span data-ttu-id="ed45e-410">這表示還原將不會重新評估相依性。</span><span class="sxs-lookup"><span data-stu-id="ed45e-410">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="ed45e-411">鎖定檔案的自訂位置。</span><span class="sxs-lookup"><span data-stu-id="ed45e-411">A custom location for the lock file.</span></span> <span data-ttu-id="ed45e-412">預設位置是專案的旁邊，而且名為 `packages.lock.json` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-412">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="ed45e-413">強制還原以重新計算相依性，並更新鎖定檔案而不發出任何警告。</span><span class="sxs-lookup"><span data-stu-id="ed45e-413">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="ed45e-414">可使用 packages.config 還原專案的加入宣告參數。僅支援 `MSBuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-414">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="ed45e-415">加入宣告參數以使用靜態圖形評估， MSBuild 而不是標準評估。</span><span class="sxs-lookup"><span data-stu-id="ed45e-415">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="ed45e-416">靜態圖表評估是一項實驗性功能，對於大型存放庫和解決方案來說更快。</span><span class="sxs-lookup"><span data-stu-id="ed45e-416">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="ed45e-417">範例</span><span class="sxs-lookup"><span data-stu-id="ed45e-417">Examples</span></span>

<span data-ttu-id="ed45e-418">命令列：</span><span class="sxs-lookup"><span data-stu-id="ed45e-418">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="ed45e-419">專案檔：</span><span class="sxs-lookup"><span data-stu-id="ed45e-419">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="ed45e-420">Restore outputs</span><span class="sxs-lookup"><span data-stu-id="ed45e-420">Restore outputs</span></span>

<span data-ttu-id="ed45e-421">還原會在組建 `obj` 資料夾中建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="ed45e-421">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="ed45e-422">檔案</span><span class="sxs-lookup"><span data-stu-id="ed45e-422">File</span></span> | <span data-ttu-id="ed45e-423">描述</span><span class="sxs-lookup"><span data-stu-id="ed45e-423">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="ed45e-424">包含所有封裝參考的相依性圖形。</span><span class="sxs-lookup"><span data-stu-id="ed45e-424">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="ed45e-425">MSBuild封裝所包含之 .props 的參考</span><span class="sxs-lookup"><span data-stu-id="ed45e-425">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="ed45e-426">MSBuild封裝中包含目標的參考</span><span class="sxs-lookup"><span data-stu-id="ed45e-426">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="ed45e-427">使用一個命令來還原和建立 MSBuild</span><span class="sxs-lookup"><span data-stu-id="ed45e-427">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="ed45e-428">由於 NuGet 可以還原可關閉 MSBuild 目標和 .props 的套件，因此會使用不同的全域屬性來執行還原和建立評估。</span><span class="sxs-lookup"><span data-stu-id="ed45e-428">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="ed45e-429">這表示下列將會有無法預測且通常不正確的行為。</span><span class="sxs-lookup"><span data-stu-id="ed45e-429">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="ed45e-430">建議的方法是：</span><span class="sxs-lookup"><span data-stu-id="ed45e-430">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="ed45e-431">相同的邏輯也適用于類似的其他目標 `build` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-431">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="ed45e-432">還原 PackageReference 和 packages.config 專案 MSBuild</span><span class="sxs-lookup"><span data-stu-id="ed45e-432">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="ed45e-433">使用 MSBuild 16.5 + 時，也支援的 packages.config `msbuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-433">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="ed45e-434">`packages.config` restore 僅適用于 `MSBuild 16.5+` 和 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="ed45e-434">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="ed45e-435">使用 MSBuild 靜態圖形評估還原</span><span class="sxs-lookup"><span data-stu-id="ed45e-435">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="ed45e-436">使用 MSBuild 16.6 版 +， NuGet 已新增實驗性功能，可從命令列使用靜態圖形評估，以大幅改善大型存放庫的還原時間。</span><span class="sxs-lookup"><span data-stu-id="ed45e-436">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="ed45e-437">或者，您可以藉由在 .Props 中設定屬性來啟用它。</span><span class="sxs-lookup"><span data-stu-id="ed45e-437">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="ed45e-438">自2019年 Visual Studio 2019 和5.x 起 NuGet ，這項功能會被視為實驗性和加入宣告。</span><span class="sxs-lookup"><span data-stu-id="ed45e-438">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="ed45e-439">依照[ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803)的詳細資訊，以瞭解何時預設會啟用這項功能。</span><span class="sxs-lookup"><span data-stu-id="ed45e-439">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="ed45e-440">靜態圖形還原會變更還原的 msbuild 部分、專案讀取和評估，但不會變更還原演算法！</span><span class="sxs-lookup"><span data-stu-id="ed45e-440">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="ed45e-441">還原演算法在所有工具上都相同， NuGet (NuGet .exe、 MSBuild .exe、dotnet.exe 和 Visual Studio) 。</span><span class="sxs-lookup"><span data-stu-id="ed45e-441">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="ed45e-442">在極少數的情況下，靜態圖形還原的行為可能會與目前的還原不同，而某些宣告的 PackageReferences 或 ProjectReferences 可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="ed45e-442">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="ed45e-443">為了簡化您的想法，請在遷移至靜態圖形還原時，考慮執行：</span><span class="sxs-lookup"><span data-stu-id="ed45e-443">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="ed45e-444">NuGet*不* 應報告任何變更。</span><span class="sxs-lookup"><span data-stu-id="ed45e-444">NuGet should *not* report any changes.</span></span> <span data-ttu-id="ed45e-445">如果您看不到差異，請在[ NuGet /Home](https://github.com/nuget/home/issues/new)提出問題。</span><span class="sxs-lookup"><span data-stu-id="ed45e-445">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="ed45e-446">取代還原圖形中的一個程式庫</span><span class="sxs-lookup"><span data-stu-id="ed45e-446">Replacing one library from a restore graph</span></span>

<span data-ttu-id="ed45e-447">如果還原內含錯誤的組件，您可以排除該套件預設選項，並將其取代為您自己的選項。</span><span class="sxs-lookup"><span data-stu-id="ed45e-447">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="ed45e-448">首先，會有最上層 `PackageReference`，但排除所有資產：</span><span class="sxs-lookup"><span data-stu-id="ed45e-448">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="ed45e-449">接下來，新增您自己對 DLL 之適當本機複本的參考：</span><span class="sxs-lookup"><span data-stu-id="ed45e-449">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
