---
title: 從 package.config 移轉至 PackageReference 格式
description: 如何將專案從 package.config 管理格式移轉至 PackageReference 為 NuGet 4.0 + 和 VS2017 和.NET 核心 2.0 所支援的詳細資訊
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 2b15d60d4f71fb2777e36c6a948ad72b4e2bc594
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="f8ee7-103">從 packages.config 移轉至 PackageReference</span><span class="sxs-lookup"><span data-stu-id="f8ee7-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="f8ee7-104">Visual Studio 2017 15.7年預覽第 3 版和更新版本支援的移轉專案，從[packages.config](./packages-config.md)來管理格式[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-104">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="f8ee7-105">使用 PackageReference 的優點</span><span class="sxs-lookup"><span data-stu-id="f8ee7-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="f8ee7-106">**管理所有的專案相依性，在一個地方**： 如同專案對專案參考和組件參考，NuGet 封裝參考 (使用`PackageReference`節點) 直接在專案檔中所管理，而不是使用不同的packages.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="f8ee7-107">**最上層的相依性的整齊的檢視**： 不同於 packages.config，PackageReference 列出只有您直接在專案中所安裝的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="f8ee7-108">如此一來，NuGet 封裝管理員 UI 和專案檔不會因為雜亂下層相依性。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="f8ee7-109">**效能改進**： 當使用 PackageReference，封裝會保留在*全域封裝*資料夾 (在上所述[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不是在`packages`方案中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="f8ee7-110">如此一來，PackageReference 執行的速度快，並耗用較少的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="f8ee7-111">**精確控制相依性，以及內容流程**： 使用 MSBuild 的現有功能可讓您[有條件地參照 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)，然後選擇 目標 framework 中，每個封裝參考組態，平台或其他樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="f8ee7-112">**PackageReference 是真的開發**： 請參閱[PackageReference 發出 GitHub 上](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="f8ee7-113">packages.config 不再是真的開發。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="f8ee7-114">限制</span><span class="sxs-lookup"><span data-stu-id="f8ee7-114">Limitations</span></span>

* <span data-ttu-id="f8ee7-115">NuGet PackageReference 不是適用於 Visual Studio 2015 及更早版本。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="f8ee7-116">只有在 Visual Studio 2017，可以開啟移轉的專案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="f8ee7-117">移轉目前不提供對於 c + + 和 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-117">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="f8ee7-118">某些封裝可能無法與 PackageReference 完全相容。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="f8ee7-119">如需詳細資訊，請參閱[封裝相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="f8ee7-120">移轉步驟</span><span class="sxs-lookup"><span data-stu-id="f8ee7-120">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="f8ee7-121">開始移轉之前，Visual Studio 會建立可讓您的專案備份[向前復原回 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-121">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="f8ee7-122">開啟包含專案所使用的方案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-122">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="f8ee7-123">在**方案總管 中**，以滑鼠右鍵按一下**參考**節點或`packages.config`檔案，然後選取**將 packages.config 移轉至 PackageReference...**.</span><span class="sxs-lookup"><span data-stu-id="f8ee7-123">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="f8ee7-124">遷移程式會分析專案的 NuGet 封裝會參照，並嘗試對其進行分類**最上層的相依性**（NuGet 封裝，您在安裝目錄） 和**可轉移的相依性**（做為相依性的最上層封裝已安裝的封裝）。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-124">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="f8ee7-125">PackageReference 支援可轉移的封裝還原，並解析相依性，以動態方式表示，可轉移的相依性需要不明確安裝。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-125">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="f8ee7-126">（選擇性）您可以選擇將所選取分類為可轉移的相依性為最上層的相依性的 NuGet 封裝**最上層**封裝的選項。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-126">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="f8ee7-127">包含不會轉移性地流動資產封裝的自動設定這個選項 (在`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`資料夾) 及那些標示開發相依性 (`developmentDependency = "true"`)。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-127">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="f8ee7-128">檢閱任何[封裝相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-128">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="f8ee7-129">選取**確定**即可開始移轉。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-129">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="f8ee7-130">在移轉程序的結束時，Visual Studio 會提供報表路徑來備份、 已安裝的封裝 （最上層相依性） 清單，做為可轉移的相依性，參考的封裝清單和清單開頭的識別的相容性問題的移轉。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-130">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="f8ee7-131">報表會儲存到備份資料夾。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-131">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="f8ee7-132">驗證建置並執行方案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-132">Validate that the solution builds and runs.</span></span> <span data-ttu-id="f8ee7-133">如果您遇到問題， [GitHub 上的檔案發生問題](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-133">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="f8ee7-134">如何回復 packages.config</span><span class="sxs-lookup"><span data-stu-id="f8ee7-134">How to roll back to packages.config</span></span>

1. <span data-ttu-id="f8ee7-135">關閉已移轉的專案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-135">Close the migrated project.</span></span>

1. <span data-ttu-id="f8ee7-136">複製專案檔和`packages.config`從備份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-136">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="f8ee7-137">開啟專案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-137">Open the project.</span></span>

1. <span data-ttu-id="f8ee7-138">開啟使用 Package Manager Console**工具 > NuGet 套件管理員 > Package Manager Console**功能表命令。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-138">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="f8ee7-139">在主控台中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f8ee7-139">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="f8ee7-140">封裝相容性問題</span><span class="sxs-lookup"><span data-stu-id="f8ee7-140">Package compatibility issues</span></span>

<span data-ttu-id="f8ee7-141">Packages.config 中支援某些層面 PackageReference 中不支援。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-141">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="f8ee7-142">遷移程式會分析，並偵測到這類問題。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-142">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="f8ee7-143">有一或多個下列問題的任何封裝可能無法如預期般在移轉之後。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-143">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="f8ee7-144">在移轉之後安裝套件時，會略過"install.ps1 」 指令碼</span><span class="sxs-lookup"><span data-stu-id="f8ee7-144">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f8ee7-145">**描述**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-145">**Description**</span></span> | <span data-ttu-id="f8ee7-146">與 PackageReference，install.ps1，uninstall.ps1 PowerShell 指令碼不會安裝或解除安裝封裝時執行。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-146">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="f8ee7-147">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-147">**Potential impact**</span></span> | <span data-ttu-id="f8ee7-148">封裝相依於這些指令碼來設定目的地專案中的某些行為可能無法如預期運作。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-148">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="f8ee7-149">移轉之後安裝此套件時，不使用 「 內容 」 資產</span><span class="sxs-lookup"><span data-stu-id="f8ee7-149">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f8ee7-150">**描述**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-150">**Description**</span></span> | <span data-ttu-id="f8ee7-151">封裝中的資產`content`資料夾 PackageReference 不支援，而且會忽略。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-151">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="f8ee7-152">PackageReference 新增支援`contentFiles`擁有更可轉移的支援和共用的內容。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-152">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="f8ee7-153">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-153">**Potential impact**</span></span> | <span data-ttu-id="f8ee7-154">中的資產`content`不會複製到專案和專案相依於是否存在這些資產的程式碼需要重構。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-154">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="f8ee7-155">在升級之後安裝此套件時，不會套用 XDT 轉換</span><span class="sxs-lookup"><span data-stu-id="f8ee7-155">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f8ee7-156">**描述**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-156">**Description**</span></span> | <span data-ttu-id="f8ee7-157">XDT 轉換不支援 PackageReference 和`.xdt`安裝或解除安裝封裝時要忽略的檔案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-157">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="f8ee7-158">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-158">**Potential impact**</span></span> | <span data-ttu-id="f8ee7-159">XDT 轉換不會套用至任何專案 XML 檔中，大多數情況下，`web.config.install.xdt`和`web.config.uninstall.xdt`，這表示專案的` web.config`安裝或解除安裝封裝時，都未更新檔案。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-159">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="f8ee7-160">在移轉之後安裝套件時，會忽略 lib 根目錄中的組件</span><span class="sxs-lookup"><span data-stu-id="f8ee7-160">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f8ee7-161">**描述**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-161">**Description**</span></span> | <span data-ttu-id="f8ee7-162">PackageReference，組件將呈現的根目錄`lib`資料夾，但目標架構特定子資料夾不會被忽略。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-162">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="f8ee7-163">NuGet 會尋找對應到專案的目標 framework 的目標 framework moniker (TFM) 比對的子資料夾，並在專案中安裝符合的組件。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-163">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="f8ee7-164">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="f8ee7-164">**Potential impact**</span></span> | <span data-ttu-id="f8ee7-165">沒有對應至專案的目標 framework 的目標 framework moniker (TFM) 比對的子資料夾的封裝可能無法如預期般轉換之後的行為或容錯移轉期間的安裝</span><span class="sxs-lookup"><span data-stu-id="f8ee7-165">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="f8ee7-166">找出發生問題？</span><span class="sxs-lookup"><span data-stu-id="f8ee7-166">Found an issue?</span></span> <span data-ttu-id="f8ee7-167">回報 ！</span><span class="sxs-lookup"><span data-stu-id="f8ee7-167">Report it!</span></span>

<span data-ttu-id="f8ee7-168">如果您遇到移轉體驗有問題，請請[NuGet GitHub 儲存機制上的檔案發生問題](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="f8ee7-168">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
