---
title: 從 package.config 移轉至 PackageReference 格式
description: 如何從 package.config 管理格式的專案移轉至 PackageReference 所支援之 NuGet 4.0 + 和 VS2017 及.NET Core 2.0 的詳細資料
author: karann-msft
ms.author: karann
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 05a82e48c7083a19c50a05fa1df74ebfff8030d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546682"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="a5684-103">從 packages.config 移轉至 PackageReference</span><span class="sxs-lookup"><span data-stu-id="a5684-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="a5684-104">Visual Studio 2017 15.7 與更新版本支援將專案從 [packages.config](./packages-config.md) 管理格式移轉為 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。</span><span class="sxs-lookup"><span data-stu-id="a5684-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="a5684-105">使用 PackageReference 的優點</span><span class="sxs-lookup"><span data-stu-id="a5684-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="a5684-106">**管理所有專案相依性，在同一個地方**： 就像專案對專案參考和組件參考，NuGet 套件參考 (使用`PackageReference`節點) 所管理直接在專案檔中，而不是使用個別packages.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5684-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="a5684-107">**最上層相依性的整齊的檢視**： 不同於 packages.config，PackageReference 會列出只有您在專案中直接安裝這些 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a5684-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="a5684-108">如此一來，NuGet 套件管理員 UI 和專案檔不被雜亂無章下層相依性。</span><span class="sxs-lookup"><span data-stu-id="a5684-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="a5684-109">**效能改進**： 當使用 PackageReference 時，封裝會在維護*全域套件*資料夾 (在上所述[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)而非在`packages`方案內的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a5684-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="a5684-110">如此一來，PackageReference 執行速度快，並取用較少的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="a5684-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="a5684-111">**妥善控制相依性和內容流動**： 使用 MSBuild 的現有功能可讓您[有條件地參考 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)選擇每個目標架構的套件參考和組態，平台或其他樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="a5684-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="a5684-112">**PackageReference 正在進行開發**： 請參閱 < [PackageReference 問題在 GitHub 上](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="a5684-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="a5684-113">packages.config 已不再進行開發。</span><span class="sxs-lookup"><span data-stu-id="a5684-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="a5684-114">限制</span><span class="sxs-lookup"><span data-stu-id="a5684-114">Limitations</span></span>

* <span data-ttu-id="a5684-115">Visual Studio 2015 和更早版本中未提供 NuGet PackageReference。</span><span class="sxs-lookup"><span data-stu-id="a5684-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="a5684-116">只可以在 Visual Studio 2017 中開啟已移轉的專案。</span><span class="sxs-lookup"><span data-stu-id="a5684-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="a5684-117">移轉目前不適用於 C++ 和 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="a5684-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="a5684-118">有些封裝可能無法完全相容，使用 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="a5684-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="a5684-119">如需詳細資訊，請參閱 <<c0> [ 封裝相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="a5684-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="a5684-120">已知問題</span><span class="sxs-lookup"><span data-stu-id="a5684-120">Known Issues</span></span>

1. <span data-ttu-id="a5684-121">滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項</span><span class="sxs-lookup"><span data-stu-id="a5684-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="a5684-122">問題</span><span class="sxs-lookup"><span data-stu-id="a5684-122">Issue</span></span> 
 
<span data-ttu-id="a5684-123">當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。</span><span class="sxs-lookup"><span data-stu-id="a5684-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="a5684-124">這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。</span><span class="sxs-lookup"><span data-stu-id="a5684-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="a5684-125">因應措施</span><span class="sxs-lookup"><span data-stu-id="a5684-125">Workaround</span></span> 

<span data-ttu-id="a5684-126">執行以下任何一個 NuGet 動作：</span><span class="sxs-lookup"><span data-stu-id="a5684-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="a5684-127">開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="a5684-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="a5684-128">開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="a5684-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="a5684-129">執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="a5684-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="a5684-130">建置專案也會觸發 NuGet 還原</span><span class="sxs-lookup"><span data-stu-id="a5684-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="a5684-131">您現在應該可以看到移轉選項。</span><span class="sxs-lookup"><span data-stu-id="a5684-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="a5684-132">請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。</span><span class="sxs-lookup"><span data-stu-id="a5684-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="a5684-133">移轉步驟</span><span class="sxs-lookup"><span data-stu-id="a5684-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="a5684-134">開始移轉之前，Visual Studio 會建立專案可讓您一份[向前復原回到 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。</span><span class="sxs-lookup"><span data-stu-id="a5684-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="a5684-135">開啟包含專案所使用的方案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="a5684-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="a5684-136">在 [**方案總管] 中**，以滑鼠右鍵按一下**參考**節點或`packages.config`檔案，然後選取**Packages.config na PackageReference...**.</span><span class="sxs-lookup"><span data-stu-id="a5684-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="a5684-137">遷移程式會分析專案的 NuGet 套件參考，並嘗試對其進行分類**最上層相依性**（您在直接安裝 NuGet 套件） 和**可轉移相依性**（已安裝為最上層套件的相依性的套件）。</span><span class="sxs-lookup"><span data-stu-id="a5684-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="a5684-138">PackageReference 支援可轉移套件還原，並解析相依性，以動態方式表示，可轉移相依性需要不明確安裝。</span><span class="sxs-lookup"><span data-stu-id="a5684-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="a5684-139">（選擇性）您可以選擇將歸類為最上層相依性可轉移相依性，藉由選取 NuGet 套件**最上層**封裝的選項。</span><span class="sxs-lookup"><span data-stu-id="a5684-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="a5684-140">此選項會自動設定的套件，其中包含的資產，不會轉移流動 (中`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`資料夾)，且這些標示為開發相依性 (`developmentDependency = "true"`)。</span><span class="sxs-lookup"><span data-stu-id="a5684-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="a5684-141">檢閱任何[封裝相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="a5684-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="a5684-142">選取 **確定**即可開始移轉。</span><span class="sxs-lookup"><span data-stu-id="a5684-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="a5684-143">在移轉結束時，Visual Studio，請提供備份，已安裝的套件 （最上層相依性） 的清單，做為可轉移的相依性，參考的套件清單的開頭所識別的相容性問題的清單的路徑與報表移轉。</span><span class="sxs-lookup"><span data-stu-id="a5684-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="a5684-144">報表會儲存到備份資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a5684-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="a5684-145">解決方案會建置並執行驗證。</span><span class="sxs-lookup"><span data-stu-id="a5684-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="a5684-146">如果您遇到問題，[在 GitHub 上提出問題](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="a5684-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="a5684-147">如何回復到 packages.config</span><span class="sxs-lookup"><span data-stu-id="a5684-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="a5684-148">關閉已移轉的專案。</span><span class="sxs-lookup"><span data-stu-id="a5684-148">Close the migrated project.</span></span>

1. <span data-ttu-id="a5684-149">將專案檔案複製並`packages.config`從備份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 至專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="a5684-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="a5684-150">如果它存在於專案根目錄，請刪除了 obj 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a5684-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="a5684-151">開啟專案。</span><span class="sxs-lookup"><span data-stu-id="a5684-151">Open the project.</span></span>

1. <span data-ttu-id="a5684-152">開啟 Package Manager Console**工具 > NuGet 套件管理員 > Package Manager Console**功能表命令。</span><span class="sxs-lookup"><span data-stu-id="a5684-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="a5684-153">在主控台中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a5684-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="a5684-154">封裝相容性問題</span><span class="sxs-lookup"><span data-stu-id="a5684-154">Package compatibility issues</span></span>

<span data-ttu-id="a5684-155">不支援 PackageReference packages.config 中所支援的某些層面。</span><span class="sxs-lookup"><span data-stu-id="a5684-155">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="a5684-156">遷移程式會分析並偵測到這類問題。</span><span class="sxs-lookup"><span data-stu-id="a5684-156">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="a5684-157">任何具有一或多個下列問題的封裝可能無法如預期般在移轉之後。</span><span class="sxs-lookup"><span data-stu-id="a5684-157">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="a5684-158">在移轉之後安裝該套件時，會忽略"install.ps1 」 指令碼</span><span class="sxs-lookup"><span data-stu-id="a5684-158">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a5684-159">**描述**</span><span class="sxs-lookup"><span data-stu-id="a5684-159">**Description**</span></span> | <span data-ttu-id="a5684-160">使用 PackageReference install.ps1 和 uninstall.ps1 PowerShell 指令碼不會安裝或解除安裝套件時執行。</span><span class="sxs-lookup"><span data-stu-id="a5684-160">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="a5684-161">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="a5684-161">**Potential impact**</span></span> | <span data-ttu-id="a5684-162">封裝相依於這些指令碼來設定目的地專案中的某些行為可能不會如預期運作。</span><span class="sxs-lookup"><span data-stu-id="a5684-162">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="a5684-163">在移轉之後安裝該套件時，不提供 「 內容 」 的資產</span><span class="sxs-lookup"><span data-stu-id="a5684-163">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a5684-164">**描述**</span><span class="sxs-lookup"><span data-stu-id="a5684-164">**Description**</span></span> | <span data-ttu-id="a5684-165">在封裝中的資產`content`資料夾不支援 PackageReference，而且會忽略。</span><span class="sxs-lookup"><span data-stu-id="a5684-165">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="a5684-166">PackageReference 新增支援`contentFiles`更可轉移的支援和共用的內容。</span><span class="sxs-lookup"><span data-stu-id="a5684-166">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="a5684-167">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="a5684-167">**Potential impact**</span></span> | <span data-ttu-id="a5684-168">中的資產`content`不會複製到專案和專案相依於這些資產是否存在的程式碼需要重構。</span><span class="sxs-lookup"><span data-stu-id="a5684-168">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="a5684-169">在升級之後安裝套件時，不會套用 XDT 轉換</span><span class="sxs-lookup"><span data-stu-id="a5684-169">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a5684-170">**描述**</span><span class="sxs-lookup"><span data-stu-id="a5684-170">**Description**</span></span> | <span data-ttu-id="a5684-171">XDT 轉換不支援使用 PackageReference 和`.xdt`安裝或解除安裝套件時，會忽略檔案。</span><span class="sxs-lookup"><span data-stu-id="a5684-171">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="a5684-172">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="a5684-172">**Potential impact**</span></span> | <span data-ttu-id="a5684-173">XDT 轉換不會套用至任何專案的 XML 檔案，最常見`web.config.install.xdt`並`web.config.uninstall.xdt`，這表示專案的` web.config`安裝或解除安裝封裝時，不會更新檔案。</span><span class="sxs-lookup"><span data-stu-id="a5684-173">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="a5684-174">在移轉之後安裝該套件時，會忽略 lib 根目錄中的組件</span><span class="sxs-lookup"><span data-stu-id="a5684-174">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a5684-175">**描述**</span><span class="sxs-lookup"><span data-stu-id="a5684-175">**Description**</span></span> | <span data-ttu-id="a5684-176">使用 PackageReference，組件會呈現的根目錄`lib`資料夾，但特定子資料夾目標 framework 不會被忽略。</span><span class="sxs-lookup"><span data-stu-id="a5684-176">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="a5684-177">NuGet 會尋找相符的對應到專案的目標 framework 的目標 framework moniker (TFM) 的子資料夾，並會比對組件安裝至專案。</span><span class="sxs-lookup"><span data-stu-id="a5684-177">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="a5684-178">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="a5684-178">**Potential impact**</span></span> | <span data-ttu-id="a5684-179">沒有相符的對應到專案的目標 framework 的目標 framework moniker (TFM) 的子資料夾的套件不能如預期轉換後或容錯移轉期間的安裝</span><span class="sxs-lookup"><span data-stu-id="a5684-179">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="a5684-180">找出問題？</span><span class="sxs-lookup"><span data-stu-id="a5684-180">Found an issue?</span></span> <span data-ttu-id="a5684-181">報告它 ！</span><span class="sxs-lookup"><span data-stu-id="a5684-181">Report it!</span></span>

<span data-ttu-id="a5684-182">如果您遇到移轉體驗有問題時，請[NuGet GitHub 存放庫上提出問題](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="a5684-182">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
