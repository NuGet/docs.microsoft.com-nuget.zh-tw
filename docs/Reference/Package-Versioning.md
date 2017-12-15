---
title: "NuGet 封裝版本參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "確切的指定版本號碼和範圍而定的 NuGet 封裝，並安裝相依性的方式在其他封裝的詳細資訊。"
keywords: "版本控制、 NuGet 封裝相依性、 NuGet 相依性版本、 NuGet 版本號碼、 NuGet 封裝版本、 版本範圍、 版本規格，正規化的版本號碼"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25b74ab629cab0fff7114bf1621606de5fc18dd2
ms.sourcegitcommit: 89bb9d429c19ff69084c35acad09daea3e16d56b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="package-versioning"></a><span data-ttu-id="3c7e4-104">封裝版本控制</span><span class="sxs-lookup"><span data-stu-id="3c7e4-104">Package versioning</span></span>

<span data-ttu-id="3c7e4-105">特定封裝永遠被指使用其封裝識別碼和確切的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="3c7e4-106">例如， [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org 上有數個數十種特定封裝可用，範圍從版本*4.1.10311*版本*6.1.3* （最新穩定發行） 和各種不同的發行前版本*6.2.0-beta1*。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="3c7e4-107">在建立封裝時，您會指定特定版本號碼的選擇性發行前的文字尾碼。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="3c7e4-108">當使用封裝，相反地，您可以指定確切的版本號碼或一個範圍的可接受的版本。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="3c7e4-109">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-109">In this topic:</span></span>

- <span data-ttu-id="3c7e4-110">[版本的基本概念](#version-basics)包括發行前版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="3c7e4-111">版本範圍與萬用字元</span><span class="sxs-lookup"><span data-stu-id="3c7e4-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="3c7e4-112">正規化的版本號碼</span><span class="sxs-lookup"><span data-stu-id="3c7e4-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="3c7e4-113">版本的基本概念</span><span class="sxs-lookup"><span data-stu-id="3c7e4-113">Version basics</span></span>

<span data-ttu-id="3c7e4-114">特定版本號碼的格式為*Major.Minor.Patch [-後置詞]*、 其中的元件具有以下意義：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="3c7e4-115">*主要*： 重大變更</span><span class="sxs-lookup"><span data-stu-id="3c7e4-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="3c7e4-116">*次要*： 新的功能，但回溯相容性</span><span class="sxs-lookup"><span data-stu-id="3c7e4-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="3c7e4-117">*修補程式*： 只有具備回溯相容性 bug 修正</span><span class="sxs-lookup"><span data-stu-id="3c7e4-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="3c7e4-118">*-尾碼*（選擇性）： 連字號後面接著此項表示應發行前版本字串 (下列[語意化版本控制或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="3c7e4-119">**範例：**</span><span class="sxs-lookup"><span data-stu-id="3c7e4-119">**Examples:**</span></span>
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="3c7e4-120">nuget.org 會拒絕任何缺少的確切的版本號碼的封裝上傳。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="3c7e4-121">必須在指定的版本`.nuspec`或用來建立封裝的專案檔。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="3c7e4-122">發行前版本</span><span class="sxs-lookup"><span data-stu-id="3c7e4-122">Pre-release versions</span></span>

<span data-ttu-id="3c7e4-123">就技術上來說，封裝建立者可以使用任何字串做為尾碼來代表發行前版本，如 NuGet 視為發行前版本的任何這類的版本，並讓其他的解譯方式。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="3c7e4-124">也就是說，NuGet 會顯示任何 UI 中的完整版本字串涉及時，取用者留下任何解譯的後置詞的意義。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="3c7e4-125">話雖如此，封裝開發人員通常會依照可辨識的命名慣例：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="3c7e4-126">`-alpha`: Alpha 版本中，通常用於工作的進度和試驗。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="3c7e4-127">`-beta`: Beta 版本，通常是已規劃的版本中，接下來的完整功能，但是可能會包含已知的錯誤的其中一個。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="3c7e4-128">`-rc`： 發行候選版本，通常是最後一個潛在的版次 (stable) 除非重大的 bug 會出現。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="3c7e4-129">NuGet 4.3.0+ 支援[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，可支援使用點標記法，發行前版本號碼中*1.0.1-build.23*。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="3c7e4-130">與之前 4.3.0 的 NuGet 版本不支援點標記法。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="3c7e4-131">您可以使用的表單*1.0.1-build23*。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="3c7e4-132">解決時封裝會參照和多個封裝版本只有不同後置詞，NuGet 首先，選擇的版本不含尾碼，然後套用至發行前版本，以反向字母順序的優先順序。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="3c7e4-133">例如，下列版本本來的順序顯示：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-133">For example, the following versions would be chosen in the exact order shown:</span></span>

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

## <a name="semantic-versioning-200"></a><span data-ttu-id="3c7e4-134">2.0.0 的語意版本設定</span><span class="sxs-lookup"><span data-stu-id="3c7e4-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="3c7e4-135">使用 NuGet 4.3.0+ 和 Visual Studio 2017 15.3 + 版本，支援 NuGet[語意版本設定 2.0.0](http://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="3c7e4-136">在舊版的用戶端不支援的 SemVer v2.0.0 特定語意。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="3c7e4-137">NuGet 會考慮下列陳述式是否是 SemVer v2.0.0 特定的封裝版本：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="3c7e4-138">發行前版本標籤是點分隔，例如*1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="3c7e4-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="3c7e4-139">版本有建置中繼資料，例如*1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="3c7e4-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="3c7e4-140">對於 nuget.org，封裝定義為 SemVer v2.0.0 封裝如果為 true，下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="3c7e4-141">封裝自己版本是 SemVer v2.0.0 相容，但相容、 不 SemVer v1.0.0 上方所定義。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="3c7e4-142">所有封裝的相依性版本範圍有不相容 SemVer v2.0.0 但相容、 不 SemVer v1.0.0; 上述定義的最小值或最大版本例如， *[1.0.0-alpha.1,)*。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="3c7e4-143">如果您要 nuget.org 傳 SemVer v2.0.0 特定封裝，封裝是看不到舊版的用戶端，並可供 只有下列 NuGet 用戶端：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="3c7e4-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="3c7e4-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="3c7e4-145">Visual Studio 2017 15.3 + 版本</span><span class="sxs-lookup"><span data-stu-id="3c7e4-145">Visual Studio 2017 version 15.3+</span></span> 
- <span data-ttu-id="3c7e4-146">dotnet.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="3c7e4-146">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="3c7e4-147">第三方用戶端：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-147">Third-party clients:</span></span>

- <span data-ttu-id="3c7e4-148">JetBrains 騎兵</span><span class="sxs-lookup"><span data-stu-id="3c7e4-148">JetBrains Rider</span></span>
- <span data-ttu-id="3c7e4-149">Paket 5.0 + 版本</span><span class="sxs-lookup"><span data-stu-id="3c7e4-149">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="3c7e4-150">版本範圍與萬用字元</span><span class="sxs-lookup"><span data-stu-id="3c7e4-150">Version ranges and wildcards</span></span>

<span data-ttu-id="3c7e4-151">當參照的套件相依性，NuGet 會支援使用間隔標記法來指定版本範圍，彙總，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-151">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="3c7e4-152">Notation</span><span class="sxs-lookup"><span data-stu-id="3c7e4-152">Notation</span></span> | <span data-ttu-id="3c7e4-153">套用的規則</span><span class="sxs-lookup"><span data-stu-id="3c7e4-153">Applied rule</span></span> | <span data-ttu-id="3c7e4-154">說明</span><span class="sxs-lookup"><span data-stu-id="3c7e4-154">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="3c7e4-155">1.0</span><span class="sxs-lookup"><span data-stu-id="3c7e4-155">1.0</span></span> | <span data-ttu-id="3c7e4-156">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="3c7e4-156">1.0 ≤ x</span></span> | <span data-ttu-id="3c7e4-157">最小版本 （含）</span><span class="sxs-lookup"><span data-stu-id="3c7e4-157">Minimum version, inclusive</span></span> |
| <span data-ttu-id="3c7e4-158">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="3c7e4-158">(1.0,)</span></span> | <span data-ttu-id="3c7e4-159">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="3c7e4-159">1.0 < x</span></span> | <span data-ttu-id="3c7e4-160">最小版本，而獨佔式</span><span class="sxs-lookup"><span data-stu-id="3c7e4-160">Minimum version, exclusive</span></span> |
| <span data-ttu-id="3c7e4-161">[1.0]</span><span class="sxs-lookup"><span data-stu-id="3c7e4-161">[1.0]</span></span> | <span data-ttu-id="3c7e4-162">x = = 1.0</span><span class="sxs-lookup"><span data-stu-id="3c7e4-162">x == 1.0</span></span> | <span data-ttu-id="3c7e4-163">確切的版本相符項目</span><span class="sxs-lookup"><span data-stu-id="3c7e4-163">Exact version match</span></span> |
| <span data-ttu-id="3c7e4-164">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="3c7e4-164">(,1.0]</span></span> | <span data-ttu-id="3c7e4-165">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="3c7e4-165">x ≤ 1.0</span></span> | <span data-ttu-id="3c7e4-166">最大版本，（含）</span><span class="sxs-lookup"><span data-stu-id="3c7e4-166">Maximum version, inclusive</span></span> |
| <span data-ttu-id="3c7e4-167">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="3c7e4-167">(,1.0)</span></span> | <span data-ttu-id="3c7e4-168">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="3c7e4-168">x < 1.0</span></span> | <span data-ttu-id="3c7e4-169">最大版本，而獨佔式</span><span class="sxs-lookup"><span data-stu-id="3c7e4-169">Maximum version, exclusive</span></span> |
| <span data-ttu-id="3c7e4-170">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="3c7e4-170">[1.0,2.0]</span></span> | <span data-ttu-id="3c7e4-171">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="3c7e4-171">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="3c7e4-172">確切的範圍內含</span><span class="sxs-lookup"><span data-stu-id="3c7e4-172">Exact range, inclusive</span></span> |
| <span data-ttu-id="3c7e4-173">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="3c7e4-173">(1.0,2.0)</span></span> | <span data-ttu-id="3c7e4-174">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="3c7e4-174">1.0 < x < 2.0</span></span> | <span data-ttu-id="3c7e4-175">確切的範圍，獨占</span><span class="sxs-lookup"><span data-stu-id="3c7e4-175">Exact range, exclusive</span></span> |
| <span data-ttu-id="3c7e4-176">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="3c7e4-176">[1.0,2.0)</span></span> | <span data-ttu-id="3c7e4-177">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="3c7e4-177">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="3c7e4-178">混合含最小值和獨佔式最大版本</span><span class="sxs-lookup"><span data-stu-id="3c7e4-178">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="3c7e4-179">(1.0)</span><span class="sxs-lookup"><span data-stu-id="3c7e4-179">(1.0)</span></span>    | <span data-ttu-id="3c7e4-180">無效</span><span class="sxs-lookup"><span data-stu-id="3c7e4-180">invalid</span></span> | <span data-ttu-id="3c7e4-181">無效</span><span class="sxs-lookup"><span data-stu-id="3c7e4-181">invalid</span></span> |

<span data-ttu-id="3c7e4-182">當使用 PackageReference 或`project.json`封裝也支援使用萬用字元標記法參考格式，NuGet \*、 主要、 次要、 修補程式，和數字的發行前版本後置字元部分。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-182">When using the PackageReference or `project.json` package reference formats, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="3c7e4-183">不支援萬用字元`packages.config`格式。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-183">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="3c7e4-184">解決版本範圍時，不會包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-184">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="3c7e4-185">發行前版本*是*包含時使用萬用字元 (\*)。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-185">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="3c7e4-186">版本範圍*[1.0,2.0]*，比方說，不包括 2.0 beta 版，但萬用字元標記法_2.0-*_沒有。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-186">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-*_ does.</span></span> <span data-ttu-id="3c7e4-187">請參閱[發出 912](https://github.com/NuGet/Home/issues/912)的進一步討論發行前版本萬用字元。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-187">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="3c7e4-188">範例</span><span class="sxs-lookup"><span data-stu-id="3c7e4-188">Examples</span></span>

<span data-ttu-id="3c7e4-189">一律在專案檔中指定版本或封裝的相依性的版本範圍`packages.config`檔案，並`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="3c7e4-190">不含版本或版本範圍，NuGet 2.8.x 稍早選擇最新可用的封裝版本時解析相依性，而 NuGet 3.x 及更新版本選擇最低的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="3c7e4-191">指定的版本或版本範圍可避免此有助於減少不確定性。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="3c7e4-192">專案檔 (PackageReference) 中的參考</span><span class="sxs-lookup"><span data-stu-id="3c7e4-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="3c7e4-193">**在參考`packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="3c7e4-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="3c7e4-194">在`packages.config`，每個相依性列為完全`version`還原封裝時所使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="3c7e4-195">`allowedVersions`屬性只有在更新作業期間用來限制可能會更新封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="3c7e4-196">**在參考`.nuspec`檔案**</span><span class="sxs-lookup"><span data-stu-id="3c7e4-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="3c7e4-197">`version`屬性`<dependency>`元素描述可接受的相依性範圍版本。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="3c7e4-198">正規化的版本號碼</span><span class="sxs-lookup"><span data-stu-id="3c7e4-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="3c7e4-199">這是一項重大變更及更新版本的 NuGet 3.4。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="3c7e4-200">取得從儲存機制的封裝，在安裝期間，重新安裝，或還原作業，NuGet 3.4 + 會將版本號碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="3c7e4-201">前置的零會從版本號碼：</span><span class="sxs-lookup"><span data-stu-id="3c7e4-201">Leading zeroes are removed from version numbers:</span></span>

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- <span data-ttu-id="3c7e4-202">版本號碼的第四個部分中的零，則會予以忽略</span><span class="sxs-lookup"><span data-stu-id="3c7e4-202">A zero in the fourth part of the version number will be omitted</span></span>

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

<span data-ttu-id="3c7e4-203">這個正規化不會影響封裝本身; 中的版本號碼它會影響只如何 NuGet 符合版本解析相依性時。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-203">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="3c7e4-204">不過，NuGet 封裝儲存機制必須與 NuGet 來避免封裝版本重複相同的方式處理這些值。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-204">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="3c7e4-205">因此，包含版本的儲存機制*1.0*的封裝不應也裝載版本*1.0.0*個別且不同的套件。</span><span class="sxs-lookup"><span data-stu-id="3c7e4-205">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
