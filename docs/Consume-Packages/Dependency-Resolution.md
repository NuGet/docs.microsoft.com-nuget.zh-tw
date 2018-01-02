---
title: "NuGet 套件相依性解析 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "在 NuGet 2.x 和 NuGet 3.x+ 中解析和安裝 NuGet 套件相依性之程序的詳細資料。"
keywords: "NuGet 套件相依性、NuGet 版本控制、相依性版本、版本圖形、版本解析、可轉移還原"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 44c69c07990fed72b439698d22021ebcbb2eed89
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="f8623-104">NuGet 如何解析套件相依性</span><span class="sxs-lookup"><span data-stu-id="f8623-104">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="f8623-105">只要安裝或重新安裝套件 (包含安裝為[還原](../consume-packages/package-restore.md)程序一部分的套件)，NuGet 也會安裝與這個第一個套件相依的任何其他套件。</span><span class="sxs-lookup"><span data-stu-id="f8623-105">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="f8623-106">這些立即相依性接著會有其自己的相依性，而這會繼續到任意深度。</span><span class="sxs-lookup"><span data-stu-id="f8623-106">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="f8623-107">這會產生所謂的「相依性圖形」，以描述套件之間的關聯性為所有層級。</span><span class="sxs-lookup"><span data-stu-id="f8623-107">This produces what's called a *dependency graph* that describes the relationships between packages are all levels.</span></span>

<span data-ttu-id="f8623-108">多個套件具有相同的相依性時，同一個套件識別碼可能會多次出現在圖形中，但可能具有不同版本的條件約束。</span><span class="sxs-lookup"><span data-stu-id="f8623-108">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="f8623-109">不過，專案中只能使用特定版本的指定套件，因此 NuGet 必須選擇要使用的版本。</span><span class="sxs-lookup"><span data-stu-id="f8623-109">However, only one version of a given package can be used in a project, so NuGet must choose which version is be used.</span></span> <span data-ttu-id="f8623-110">確切程序取決於所使用的套件參考格式。</span><span class="sxs-lookup"><span data-stu-id="f8623-110">The exact process depends on the package reference format being used.</span></span>

<span data-ttu-id="f8623-111">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="f8623-111">In this topic:</span></span>
- [<span data-ttu-id="f8623-112">使用 PackageReference 和 project.json 的相依性解析</span><span class="sxs-lookup"><span data-stu-id="f8623-112">Dependency resolution with PackageReference and project.json</span></span>](#dependency-resolution-with-packagereference-and-projectjson)
- [<span data-ttu-id="f8623-113">使用 packages.config 的相依性解析</span><span class="sxs-lookup"><span data-stu-id="f8623-113">Dependency resolution with packages.config</span></span>](#dependency-resolution-with-packagesconfig)
- <span data-ttu-id="f8623-114">[排除參考](#excluding-references)，這在某個專案中所指定相依性與另一個專案所產生組件之間衝突時是必要的。</span><span class="sxs-lookup"><span data-stu-id="f8623-114">[Excluding references](#excluding-references), which is necessary when there's a conflict between a dependency specified in one project and an assembly that's produced by another.</span></span>
- [<span data-ttu-id="f8623-115">套件安裝期間的相依性更新</span><span class="sxs-lookup"><span data-stu-id="f8623-115">Dependency updates during package install</span></span>](#dependency-updates-during-package-install)
- [<span data-ttu-id="f8623-116">解決不相容的套件錯誤</span><span class="sxs-lookup"><span data-stu-id="f8623-116">Resolving incompatible package errors</span></span>](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a><span data-ttu-id="f8623-117">使用 PackageReference 和 project.json 的相依性解析</span><span class="sxs-lookup"><span data-stu-id="f8623-117">Dependency resolution with PackageReference and project.json</span></span>

<span data-ttu-id="f8623-118">使用 PackageReference 或 `project.json` 格式將套件安裝至專案時，NuGet 會新增適當檔案中一般套件圖形的參考，並事先解決衝突。</span><span class="sxs-lookup"><span data-stu-id="f8623-118">When installing packages into projects using the PackageReference or `project.json` formats, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="f8623-119">此程序稱為「可轉移還原」。</span><span class="sxs-lookup"><span data-stu-id="f8623-119">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="f8623-120">重新安裝或還原套件則是下載圖形中所列套件的程序，導致更快速且更容易預測的組建。</span><span class="sxs-lookup"><span data-stu-id="f8623-120">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="f8623-121">您也可以利用萬用字元 (浮動) 版本 (例如 2.8.\*)，避免用戶端電腦和組建伺服器上對 `nuget update` 的昂貴且容易出錯的呼叫。</span><span class="sxs-lookup"><span data-stu-id="f8623-121">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="f8623-122">NuGet 還原程序在建置之前執行時，會先解析記憶體中的相依性，然後使用 PackageReference 將產生的圖形寫入至專案之 `obj` 資料夾中稱為 `project.assets.json` 的檔案，或名為 `project.lock.json` 的檔案和 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="f8623-122">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json` in the `obj` folder of a project using PackageReference, or in a file named `project.lock.json` alongside `project.json`.</span></span> <span data-ttu-id="f8623-123">MSBuild 接著會讀取這個檔案，並將它轉譯成一組可找到可能參考的資料夾，然後將它們新增至記憶體中的專案樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="f8623-123">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="f8623-124">鎖定檔案是暫時的，不應該新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="f8623-124">The lock file is temporary and should not be added to source control.</span></span> <span data-ttu-id="f8623-125">它預設會列在 `.gitignore` 和 `.tfignore` 中。</span><span class="sxs-lookup"><span data-stu-id="f8623-125">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="f8623-126">請參閱[套件和原始檔控制](Packages-and-Source-Control.md)。</span><span class="sxs-lookup"><span data-stu-id="f8623-126">See [Packages and source control](Packages-and-Source-Control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="f8623-127">相依性解析規則</span><span class="sxs-lookup"><span data-stu-id="f8623-127">Dependency resolution rules</span></span>

<span data-ttu-id="f8623-128">可轉移還原會套用四個主要規則以解析相依性：最低適用版本、浮動版本、最近獲取和鄰近相依性。</span><span class="sxs-lookup"><span data-stu-id="f8623-128">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="f8623-129">最低適用版本</span><span class="sxs-lookup"><span data-stu-id="f8623-129">Lowest applicable version</span></span>

<span data-ttu-id="f8623-130">最低適用版本規則可還原依其相依性所定義之最低可能版本的套件。</span><span class="sxs-lookup"><span data-stu-id="f8623-130">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="f8623-131">除非宣告為[浮動](#floating-versions)，否則它也適用於與應用程式或類別庫的相依性。</span><span class="sxs-lookup"><span data-stu-id="f8623-131">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="f8623-132">例如，在下圖中，將 1.0-beta 視為低於 1.0，因此 NuGet 會選擇 1.0 版：</span><span class="sxs-lookup"><span data-stu-id="f8623-132">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![選擇最低適用版本](media/projectJson-dependency-1.png)

<span data-ttu-id="f8623-134">在下圖中，摘要上未提供 2.1 版，但因為版本條件約束 >= 2.1，所以 NuGet 會挑選它可找到的下一個最低版本，在此情況下為 2.2：</span><span class="sxs-lookup"><span data-stu-id="f8623-134">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![選擇摘要上下一個可用的最低版本](media/projectJson-dependency-2.png)

<span data-ttu-id="f8623-136">如果應用程式指定不適用於摘要的確切版本號碼 (例如 1.2)，則嘗試安裝或還原套件時，NuGet 會失敗並發生錯誤：</span><span class="sxs-lookup"><span data-stu-id="f8623-136">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![NuGet 會在確切套件版本無法使用時產生錯誤](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="f8623-138">浮動 (萬用字元) 版本</span><span class="sxs-lookup"><span data-stu-id="f8623-138">Floating (wildcard) versions</span></span>

<span data-ttu-id="f8623-139">浮動或萬用字元相依性版本是使用 \* 萬用字元所指定，與 6.0.\* 相同。</span><span class="sxs-lookup"><span data-stu-id="f8623-139">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="f8623-140">此版本規格指出「使用最新的 6.0.x 版」；4.\* 表示「使用最新的 4.x 版」。</span><span class="sxs-lookup"><span data-stu-id="f8623-140">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="f8623-141">使用萬用字元，可讓相依性套件繼續發展，而不需要變更取用中應用程式 (或套件)。</span><span class="sxs-lookup"><span data-stu-id="f8623-141">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="f8623-142">使用萬用字元時，NuGet 會解析符合版本模式的套件最高版本，例如，6.0.\* 所取得之套件最高版本的開頭為 6.0：</span><span class="sxs-lookup"><span data-stu-id="f8623-142">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![在要求浮動版本 6.0.* 時選擇 6.0.1 版](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="f8623-144">如需萬用字元和發行前版本之行為的資訊，請參閱[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="f8623-144">For information on the behavior of wildcards and pre-release versions, see [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="f8623-145">最近獲取</span><span class="sxs-lookup"><span data-stu-id="f8623-145">Nearest wins</span></span>

<span data-ttu-id="f8623-146">應用程式的套件圖形包含相同套件的不同版本時，NuGet 會選擇最接近圖形中應用程式的套件，並忽略所有其他套件。</span><span class="sxs-lookup"><span data-stu-id="f8623-146">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="f8623-147">此行為允許應用程式覆寫相依性圖形中的任何特定套件版本。</span><span class="sxs-lookup"><span data-stu-id="f8623-147">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="f8623-148">在下列範例中，應用程式直接與版本條件約束 >=2.0 的套件 B 相依。</span><span class="sxs-lookup"><span data-stu-id="f8623-148">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="f8623-149">應用程式也與套件 A 相依，而套件 A 接著也與套件 B 相依，但具有 >=1.0 條件約束。</span><span class="sxs-lookup"><span data-stu-id="f8623-149">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="f8623-150">因為與套件 B 2.0 的相依性較接近圖形中的應用程式，所以會使用該版本：</span><span class="sxs-lookup"><span data-stu-id="f8623-150">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![使用最近獲取規則的應用程式](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="f8623-152">最近獲取規則可能會導致套件版本降級，因此可能中斷圖形中的其他相依性。</span><span class="sxs-lookup"><span data-stu-id="f8623-152">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="f8623-153">因此，會套用此規則，並發出警告來提醒使用者。</span><span class="sxs-lookup"><span data-stu-id="f8623-153">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="f8623-154">此規則也會讓大型相依性圖形具有更高的效率 (例如具有 BCL 套件的圖形)，因為忽略指定的相依性之後，NuGet 也會忽略與圖形該分支的所有剩餘相依性。</span><span class="sxs-lookup"><span data-stu-id="f8623-154">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="f8623-155">例如，在下圖中，因為使用套件 C 2.0，所以 NuGet 會忽略圖形中任何參照舊版套件 C 的分支：</span><span class="sxs-lookup"><span data-stu-id="f8623-155">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![NuGet 忽略圖形中的套件時，會忽略整個分支](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="f8623-157">鄰近相依性</span><span class="sxs-lookup"><span data-stu-id="f8623-157">Cousin dependencies</span></span>

<span data-ttu-id="f8623-158">從應用程式中於圖形的相同距離參照不同的套件版本時，NuGet 會使用符合所有版本需求的最低版本 (如同使用就像[最低適用版本](#lowest-applicable-version)和[浮動版本](#floating-versions)規則一樣)。</span><span class="sxs-lookup"><span data-stu-id="f8623-158">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="f8623-159">例如，在下圖中，2.0 版的套件 B 符合另一個 >=1.0 條件約束，因此予以使用：</span><span class="sxs-lookup"><span data-stu-id="f8623-159">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![使用符合所有條件約束的較低版本來解析鄰近相依性](media/projectJson-dependency-7.png)

<span data-ttu-id="f8623-161">在某些情況下，無法符合所有版本需求。</span><span class="sxs-lookup"><span data-stu-id="f8623-161">In some cases, it is not possible to meet all version requirements.</span></span> <span data-ttu-id="f8623-162">如下所示，如果套件 A 只需要套件 B 1.0，而套件 C 需要套件 B >=2.0，則 NuGet 無法解析相依性，而且會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8623-162">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![因確切版本需求而有無法解析的相依性](media/projectJson-dependency-8.png)

<span data-ttu-id="f8623-164">在這些情況下，最上層取用者 (應用程式或套件) 應該新增其與套件 B 的專屬直接相依性，因此套用[最近者獲取](#nearest-wins)規則。</span><span class="sxs-lookup"><span data-stu-id="f8623-164">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="f8623-165">使用 packages.config 的相依性解析</span><span class="sxs-lookup"><span data-stu-id="f8623-165">Dependency resolution with packages.config</span></span>

<span data-ttu-id="f8623-166">使用 `packages.config`，專案的相依性會寫入至 `packages.config` 作為一般清單。</span><span class="sxs-lookup"><span data-stu-id="f8623-166">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="f8623-167">這些套件的任何相依性也會寫入相同的清單中。</span><span class="sxs-lookup"><span data-stu-id="f8623-167">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="f8623-168">安裝套件之後，NuGet 也可能會修改 `.csproj` 檔案、`app.config`、`web.config` 和其他個別檔案。</span><span class="sxs-lookup"><span data-stu-id="f8623-168">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="f8623-169">使用 `packages.config`，NuGet 會嘗試在每個個別套件安裝期間解決相依性衝突。</span><span class="sxs-lookup"><span data-stu-id="f8623-169">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="f8623-170">也就是說，如果套件 A 已安裝並與套件 B 相依，而且套件 B 已列在 `packages.config` 中作為其他項目的相依性，則 NuGet 會比較所要求的套件 B 版本，並嘗試找到符合所有版本條件約束的版本。</span><span class="sxs-lookup"><span data-stu-id="f8623-170">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="f8623-171">具體來說，NuGet 會選取符合相依性的較低 *major.minor* 版本。</span><span class="sxs-lookup"><span data-stu-id="f8623-171">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="f8623-172">NuGet 2.7 和更早版本預設會解析最高「修補程式」版本 (使用 *major.minor.patch.build* 慣例)。</span><span class="sxs-lookup"><span data-stu-id="f8623-172">By default, NuGet 2.7 and earlier resolves the highest *patch* version (using the *major.minor.patch.build* convention).</span></span> <span data-ttu-id="f8623-173">[NuGet 2.8 和更高版本](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)預設會變更此行為來尋找最低修補程式版本。</span><span class="sxs-lookup"><span data-stu-id="f8623-173">[NuGet 2.8 and higher](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) changes this behavior to look for the lowest patch version by default.</span></span> <span data-ttu-id="f8623-174">您可以透過 `Nuget.Config` 中的 `DependencyVersion` 屬性和命令列上的 `-DependencyVersion` 參數，來控制此設定。</span><span class="sxs-lookup"><span data-stu-id="f8623-174">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="f8623-175">針對較大的相依性圖形，解析相依性的 `packages.config` 程序會更為複雜。</span><span class="sxs-lookup"><span data-stu-id="f8623-175">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="f8623-176">每個新套件安裝都需要周遊整個圖形，而且會引發版本衝突機會。</span><span class="sxs-lookup"><span data-stu-id="f8623-176">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="f8623-177">發生衝突時，會停止安裝，並讓專案處於不定狀態，特別是對專案檔本身進行可能的修改。</span><span class="sxs-lookup"><span data-stu-id="f8623-177">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="f8623-178">使用其他套件參考格式時，這不是問題。</span><span class="sxs-lookup"><span data-stu-id="f8623-178">This is not an issue when using other package reference formats.</span></span>


## <a name="managing-dependency-assets"></a><span data-ttu-id="f8623-179">管理相依性資產</span><span class="sxs-lookup"><span data-stu-id="f8623-179">Managing dependency assets</span></span>

<span data-ttu-id="f8623-180">使用 `project.json` 或 PackageReference 格式時，您可以控制從相依性流入最上層專案的資產。</span><span class="sxs-lookup"><span data-stu-id="f8623-180">When using the `project.json` or PackageReference formats, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="f8623-181">如需詳細資料，請參閱 [project.json](../Schema/project-json.md) 和[專案檔中的套件參考](Package-References-in-Project-Files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="f8623-181">For details, see [project.json](../Schema/project-json.md) and [Package references in project files](Package-References-in-Project-Files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="f8623-182">最上層專案本身是套件時，也可以搭配使用 `include` 和 `exclude` 屬性與 `.nuspec` 檔案中所列相依性來控制此流量。</span><span class="sxs-lookup"><span data-stu-id="f8623-182">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="f8623-183">請參閱 [.nu-/spec 參考 - 相依性](../Schema/nuspec.md#dependencies)。</span><span class="sxs-lookup"><span data-stu-id="f8623-183">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="f8623-184">排除參考</span><span class="sxs-lookup"><span data-stu-id="f8623-184">Excluding references</span></span>

<span data-ttu-id="f8623-185">在某些情況下，可能會在專案中多次參考同名的組件，並產生設計階段和建置時間錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8623-185">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="f8623-186">請考慮包含 `C.dll` 之自訂版本的專案，並參考也包含 `C.dll` 的套件 C。</span><span class="sxs-lookup"><span data-stu-id="f8623-186">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="f8623-187">同時，專案也與套件 B 相依，而套件 B 也與套件 C 和 `C.dll` 相依。</span><span class="sxs-lookup"><span data-stu-id="f8623-187">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="f8623-188">因此，NuGet 無法決定要使用的 `C.dll`，但您不能只移除專案與套件 C 的相依性，因為套件 B 也與其相依。</span><span class="sxs-lookup"><span data-stu-id="f8623-188">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="f8623-189">若要解決此問題，您必須直接參考想要的 `C.dll` (或使用另一個參考正確項目的套件)，然後新增與排除所有資產之套件 C 的相依性。</span><span class="sxs-lookup"><span data-stu-id="f8623-189">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="f8623-190">這是根據使用中的套件參考格式所進行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8623-190">This is done as follows depending on the package reference format in use:</span></span>

- <span data-ttu-id="f8623-191">[PackageReference](../consume-packages/package-references-in-project-files.md)：在相依性中新增 `Exclude="All"`：</span><span class="sxs-lookup"><span data-stu-id="f8623-191">[PackageReference](../consume-packages/package-references-in-project-files.md): add `Exclude="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- <span data-ttu-id="f8623-192">`packages.config`：從 `.csproj` 檔案中移除套件 C 的參考，讓它只參考您想要的 `C.dll` 版本。</span><span class="sxs-lookup"><span data-stu-id="f8623-192">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
- <span data-ttu-id="f8623-193">`project.json`：在套件 C 的相依性中新增 `"exclude" : "all"`：</span><span class="sxs-lookup"><span data-stu-id="f8623-193">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="f8623-194">套件安裝期間的相依性更新</span><span class="sxs-lookup"><span data-stu-id="f8623-194">Dependency updates during package install</span></span> 

<span data-ttu-id="f8623-195">使用 NuGet 2.4.x 和更早版本時，如果專案中已有所安裝套件的相依性，則會將相依性更新為符合版本條件約束的最新版本，即使現有版本亦符合這些條件約束也是一樣。</span><span class="sxs-lookup"><span data-stu-id="f8623-195">With NuGet 2.4.x and earlier, when a package is installed whose dependency already exists in the project, the dependency is updated to the latest version that satisfies the version constraints, even if the existing version also satisfies those constraints.</span></span> 

<span data-ttu-id="f8623-196">例如，請考慮使用與套件 B 相依並指定 1.0 作為版本號碼的套件 A。</span><span class="sxs-lookup"><span data-stu-id="f8623-196">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="f8623-197">來源存放庫包含 1.0、1.1 和 1.2 版的套件 B。如果在已包含 B 1.0 版的專案中安裝 A，則會將 B 更新為 1.2 版。</span><span class="sxs-lookup"><span data-stu-id="f8623-197">The source repository contains both versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B is updated to version 1.2.</span></span> 

<span data-ttu-id="f8623-198">使用 NuGet 2.5 和更新版本時，如果已符合相依性版本，則不會在其他套件安裝期間更新相依性。</span><span class="sxs-lookup"><span data-stu-id="f8623-198">With NuGet 2.5 and later, if a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> 

<span data-ttu-id="f8623-199">在上述相同範例中，使用 NuGet 2.5 和更新版本將套件 A 安裝至專案會在專案中保留套件 B 1.0，因為它已符合版本條件約束。</span><span class="sxs-lookup"><span data-stu-id="f8623-199">In the same example above, installing package A into a project with NuGet 2.5 and later leaves package B 1.0 in the project, as it already satisfies the version constraint.</span></span> <span data-ttu-id="f8623-200">不過，如果套件 A 要求 1.1 版或更高版本的 B，則會安裝 B 1.2。</span><span class="sxs-lookup"><span data-stu-id="f8623-200">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="f8623-201">解決不相容的套件錯誤</span><span class="sxs-lookup"><span data-stu-id="f8623-201">Resolving incompatible package errors</span></span>

<span data-ttu-id="f8623-202">在套件還原作業期間，您可能會看到「一或多個套件不相容...」錯誤，或套件與專案目標架構「不相容」。</span><span class="sxs-lookup"><span data-stu-id="f8623-202">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="f8623-203">專案中參考的一或多個套件未指出它們支援專案的目標架構時，會發生此錯誤；也就是說，套件在其 `lib` 資料夾中未包含與專案相容之目標架構的適合 DLL </span><span class="sxs-lookup"><span data-stu-id="f8623-203">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="f8623-204">(如需清單，請參閱[目標架構](../Schema/Target-Frameworks.md))。</span><span class="sxs-lookup"><span data-stu-id="f8623-204">(See [Target frameworks](../Schema/Target-Frameworks.md) for a list.)</span></span> 

<span data-ttu-id="f8623-205">例如，如果專案的目標設為 `netstandard1.6`，而且您嘗試安裝只包含 `lib\net20` 和 `\lib\net45` 資料夾中 DLL 的套件，則會看到套件和其相依項的下列這類訊息：</span><span class="sxs-lookup"><span data-stu-id="f8623-205">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you'll see messages like the following for the package and possibly its dependents:</span></span>

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

<span data-ttu-id="f8623-206">若要解決不相容，請執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="f8623-206">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="f8623-207">將專案的目標重新設為您想要使用的套件所支援的架構。</span><span class="sxs-lookup"><span data-stu-id="f8623-207">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="f8623-208">請連絡套件作者，並與他們合作以新增所選擇架構的支援。</span><span class="sxs-lookup"><span data-stu-id="f8623-208">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="f8623-209">基於此用途，[nuget.org](https://www.nuget.org/) 上的每個套件列出頁面都具有**連絡人負責人**連結。</span><span class="sxs-lookup"><span data-stu-id="f8623-209">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>
- <span data-ttu-id="f8623-210">**不建議**：作為與套件作者合作時的暫時方案，目標設為 `netcore`、`netstandard` 和 `netcoreapp` 的專案可以將其他架構表示為相容，進而允許使用將目標設為這些其他架構的套件。</span><span class="sxs-lookup"><span data-stu-id="f8623-210">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="f8623-211">請參閱 [project.json 匯入](../Schema/project-json.md#imports)和 [MSBuild 還原目標 PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback)。</span><span class="sxs-lookup"><span data-stu-id="f8623-211">See [project.json imports](../Schema/project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="f8623-212">這可能會造成非預期的行為，因此，同樣地，最好與套件作者合作處理更新，以解決套件不相容。</span><span class="sxs-lookup"><span data-stu-id="f8623-212">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>
