---
title: NuGet 1.4 版本資訊
description: NuGet 1.4 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777150"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="5742d-103">NuGet 1.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="5742d-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="5742d-104">[NuGet 1.3 版本](../release-notes/nuget-1.3.md)  |  資訊[NuGet 1.5 版本](../release-notes/nuget-1.5.md)資訊</span><span class="sxs-lookup"><span data-stu-id="5742d-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="5742d-105">NuGet 1.4 已于2011年6月17日發行。</span><span class="sxs-lookup"><span data-stu-id="5742d-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="5742d-106">功能</span><span class="sxs-lookup"><span data-stu-id="5742d-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="5742d-107">Update-Package 改進</span><span class="sxs-lookup"><span data-stu-id="5742d-107">Update-Package improvements</span></span>
<span data-ttu-id="5742d-108">NuGet 1.4 對 Update-Package 命令引進了許多改進，讓您更輕鬆地在解決方案中的多個專案之間保持相同版本的套件。</span><span class="sxs-lookup"><span data-stu-id="5742d-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="5742d-109">例如，將封裝升級至最新版本時，您通常會想要將該套件安裝的所有專案更新為相同 verision。</span><span class="sxs-lookup"><span data-stu-id="5742d-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="5742d-110">`Update-Package`命令現在可讓您更輕鬆地：</span><span class="sxs-lookup"><span data-stu-id="5742d-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="5742d-111">更新單一專案中的所有套件</span><span class="sxs-lookup"><span data-stu-id="5742d-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="5742d-112">更新所有專案中的封裝</span><span class="sxs-lookup"><span data-stu-id="5742d-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="5742d-113">更新所有專案中的所有封裝</span><span class="sxs-lookup"><span data-stu-id="5742d-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="5742d-114">對所有套件執行「安全」更新</span><span class="sxs-lookup"><span data-stu-id="5742d-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="5742d-115">旗標會 `-Safe` 限制只升級為具有相同主要和次要版本元件的版本。</span><span class="sxs-lookup"><span data-stu-id="5742d-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="5742d-116">例如，如果已安裝版本1.0.0 的封裝，且摘要中有版本1.0.1、1.0.2 和1.1，旗標就會將 `-Safe` 套件更新為1.0.2。</span><span class="sxs-lookup"><span data-stu-id="5742d-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="5742d-117">如果沒有旗標升級， `-Safe` 就會將套件升級為最新版本1.1。</span><span class="sxs-lookup"><span data-stu-id="5742d-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="5742d-118">在解決方案層級管理套件</span><span class="sxs-lookup"><span data-stu-id="5742d-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="5742d-119">在 NuGet 1.4 之前，使用對話方塊將套件安裝至多個專案會很麻煩。</span><span class="sxs-lookup"><span data-stu-id="5742d-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="5742d-120">每個專案都需要啟動對話方塊一次。</span><span class="sxs-lookup"><span data-stu-id="5742d-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="5742d-121">NuGet 1.4 新增了同時在多個專案中安裝/卸載/更新套件的支援。</span><span class="sxs-lookup"><span data-stu-id="5742d-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="5742d-122">只要以滑鼠右鍵按一下方案，然後選取 [ **管理 NuGet 套件** ] 功能表選項，即可啟動。</span><span class="sxs-lookup"><span data-stu-id="5742d-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![解決方案層級 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="5742d-124">請注意，在對話方塊的標題列中，會顯示方案的名稱，而不是專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="5742d-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="5742d-125">封裝作業現在會提供核取方塊清單，其中包含應套用作業的專案清單。</span><span class="sxs-lookup"><span data-stu-id="5742d-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![管理 NuGet 套件專案選取專案](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="5742d-127">如需詳細資訊，請參閱 [管理解決方案套件](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)的主題。</span><span class="sxs-lookup"><span data-stu-id="5742d-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="5742d-128">將升級限制為允許的版本</span><span class="sxs-lookup"><span data-stu-id="5742d-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="5742d-129">根據預設，在 `Update-Package` 封裝上執行命令 (或使用對話方塊) 更新套件時，將會更新為摘要中的最新版本。</span><span class="sxs-lookup"><span data-stu-id="5742d-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="5742d-130">有了更新所有封裝的新支援，在某些情況下，您可能會想要將套件鎖定至特定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="5742d-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="5742d-131">例如，您可能事先知道您的應用程式只會使用版本 2. \* 的封裝，而不是3.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5742d-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="5742d-132">為了避免不小心將套件更新為3，NuGet 1.4 新增了支援，以限制可以升級套件的版本範圍，方法是 `packages.config` 使用新屬性手動編輯檔案 `allowedVersions` 。</span><span class="sxs-lookup"><span data-stu-id="5742d-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="5742d-133">例如，下列範例示範如何鎖定 `SomePackage` 套件版本範圍 2.0-3.0 (獨佔) 。</span><span class="sxs-lookup"><span data-stu-id="5742d-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="5742d-134">`allowedVersions`屬性接受使用[版本範圍格式](../concepts/package-versioning.md#version-ranges)的值。</span><span class="sxs-lookup"><span data-stu-id="5742d-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="5742d-135">請注意，在1.4 中，鎖定特定版本範圍的套件必須是手動編輯的。</span><span class="sxs-lookup"><span data-stu-id="5742d-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="5742d-136">在 NuGet 1.5 中，我們計畫新增透過命令來放置此範圍的支援 `Install-Package` 。</span><span class="sxs-lookup"><span data-stu-id="5742d-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="5742d-137">封裝視覺化</span><span class="sxs-lookup"><span data-stu-id="5742d-137">Package Visualizer</span></span>
<span data-ttu-id="5742d-138">透過 [**工具**  ->  **庫封裝管理員** 套件視覺化檢視] 功能表選項啟動的新封裝視覺化檢視，可  ->  讓您輕鬆地視覺化方案內的所有專案及其套件相依性。</span><span class="sxs-lookup"><span data-stu-id="5742d-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="5742d-139">_**重要注意事項：** 這項功能會利用 Visual Studio 中的 DGML 支援。只有 Visual Studio Ultimate 才支援建立視覺效果。只有 Visual Studio Premium 或更高版本才支援查看 DGML 圖表。_</span><span class="sxs-lookup"><span data-stu-id="5742d-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![封裝視覺化](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="5742d-141">NuGet 對話方塊的自動更新檢查</span><span class="sxs-lookup"><span data-stu-id="5742d-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="5742d-142">某些版本的 NuGet 引進了透過檔案表示的新功能， `.nuspec` 這些功能是舊版 NuGet 對話方塊無法理解的。</span><span class="sxs-lookup"><span data-stu-id="5742d-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="5742d-143">其中一個範例是 NuGet 1.4 中用來 [指定架構元件](../release-notes/nuget-1.2.md#framework-assembly-refs)的簡介。</span><span class="sxs-lookup"><span data-stu-id="5742d-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="5742d-144">因此，請務必使用最新版本的 NuGet，以確保您可以使用封裝，以利用最新的功能。</span><span class="sxs-lookup"><span data-stu-id="5742d-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="5742d-145">若要讓 NuGet 的更新更清楚，NuGet 對話方塊會包含可在有較新版本可用時醒目提示的邏輯。</span><span class="sxs-lookup"><span data-stu-id="5742d-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="5742d-146">_**注意**：只有在目前的會話中選取 [ **線上** ] 索引標籤時，才會進行檢查。_</span><span class="sxs-lookup"><span data-stu-id="5742d-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![有新版本可用的 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="5742d-148">若要關閉自動檢查更新，請移至 [NuGet 設定] 對話方塊，並取消核取 [ **自動檢查更新**]。</span><span class="sxs-lookup"><span data-stu-id="5742d-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 設定](./media/nuget-settings.png)

<span data-ttu-id="5742d-150">這項功能實際上是新增在 NuGet 1.3 中，但在更新至1.3 之前（例如 NuGet 1.4），將不會顯示。</span><span class="sxs-lookup"><span data-stu-id="5742d-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="5742d-151">封裝管理員對話方塊改進</span><span class="sxs-lookup"><span data-stu-id="5742d-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="5742d-152">**改良的功能表名稱**：為了清楚起見，已重新命名啟動對話方塊的功能表選項。</span><span class="sxs-lookup"><span data-stu-id="5742d-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="5742d-153">功能表選項現在是 [ **管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="5742d-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="5742d-154">**詳細資料窗格會顯示最新的更新日期**：當選取 [ **線上** ] 或 [ **更新** ] 索引標籤時，NuGet 對話方塊會在套件的詳細資料窗格中顯示最新的更新日期。</span><span class="sxs-lookup"><span data-stu-id="5742d-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="5742d-155">**顯示的標記清單**： Nuget 對話方塊會顯示標記。</span><span class="sxs-lookup"><span data-stu-id="5742d-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="5742d-156">Powershell 改進</span><span class="sxs-lookup"><span data-stu-id="5742d-156">Powershell Improvements</span></span>
* <span data-ttu-id="5742d-157">**已簽署的 powershell 腳本**： NuGet 包含已簽署的 powershell 腳本，以便在更嚴格的環境中使用。</span><span class="sxs-lookup"><span data-stu-id="5742d-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="5742d-158">**提示支援**：封裝管理員主控台現在支援透過 `$host.ui.Prompt` 和命令的提示 `$host.ui.PromptForChoice` 。</span><span class="sxs-lookup"><span data-stu-id="5742d-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="5742d-159">**封裝來源名稱**：使用旗標指定套件來源時，支援提供封裝來源的名稱 `-Source` 。</span><span class="sxs-lookup"><span data-stu-id="5742d-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="5742d-160">nuget.exe 命令列改進</span><span class="sxs-lookup"><span data-stu-id="5742d-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="5742d-161">**NuGet 自訂命令**： nuget.exe 可透過使用 MEF 的自訂命令進行擴充。</span><span class="sxs-lookup"><span data-stu-id="5742d-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="5742d-162">**建立符號套件的工作流程更簡單**： `-Symbols` 旗標可以套用至一般慣例式資料夾結構，只要在資料夾內包含來源和檔案，就可以建立符號套件 `.pdb` 。</span><span class="sxs-lookup"><span data-stu-id="5742d-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="5742d-163">**指定多個來源**： `NuGet install` 命令支援使用分號做為分隔符號來指定多個來源，或是指定 `-Source` 多次。</span><span class="sxs-lookup"><span data-stu-id="5742d-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="5742d-164">**Proxy 驗證支援**：當在需要驗證的 Proxy 後方使用 nuget 時，nuget 1.4 新增了提示使用者認證的支援。</span><span class="sxs-lookup"><span data-stu-id="5742d-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="5742d-165">**nuget.exe 更新中斷變更**： `-Self` nuget.exe 必須有旗標才能自行更新。</span><span class="sxs-lookup"><span data-stu-id="5742d-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="5742d-166">`nuget.exe Update` 現在會取得檔案的路徑 `packages.config` ，並嘗試更新套件。</span><span class="sxs-lookup"><span data-stu-id="5742d-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="5742d-167">請注意，此更新的限制為不會： \* \* 更新、新增、移除專案檔中的內容。</span><span class="sxs-lookup"><span data-stu-id="5742d-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="5742d-168">\* \* 在封裝內執行 Powershell 腳本。</span><span class="sxs-lookup"><span data-stu-id="5742d-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="5742d-169">使用 nuget.exe 推送套件的 NuGet 伺服器支援</span><span class="sxs-lookup"><span data-stu-id="5742d-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="5742d-170">NuGet 包含簡單的方法，可透過 nuget 套件裝載 [輕量 web 型 NuGet 存放庫](../hosting-packages/nuget-server.md) `NuGet.Server` 。</span><span class="sxs-lookup"><span data-stu-id="5742d-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="5742d-171">使用 NuGet 1.4，輕量伺服器支援使用 nuget.exe 來推送和刪除封裝。</span><span class="sxs-lookup"><span data-stu-id="5742d-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="5742d-172">的最新版本會 `NuGet.Server` 新增 `appSetting` 名為的新 `apiKey` 。</span><span class="sxs-lookup"><span data-stu-id="5742d-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="5742d-173">當索引鍵省略或保留空白時，就會停用將套件推送至摘要的功能。</span><span class="sxs-lookup"><span data-stu-id="5742d-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="5742d-174">將 apiKey 設定為值 (理想的強式密碼) 使用 nuget.exe 來推送套件。</span><span class="sxs-lookup"><span data-stu-id="5742d-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="5742d-175">支援 Windows Phone Tools Mango Edition</span><span class="sxs-lookup"><span data-stu-id="5742d-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="5742d-176">Windows Phone Tools for Mango 的發行候選版本現在支援 NuGet。</span><span class="sxs-lookup"><span data-stu-id="5742d-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="5742d-177">Windows Phone 工具目前不支援 Visual Studio 的延伸模組管理員，因此若要安裝適用于 Windows Phone 工具的 NuGet，您可能需要手動下載並執行 VSIX。</span><span class="sxs-lookup"><span data-stu-id="5742d-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="5742d-178">若要卸載 Windows Phone 工具的 NuGet，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="5742d-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="5742d-179">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="5742d-179">Bug Fixes</span></span>
<span data-ttu-id="5742d-180">NuGet 1.4 總共修正了88個工作專案。</span><span class="sxs-lookup"><span data-stu-id="5742d-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="5742d-181">這些標記為 bug 的71。</span><span class="sxs-lookup"><span data-stu-id="5742d-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="5742d-182">如需 NuGet 1.4 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="5742d-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="5742d-183">Bug 修正值得注意：</span><span class="sxs-lookup"><span data-stu-id="5742d-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="5742d-184">[問題 603](http://nuget.codeplex.com/workitem/603)：指定特定套件來源時，跨不同存放庫的套件相依性可正確解析。</span><span class="sxs-lookup"><span data-stu-id="5742d-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="5742d-185">[問題 1036](http://nuget.codeplex.com/workitem/1036)：新增 `NuGet Pack SomeProject.csproj` 到後置建立事件不再造成無限迴圈。</span><span class="sxs-lookup"><span data-stu-id="5742d-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="5742d-186">[問題 961](http://nuget.codeplex.com/workitem/961)： `-Source` 旗標支援相對路徑。</span><span class="sxs-lookup"><span data-stu-id="5742d-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="5742d-187">NuGet 1.4 更新</span><span class="sxs-lookup"><span data-stu-id="5742d-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="5742d-188">在發行 NuGet 1.4 之後不久，我們發現有幾個重要的問題要修正。</span><span class="sxs-lookup"><span data-stu-id="5742d-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="5742d-189">此更新至1.4 的特定版本號碼為1.4.20615.9020。</span><span class="sxs-lookup"><span data-stu-id="5742d-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="5742d-190">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="5742d-190">Bug Fixes</span></span>
* <span data-ttu-id="5742d-191">[問題 1220](http://nuget.codeplex.com/workitem/1220)： `install.ps1` / `uninstall.ps1` 當有一個以上的專案時，Update-Package 不會在所有專案中執行</span><span class="sxs-lookup"><span data-stu-id="5742d-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="5742d-192">[問題 1156](http://nuget.codeplex.com/workitem/1156)：未安裝 Powershell 2 時，封裝管理員主控台卡在 W2K3/XP () </span><span class="sxs-lookup"><span data-stu-id="5742d-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
