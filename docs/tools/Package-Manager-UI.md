---
title: 安裝和管理 Visual Studio 中的 NuGet 套件
description: 使用 Visual Studio 中的 NuGet 套件管理員 UI，使用 NuGet 套件的指示。
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426242"
---
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="f1508-103">安裝和管理 Visual Studio 中的封裝</span><span class="sxs-lookup"><span data-stu-id="f1508-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="f1508-104">在 Windows 上的 Visual Studio 中的 NuGet 套件管理員 UI 可讓您輕鬆地安裝、 解除安裝，並更新專案和方案中的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="f1508-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="f1508-105">在 Visual Studio for Mac 的體驗，請參閱 <<c0> [ 在專案中的包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="f1508-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="f1508-106">找不到隨附於 Visual Studio Code 的套件管理員 UI。</span><span class="sxs-lookup"><span data-stu-id="f1508-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="f1508-107">如果您缺少的 NuGet 套件管理員，在 Visual Studio 2015，請檢查**工具 > 擴充功能和更新...** 並搜尋*NuGet 套件管理員*延伸模組。</span><span class="sxs-lookup"><span data-stu-id="f1508-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="f1508-108">如果您無法使用 Visual Studio 中的延伸模組安裝程式，請下載擴充功能直接從[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="f1508-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="f1508-109">從 Visual Studio 2017，NuGet 和 NuGet 套件管理員會自動安裝任何。NET 相關的工作負載。</span><span class="sxs-lookup"><span data-stu-id="f1508-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="f1508-110">藉由選取個別安裝**個別元件 > 程式碼工具 > NuGet 套件管理員**Visual Studio 安裝程式中的選項。</span><span class="sxs-lookup"><span data-stu-id="f1508-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="f1508-111">尋找和安裝封裝</span><span class="sxs-lookup"><span data-stu-id="f1508-111">Finding and installing a package</span></span>

1. <span data-ttu-id="f1508-112">在 **方案總管**，以滑鼠右鍵按一下其中一個**參考**或專案，然後選取**管理 NuGet 套件...** .</span><span class="sxs-lookup"><span data-stu-id="f1508-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![管理 NuGet 套件 功能表選項](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="f1508-114">**瀏覽**索引標籤會顯示依熱門程度從目前所選來源的封裝 (請參閱[套件來源](#package-sources))。</span><span class="sxs-lookup"><span data-stu-id="f1508-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="f1508-115">搜尋特定的封裝，使用在左上方的搜尋方塊中。</span><span class="sxs-lookup"><span data-stu-id="f1508-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="f1508-116">選取封裝，從清單中，以顯示其資訊，也可讓**安裝**以及版本選取項目下拉式清單的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1508-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![管理 NuGet 封裝對話方塊瀏覽 索引標籤](media/Search.png)

1. <span data-ttu-id="f1508-118">從下拉式清單中選取所需的版本，然後選取**安裝**。</span><span class="sxs-lookup"><span data-stu-id="f1508-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="f1508-119">Visual Studio 會將封裝和其相依性安裝到專案。</span><span class="sxs-lookup"><span data-stu-id="f1508-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="f1508-120">系統可能會要求您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="f1508-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="f1508-121">新增的套件安裝完成時，出現在**已安裝** 索引標籤。套件也會列在**參考**節點的 方案總管 中，表示您可以在專案中有參考這些`using`陳述式。</span><span class="sxs-lookup"><span data-stu-id="f1508-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![在 [方案總管] 中的參考](media/References.png)

> [!Tip]
> <span data-ttu-id="f1508-123">若要在搜尋中，包含發行前版本，並發行前版本中提供版本下拉式清單，選取**包含發行前版本**選項。</span><span class="sxs-lookup"><span data-stu-id="f1508-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="f1508-124">解除安裝套件</span><span class="sxs-lookup"><span data-stu-id="f1508-124">Uninstalling a package</span></span>

1. <span data-ttu-id="f1508-125">在 [**方案總管] 中**，以滑鼠右鍵按一下其中一個**參考**或所需的專案，然後選取**管理 NuGet 套件...** .</span><span class="sxs-lookup"><span data-stu-id="f1508-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f1508-126">選取 [**已安裝**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f1508-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="f1508-127">選取要解除安裝 （使用搜尋來篩選清單，如有必要） 的封裝，然後選取**解除安裝**。</span><span class="sxs-lookup"><span data-stu-id="f1508-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![解除安裝套件](media/UninstallPackage.png)

1. <span data-ttu-id="f1508-129">請注意，**包括發行前版本**並**套件來源**解除安裝套件時，控制項沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="f1508-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="f1508-130">更新套件</span><span class="sxs-lookup"><span data-stu-id="f1508-130">Updating a package</span></span>

1. <span data-ttu-id="f1508-131">在 [**方案總管] 中**，以滑鼠右鍵按一下其中一個**參考**或所需的專案，然後選取**管理 NuGet 套件...** .(在網站專案中，以滑鼠右鍵按一下**Bin**資料夾。)</span><span class="sxs-lookup"><span data-stu-id="f1508-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="f1508-132">選取 [**更新**] 索引標籤，查看有可用的更新，從選取的封裝來源的封裝。</span><span class="sxs-lookup"><span data-stu-id="f1508-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="f1508-133">選取 **包含發行前版本**包含發行前版本的套件清單中的更新。</span><span class="sxs-lookup"><span data-stu-id="f1508-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="f1508-134">選取要更新，從右邊的下拉式清單中選取所需的版本，並選取封裝**更新**。</span><span class="sxs-lookup"><span data-stu-id="f1508-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![更新套件](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="f1508-136">某些封裝，如**更新**按鈕已停用，且會出現訊息指出，它會 「 隱含參考 SDK 」 （或 「 自動參考 」）。</span><span class="sxs-lookup"><span data-stu-id="f1508-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="f1508-137">此訊息表示封裝是較大的架構或 SDK 的一部分，而且不應獨立更新。</span><span class="sxs-lookup"><span data-stu-id="f1508-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="f1508-138">(這類套件會在內部標示與`<IsImplicitlyDefined>True</IsImplicitlyDefined>`。)比方說，`Microsoft.NETCore.App`屬於.NET Core SDK 和套件版本不相同的應用程式所使用的執行階段 framework 版本。</span><span class="sxs-lookup"><span data-stu-id="f1508-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="f1508-139">您需要[更新您的.NET Core 安裝](https://aka.ms/dotnet-download)來取得新版本的 ASP.NET Core 和.NET Core 執行階段。</span><span class="sxs-lookup"><span data-stu-id="f1508-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="f1508-140">[請參閱這份文件，如需詳細資訊，.NET Core 中繼套件和版本控制](/dotnet/core/packages)。</span><span class="sxs-lookup"><span data-stu-id="f1508-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="f1508-141">這適用於下列常用的套件：</span><span class="sxs-lookup"><span data-stu-id="f1508-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="f1508-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="f1508-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="f1508-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="f1508-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="f1508-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="f1508-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="f1508-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="f1508-145">NETStandard.Library</span></span>

    ![範例封裝標示隱含參考或自動參考](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="f1508-147">若要更新為最新版本的多個封裝，選取清單中選取**更新**清單上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1508-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="f1508-148">您也可以更新從個別封裝**已安裝** 索引標籤。在此情況下，封裝的詳細資料包含版本選擇器 (受**包括發行前版本**選項) 和**更新** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1508-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="f1508-149">管理解決方案套件</span><span class="sxs-lookup"><span data-stu-id="f1508-149">Managing packages for the solution</span></span>

<span data-ttu-id="f1508-150">管理解決方案封裝是同時使用多個專案的便利方法。</span><span class="sxs-lookup"><span data-stu-id="f1508-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="f1508-151">選取**工具 > NuGet 套件管理員 > 管理方案的 NuGet 套件...** 功能表命令，或以滑鼠右鍵按一下方案，然後選取**管理 NuGet 套件...** :</span><span class="sxs-lookup"><span data-stu-id="f1508-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![管理解決方案的 NuGet 封裝](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="f1508-153">在管理解決方案的封裝時，UI 可讓您選取的專案，會受到作業：</span><span class="sxs-lookup"><span data-stu-id="f1508-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![管理方案的套件時的專案選取器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="f1508-155">彙總索引標籤</span><span class="sxs-lookup"><span data-stu-id="f1508-155">Consolidate tab</span></span>

<span data-ttu-id="f1508-156">開發人員通常認為不建議您在相同方案中的不同專案中使用相同的 NuGet 套件的不同版本。</span><span class="sxs-lookup"><span data-stu-id="f1508-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="f1508-157">當您選擇管理解決方案套件時，套件管理員 UI 提供**合併** 索引標籤您可以輕易看到方案中的不同專案，使用封裝名稱中有不同的版本號碼：</span><span class="sxs-lookup"><span data-stu-id="f1508-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![套件管理員 UI 合併 索引標籤](media/ConsolidateTab.png)

<span data-ttu-id="f1508-159">在此範例中，而 ConsoleApp1 使用 EntityFramework 6.1.0 ClassLibrary1 專案時，會使用 EntityFramework 6.2.0。</span><span class="sxs-lookup"><span data-stu-id="f1508-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="f1508-160">若要彙總套件版本，執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="f1508-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="f1508-161">選取 [專案] 清單中要更新的專案。</span><span class="sxs-lookup"><span data-stu-id="f1508-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="f1508-162">選取要使用所有這些專案中的版本**版本**控制項，例如 EntityFramework 6.2.0。</span><span class="sxs-lookup"><span data-stu-id="f1508-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="f1508-163">選取 [**安裝**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1508-163">Select the **Install** button.</span></span>

<span data-ttu-id="f1508-164">封裝管理員會選取的封裝版本安裝到所有選取的專案之後，封裝不會再出現在**合併** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f1508-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="f1508-165">套件來源</span><span class="sxs-lookup"><span data-stu-id="f1508-165">Package sources</span></span>

<span data-ttu-id="f1508-166">若要變更 Visual Studio 將會從中取得封裝的來源，選取從來源選取器的其中一個：</span><span class="sxs-lookup"><span data-stu-id="f1508-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![在 套件管理員 UI 中的封裝來源選取器](media/PackageSourceDropDown.png)

<span data-ttu-id="f1508-168">若要管理的套件來源：</span><span class="sxs-lookup"><span data-stu-id="f1508-168">To manage package sources:</span></span>

1. <span data-ttu-id="f1508-169">選取 **設定**套件管理員 UI 中的圖示如下所述，或使用**工具 > 選項**命令，然後捲動至**NuGet 套件管理員**:</span><span class="sxs-lookup"><span data-stu-id="f1508-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![套件管理員 UI 設定圖示](media/PackageSourceSettings.png)

1. <span data-ttu-id="f1508-171">選取 **套件來源**節點：</span><span class="sxs-lookup"><span data-stu-id="f1508-171">Select the **Package Sources** node:</span></span>

    ![封裝來源選項](media/options.png)

1. <span data-ttu-id="f1508-173">若要新增為來源，請選取 **+** 、 編輯名稱、 輸入的路徑或 URL **來源** 控制項，然後選取 **更新** 。</span><span class="sxs-lookup"><span data-stu-id="f1508-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="f1508-174">來源現在會出現在選取器下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="f1508-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="f1508-175">若要變更的套件來源，請選取它，進行中的編輯**名稱**並**來源**方塊中，然後選取**Update**。</span><span class="sxs-lookup"><span data-stu-id="f1508-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="f1508-176">若要停用的套件來源，請清除方塊左邊的清單中的名稱。</span><span class="sxs-lookup"><span data-stu-id="f1508-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="f1508-177">若要移除的套件來源，請選取它，然後按**X**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1508-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="f1508-178">使用向上和向下箭號按鈕不會變更的套件來源的優先順序。</span><span class="sxs-lookup"><span data-stu-id="f1508-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="f1508-179">Visual Studio 會忽略套件來源的順序，使用從任一個來源是一個最先回應要求。</span><span class="sxs-lookup"><span data-stu-id="f1508-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="f1508-180">如需詳細資訊，請參閱 <<c0> [ 套件還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="f1508-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="f1508-181">如果套件來源之後刪除它再次發生，表示它可能會列在電腦層級或使用者層級`NuGet.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="f1508-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="f1508-182">請參閱[常見的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)這些檔案的位置，然後移除來源以手動方式編輯檔案，或使用[nuget 來源命令](../tools/nuget-exe-CLI-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="f1508-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="f1508-183">套件管理員選項控制</span><span class="sxs-lookup"><span data-stu-id="f1508-183">Package manager Options control</span></span>

<span data-ttu-id="f1508-184">選取套件時，套件管理員 UI 會顯示一個小型的可展開**選項**下方 （如下所示同時摺疊和展開） 版本選擇器控制項。</span><span class="sxs-lookup"><span data-stu-id="f1508-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="f1508-185">請注意，某些專案類型，才**顯示預覽視窗**提供選項。</span><span class="sxs-lookup"><span data-stu-id="f1508-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![套件管理員選項](media/PackageManagerUIOptions.png)

<span data-ttu-id="f1508-187">下列各節說明這些選項。</span><span class="sxs-lookup"><span data-stu-id="f1508-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="f1508-188">顯示預覽視窗</span><span class="sxs-lookup"><span data-stu-id="f1508-188">Show preview window</span></span>

<span data-ttu-id="f1508-189">選取時，強制回應視窗會顯示其所選套件的相依性之前安裝套件：</span><span class="sxs-lookup"><span data-stu-id="f1508-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![範例預覽對話方塊](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="f1508-191">Možnosti instalace a Aktualizace</span><span class="sxs-lookup"><span data-stu-id="f1508-191">Install and Update Options</span></span>

<span data-ttu-id="f1508-192">（不適用所有專案類型）。</span><span class="sxs-lookup"><span data-stu-id="f1508-192">(Not available for all project types.)</span></span>

<span data-ttu-id="f1508-193">**相依性行為**設定 NuGet 如何決定要安裝的相依套件版本：</span><span class="sxs-lookup"><span data-stu-id="f1508-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="f1508-194">*略過相依性*略過安裝任何相依性，這通常會中斷安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="f1508-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="f1508-195">*最低*[Default] 安裝相依性最低的版本號碼符合主要的所選套件的需求。</span><span class="sxs-lookup"><span data-stu-id="f1508-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="f1508-196">*最高的修補程式*安裝的版本具有相同的主要和次要版本號碼，但最高的修補程式數目。</span><span class="sxs-lookup"><span data-stu-id="f1508-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="f1508-197">比方說，如果未指定版本 1.2.2 則開頭為 1.2 的最高版本將會安裝</span><span class="sxs-lookup"><span data-stu-id="f1508-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="f1508-198">*最高次要*安裝的版本，使用相同的主要版本號碼，但最高次要號碼和修補程式數目。</span><span class="sxs-lookup"><span data-stu-id="f1508-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="f1508-199">如果指定 1.2.2 版，則會從 1 開始的最高版本將會安裝</span><span class="sxs-lookup"><span data-stu-id="f1508-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="f1508-200">*最高*安裝封裝的最高可用版本。</span><span class="sxs-lookup"><span data-stu-id="f1508-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="f1508-201">**檔案衝突動作**指定 NuGet 應如何處理已經存在於專案或本機電腦的封裝：</span><span class="sxs-lookup"><span data-stu-id="f1508-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="f1508-202">*提示*會指示 NuGet 詢問是否要保留或覆寫現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="f1508-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="f1508-203">*全部忽略*會指示 NuGet 略過覆寫任何現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="f1508-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="f1508-204">*覆寫所有*會指示 NuGet 覆寫任何現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="f1508-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="f1508-205">解除安裝選項</span><span class="sxs-lookup"><span data-stu-id="f1508-205">Uninstall Options</span></span>

<span data-ttu-id="f1508-206">（不適用所有專案類型）。</span><span class="sxs-lookup"><span data-stu-id="f1508-206">(Not available for all project types.)</span></span>

<span data-ttu-id="f1508-207">**移除相依性**： 選取時，會移除任何相依的套件如果它們是在其他地方專案中未參考。</span><span class="sxs-lookup"><span data-stu-id="f1508-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="f1508-208">**強制解除安裝，即使它有相依性**： 選取時，解除安裝封裝即使仍在專案中參考。</span><span class="sxs-lookup"><span data-stu-id="f1508-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="f1508-209">這通常用於搭配**移除相依性**移除套件及任何相依性安裝它。</span><span class="sxs-lookup"><span data-stu-id="f1508-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="f1508-210">使用此選項可能，不過，會導致中斷的參考，專案中。</span><span class="sxs-lookup"><span data-stu-id="f1508-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="f1508-211">在此情況下，您可能需要[重新安裝這些其他套件](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="f1508-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
