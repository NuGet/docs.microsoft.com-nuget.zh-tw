---
title: NuGet 套件版本參考
description: 為 NuGet 套件相依的其他套件指定版本號碼和範圍，以及相依性安裝方式的確切詳細資料。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520348"
---
# <a name="package-versioning"></a><span data-ttu-id="31be2-103">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="31be2-103">Package versioning</span></span>

<span data-ttu-id="31be2-104">您一律必須使用套件的套件識別碼與確切版本號碼來參考特定套件。</span><span class="sxs-lookup"><span data-stu-id="31be2-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="31be2-105">例如，nuget.org 上的 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) \(英文\) 有數十個特定套件可用，範圍從 *4.1.10311* 版到 *6.1.3* 版 (最新穩定版本) 與各種發行前版本 (像是 *6.2.0-beta1*)。</span><span class="sxs-lookup"><span data-stu-id="31be2-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="31be2-106">在建立套件時，您可以搭配選擇性的發行前版本文字尾碼來指派特定版本號碼。</span><span class="sxs-lookup"><span data-stu-id="31be2-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="31be2-107">另一方面，在取用套件時，您可以指定確切版本號碼或可接受的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="31be2-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="31be2-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="31be2-108">In this topic:</span></span>

- <span data-ttu-id="31be2-109">[版本基本概念](#version-basics)包含發行前版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="31be2-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="31be2-110">版本範圍和萬用字元</span><span class="sxs-lookup"><span data-stu-id="31be2-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="31be2-111">標準化版本號碼</span><span class="sxs-lookup"><span data-stu-id="31be2-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="31be2-112">版本基本概念</span><span class="sxs-lookup"><span data-stu-id="31be2-112">Version basics</span></span>

<span data-ttu-id="31be2-113">特定版本號碼的格式為「主要.次要.修補程式[-尾碼]」  ，其中的元件具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="31be2-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="31be2-114">主要  ：重大變更</span><span class="sxs-lookup"><span data-stu-id="31be2-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="31be2-115">次要  ：新功能，但具回溯相容性</span><span class="sxs-lookup"><span data-stu-id="31be2-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="31be2-116">修補程式  ：僅具有回溯相容的錯誤 (Bug) 修正</span><span class="sxs-lookup"><span data-stu-id="31be2-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="31be2-117">「-尾碼」  (選擇性)：後面接著字串的連字號，表示發行前版本 (遵循[語意化版本控制系統或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="31be2-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="31be2-118">**範例：**</span><span class="sxs-lookup"><span data-stu-id="31be2-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="31be2-119">nuget.org 會拒絕任何缺少確切版本號碼的套件上傳。</span><span class="sxs-lookup"><span data-stu-id="31be2-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="31be2-120">您必須在 `.nuspec` 中，或在用來建立套件的專案檔中指定版本。</span><span class="sxs-lookup"><span data-stu-id="31be2-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="31be2-121">發行前版本</span><span class="sxs-lookup"><span data-stu-id="31be2-121">Pre-release versions</span></span>

<span data-ttu-id="31be2-122">就技術上而言，套件建立者可以使用任何字串作為尾碼來表示發行前版本，因為 NuGet 會將任何此類版本視為發行前版本，而且不會進行任何其他解讀。</span><span class="sxs-lookup"><span data-stu-id="31be2-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="31be2-123">也就是說，NuGet 會在牽涉到的任何 UI 中顯示完整版本字串，尾碼之意義的任何解讀，都保留給取用者。</span><span class="sxs-lookup"><span data-stu-id="31be2-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="31be2-124">話雖如此，套件開發人員通常會遵循公認的命名慣例：</span><span class="sxs-lookup"><span data-stu-id="31be2-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="31be2-125">`-alpha`：Alpha 版本，通常用於進行中的工作和實驗。</span><span class="sxs-lookup"><span data-stu-id="31be2-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="31be2-126">`-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的錯誤 (Bug)。</span><span class="sxs-lookup"><span data-stu-id="31be2-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="31be2-127">`-rc`：候選版，除非出現重大的錯誤 (Bug)，不然通常是準最終版本 (穩定版)。</span><span class="sxs-lookup"><span data-stu-id="31be2-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="31be2-128">NuGet 4.3.0+ 支援 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，它支援使用點標記法的發行前版本號碼，如 *1.0.1-build.23*。</span><span class="sxs-lookup"><span data-stu-id="31be2-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="31be2-129">4\.3.0 之前的 NuGet 版本不支援點標記法。</span><span class="sxs-lookup"><span data-stu-id="31be2-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="31be2-130">您可以使用像 *1.0.1-build23* 的格式。</span><span class="sxs-lookup"><span data-stu-id="31be2-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="31be2-131">解析套件參考且多個套件版本只有尾碼不同時，NuGet 會先選擇不含尾碼的版本，然後再依相反字母順序套用發行前版本。</span><span class="sxs-lookup"><span data-stu-id="31be2-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="31be2-132">例如，系統會依照所示的順序選擇下列版本：</span><span class="sxs-lookup"><span data-stu-id="31be2-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="31be2-133">語意化版本控制系統 2.0.0</span><span class="sxs-lookup"><span data-stu-id="31be2-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="31be2-134">使用 NuGet 4.3.0+ 與 Visual Studio 2017 15.3+ 版，NuGet 支援[語意化版本控制系統 2.0.0](http://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="31be2-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="31be2-135">較舊的用戶端不支援 SemVer v2.0.0 的某些語意。</span><span class="sxs-lookup"><span data-stu-id="31be2-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="31be2-136">如果下列其中一個敘述成立，則 NuGet 會將套件版本視為 SemVer v2.0.0 特定：</span><span class="sxs-lookup"><span data-stu-id="31be2-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="31be2-137">發行前版本標籤是以點分隔的，例如 *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="31be2-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="31be2-138">版本有組建中繼資料，例如 *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="31be2-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="31be2-139">針對 nuget.org，如果下列其中一個敘述立，則會將套件定義為 SemVer v2.0.0 套件：</span><span class="sxs-lookup"><span data-stu-id="31be2-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="31be2-140">套件本身的版本符合 SemVer v2.0.0 的規範，但不符合 SemVer v1.0.0 的規範，如上面所定義。</span><span class="sxs-lookup"><span data-stu-id="31be2-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="31be2-141">套件的任何相依性版本範圍都有最小或最大版本，它們符合 SemVer v2.0.0 的規範，但不符合 SemVer v1.0.0 規範，如上面所定義；例如， *[1.0.0-alpha.1, )* 。</span><span class="sxs-lookup"><span data-stu-id="31be2-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="31be2-142">如果您將 SemVer v2.0.0 特定套件上傳到 nuget.org，則舊版用戶端看不到該套件，只有下列 NuGet 用戶端可以取得該套件：</span><span class="sxs-lookup"><span data-stu-id="31be2-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="31be2-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="31be2-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="31be2-144">Visual Studio 2017 15.3+ 版</span><span class="sxs-lookup"><span data-stu-id="31be2-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="31be2-145">Visual Studio 2015 (含 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix))</span><span class="sxs-lookup"><span data-stu-id="31be2-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="31be2-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="31be2-146">dotnet</span></span>
  - <span data-ttu-id="31be2-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="31be2-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="31be2-148">協力廠商用戶端：</span><span class="sxs-lookup"><span data-stu-id="31be2-148">Third-party clients:</span></span>

- <span data-ttu-id="31be2-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="31be2-149">JetBrains Rider</span></span>
- <span data-ttu-id="31be2-150">Paket 5.0+ 版</span><span class="sxs-lookup"><span data-stu-id="31be2-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="31be2-151">版本範圍和萬用字元</span><span class="sxs-lookup"><span data-stu-id="31be2-151">Version ranges and wildcards</span></span>

<span data-ttu-id="31be2-152">在參考套件相依性時，NuGet 支援使用間隔標記法來指定版本範圍，摘要說明如下：</span><span class="sxs-lookup"><span data-stu-id="31be2-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="31be2-153">標記法</span><span class="sxs-lookup"><span data-stu-id="31be2-153">Notation</span></span> | <span data-ttu-id="31be2-154">套用的規則</span><span class="sxs-lookup"><span data-stu-id="31be2-154">Applied rule</span></span> | <span data-ttu-id="31be2-155">描述說明</span><span class="sxs-lookup"><span data-stu-id="31be2-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="31be2-156">1.0</span><span class="sxs-lookup"><span data-stu-id="31be2-156">1.0</span></span> | <span data-ttu-id="31be2-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="31be2-157">x ≥ 1.0</span></span> | <span data-ttu-id="31be2-158">最小版本 (包含)</span><span class="sxs-lookup"><span data-stu-id="31be2-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="31be2-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="31be2-159">(1.0,)</span></span> | <span data-ttu-id="31be2-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="31be2-160">x > 1.0</span></span> | <span data-ttu-id="31be2-161">最小版本 (不包含)</span><span class="sxs-lookup"><span data-stu-id="31be2-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="31be2-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="31be2-162">[1.0]</span></span> | <span data-ttu-id="31be2-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="31be2-163">x == 1.0</span></span> | <span data-ttu-id="31be2-164">完全相符的版本</span><span class="sxs-lookup"><span data-stu-id="31be2-164">Exact version match</span></span> |
| <span data-ttu-id="31be2-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="31be2-165">(,1.0]</span></span> | <span data-ttu-id="31be2-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="31be2-166">x ≤ 1.0</span></span> | <span data-ttu-id="31be2-167">最大版本 (包含)</span><span class="sxs-lookup"><span data-stu-id="31be2-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="31be2-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="31be2-168">(,1.0)</span></span> | <span data-ttu-id="31be2-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="31be2-169">x < 1.0</span></span> | <span data-ttu-id="31be2-170">最大版本 (不包含)</span><span class="sxs-lookup"><span data-stu-id="31be2-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="31be2-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="31be2-171">[1.0,2.0]</span></span> | <span data-ttu-id="31be2-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="31be2-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="31be2-173">完全相符的範圍 (包含)</span><span class="sxs-lookup"><span data-stu-id="31be2-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="31be2-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="31be2-174">(1.0,2.0)</span></span> | <span data-ttu-id="31be2-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="31be2-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="31be2-176">完全相符的範圍 (不包含)</span><span class="sxs-lookup"><span data-stu-id="31be2-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="31be2-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="31be2-177">[1.0,2.0)</span></span> | <span data-ttu-id="31be2-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="31be2-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="31be2-179">混合包含最小且不包含最大版本</span><span class="sxs-lookup"><span data-stu-id="31be2-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="31be2-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="31be2-180">(1.0)</span></span>    | <span data-ttu-id="31be2-181">無效</span><span class="sxs-lookup"><span data-stu-id="31be2-181">invalid</span></span> | <span data-ttu-id="31be2-182">無效</span><span class="sxs-lookup"><span data-stu-id="31be2-182">invalid</span></span> |

<span data-ttu-id="31be2-183">當使用 PackageReference 格式時，針對編號的主要、次要、修補與發行前版本後置詞部分，NuGet 也支援使用萬用字元標記法 (\*)。</span><span class="sxs-lookup"><span data-stu-id="31be2-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="31be2-184">`packages.config` 格式不支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="31be2-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="31be2-185">PackageReference 中的版本範圍包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="31be2-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="31be2-186">根據設計，浮動版本不會解析發行前版本，除非選擇加入。</span><span class="sxs-lookup"><span data-stu-id="31be2-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="31be2-187">如需相關功能要求的狀態，請參閱[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="31be2-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="31be2-188">範例</span><span class="sxs-lookup"><span data-stu-id="31be2-188">Examples</span></span>

<span data-ttu-id="31be2-189">請一律針對專案檔、`packages.config` 檔案與 `.nuspec` 檔案中的套件相依性指定版本或版本範圍。</span><span class="sxs-lookup"><span data-stu-id="31be2-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="31be2-190">如果沒有版本或版本範圍，NuGet 2.8. x 和更早的版本會在解析相依性時選擇最新可用套件版本，而 NuGet 3.x 和更新版本會選擇最低套件版本。</span><span class="sxs-lookup"><span data-stu-id="31be2-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="31be2-191">指定版本或版本範圍可避免這種不確定性。</span><span class="sxs-lookup"><span data-stu-id="31be2-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="31be2-192">專案檔中的參考 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="31be2-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="31be2-193">**`packages.config` 中的參考：**</span><span class="sxs-lookup"><span data-stu-id="31be2-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="31be2-194">在 `packages.config` 中，每個相依性都會隨還原套件時使用的確切 `version` 屬性一併列出。</span><span class="sxs-lookup"><span data-stu-id="31be2-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="31be2-195">只有在更新作業期間，才會使用 `allowedVersions` 屬性來限制套件可能更新的版本。</span><span class="sxs-lookup"><span data-stu-id="31be2-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="31be2-196">**`.nuspec` 檔案中的參考**</span><span class="sxs-lookup"><span data-stu-id="31be2-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="31be2-197">`<dependency>` 元素中的 `version` 屬性描述相依性可接受的範圍版本。</span><span class="sxs-lookup"><span data-stu-id="31be2-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="31be2-198">標準化版本號碼</span><span class="sxs-lookup"><span data-stu-id="31be2-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="31be2-199">這是 NuGet 3.4 和更新版本的中斷性變更。</span><span class="sxs-lookup"><span data-stu-id="31be2-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="31be2-200">在安裝、重新安裝或還原作業期間從存放庫取得套件時，NuGet 3.4+ 會依照下列方式來對待版本號碼：</span><span class="sxs-lookup"><span data-stu-id="31be2-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="31be2-201">系統會將前置零從版本號碼移除：</span><span class="sxs-lookup"><span data-stu-id="31be2-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="31be2-202">系統會移除在版本號碼第四部分中的零</span><span class="sxs-lookup"><span data-stu-id="31be2-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="31be2-203">`pack` 與 `restore` 作業會盡可能將版本標準化。</span><span class="sxs-lookup"><span data-stu-id="31be2-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="31be2-204">針對已建置的套件，此標準化不會影響套件本身的版本號碼；它只會影響 NuGet 在解析相依性時如何比對版本。</span><span class="sxs-lookup"><span data-stu-id="31be2-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="31be2-205">不過，NuGet 套件存放庫必須以與 NuGet 相同的方式來處理這些值，以防止套件版本重複。</span><span class="sxs-lookup"><span data-stu-id="31be2-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="31be2-206">因此，包含 *1.0* 版套件的存放庫，不應該也裝載 *1.0.0* 版，並作為個別且不同的套件。</span><span class="sxs-lookup"><span data-stu-id="31be2-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
