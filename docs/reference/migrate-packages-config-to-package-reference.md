---
title: 從 config.xml 遷移至 PackageReference 格式
description: 有關如何將專案從 config.xml 管理格式遷移至 PackageReference 的詳細資料, 如 NuGet 4.0 + 和 VS2017 和 .NET Core 2.0 所支援
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433283"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="dedce-103">從封裝中遷移至 PackageReference</span><span class="sxs-lookup"><span data-stu-id="dedce-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="dedce-104">Visual Studio 2017 15.7 與更新版本支援將專案從 [packages.config](./packages-config.md) 管理格式移轉為 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。</span><span class="sxs-lookup"><span data-stu-id="dedce-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="dedce-105">使用 PackageReference 的優點</span><span class="sxs-lookup"><span data-stu-id="dedce-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="dedce-106">**在一個位置管理所有專案**相依性:就像專案對專案參考和元件參考一樣, NuGet 套件參考 (使用`PackageReference`節點) 會直接在專案檔內進行管理, 而不是使用個別的封裝 .config 檔案。</span><span class="sxs-lookup"><span data-stu-id="dedce-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="dedce-107">**最上層相依性的整齊觀點**:不同于 PackageReference, 您只會列出直接安裝在專案中的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="dedce-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="dedce-108">因此, NuGet 套件管理員 UI 和專案檔不會隨著下層相依性而變得雜亂。</span><span class="sxs-lookup"><span data-stu-id="dedce-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="dedce-109">**效能改進**:使用 PackageReference 時, 套件會保留在*全域封裝*資料夾中 (如[管理全域套件和](../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾, 而不是解決方案中的`packages`資料夾中所述)。</span><span class="sxs-lookup"><span data-stu-id="dedce-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="dedce-110">因此, PackageReference 的執行速度較快, 且耗用的磁碟空間較少。</span><span class="sxs-lookup"><span data-stu-id="dedce-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="dedce-111">**對相依性和內容流程進行細微控制**:使用 MSBuild 的現有功能, 可讓您有[條件地參考 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition), 並選擇每個目標 framework、設定、平臺或其他軸的套件參考。</span><span class="sxs-lookup"><span data-stu-id="dedce-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="dedce-112">**PackageReference 正處於開發階段**:請參閱[GitHub 上的 PackageReference 問題](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="dedce-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="dedce-113">封裝已不再進行開發。</span><span class="sxs-lookup"><span data-stu-id="dedce-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="dedce-114">限制</span><span class="sxs-lookup"><span data-stu-id="dedce-114">Limitations</span></span>

* <span data-ttu-id="dedce-115">Visual Studio 2015 和更早版本中未提供 NuGet PackageReference。</span><span class="sxs-lookup"><span data-stu-id="dedce-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="dedce-116">遷移的專案只能在 Visual Studio 2017 和更新版本中開啟。</span><span class="sxs-lookup"><span data-stu-id="dedce-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="dedce-117">移轉目前不適用於 C++ 和 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="dedce-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="dedce-118">某些套件可能無法與 PackageReference 完全相容。</span><span class="sxs-lookup"><span data-stu-id="dedce-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="dedce-119">如需詳細資訊, 請參閱[套件相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="dedce-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="dedce-120">已知問題</span><span class="sxs-lookup"><span data-stu-id="dedce-120">Known Issues</span></span>

1. <span data-ttu-id="dedce-121">滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項</span><span class="sxs-lookup"><span data-stu-id="dedce-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="dedce-122">問題</span><span class="sxs-lookup"><span data-stu-id="dedce-122">Issue</span></span> 
 
<span data-ttu-id="dedce-123">當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。</span><span class="sxs-lookup"><span data-stu-id="dedce-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="dedce-124">這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。</span><span class="sxs-lookup"><span data-stu-id="dedce-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="dedce-125">因應措施</span><span class="sxs-lookup"><span data-stu-id="dedce-125">Workaround</span></span> 

<span data-ttu-id="dedce-126">執行以下任何一個 NuGet 動作：</span><span class="sxs-lookup"><span data-stu-id="dedce-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="dedce-127">開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="dedce-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="dedce-128">開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="dedce-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="dedce-129">執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="dedce-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="dedce-130">建置專案也會觸發 NuGet 還原</span><span class="sxs-lookup"><span data-stu-id="dedce-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="dedce-131">您現在應該可以看到移轉選項。</span><span class="sxs-lookup"><span data-stu-id="dedce-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="dedce-132">請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。</span><span class="sxs-lookup"><span data-stu-id="dedce-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="dedce-133">遷移步驟</span><span class="sxs-lookup"><span data-stu-id="dedce-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="dedce-134">開始遷移之前, Visual Studio 會建立專案的備份, 以允許您在必要時[復原到 config.xml。](#how-to-roll-back-to-packagesconfig)</span><span class="sxs-lookup"><span data-stu-id="dedce-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="dedce-135">使用`packages.config`開啟包含專案的方案。</span><span class="sxs-lookup"><span data-stu-id="dedce-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="dedce-136">在**方案總管**中, 以滑鼠右鍵按一下 [**參考**] `packages.config`節點或檔案, 然後選取 [**將 PackageReference 遷移至**]。</span><span class="sxs-lookup"><span data-stu-id="dedce-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="dedce-137">遷移程式會分析專案的 NuGet 套件參考, 並嘗試將它們分類成**最上層**相依性 (您直接安裝的 nuget 套件) 和可**轉移**的相依性 (已安裝為的套件最上層套件的相依性)。</span><span class="sxs-lookup"><span data-stu-id="dedce-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="dedce-138">PackageReference 支援可轉移的套件還原並動態解析相依性, 這表示不需要明確安裝可轉移的相依性。</span><span class="sxs-lookup"><span data-stu-id="dedce-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="dedce-139">選擇性您可以選取封裝的**最上層**選項, 將 NuGet 套件分類為可轉移的相依性, 做為最上層的相依性。</span><span class="sxs-lookup"><span data-stu-id="dedce-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="dedce-140">此選項會針對包含不是以可轉移方式 (在`build`、 `buildCrossTargeting`、 `contentFiles`或`analyzers`資料夾中) 的資產, 以及標示為開發相依性 (`developmentDependency = "true"`) 的套件進行自動設定。</span><span class="sxs-lookup"><span data-stu-id="dedce-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="dedce-141">檢查任何[套件相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="dedce-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="dedce-142">選取 **[確定]** 開始進行遷移。</span><span class="sxs-lookup"><span data-stu-id="dedce-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="dedce-143">在遷移結束時, Visual Studio 會提供一份報告, 其中包含備份的路徑、已安裝的套件清單 (最上層的相依性)、參考為可轉移相依性的套件清單, 以及在開頭移動.</span><span class="sxs-lookup"><span data-stu-id="dedce-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="dedce-144">報表會儲存至 [備份] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="dedce-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="dedce-145">驗證解決方案是否已建立並執行。</span><span class="sxs-lookup"><span data-stu-id="dedce-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="dedce-146">如果您遇到問題, 請[在 GitHub 上提出問題](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="dedce-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="dedce-147">如何回復為封裝 .config</span><span class="sxs-lookup"><span data-stu-id="dedce-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="dedce-148">關閉已遷移的專案。</span><span class="sxs-lookup"><span data-stu-id="dedce-148">Close the migrated project.</span></span>

1. <span data-ttu-id="dedce-149">將專案檔和`packages.config`備份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`是) 複製到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="dedce-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="dedce-150">刪除 obj 資料夾 (如果它存在於專案根目錄中)。</span><span class="sxs-lookup"><span data-stu-id="dedce-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="dedce-151">開啟專案。</span><span class="sxs-lookup"><span data-stu-id="dedce-151">Open the project.</span></span>

1. <span data-ttu-id="dedce-152">使用 **工具 > NuGet 套件管理員 > 套件管理員主控台** 功能表命令來開啟 套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="dedce-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="dedce-153">在主控台中執行下列命令:</span><span class="sxs-lookup"><span data-stu-id="dedce-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="dedce-154">在遷移後建立封裝</span><span class="sxs-lookup"><span data-stu-id="dedce-154">Create a package after migration</span></span>

<span data-ttu-id="dedce-155">完成遷移之後, 建議您新增[nuget.exe](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget 封裝的參考, 然後使用[msbuild-t:pack](../reference/msbuild-targets.md#pack-target)來建立封裝, 以建立套件。</span><span class="sxs-lookup"><span data-stu-id="dedce-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="dedce-156">雖然在某些情況下`dotnet.exe pack` `msbuild -t:pack`, 您可以使用而不是, 但不建議這麼做。</span><span class="sxs-lookup"><span data-stu-id="dedce-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="dedce-157">套件相容性問題</span><span class="sxs-lookup"><span data-stu-id="dedce-157">Package compatibility issues</span></span>

<span data-ttu-id="dedce-158">PackageReference 中不支援某些在套件中支援的部分。</span><span class="sxs-lookup"><span data-stu-id="dedce-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="dedce-159">遷移會分析並偵測此類問題。</span><span class="sxs-lookup"><span data-stu-id="dedce-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="dedce-160">有一或多個下列問題的任何套件, 在遷移之後可能不會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="dedce-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="dedce-161">在遷移之後安裝套件時, 會忽略 "install. ps1" 腳本</span><span class="sxs-lookup"><span data-stu-id="dedce-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dedce-162">**描述**</span><span class="sxs-lookup"><span data-stu-id="dedce-162">**Description**</span></span> | <span data-ttu-id="dedce-163">使用 PackageReference 時, 請安裝 ps1 並卸載。在安裝或卸載套件時, 不會執行此 PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="dedce-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="dedce-164">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="dedce-164">**Potential impact**</span></span> | <span data-ttu-id="dedce-165">相依于這些腳本以在目的專案中設定某些行為的封裝, 可能無法如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="dedce-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="dedce-166">在遷移之後安裝套件時, 無法使用「內容」資產</span><span class="sxs-lookup"><span data-stu-id="dedce-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dedce-167">**描述**</span><span class="sxs-lookup"><span data-stu-id="dedce-167">**Description**</span></span> | <span data-ttu-id="dedce-168">套件的`content`資料夾中不支援使用 PackageReference 的資產, 而且會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="dedce-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="dedce-169">PackageReference 新增的支援`contentFiles` , 以獲得更好的可轉移支援和共用內容。</span><span class="sxs-lookup"><span data-stu-id="dedce-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="dedce-170">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="dedce-170">**Potential impact**</span></span> | <span data-ttu-id="dedce-171">中的`content`資產不會複製到專案和專案程式碼中, 而相依于那些資產是否需要重構。</span><span class="sxs-lookup"><span data-stu-id="dedce-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="dedce-172">升級後安裝套件時, 不會套用 XDT 轉換</span><span class="sxs-lookup"><span data-stu-id="dedce-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dedce-173">**描述**</span><span class="sxs-lookup"><span data-stu-id="dedce-173">**Description**</span></span> | <span data-ttu-id="dedce-174">XDT 轉換不支援 PackageReference, 而且在`.xdt`安裝或卸載套件時, 會忽略檔案。</span><span class="sxs-lookup"><span data-stu-id="dedce-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="dedce-175">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="dedce-175">**Potential impact**</span></span> | <span data-ttu-id="dedce-176">XDT 轉換不會套用至任何專案 XML 檔案, 最常見的`web.config.install.xdt`是`web.config.uninstall.xdt`和, 這表示當安裝` web.config`或卸載封裝時, 不會更新專案的檔案。</span><span class="sxs-lookup"><span data-stu-id="dedce-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="dedce-177">在遷移之後安裝套件時, 會忽略 lib 根中的元件</span><span class="sxs-lookup"><span data-stu-id="dedce-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dedce-178">**描述**</span><span class="sxs-lookup"><span data-stu-id="dedce-178">**Description**</span></span> | <span data-ttu-id="dedce-179">使用 PackageReference 時, 會忽略不含目標`lib` framework 特定子資料夾的資料夾根目錄中所出現的元件。</span><span class="sxs-lookup"><span data-stu-id="dedce-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="dedce-180">NuGet 會尋找符合與專案的目標架構對應的目標 framework 標記 (TFM) 的子資料夾, 並將相符的元件安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="dedce-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="dedce-181">**可能的影響**</span><span class="sxs-lookup"><span data-stu-id="dedce-181">**Potential impact**</span></span> | <span data-ttu-id="dedce-182">沒有子資料夾符合對應于專案目標 framework 的目標 framework 標記 (TFM) 的封裝, 在遷移期間轉換或安裝失敗後, 可能無法如預期般運作</span><span class="sxs-lookup"><span data-stu-id="dedce-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="dedce-183">發現問題嗎？</span><span class="sxs-lookup"><span data-stu-id="dedce-183">Found an issue?</span></span> <span data-ttu-id="dedce-184">報表!</span><span class="sxs-lookup"><span data-stu-id="dedce-184">Report it!</span></span>

<span data-ttu-id="dedce-185">如果您遇到遷移體驗的問題, 請[在 NuGet GitHub 存放庫](https://github.com/NuGet/Home/issues/)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="dedce-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
