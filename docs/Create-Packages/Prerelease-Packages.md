---
title: "NuGet 套件中的發行前版本 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df6a366a-22c1-47bb-8017-18231311ce88
description: "建置發行前版本套件的指引"
keywords: "版本控制, NuGet 套件版本控制, NuGet 發行前版本, NuGet 發行前版本套件, 預覽套件版本, RC 套件版本, 搶鮮版 (Beta) 套件版本, NuGet 語意版本控制"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07cb9b9bdeeea6f283e95a11a06d7f2043c9b17c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="8187c-104">建置發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="8187c-104">Building pre-release packages</span></span>

<span data-ttu-id="8187c-105">每當您使用新的版本號碼發行更新的套件時，NuGet 會將它視為「最新的穩定版本」(如範例所示)，例如在 Visual Studio 的套件管理員 UI 中：</span><span class="sxs-lookup"><span data-stu-id="8187c-105">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![顯示最新穩定版本的套件管理員 UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="8187c-107">穩定版本是認為足夠可靠能在生產環境中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="8187c-107">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="8187c-108">最新的穩定版本也是會安裝為套件更新或在套件還原期間安裝的版本 (受[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)中所述的條件約束)。</span><span class="sxs-lookup"><span data-stu-id="8187c-108">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="8187c-109">為支援軟體發行生命週期，NuGet 1.6 和更新版本允許散發發行前套件，它們的版本號碼包含語意版本尾碼，例如 `-alpha`、`-beta` 或 `-rc`。</span><span class="sxs-lookup"><span data-stu-id="8187c-109">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="8187c-110">如需詳細資訊，請參閱[套件版本控制](../reference/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="8187c-110">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="8187c-111">有兩種方式可以指定這類版本：</span><span class="sxs-lookup"><span data-stu-id="8187c-111">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="8187c-112">`.nuspec` 檔案：`version` 項目中包含語意版本尾碼：</span><span class="sxs-lookup"><span data-stu-id="8187c-112">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="8187c-113">組件屬性：從 Visual Studio 專案建置套件時 (`.csproj` 或 `.vbproj`)，使用 `AssemblyInformationalVersionAttribute` 指定版本：</span><span class="sxs-lookup"><span data-stu-id="8187c-113">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="8187c-114">NuGet 會挑選此值，而非不支援語意版本控制的 `AssemblyVersion` 屬性中指定的值。</span><span class="sxs-lookup"><span data-stu-id="8187c-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="8187c-115">當您準備好要發行穩定版本時，只要移除尾碼，套件就會優先於任何發行前版本。</span><span class="sxs-lookup"><span data-stu-id="8187c-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="8187c-116">請再次參考[套件版本控制](../reference/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="8187c-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>


## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="8187c-117">安裝和更新發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="8187c-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="8187c-118">NuGet 使用套件時預設不包含發行前版本，但是您可以如下所示變更此行為：</span><span class="sxs-lookup"><span data-stu-id="8187c-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="8187c-119">**Visual Studio 中的套件管理員 UI**：在 [管理 NuGet 套件] UI 中，核取 [包含發行前版本] 方塊：</span><span class="sxs-lookup"><span data-stu-id="8187c-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio 的 [包含發行前版本] 核取方塊](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="8187c-121">設定或清除此方塊會重新整理套件管理員 UI，以及您可以安裝的可用版本清單。</span><span class="sxs-lookup"><span data-stu-id="8187c-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="8187c-122">**套件管理員主控台**：使用 `-IncludePrerelease` 參數搭配 `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package` 和 `Update-Package` 命令。</span><span class="sxs-lookup"><span data-stu-id="8187c-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="8187c-123">請參閱 [PowerShell 參考](../tools/powershell-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="8187c-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="8187c-124">**NuGet CLI**：使用 `-prerelease` 參數搭配 `install`、`update`、`delete` 和 `mirror` 命令。</span><span class="sxs-lookup"><span data-stu-id="8187c-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="8187c-125">請參閱 [NuGet CLI 參考](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="8187c-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>


## <a name="semantic-versioning"></a><span data-ttu-id="8187c-126">語意版本控制</span><span class="sxs-lookup"><span data-stu-id="8187c-126">Semantic versioning</span></span>

<span data-ttu-id="8187c-127">[語意版本控制或 SemVer 慣例](http://semver.org/spec/v1.0.0.html)描述如何利用版本號碼中的字串傳遞其表示的基礎程式碼。</span><span class="sxs-lookup"><span data-stu-id="8187c-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="8187c-128">在此慣例中，每個版本都有三個部分 `Major.Minor.Patch`，代表意義如下：</span><span class="sxs-lookup"><span data-stu-id="8187c-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="8187c-129">`Major`：重大變更</span><span class="sxs-lookup"><span data-stu-id="8187c-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="8187c-130">`Minor`：新功能，但具回溯相容性</span><span class="sxs-lookup"><span data-stu-id="8187c-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="8187c-131">`Patch`：僅具有回溯相容的 Bug 修正</span><span class="sxs-lookup"><span data-stu-id="8187c-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="8187c-132">然後在發行前版本的修補程式編號後附加連字號和一個字串。</span><span class="sxs-lookup"><span data-stu-id="8187c-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="8187c-133">就技術層面而言，連字號後面可以使用「任何」**字串，NuGet 會將套件視為發行前版本。</span><span class="sxs-lookup"><span data-stu-id="8187c-133">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="8187c-134">然後，NuGet 會在適用的 UI 中顯示完整的版本號碼，讓取用者自行解譯其意義。</span><span class="sxs-lookup"><span data-stu-id="8187c-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="8187c-135">請記住，通常遵循如下所示的可辨識命名慣例會比較好：</span><span class="sxs-lookup"><span data-stu-id="8187c-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="8187c-136">`-alpha`：Alpha 版本，通常用於進行中的工作和實驗</span><span class="sxs-lookup"><span data-stu-id="8187c-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="8187c-137">`-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的 Bug。</span><span class="sxs-lookup"><span data-stu-id="8187c-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="8187c-138">`-rc`：候選版，除非出現重大的 Bug，不然通常是準最終版本 (穩定版)。</span><span class="sxs-lookup"><span data-stu-id="8187c-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="8187c-139">NuGet 不支援 [SemVer 相容 (v2.0.0)](http://semver.org/spec/v2.0.0.html) 發行前版本編號使用點標記法，如同 `1.0.1-build.23`。</span><span class="sxs-lookup"><span data-stu-id="8187c-139">NuGet does not support [SemVer-compatible (v2.0.0)](http://semver.org/spec/v2.0.0.html) prerelease numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="8187c-140">您可以使用 `1.0.1-build23` 的格式，但這一律會視為發行前版本。</span><span class="sxs-lookup"><span data-stu-id="8187c-140">You can use a form like `1.0.1-build23` but this is always considered a pre-release version.</span></span>

<span data-ttu-id="8187c-141">但無論使用什麼樣的尾碼，NuGet 都會以反向字母順序給予它們優先權：</span><span class="sxs-lookup"><span data-stu-id="8187c-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta12
1.0.1-beta05
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
```

<span data-ttu-id="8187c-142">如範例所示，不含任何尾碼的版本一律優先於發行前版本。</span><span class="sxs-lookup"><span data-stu-id="8187c-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="8187c-143">另請注意，如果您使用數值尾碼和可能使用兩位數 (或以上) 數字的發行前版本標籤，請和 beta01 及 beta05 一樣前面加零，以確保數字變大時正確排序。</span><span class="sxs-lookup"><span data-stu-id="8187c-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>