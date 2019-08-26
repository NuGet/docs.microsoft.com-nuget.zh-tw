---
title: 從 package.config 移轉到 PackageReference 格式
description: 詳細說明如何將專案從 package.config 管理格式移轉到受 NuGet 4.0+、VS2017 與 .NET Core 2.0 支援的 PackageReference
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 6f659af6b09a12be54a5ef843d34f956119b33f4
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520488"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="011f5-103">從 package.config 移轉到 PackageReference</span><span class="sxs-lookup"><span data-stu-id="011f5-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="011f5-104">Visual Studio 2017 15.7 版和更新版本支援將專案從 [packages.config](../reference/packages-config.md) 管理格式移轉到 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。</span><span class="sxs-lookup"><span data-stu-id="011f5-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](../reference/packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="011f5-105">使用 PackageReference 的優點</span><span class="sxs-lookup"><span data-stu-id="011f5-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="011f5-106">**在一個位置管理所有專案相依性**：就像專案對專案參考與元件參考一樣，NuGet 套件參考 (使用 `PackageReference` 節點) 是直接在專案檔內進行管理，而不是使用個別的 packages.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="011f5-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="011f5-107">**頂層相依性的整齊檢視**：不同於 packages.config，PackageReference 只列出您在專案中直接安裝的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="011f5-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="011f5-108">因此，NuGet 套件管理員 UI 和專案檔不會因包含下層相依性而變得雜亂。</span><span class="sxs-lookup"><span data-stu-id="011f5-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="011f5-109">**效能改進**：使用 PackageReference 時，套件是保存在 [global-packages]  資料夾中 (如[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述)，而不是在解決方案內的 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="011f5-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="011f5-110">因此，PackageReference 執行較快，且耗用較少磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="011f5-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="011f5-111">**對相依性和內容流動進行精細控制**：使用 MSBuild 的現有功能可讓您[有條件地參考 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)，並針對每個目標 Framework、設定、平台或其他樞紐選擇套件參考。</span><span class="sxs-lookup"><span data-stu-id="011f5-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="011f5-112">**PackageReference 正處於開發階段**：請參閱 [GitHub 上的 PackageReference 問題](https://aka.ms/nuget-pr-improvements) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="011f5-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="011f5-113">packages.config 已不再進行開發。</span><span class="sxs-lookup"><span data-stu-id="011f5-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="011f5-114">限制</span><span class="sxs-lookup"><span data-stu-id="011f5-114">Limitations</span></span>

* <span data-ttu-id="011f5-115">在 Visual Studio 2015 與更早版本中，無法使用 NuGet PackageReference。</span><span class="sxs-lookup"><span data-stu-id="011f5-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="011f5-116">已移轉專案只能在 Visual Studio 2017 與更新版本中開啟。</span><span class="sxs-lookup"><span data-stu-id="011f5-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="011f5-117">移轉目前不適用於 C++ 和 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="011f5-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="011f5-118">某些套件可能無法與 PackageReference 完全相容。</span><span class="sxs-lookup"><span data-stu-id="011f5-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="011f5-119">如需詳細資訊，請參閱[套件相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="011f5-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="011f5-120">已知問題</span><span class="sxs-lookup"><span data-stu-id="011f5-120">Known Issues</span></span>

1. <span data-ttu-id="011f5-121">滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項</span><span class="sxs-lookup"><span data-stu-id="011f5-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="011f5-122">問題</span><span class="sxs-lookup"><span data-stu-id="011f5-122">Issue</span></span> 
 
<span data-ttu-id="011f5-123">當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。</span><span class="sxs-lookup"><span data-stu-id="011f5-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="011f5-124">這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。</span><span class="sxs-lookup"><span data-stu-id="011f5-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="011f5-125">因應措施</span><span class="sxs-lookup"><span data-stu-id="011f5-125">Workaround</span></span> 

<span data-ttu-id="011f5-126">執行以下任何一個 NuGet 動作：</span><span class="sxs-lookup"><span data-stu-id="011f5-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="011f5-127">開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="011f5-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="011f5-128">開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="011f5-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="011f5-129">執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="011f5-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="011f5-130">建置專案也會觸發 NuGet 還原</span><span class="sxs-lookup"><span data-stu-id="011f5-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="011f5-131">您現在應該可以看到移轉選項。</span><span class="sxs-lookup"><span data-stu-id="011f5-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="011f5-132">請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。</span><span class="sxs-lookup"><span data-stu-id="011f5-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="011f5-133">移轉步驟</span><span class="sxs-lookup"><span data-stu-id="011f5-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="011f5-134">移轉開始之前，Visual Studio 會建立專案的備份，以允許您在必要時[復原到 packages.config](#how-to-roll-back-to-packagesconfig)。</span><span class="sxs-lookup"><span data-stu-id="011f5-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="011f5-135">開啟包含使用 `packages.config` 之專案的解決方案。</span><span class="sxs-lookup"><span data-stu-id="011f5-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="011f5-136">在 [方案總管]  中，以滑鼠右鍵按一下 [參考]  節點或 `packages.config` 檔案，然後選取 [將 packages.config 移轉至 PackageReference]  。</span><span class="sxs-lookup"><span data-stu-id="011f5-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="011f5-137">移轉程式會分析專案的 NuGet 套件參考，並嘗試將它們分類成**頂層相依性** (您直接安裝的 NuGet 套件) 與**可轉移的相依性** (已安裝為頂層套件相依性的套件)。</span><span class="sxs-lookup"><span data-stu-id="011f5-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="011f5-138">PackageReference 支援可轉移套件還原，且會動態地解析相依性，這表示不需要明確地安裝可轉移的相依性。</span><span class="sxs-lookup"><span data-stu-id="011f5-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="011f5-139">(選擇性) 您可以選取 NuGet 套件的 [頂層]  選項，將套件分類為頂層可轉移的相依性。</span><span class="sxs-lookup"><span data-stu-id="011f5-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="011f5-140">針對包含無法轉移的資產 (在 `build`、`buildCrossTargeting`、`contentFiles` 或 `analyzers` 資料夾中) 的套件，以及標示為開發相依性 (`developmentDependency = "true"`) 的套件，系統會自動為它們設定此選項。</span><span class="sxs-lookup"><span data-stu-id="011f5-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="011f5-141">檢閱任何[套件相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="011f5-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="011f5-142">選取 [確定]  來開始移轉。</span><span class="sxs-lookup"><span data-stu-id="011f5-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="011f5-143">當移轉結束時，Visual Studio 會提供一份報告，其中包含備份的路徑、已安裝套件的清單 (頂層相依性)、參考為可轉移相依性之套件的清單，以及在開始移轉時識別出的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="011f5-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="011f5-144">報表會儲存至 [backup] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="011f5-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="011f5-145">驗證解決方案可建置並執行。</span><span class="sxs-lookup"><span data-stu-id="011f5-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="011f5-146">如果您遇到問題，請[在 GitHub 上提出問題](https://github.com/NuGet/Home/issues/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="011f5-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="011f5-147">如何復原為 packages.config</span><span class="sxs-lookup"><span data-stu-id="011f5-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="011f5-148">關閉已移轉專案。</span><span class="sxs-lookup"><span data-stu-id="011f5-148">Close the migrated project.</span></span>

1. <span data-ttu-id="011f5-149">將專案檔與 `packages.config` 從備份 (通常在 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 複製到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="011f5-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="011f5-150">如果 obj 資料夾存在於專案根目錄中，請將它刪除。</span><span class="sxs-lookup"><span data-stu-id="011f5-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="011f5-151">開啟專案。</span><span class="sxs-lookup"><span data-stu-id="011f5-151">Open the project.</span></span>

1. <span data-ttu-id="011f5-152">使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台]  功能表命令來開啟 [套件管理器主控台]。</span><span class="sxs-lookup"><span data-stu-id="011f5-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="011f5-153">在主控台中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="011f5-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="011f5-154">移轉之後建立套件</span><span class="sxs-lookup"><span data-stu-id="011f5-154">Create a package after migration</span></span>

<span data-ttu-id="011f5-155">完成移轉之後，建議您新增 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) \(英文\) nuget 套件的參考，然後使用 [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) 來建立套件。</span><span class="sxs-lookup"><span data-stu-id="011f5-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="011f5-156">雖然在某些情況下，您可以使用 `dotnet.exe pack` 而不是 `msbuild -t:pack`，但不建議這麼做。</span><span class="sxs-lookup"><span data-stu-id="011f5-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="011f5-157">套件相容性問題</span><span class="sxs-lookup"><span data-stu-id="011f5-157">Package compatibility issues</span></span>

<span data-ttu-id="011f5-158">PackageReference 中不支援某些在 packages.config 中支援的層面。</span><span class="sxs-lookup"><span data-stu-id="011f5-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="011f5-159">移轉程式會分析並偵測此類問題。</span><span class="sxs-lookup"><span data-stu-id="011f5-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="011f5-160">有一或多個下列問題的任何套件，在移轉之後可能不會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="011f5-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="011f5-161">當套件是在移轉之後安裝時，系統會忽略 "install. ps1" 指令碼</span><span class="sxs-lookup"><span data-stu-id="011f5-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="011f5-162">**描述**</span><span class="sxs-lookup"><span data-stu-id="011f5-162">**Description**</span></span> | <span data-ttu-id="011f5-163">使用 PackageReference 時，在安裝套件或將套件解除時，不會執行 install.ps1 與 uninstall.ps1 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="011f5-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="011f5-164">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="011f5-164">**Potential impact**</span></span> | <span data-ttu-id="011f5-165">相依於這些指令碼以在目的專案中設定某些行為的套件，可能無法如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="011f5-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="011f5-166">當套件是在移轉之後安裝時，會無法使用「內容」資產</span><span class="sxs-lookup"><span data-stu-id="011f5-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="011f5-167">**描述**</span><span class="sxs-lookup"><span data-stu-id="011f5-167">**Description**</span></span> | <span data-ttu-id="011f5-168">PackageReference 不支援在套件的 `content` 資料夾中的資產，因此系統會忽略它們。</span><span class="sxs-lookup"><span data-stu-id="011f5-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="011f5-169">PackageReference 新增對 `contentFiles` 的支援，以獲得更好的可轉移支援和共用內容。</span><span class="sxs-lookup"><span data-stu-id="011f5-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="011f5-170">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="011f5-170">**Potential impact**</span></span> | <span data-ttu-id="011f5-171">`content` 中的資產未複製到專案中，且依賴那些資產存在的專案程式碼必須重構。</span><span class="sxs-lookup"><span data-stu-id="011f5-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="011f5-172">當套件是在升級後安裝時，不會套用 XDT 轉換</span><span class="sxs-lookup"><span data-stu-id="011f5-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="011f5-173">**描述**</span><span class="sxs-lookup"><span data-stu-id="011f5-173">**Description**</span></span> | <span data-ttu-id="011f5-174">PackageReference 不支援 XDT 轉換，而且在安裝套件或將套件解除安裝時，系統會忽略 `.xdt` 檔案。</span><span class="sxs-lookup"><span data-stu-id="011f5-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="011f5-175">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="011f5-175">**Potential impact**</span></span> | <span data-ttu-id="011f5-176">XDT 轉換不會套用至任何專案 XML 檔案，最常見的是 `web.config.install.xdt` 與 `web.config.uninstall.xdt`，這表示專案的 ` web.config` 檔案，沒有在安裝套件或將套件解除安裝時更新。</span><span class="sxs-lookup"><span data-stu-id="011f5-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="011f5-177">當套件是在遷移之後安裝時，系統會忽略 lib 根目錄中的組件</span><span class="sxs-lookup"><span data-stu-id="011f5-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="011f5-178">**描述**</span><span class="sxs-lookup"><span data-stu-id="011f5-178">**Description**</span></span> | <span data-ttu-id="011f5-179">使用 PackageReference 時，系統會忽略出現在 `lib` 資料夾根目錄且沒有目標架構特定子資料夾的組件。</span><span class="sxs-lookup"><span data-stu-id="011f5-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="011f5-180">NuGet 會尋找與專案目標 Framework 對應之目標 Framework Moniker (TFM) 相符的子資料夾，並將相符的元件安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="011f5-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="011f5-181">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="011f5-181">**Potential impact**</span></span> | <span data-ttu-id="011f5-182">若套件沒有與專案目標架構對應之目標 Framework Moniker (TFM) 相符的子資料夾，在移轉之後可能無法如預期般運作，或可能在移轉期間安裝失敗</span><span class="sxs-lookup"><span data-stu-id="011f5-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="011f5-183">發現問題嗎？</span><span class="sxs-lookup"><span data-stu-id="011f5-183">Found an issue?</span></span> <span data-ttu-id="011f5-184">請回報！</span><span class="sxs-lookup"><span data-stu-id="011f5-184">Report it!</span></span>

<span data-ttu-id="011f5-185">如果您遇到移轉體驗的問題，請[在 NuGet GitHub 存放庫中提出問題](https://github.com/NuGet/Home/issues/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="011f5-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
