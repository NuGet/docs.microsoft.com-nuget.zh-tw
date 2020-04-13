---
title: 從 package.config 移轉到 PackageReference 格式
description: 詳細說明如何將專案從 package.config 管理格式移轉到受 NuGet 4.0+、VS2017 與 .NET Core 2.0 支援的 PackageReference
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428888"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="9554d-103">從 package.config 移轉到 PackageReference</span><span class="sxs-lookup"><span data-stu-id="9554d-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="9554d-104">Visual Studio 2017 15.7 版和更新版本支援將專案從 [packages.config](../reference/packages-config.md) 管理格式移轉到 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。</span><span class="sxs-lookup"><span data-stu-id="9554d-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](../reference/packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="9554d-105">使用 PackageReference 的優點</span><span class="sxs-lookup"><span data-stu-id="9554d-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="9554d-106">**在一個位置管理所有項目依賴項**:就像專案到專案引用和程式集引用一樣,NuGet 包`PackageReference`引用( 使用節點)直接在專案檔中管理,而不是使用單獨的包。</span><span class="sxs-lookup"><span data-stu-id="9554d-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="9554d-107">**頂級依賴項的整潔檢視**:與包.config 不同,包參考僅列出您直接安裝在專案中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="9554d-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="9554d-108">因此，NuGet 套件管理員 UI 和專案檔不會因包含下層相依性而變得雜亂。</span><span class="sxs-lookup"><span data-stu-id="9554d-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="9554d-109">**性能改進**:使用 PackageReference 時,包將保存在*全域包*資料夾中(如[管理全域包和緩存資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)時所述`packages`,而不是解決方案中的 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9554d-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="9554d-110">因此，PackageReference 執行較快，且耗用較少磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="9554d-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="9554d-111">**對依賴項和內容流的精細控制**:使用 MSBuild 的現有功能,您可以[有條件地引用 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition),並選擇每個目標框架、配置、平臺或其他數據透視的包引用。</span><span class="sxs-lookup"><span data-stu-id="9554d-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="9554d-112">**套件參考正在積極開發中**:請參閱[GitHub 上的套件參考問題](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="9554d-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="9554d-113">packages.config 已不再進行開發。</span><span class="sxs-lookup"><span data-stu-id="9554d-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="9554d-114">限制</span><span class="sxs-lookup"><span data-stu-id="9554d-114">Limitations</span></span>

* <span data-ttu-id="9554d-115">在 Visual Studio 2015 與更早版本中，無法使用 NuGet PackageReference。</span><span class="sxs-lookup"><span data-stu-id="9554d-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="9554d-116">已移轉專案只能在 Visual Studio 2017 與更新版本中開啟。</span><span class="sxs-lookup"><span data-stu-id="9554d-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="9554d-117">移轉目前不適用於 C++ 和 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="9554d-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="9554d-118">某些套件可能無法與 PackageReference 完全相容。</span><span class="sxs-lookup"><span data-stu-id="9554d-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="9554d-119">如需詳細資訊，請參閱[套件相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="9554d-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

<span data-ttu-id="9554d-120">此外,與包相比,Package參考的工作方式也存在一些差異。例如-[約束升級版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)不是由包參考,但添加對[浮動版本](../consume-packages/package-references-in-project-files.md#floating-versions)的支援。</span><span class="sxs-lookup"><span data-stu-id="9554d-120">In addition, there are some differences in how PackageReferences work compared to packages.config. For example - [constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) is not supprted by PackageReference but add support for [Floating Versions](../consume-packages/package-references-in-project-files.md#floating-versions).</span></span>

### <a name="known-issues"></a><span data-ttu-id="9554d-121">已知問題</span><span class="sxs-lookup"><span data-stu-id="9554d-121">Known Issues</span></span>

1. <span data-ttu-id="9554d-122">滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項</span><span class="sxs-lookup"><span data-stu-id="9554d-122">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="9554d-123">問題</span><span class="sxs-lookup"><span data-stu-id="9554d-123">Issue</span></span> 
 
<span data-ttu-id="9554d-124">當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。</span><span class="sxs-lookup"><span data-stu-id="9554d-124">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="9554d-125">這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。</span><span class="sxs-lookup"><span data-stu-id="9554d-125">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="9554d-126">因應措施</span><span class="sxs-lookup"><span data-stu-id="9554d-126">Workaround</span></span> 

<span data-ttu-id="9554d-127">執行以下任何一個 NuGet 動作：</span><span class="sxs-lookup"><span data-stu-id="9554d-127">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="9554d-128">開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="9554d-128">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="9554d-129">開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="9554d-129">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="9554d-130">執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="9554d-130">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="9554d-131">建置專案也會觸發 NuGet 還原</span><span class="sxs-lookup"><span data-stu-id="9554d-131">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="9554d-132">您現在應該可以看到移轉選項。</span><span class="sxs-lookup"><span data-stu-id="9554d-132">You should now be able to see the migration option.</span></span> <span data-ttu-id="9554d-133">請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。</span><span class="sxs-lookup"><span data-stu-id="9554d-133">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="9554d-134">移轉步驟</span><span class="sxs-lookup"><span data-stu-id="9554d-134">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="9554d-135">移轉開始之前，Visual Studio 會建立專案的備份，以允許您在必要時[復原到 packages.config](#how-to-roll-back-to-packagesconfig)。</span><span class="sxs-lookup"><span data-stu-id="9554d-135">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="9554d-136">開啟包含使用 `packages.config` 之專案的解決方案。</span><span class="sxs-lookup"><span data-stu-id="9554d-136">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="9554d-137">在 [方案總管]\*\*\*\* 中，以滑鼠右鍵按一下 [參考]\*\*\*\* 節點或 `packages.config` 檔案，然後選取 [將 packages.config 移轉至 PackageReference]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="9554d-137">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="9554d-138">移轉程式會分析專案的 NuGet 套件參考，並嘗試將它們分類成**頂層相依性** (您直接安裝的 NuGet 套件) 與**可轉移的相依性** (已安裝為頂層套件相依性的套件)。</span><span class="sxs-lookup"><span data-stu-id="9554d-138">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="9554d-139">PackageReference 支援可轉移套件還原，且會動態地解析相依性，這表示不需要明確地安裝可轉移的相依性。</span><span class="sxs-lookup"><span data-stu-id="9554d-139">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="9554d-140">(選擇性) 您可以選取 NuGet 套件的 [頂層]\*\*\*\* 選項，將套件分類為頂層可轉移的相依性。</span><span class="sxs-lookup"><span data-stu-id="9554d-140">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="9554d-141">針對包含無法轉移的資產 (在 `build`、`buildCrossTargeting`、`contentFiles` 或 `analyzers` 資料夾中) 的套件，以及標示為開發相依性 (`developmentDependency = "true"`) 的套件，系統會自動為它們設定此選項。</span><span class="sxs-lookup"><span data-stu-id="9554d-141">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="9554d-142">檢閱任何[套件相容性問題](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="9554d-142">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="9554d-143">選取 [確定]\*\*\*\* 來開始移轉。</span><span class="sxs-lookup"><span data-stu-id="9554d-143">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="9554d-144">當移轉結束時，Visual Studio 會提供一份報告，其中包含備份的路徑、已安裝套件的清單 (頂層相依性)、參考為可轉移相依性之套件的清單，以及在開始移轉時識別出的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="9554d-144">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="9554d-145">報表會儲存至 [backup] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9554d-145">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="9554d-146">驗證解決方案可建置並執行。</span><span class="sxs-lookup"><span data-stu-id="9554d-146">Validate that the solution builds and runs.</span></span> <span data-ttu-id="9554d-147">如果您遇到問題，請[在 GitHub 上提出問題](https://github.com/NuGet/Home/issues/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="9554d-147">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="9554d-148">如何復原為 packages.config</span><span class="sxs-lookup"><span data-stu-id="9554d-148">How to roll back to packages.config</span></span>

1. <span data-ttu-id="9554d-149">關閉已移轉專案。</span><span class="sxs-lookup"><span data-stu-id="9554d-149">Close the migrated project.</span></span>

1. <span data-ttu-id="9554d-150">將專案檔與 `packages.config` 從備份 (通常在 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 複製到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="9554d-150">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="9554d-151">如果 obj 資料夾存在於專案根目錄中，請將它刪除。</span><span class="sxs-lookup"><span data-stu-id="9554d-151">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="9554d-152">開啟專案。</span><span class="sxs-lookup"><span data-stu-id="9554d-152">Open the project.</span></span>

1. <span data-ttu-id="9554d-153">使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台]\*\*\*\* 功能表命令來開啟 [套件管理器主控台]。</span><span class="sxs-lookup"><span data-stu-id="9554d-153">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="9554d-154">在主控台中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="9554d-154">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="9554d-155">移轉之後建立套件</span><span class="sxs-lookup"><span data-stu-id="9554d-155">Create a package after migration</span></span>

<span data-ttu-id="9554d-156">完成移轉之後，建議您新增 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) \(英文\) nuget 套件的參考，然後使用 [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) 來建立套件。</span><span class="sxs-lookup"><span data-stu-id="9554d-156">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="9554d-157">雖然在某些情況下，您可以使用 `dotnet.exe pack` 而不是 `msbuild -t:pack`，但不建議這麼做。</span><span class="sxs-lookup"><span data-stu-id="9554d-157">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="9554d-158">套件相容性問題</span><span class="sxs-lookup"><span data-stu-id="9554d-158">Package compatibility issues</span></span>

<span data-ttu-id="9554d-159">PackageReference 中不支援某些在 packages.config 中支援的層面。</span><span class="sxs-lookup"><span data-stu-id="9554d-159">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="9554d-160">移轉程式會分析並偵測此類問題。</span><span class="sxs-lookup"><span data-stu-id="9554d-160">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="9554d-161">有一或多個下列問題的任何套件，在移轉之後可能不會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="9554d-161">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="9554d-162">當套件是在移轉之後安裝時，系統會忽略 "install. ps1" 指令碼</span><span class="sxs-lookup"><span data-stu-id="9554d-162">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9554d-163">**說明**</span><span class="sxs-lookup"><span data-stu-id="9554d-163">**Description**</span></span> | <span data-ttu-id="9554d-164">使用 PackageReference 時，在安裝套件或將套件解除時，不會執行 install.ps1 與 uninstall.ps1 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9554d-164">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="9554d-165">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="9554d-165">**Potential impact**</span></span> | <span data-ttu-id="9554d-166">相依於這些指令碼以在目的專案中設定某些行為的套件，可能無法如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="9554d-166">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="9554d-167">當套件是在移轉之後安裝時，會無法使用「內容」資產</span><span class="sxs-lookup"><span data-stu-id="9554d-167">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9554d-168">**說明**</span><span class="sxs-lookup"><span data-stu-id="9554d-168">**Description**</span></span> | <span data-ttu-id="9554d-169">PackageReference 不支援在套件的 `content` 資料夾中的資產，因此系統會忽略它們。</span><span class="sxs-lookup"><span data-stu-id="9554d-169">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="9554d-170">PackageReference 新增對 `contentFiles` 的支援，以獲得更好的可轉移支援和共用內容。</span><span class="sxs-lookup"><span data-stu-id="9554d-170">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="9554d-171">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="9554d-171">**Potential impact**</span></span> | <span data-ttu-id="9554d-172">`content` 中的資產未複製到專案中，且依賴那些資產存在的專案程式碼必須重構。</span><span class="sxs-lookup"><span data-stu-id="9554d-172">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="9554d-173">當套件是在升級後安裝時，不會套用 XDT 轉換</span><span class="sxs-lookup"><span data-stu-id="9554d-173">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9554d-174">**說明**</span><span class="sxs-lookup"><span data-stu-id="9554d-174">**Description**</span></span> | <span data-ttu-id="9554d-175">PackageReference 不支援 XDT 轉換，而且在安裝套件或將套件解除安裝時，系統會忽略 `.xdt` 檔案。</span><span class="sxs-lookup"><span data-stu-id="9554d-175">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="9554d-176">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="9554d-176">**Potential impact**</span></span> | <span data-ttu-id="9554d-177">XDT 轉換不會套用至任何專案 XML 檔案，最常見的是 `web.config.install.xdt` 與 `web.config.uninstall.xdt`，這表示專案的 ` web.config` 檔案，沒有在安裝套件或將套件解除安裝時更新。</span><span class="sxs-lookup"><span data-stu-id="9554d-177">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="9554d-178">當套件是在遷移之後安裝時，系統會忽略 lib 根目錄中的組件</span><span class="sxs-lookup"><span data-stu-id="9554d-178">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9554d-179">**說明**</span><span class="sxs-lookup"><span data-stu-id="9554d-179">**Description**</span></span> | <span data-ttu-id="9554d-180">使用 PackageReference 時，系統會忽略出現在 `lib` 資料夾根目錄且沒有目標架構特定子資料夾的組件。</span><span class="sxs-lookup"><span data-stu-id="9554d-180">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="9554d-181">NuGet 會尋找與專案目標 Framework 對應之目標 Framework Moniker (TFM) 相符的子資料夾，並將相符的元件安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="9554d-181">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="9554d-182">**潛在影響**</span><span class="sxs-lookup"><span data-stu-id="9554d-182">**Potential impact**</span></span> | <span data-ttu-id="9554d-183">若套件沒有與專案目標架構對應之目標 Framework Moniker (TFM) 相符的子資料夾，在移轉之後可能無法如預期般運作，或可能在移轉期間安裝失敗</span><span class="sxs-lookup"><span data-stu-id="9554d-183">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="9554d-184">發現問題嗎？</span><span class="sxs-lookup"><span data-stu-id="9554d-184">Found an issue?</span></span> <span data-ttu-id="9554d-185">請回報！</span><span class="sxs-lookup"><span data-stu-id="9554d-185">Report it!</span></span>

<span data-ttu-id="9554d-186">如果您遇到移轉體驗的問題，請[在 NuGet GitHub 存放庫中提出問題](https://github.com/NuGet/Home/issues/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="9554d-186">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
