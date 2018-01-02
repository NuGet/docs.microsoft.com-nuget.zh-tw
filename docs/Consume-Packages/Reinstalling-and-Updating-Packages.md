---
title: "重新安裝和更新 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2785879b-97f0-4a85-b3cc-bf4eaa5c39bf
description: "何時需要重新安裝和更新套件的詳細資料，與 Visual Studio 中的損毀套件參考相同。"
keywords: "NuGet 套件安裝、NuGet 套件重新安裝、NuGet 套件還原、更新套件、還原套件、修正損毀參考"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 898a431af4ed2e090b87d97bf43cec965b72d3c3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="how-to-reinstall-and-update-packages"></a><span data-ttu-id="0af9c-104">如何重新安裝和更新套件</span><span class="sxs-lookup"><span data-stu-id="0af9c-104">How to reinstall and update packages</span></span>

<span data-ttu-id="0af9c-105">在[重新安裝套件的時機](#when-to-reinstall-a-package)下方所述的許多情況中，Visual Studio 專案內套件的參考可能損毀。</span><span class="sxs-lookup"><span data-stu-id="0af9c-105">There are a number of situations, described below under [When to Reinstall a Package](#when-to-reinstall-a-package), where references to a package might get broken within a Visual Studio project.</span></span> <span data-ttu-id="0af9c-106">在這些情況下，解除安裝後重新安裝相同版本的套件，將會還原這些工作順序參考。</span><span class="sxs-lookup"><span data-stu-id="0af9c-106">In these cases, uninstalling and then reinstalling the same version of the package will restore those references to working order.</span></span> <span data-ttu-id="0af9c-107">更新套件，只是表示安裝更新的版本，這通常會還原套件的工作順序。</span><span class="sxs-lookup"><span data-stu-id="0af9c-107">Updating a package simply means installing an updated version, which often restores a package to working order.</span></span>

<span data-ttu-id="0af9c-108">更新和重新安裝套件已完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0af9c-108">Updating and reinstalling packages is accomplished as follows:</span></span>

| <span data-ttu-id="0af9c-109">方法</span><span class="sxs-lookup"><span data-stu-id="0af9c-109">Method</span></span> | <span data-ttu-id="0af9c-110">更新</span><span class="sxs-lookup"><span data-stu-id="0af9c-110">Update</span></span> | <span data-ttu-id="0af9c-111">重新安裝</span><span class="sxs-lookup"><span data-stu-id="0af9c-111">Reinstall</span></span> | 
| --- | --- | --- |
| <span data-ttu-id="0af9c-112">套件管理員主控台 (如[使用 Update-Package](#using-update-package) 中所述)</span><span class="sxs-lookup"><span data-stu-id="0af9c-112">Package Manager console (described in [Using Update-Package](#using-update-package))</span></span> | <span data-ttu-id="0af9c-113">`Update-Package` 命令</span><span class="sxs-lookup"><span data-stu-id="0af9c-113">`Update-Package` command</span></span> | <span data-ttu-id="0af9c-114">`Update-Package -reinstall` 命令</span><span class="sxs-lookup"><span data-stu-id="0af9c-114">`Update-Package -reinstall` command</span></span> |
| <span data-ttu-id="0af9c-115">套件管理員 UI</span><span class="sxs-lookup"><span data-stu-id="0af9c-115">Package Manager UI</span></span> | <span data-ttu-id="0af9c-116">在 [更新] 索引標籤上，選取一或多個套件，然後選取 [更新]</span><span class="sxs-lookup"><span data-stu-id="0af9c-116">On the **Updates** tab, select one or more packages and select **Update**</span></span> | <span data-ttu-id="0af9c-117">在 [已安裝] 索引標籤上，選取套件，並記錄其名稱，然後選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="0af9c-117">On the **Installed** tab, select a package, record its name, then select **Uninstall**.</span></span> <span data-ttu-id="0af9c-118">切換至 [瀏覽] 索引標籤，並搜尋套件名稱，再選取它，然後選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="0af9c-118">Switch to the **Browse** tab, search for the package name, select it, then select **Install**).</span></span> |
| <span data-ttu-id="0af9c-119">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="0af9c-119">nuget.exe CLI</span></span> | <span data-ttu-id="0af9c-120">`nuget update` 命令</span><span class="sxs-lookup"><span data-stu-id="0af9c-120">`nuget update` command</span></span> | <span data-ttu-id="0af9c-121">針對所有套件，刪除套件資料夾，然後執行 `nuget install`。</span><span class="sxs-lookup"><span data-stu-id="0af9c-121">For all packages, delete the package folder, then run `nuget install`.</span></span> <span data-ttu-id="0af9c-122">針對單一套件，刪除套件資料夾，然後使用 `nuget install <id>` 重新安裝相同套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-122">For a single package, delete the package folder and use `nuget install <id>` to reinstall the same one.</span></span> |

<span data-ttu-id="0af9c-123">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="0af9c-123">In this topic:</span></span>
- [<span data-ttu-id="0af9c-124">重新安裝套件的時機</span><span class="sxs-lookup"><span data-stu-id="0af9c-124">When to Reinstall a Package</span></span>](#when-to-reinstall-a-package)
- [<span data-ttu-id="0af9c-125">限制升級版本</span><span class="sxs-lookup"><span data-stu-id="0af9c-125">Constraining upgrade versions</span></span>](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a><span data-ttu-id="0af9c-126">重新安裝套件的時機</span><span class="sxs-lookup"><span data-stu-id="0af9c-126">When to Reinstall a Package</span></span>

1. <span data-ttu-id="0af9c-127">**套件還原之後參考損毀**：如果您已開啟專案並還原 NuGet 套件，但仍看到損毀參考，請嘗試重新安裝所有這些套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-127">**Broken references after package restore**: If you've opened a project and restored NuGet packages, but still see broken references, try reinstalling each of those packages.</span></span>
1. <span data-ttu-id="0af9c-128">**專案因已刪除檔案而中斷**：NuGet 不會防止您移除已從套件新增的項目，因此很容易不慎修改從套件安裝的內容，並中斷您的專案。</span><span class="sxs-lookup"><span data-stu-id="0af9c-128">**Project is broken due to deleted files**: NuGet does not prevent you from removing items added from packages, so it's easy to inadvertently modify contents installed from a package and break your project.</span></span> <span data-ttu-id="0af9c-129">若要還原專案，請重新安裝受影響的套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-129">To restore the project, reinstall the affected packages.</span></span>
1. <span data-ttu-id="0af9c-130">**套件更新中斷專案**：如果套件的更新中斷專案，則可能已存在的相依性套件一般會導致失敗。</span><span class="sxs-lookup"><span data-stu-id="0af9c-130">**Package update broke the project**: If an update to a package breaks a project, the failure is generally caused by a dependency package which may have also been.</span></span> <span data-ttu-id="0af9c-131">若要還原相依性的狀態，請重新安裝該特定套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-131">To restore the state of the dependency, reinstall that specific package.</span></span>
1. <span data-ttu-id="0af9c-132">**保護重設目標或升級**：已對專案重設目標或升級時，以及套件因目標架構變更而需要重新安裝時，這可能十分好用。</span><span class="sxs-lookup"><span data-stu-id="0af9c-132">**Project retargeting or upgrade**: This can be useful when a project has been retargeted or upgraded and if the package requires reinstallation due to the change in target framework.</span></span> <span data-ttu-id="0af9c-133">在這類情況下，NuGet 2.7 和更新版本會在專案重定目標之後立即顯示組建錯誤，而後續的組建警告可讓您知道可能需要重新安裝套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-133">NuGet 2.7 and later shows a build error in such cases immediately after project retargeting, and subsequent build warnings let you know that the package may need to be reinstalled.</span></span> <span data-ttu-id="0af9c-134">針對專案升級，NuGet 會在專案升級記錄中顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="0af9c-134">For project upgrade, NuGet shows an error in the Project Upgrade Log.</span></span>
1. <span data-ttu-id="0af9c-135">**在開發套件期間重新安裝套件**：套件作者通常需要重新安裝他們所開發以測試該行為之相同版本的套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-135">**Reinstalling a package during its development**: Package authors often need to reinstall the same version of package they're developing to test the behavior.</span></span> <span data-ttu-id="0af9c-136">`Install-Package` 命令未提供選項來強制重新安裝，因此請改用 `Update-Package -reinstall`。</span><span class="sxs-lookup"><span data-stu-id="0af9c-136">The `Install-Package` command does not provide an option to force a reinstall, so use `Update-Package -reinstall` instead.</span></span>

## <a name="constraining-upgrade-versions"></a><span data-ttu-id="0af9c-137">限制升級版本</span><span class="sxs-lookup"><span data-stu-id="0af9c-137">Constraining upgrade versions</span></span>

<span data-ttu-id="0af9c-138">重新安裝或更新套件預設「一律」會安裝套件來源中可用的最新版本。</span><span class="sxs-lookup"><span data-stu-id="0af9c-138">By default, reinstalling or updating a package *always* installs the latest version available from the package source.</span></span>

<span data-ttu-id="0af9c-139">不過，在使用 `packages.config` 參考格式的專案中，您可以特別限制版本範圍。</span><span class="sxs-lookup"><span data-stu-id="0af9c-139">In projects using the `packages.config` reference format, however, you can specifically constrain the version range.</span></span> <span data-ttu-id="0af9c-140">例如，如果您知道您的應用程式僅適用於 1.x 版的套件，而不是 2.0 和更新版本 (可能是套件 API 中的主要變更所造成)，則會想要限制 1.x 版的升級。</span><span class="sxs-lookup"><span data-stu-id="0af9c-140">For example, if you know that your application works only with version 1.x of a package but not 2.0 and above, perhaps due to a major change in the package API, then you'd want to constrain upgrades to 1.x versions.</span></span> <span data-ttu-id="0af9c-141">這可避免破壞應用程式的意外更新。</span><span class="sxs-lookup"><span data-stu-id="0af9c-141">This prevents accidental updates that would break the application.</span></span>

<span data-ttu-id="0af9c-142">若要設定條件約束，請在文字編輯器中開啟 `packages.config`，並找到有問題的相依性，然後使用版本範圍新增 `allowedVersions` 屬性。</span><span class="sxs-lookup"><span data-stu-id="0af9c-142">To set a constraint, open `packages.config` in a text editor, locate the dependency in question, and add the `allowedVersions` attribute with a version range.</span></span> <span data-ttu-id="0af9c-143">例如，若要限制 1.x 版的更新，請將 `allowedVersions` 設定為 `[1,2)`：</span><span class="sxs-lookup"><span data-stu-id="0af9c-143">For example, to constrain updates to version 1.x, set `allowedVersions` to `[1,2)`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

<span data-ttu-id="0af9c-144">在所有情況下，都請使用[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中所述的標記法。</span><span class="sxs-lookup"><span data-stu-id="0af9c-144">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-update-package"></a><span data-ttu-id="0af9c-145">使用 Update-Package</span><span class="sxs-lookup"><span data-stu-id="0af9c-145">Using Update-Package</span></span>

<span data-ttu-id="0af9c-146">請注意下面所述的[考量](#considerations)，您可以在 Visual Studio 套件管理員主控台中使用 [Update-Package 命令](../Tools/ps-ref-update-package.md)，輕鬆地重新安裝任何套件 ([工具] > [NuGet 套件管理員] > [套件管理員主控台])：</span><span class="sxs-lookup"><span data-stu-id="0af9c-146">Being mindful of the [Considerations](#considerations) described below, you can easily reinstall any package using the [Update-Package command](../Tools/ps-ref-update-package.md) in the Visual Studio Package Manager Console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

```ps
Update-Package -Id <package_name> –reinstall
```

<span data-ttu-id="0af9c-147">使用此命令，會比移除套件後嘗試使用相同的版本在 NuGet 資源庫中找到相同的套件更為簡單。</span><span class="sxs-lookup"><span data-stu-id="0af9c-147">Using this command is much easier than removing a package and then trying to locate the same package in the NuGet gallery with the same version.</span></span> <span data-ttu-id="0af9c-148">請注意，`-Id` 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="0af9c-148">Note that the `-Id` switch is optional.</span></span>

<span data-ttu-id="0af9c-149">沒有 `-reinstall` 的相同命令會將套件更新為較新版本 (適用時)。</span><span class="sxs-lookup"><span data-stu-id="0af9c-149">The same command without `-reinstall` updates a package to a newer version, if applicable.</span></span> <span data-ttu-id="0af9c-150">如果專案中尚未安裝有問題的套件，則此命令會顯示錯誤；也就是說，`Update-Package` 不會直接安裝套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-150">The command gives an error if the package in question is not already installed in a project; that is, `Update-Package` does not install packages directly.</span></span>

```ps
Update-Package <package_name>
```

<span data-ttu-id="0af9c-151">`Update-Package` 預設會影響方案中的所有套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-151">By default, `Update-Package` affects all packages in a solution.</span></span> <span data-ttu-id="0af9c-152">若要將動作限制為特定專案，請使用 `-ProjectName` 參數，並使用出現在方案總管中的專案名稱：</span><span class="sxs-lookup"><span data-stu-id="0af9c-152">To limit the action to a specific project, use the `-ProjectName` switch, using the name of the project as it appears in Solution Explorer:</span></span>

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```
<span data-ttu-id="0af9c-153">若要「更新」專案中的所有套件 (或使用 `-reinstall` 重新安裝)，請使用 `-ProjectName`，而不指定任何特定套件：</span><span class="sxs-lookup"><span data-stu-id="0af9c-153">To *update* all packages in a project (or reinstall using `-reinstall`), use `-ProjectName` without specifying any particular package:</span></span>

```ps
Update-Package -ProjectName MyProject
```

<span data-ttu-id="0af9c-154">若要更新方案中的所有套件，只需要使用 `Update-Package` 本身，而沒有其他引數或參數。</span><span class="sxs-lookup"><span data-stu-id="0af9c-154">To update all packages in a solution, just use `Update-Package` by itself with no other arguments or switches.</span></span> <span data-ttu-id="0af9c-155">請小心使用此表單，因為它可能需要相當長的時間才能執行所有更新：</span><span class="sxs-lookup"><span data-stu-id="0af9c-155">Use this form carefully, because it can take considerable time to perform all the updates:</span></span>

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

<span data-ttu-id="0af9c-156">使用 `project.json` 或[專案檔中的套件參考](../Consume-Packages/Package-References-in-Project-Files.md)來更新專案或方案中的套件，一律會更新為套件的最新版本 (發行前套件除外)。</span><span class="sxs-lookup"><span data-stu-id="0af9c-156">Updating packages in a project or solution using `project.json` or [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) always updates to the latest version of the package (excluding pre-release packages).</span></span> <span data-ttu-id="0af9c-157">如有需要，使用 `packages.config` 的專案可以限制下面[限制升級版本](#constraining-upgrade-versions)中所述的更新版本。</span><span class="sxs-lookup"><span data-stu-id="0af9c-157">Projects that use `packages.config` can, if desired, limit update versions as described below in [Constraining upgrade versions](#constraining-upgrade-versions).</span></span>

<span data-ttu-id="0af9c-158">如需命令的完整詳細資料，請參閱 [Update-Package](../Tools/ps-ref-update-package.md) 參考。</span><span class="sxs-lookup"><span data-stu-id="0af9c-158">For full details on the command, see the [Update-Package](../Tools/ps-ref-update-package.md) reference.</span></span>

### <a name="considerations"></a><span data-ttu-id="0af9c-159">考量</span><span class="sxs-lookup"><span data-stu-id="0af9c-159">Considerations</span></span>

<span data-ttu-id="0af9c-160">重新安裝套件時，下列可能會受到影響：</span><span class="sxs-lookup"><span data-stu-id="0af9c-160">The following may be affected when reinstalling a package:</span></span>

1. <span data-ttu-id="0af9c-161">**根據專案目標架構重設目標來重新安裝套件**</span><span class="sxs-lookup"><span data-stu-id="0af9c-161">**Reinstalling packages according to project target framework retargeting**</span></span>
    - <span data-ttu-id="0af9c-162">在簡單的情況下，使用 `Update-Package –reinstall <package_name>` 重新安裝套件就能運作。</span><span class="sxs-lookup"><span data-stu-id="0af9c-162">In a simple case, just reinstalling a package using `Update-Package –reinstall <package_name>` works.</span></span> <span data-ttu-id="0af9c-163">解除安裝針對舊目標架構所安裝的套件，並針對專案的目前目標架構安裝相同套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-163">A package that is installed against an old target framework gets uninstalled and the same package gets installed against the current target framework of the project.</span></span>
    - <span data-ttu-id="0af9c-164">在某些情況下，可能會有不支援新目標架構的套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-164">In some cases, there may be a package that does not support the new target framework.</span></span>
        - <span data-ttu-id="0af9c-165">如果套件支援可攜式類別庫 (PCL)，並將專案的目標重設為套件不再支援的平台組合，則套件的參考會在重新安裝之後遺失。</span><span class="sxs-lookup"><span data-stu-id="0af9c-165">If a package supports portable class libraries (PCLs) and the project is retargeted to a combination of platforms no longer supported by the package, references to the package will be missing after reinstalling.</span></span>
        - <span data-ttu-id="0af9c-166">這可能會出現您直接使用的套件，或作為相依性而安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-166">This can surface for packages you're using directly or for packages installed as dependencies.</span></span> <span data-ttu-id="0af9c-167">您使用的套件可能會直接支援新的目標架構，而其相依性則否。</span><span class="sxs-lookup"><span data-stu-id="0af9c-167">It's possible for the package you're using directly to support the new target framework while its dependency does not.</span></span>
        - <span data-ttu-id="0af9c-168">如果在重設應用程式的目標之後重新安裝套件導致組建或執行階段錯誤，您可能需要還原目標架構，或搜尋正確支援新目標架構的替代套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-168">If reinstalling packages after retargeting your application results in build or runtime errors, you may need to revert your target framework or search for alternative packages that properly support your new target framework.</span></span>

1. <span data-ttu-id="0af9c-169">**專案重設目標或升級之後 packages.config 中所新增的 requireReinstallation 屬性**</span><span class="sxs-lookup"><span data-stu-id="0af9c-169">**requireReinstallation attribute added in packages.config after project retargeting or upgrade**</span></span>
    - <span data-ttu-id="0af9c-170">如果 NuGet 偵測到重設目標或升級專案已影響套件，則會將 `packages.config` 中的 `requireReinstallation="true"` 屬性新增至所有受影響的套件參考。</span><span class="sxs-lookup"><span data-stu-id="0af9c-170">If NuGet detects that packages were affected by retargeting or upgrading a project, it adds a `requireReinstallation="true"` attribute in  `packages.config` to all affected package references.</span></span> <span data-ttu-id="0af9c-171">因此，Visual Studio 中的每個後續組建都會引發這些套件的組建警告，讓您可以記得重新安裝它們。</span><span class="sxs-lookup"><span data-stu-id="0af9c-171">Because of this, each subsequent build in Visual Studio raises build warnings for those packages so you can remember to reinstall them.</span></span>

1. <span data-ttu-id="0af9c-172">**使用相依性重新安裝套件**</span><span class="sxs-lookup"><span data-stu-id="0af9c-172">**Reinstalling packages with dependencies**</span></span>
    - <span data-ttu-id="0af9c-173">`Update-Package –reinstall` 會重新安裝相同版本的原始套件，但除非提供特定版本條件約束，否則會安裝最新版本的相依性。</span><span class="sxs-lookup"><span data-stu-id="0af9c-173">`Update-Package –reinstall` reinstalls the same version of the original package, but installs the latest version of dependencies unless specific version constraints are provided.</span></span> <span data-ttu-id="0af9c-174">這可讓您視需要僅更新相依性，以修正問題。</span><span class="sxs-lookup"><span data-stu-id="0af9c-174">This allows you to update only the dependencies as required to fix an issue.</span></span> <span data-ttu-id="0af9c-175">不過，如果這會將相依性復原為舊版本，則您可以使用 `Update-Package <dependency_name>` 重新安裝該相依性，而不影響相依的套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-175">However, if this rolls a dependency back to an earlier version, you can use `Update-Package <dependency_name>` to reinstall that one dependency without affecting the dependent package.</span></span>
    - <span data-ttu-id="0af9c-176">`Update-Package –reinstall <packageName> -ignoreDependencies` 會重新安裝相同版本的原始套件，但不重新安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="0af9c-176">`Update-Package –reinstall <packageName> -ignoreDependencies` reinstalls the same version of the original package but does not reinstall dependencies.</span></span> <span data-ttu-id="0af9c-177">更新套件相依性可能導致中斷狀態時，請使用此項目</span><span class="sxs-lookup"><span data-stu-id="0af9c-177">Use this when updating package dependencies might result in a broken state</span></span>

1. <span data-ttu-id="0af9c-178">**在涉及相依的版本時重新安裝套件**</span><span class="sxs-lookup"><span data-stu-id="0af9c-178">**Reinstalling packages when dependent versions are involved**</span></span>
    - <span data-ttu-id="0af9c-179">如上所述，重新安裝套件時不會變更與其相依之任何其他已安裝套件的版本。</span><span class="sxs-lookup"><span data-stu-id="0af9c-179">As explained above, reinstalling a package does not change versions of any other installed packages that depend on it.</span></span> <span data-ttu-id="0af9c-180">接著，重新安裝相依性可能會中斷相依的套件。</span><span class="sxs-lookup"><span data-stu-id="0af9c-180">It's possible, then, that reinstalling a dependency could break the dependent package.</span></span>

