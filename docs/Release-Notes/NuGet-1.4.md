---
title: NuGet 1.4 版本資訊 |Microsoft 文件
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.4。
keywords: NuGet 1.4 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1229cd7fddb826902478b69cfdbc16a8ed192b64
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="42fca-104">NuGet 1.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="42fca-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="42fca-105">[NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md) | [NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="42fca-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="42fca-106">NuGet 1.4 已於 2011 年 6 月 17 日發行。</span><span class="sxs-lookup"><span data-stu-id="42fca-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="42fca-107">功能</span><span class="sxs-lookup"><span data-stu-id="42fca-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="42fca-108">更新套件增強功能</span><span class="sxs-lookup"><span data-stu-id="42fca-108">Update-Package improvements</span></span>
<span data-ttu-id="42fca-109">NuGet 1.4 導入了許多增強功能輕鬆地保持在相同版本的封裝，跨多個專案方案中的 [更新套件] 命令。</span><span class="sxs-lookup"><span data-stu-id="42fca-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="42fca-110">例如，封裝升級至最新版本，時很常見，想要與相同 verision 更新已安裝該套件的所有專案。</span><span class="sxs-lookup"><span data-stu-id="42fca-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="42fca-111">`Update-Package`命令現在可讓您更輕鬆地：</span><span class="sxs-lookup"><span data-stu-id="42fca-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="42fca-112">更新單一專案中的所有套件</span><span class="sxs-lookup"><span data-stu-id="42fca-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="42fca-113">更新所有專案的封裝</span><span class="sxs-lookup"><span data-stu-id="42fca-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="42fca-114">更新所有專案中的所有套件</span><span class="sxs-lookup"><span data-stu-id="42fca-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="42fca-115">所有封裝執行的 「 安全 」 的更新</span><span class="sxs-lookup"><span data-stu-id="42fca-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="42fca-116">`-Safe`旗標限制只升級至具有相同主要和次要版本元件的唯一版本。</span><span class="sxs-lookup"><span data-stu-id="42fca-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="42fca-117">例如，若已安裝版本 1.0.0 的封裝，而摘要中有 1.0.1、 1.0.2 和 1.1 版`-Safe`旗標會將套件更新為 1.0.2。</span><span class="sxs-lookup"><span data-stu-id="42fca-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="42fca-118">升級，而`-Safe`旗標會將封裝升級至最新版本，也就是 1.1。</span><span class="sxs-lookup"><span data-stu-id="42fca-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="42fca-119">管理方案層級的封裝</span><span class="sxs-lookup"><span data-stu-id="42fca-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="42fca-120">NuGet 1.4 之前安裝的套件分成多個專案問世使用對話方塊。</span><span class="sxs-lookup"><span data-stu-id="42fca-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="42fca-121">您需要啟動 [一次每個專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="42fca-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="42fca-122">NuGet 1.4 同時在多個專案新增安裝/解除安裝/更新封裝的支援。</span><span class="sxs-lookup"><span data-stu-id="42fca-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="42fca-123">只要啟動以滑鼠右鍵按一下方案並選取**管理 NuGet 封裝**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="42fca-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![方案層級管理 NuGet 套件對話方塊](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="42fca-125">請注意，在對話方塊的標題列，會顯示方案的名稱，而不是專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="42fca-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="42fca-126">封裝作業現在會提供一份核取方塊，包含作業應套用至專案的清單。</span><span class="sxs-lookup"><span data-stu-id="42fca-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![管理 NuGet 封裝專案選取項目](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="42fca-128">如需詳細資訊，請參閱主題[解決方案的管理套件](../tools/package-manager-ui.md#managing-packages-for-the-solution)。</span><span class="sxs-lookup"><span data-stu-id="42fca-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="42fca-129">條件約束至允許的版本升級</span><span class="sxs-lookup"><span data-stu-id="42fca-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="42fca-130">根據預設，當執行`Update-Package`命令封裝 （或更新套件，對話方塊），將會更新摘要中的最新版本。</span><span class="sxs-lookup"><span data-stu-id="42fca-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="42fca-131">更新所有封裝的新支援，可能情況下，您要鎖定的特定版本範圍封裝。</span><span class="sxs-lookup"><span data-stu-id="42fca-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="42fca-132">例如，您可能事先知道您的應用程式將只使用版本 2.\*，但不是 3.0 和更新版本的封裝。</span><span class="sxs-lookup"><span data-stu-id="42fca-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="42fca-133">若要避免不小心更新為 3 的套件，NuGet 1.4 新增的條件約束可由手動編輯來升級封裝的版本範圍支援`packages.config`檔案使用新`allowedVersions`屬性。</span><span class="sxs-lookup"><span data-stu-id="42fca-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="42fca-134">例如，下列範例顯示如何鎖定`SomePackage`套件版本範圍 2.0 3.0 （獨佔）。</span><span class="sxs-lookup"><span data-stu-id="42fca-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="42fca-135">`allowedVersions`屬性接受的值使用[版本範圍格式](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="42fca-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="42fca-136">請注意，在 1.4，鎖定特定的版本範圍封裝必須手動編輯。</span><span class="sxs-lookup"><span data-stu-id="42fca-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="42fca-137">我們計劃 NuGet 1.5 中加入支援將透過此範圍`Install-Package`命令。</span><span class="sxs-lookup"><span data-stu-id="42fca-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="42fca-138">封裝的視覺化檢視</span><span class="sxs-lookup"><span data-stu-id="42fca-138">Package Visualizer</span></span>
<span data-ttu-id="42fca-139">新的封裝視覺化檢視，啟動透過**工具** -> **程式庫套件管理員** -> **封裝視覺化檢視**功能表選項，可讓您輕鬆地將所有專案與方案中的封裝相依性視覺化。</span><span class="sxs-lookup"><span data-stu-id="42fca-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="42fca-140">_**重要事項：**這項功能會利用 DGML 支援 Visual Studio 中。在 Visual Studio Ultimate 中才支援建立視覺效果。只支援在 Visual Studio Premium 或高階檢視 DGML 圖表。_</span><span class="sxs-lookup"><span data-stu-id="42fca-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![封裝的視覺化檢視](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="42fca-142">自動更新檢查 NuGet 對話方塊</span><span class="sxs-lookup"><span data-stu-id="42fca-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="42fca-143">某些版本的 NuGet 導入新的功能，以表示透過`.nuspec`較舊版本的 NuGet 對話方塊不了解的檔案。</span><span class="sxs-lookup"><span data-stu-id="42fca-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="42fca-144">其中一個範例是簡介 > 中的 NuGet 1.4[指定 framework 組件](../release-notes/nuget-1.2.md#framework-assembly-refs)。</span><span class="sxs-lookup"><span data-stu-id="42fca-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="42fca-145">基於此原因，是使用最新版的 NuGet 以確保您可以使用套件利用最新的功能。</span><span class="sxs-lookup"><span data-stu-id="42fca-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="42fca-146">若要更新 NuGet 更明顯可見，NuGet 對話方塊會包含邏輯，以較新版本可用時，反白顯示。</span><span class="sxs-lookup"><span data-stu-id="42fca-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="42fca-147">_**請注意**： 檢查只會**線上**已選取目前的工作階段中的索引標籤。_</span><span class="sxs-lookup"><span data-stu-id="42fca-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![管理與新的版本可用的 NuGet 套件 對話方塊](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="42fca-149">若要關閉自動檢查更新，請移至 [NuGet 設定] 對話方塊，並取消選取**自動檢查更新**。</span><span class="sxs-lookup"><span data-stu-id="42fca-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 設定](./media/nuget-settings.png)

<span data-ttu-id="42fca-151">這項功能實際上已加入 NuGet 1.3 但不是會顯示，而且當然 1.3，例如 NuGet 1.4 更新之前，已提供。</span><span class="sxs-lookup"><span data-stu-id="42fca-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="42fca-152">封裝管理員對話方塊改進</span><span class="sxs-lookup"><span data-stu-id="42fca-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="42fca-153">**改善的功能表名稱**： 更清楚，所以已重新命名功能表選項，以啟動對話方塊。</span><span class="sxs-lookup"><span data-stu-id="42fca-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="42fca-154">功能表選項現在是**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="42fca-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="42fca-155">**詳細資料 窗格會顯示最新的更新日期**: NuGet 對話方塊顯示封裝的詳細資料窗格中的最新的更新的日期時**線上**或**更新**選取索引標籤。</span><span class="sxs-lookup"><span data-stu-id="42fca-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="42fca-156">**顯示的標記清單**: Nuget 對話方塊會顯示標籤。</span><span class="sxs-lookup"><span data-stu-id="42fca-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="42fca-157">Powershell 增強功能</span><span class="sxs-lookup"><span data-stu-id="42fca-157">Powershell Improvements</span></span>
* <span data-ttu-id="42fca-158">**簽署的 PowerShell 指令碼**: NuGet 包含帶正負號的 Powershell 指令碼啟用更嚴格的環境中的使用量。</span><span class="sxs-lookup"><span data-stu-id="42fca-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="42fca-159">**提示支援**: Package Manager Console 現在支援透過提示`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令。</span><span class="sxs-lookup"><span data-stu-id="42fca-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="42fca-160">**封裝來源名稱**： 時，指定封裝來源，使用提供的套件來源名稱支援`-Source`旗標。</span><span class="sxs-lookup"><span data-stu-id="42fca-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="42fca-161">nuget.exe 命令列增強功能</span><span class="sxs-lookup"><span data-stu-id="42fca-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="42fca-162">**自訂的 NuGet 命令**: nuget.exe 是透過自訂的命令使用 MEF 可延伸。</span><span class="sxs-lookup"><span data-stu-id="42fca-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="42fca-163">**更簡單的工作流程建立符號封裝**:`-Symbols`旗標可套用至建立符號封裝只包括來源的一般慣例為基礎資料夾結構和`.pdb`資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="42fca-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="42fca-164">**指定多個來源**:`NuGet install`命令支援指定的分隔符號，或藉由指定使用分號分隔的多個來源`-Source`多次。</span><span class="sxs-lookup"><span data-stu-id="42fca-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="42fca-165">**Proxy 驗證支援**: NuGet 1.4 新增支援使用 NuGet 需要驗證的 proxy 後面時，提示使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="42fca-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="42fca-166">**nuget.exe 更新的重大變更**:`-Self`旗標現在是所需的 nuget.exe 自行更新。</span><span class="sxs-lookup"><span data-stu-id="42fca-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="42fca-167">`nuget.exe Update` 中的路徑現在採用`packages.config`檔案，並嘗試更新套件。</span><span class="sxs-lookup"><span data-stu-id="42fca-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="42fca-168">請注意，這項更新限制，則不會: * * 更新，新增、 移除內容中的專案檔。</span><span class="sxs-lookup"><span data-stu-id="42fca-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="42fca-169">* * 在封裝中的執行 Powershell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="42fca-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="42fca-170">使用 nuget.exe 推送封裝的 NuGet 伺服器支援</span><span class="sxs-lookup"><span data-stu-id="42fca-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="42fca-171">NuGet 包含簡單的方式來主機[輕量 web 型 NuGet 儲存機制](../hosting-packages/nuget-server.md)透過`NuGet.Server`NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="42fca-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="42fca-172">使用 NuGet 1.4 輕量型伺服器支援推入和刪除使用 nuget.exe 的封裝。</span><span class="sxs-lookup"><span data-stu-id="42fca-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="42fca-173">最新版`NuGet.Server`加入新`appSetting`具名`apiKey`。</span><span class="sxs-lookup"><span data-stu-id="42fca-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="42fca-174">索引鍵是省略或保留空白，將封裝推送到摘要會停用。</span><span class="sxs-lookup"><span data-stu-id="42fca-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="42fca-175">設定 apiKey 的值 （最好是強式密碼），可讓使用 nuget.exe 推送的封裝。</span><span class="sxs-lookup"><span data-stu-id="42fca-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="42fca-176">Windows Phone 工具 Mango 版本支援</span><span class="sxs-lookup"><span data-stu-id="42fca-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="42fca-177">NuGet 現在支援 Mango 的 Windows Phone 工具發行候選版本中。</span><span class="sxs-lookup"><span data-stu-id="42fca-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="42fca-178">目前，Windows Phone 工具並沒有支援的 Visual Studio 擴充功能管理員，因此若要安裝 Windows Phone 工具的 NuGet，您可能需要下載並手動執行 VSIX。</span><span class="sxs-lookup"><span data-stu-id="42fca-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="42fca-179">若要解除安裝 Windows Phone 工具的 NuGet，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="42fca-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="42fca-180">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="42fca-180">Bug Fixes</span></span>
<span data-ttu-id="42fca-181">NuGet 1.4 有工作項目固定 88 總數。</span><span class="sxs-lookup"><span data-stu-id="42fca-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="42fca-182">這些 71 已標示為錯誤。</span><span class="sxs-lookup"><span data-stu-id="42fca-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="42fca-183">如需完整的工作清單項目固定在 NuGet 1.4 中請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="42fca-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="42fca-184">值得注意的 bug 修正：</span><span class="sxs-lookup"><span data-stu-id="42fca-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="42fca-185">[問題 603](http://nuget.codeplex.com/workitem/603)： 跨不同的儲存機制的封裝相依性時，可以解決正確地指定特定的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="42fca-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="42fca-186">[問題 1036年](http://nuget.codeplex.com/workitem/1036)： 加入`NuGet Pack SomeProject.csproj`來建置後事件不會再造成無限迴圈。</span><span class="sxs-lookup"><span data-stu-id="42fca-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="42fca-187">[問題 961](http://nuget.codeplex.com/workitem/961):`-Source`旗標可支援相對路徑。</span><span class="sxs-lookup"><span data-stu-id="42fca-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="42fca-188">NuGet 1.4 更新</span><span class="sxs-lookup"><span data-stu-id="42fca-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="42fca-189">不久後 NuGet 1.4 版本中，我們可以發現幾個重要修正的問題。</span><span class="sxs-lookup"><span data-stu-id="42fca-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="42fca-190">這項更新 1.4 的特定版本號碼是 1.4.20615.9020。</span><span class="sxs-lookup"><span data-stu-id="42fca-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="42fca-191">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="42fca-191">Bug Fixes</span></span>
* <span data-ttu-id="42fca-192">[問題 1220年](http://nuget.codeplex.com/workitem/1220)： 不會執行更新套件`install.ps1` / `uninstall.ps1`多個專案時，所有專案中</span><span class="sxs-lookup"><span data-stu-id="42fca-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="42fca-193">[問題 1156年](http://nuget.codeplex.com/workitem/1156)： 封裝管理員主控台卡 W2K3/XP 上 （當未安裝 Powershell 2）</span><span class="sxs-lookup"><span data-stu-id="42fca-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
