---
title: NuGet 套件中的發行前版本
description: 建置發行前版本套件的指引
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 845f0ea84bcb92fedf9e5f4fb2b1deee1462a004
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610492"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="2f0d9-103">建置發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="2f0d9-103">Building pre-release packages</span></span>

<span data-ttu-id="2f0d9-104">每當您使用新的版本號碼發行更新的套件時，NuGet 會將它視為「最新的穩定版本」(如範例所示)，例如在 Visual Studio 的套件管理員 UI 中：</span><span class="sxs-lookup"><span data-stu-id="2f0d9-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![顯示最新穩定版本的套件管理員 UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="2f0d9-106">穩定版本是認為足夠可靠能在生產環境中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="2f0d9-107">最新的穩定版本也是會安裝為套件更新或在套件還原期間安裝的版本 (受[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)中所述的條件約束)。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="2f0d9-108">為支援軟體發行生命週期，NuGet 1.6 和更新版本允許散發發行前套件，它們的版本號碼包含語意版本尾碼，例如 `-alpha`、`-beta` 或 `-rc`。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="2f0d9-109">如需詳細資訊，請參閱[套件版本控制](../reference/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="2f0d9-110">您可以使用下列其中一種方式指定此版本：</span><span class="sxs-lookup"><span data-stu-id="2f0d9-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="2f0d9-111">**若您的專案使用 [`PackageReference`](../consume-packages/package-references-in-project-files.md)**：在 `.csproj` 檔案的 [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) 元素中包括語意版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="2f0d9-112">**若您的專案有 [`packages.config`](../reference/packages-config.md)** 檔案：在 [`.nuspec`](../reference/nuspec.md)[ 檔案的 `version`](../reference/nuspec.md#version) 元素中包括語意版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="2f0d9-113">當您準備好要發行穩定版本時，只要移除尾碼，套件就會優先於任何發行前版本。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="2f0d9-114">請再次參考[套件版本控制](../reference/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-114">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="2f0d9-115">安裝和更新發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="2f0d9-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="2f0d9-116">NuGet 使用套件時預設不包含發行前版本，但是您可以如下所示變更此行為：</span><span class="sxs-lookup"><span data-stu-id="2f0d9-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="2f0d9-117">**Visual Studio 中的套件管理員 UI**：在 [管理 NuGet 套件] UI 中，選取 [包含發行前版本] 方塊：</span><span class="sxs-lookup"><span data-stu-id="2f0d9-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio 中的 [包含發行前版本] 核取方塊](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="2f0d9-119">設定或清除此方塊會重新整理套件管理員 UI，以及您可以安裝的可用版本清單。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="2f0d9-120">**套件管理員主控台**：使用 `-IncludePrerelease` 參數搭配 `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package` 與 `Update-Package` 命令。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="2f0d9-121">請參閱 [PowerShell 參考](../tools/powershell-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-121">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="2f0d9-122">**NuGet CLI**：使用 `-prerelease` 參數搭配 `install`、`update`、`delete` 與 `mirror` 命令。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="2f0d9-123">請參閱 [NuGet CLI 參考](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="2f0d9-123">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="2f0d9-124">語意版本控制</span><span class="sxs-lookup"><span data-stu-id="2f0d9-124">Semantic versioning</span></span>

<span data-ttu-id="2f0d9-125">[語意化版本控制系統或 SemVer 慣例](http://semver.org/spec/v1.0.0.html)描述如何利用版本號碼中的字串傳遞基礎程式碼的意涵。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-125">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="2f0d9-126">在此慣例中，每個版本都有三個部分 `Major.Minor.Patch`，代表意義如下：</span><span class="sxs-lookup"><span data-stu-id="2f0d9-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="2f0d9-127">`Major`：重大變更</span><span class="sxs-lookup"><span data-stu-id="2f0d9-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="2f0d9-128">`Minor`：新功能，但具回溯相容性</span><span class="sxs-lookup"><span data-stu-id="2f0d9-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="2f0d9-129">`Patch`：僅具有回溯相容的錯誤 (Bug) 修正</span><span class="sxs-lookup"><span data-stu-id="2f0d9-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="2f0d9-130">然後在發行前版本的修補程式編號後附加連字號和一個字串。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="2f0d9-131">就技術層面而言，連字號後面可以使用「任何」字串，NuGet 會將套件視為發行前版本。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="2f0d9-132">然後，NuGet 會在適用的 UI 中顯示完整的版本號碼，讓取用者自行解譯其意義。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="2f0d9-133">請記住，通常遵循如下所示的可辨識命名慣例會比較好：</span><span class="sxs-lookup"><span data-stu-id="2f0d9-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="2f0d9-134">`-alpha`：Alpha 版本，通常用於進行中的工作和實驗</span><span class="sxs-lookup"><span data-stu-id="2f0d9-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="2f0d9-135">`-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的錯誤 (Bug)。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="2f0d9-136">`-rc`：候選版，除非出現重大的錯誤 (Bug)，不然通常是準最終版本 (穩定版)。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="2f0d9-137">NuGet 4.3.0+ 支援[ v2.0.0](http://semver.org/spec/v2.0.0.html)，其支援使用點標記法的發行前版本號碼，如同 `1.0.1-build.23`。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="2f0d9-138">4.3.0 之前的 NuGet 版本不支援點標記法。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="2f0d9-139">在舊版的 NuGet 中，您可以使用類似 `1.0.1-build23` 的形式，但之前向來將這視為發行前版本。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="2f0d9-140">但無論使用什麼樣的尾碼，NuGet 都會以反向字母順序給予它們優先權：</span><span class="sxs-lookup"><span data-stu-id="2f0d9-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="2f0d9-141">如範例所示，不含任何尾碼的版本一律優先於發行前版本。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="2f0d9-142">另請注意，如果您使用數值尾碼和可能使用兩位數 (或以上) 數字的發行前版本標籤，請和 beta01 及 beta05 一樣前面加零，以確保數字變大時正確排序。</span><span class="sxs-lookup"><span data-stu-id="2f0d9-142">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
