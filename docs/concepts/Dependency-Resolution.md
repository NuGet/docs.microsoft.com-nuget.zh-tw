---
title: NuGet 套件相依性解析
description: 在 NuGet 2.x 和 NuGet 3.x+ 中解析和安裝 NuGet 套件相依性之程序的詳細資料。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: c6f50e6eb21826afebcdcd4045c7ab8b6e6489e3
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813321"
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="b52b3-103">NuGet 如何解析套件相依性</span><span class="sxs-lookup"><span data-stu-id="b52b3-103">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="b52b3-104">只要安裝或重新安裝套件 (包含安裝為[還原](../consume-packages/package-restore.md)程序一部分的套件)，NuGet 也會安裝與這個第一個套件相依的任何其他套件。</span><span class="sxs-lookup"><span data-stu-id="b52b3-104">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="b52b3-105">這些立即相依性接著會有其自己的相依性，而這會繼續到任意深度。</span><span class="sxs-lookup"><span data-stu-id="b52b3-105">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="b52b3-106">這會產生所謂的「相依性圖形」，以描述所有層級上套件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="b52b3-106">This produces what's called a *dependency graph* that describes the relationships between packages at all levels.</span></span>

<span data-ttu-id="b52b3-107">多個套件具有相同的相依性時，同一個套件識別碼可能會多次出現在圖形中，但可能具有不同版本的條件約束。</span><span class="sxs-lookup"><span data-stu-id="b52b3-107">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="b52b3-108">不過，專案中只能使用一個指定套件的版本，因此 NuGet 必須選擇要使用的版本。</span><span class="sxs-lookup"><span data-stu-id="b52b3-108">However, only one version of a given package can be used in a project, so NuGet must choose which version is used.</span></span> <span data-ttu-id="b52b3-109">確切的處理序取決於所使用的套件管理格式。</span><span class="sxs-lookup"><span data-stu-id="b52b3-109">The exact process depends on the package management format being used.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="b52b3-110">使用 PackageReference 的相依性解析</span><span class="sxs-lookup"><span data-stu-id="b52b3-110">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="b52b3-111">使用 PackageReference 格式來將套件安裝至專案時，NuGet 會新增適當檔案中一般套件圖形的參考，並事先解決衝突。</span><span class="sxs-lookup"><span data-stu-id="b52b3-111">When installing packages into projects using the PackageReference format, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="b52b3-112">此程序稱為「可轉移還原」。</span><span class="sxs-lookup"><span data-stu-id="b52b3-112">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="b52b3-113">重新安裝或還原套件則是下載圖形中所列套件的程序，導致更快速且更容易預測的組建。</span><span class="sxs-lookup"><span data-stu-id="b52b3-113">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="b52b3-114">您也可以利用萬用字元 (浮動) 版本 (例如 2.8.\*)，避免用戶端電腦和組建伺服器上對 `nuget update` 的昂貴且容易出錯的呼叫。</span><span class="sxs-lookup"><span data-stu-id="b52b3-114">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="b52b3-115">若 NuGet 還原程序在建置之前執行，就會先解析記憶體中的相依性，然後將產生的圖形寫入稱為 `project.assets.json` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b52b3-115">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json`.</span></span> <span data-ttu-id="b52b3-116">如果[已啟用鎖定檔案功能](../consume-packages/package-references-in-project-files.md#locking-dependencies)，它也會將已解析的相依性寫入名為 `packages.lock.json` 的鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="b52b3-116">It also writes the resolved dependencies to a lock file named `packages.lock.json`, if the [lock file functionality is enabled](../consume-packages/package-references-in-project-files.md#locking-dependencies).</span></span>
<span data-ttu-id="b52b3-117">資產檔案位於 `MSBuildProjectExtensionsPath`，其預設為專案的 'obj' 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b52b3-117">The assets file is located at `MSBuildProjectExtensionsPath`, which defaults to the project's 'obj' folder.</span></span> <span data-ttu-id="b52b3-118">MSBuild 接著會讀取這個檔案，並將它轉譯成一組可找到可能參考的資料夾，然後將它們新增至記憶體中的專案樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="b52b3-118">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="b52b3-119">`project.assets.json` 檔案是暫時的，不應該新增至原始程式碼控制。</span><span class="sxs-lookup"><span data-stu-id="b52b3-119">The `project.assets.json` file is temporary and should not be added to source control.</span></span> <span data-ttu-id="b52b3-120">它預設會列在 `.gitignore` 和 `.tfignore` 中。</span><span class="sxs-lookup"><span data-stu-id="b52b3-120">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="b52b3-121">請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="b52b3-121">See [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="b52b3-122">相依性解析規則</span><span class="sxs-lookup"><span data-stu-id="b52b3-122">Dependency resolution rules</span></span>

<span data-ttu-id="b52b3-123">可轉移還原會套用四個主要規則以解析相依性：最低適用版本、浮動版本、最近獲取和鄰近相依性。</span><span class="sxs-lookup"><span data-stu-id="b52b3-123">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="b52b3-124">最低適用版本</span><span class="sxs-lookup"><span data-stu-id="b52b3-124">Lowest applicable version</span></span>

<span data-ttu-id="b52b3-125">最低適用版本規則可還原依其相依性所定義之最低可能版本的套件。</span><span class="sxs-lookup"><span data-stu-id="b52b3-125">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="b52b3-126">除非宣告為[浮動](#floating-versions)，否則它也適用於與應用程式或類別庫的相依性。</span><span class="sxs-lookup"><span data-stu-id="b52b3-126">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="b52b3-127">例如，在下圖中，將 1.0-beta 視為低於 1.0，因此 NuGet 會選擇 1.0 版：</span><span class="sxs-lookup"><span data-stu-id="b52b3-127">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![選擇最低適用版本](media/projectJson-dependency-1.png)

<span data-ttu-id="b52b3-129">在下圖中，摘要上未提供 2.1 版，但因為版本條件約束 >= 2.1，所以 NuGet 會挑選它可找到的下一個最低版本，在此情況下為 2.2：</span><span class="sxs-lookup"><span data-stu-id="b52b3-129">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![選擇摘要上下一個可用的最低版本](media/projectJson-dependency-2.png)

<span data-ttu-id="b52b3-131">如果應用程式指定不適用於摘要的確切版本號碼 (例如 1.2)，則嘗試安裝或還原套件時，NuGet 會失敗並發生錯誤：</span><span class="sxs-lookup"><span data-stu-id="b52b3-131">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![NuGet 會在確切套件版本無法使用時產生錯誤](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="b52b3-133">浮動 (萬用字元) 版本</span><span class="sxs-lookup"><span data-stu-id="b52b3-133">Floating (wildcard) versions</span></span>

<span data-ttu-id="b52b3-134">浮動或萬用字元相依性版本是使用 \* 萬用字元所指定，與 6.0.\* 相同。</span><span class="sxs-lookup"><span data-stu-id="b52b3-134">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="b52b3-135">此版本規格指出「使用最新的 6.0.x 版」；4.\* 表示「使用最新的 4.x 版」。</span><span class="sxs-lookup"><span data-stu-id="b52b3-135">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="b52b3-136">使用萬用字元，可讓相依性套件繼續發展，而不需要變更取用中應用程式 (或套件)。</span><span class="sxs-lookup"><span data-stu-id="b52b3-136">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="b52b3-137">使用萬用字元時，NuGet 會解析符合版本模式的套件最高版本，例如，6.0.\* 所取得之套件最高版本的開頭為 6.0：</span><span class="sxs-lookup"><span data-stu-id="b52b3-137">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![在要求浮動版本 6.0.\* 時選擇 6.0.1 版](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="b52b3-139">如需萬用字元和發行前版本之行為的資訊，請參閱[套件版本控制](package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="b52b3-139">For information on the behavior of wildcards and pre-release versions, see [Package versioning](package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="b52b3-140">最近獲取</span><span class="sxs-lookup"><span data-stu-id="b52b3-140">Nearest wins</span></span>

<span data-ttu-id="b52b3-141">應用程式的套件圖形包含相同套件的不同版本時，NuGet 會選擇最接近圖形中應用程式的套件，並忽略所有其他套件。</span><span class="sxs-lookup"><span data-stu-id="b52b3-141">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="b52b3-142">此行為允許應用程式覆寫相依性圖形中的任何特定套件版本。</span><span class="sxs-lookup"><span data-stu-id="b52b3-142">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="b52b3-143">在下列範例中，應用程式直接與版本條件約束 >=2.0 的套件 B 相依。</span><span class="sxs-lookup"><span data-stu-id="b52b3-143">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="b52b3-144">應用程式也與套件 A 相依，而套件 A 接著也與套件 B 相依，但具有 >=1.0 條件約束。</span><span class="sxs-lookup"><span data-stu-id="b52b3-144">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="b52b3-145">因為與套件 B 2.0 的相依性較接近圖形中的應用程式，所以會使用該版本：</span><span class="sxs-lookup"><span data-stu-id="b52b3-145">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![使用最近獲取規則的應用程式](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="b52b3-147">最近獲取規則可能會導致套件版本降級，因此可能中斷圖形中的其他相依性。</span><span class="sxs-lookup"><span data-stu-id="b52b3-147">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="b52b3-148">因此，會套用此規則，並發出警告來提醒使用者。</span><span class="sxs-lookup"><span data-stu-id="b52b3-148">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="b52b3-149">此規則也會讓大型相依性圖形具有更高的效率 (例如具有 BCL 套件的圖形)，因為忽略指定的相依性之後，NuGet 也會忽略與圖形該分支的所有剩餘相依性。</span><span class="sxs-lookup"><span data-stu-id="b52b3-149">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="b52b3-150">例如，在下圖中，因為使用套件 C 2.0，所以 NuGet 會忽略圖形中任何參照舊版套件 C 的分支：</span><span class="sxs-lookup"><span data-stu-id="b52b3-150">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![NuGet 忽略圖形中的套件時，會忽略整個分支](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="b52b3-152">鄰近相依性</span><span class="sxs-lookup"><span data-stu-id="b52b3-152">Cousin dependencies</span></span>

<span data-ttu-id="b52b3-153">從應用程式中於圖形的相同距離參照不同的套件版本時，NuGet 會使用符合所有版本需求的最低版本 (如同使用就像[最低適用版本](#lowest-applicable-version)和[浮動版本](#floating-versions)規則一樣)。</span><span class="sxs-lookup"><span data-stu-id="b52b3-153">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="b52b3-154">例如，在下圖中，2.0 版的套件 B 符合另一個 >=1.0 條件約束，因此予以使用：</span><span class="sxs-lookup"><span data-stu-id="b52b3-154">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![使用符合所有條件約束的較低版本來解析鄰近相依性](media/projectJson-dependency-7.png)

<span data-ttu-id="b52b3-156">在某些情況下，無法符合所有版本需求。</span><span class="sxs-lookup"><span data-stu-id="b52b3-156">In some cases, it's not possible to meet all version requirements.</span></span> <span data-ttu-id="b52b3-157">如下所示，如果套件 A 只需要套件 B 1.0，而套件 C 需要套件 B >=2.0，則 NuGet 無法解析相依性，而且會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b52b3-157">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![因確切版本需求而有無法解析的相依性](media/projectJson-dependency-8.png)

<span data-ttu-id="b52b3-159">在這些情況下，最上層取用者 (應用程式或套件) 應該新增其與套件 B 的專屬直接相依性，因此套用[最近者獲取](#nearest-wins)規則。</span><span class="sxs-lookup"><span data-stu-id="b52b3-159">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="b52b3-160">使用 packages.config 的相依性解析</span><span class="sxs-lookup"><span data-stu-id="b52b3-160">Dependency resolution with packages.config</span></span>

<span data-ttu-id="b52b3-161">使用 `packages.config`，專案的相依性會寫入至 `packages.config` 作為一般清單。</span><span class="sxs-lookup"><span data-stu-id="b52b3-161">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="b52b3-162">這些套件的任何相依性也會寫入相同的清單中。</span><span class="sxs-lookup"><span data-stu-id="b52b3-162">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="b52b3-163">安裝套件之後，NuGet 也可能會修改 `.csproj` 檔案、`app.config`、`web.config` 和其他個別檔案。</span><span class="sxs-lookup"><span data-stu-id="b52b3-163">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="b52b3-164">使用 `packages.config`，NuGet 會嘗試在每個個別套件安裝期間解決相依性衝突。</span><span class="sxs-lookup"><span data-stu-id="b52b3-164">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="b52b3-165">也就是說，如果套件 A 已安裝並與套件 B 相依，而且套件 B 已列在 `packages.config` 中作為其他項目的相依性，則 NuGet 會比較所要求的套件 B 版本，並嘗試找到符合所有版本條件約束的版本。</span><span class="sxs-lookup"><span data-stu-id="b52b3-165">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="b52b3-166">具體來說，NuGet 會選取符合相依性的較低 *major.minor* 版本。</span><span class="sxs-lookup"><span data-stu-id="b52b3-166">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="b52b3-167">根據預設，NuGet 2.8 會尋找最低的修補程式版本 (請參閱 [NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies))。</span><span class="sxs-lookup"><span data-stu-id="b52b3-167">By default, NuGet 2.8 looks for the lowest patch version (see [NuGet 2.8 release notes](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span></span> <span data-ttu-id="b52b3-168">您可以透過 `Nuget.Config` 中的 `DependencyVersion` 屬性和命令列上的 `-DependencyVersion` 參數，來控制此設定。</span><span class="sxs-lookup"><span data-stu-id="b52b3-168">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="b52b3-169">針對較大的相依性圖形，解析相依性的 `packages.config` 程序會更為複雜。</span><span class="sxs-lookup"><span data-stu-id="b52b3-169">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="b52b3-170">每個新套件安裝都需要周遊整個圖形，而且會引發版本衝突機會。</span><span class="sxs-lookup"><span data-stu-id="b52b3-170">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="b52b3-171">發生衝突時，會停止安裝，並讓專案處於不定狀態，特別是對專案檔本身進行可能的修改。</span><span class="sxs-lookup"><span data-stu-id="b52b3-171">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="b52b3-172">使用其他套件管理格式時，這不是問題。</span><span class="sxs-lookup"><span data-stu-id="b52b3-172">This is not an issue when using other package management formats.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="b52b3-173">管理相依性資產</span><span class="sxs-lookup"><span data-stu-id="b52b3-173">Managing dependency assets</span></span>

<span data-ttu-id="b52b3-174">使用 PackageReference 格式時，您可以控制從相依性流入最上層專案的資產。</span><span class="sxs-lookup"><span data-stu-id="b52b3-174">When using the PackageReference format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="b52b3-175">如需詳細資訊，請參閱 [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="b52b3-175">For details, see [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="b52b3-176">最上層專案本身是套件時，也可以搭配使用 `include` 和 `exclude` 屬性與 `.nuspec` 檔案中所列相依性來控制此流量。</span><span class="sxs-lookup"><span data-stu-id="b52b3-176">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="b52b3-177">請參閱 [.nu-/spec 參考 - 相依性](../reference/nuspec.md#dependencies)。</span><span class="sxs-lookup"><span data-stu-id="b52b3-177">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="b52b3-178">排除參考</span><span class="sxs-lookup"><span data-stu-id="b52b3-178">Excluding references</span></span>

<span data-ttu-id="b52b3-179">在某些情況下，可能會在專案中多次參考同名的組件，並產生設計階段和建置時間錯誤。</span><span class="sxs-lookup"><span data-stu-id="b52b3-179">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="b52b3-180">請考慮包含 `C.dll` 之自訂版本的專案，並參考也包含 `C.dll` 的套件 C。</span><span class="sxs-lookup"><span data-stu-id="b52b3-180">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="b52b3-181">同時，專案也與套件 B 相依，而套件 B 也與套件 C 和 `C.dll` 相依。</span><span class="sxs-lookup"><span data-stu-id="b52b3-181">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="b52b3-182">因此，NuGet 無法決定要使用的 `C.dll`，但您不能只移除專案與套件 C 的相依性，因為套件 B 也與其相依。</span><span class="sxs-lookup"><span data-stu-id="b52b3-182">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="b52b3-183">若要解決此問題，您必須直接參考想要的 `C.dll` (或使用另一個參考正確項目的套件)，然後新增與排除所有資產之套件 C 的相依性。</span><span class="sxs-lookup"><span data-stu-id="b52b3-183">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="b52b3-184">這是根據使用中的套件管理格式所進行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b52b3-184">This is done as follows depending on the package management format in use:</span></span>

- <span data-ttu-id="b52b3-185">[PackageReference](../consume-packages/package-references-in-project-files.md)：在相依性中新增 `ExcludeAssets="All"`：</span><span class="sxs-lookup"><span data-stu-id="b52b3-185">[PackageReference](../consume-packages/package-references-in-project-files.md): add `ExcludeAssets="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- <span data-ttu-id="b52b3-186">`packages.config`：從 `.csproj` 檔案中移除套件 C 的參考，讓它只參考您想要的 `C.dll` 版本。</span><span class="sxs-lookup"><span data-stu-id="b52b3-186">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="b52b3-187">套件安裝期間的相依性更新</span><span class="sxs-lookup"><span data-stu-id="b52b3-187">Dependency updates during package install</span></span> 

<span data-ttu-id="b52b3-188">如果已符合相依性版本，則不會在其他套件安裝期間更新相依性。</span><span class="sxs-lookup"><span data-stu-id="b52b3-188">If a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> <span data-ttu-id="b52b3-189">例如，請考慮使用與套件 B 相依並指定 1.0 作為版本號碼的套件 A。</span><span class="sxs-lookup"><span data-stu-id="b52b3-189">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="b52b3-190">來源存放庫包含 1.0、1.1 和 1.2 版的套件 B。如果在已包含 B 1.0 版的專案中安裝 A，則 B 1.0 仍會維持使用中狀態，因為它符合版本限制。</span><span class="sxs-lookup"><span data-stu-id="b52b3-190">The source repository contains versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B 1.0 remains in use because it satisfies the version constraint.</span></span> <span data-ttu-id="b52b3-191">不過，如果套件 A 要求 1.1 版或更高版本的 B，則會安裝 B 1.2。</span><span class="sxs-lookup"><span data-stu-id="b52b3-191">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="b52b3-192">解決不相容的套件錯誤</span><span class="sxs-lookup"><span data-stu-id="b52b3-192">Resolving incompatible package errors</span></span>

<span data-ttu-id="b52b3-193">在套件還原作業期間，您可能會看到「一或多個套件不相容...」錯誤，或套件與專案目標架構「不相容」。</span><span class="sxs-lookup"><span data-stu-id="b52b3-193">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="b52b3-194">專案中參考的一或多個套件未指出它們支援專案的目標架構時，會發生此錯誤；也就是說，套件在其 `lib` 資料夾中未包含與專案相容之目標架構的適合 DLL</span><span class="sxs-lookup"><span data-stu-id="b52b3-194">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="b52b3-195">(如需清單，請參閱[目標架構](../reference/target-frameworks.md))。</span><span class="sxs-lookup"><span data-stu-id="b52b3-195">(See [Target frameworks](../reference/target-frameworks.md) for a list.)</span></span> 

<span data-ttu-id="b52b3-196">例如，如果專案的目標設為 `netstandard1.6`，而且您嘗試安裝只包含 `lib\net20` 和 `\lib\net45` 資料夾中 DLL 的套件，則會看到套件和其相依項的下列這類訊息：</span><span class="sxs-lookup"><span data-stu-id="b52b3-196">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you see messages like the following for the package and possibly its dependents:</span></span>

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

<span data-ttu-id="b52b3-197">若要解決不相容，請執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="b52b3-197">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="b52b3-198">將專案的目標重新設為您想要使用的套件所支援的架構。</span><span class="sxs-lookup"><span data-stu-id="b52b3-198">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="b52b3-199">請連絡套件作者，並與他們合作以新增所選擇架構的支援。</span><span class="sxs-lookup"><span data-stu-id="b52b3-199">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="b52b3-200">基於此用途，[nuget.org](https://www.nuget.org/) 上的每個套件列出頁面都具有**連絡人負責人**連結。</span><span class="sxs-lookup"><span data-stu-id="b52b3-200">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>
