---
title: "NuGet 封裝管理員 UI 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: "使用 NuGet 封裝，使用 Visual Studio 中的 NuGet 封裝管理員 UI 的指示。"
keywords: "NuGet UI，NuGet 封裝管理員 UI 中，在 Visual Studio 中，管理 NuGet 封裝、 NuGet 使用者介面、 封裝管理員 Visual Studio 中的 NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 35bb856ccff43c77af7eac67da4614d83dcdc533
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="410c7-104">NuGet 封裝管理員 UI</span><span class="sxs-lookup"><span data-stu-id="410c7-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="410c7-105">在 Windows 上的 Visual Studio 中的 NuGet 封裝管理員 UI 可讓您輕鬆地安裝、 解除安裝，及更新在專案和方案的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="410c7-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="410c7-106">Visual Studio 中適用於 Mac 的經驗，請參閱[您的專案中包括的 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="410c7-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="410c7-107">「 封裝管理員 」 UI 未隨附於 Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="410c7-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="410c7-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="410c7-108">In this topic:</span></span>

- [<span data-ttu-id="410c7-109">尋找和安裝封裝 （瀏覽 索引標籤）</span><span class="sxs-lookup"><span data-stu-id="410c7-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="410c7-110">解除安裝封裝 （已安裝 索引標籤）</span><span class="sxs-lookup"><span data-stu-id="410c7-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="410c7-111">[更新封裝 （已安裝與更新索引標籤）](#updating-a-package) (包括["隱含參考 sdk"或"AutoReferenced 」 訊息](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="410c7-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="410c7-112">[管理解決方案套件](#managing-packages-for-the-solution)（在同一時間方式處理多個專案）。</span><span class="sxs-lookup"><span data-stu-id="410c7-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="410c7-113">封裝來源</span><span class="sxs-lookup"><span data-stu-id="410c7-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="410c7-114">封裝管理員選項 控制項</span><span class="sxs-lookup"><span data-stu-id="410c7-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="410c7-115">如果您遺漏的 NuGet 封裝管理員 Visual Studio 2015 中，檢查**工具 > 擴充功能和更新...**並搜尋*NuGet 套件管理員*延伸模組。</span><span class="sxs-lookup"><span data-stu-id="410c7-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="410c7-116">如果您無法使用 Visual Studio 中的擴充功能安裝程式，下載擴充功能直接從[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="410c7-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="410c7-117">在 Visual Studio 2017，NuGet 和 NuGet 套件管理員自動安裝任何。網路相關的工作負載。</span><span class="sxs-lookup"><span data-stu-id="410c7-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="410c7-118">選取個別安裝**個別元件 > 程式碼工具 > NuGet 套件管理員**選項在 Visual Studio 2017 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="410c7-118">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="410c7-119">尋找和安裝封裝</span><span class="sxs-lookup"><span data-stu-id="410c7-119">Finding and installing a package</span></span>

1. <span data-ttu-id="410c7-120">在**方案總管] 中**，以滑鼠右鍵按一下 [**參考**或專案，然後選取**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="410c7-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![管理 NuGet 封裝 功能表選項](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="410c7-122">**瀏覽**索引標籤會顯示受歡迎情況看出從目前選取的來源封裝 (請參閱[封裝來源](#package-sources))。</span><span class="sxs-lookup"><span data-stu-id="410c7-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="410c7-123">搜尋特定的封裝，使用在左上方的 [搜尋] 方塊。</span><span class="sxs-lookup"><span data-stu-id="410c7-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="410c7-124">封裝從清單選取以顯示其資訊，也可讓**安裝**版本選取項目下拉式清單以及按鈕。</span><span class="sxs-lookup"><span data-stu-id="410c7-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![管理 NuGet 套件對話方塊瀏覽 索引標籤](media/Search.png)

1. <span data-ttu-id="410c7-126">從下拉式清單選取所需的版本，然後選取**安裝**。</span><span class="sxs-lookup"><span data-stu-id="410c7-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="410c7-127">Visual Studio 會將封裝和其相依性安裝到專案。</span><span class="sxs-lookup"><span data-stu-id="410c7-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="410c7-128">系統可能會要求您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="410c7-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="410c7-129">已加入的套件安裝完成時，出現在**已安裝** 索引標籤。封裝也會列在**參考**節點的 方案總管 中，表示您可以在專案中有參考它們`using`陳述式。</span><span class="sxs-lookup"><span data-stu-id="410c7-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![在 [方案總管] 的參考](media/References.png)

> [!Tip]
    > <span data-ttu-id="410c7-131">若要在搜尋中，包含發行前版本，而且建立發行前版本版本中提供下拉式清單，請選取**包含發行前版本**選項。</span><span class="sxs-lookup"><span data-stu-id="410c7-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="410c7-132">解除安裝封裝</span><span class="sxs-lookup"><span data-stu-id="410c7-132">Uninstalling a package</span></span>

1. <span data-ttu-id="410c7-133">在**方案總管] 中**，以滑鼠右鍵按一下 [**參考**或所需的專案，然後選取**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="410c7-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="410c7-134">選取**已安裝** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="410c7-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="410c7-135">選取要解除安裝 （使用搜尋來篩選清單，如有必要） 的套件，然後選取**解除安裝**。</span><span class="sxs-lookup"><span data-stu-id="410c7-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![解除安裝封裝](media/UninstallPackage.png)

1. <span data-ttu-id="410c7-137">請注意，**包含發行前版本**和**套件來源**解除安裝封裝時，控制項沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="410c7-137">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="410c7-138">更新封裝</span><span class="sxs-lookup"><span data-stu-id="410c7-138">Updating a package</span></span>

1. <span data-ttu-id="410c7-139">在**方案總管] 中**，以滑鼠右鍵按一下 [**參考**或所需的專案，然後選取**管理 NuGet 封裝...**.(在網站專案中，以滑鼠右鍵按一下**Bin**資料夾。)</span><span class="sxs-lookup"><span data-stu-id="410c7-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="410c7-140">選取**更新**索引標籤，查看所選取的封裝來源中有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="410c7-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="410c7-141">選取**包含發行前版本**要在更新清單中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="410c7-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="410c7-142">選取要更新，在右側下拉式清單中選取所需的版本，並選取封裝**更新**。</span><span class="sxs-lookup"><span data-stu-id="410c7-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![更新封裝](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="410c7-144">針對某些封裝，**更新**按鈕會停用，而且會出現訊息指出，它 「 隱含由參考 SDK"（或 「 AutoReferenced"）。</span><span class="sxs-lookup"><span data-stu-id="410c7-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="410c7-145">訊息會指出封裝，例如 Microsoft.NETCore.App 或 Microsoft.NETStandard.Library，是較大的架構或 SDK 的一部分，而且不應該獨立更新。</span><span class="sxs-lookup"><span data-stu-id="410c7-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="410c7-146">(這類封裝會在內部標示`<IsImplicitlyDefined>True</IsImplicitlyDefined>`。)若要更新封裝，更新其所屬的 SDK。</span><span class="sxs-lookup"><span data-stu-id="410c7-146">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![範例封裝標示為隱含參考或 AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="410c7-148">若要為其最新版本更新多個封裝，選取這些清單並選取**更新**清單上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="410c7-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="410c7-149">您也可以更新從個別封裝**已安裝** 索引標籤。在此情況下，封裝的詳細資料包含版本選取器 (受**包含發行前版本**選項) 和**更新** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="410c7-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="410c7-150">管理方案套件</span><span class="sxs-lookup"><span data-stu-id="410c7-150">Managing packages for the solution</span></span>

<span data-ttu-id="410c7-151">管理方案套件是方便的方法，來同時使用多個專案。</span><span class="sxs-lookup"><span data-stu-id="410c7-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="410c7-152">選取**工具 > NuGet 套件管理員 > 管理方案的 NuGet 封裝...**功能表命令時，或以滑鼠右鍵按一下方案並選取**管理 NuGet 封裝...**:</span><span class="sxs-lookup"><span data-stu-id="410c7-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![管理方案的 NuGet 封裝](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="410c7-154">當管理解決方案的封裝時，UI 可讓您選取受作業影響的專案：</span><span class="sxs-lookup"><span data-stu-id="410c7-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![管理方案的封裝時的專案選取器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="410c7-156">彙總索引標籤</span><span class="sxs-lookup"><span data-stu-id="410c7-156">Consolidate tab</span></span>

<span data-ttu-id="410c7-157">開發人員通常人認為非常不建議您在相同方案中的不同專案中使用不同版本的相同的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="410c7-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="410c7-158">當您選擇管理解決方案的封裝時，封裝管理員 UI 提供**合併彙算**所在您很容易其中封裝名稱中有不同的版本號碼由不同專案方案中的索引標籤：</span><span class="sxs-lookup"><span data-stu-id="410c7-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![封裝管理員 UI 合併索引標籤](media/ConsolidateTab.png)

<span data-ttu-id="410c7-160">在此範例中，而 ConsoleApp1 使用 EntityFramework 6.1.0 ClassLibrary1 專案時，使用 EntityFramework 6.2.0。</span><span class="sxs-lookup"><span data-stu-id="410c7-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="410c7-161">彙總套件版本，執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="410c7-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="410c7-162">選取要更新專案清單中的專案。</span><span class="sxs-lookup"><span data-stu-id="410c7-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="410c7-163">選取要使用所有這些專案中的版本**版本**控制權，例如 EntityFramework 6.2.0。</span><span class="sxs-lookup"><span data-stu-id="410c7-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="410c7-164">選取**安裝** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="410c7-164">Select the **Install** button.</span></span>

<span data-ttu-id="410c7-165">封裝管理員安裝到所有選取的專案，在其後封裝不會再出現在選取的封裝版本**合併彙算** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="410c7-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="410c7-166">封裝來源</span><span class="sxs-lookup"><span data-stu-id="410c7-166">Package sources</span></span>

<span data-ttu-id="410c7-167">若要變更 Visual Studio 將會從中取得封裝的來源，請選取從來源選取器的其中一個：</span><span class="sxs-lookup"><span data-stu-id="410c7-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![封裝管理員 UI 中的 封裝來源選取器](media/PackageSourceDropDown.png)

<span data-ttu-id="410c7-169">若要管理的封裝來源：</span><span class="sxs-lookup"><span data-stu-id="410c7-169">To manage package sources:</span></span>

1. <span data-ttu-id="410c7-170">選取**設定**封裝管理員 UI 中的圖示如下所述，或使用**工具 > 選項**命令，然後捲動至**NuGet 套件管理員**:</span><span class="sxs-lookup"><span data-stu-id="410c7-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![封裝管理員 UI 設定圖示](media/PackageSourceSettings.png)

1. <span data-ttu-id="410c7-172">選取**封裝來源**節點：</span><span class="sxs-lookup"><span data-stu-id="410c7-172">Select the **Package Sources** node:</span></span>

    ![封裝來源選項](media/options.png)

1. <span data-ttu-id="410c7-174">若要新增為來源，請選取 **+** 、 編輯名稱、 輸入的路徑或 URL**來源**控制項，然後選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="410c7-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="410c7-175">來源現在會出現在選取器下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="410c7-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="410c7-176">若要變更的封裝來源，請選取它，進行中的編輯**名稱**和**來源**方塊，然後選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="410c7-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="410c7-177">若要停用封裝來源，請清除方塊左邊的清單中的名稱。</span><span class="sxs-lookup"><span data-stu-id="410c7-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="410c7-178">若要移除的封裝來源，加以選取，然後選取**X**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="410c7-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="410c7-179">使用向上和向下箭號按鈕以變更的封裝來源的優先順序。</span><span class="sxs-lookup"><span data-stu-id="410c7-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="410c7-180">還原專案的封裝時，visual Studio 會搜尋這些來源中的優先順序。</span><span class="sxs-lookup"><span data-stu-id="410c7-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="410c7-181">如需詳細資訊，請參閱[封裝還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="410c7-181">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="410c7-182">如果套件來源再次出現之後刪除它，它可能會列在電腦層級或使用者層級`NuGet.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="410c7-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="410c7-183">請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)針對這些檔案的位置，然後移除來源以手動方式編輯檔案，或使用[nuget 來源命令](../tools/nuget-exe-CLI-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="410c7-183">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="410c7-184">封裝管理員選項 控制項</span><span class="sxs-lookup"><span data-stu-id="410c7-184">Package manager Options control</span></span>

<span data-ttu-id="410c7-185">選取封裝時，「 封裝管理員 」 UI 會顯示小，可展開**選項**下方 （如下所示同時摺疊和展開） 版本選擇器控制項。</span><span class="sxs-lookup"><span data-stu-id="410c7-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="410c7-186">請注意，某些專案類型，才**顯示預覽視窗**提供選項。</span><span class="sxs-lookup"><span data-stu-id="410c7-186">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![封裝管理員選項](media/PackageManagerUIOptions.png)

<span data-ttu-id="410c7-188">下列各節說明這些選項。</span><span class="sxs-lookup"><span data-stu-id="410c7-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="410c7-189">顯示預覽視窗</span><span class="sxs-lookup"><span data-stu-id="410c7-189">Show preview window</span></span>

<span data-ttu-id="410c7-190">選取時，強制回應視窗會顯示其中所選封裝的相依性套件之前，先：</span><span class="sxs-lookup"><span data-stu-id="410c7-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![範例預覽對話方塊](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="410c7-192">安裝及更新選項</span><span class="sxs-lookup"><span data-stu-id="410c7-192">Install and Update Options</span></span>

<span data-ttu-id="410c7-193">（不適用的所有專案類型）。</span><span class="sxs-lookup"><span data-stu-id="410c7-193">(Not available for all project types.)</span></span>

<span data-ttu-id="410c7-194">**相依性行為**設定 NuGet 如何決定要安裝的相依套件版本：</span><span class="sxs-lookup"><span data-stu-id="410c7-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="410c7-195">*忽略的相依性*略過安裝任何相依性，這通常會中斷所安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="410c7-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="410c7-196">*最低*[Default] 安裝相依性以符合需求的主要的所選套件的最小的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="410c7-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="410c7-197">*最高的修補程式*安裝的版本具有相同主要和次要版本號碼，而最高的修補程式數目。</span><span class="sxs-lookup"><span data-stu-id="410c7-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="410c7-198">比方說，如果已指定版本 1.2.2 然後開頭 1.2 最高的版本將會安裝</span><span class="sxs-lookup"><span data-stu-id="410c7-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="410c7-199">*最高次要*安裝的版本具有相同主要版本號碼，但最高次要號碼和修補程式數目。</span><span class="sxs-lookup"><span data-stu-id="410c7-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="410c7-200">如果指定 1.2.2 版本，然後以 1 為開頭的最高版本將會安裝</span><span class="sxs-lookup"><span data-stu-id="410c7-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="410c7-201">*最高*安裝封裝的最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="410c7-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="410c7-202">**檔案衝突 動作**指定 NuGet 應該如何處理已經存在於專案或本機電腦的封裝：</span><span class="sxs-lookup"><span data-stu-id="410c7-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="410c7-203">*提示*指示 NuGet 詢問是否要保留或覆寫現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="410c7-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="410c7-204">*忽略以上所有*指示 NuGet 略過覆寫任何現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="410c7-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="410c7-205">*覆寫所有*指示 NuGet 覆寫任何現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="410c7-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="410c7-206">解除安裝選項</span><span class="sxs-lookup"><span data-stu-id="410c7-206">Uninstall Options</span></span>

<span data-ttu-id="410c7-207">（不適用的所有專案類型）。</span><span class="sxs-lookup"><span data-stu-id="410c7-207">(Not available for all project types.)</span></span>

<span data-ttu-id="410c7-208">**移除依存性**： 選取時，移除任何相依的套件如果它們未參考其他地方專案中。</span><span class="sxs-lookup"><span data-stu-id="410c7-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="410c7-209">**強制解除安裝，即使相依於它也是**： 選取時，會解除安裝封裝即使仍在專案中參考。</span><span class="sxs-lookup"><span data-stu-id="410c7-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="410c7-210">這通常用於搭配**移除相依性**移除封裝和任何相依性安裝它。</span><span class="sxs-lookup"><span data-stu-id="410c7-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="410c7-211">使用此選項可能，不過，會導致中斷的參考專案中。</span><span class="sxs-lookup"><span data-stu-id="410c7-211">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="410c7-212">在這種情況下，您可能需要[重新安裝這些其他封裝](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="410c7-212">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
