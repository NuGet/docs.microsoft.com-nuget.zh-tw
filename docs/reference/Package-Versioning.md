---
title: NuGet 套件版本參考
description: 有關為 NuGet 套件相依的其他套件指定版本號碼和範圍的確切詳細資料, 以及安裝相依性的方式。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020002"
---
# <a name="package-versioning"></a><span data-ttu-id="5a34c-103">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="5a34c-103">Package versioning</span></span>

<span data-ttu-id="5a34c-104">特定套件一律會使用其套件識別碼和確切的版本號碼來參考。</span><span class="sxs-lookup"><span data-stu-id="5a34c-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="5a34c-105">例如, nuget.org 上的[Entity Framework](https://www.nuget.org/packages/EntityFramework/)有數個特定的套件可用, 範圍從版本*4.1.10311*到版本*之 ef6.1.3* (最新的穩定版本) 和各種發行前版本 (例如*6.2.0-Beta1)* .</span><span class="sxs-lookup"><span data-stu-id="5a34c-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="5a34c-106">建立封裝時, 您可以使用選擇性的發行前文字尾碼來指派特定版本號碼。</span><span class="sxs-lookup"><span data-stu-id="5a34c-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="5a34c-107">另一方面, 使用封裝時, 您可以指定確切的版本號碼或可接受的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="5a34c-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="5a34c-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="5a34c-108">In this topic:</span></span>

- <span data-ttu-id="5a34c-109">[版本基本概念](#version-basics), 包括發行前版本的尾碼。</span><span class="sxs-lookup"><span data-stu-id="5a34c-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="5a34c-110">版本範圍和萬用字元</span><span class="sxs-lookup"><span data-stu-id="5a34c-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="5a34c-111">正規化版本號碼</span><span class="sxs-lookup"><span data-stu-id="5a34c-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="5a34c-112">版本基本概念</span><span class="sxs-lookup"><span data-stu-id="5a34c-112">Version basics</span></span>

<span data-ttu-id="5a34c-113">特定版本號碼的格式為 *[主要. 次要修補程式 [-尾碼]]* , 其中元件具有下列意義:</span><span class="sxs-lookup"><span data-stu-id="5a34c-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="5a34c-114">*主要*:重大變更</span><span class="sxs-lookup"><span data-stu-id="5a34c-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="5a34c-115">*次要*:新功能，但具回溯相容性</span><span class="sxs-lookup"><span data-stu-id="5a34c-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="5a34c-116">*修補程式*:僅具有回溯相容的錯誤 (Bug) 修正</span><span class="sxs-lookup"><span data-stu-id="5a34c-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="5a34c-117">*-尾碼*(選擇性): 連字號後面接著字串, 表示發行前版本 (遵循[語義版本控制或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="5a34c-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="5a34c-118">**典型**</span><span class="sxs-lookup"><span data-stu-id="5a34c-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="5a34c-119">nuget.org 會拒絕任何缺少確切版本號碼的套件上傳。</span><span class="sxs-lookup"><span data-stu-id="5a34c-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="5a34c-120">您必須在用來建立封裝`.nuspec`的或專案檔中指定版本。</span><span class="sxs-lookup"><span data-stu-id="5a34c-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="5a34c-121">發行前版本</span><span class="sxs-lookup"><span data-stu-id="5a34c-121">Pre-release versions</span></span>

<span data-ttu-id="5a34c-122">就技術上而言, 套件建立者可以使用任何字串做為後置詞來表示發行前版本, 因為 NuGet 會將任何此類版本視為預先發行版本, 而且不會進行任何其他轉譯。</span><span class="sxs-lookup"><span data-stu-id="5a34c-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="5a34c-123">也就是說, NuGet 會在牽涉到的任何 UI 中顯示完整的版本字串, 並將後置詞意義的任何解釋, 保留給取用者。</span><span class="sxs-lookup"><span data-stu-id="5a34c-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="5a34c-124">話雖如此, 封裝開發人員通常會遵循公認的命名慣例:</span><span class="sxs-lookup"><span data-stu-id="5a34c-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="5a34c-125">`-alpha`：Alpha 版本, 通常用於進行中的工作和實驗。</span><span class="sxs-lookup"><span data-stu-id="5a34c-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="5a34c-126">`-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的錯誤 (Bug)。</span><span class="sxs-lookup"><span data-stu-id="5a34c-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="5a34c-127">`-rc`：候選版，除非出現重大的錯誤 (Bug)，不然通常是準最終版本 (穩定版)。</span><span class="sxs-lookup"><span data-stu-id="5a34c-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="5a34c-128">NuGet 4.3.0 + 支援[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), 其支援具有點標記法的發行前版本號碼, 如同*1.0.1-build. 23*。</span><span class="sxs-lookup"><span data-stu-id="5a34c-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="5a34c-129">4\.3.0 之前的 NuGet 版本不支援點標記法。</span><span class="sxs-lookup"><span data-stu-id="5a34c-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="5a34c-130">您可以使用像是*1.0.1-build23*的表單。</span><span class="sxs-lookup"><span data-stu-id="5a34c-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="5a34c-131">解析套件參考和多個套件版本只有尾碼不同時, NuGet 會先選擇不含尾碼的版本, 然後再以相反的字母順序套用至發行前版本。</span><span class="sxs-lookup"><span data-stu-id="5a34c-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="5a34c-132">例如, 下列版本會依照所示的正確順序來選擇:</span><span class="sxs-lookup"><span data-stu-id="5a34c-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="5a34c-133">語義版本控制2.0。0</span><span class="sxs-lookup"><span data-stu-id="5a34c-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="5a34c-134">使用 NuGet 4.3.0 + 和 Visual Studio 2017 版本 15.3 +, NuGet 支援[語義版本設定 2.0.0](http://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="5a34c-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="5a34c-135">較舊的用戶端不支援 SemVer v 2.0.0 的某些語義。</span><span class="sxs-lookup"><span data-stu-id="5a34c-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="5a34c-136">如果下列其中一個陳述成立, NuGet 會將套件版本視為 SemVer v 2.0.0 特定:</span><span class="sxs-lookup"><span data-stu-id="5a34c-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="5a34c-137">發行前版本標籤是以點分隔的, 例如*1.0.0-Alpha。 1*</span><span class="sxs-lookup"><span data-stu-id="5a34c-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="5a34c-138">版本具有組建中繼資料, 例如*1.0.0 + githash*</span><span class="sxs-lookup"><span data-stu-id="5a34c-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="5a34c-139">針對 nuget.org, 如果下列其中一個陳述為 true, 則會將套件定義為 SemVer v 2.0.0 套件:</span><span class="sxs-lookup"><span data-stu-id="5a34c-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="5a34c-140">套件本身的版本為 SemVer v 2.0.0 相容, 但不符合 SemVer 1.0.0 版, 如上面所定義。</span><span class="sxs-lookup"><span data-stu-id="5a34c-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="5a34c-141">套件的任何相依性版本範圍都有最小或最大版本, 其為 SemVer v 2.0.0 相容, 但不符合 SemVer 1.0.0 標準, 定義于上方;例如, *[1.0.0-Alpha. 1,)* ]。</span><span class="sxs-lookup"><span data-stu-id="5a34c-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="5a34c-142">如果您將 SemVer v 2.0.0 特定封裝上傳到 nuget.org, 舊版用戶端就看不到套件, 而且只有下列 NuGet 用戶端可以使用:</span><span class="sxs-lookup"><span data-stu-id="5a34c-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="5a34c-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="5a34c-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="5a34c-144">Visual Studio 2017 版本 15.3 +</span><span class="sxs-lookup"><span data-stu-id="5a34c-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="5a34c-145">Visual Studio 2015 搭配[NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="5a34c-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="5a34c-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="5a34c-146">dotnet</span></span>
  - <span data-ttu-id="5a34c-147">dotnetcore .exe (.NET SDK 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="5a34c-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="5a34c-148">協力廠商用戶端:</span><span class="sxs-lookup"><span data-stu-id="5a34c-148">Third-party clients:</span></span>

- <span data-ttu-id="5a34c-149">JetBrains 附件</span><span class="sxs-lookup"><span data-stu-id="5a34c-149">JetBrains Rider</span></span>
- <span data-ttu-id="5a34c-150">Paket 5.0 版 +</span><span class="sxs-lookup"><span data-stu-id="5a34c-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="5a34c-151">版本範圍和萬用字元</span><span class="sxs-lookup"><span data-stu-id="5a34c-151">Version ranges and wildcards</span></span>

<span data-ttu-id="5a34c-152">在參考套件相依性時, NuGet 支援使用間隔標記法來指定版本範圍, 摘要如下:</span><span class="sxs-lookup"><span data-stu-id="5a34c-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="5a34c-153">Notation</span><span class="sxs-lookup"><span data-stu-id="5a34c-153">Notation</span></span> | <span data-ttu-id="5a34c-154">套用的規則</span><span class="sxs-lookup"><span data-stu-id="5a34c-154">Applied rule</span></span> | <span data-ttu-id="5a34c-155">描述</span><span class="sxs-lookup"><span data-stu-id="5a34c-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="5a34c-156">1.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-156">1.0</span></span> | <span data-ttu-id="5a34c-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-157">x ≥ 1.0</span></span> | <span data-ttu-id="5a34c-158">最小版本 (含)</span><span class="sxs-lookup"><span data-stu-id="5a34c-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="5a34c-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="5a34c-159">(1.0,)</span></span> | <span data-ttu-id="5a34c-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-160">x > 1.0</span></span> | <span data-ttu-id="5a34c-161">最低版本, 獨佔</span><span class="sxs-lookup"><span data-stu-id="5a34c-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="5a34c-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="5a34c-162">[1.0]</span></span> | <span data-ttu-id="5a34c-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-163">x == 1.0</span></span> | <span data-ttu-id="5a34c-164">完全相符的版本</span><span class="sxs-lookup"><span data-stu-id="5a34c-164">Exact version match</span></span> |
| <span data-ttu-id="5a34c-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="5a34c-165">(,1.0]</span></span> | <span data-ttu-id="5a34c-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-166">x ≤ 1.0</span></span> | <span data-ttu-id="5a34c-167">最大版本 (含)</span><span class="sxs-lookup"><span data-stu-id="5a34c-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="5a34c-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="5a34c-168">(,1.0)</span></span> | <span data-ttu-id="5a34c-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-169">x < 1.0</span></span> | <span data-ttu-id="5a34c-170">最大版本, 獨佔</span><span class="sxs-lookup"><span data-stu-id="5a34c-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="5a34c-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="5a34c-171">[1.0,2.0]</span></span> | <span data-ttu-id="5a34c-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="5a34c-173">確切範圍 (含)</span><span class="sxs-lookup"><span data-stu-id="5a34c-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="5a34c-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="5a34c-174">(1.0,2.0)</span></span> | <span data-ttu-id="5a34c-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="5a34c-176">精確範圍, 獨佔</span><span class="sxs-lookup"><span data-stu-id="5a34c-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="5a34c-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="5a34c-177">[1.0,2.0)</span></span> | <span data-ttu-id="5a34c-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="5a34c-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="5a34c-179">混合內含的最小和最大排除版本</span><span class="sxs-lookup"><span data-stu-id="5a34c-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="5a34c-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="5a34c-180">(1.0)</span></span>    | <span data-ttu-id="5a34c-181">無效</span><span class="sxs-lookup"><span data-stu-id="5a34c-181">invalid</span></span> | <span data-ttu-id="5a34c-182">無效</span><span class="sxs-lookup"><span data-stu-id="5a34c-182">invalid</span></span> |

<span data-ttu-id="5a34c-183">使用 PackageReference 格式時, NuGet 也支援使用萬用字元標記法, \*用於數位的主要、次要、修補和預先發行尾碼部分。</span><span class="sxs-lookup"><span data-stu-id="5a34c-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="5a34c-184">`packages.config`格式不支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="5a34c-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="5a34c-185">PackageReference 中的版本範圍包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="5a34c-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="5a34c-186">根據設計, 浮動版本不會解析發行前版本, 除非加入宣告。</span><span class="sxs-lookup"><span data-stu-id="5a34c-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="5a34c-187">如需相關功能要求的狀態, 請參閱[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)。</span><span class="sxs-lookup"><span data-stu-id="5a34c-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="5a34c-188">範例</span><span class="sxs-lookup"><span data-stu-id="5a34c-188">Examples</span></span>

<span data-ttu-id="5a34c-189">請一律針對專案檔、 `packages.config`檔案和`.nuspec`檔案中的封裝相依性指定版本或版本範圍。</span><span class="sxs-lookup"><span data-stu-id="5a34c-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="5a34c-190">如果沒有版本或版本範圍, NuGet 2.8. x 和更早的版本會在解析相依性時選擇最新可用的套件版本, 而 NuGet 3.x 和更新版本會選擇最低的套件版本。</span><span class="sxs-lookup"><span data-stu-id="5a34c-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="5a34c-191">指定版本或版本範圍可避免這種不確定性。</span><span class="sxs-lookup"><span data-stu-id="5a34c-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="5a34c-192">專案檔中的參考 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="5a34c-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="5a34c-193">**中的`packages.config`參考:**</span><span class="sxs-lookup"><span data-stu-id="5a34c-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="5a34c-194">在`packages.config`中, 每個相依性都會與`version`還原套件時使用的確切屬性一併列出。</span><span class="sxs-lookup"><span data-stu-id="5a34c-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="5a34c-195">只有在更新作業期間, 才會使用屬性來限制封裝可能更新的版本。`allowedVersions`</span><span class="sxs-lookup"><span data-stu-id="5a34c-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="5a34c-196">**檔案中`.nuspec`的參考**</span><span class="sxs-lookup"><span data-stu-id="5a34c-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="5a34c-197">元素中的`version`屬性會描述相依性可接受的範圍版本。 `<dependency>`</span><span class="sxs-lookup"><span data-stu-id="5a34c-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="5a34c-198">正規化版本號碼</span><span class="sxs-lookup"><span data-stu-id="5a34c-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="5a34c-199">這是 NuGet 3.4 和更新版本的重大變更。</span><span class="sxs-lookup"><span data-stu-id="5a34c-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="5a34c-200">在安裝、重新安裝或還原作業期間從存放庫取得套件時, NuGet 3.4 + 會依照下列方式來對待版本號碼:</span><span class="sxs-lookup"><span data-stu-id="5a34c-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="5a34c-201">開頭的零會從版本號碼中移除:</span><span class="sxs-lookup"><span data-stu-id="5a34c-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="5a34c-202">在版本號碼的第四個部分中, 會省略零</span><span class="sxs-lookup"><span data-stu-id="5a34c-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="5a34c-203">`pack`和`restore`作業會盡可能將版本正規化。</span><span class="sxs-lookup"><span data-stu-id="5a34c-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="5a34c-204">針對已建立的封裝, 此正規化不會影響封裝本身的版本號碼;它只會影響 NuGet 在解析相依性時如何符合版本。</span><span class="sxs-lookup"><span data-stu-id="5a34c-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="5a34c-205">不過, NuGet 套件存放庫必須以與 NuGet 相同的方式來處理這些值, 以防止封裝版本重複。</span><span class="sxs-lookup"><span data-stu-id="5a34c-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="5a34c-206">因此, 包含*1.0*版套件的存放庫, 也不應該將*1.0.0*版裝載為不同的套件。</span><span class="sxs-lookup"><span data-stu-id="5a34c-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
