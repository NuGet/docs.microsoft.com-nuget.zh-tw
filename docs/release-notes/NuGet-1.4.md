---
title: NuGet 1.4 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.4 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550627"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="86bb0-103">NuGet 1.4 的版本資訊</span><span class="sxs-lookup"><span data-stu-id="86bb0-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="86bb0-104">[NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md) | [NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="86bb0-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="86bb0-105">於 2011 年 6 月 17 日發行 NuGet 1.4。</span><span class="sxs-lookup"><span data-stu-id="86bb0-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="86bb0-106">功能</span><span class="sxs-lookup"><span data-stu-id="86bb0-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="86bb0-107">更新套件改善</span><span class="sxs-lookup"><span data-stu-id="86bb0-107">Update-Package improvements</span></span>
<span data-ttu-id="86bb0-108">NuGet 1.4 導入了許多增強功能讓您更輕鬆地保持相同的版本中的封裝，在方案中的多個專案的 [更新套件] 命令。</span><span class="sxs-lookup"><span data-stu-id="86bb0-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="86bb0-109">例如，升級為最新版本的封裝，時很常見，要更新為相同 verision 已安裝該套件的所有專案。</span><span class="sxs-lookup"><span data-stu-id="86bb0-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="86bb0-110">`Update-Package`命令現在可讓您更輕鬆地：</span><span class="sxs-lookup"><span data-stu-id="86bb0-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="86bb0-111">更新單一專案中的所有封裝</span><span class="sxs-lookup"><span data-stu-id="86bb0-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="86bb0-112">更新所有專案中的套件</span><span class="sxs-lookup"><span data-stu-id="86bb0-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="86bb0-113">更新所有專案中的所有封裝</span><span class="sxs-lookup"><span data-stu-id="86bb0-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="86bb0-114">所有封裝執行的 「 安全 」 的更新</span><span class="sxs-lookup"><span data-stu-id="86bb0-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="86bb0-115">`-Safe`旗標限制升級至具有相同的主要和次要版本元件的唯一版本。</span><span class="sxs-lookup"><span data-stu-id="86bb0-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="86bb0-116">例如，如果已安裝版本 1.0.0 的封裝，而有版本 1.0.1、 1.0.2 與 1.1 可用的摘要中`-Safe`旗標將此封裝更新至 1.0.2。</span><span class="sxs-lookup"><span data-stu-id="86bb0-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="86bb0-117">升級不含`-Safe`旗標會將套件升級為最新版本，也就是 1.1。</span><span class="sxs-lookup"><span data-stu-id="86bb0-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="86bb0-118">方案層級的管理套件</span><span class="sxs-lookup"><span data-stu-id="86bb0-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="86bb0-119">在 NuGet 1.4 之前套件安裝至多個專案十分麻煩使用對話方塊。</span><span class="sxs-lookup"><span data-stu-id="86bb0-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="86bb0-120">您需要啟動每一次的專案 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="86bb0-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="86bb0-121">NuGet 1.4 會新增多個專案中安裝/解除安裝/更新封裝的支援，在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="86bb0-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="86bb0-122">只要啟動方案上按一下滑鼠右鍵，然後選取**管理 NuGet 套件**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="86bb0-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![方案層級管理 NuGet 套件 對話方塊](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="86bb0-124">請注意，在對話方塊的標題列中，會顯示方案的名稱，而不是專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="86bb0-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="86bb0-125">封裝作業現在會提供核取方塊的清單作業應該套用到專案的清單。</span><span class="sxs-lookup"><span data-stu-id="86bb0-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![管理 NuGet 封裝專案選取項目](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="86bb0-127">如需詳細資訊，請參閱主題[管理方案的套件](../tools/package-manager-ui.md#managing-packages-for-the-solution)。</span><span class="sxs-lookup"><span data-stu-id="86bb0-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="86bb0-128">限制升級至允許的版本</span><span class="sxs-lookup"><span data-stu-id="86bb0-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="86bb0-129">根據預設，當執行`Update-Package`命令封裝 （或更新套件，對話方塊），將會更新為最新的版本，摘要中。</span><span class="sxs-lookup"><span data-stu-id="86bb0-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="86bb0-130">更新所有封裝的新支援，可能情況下您想要鎖定在特定版本範圍內的封裝。</span><span class="sxs-lookup"><span data-stu-id="86bb0-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="86bb0-131">例如，您可能事先知道您的應用程式只會使用 2.\* 版的封裝，但不是 3.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="86bb0-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="86bb0-132">為了防止意外更新為 3 的套件，NuGet 1.4 新增對限制的封裝可以升級為，透過手動編輯的版本範圍`packages.config`檔案中，使用新`allowedVersions`屬性。</span><span class="sxs-lookup"><span data-stu-id="86bb0-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="86bb0-133">例如，下列範例顯示如何鎖定`SomePackage`套件版本範圍 2.0-3.0 （獨佔）。</span><span class="sxs-lookup"><span data-stu-id="86bb0-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="86bb0-134">`allowedVersions`屬性可接受的值使用[版本範圍格式](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="86bb0-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="86bb0-135">請注意，在 1.4，鎖定特定版本範圍封裝必須手動編輯。</span><span class="sxs-lookup"><span data-stu-id="86bb0-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="86bb0-136">我們計劃 NuGet 1.5 中加入此支援將透過此範圍`Install-Package`命令。</span><span class="sxs-lookup"><span data-stu-id="86bb0-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="86bb0-137">封裝視覺化檢視</span><span class="sxs-lookup"><span data-stu-id="86bb0-137">Package Visualizer</span></span>
<span data-ttu-id="86bb0-138">新的封裝視覺化檢視，透過啟動**工具** -> **程式庫套件管理員** -> **封裝視覺化檢視**功能表選項，可讓您輕鬆地以視覺化方式檢視所有專案和其解決方案中的封裝相依性。</span><span class="sxs-lookup"><span data-stu-id="86bb0-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="86bb0-139">_**重要事項：** 這項功能會利用 DGML 支援中的 Visual Studio。在 Visual Studio Ultimate 中才支援建立視覺效果。檢視 DGML 圖表僅適用於 Visual Studio Premium 或高等教育中。_</span><span class="sxs-lookup"><span data-stu-id="86bb0-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![封裝視覺化檢視](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="86bb0-141">[NuGet] 對話方塊中的自動更新檢查</span><span class="sxs-lookup"><span data-stu-id="86bb0-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="86bb0-142">某些版本的 NuGet 引進新功能，透過表示`.nuspec`不了解舊版 NuGet 對話方塊的檔案。</span><span class="sxs-lookup"><span data-stu-id="86bb0-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="86bb0-143">其中一個範例是在 NuGet 1.4 的簡介[指定 framework 組件](../release-notes/nuget-1.2.md#framework-assembly-refs)。</span><span class="sxs-lookup"><span data-stu-id="86bb0-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="86bb0-144">基於這個原因，請務必使用最新版的 NuGet，以確保您可以使用套件利用最新的功能。</span><span class="sxs-lookup"><span data-stu-id="86bb0-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="86bb0-145">若要讓 NuGet 的更新更明顯可見，NuGet 對話方塊會包含更新的版本時反白顯示的邏輯。</span><span class="sxs-lookup"><span data-stu-id="86bb0-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="86bb0-146">_**附註**： 如果，才有核取**Online**目前工作階段中已選取索引標籤。_</span><span class="sxs-lookup"><span data-stu-id="86bb0-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![[管理 NuGet 套件] 對話方塊，可用的新版本](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="86bb0-148">若要關閉自動檢查更新，請移至 NuGet 的 [設定] 對話方塊，並取消核取**自動檢查更新**。</span><span class="sxs-lookup"><span data-stu-id="86bb0-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 設定](./media/nuget-settings.png)

<span data-ttu-id="86bb0-150">這項功能實際上已加入 NuGet 1.3，但就不會顯示，當然，1.3，例如 NuGet 1.4 的更新，所提供。</span><span class="sxs-lookup"><span data-stu-id="86bb0-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="86bb0-151">套件管理員 對話方塊改良</span><span class="sxs-lookup"><span data-stu-id="86bb0-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="86bb0-152">**改善的功能表名稱**： 為了清楚起見已重新命名功能表選項，以啟動對話方塊。</span><span class="sxs-lookup"><span data-stu-id="86bb0-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="86bb0-153">功能表選項現**管理 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="86bb0-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="86bb0-154">**詳細資料 窗格會顯示最新的更新日期**: NuGet 對話方塊會顯示封裝的詳細資料窗格中的最新的更新的日期時**Online**或是**更新**選取索引標籤。</span><span class="sxs-lookup"><span data-stu-id="86bb0-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="86bb0-155">**顯示的標記清單**: Nuget 對話方塊就會顯示標籤。</span><span class="sxs-lookup"><span data-stu-id="86bb0-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="86bb0-156">Powershell 增強功能</span><span class="sxs-lookup"><span data-stu-id="86bb0-156">Powershell Improvements</span></span>
* <span data-ttu-id="86bb0-157">**簽署的 PowerShell 指令碼**: NuGet 包含帶正負號的 Powershell 指令碼啟用更嚴格的環境中的使用量。</span><span class="sxs-lookup"><span data-stu-id="86bb0-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="86bb0-158">**提示支援**: 套件管理員主控台現在支援透過提示`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令。</span><span class="sxs-lookup"><span data-stu-id="86bb0-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="86bb0-159">**套件來源名稱**： 提供的套件來源的名稱指定套件來源使用時，支援`-Source`旗標。</span><span class="sxs-lookup"><span data-stu-id="86bb0-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="86bb0-160">nuget.exe 命令列改進功能</span><span class="sxs-lookup"><span data-stu-id="86bb0-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="86bb0-161">**NuGet 的自訂命令**: nuget.exe 可透過使用 MEF 的自訂命令。</span><span class="sxs-lookup"><span data-stu-id="86bb0-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="86bb0-162">**更簡單的工作流程建立符號套件**:`-Symbols`旗標可以用來建立符號套件僅包含來源的一般慣例為基礎資料夾結構和`.pdb`資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="86bb0-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="86bb0-163">**指定多個來源**:`NuGet install`命令支援指定多個使用分號作為分隔符號，或藉由指定的來源`-Source`多次。</span><span class="sxs-lookup"><span data-stu-id="86bb0-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="86bb0-164">**Proxy 驗證支援**: NuGet 1.4 新增對需要驗證的 proxy 後方使用 NuGet 時提示使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="86bb0-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="86bb0-165">**nuget.exe 更新的重大變更**:`-Self`現在是旗標所需的 nuget.exe 更新本身。</span><span class="sxs-lookup"><span data-stu-id="86bb0-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="86bb0-166">`nuget.exe Update` 現在會採用的路徑`packages.config`檔案，並將嘗試更新套件。</span><span class="sxs-lookup"><span data-stu-id="86bb0-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="86bb0-167">請注意，這項更新限制，則不會: * * 更新，新增、 移除專案檔案中的內容。</span><span class="sxs-lookup"><span data-stu-id="86bb0-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="86bb0-168">* * 封裝內的執行 Powershell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="86bb0-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="86bb0-169">使用 nuget.exe 推送套件的 NuGet 伺服器支援</span><span class="sxs-lookup"><span data-stu-id="86bb0-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="86bb0-170">NuGet 包含簡單的方式來裝載[輕量 web 型 NuGet 存放庫](../hosting-packages/nuget-server.md)透過`NuGet.Server`NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="86bb0-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="86bb0-171">使用 NuGet 1.4 輕量級伺服器支援推送和刪除使用 nuget.exe 的封裝。</span><span class="sxs-lookup"><span data-stu-id="86bb0-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="86bb0-172">最新版`NuGet.Server`將新`appSetting`具名`apiKey`。</span><span class="sxs-lookup"><span data-stu-id="86bb0-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="86bb0-173">當索引鍵是省略或留白時，會停用將套件推送至摘要。</span><span class="sxs-lookup"><span data-stu-id="86bb0-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="86bb0-174">設定 apiKey 的值 （在理想情況下是強式密碼），可讓使用 nuget.exe 推送套件。</span><span class="sxs-lookup"><span data-stu-id="86bb0-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="86bb0-175">適用於 Windows Phone 工具 Mango Edition 的支援</span><span class="sxs-lookup"><span data-stu-id="86bb0-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="86bb0-176">NuGet 現在支援 Windows Phone Mango 工具發行候選版本中。</span><span class="sxs-lookup"><span data-stu-id="86bb0-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="86bb0-177">目前，Windows Phone 工具並沒有 Visual Studio 擴充功能管理員，因此，若要安裝 Windows Phone 工具的 NuGet 支援，您可能需要下載並手動執行 VSIX。</span><span class="sxs-lookup"><span data-stu-id="86bb0-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="86bb0-178">若要解除安裝 NuGet for Windows Phone 工具，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="86bb0-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="86bb0-179">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="86bb0-179">Bug Fixes</span></span>
<span data-ttu-id="86bb0-180">NuGet 1.4 有工作項目固定為 88 總計。</span><span class="sxs-lookup"><span data-stu-id="86bb0-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="86bb0-181">這些 71 已標示為錯誤。</span><span class="sxs-lookup"><span data-stu-id="86bb0-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="86bb0-182">如需完整的工作清單項目固定在 NuGet 1.4，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="86bb0-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="86bb0-183">值得注意的錯誤修正：</span><span class="sxs-lookup"><span data-stu-id="86bb0-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="86bb0-184">[問題 603](http://nuget.codeplex.com/workitem/603)： 跨不同的存放庫的套件相依性時，可以解決正確地指定特定的套件來源。</span><span class="sxs-lookup"><span data-stu-id="86bb0-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="86bb0-185">[問題 1036年](http://nuget.codeplex.com/workitem/1036)： 新增`NuGet Pack SomeProject.csproj`來建置後事件不會再造成無限迴圈。</span><span class="sxs-lookup"><span data-stu-id="86bb0-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="86bb0-186">[問題 961](http://nuget.codeplex.com/workitem/961):`-Source`旗標支援相對路徑。</span><span class="sxs-lookup"><span data-stu-id="86bb0-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="86bb0-187">NuGet 1.4 更新</span><span class="sxs-lookup"><span data-stu-id="86bb0-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="86bb0-188">不久後 NuGet 1.4 的版本中，我們會發現幾個重要修正的問題。</span><span class="sxs-lookup"><span data-stu-id="86bb0-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="86bb0-189">這項更新 1.4 的特定版本號碼是 1.4.20615.9020。</span><span class="sxs-lookup"><span data-stu-id="86bb0-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="86bb0-190">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="86bb0-190">Bug Fixes</span></span>
* <span data-ttu-id="86bb0-191">[問題 1220年](http://nuget.codeplex.com/workitem/1220)： 不會執行更新套件`install.ps1` / `uninstall.ps1`中有多個專案時的所有專案</span><span class="sxs-lookup"><span data-stu-id="86bb0-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="86bb0-192">[問題 1156年](http://nuget.codeplex.com/workitem/1156): W2K3/XP 上 （未安裝 Powershell 第 2） 時停滯的套件管理員主控台</span><span class="sxs-lookup"><span data-stu-id="86bb0-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
