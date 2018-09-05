---
title: NuGet 套件版本參考
description: 需指定版本號碼和範圍而定的 NuGet 套件，並安裝相依性的方式在其他套件的確切詳細資料。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549769"
---
# <a name="package-versioning"></a><span data-ttu-id="79336-103">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="79336-103">Package versioning</span></span>

<span data-ttu-id="79336-104">特定封裝一律被指使用其封裝識別碼和確切的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="79336-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="79336-105">例如， [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org 上有數個數十個特定套件可供使用，範圍從版本*4.1.10311*版本*6.1.3* （最新的穩定發行） 和各種不同的發行前版本*6.2.0-beta1*。</span><span class="sxs-lookup"><span data-stu-id="79336-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="79336-106">在建立封裝時，您可以指派包含發行前版本的選擇性文字尾碼的特定版本號碼。</span><span class="sxs-lookup"><span data-stu-id="79336-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="79336-107">當使用套件，相反地，您可以指定確切的版本號碼或可接受的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="79336-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="79336-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="79336-108">In this topic:</span></span>

- <span data-ttu-id="79336-109">[版本的基本概念](#version-basics)包括發行前版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="79336-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="79336-110">版本範圍和萬用字元</span><span class="sxs-lookup"><span data-stu-id="79336-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="79336-111">正規化的版本號碼</span><span class="sxs-lookup"><span data-stu-id="79336-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="79336-112">版本的基本概念</span><span class="sxs-lookup"><span data-stu-id="79336-112">Version basics</span></span>

<span data-ttu-id="79336-113">特定版本號碼的格式*Major.Minor.Patch [-後置詞]*，其中的元件具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="79336-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="79336-114">*主要*： 重大變更</span><span class="sxs-lookup"><span data-stu-id="79336-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="79336-115">*次要*： 新功能，但具有回溯相容性</span><span class="sxs-lookup"><span data-stu-id="79336-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="79336-116">*修補程式*： 只有具備回溯相容性 bug 修正</span><span class="sxs-lookup"><span data-stu-id="79336-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="79336-117">*-後置詞*（選擇性）： 連字號後面接著用來表示發行前版本字串 (下列[語意版本控制或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="79336-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="79336-118">**範例：**</span><span class="sxs-lookup"><span data-stu-id="79336-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="79336-119">nuget.org 會拒絕任何缺少的確切版本號碼的封裝上傳。</span><span class="sxs-lookup"><span data-stu-id="79336-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="79336-120">必須指定版本`.nuspec`或用來建立封裝的專案檔。</span><span class="sxs-lookup"><span data-stu-id="79336-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="79336-121">發行前版本</span><span class="sxs-lookup"><span data-stu-id="79336-121">Pre-release versions</span></span>

<span data-ttu-id="79336-122">就技術上而言，套件建立者可以使用任何字串做為尾碼來代表發行前版本，NuGet 任何這類版本視為發行前版本，並讓其他的解譯方式。</span><span class="sxs-lookup"><span data-stu-id="79336-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="79336-123">也就是說，NuGet 會顯示完整的版本字串中任何的 UI 與此有關，給取用者離開後置詞的意義的任何解譯。</span><span class="sxs-lookup"><span data-stu-id="79336-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="79336-124">話雖如此，封裝開發人員一般會遵循可辨識的命名慣例：</span><span class="sxs-lookup"><span data-stu-id="79336-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="79336-125">`-alpha`: Alpha 版本，通常用來工作的進度和測試。</span><span class="sxs-lookup"><span data-stu-id="79336-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="79336-126">`-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的 Bug。</span><span class="sxs-lookup"><span data-stu-id="79336-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="79336-127">`-rc`：候選版，除非出現重大的 Bug，不然通常是準最終版本 (穩定版)。</span><span class="sxs-lookup"><span data-stu-id="79336-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="79336-128">NuGet 4.3.0 + 支援[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，其支援發行前版本編號使用點標記法，如同*1.0.1-build.23*。</span><span class="sxs-lookup"><span data-stu-id="79336-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="79336-129">4.3.0 之前的 NuGet 版本不支援點標記法。</span><span class="sxs-lookup"><span data-stu-id="79336-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="79336-130">您可以使用的格式*1.0.1-build23*。</span><span class="sxs-lookup"><span data-stu-id="79336-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="79336-131">當解析套件參考和多個封裝版本只有不同後置詞，NuGet 首先，選擇沒有尾碼的版本，則適用於發行前版本以反向字母順序的優先順序。</span><span class="sxs-lookup"><span data-stu-id="79336-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="79336-132">例如，下列版本會選擇正確的順序顯示：</span><span class="sxs-lookup"><span data-stu-id="79336-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="79336-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="79336-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="79336-134">NuGet 4.3.0 + 和 Visual Studio 2017 版本 15.3 +，NuGet 支援[Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="79336-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="79336-135">在舊版的用戶端不支援的 SemVer v2.0.0 特定語意。</span><span class="sxs-lookup"><span data-stu-id="79336-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="79336-136">NuGet 會考慮將封裝版本為特定的 SemVer v2.0.0，如果下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="79336-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="79336-137">發行前版本標籤是句點分隔，例如*1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="79336-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="79336-138">版本具有組建中繼資料，例如*1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="79336-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="79336-139">對於 nuget.org，封裝被定義為 SemVer v2.0.0 封裝，如果下列陳述式為 true:</span><span class="sxs-lookup"><span data-stu-id="79336-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="79336-140">封裝自己的版本為 SemVer v2.0.0 相容，但不是 SemVer 1.0.0 版相容，如上面所定義。</span><span class="sxs-lookup"><span data-stu-id="79336-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="79336-141">中的任何套件的相依性版本範圍有的最小值或最大版本 SemVer v2.0.0 相容，但不是 SemVer 1.0.0 版相容的上述; 定義例如， *[1.0.0-alpha.1,)*。</span><span class="sxs-lookup"><span data-stu-id="79336-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="79336-142">如果您上傳至 nuget.org 的 SemVer v2.0.0 特定套件，套件會是看不到舊的用戶端，並可供 只有下列的 NuGet 用戶端：</span><span class="sxs-lookup"><span data-stu-id="79336-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="79336-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="79336-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="79336-144">Visual Studio 2017 版本 15.3 +</span><span class="sxs-lookup"><span data-stu-id="79336-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="79336-145">Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="79336-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="79336-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="79336-146">dotnet</span></span>
  - <span data-ttu-id="79336-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="79336-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="79336-148">第三方用戶端：</span><span class="sxs-lookup"><span data-stu-id="79336-148">Third-party clients:</span></span>

- <span data-ttu-id="79336-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="79336-149">JetBrains Rider</span></span>
- <span data-ttu-id="79336-150">Paket 版本 5.0 +</span><span class="sxs-lookup"><span data-stu-id="79336-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="79336-151">版本範圍和萬用字元</span><span class="sxs-lookup"><span data-stu-id="79336-151">Version ranges and wildcards</span></span>

<span data-ttu-id="79336-152">當參考的套件相依性，NuGet 會支援使用間隔標記法來指定版本範圍，彙總，如下所示：</span><span class="sxs-lookup"><span data-stu-id="79336-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="79336-153">Notation</span><span class="sxs-lookup"><span data-stu-id="79336-153">Notation</span></span> | <span data-ttu-id="79336-154">套用的規則</span><span class="sxs-lookup"><span data-stu-id="79336-154">Applied rule</span></span> | <span data-ttu-id="79336-155">描述</span><span class="sxs-lookup"><span data-stu-id="79336-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="79336-156">1.0</span><span class="sxs-lookup"><span data-stu-id="79336-156">1.0</span></span> | <span data-ttu-id="79336-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="79336-157">x ≥ 1.0</span></span> | <span data-ttu-id="79336-158">最小版本含</span><span class="sxs-lookup"><span data-stu-id="79336-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="79336-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="79336-159">(1.0,)</span></span> | <span data-ttu-id="79336-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="79336-160">x > 1.0</span></span> | <span data-ttu-id="79336-161">最小版本獨佔</span><span class="sxs-lookup"><span data-stu-id="79336-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="79336-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="79336-162">[1.0]</span></span> | <span data-ttu-id="79336-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="79336-163">x == 1.0</span></span> | <span data-ttu-id="79336-164">確切的版本相符</span><span class="sxs-lookup"><span data-stu-id="79336-164">Exact version match</span></span> |
| <span data-ttu-id="79336-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="79336-165">(,1.0]</span></span> | <span data-ttu-id="79336-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="79336-166">x ≤ 1.0</span></span> | <span data-ttu-id="79336-167">最高版本內含</span><span class="sxs-lookup"><span data-stu-id="79336-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="79336-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="79336-168">(,1.0)</span></span> | <span data-ttu-id="79336-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="79336-169">x < 1.0</span></span> | <span data-ttu-id="79336-170">最高版本獨佔</span><span class="sxs-lookup"><span data-stu-id="79336-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="79336-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="79336-171">[1.0,2.0]</span></span> | <span data-ttu-id="79336-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="79336-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="79336-173">確切的範圍內含</span><span class="sxs-lookup"><span data-stu-id="79336-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="79336-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="79336-174">(1.0,2.0)</span></span> | <span data-ttu-id="79336-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="79336-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="79336-176">確切的範圍內獨佔</span><span class="sxs-lookup"><span data-stu-id="79336-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="79336-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="79336-177">[1.0,2.0)</span></span> | <span data-ttu-id="79336-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="79336-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="79336-179">混合式內含最小值和專屬的最高版本</span><span class="sxs-lookup"><span data-stu-id="79336-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="79336-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="79336-180">(1.0)</span></span>    | <span data-ttu-id="79336-181">無效</span><span class="sxs-lookup"><span data-stu-id="79336-181">invalid</span></span> | <span data-ttu-id="79336-182">無效</span><span class="sxs-lookup"><span data-stu-id="79336-182">invalid</span></span> |

<span data-ttu-id="79336-183">使用 PackageReference 格式時，NuGet 也支援使用萬用字元標記法， \*、 為主要、 次要、 修補程式和數字的發行前版本後置詞部分。</span><span class="sxs-lookup"><span data-stu-id="79336-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="79336-184">不支援萬用字元`packages.config`格式。</span><span class="sxs-lookup"><span data-stu-id="79336-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="79336-185">解析版本範圍時，不包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="79336-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="79336-186">發行前版本*都*包含時使用萬用字元 (\*)。</span><span class="sxs-lookup"><span data-stu-id="79336-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="79336-187">版本範圍 *[1.0,2.0]*，比方說，不包含 2.0 beta 版，但萬用字元標記法_2.0-\*_ 沒有。</span><span class="sxs-lookup"><span data-stu-id="79336-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="79336-188">請參閱[發出 912](https://github.com/NuGet/Home/issues/912)進一步討論需發行前版本的萬用字元。</span><span class="sxs-lookup"><span data-stu-id="79336-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="79336-189">範例</span><span class="sxs-lookup"><span data-stu-id="79336-189">Examples</span></span>

<span data-ttu-id="79336-190">一定要在專案檔中指定的版本或版本範圍，如封裝相依性`packages.config`檔案，和`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="79336-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="79336-191">不含版本或版本範圍，NuGet 2.8.x 和稍早選擇最新可用的套件版本時解析相依性，而 NuGet 3.x 和更新版本會選擇最低套件版本。</span><span class="sxs-lookup"><span data-stu-id="79336-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="79336-192">指定的版本或版本範圍可避免這種不確定性。</span><span class="sxs-lookup"><span data-stu-id="79336-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="79336-193">專案檔 (PackageReference) 中的參考</span><span class="sxs-lookup"><span data-stu-id="79336-193">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="79336-194">**在參考`packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="79336-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="79336-195">在  `packages.config`，有列出每個相依性，且確切`version`還原套件時使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="79336-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="79336-196">`allowedVersions`屬性僅更新作業期間用來限制可能會更新封裝版本。</span><span class="sxs-lookup"><span data-stu-id="79336-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="79336-197">**在參考`.nuspec`檔案**</span><span class="sxs-lookup"><span data-stu-id="79336-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="79336-198">`version`屬性中`<dependency>`項目描述範圍的版本可接受相依性。</span><span class="sxs-lookup"><span data-stu-id="79336-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="79336-199">正規化的版本號碼</span><span class="sxs-lookup"><span data-stu-id="79336-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="79336-200">這是一項重大變更適用於 NuGet 3.4 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="79336-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="79336-201">取得從存放庫的封裝，在安裝期間，重新安裝或還原作業，NuGet 3.4 + 會將版本號碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="79336-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="79336-202">前置的零會自版本號碼：</span><span class="sxs-lookup"><span data-stu-id="79336-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="79336-203">版本號碼的第四個部分中的零，則會予以忽略</span><span class="sxs-lookup"><span data-stu-id="79336-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="79336-204">這個正規化並不會影響套件本身; 中的版本號碼它會影響只如何 NuGet 會比對版本時解析相依性。</span><span class="sxs-lookup"><span data-stu-id="79336-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="79336-205">不過，NuGet 套件存放庫必須在與 NuGet 以避免套件版本重複相同的方式處理這些值。</span><span class="sxs-lookup"><span data-stu-id="79336-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="79336-206">因此包含版本的儲存機制*1.0*的封裝不應也裝載版本*1.0.0*為個別且不同的套件。</span><span class="sxs-lookup"><span data-stu-id="79336-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
