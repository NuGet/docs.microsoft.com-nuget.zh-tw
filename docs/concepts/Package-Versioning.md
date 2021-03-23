---
title: NuGet 套件版本參考
description: 為 NuGet 套件相依的其他套件指定版本號碼和範圍，以及相依性安裝方式的確切詳細資料。
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 77b96e83f8fc7afd391537d16120d037585dd379
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859196"
---
# <a name="package-versioning"></a><span data-ttu-id="7dad3-103">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="7dad3-103">Package versioning</span></span>

<span data-ttu-id="7dad3-104">您一律必須使用套件的套件識別碼與確切版本號碼來參考特定套件。</span><span class="sxs-lookup"><span data-stu-id="7dad3-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="7dad3-105">例如，nuget.org 上的 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) \(英文\) 有數十個特定套件可用，範圍從 *4.1.10311* 版到 *6.1.3* 版 (最新穩定版本) 與各種發行前版本 (像是 *6.2.0-beta1*)。</span><span class="sxs-lookup"><span data-stu-id="7dad3-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="7dad3-106">在建立套件時，您可以搭配選擇性的發行前版本文字尾碼來指派特定版本號碼。</span><span class="sxs-lookup"><span data-stu-id="7dad3-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="7dad3-107">另一方面，在取用套件時，您可以指定確切版本號碼或可接受的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="7dad3-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="7dad3-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="7dad3-108">In this topic:</span></span>

- <span data-ttu-id="7dad3-109">[版本基本概念](#version-basics)包含發行前版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="7dad3-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="7dad3-110">版本範圍</span><span class="sxs-lookup"><span data-stu-id="7dad3-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="7dad3-111">標準化版本號碼</span><span class="sxs-lookup"><span data-stu-id="7dad3-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="7dad3-112">版本基本概念</span><span class="sxs-lookup"><span data-stu-id="7dad3-112">Version basics</span></span>

<span data-ttu-id="7dad3-113">特定版本號碼的格式為「主要.次要.修補程式[-尾碼]」，其中的元件具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="7dad3-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="7dad3-114">*主要*：重大變更</span><span class="sxs-lookup"><span data-stu-id="7dad3-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="7dad3-115">*次要*：新功能，但與舊版相容</span><span class="sxs-lookup"><span data-stu-id="7dad3-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="7dad3-116">*Patch*：僅回溯相容的 bug 修正</span><span class="sxs-lookup"><span data-stu-id="7dad3-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="7dad3-117">「-尾碼」(選擇性)：後面接著字串的連字號，表示發行前版本 (遵循[語意化版本控制系統或 SemVer 1.0 慣例](https://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="7dad3-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="7dad3-118">**範例：**</span><span class="sxs-lookup"><span data-stu-id="7dad3-118">**Examples:**</span></span>

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="7dad3-119">nuget.org 會拒絕任何缺少確切版本號碼的套件上傳。</span><span class="sxs-lookup"><span data-stu-id="7dad3-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="7dad3-120">您必須在 `.nuspec` 中，或在用來建立套件的專案檔中指定版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="7dad3-121">發行前版本</span><span class="sxs-lookup"><span data-stu-id="7dad3-121">Pre-release versions</span></span>

<span data-ttu-id="7dad3-122">就技術上而言，套件建立者可以使用任何字串作為尾碼來表示發行前版本，因為 NuGet 會將任何此類版本視為發行前版本，而且不會進行任何其他解讀。</span><span class="sxs-lookup"><span data-stu-id="7dad3-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="7dad3-123">也就是說，NuGet 會在牽涉到的任何 UI 中顯示完整版本字串，尾碼之意義的任何解讀，都保留給取用者。</span><span class="sxs-lookup"><span data-stu-id="7dad3-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="7dad3-124">話雖如此，套件開發人員通常會遵循公認的命名慣例：</span><span class="sxs-lookup"><span data-stu-id="7dad3-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="7dad3-125">`-alpha`： Alpha 版本，通常用於進行中的工作和實驗。</span><span class="sxs-lookup"><span data-stu-id="7dad3-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="7dad3-126">`-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的 Bug。</span><span class="sxs-lookup"><span data-stu-id="7dad3-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="7dad3-127">`-rc`：候選版，除非出現重大的 Bug，不然通常是準最終版本 (穩定版)。</span><span class="sxs-lookup"><span data-stu-id="7dad3-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="7dad3-128">NuGet 4.3.0+ 支援 [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html)，它支援使用點標記法的發行前版本號碼，如 *1.0.1-build.23*。</span><span class="sxs-lookup"><span data-stu-id="7dad3-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="7dad3-129">4.3.0 之前的 NuGet 版本不支援點標記法。</span><span class="sxs-lookup"><span data-stu-id="7dad3-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="7dad3-130">您可以使用像 *1.0.1-build23* 的格式。</span><span class="sxs-lookup"><span data-stu-id="7dad3-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="7dad3-131">解析套件參考且多個套件版本只有尾碼不同時，NuGet 會先選擇不含尾碼的版本，然後再依相反字母順序套用發行前版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="7dad3-132">例如，系統會依照所示的順序選擇下列版本：</span><span class="sxs-lookup"><span data-stu-id="7dad3-132">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="7dad3-133">語意化版本控制系統 2.0.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="7dad3-134">使用 NuGet 4.3.0+ 與 Visual Studio 2017 15.3+ 版，NuGet 支援[語意化版本控制系統 2.0.0](https://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="7dad3-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="7dad3-135">較舊的用戶端不支援 SemVer v2.0.0 的某些語意。</span><span class="sxs-lookup"><span data-stu-id="7dad3-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="7dad3-136">如果下列其中一個敘述成立，則 NuGet 會將套件版本視為 SemVer v2.0.0 特定：</span><span class="sxs-lookup"><span data-stu-id="7dad3-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="7dad3-137">發行前版本標籤是以點分隔的，例如 *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="7dad3-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="7dad3-138">版本有組建中繼資料，例如 *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="7dad3-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="7dad3-139">針對 nuget.org，如果下列其中一個敘述立，則會將套件定義為 SemVer v2.0.0 套件：</span><span class="sxs-lookup"><span data-stu-id="7dad3-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="7dad3-140">套件本身的版本符合 SemVer v2.0.0 的規範，但不符合 SemVer v1.0.0 的規範，如上面所定義。</span><span class="sxs-lookup"><span data-stu-id="7dad3-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="7dad3-141">套件的任何相依性版本範圍都有最小或最大版本，它們符合 SemVer v2.0.0 的規範，但不符合 SemVer v1.0.0 規範，如上面所定義；例如，*[1.0.0-alpha.1, )*。</span><span class="sxs-lookup"><span data-stu-id="7dad3-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="7dad3-142">如果您將 SemVer v2.0.0 特定套件上傳到 nuget.org，則舊版用戶端看不到該套件，只有下列 NuGet 用戶端可以取得該套件：</span><span class="sxs-lookup"><span data-stu-id="7dad3-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="7dad3-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="7dad3-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="7dad3-144">Visual Studio 2017 15.3+ 版</span><span class="sxs-lookup"><span data-stu-id="7dad3-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="7dad3-145">Visual Studio 2015 (含 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix))</span><span class="sxs-lookup"><span data-stu-id="7dad3-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="7dad3-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="7dad3-146">dotnet</span></span>
  - <span data-ttu-id="7dad3-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="7dad3-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="7dad3-148">協力廠商用戶端：</span><span class="sxs-lookup"><span data-stu-id="7dad3-148">Third-party clients:</span></span>

- <span data-ttu-id="7dad3-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="7dad3-149">JetBrains Rider</span></span>
- <span data-ttu-id="7dad3-150">Paket 5.0+ 版</span><span class="sxs-lookup"><span data-stu-id="7dad3-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="7dad3-151">版本範圍</span><span class="sxs-lookup"><span data-stu-id="7dad3-151">Version ranges</span></span>

<span data-ttu-id="7dad3-152">在參考套件相依性時，NuGet 支援使用間隔標記法來指定版本範圍，摘要說明如下：</span><span class="sxs-lookup"><span data-stu-id="7dad3-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="7dad3-153">表示法</span><span class="sxs-lookup"><span data-stu-id="7dad3-153">Notation</span></span> | <span data-ttu-id="7dad3-154">套用的規則</span><span class="sxs-lookup"><span data-stu-id="7dad3-154">Applied rule</span></span> | <span data-ttu-id="7dad3-155">描述</span><span class="sxs-lookup"><span data-stu-id="7dad3-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="7dad3-156">1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-156">1.0</span></span> | <span data-ttu-id="7dad3-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-157">x ≥ 1.0</span></span> | <span data-ttu-id="7dad3-158">最小版本 (包含)</span><span class="sxs-lookup"><span data-stu-id="7dad3-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="7dad3-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="7dad3-159">(1.0,)</span></span> | <span data-ttu-id="7dad3-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-160">x > 1.0</span></span> | <span data-ttu-id="7dad3-161">最小版本 (不包含)</span><span class="sxs-lookup"><span data-stu-id="7dad3-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="7dad3-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="7dad3-162">[1.0]</span></span> | <span data-ttu-id="7dad3-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-163">x == 1.0</span></span> | <span data-ttu-id="7dad3-164">完全相符的版本</span><span class="sxs-lookup"><span data-stu-id="7dad3-164">Exact version match</span></span> |
| <span data-ttu-id="7dad3-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="7dad3-165">(,1.0]</span></span> | <span data-ttu-id="7dad3-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-166">x ≤ 1.0</span></span> | <span data-ttu-id="7dad3-167">最大版本 (包含)</span><span class="sxs-lookup"><span data-stu-id="7dad3-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="7dad3-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="7dad3-168">(,1.0)</span></span> | <span data-ttu-id="7dad3-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-169">x < 1.0</span></span> | <span data-ttu-id="7dad3-170">最大版本 (不包含)</span><span class="sxs-lookup"><span data-stu-id="7dad3-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="7dad3-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="7dad3-171">[1.0,2.0]</span></span> | <span data-ttu-id="7dad3-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="7dad3-173">完全相符的範圍 (包含)</span><span class="sxs-lookup"><span data-stu-id="7dad3-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="7dad3-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="7dad3-174">(1.0,2.0)</span></span> | <span data-ttu-id="7dad3-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="7dad3-176">完全相符的範圍 (不包含)</span><span class="sxs-lookup"><span data-stu-id="7dad3-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="7dad3-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="7dad3-177">[1.0,2.0)</span></span> | <span data-ttu-id="7dad3-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="7dad3-179">混合包含最小且不包含最大版本</span><span class="sxs-lookup"><span data-stu-id="7dad3-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="7dad3-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="7dad3-180">(1.0)</span></span>    | <span data-ttu-id="7dad3-181">無效</span><span class="sxs-lookup"><span data-stu-id="7dad3-181">invalid</span></span> | <span data-ttu-id="7dad3-182">無效</span><span class="sxs-lookup"><span data-stu-id="7dad3-182">invalid</span></span> |

<span data-ttu-id="7dad3-183">使用 PackageReference 格式時，NuGet 也支援使用浮動標記法， \* 以用於數位的主要、次要、修補和預先發行尾碼部分。</span><span class="sxs-lookup"><span data-stu-id="7dad3-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="7dad3-184">格式不支援浮動版本 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="7dad3-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="7dad3-185">當指定浮動版本時，規則會解析為符合版本描述的最高版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="7dad3-186">浮動版本和解決方法的範例如下。</span><span class="sxs-lookup"><span data-stu-id="7dad3-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="7dad3-187">PackageReference 中的版本範圍包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="7dad3-188">根據設計，浮動版本不會解析發行前版本，除非選擇加入。</span><span class="sxs-lookup"><span data-stu-id="7dad3-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="7dad3-189">如需相關功能要求的狀態，請參閱[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7dad3-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="7dad3-190">範例</span><span class="sxs-lookup"><span data-stu-id="7dad3-190">Examples</span></span>

<span data-ttu-id="7dad3-191">請一律針對專案檔、`packages.config` 檔案與 `.nuspec` 檔案中的套件相依性指定版本或版本範圍。</span><span class="sxs-lookup"><span data-stu-id="7dad3-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="7dad3-192">如果沒有版本或版本範圍，NuGet 2.8. x 和更早的版本會在解析相依性時選擇最新可用套件版本，而 NuGet 3.x 和更新版本會選擇最低套件版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="7dad3-193">指定版本或版本範圍可避免這種不確定性。</span><span class="sxs-lookup"><span data-stu-id="7dad3-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="7dad3-194">專案檔中的參考 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="7dad3-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="7dad3-195">浮動版本解析</span><span class="sxs-lookup"><span data-stu-id="7dad3-195">Floating version resolutions</span></span> 

| <span data-ttu-id="7dad3-196">版本</span><span class="sxs-lookup"><span data-stu-id="7dad3-196">Version</span></span> | <span data-ttu-id="7dad3-197">存在於伺服器上的版本</span><span class="sxs-lookup"><span data-stu-id="7dad3-197">Versions present on server</span></span> | <span data-ttu-id="7dad3-198">解決方案</span><span class="sxs-lookup"><span data-stu-id="7dad3-198">Resolution</span></span> | <span data-ttu-id="7dad3-199">原因</span><span class="sxs-lookup"><span data-stu-id="7dad3-199">Reason</span></span> | <span data-ttu-id="7dad3-200">備註</span><span class="sxs-lookup"><span data-stu-id="7dad3-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="7dad3-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-201">1.1.0</span></span> <br> <span data-ttu-id="7dad3-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="7dad3-202">1.1.1</span></span> <br> <span data-ttu-id="7dad3-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-203">1.2.0</span></span> <br> <span data-ttu-id="7dad3-204">1.3.0-Alpha</span><span class="sxs-lookup"><span data-stu-id="7dad3-204">1.3.0-alpha</span></span>  | <span data-ttu-id="7dad3-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-205">1.2.0</span></span> | <span data-ttu-id="7dad3-206">最高穩定版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-206">The highest stable version.</span></span> |
| <span data-ttu-id="7dad3-207">1.1.\*</span><span class="sxs-lookup"><span data-stu-id="7dad3-207">1.1.\*</span></span> | <span data-ttu-id="7dad3-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-208">1.1.0</span></span> <br> <span data-ttu-id="7dad3-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="7dad3-209">1.1.1</span></span> <br> <span data-ttu-id="7dad3-210">1.1.2-Alpha</span><span class="sxs-lookup"><span data-stu-id="7dad3-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="7dad3-211">1.2.0-Alpha</span><span class="sxs-lookup"><span data-stu-id="7dad3-211">1.2.0-alpha</span></span> | <span data-ttu-id="7dad3-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="7dad3-212">1.1.1</span></span> | <span data-ttu-id="7dad3-213">遵循指定模式的最高穩定版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="7dad3-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="7dad3-214">\* - \*</span></span> | <span data-ttu-id="7dad3-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-215">1.1.0</span></span> <br> <span data-ttu-id="7dad3-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="7dad3-216">1.1.1</span></span> <br> <span data-ttu-id="7dad3-217">1.1.2-Alpha</span><span class="sxs-lookup"><span data-stu-id="7dad3-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="7dad3-218">1.3.0-Beta</span><span class="sxs-lookup"><span data-stu-id="7dad3-218">1.3.0-beta</span></span>  | <span data-ttu-id="7dad3-219">1.3.0-Beta</span><span class="sxs-lookup"><span data-stu-id="7dad3-219">1.3.0-beta</span></span> | <span data-ttu-id="7dad3-220">最高版本，包括不穩定版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="7dad3-221">適用于 Visual Studio 16.6 版、NuGet 5.6 版、.NET Core SDK 版本3.1.300</span><span class="sxs-lookup"><span data-stu-id="7dad3-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="7dad3-222">1.1. *-*</span><span class="sxs-lookup"><span data-stu-id="7dad3-222">1.1.\* - \*</span></span> | <span data-ttu-id="7dad3-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="7dad3-223">1.1.0</span></span> <br> <span data-ttu-id="7dad3-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="7dad3-224">1.1.1</span></span> <br> <span data-ttu-id="7dad3-225">1.1.2-Alpha</span><span class="sxs-lookup"><span data-stu-id="7dad3-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="7dad3-226">1.1.2-Beta</span><span class="sxs-lookup"><span data-stu-id="7dad3-226">1.1.2-beta</span></span> <br> <span data-ttu-id="7dad3-227">1.3.0-Beta</span><span class="sxs-lookup"><span data-stu-id="7dad3-227">1.3.0-beta</span></span>  | <span data-ttu-id="7dad3-228">1.1.2-Beta</span><span class="sxs-lookup"><span data-stu-id="7dad3-228">1.1.2-beta</span></span> | <span data-ttu-id="7dad3-229">採用模式並包含不穩定版本的最高版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="7dad3-230">適用于 Visual Studio 16.6 版、NuGet 5.6 版、.NET Core SDK 版本3.1.300</span><span class="sxs-lookup"><span data-stu-id="7dad3-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="7dad3-231">**`packages.config` 中的參考：**</span><span class="sxs-lookup"><span data-stu-id="7dad3-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="7dad3-232">在 `packages.config` 中，每個相依性都會隨還原套件時使用的確切 `version` 屬性一併列出。</span><span class="sxs-lookup"><span data-stu-id="7dad3-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="7dad3-233">只有在更新作業期間，才會使用 `allowedVersions` 屬性來限制套件可能更新的版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="7dad3-234">**`.nuspec` 檔案中的參考**</span><span class="sxs-lookup"><span data-stu-id="7dad3-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="7dad3-235">`<dependency>` 元素中的 `version` 屬性描述相依性可接受的範圍版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="7dad3-236">標準化版本號碼</span><span class="sxs-lookup"><span data-stu-id="7dad3-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="7dad3-237">這是 NuGet 3.4 和更新版本的中斷性變更。</span><span class="sxs-lookup"><span data-stu-id="7dad3-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="7dad3-238">在安裝、重新安裝或還原作業期間從存放庫取得套件時，NuGet 3.4+ 會依照下列方式來對待版本號碼：</span><span class="sxs-lookup"><span data-stu-id="7dad3-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="7dad3-239">系統會將前置零從版本號碼移除：</span><span class="sxs-lookup"><span data-stu-id="7dad3-239">Leading zeroes are removed from version numbers:</span></span>

  <span data-ttu-id="7dad3-240">1.00 被視為 1.0 1.01.1 被視為 1.1.1 1.00.0.1 被視為1.0.0。1</span><span class="sxs-lookup"><span data-stu-id="7dad3-240">1.00 is treated as 1.0 1.01.1 is treated as 1.1.1 1.00.0.1 is treated as 1.0.0.1</span></span>

- <span data-ttu-id="7dad3-241">系統會移除在版本號碼第四部分中的零</span><span class="sxs-lookup"><span data-stu-id="7dad3-241">A zero in the fourth part of the version number will be omitted</span></span>

  <span data-ttu-id="7dad3-242">1.0.0.0 被視為 1.0.0 1.0.01.0 被視為1.0。1</span><span class="sxs-lookup"><span data-stu-id="7dad3-242">1.0.0.0 is treated as 1.0.0 1.0.01.0 is treated as 1.0.1</span></span>

- <span data-ttu-id="7dad3-243">已移除 SemVer 2.0.0 組建中繼資料</span><span class="sxs-lookup"><span data-stu-id="7dad3-243">SemVer 2.0.0 build metadata is removed</span></span>

  <span data-ttu-id="7dad3-244">1.0.7 + r3456 被視為1.0。7</span><span class="sxs-lookup"><span data-stu-id="7dad3-244">1.0.7+r3456 is treated as 1.0.7</span></span>

<span data-ttu-id="7dad3-245">`pack` 與 `restore` 作業會盡可能將版本標準化。</span><span class="sxs-lookup"><span data-stu-id="7dad3-245">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="7dad3-246">針對已建置的套件，此標準化不會影響套件本身的版本號碼；它只會影響 NuGet 在解析相依性時如何比對版本。</span><span class="sxs-lookup"><span data-stu-id="7dad3-246">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="7dad3-247">不過，NuGet 套件存放庫必須以與 NuGet 相同的方式來處理這些值，以防止套件版本重複。</span><span class="sxs-lookup"><span data-stu-id="7dad3-247">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="7dad3-248">因此，包含 *1.0* 版套件的存放庫，不應該也裝載 *1.0.0* 版，並作為個別且不同的套件。</span><span class="sxs-lookup"><span data-stu-id="7dad3-248">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>

## <a name="where-nugetversion-diverges-from-semantic-versioning"></a><span data-ttu-id="7dad3-249">從語義版本控制 NuGetVersion 分歧</span><span class="sxs-lookup"><span data-stu-id="7dad3-249">Where NuGetVersion diverges from Semantic Versioning</span></span>

<span data-ttu-id="7dad3-250">如果您想要以程式設計方式使用 NuGet 套件版本，強烈建議使用 [封裝 nuget。版本控制](https://www.nuget.org/packages/NuGet.Versioning)。</span><span class="sxs-lookup"><span data-stu-id="7dad3-250">If you want to programatically use NuGet package versions, it is strongly recommended to use [the package NuGet.Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span></span> <span data-ttu-id="7dad3-251">靜態方法 `NuGetVersion.Parse(string)` 可用來剖析版本字串，而且 `VersionComparer` 可以用來排序 `NuGetVersion` 實例。</span><span class="sxs-lookup"><span data-stu-id="7dad3-251">The static method `NuGetVersion.Parse(string)` can be used to parse the version strings, and `VersionComparer` can be used to sort `NuGetVersion` instances.</span></span>

<span data-ttu-id="7dad3-252">如果您要使用不在 .NET 上執行的語言來執行 NuGet 功能，以下是和語義版本控制之間的已知差異清單 `NuGetVersion` ，以及現有的語義版本設定庫對於已在 nuget.org 上發行的封裝而言可能無法運作的原因。</span><span class="sxs-lookup"><span data-stu-id="7dad3-252">If you are implementing NuGet functionality in a language that does not run on .NET, here are the known list of differences between `NuGetVersion` and Semantic Versioning, and the reasons why an existing Semantic Versioning library might not work for packages already published on nuget.org.</span></span>

1. <span data-ttu-id="7dad3-253">`NuGetVersion` 支援第四個版本區段， `Revision` 以相容于或的超集合 [`System.Version`](/dotnet/api/system.version) 。</span><span class="sxs-lookup"><span data-stu-id="7dad3-253">`NuGetVersion` supports a 4th version segment, `Revision`, to be compatible with, or a superset of, [`System.Version`](/dotnet/api/system.version).</span></span> <span data-ttu-id="7dad3-254">因此，不包括發行前版本和中繼資料標籤，版本字串為 `Major.Minor.Patch.Revision` 。</span><span class="sxs-lookup"><span data-stu-id="7dad3-254">Therefore, excluding prerelease and metadata labels, a version string is `Major.Minor.Patch.Revision`.</span></span> <span data-ttu-id="7dad3-255">根據上面所述的版本正規化，如果 `Revision` 是零，則會省略正規化版本字串中的。</span><span class="sxs-lookup"><span data-stu-id="7dad3-255">As per version normalization described above, if `Revision` is zero, it is omit from the normalized version string.</span></span>
2. <span data-ttu-id="7dad3-256">`NuGetVersion` 只需要定義主要區段。</span><span class="sxs-lookup"><span data-stu-id="7dad3-256">`NuGetVersion` only requires the major segment to be defined.</span></span> <span data-ttu-id="7dad3-257">所有其他專案都是選擇性的，且相當於零。</span><span class="sxs-lookup"><span data-stu-id="7dad3-257">All others are optional, and are equivalent to zero.</span></span> <span data-ttu-id="7dad3-258">這表示 `1` 、、 `1.0` `1.0.0` 和 `1.0.0.0` 都是已接受且相等的。</span><span class="sxs-lookup"><span data-stu-id="7dad3-258">This means that `1`, `1.0`, `1.0.0`, and `1.0.0.0` are all accepted and equal.</span></span>
3. <span data-ttu-id="7dad3-259">`NuGetVersion` 使用案例 insenstive 預先發行元件的字串比較。</span><span class="sxs-lookup"><span data-stu-id="7dad3-259">`NuGetVersion` uses case insenstive string comparisons for pre-release components.</span></span> <span data-ttu-id="7dad3-260">這表示 `1.0.0-alpha` 和 `1.0.0-Alpha` 相等。</span><span class="sxs-lookup"><span data-stu-id="7dad3-260">This means that `1.0.0-alpha` and `1.0.0-Alpha` are equal.</span></span>
