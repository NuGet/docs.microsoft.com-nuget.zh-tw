---
title: NuGet 1.4 版本資訊
description: NuGet 1.4 的版本資訊, 包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5f1d3ed6a1b20fb07437f1718faafaac0a193773
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488701"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="a19ea-103">NuGet 1.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a19ea-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="a19ea-104">[Nuget 1.3 版本](../release-notes/nuget-1.3.md) | 資訊[nuget 1.5 版本](../release-notes/nuget-1.5.md)資訊</span><span class="sxs-lookup"><span data-stu-id="a19ea-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="a19ea-105">NuGet 1.4 已于2011年6月17日發行。</span><span class="sxs-lookup"><span data-stu-id="a19ea-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="a19ea-106">功能</span><span class="sxs-lookup"><span data-stu-id="a19ea-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="a19ea-107">更新-套件改良功能</span><span class="sxs-lookup"><span data-stu-id="a19ea-107">Update-Package improvements</span></span>
<span data-ttu-id="a19ea-108">NuGet 1.4 引進了許多更新封裝命令的改良功能, 讓您更輕鬆地在解決方案中的多個專案之間保持相同版本的套件。</span><span class="sxs-lookup"><span data-stu-id="a19ea-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="a19ea-109">例如, 將套件升級至最新版本時, 要將安裝該套件的所有專案更新為相同的 verision, 是很常見的情況。</span><span class="sxs-lookup"><span data-stu-id="a19ea-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="a19ea-110">`Update-Package`命令現在可讓您更輕鬆地執行下列作業:</span><span class="sxs-lookup"><span data-stu-id="a19ea-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="a19ea-111">更新單一專案中的所有封裝</span><span class="sxs-lookup"><span data-stu-id="a19ea-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="a19ea-112">更新所有專案中的封裝</span><span class="sxs-lookup"><span data-stu-id="a19ea-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="a19ea-113">更新所有專案中的所有封裝</span><span class="sxs-lookup"><span data-stu-id="a19ea-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="a19ea-114">對所有套件執行「安全」更新</span><span class="sxs-lookup"><span data-stu-id="a19ea-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="a19ea-115">`-Safe`旗標會限制只能升級至具有相同主要和次要版本元件的版本。</span><span class="sxs-lookup"><span data-stu-id="a19ea-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="a19ea-116">例如, 如果已安裝版本1.0.0 的封裝, 而摘要中有版本1.0.1、1.0.2 和 1.1, `-Safe`旗標就會將套件更新為1.0.2。</span><span class="sxs-lookup"><span data-stu-id="a19ea-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="a19ea-117">升級時若`-Safe`沒有旗標, 會將套件升級至最新版本1.1。</span><span class="sxs-lookup"><span data-stu-id="a19ea-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="a19ea-118">在解決方案層級管理封裝</span><span class="sxs-lookup"><span data-stu-id="a19ea-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="a19ea-119">在 NuGet 1.4 之前, 使用對話方塊將封裝安裝到多個專案會很麻煩。</span><span class="sxs-lookup"><span data-stu-id="a19ea-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="a19ea-120">每個專案都必須啟動對話方塊一次。</span><span class="sxs-lookup"><span data-stu-id="a19ea-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="a19ea-121">NuGet 1.4 加入了在多個專案中同時安裝/卸載/更新套件的支援。</span><span class="sxs-lookup"><span data-stu-id="a19ea-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="a19ea-122">只要以滑鼠右鍵按一下方案, 然後選取 [**管理 NuGet 套件**] 功能表選項, 即可啟動。</span><span class="sxs-lookup"><span data-stu-id="a19ea-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![解決方案層級的 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="a19ea-124">請注意, 在對話方塊的標題列中, 會顯示方案的名稱, 而不是專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="a19ea-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="a19ea-125">封裝作業現在提供具有作業應套用之專案清單的核取方塊清單。</span><span class="sxs-lookup"><span data-stu-id="a19ea-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![管理 NuGet 套件專案選擇](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="a19ea-127">如需詳細資訊, 請參閱[管理解決方案的封裝](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)主題。</span><span class="sxs-lookup"><span data-stu-id="a19ea-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="a19ea-128">限制升級為允許的版本</span><span class="sxs-lookup"><span data-stu-id="a19ea-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="a19ea-129">根據預設, 在封裝上`Update-Package`執行命令 (或使用對話方塊更新封裝) 時, 它會更新為摘要中的最新版本。</span><span class="sxs-lookup"><span data-stu-id="a19ea-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="a19ea-130">有了更新所有封裝的新支援, 您可能會想要將封裝鎖定至特定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="a19ea-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="a19ea-131">例如, 您可能事先知道, 您的應用程式只會使用版本 2. \* 的套件, 而不是3.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="a19ea-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="a19ea-132">為了避免不小心將套件更新為 3, NuGet 1.4 加入了限制封裝可升級的版本的支援, 方法是使用新`packages.config` `allowedVersions`的屬性手動編輯該檔案。</span><span class="sxs-lookup"><span data-stu-id="a19ea-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="a19ea-133">例如, 下列範例示範如何鎖定`SomePackage`版本範圍 2.0-3.0 (獨佔) 的套件。</span><span class="sxs-lookup"><span data-stu-id="a19ea-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="a19ea-134">屬性會接受使用[版本範圍格式](../concepts/package-versioning.md#version-ranges-and-wildcards)的值。 `allowedVersions`</span><span class="sxs-lookup"><span data-stu-id="a19ea-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="a19ea-135">請注意, 在1.4 中, 必須手動編輯特定版本範圍的封裝。</span><span class="sxs-lookup"><span data-stu-id="a19ea-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="a19ea-136">在 NuGet 1.5 中, 我們打算新增透過`Install-Package`命令來放置此範圍的支援。</span><span class="sxs-lookup"><span data-stu-id="a19ea-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="a19ea-137">封裝視覺化</span><span class="sxs-lookup"><span data-stu-id="a19ea-137">Package Visualizer</span></span>
<span data-ttu-id="a19ea-138">新的封裝視覺化檢視會透過 [**工具** -> ] [程式庫] [**套件管理員** -> **封裝**] 功能表選項來啟動, 讓您可以輕鬆地將所有專案及其在中的套件相依性視覺化解.</span><span class="sxs-lookup"><span data-stu-id="a19ea-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="a19ea-139">_**重要注意事項:** 這項功能會利用 Visual Studio 中的 DGML 支援。只有在 Visual Studio Ultimate 中才支援建立視覺效果。只有 Visual Studio Premium 或更高版本才支援視圖 DGML 圖表。_</span><span class="sxs-lookup"><span data-stu-id="a19ea-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![封裝視覺化](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="a19ea-141">NuGet 對話的自動更新檢查</span><span class="sxs-lookup"><span data-stu-id="a19ea-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="a19ea-142">某些版本的 nuget 會導入透過檔案所`.nuspec`表示的新功能, 而舊版的 nuget 對話並不瞭解。</span><span class="sxs-lookup"><span data-stu-id="a19ea-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="a19ea-143">其中一個範例是 NuGet 1.4 中用來[指定架構元件](../release-notes/nuget-1.2.md#framework-assembly-refs)的簡介。</span><span class="sxs-lookup"><span data-stu-id="a19ea-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="a19ea-144">因此, 請務必使用最新版本的 NuGet, 以確保您可以使用可利用最新功能的套件。</span><span class="sxs-lookup"><span data-stu-id="a19ea-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="a19ea-145">若要讓 NuGet 的更新更可見, NuGet 對話方塊會包含在有較新版本可用時反白顯示的邏輯。</span><span class="sxs-lookup"><span data-stu-id="a19ea-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="a19ea-146">_**注意**:只有在目前的會話中選取 [**線上**] 索引標籤時, 才會進行檢查。_</span><span class="sxs-lookup"><span data-stu-id="a19ea-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![提供新版本的 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="a19ea-148">若要關閉自動檢查更新, 請移至 [NuGet 設定] 對話方塊, 並取消核取 [**自動檢查更新**]。</span><span class="sxs-lookup"><span data-stu-id="a19ea-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 設定](./media/nuget-settings.png)

<span data-ttu-id="a19ea-150">這項功能實際上是在 NuGet 1.3 中新增, 但是在更新至 1.3 (例如 NuGet 1.4) 之前, 並不會顯示。</span><span class="sxs-lookup"><span data-stu-id="a19ea-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="a19ea-151">套件管理員對話方塊改善</span><span class="sxs-lookup"><span data-stu-id="a19ea-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="a19ea-152">**改良的功能表名稱**:為了清楚起見, 啟動對話方塊的功能表選項已重新命名。</span><span class="sxs-lookup"><span data-stu-id="a19ea-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="a19ea-153">[功能表] 選項現在是 [**管理 NuGet 封裝**]。</span><span class="sxs-lookup"><span data-stu-id="a19ea-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="a19ea-154">[**詳細資料] 窗格會顯示最新的更新日期**:當選取 [**線上**] 或 [**更新**] 索引標籤時, [NuGet] 對話方塊會在封裝的詳細資料窗格中顯示最新更新的日期。</span><span class="sxs-lookup"><span data-stu-id="a19ea-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="a19ea-155">**顯示的標記清單**:Nuget 對話方塊會顯示標記。</span><span class="sxs-lookup"><span data-stu-id="a19ea-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="a19ea-156">Powershell 改良功能</span><span class="sxs-lookup"><span data-stu-id="a19ea-156">Powershell Improvements</span></span>
* <span data-ttu-id="a19ea-157">**已簽署的 PowerShell 腳本**:NuGet 包含已簽署的 Powershell 腳本, 讓您在更嚴格的環境中使用。</span><span class="sxs-lookup"><span data-stu-id="a19ea-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="a19ea-158">**提示支援**:套件管理員主控台現在支援透過`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令的提示。</span><span class="sxs-lookup"><span data-stu-id="a19ea-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="a19ea-159">**套件來源名稱**:使用`-Source`旗標指定封裝來源時, 支援提供封裝來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="a19ea-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="a19ea-160">nuget.exe 命令列改良功能</span><span class="sxs-lookup"><span data-stu-id="a19ea-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="a19ea-161">**Nuget 自訂命令**: nuget.exe 可透過使用 MEF 的自訂命令進行擴充。</span><span class="sxs-lookup"><span data-stu-id="a19ea-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="a19ea-162">**更簡單地建立符號套件的工作流程**:旗標可以套用至一般慣例式資料夾結構, 只需包含資料夾中的來源和`.pdb`檔案, 即可建立符號套件。 `-Symbols`</span><span class="sxs-lookup"><span data-stu-id="a19ea-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="a19ea-163">**指定多個來源**:命令支援使用分號做為分隔符號, 或指定`-Source`多次來指定多個來源。 `NuGet install`</span><span class="sxs-lookup"><span data-stu-id="a19ea-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="a19ea-164">**Proxy 驗證支援**:在需要驗證的 proxy 後方使用 NuGet 時, NuGet 1.4 新增了提示輸入使用者認證的支援。</span><span class="sxs-lookup"><span data-stu-id="a19ea-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="a19ea-165">**Nuget.exe 更新中斷性變更**:現在需要有旗標, nuget.exe 才會自行更新。 `-Self`</span><span class="sxs-lookup"><span data-stu-id="a19ea-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="a19ea-166">`nuget.exe Update`現在會採用檔案的路徑`packages.config` , 並嘗試更新套件。</span><span class="sxs-lookup"><span data-stu-id="a19ea-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="a19ea-167">請注意, 這項更新的限制在於, 它不會: \* \* 更新、新增、移除專案檔中的內容。</span><span class="sxs-lookup"><span data-stu-id="a19ea-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="a19ea-168">\* \* 在封裝內執行 Powershell 腳本。</span><span class="sxs-lookup"><span data-stu-id="a19ea-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="a19ea-169">NuGet 伺服器支援使用 nuget.exe 推送套件</span><span class="sxs-lookup"><span data-stu-id="a19ea-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="a19ea-170">Nuget 包含一個簡單的方式, 可透過`NuGet.Server` NuGet 套件裝載[輕量的 web 型 NuGet 存放庫](../hosting-packages/nuget-server.md)。</span><span class="sxs-lookup"><span data-stu-id="a19ea-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="a19ea-171">使用 NuGet 1.4, 輕量伺服器支援使用 nuget.exe 推送和刪除套件。</span><span class="sxs-lookup"><span data-stu-id="a19ea-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="a19ea-172">的最新版本`NuGet.Server`會新增名`appSetting`為`apiKey`的新。</span><span class="sxs-lookup"><span data-stu-id="a19ea-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="a19ea-173">當省略金鑰或保留空白時, 會停用將套件推送至摘要的功能。</span><span class="sxs-lookup"><span data-stu-id="a19ea-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="a19ea-174">將 apiKey 設定為值 (最好是強式密碼), 可以使用 nuget.exe 來推送套件。</span><span class="sxs-lookup"><span data-stu-id="a19ea-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="a19ea-175">Windows Phone Tools Mango Edition 的支援</span><span class="sxs-lookup"><span data-stu-id="a19ea-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="a19ea-176">Windows Phone Tools for Mango 的發行候選版本現在支援 NuGet。</span><span class="sxs-lookup"><span data-stu-id="a19ea-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="a19ea-177">Windows Phone 工具目前不支援 Visual Studio 延伸模組管理員, 因此若要安裝適用于 Windows Phone 工具的 NuGet, 您可能需要手動下載並執行 VSIX。</span><span class="sxs-lookup"><span data-stu-id="a19ea-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="a19ea-178">若要卸載 Windows Phone 工具的 NuGet, 請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="a19ea-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="a19ea-179">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="a19ea-179">Bug Fixes</span></span>
<span data-ttu-id="a19ea-180">NuGet 1.4 總共已修正88個工作專案。</span><span class="sxs-lookup"><span data-stu-id="a19ea-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="a19ea-181">71的已標示為 bug。</span><span class="sxs-lookup"><span data-stu-id="a19ea-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="a19ea-182">如需 NuGet 1.4 中已修正之工作專案的完整清單, 請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="a19ea-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="a19ea-183">錯誤修正值得注意:</span><span class="sxs-lookup"><span data-stu-id="a19ea-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="a19ea-184">[問題 603](http://nuget.codeplex.com/workitem/603):指定特定封裝來源時, 跨不同存放庫的套件相依性會正確解析。</span><span class="sxs-lookup"><span data-stu-id="a19ea-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="a19ea-185">[問題 1036](http://nuget.codeplex.com/workitem/1036):新增`NuGet Pack SomeProject.csproj`至後置組建事件不會再造成無限迴圈。</span><span class="sxs-lookup"><span data-stu-id="a19ea-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="a19ea-186">[問題 961](http://nuget.codeplex.com/workitem/961): `-Source`旗標支援相對路徑。</span><span class="sxs-lookup"><span data-stu-id="a19ea-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="a19ea-187">NuGet 1.4 更新</span><span class="sxs-lookup"><span data-stu-id="a19ea-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="a19ea-188">在 NuGet 1.4 發行之後不久, 我們發現有幾個重要的問題要修正。</span><span class="sxs-lookup"><span data-stu-id="a19ea-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="a19ea-189">此更新至1.4 的特定版本號碼為1.4.20615.9020。</span><span class="sxs-lookup"><span data-stu-id="a19ea-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="a19ea-190">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="a19ea-190">Bug Fixes</span></span>
* <span data-ttu-id="a19ea-191">[問題 1220](http://nuget.codeplex.com/workitem/1220):當有一個以上的`install.ps1`專案時, 更新套件不會在所有專案中執行/ `uninstall.ps1`</span><span class="sxs-lookup"><span data-stu-id="a19ea-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="a19ea-192">[問題 1156](http://nuget.codeplex.com/workitem/1156):套件管理員主控台卡在 W2K3/XP 上 (未安裝 Powershell 2 時)</span><span class="sxs-lookup"><span data-stu-id="a19ea-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
