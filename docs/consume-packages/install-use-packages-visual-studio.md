---
title: 在 Visual Studio 中安裝和管理 NuGet 套件
description: 使用 Visual Studio 中的 NuGet 套件管理員 UI 來處理 NuGet 套件的指示。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231003"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="54764-103">在 Visual Studio 中，使用 NuGet 套件管理員來安裝和管理套件</span><span class="sxs-lookup"><span data-stu-id="54764-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="54764-104">Visual Studio 中的 NuGet 套件管理員 UI 可讓您在專案和解決方案中，輕鬆地安裝、解除安裝和更新 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="54764-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="54764-105">如需 Visual Studio for Mac 中的體驗，請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)。</span><span class="sxs-lookup"><span data-stu-id="54764-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="54764-106">套件管理員 UI 未隨附於 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="54764-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="54764-107">如果您在 Visual Studio 2015 中遺漏 NuGet 套件管理員，請查看 [工具] > [擴充功能和更新]，然後搜尋「NuGet 套件管理員」擴充功能。</span><span class="sxs-lookup"><span data-stu-id="54764-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="54764-108">如果您無法在 Visual Studio 中使用擴充功能安裝程式，請直接從 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) \(英文\) 下載擴充功能。</span><span class="sxs-lookup"><span data-stu-id="54764-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="54764-109">從 Visual Studio 2017 開始，NuGet 和 NuGet 套件管理員會隨任何 .NET 相關的工作負載自動安裝。</span><span class="sxs-lookup"><span data-stu-id="54764-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="54764-110">若要個別地安裝，請在 Visual Studio 安裝程式中選取 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 選項。</span><span class="sxs-lookup"><span data-stu-id="54764-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="54764-111">尋找並安裝套件</span><span class="sxs-lookup"><span data-stu-id="54764-111">Find and install a package</span></span>

1. <span data-ttu-id="54764-112">在 [方案總管] 中，以滑鼠右鍵按一下 [參考] 或專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="54764-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![[管理 NuGet 套件] 功能表選項](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="54764-114">[瀏覽] 索引標籤會依熱門度顯示目前所選來源的套件 (請參閱[套件來源](#package-sources))。</span><span class="sxs-lookup"><span data-stu-id="54764-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="54764-115">使用左上方的搜尋方塊來搜尋特定套件。</span><span class="sxs-lookup"><span data-stu-id="54764-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="54764-116">從清單中選取套件以顯示其資訊，這也會啟用 [安裝] 按鈕和版本選擇下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="54764-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![管理 NuGet 套件對話方塊 [瀏覽] 索引標籤](media/Search.png)

1. <span data-ttu-id="54764-118">從下拉式清單選取所需的版本然後選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="54764-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="54764-119">Visual Studio 會將套件及其相依性安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="54764-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="54764-120">系統可能會要求您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="54764-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="54764-121">安裝完成時，新增的封裝會出現在 [**已安裝**] 索引標籤上。套件也會列在方案總管的 [**參考**] 節點中，表示您可以在專案中使用 `using` 的語句來參考它們。</span><span class="sxs-lookup"><span data-stu-id="54764-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![方案總管中的 [參考]](media/References.png)

> [!Tip]
> <span data-ttu-id="54764-123">若要在搜尋中包含發行前版本，並且讓發行前版本可在 [版本] 下拉式清單中取得，請選取 [包含發行前版本] 選項。</span><span class="sxs-lookup"><span data-stu-id="54764-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="54764-124">NuGet 有兩種格式，可供專案使用封裝： [`PackageReference`](package-references-in-project-files.md)和[`packages.config`](../reference/packages-config.md)。</span><span class="sxs-lookup"><span data-stu-id="54764-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="54764-125">[預設值可以在 Visual Studio 的 [選項] 視窗中設定](Package-Restore.md#choose-default-package-management-format)。</span><span class="sxs-lookup"><span data-stu-id="54764-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="54764-126">解除安裝套件</span><span class="sxs-lookup"><span data-stu-id="54764-126">Uninstall a package</span></span>

1. <span data-ttu-id="54764-127">在 [方案總管] 中，以滑鼠右鍵按一下 [參考] 或所需的專案，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="54764-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="54764-128">選取 [已安裝] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="54764-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="54764-129">選取要解除安裝的套件 (如有必要，請使用搜尋功能篩選清單)，然後選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="54764-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![將套件解除安裝](media/UninstallPackage.png)

1. <span data-ttu-id="54764-131">請注意，將套件解除安裝時，[包含發行前版本] 和 [套件來源] 控制項沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="54764-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="54764-132">更新套件</span><span class="sxs-lookup"><span data-stu-id="54764-132">Update a package</span></span>

1. <span data-ttu-id="54764-133">在**方案總管**中，以滑鼠右鍵按一下 [**參考**] 或所需的專案，然後選取 [**管理 NuGet 套件 ...**]。（在網站專案中，以滑鼠右鍵按一下 [ **Bin** ] 資料夾）。</span><span class="sxs-lookup"><span data-stu-id="54764-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="54764-134">選取 [更新] 索引標籤，以查看在所選套件來源有可用更新的套件。</span><span class="sxs-lookup"><span data-stu-id="54764-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="54764-135">選取 [包含發行前版本]，以在更新清單中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="54764-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="54764-136">選取要更新的套件、從右邊的下拉式清單選取所需的版本，然後選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="54764-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![更新套件](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="54764-138">對於某些套件，其 [更新] 按鈕已停用，並顯示訊息指出該套件「由 SDK 隱含參考」(或 "AutoReferenced")。</span><span class="sxs-lookup"><span data-stu-id="54764-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="54764-139">此訊息表示套件是較大架構或 SDK 的一部分，不應獨立更新。</span><span class="sxs-lookup"><span data-stu-id="54764-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="54764-140">（這類套件會在內部以 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`標示）。例如，`Microsoft.NETCore.App` 是 .NET Core SDK 的一部分，而封裝版本與應用程式所使用的執行時間架構版本不同。</span><span class="sxs-lookup"><span data-stu-id="54764-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="54764-141">您必須[更新 .NET Core 安裝](https://aka.ms/dotnet-download) \(英文\)，以取得新版本 ASP.NET Core 和 .Net Core 執行階段。</span><span class="sxs-lookup"><span data-stu-id="54764-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="54764-142">[如需 .NET Core 中繼套件和版本控制的詳細資料，請參閱此文件](/dotnet/core/packages)。</span><span class="sxs-lookup"><span data-stu-id="54764-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="54764-143">這適用於下列常用的套件：</span><span class="sxs-lookup"><span data-stu-id="54764-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="54764-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="54764-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="54764-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="54764-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="54764-146">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="54764-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="54764-147">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="54764-147">NETStandard.Library</span></span>

    ![標示為隱含參考或 AutoReferenced 的範例套件](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="54764-149">若要將多個套件更新為最新版本，請在清單中選取它們，然後選取清單上方的 [更新] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="54764-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="54764-150">您也可以從 [**已安裝**] 索引標籤更新個別的封裝。在此情況下，封裝的詳細資料包含版本選取器（受限於 [**包含發行**前版本] 選項）和 [**更新**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="54764-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="54764-151">管理解決方案的套件</span><span class="sxs-lookup"><span data-stu-id="54764-151">Manage packages for the solution</span></span>

<span data-ttu-id="54764-152">管理解決方案的套件可讓同時處理多個專案更方便。</span><span class="sxs-lookup"><span data-stu-id="54764-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="54764-153">選取 [工具] > [NuGet 套件管理員] > [管理解決方案的 NuGet 套件] 功能表命令，或以滑鼠右鍵按一下解決方案並選取 [管理 NuGet 套件]：</span><span class="sxs-lookup"><span data-stu-id="54764-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![管理解決方案的 NuGet 套件](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="54764-155">在管理解決方案的套件時，UI 可讓您選取受作業影響的專案：</span><span class="sxs-lookup"><span data-stu-id="54764-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![管理解決方案套件時的專案選取器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="54764-157">[合併] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="54764-157">Consolidate tab</span></span>

<span data-ttu-id="54764-158">開發人員通常會認為在相同的解決方案中，跨不同專案使用同一個 NuGet 套件的不同版本是不好的做法。</span><span class="sxs-lookup"><span data-stu-id="54764-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="54764-159">當您要管理解決方案的套件時，套件管理員 UI 提供 [合併] 索引標籤，您可以在其中輕鬆地查看解決方案中有哪些不同專案使用的套件具有不同版本號碼：</span><span class="sxs-lookup"><span data-stu-id="54764-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![套件管理員 UI [合併] 索引標籤](media/ConsolidateTab.png)

<span data-ttu-id="54764-161">在此範例中，ClassLibrary1 專案使用 EntityFramework 6.2.0，而 ConsoleApp1 使用 EntityFramework 6.1.0。</span><span class="sxs-lookup"><span data-stu-id="54764-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="54764-162">若要合併套件版本，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="54764-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="54764-163">在 [專案] 清單中選取要更新的專案。</span><span class="sxs-lookup"><span data-stu-id="54764-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="54764-164">在 [版本] 控制項中選取要在所有這些專案中使用的版本，例如，EntityFramework 6.2.0。</span><span class="sxs-lookup"><span data-stu-id="54764-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="54764-165">選取 [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="54764-165">Select the **Install** button.</span></span>

<span data-ttu-id="54764-166">套件管理員會將選取的套件版本安裝到所有已選取的專案中，之後套件就不會再出現在 [合併] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="54764-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="54764-167">套件來源</span><span class="sxs-lookup"><span data-stu-id="54764-167">Package sources</span></span>

<span data-ttu-id="54764-168">若要變更 Visual Studio 取得套件的來源，請從來源選取器中選取：</span><span class="sxs-lookup"><span data-stu-id="54764-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![套件管理員 UI 中的 [套件來源] 選取器](media/PackageSourceDropDown.png)

<span data-ttu-id="54764-170">若要管理套件來源：</span><span class="sxs-lookup"><span data-stu-id="54764-170">To manage package sources:</span></span>

1. <span data-ttu-id="54764-171">選取底下所示套件管理員 UI 中的 [設定] 圖示，或使用 [工具] > [選項] 命令，並捲動至 [NuGet 套件管理員]：</span><span class="sxs-lookup"><span data-stu-id="54764-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![套件管理員 UI 設定圖示](media/PackageSourceSettings.png)

1. <span data-ttu-id="54764-173">選取 [套件來源] 節點：</span><span class="sxs-lookup"><span data-stu-id="54764-173">Select the **Package Sources** node:</span></span>

    ![[套件來源] 選項](media/options.png)

1. <span data-ttu-id="54764-175">若要新增來源，請選取 **+**、編輯名稱、在 [來源] 控制項中輸入 URL 或路徑，然後選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="54764-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="54764-176">來源現在會顯示在選取器下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="54764-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="54764-177">若要變更套件來源，請選取套件、在 [名稱] 和 [來源] 方塊中編輯，然後選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="54764-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="54764-178">若要停用套件來源，請取消選取清單中名稱左邊的方塊。</span><span class="sxs-lookup"><span data-stu-id="54764-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="54764-179">若要移除套件來源，請選取它，然後選取 [X] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="54764-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="54764-180">使用向上和向下箭號按鈕不會變更套件來源的優先順序。</span><span class="sxs-lookup"><span data-stu-id="54764-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="54764-181">Visual Studio 會忽略套件來源的順序，而使用任一個最先回應要求的來源。</span><span class="sxs-lookup"><span data-stu-id="54764-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="54764-182">如需詳細資訊，請參閱[套件還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="54764-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="54764-183">如果套件來源在刪除後重新出現，它可能是列在電腦層級或使用者層級的 `NuGet.Config` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="54764-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="54764-184">請參閱[常用的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)，以了解這些檔案的位置，然後手動編輯這些檔案或使用 [nuget sources 命令](../reference/nuget-exe-CLI-reference.md)將來源移除。</span><span class="sxs-lookup"><span data-stu-id="54764-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="54764-185">套件管理員 [選項] 控制項</span><span class="sxs-lookup"><span data-stu-id="54764-185">Package manager Options control</span></span>

<span data-ttu-id="54764-186">選取套件時，套件管理員 UI 會在版本選取器下方顯示一個小型、可展開的 [選項] 控制項 (在此顯示摺疊和展開的狀態)。</span><span class="sxs-lookup"><span data-stu-id="54764-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="54764-187">請注意，某些專案類型只提供 [顯示預覽視窗] 選項。</span><span class="sxs-lookup"><span data-stu-id="54764-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![套件管理員選項](media/PackageManagerUIOptions.png)

<span data-ttu-id="54764-189">下列各節會說明這些選項。</span><span class="sxs-lookup"><span data-stu-id="54764-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="54764-190">顯示預覽視窗</span><span class="sxs-lookup"><span data-stu-id="54764-190">Show preview window</span></span>

<span data-ttu-id="54764-191">選取此選項時，系統會在安裝套件之前顯示強制回應視窗，顯示所選套件的相依性：</span><span class="sxs-lookup"><span data-stu-id="54764-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![範例預覽對話方塊](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="54764-193">安裝和更新選項</span><span class="sxs-lookup"><span data-stu-id="54764-193">Install and Update Options</span></span>

<span data-ttu-id="54764-194">(並非所有專案類型都適用)。</span><span class="sxs-lookup"><span data-stu-id="54764-194">(Not available for all project types.)</span></span>

<span data-ttu-id="54764-195">[相依性行為] 會設定 NuGet 如何決定要安裝的相依套件版本：</span><span class="sxs-lookup"><span data-stu-id="54764-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="54764-196">[忽略相依性] 會略過安裝任何相依性，這通常會使安裝的套件無法運作。</span><span class="sxs-lookup"><span data-stu-id="54764-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="54764-197">[最低] [預設] 會使用符合主要所選套件需求的最小版本號碼來安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="54764-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="54764-198">[最高修補程式] 會使用相同的主要和次要版本號碼 (但有最高的修補程式號碼) 來安裝版本。</span><span class="sxs-lookup"><span data-stu-id="54764-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="54764-199">例如，如果指定 1.2.2 版則會安裝開頭為 1.2 的最高版本</span><span class="sxs-lookup"><span data-stu-id="54764-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="54764-200">[最高次要] 會使用相同的主要版本號碼，但最高的次要號碼和修補程式號碼來安裝版本。</span><span class="sxs-lookup"><span data-stu-id="54764-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="54764-201">如果指定 1.2.2 版，則會安裝開頭為 1 的最高版本</span><span class="sxs-lookup"><span data-stu-id="54764-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="54764-202">[最高] 會安裝套件的最高可用版本。</span><span class="sxs-lookup"><span data-stu-id="54764-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="54764-203">[檔案衝突動作] 會指定 NuGet 應如何處理已存在於專案或本機電腦中的套件：</span><span class="sxs-lookup"><span data-stu-id="54764-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="54764-204">[提示] 會指示 NuGet 詢問要保留或覆寫現有套件。</span><span class="sxs-lookup"><span data-stu-id="54764-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="54764-205">[全部忽略] 會指示 NuGet 略過覆寫任何現有套件。</span><span class="sxs-lookup"><span data-stu-id="54764-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="54764-206">[全部覆寫] 會指示 NuGet 覆寫任何現有套件。</span><span class="sxs-lookup"><span data-stu-id="54764-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="54764-207">解除安裝選項</span><span class="sxs-lookup"><span data-stu-id="54764-207">Uninstall Options</span></span>

<span data-ttu-id="54764-208">(並非所有專案類型都適用)。</span><span class="sxs-lookup"><span data-stu-id="54764-208">(Not available for all project types.)</span></span>

<span data-ttu-id="54764-209">[移除相依性]：選取此選項時，系統會移除未在專案中其他位置參考的任何相依性套件。</span><span class="sxs-lookup"><span data-stu-id="54764-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="54764-210">[即使有相依性仍強制解除安裝]：選取時，即使專案中仍有項目參考該套件，也會將該套件解除安裝。</span><span class="sxs-lookup"><span data-stu-id="54764-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="54764-211">這通常與 [移除相依性] 結合使用，以移除套件和它所安裝的任何相依性。</span><span class="sxs-lookup"><span data-stu-id="54764-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="54764-212">不過，使用這個選項可能會導致專案中的參考無法運作。</span><span class="sxs-lookup"><span data-stu-id="54764-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="54764-213">在此情況下，您可能必須[重新安裝其他套件](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="54764-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
