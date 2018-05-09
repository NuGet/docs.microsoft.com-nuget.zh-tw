---
title: NuGet 封裝版本的參考
description: 確切的指定版本號碼和範圍而定的 NuGet 封裝，並安裝相依性的方式在其他封裝的詳細資訊。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: d17d964ac73075f05678b9727e90d481a30da62e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="package-versioning"></a><span data-ttu-id="af48d-103">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="af48d-103">Package versioning</span></span>

<span data-ttu-id="af48d-104">特定封裝永遠被指使用其封裝識別碼和確切的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="af48d-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="af48d-105">例如， [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org 上有數個數十種特定封裝可用，範圍從版本*4.1.10311*版本*6.1.3* （最新穩定發行） 和各種不同的發行前版本*6.2.0-beta1*。</span><span class="sxs-lookup"><span data-stu-id="af48d-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="af48d-106">在建立封裝時，您會指定特定版本號碼的選擇性發行前的文字尾碼。</span><span class="sxs-lookup"><span data-stu-id="af48d-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="af48d-107">當使用封裝，相反地，您可以指定確切的版本號碼或一個範圍的可接受的版本。</span><span class="sxs-lookup"><span data-stu-id="af48d-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="af48d-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="af48d-108">In this topic:</span></span>

- <span data-ttu-id="af48d-109">[版本的基本概念](#version-basics)包括發行前版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="af48d-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="af48d-110">版本範圍與萬用字元</span><span class="sxs-lookup"><span data-stu-id="af48d-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="af48d-111">正規化的版本號碼</span><span class="sxs-lookup"><span data-stu-id="af48d-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="af48d-112">版本的基本概念</span><span class="sxs-lookup"><span data-stu-id="af48d-112">Version basics</span></span>

<span data-ttu-id="af48d-113">特定版本號碼的格式為*Major.Minor.Patch [-後置詞]*、 其中的元件具有以下意義：</span><span class="sxs-lookup"><span data-stu-id="af48d-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="af48d-114">*主要*： 重大變更</span><span class="sxs-lookup"><span data-stu-id="af48d-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="af48d-115">*次要*： 新的功能，但回溯相容性</span><span class="sxs-lookup"><span data-stu-id="af48d-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="af48d-116">*修補程式*： 只有具備回溯相容性 bug 修正</span><span class="sxs-lookup"><span data-stu-id="af48d-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="af48d-117">*-尾碼*（選擇性）： 連字號後面接著此項表示應發行前版本字串 (下列[語意化版本控制或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="af48d-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="af48d-118">**範例：**</span><span class="sxs-lookup"><span data-stu-id="af48d-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="af48d-119">nuget.org 會拒絕任何缺少的確切的版本號碼的封裝上傳。</span><span class="sxs-lookup"><span data-stu-id="af48d-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="af48d-120">必須在指定的版本`.nuspec`或用來建立封裝的專案檔。</span><span class="sxs-lookup"><span data-stu-id="af48d-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="af48d-121">發行前版本</span><span class="sxs-lookup"><span data-stu-id="af48d-121">Pre-release versions</span></span>

<span data-ttu-id="af48d-122">就技術上來說，封裝建立者可以使用任何字串做為尾碼來代表發行前版本，如 NuGet 視為發行前版本的任何這類的版本，並讓其他的解譯方式。</span><span class="sxs-lookup"><span data-stu-id="af48d-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="af48d-123">也就是說，NuGet 會顯示任何 UI 中的完整版本字串涉及時，取用者留下任何解譯的後置詞的意義。</span><span class="sxs-lookup"><span data-stu-id="af48d-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="af48d-124">話雖如此，封裝開發人員通常會依照可辨識的命名慣例：</span><span class="sxs-lookup"><span data-stu-id="af48d-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="af48d-125">`-alpha`: Alpha 版本中，通常用於工作的進度和試驗。</span><span class="sxs-lookup"><span data-stu-id="af48d-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="af48d-126">`-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的 Bug。</span><span class="sxs-lookup"><span data-stu-id="af48d-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="af48d-127">`-rc`：候選版，除非出現重大的 Bug，不然通常是準最終版本 (穩定版)。</span><span class="sxs-lookup"><span data-stu-id="af48d-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="af48d-128">NuGet 4.3.0+ 支援[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，可支援使用點標記法，發行前版本號碼中*1.0.1-build.23*。</span><span class="sxs-lookup"><span data-stu-id="af48d-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="af48d-129">4.3.0 之前的 NuGet 版本不支援點標記法。</span><span class="sxs-lookup"><span data-stu-id="af48d-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="af48d-130">您可以使用的表單*1.0.1-build23*。</span><span class="sxs-lookup"><span data-stu-id="af48d-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="af48d-131">解決時封裝會參照和多個封裝版本只有不同後置詞，NuGet 首先，選擇的版本不含尾碼，然後套用至發行前版本，以反向字母順序的優先順序。</span><span class="sxs-lookup"><span data-stu-id="af48d-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="af48d-132">例如，下列版本本來的順序顯示：</span><span class="sxs-lookup"><span data-stu-id="af48d-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="af48d-133">2.0.0 的語意版本設定</span><span class="sxs-lookup"><span data-stu-id="af48d-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="af48d-134">使用 NuGet 4.3.0+ 和 Visual Studio 2017 15.3 + 版本，支援 NuGet[語意版本設定 2.0.0](http://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="af48d-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="af48d-135">在舊版的用戶端不支援的 SemVer v2.0.0 特定語意。</span><span class="sxs-lookup"><span data-stu-id="af48d-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="af48d-136">NuGet 會考慮下列陳述式是否是 SemVer v2.0.0 特定的封裝版本：</span><span class="sxs-lookup"><span data-stu-id="af48d-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="af48d-137">發行前版本標籤是點分隔，例如*1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="af48d-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="af48d-138">版本有建置中繼資料，例如*1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="af48d-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="af48d-139">對於 nuget.org，封裝定義為 SemVer v2.0.0 封裝如果為 true，下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="af48d-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="af48d-140">封裝自己版本是 SemVer v2.0.0 相容，但相容、 不 SemVer v1.0.0 上方所定義。</span><span class="sxs-lookup"><span data-stu-id="af48d-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="af48d-141">所有封裝的相依性版本範圍有不相容 SemVer v2.0.0 但相容、 不 SemVer v1.0.0; 上述定義的最小值或最大版本例如， *[1.0.0-alpha.1,)*。</span><span class="sxs-lookup"><span data-stu-id="af48d-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="af48d-142">如果您要 nuget.org 傳 SemVer v2.0.0 特定封裝，封裝是看不到舊版的用戶端，並可供 只有下列 NuGet 用戶端：</span><span class="sxs-lookup"><span data-stu-id="af48d-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="af48d-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="af48d-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="af48d-144">Visual Studio 2017 15.3 + 版本</span><span class="sxs-lookup"><span data-stu-id="af48d-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="af48d-145">Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="af48d-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="af48d-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="af48d-146">dotnet</span></span>
  - <span data-ttu-id="af48d-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="af48d-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="af48d-148">第三方用戶端：</span><span class="sxs-lookup"><span data-stu-id="af48d-148">Third-party clients:</span></span>

- <span data-ttu-id="af48d-149">JetBrains 騎兵</span><span class="sxs-lookup"><span data-stu-id="af48d-149">JetBrains Rider</span></span>
- <span data-ttu-id="af48d-150">Paket 5.0 + 版本</span><span class="sxs-lookup"><span data-stu-id="af48d-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="af48d-151">版本範圍與萬用字元</span><span class="sxs-lookup"><span data-stu-id="af48d-151">Version ranges and wildcards</span></span>

<span data-ttu-id="af48d-152">當參照的套件相依性，NuGet 會支援使用間隔標記法來指定版本範圍，彙總，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af48d-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="af48d-153">Notation</span><span class="sxs-lookup"><span data-stu-id="af48d-153">Notation</span></span> | <span data-ttu-id="af48d-154">套用的規則</span><span class="sxs-lookup"><span data-stu-id="af48d-154">Applied rule</span></span> | <span data-ttu-id="af48d-155">描述</span><span class="sxs-lookup"><span data-stu-id="af48d-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="af48d-156">1.0</span><span class="sxs-lookup"><span data-stu-id="af48d-156">1.0</span></span> | <span data-ttu-id="af48d-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="af48d-157">x ≥ 1.0</span></span> | <span data-ttu-id="af48d-158">最小版本 （含）</span><span class="sxs-lookup"><span data-stu-id="af48d-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="af48d-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="af48d-159">(1.0,)</span></span> | <span data-ttu-id="af48d-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="af48d-160">x > 1.0</span></span> | <span data-ttu-id="af48d-161">最小版本，而獨佔式</span><span class="sxs-lookup"><span data-stu-id="af48d-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="af48d-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="af48d-162">[1.0]</span></span> | <span data-ttu-id="af48d-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="af48d-163">x == 1.0</span></span> | <span data-ttu-id="af48d-164">確切的版本相符項目</span><span class="sxs-lookup"><span data-stu-id="af48d-164">Exact version match</span></span> |
| <span data-ttu-id="af48d-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="af48d-165">(,1.0]</span></span> | <span data-ttu-id="af48d-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="af48d-166">x ≤ 1.0</span></span> | <span data-ttu-id="af48d-167">最大版本，（含）</span><span class="sxs-lookup"><span data-stu-id="af48d-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="af48d-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="af48d-168">(,1.0)</span></span> | <span data-ttu-id="af48d-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="af48d-169">x < 1.0</span></span> | <span data-ttu-id="af48d-170">最大版本，而獨佔式</span><span class="sxs-lookup"><span data-stu-id="af48d-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="af48d-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="af48d-171">[1.0,2.0]</span></span> | <span data-ttu-id="af48d-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="af48d-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="af48d-173">確切的範圍內含</span><span class="sxs-lookup"><span data-stu-id="af48d-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="af48d-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="af48d-174">(1.0,2.0)</span></span> | <span data-ttu-id="af48d-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="af48d-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="af48d-176">確切的範圍，獨占</span><span class="sxs-lookup"><span data-stu-id="af48d-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="af48d-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="af48d-177">[1.0,2.0)</span></span> | <span data-ttu-id="af48d-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="af48d-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="af48d-179">混合含最小值和獨佔式最大版本</span><span class="sxs-lookup"><span data-stu-id="af48d-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="af48d-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="af48d-180">(1.0)</span></span>    | <span data-ttu-id="af48d-181">無效</span><span class="sxs-lookup"><span data-stu-id="af48d-181">invalid</span></span> | <span data-ttu-id="af48d-182">無效</span><span class="sxs-lookup"><span data-stu-id="af48d-182">invalid</span></span> |

<span data-ttu-id="af48d-183">使用 PackageReference 格式時，NuGet 也支援使用萬用字元標記法\*、 主要、 次要、 修補程式，和數字的發行前版本後置字元部分。</span><span class="sxs-lookup"><span data-stu-id="af48d-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="af48d-184">不支援萬用字元`packages.config`格式。</span><span class="sxs-lookup"><span data-stu-id="af48d-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="af48d-185">解決版本範圍時，不會包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="af48d-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="af48d-186">發行前版本*是*包含時使用萬用字元 (\*)。</span><span class="sxs-lookup"><span data-stu-id="af48d-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="af48d-187">版本範圍 *[1.0,2.0]*，比方說，不包括 2.0 beta 版，但萬用字元標記法_2.0-\*_ 沒有。</span><span class="sxs-lookup"><span data-stu-id="af48d-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="af48d-188">請參閱[發出 912](https://github.com/NuGet/Home/issues/912)的進一步討論發行前版本萬用字元。</span><span class="sxs-lookup"><span data-stu-id="af48d-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="af48d-189">範例</span><span class="sxs-lookup"><span data-stu-id="af48d-189">Examples</span></span>

<span data-ttu-id="af48d-190">一律在專案檔中指定版本或封裝的相依性的版本範圍`packages.config`檔案，並`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="af48d-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="af48d-191">不含版本或版本範圍，NuGet 2.8.x 稍早選擇最新可用的封裝版本時解析相依性，而 NuGet 3.x 及更新版本選擇最低的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="af48d-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="af48d-192">指定的版本或版本範圍可避免此有助於減少不確定性。</span><span class="sxs-lookup"><span data-stu-id="af48d-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="af48d-193">專案檔 (PackageReference) 中的參考</span><span class="sxs-lookup"><span data-stu-id="af48d-193">References in project files (PackageReference)</span></span>

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="af48d-194">**在參考`packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="af48d-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="af48d-195">在`packages.config`，每個相依性列為完全`version`還原封裝時所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="af48d-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="af48d-196">`allowedVersions`屬性只有在更新作業期間用來限制可能會更新封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="af48d-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="af48d-197">**在參考`.nuspec`檔案**</span><span class="sxs-lookup"><span data-stu-id="af48d-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="af48d-198">`version`屬性`<dependency>`元素描述可接受的相依性範圍版本。</span><span class="sxs-lookup"><span data-stu-id="af48d-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="af48d-199">正規化的版本號碼</span><span class="sxs-lookup"><span data-stu-id="af48d-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="af48d-200">這是一項重大變更及更新版本的 NuGet 3.4。</span><span class="sxs-lookup"><span data-stu-id="af48d-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="af48d-201">取得從儲存機制的封裝，在安裝期間，重新安裝，或還原作業，NuGet 3.4 + 會將版本號碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af48d-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="af48d-202">前置的零會從版本號碼：</span><span class="sxs-lookup"><span data-stu-id="af48d-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="af48d-203">版本號碼的第四個部分中的零，則會予以忽略</span><span class="sxs-lookup"><span data-stu-id="af48d-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="af48d-204">這個正規化不會影響封裝本身; 中的版本號碼它會影響只如何 NuGet 符合版本解析相依性時。</span><span class="sxs-lookup"><span data-stu-id="af48d-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="af48d-205">不過，NuGet 封裝儲存機制必須與 NuGet 來避免封裝版本重複相同的方式處理這些值。</span><span class="sxs-lookup"><span data-stu-id="af48d-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="af48d-206">因此，包含版本的儲存機制*1.0*的封裝不應也裝載版本*1.0.0*個別且不同的套件。</span><span class="sxs-lookup"><span data-stu-id="af48d-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
