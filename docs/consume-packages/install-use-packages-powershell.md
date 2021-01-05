---
title: 在 Visual Studio 中使用主控台安裝及管理 NuGet 套件
description: 在 Visual Studio 中使用 NuGet 套件管理員主控台來處理套件的指示。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 31fa51bc017eaaf9306d5f267e5d4b0d7a15ec9c
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699838"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="a5ef5-103">在 Visual Studio 中使用套件管理員主控台安裝及管理套件 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a5ef5-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="a5ef5-104">Nuget 套件管理員主控台可讓您使用 [NuGet PowerShell 命令](../reference/powershell-reference.md)來尋找、安裝、解除安裝及更新 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="a5ef5-105">在套件管理員 UI 無法執行作業的情況下，則必須使用主控台。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="a5ef5-106">若要在主控台中使用 `nuget.exe` CLI 命令，請參閱[在主控台中使用 nuget.exe CLI](#use-the-nugetexe-cli-in-the-console)。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="a5ef5-107">主控台內建於 Windows 上的 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="a5ef5-108">它不包含在 Visual Studio for Mac 或 Visual Studio Code 中。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

> [!Important]
> <span data-ttu-id="a5ef5-109">此處所列的命令是 Visual Studio 中的封裝管理員主控台特定的命令，不同于一般 PowerShell 環境中可用的 [套件管理模組命令](/powershell/module/packagemanagement/) 。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="a5ef5-110">具體而言，每個環境都有其他無法使用的命令，而且具有相同名稱的命令在其特定引數中也可能不同。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="a5ef5-111">當您在 Visual Studio 中使用套件管理主控台時，適用于本主題中記載的命令和引數適用于。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="a5ef5-112">尋找並安裝套件</span><span class="sxs-lookup"><span data-stu-id="a5ef5-112">Find and install a package</span></span>

<span data-ttu-id="a5ef5-113">例如，尋找並安裝套件是透過三個簡單的步驟來完成：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-113">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="a5ef5-114">在 Visual Studio 中開啟專案/方案，然後使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台] 命令來開啟主控台。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-114">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="a5ef5-115">尋找您要安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-115">Find the package you want to install.</span></span> <span data-ttu-id="a5ef5-116">如果您已經知道這一點，請跳到步驟 3。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-116">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="a5ef5-117">執行安裝命令：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-117">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="a5ef5-118">主控台中可用的所有作業也可以使用 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 來完成。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-118">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="a5ef5-119">不過，主控台命令會在 Visual Studio 內容與已儲存的專案/解決方案中運作，而且通常會比對等的 CLI 命令完成更多操作。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-119">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="a5ef5-120">例如，透過主控台安裝套件會將參考新增至專案，而 CLI 命令則不會。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-120">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="a5ef5-121">基於這個理由，使用 Visual Studio 的開發人員通常更喜歡使用主控台而不是 CLI。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-121">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="a5ef5-122">許多主控台作業都取決於在 Visual Studio 中使用已知的路徑名稱開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-122">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="a5ef5-123">如果您有未儲存的解決方案或是沒有解決方案，則會看到錯誤「未開啟或儲存方案。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-123">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="a5ef5-124">請確定您有已開啟和已儲存的方案。」</span><span class="sxs-lookup"><span data-stu-id="a5ef5-124">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="a5ef5-125">這表示主控台無法判斷解決方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-125">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="a5ef5-126">儲存未儲存的方案，或建立並儲存方案 (如果您沒有開啟的方案)，應該可以更正錯誤。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-126">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="a5ef5-127">開啟主控台與主控台控制項</span><span class="sxs-lookup"><span data-stu-id="a5ef5-127">Opening the console and console controls</span></span>

1. <span data-ttu-id="a5ef5-128">在 Visual Studio 中，使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台] 命令來開啟主控台。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-128">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="a5ef5-129">主控台是一個 Visual Studio 視窗，可依您的需要進行排列和定位 (請參閱[在 Visual Studio 中自訂視窗版面配置](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-129">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="a5ef5-130">根據預設，主控台命令會針對視窗頂端的控制項中設定的特定套件來源與專案進行操作：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-130">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![套件來源與專案的套件管理員主控台控制項](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="a5ef5-132">選取不同的套件來源和/或專案會變更後續命令的預設值。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-132">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="a5ef5-133">若要在不變更預設值的情況下覆寫這些設定，大部分的命令都支援 `-Source` 與 `-ProjectName` 選項。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-133">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="a5ef5-134">若要管理套件來源，請選取齒輪圖示。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-134">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="a5ef5-135">這是 [工具] > [選項] > [NuGet 套件管理員] > [套件來源] 對話方塊的捷徑，如[套件管理員 UI](install-use-packages-visual-studio.md#package-sources) 頁面所述。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-135">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="a5ef5-136">此外，專案選取器右側的控制項可清除主控台的內容：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-136">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![套件管理員主控台設定與清除控制項](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="a5ef5-138">最右邊的按鈕會中斷長時間執行的命令。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-138">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="a5ef5-139">例如，執行 `Get-Package -ListAvailable -PageSize 500` 會列出預設來源 (例如 nuget.org) 上的前 500 個套件，這可能需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-139">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![套件管理員主控台停止控制項](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="a5ef5-141">安裝套件</span><span class="sxs-lookup"><span data-stu-id="a5ef5-141">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="a5ef5-142">請參閱 [Install-Package](../reference/ps-reference/ps-ref-install-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-142">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="a5ef5-143">在主控台中安裝套件時執行的步驟，與[安裝套件時會發生什麼事](../concepts/package-installation-process.md)中所述相同，此外還會：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-143">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="a5ef5-144">主控台會在其視窗中顯示適用的授權條款，並附帶隱含的合約。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-144">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="a5ef5-145">如果您不同意這些條款，則應該立即將套件解除安裝。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-145">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="a5ef5-146">此外，對套件的參考也會加入至專案檔中，並顯示在 [方案總管] 中的 [參考] 節點下，您必須儲存專案才能直接查看專案檔中的變更。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-146">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="a5ef5-147">解除安裝套件</span><span class="sxs-lookup"><span data-stu-id="a5ef5-147">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="a5ef5-148">請參閱 [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-148">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="a5ef5-149">如果您需要尋找識別碼，請使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 來查看目前安裝在預設專案中的所有套件。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-149">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="a5ef5-150">解除安裝套件會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-150">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="a5ef5-151">從專案中移除套件的參考 (以及任何使用中的管理格式)。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-151">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="a5ef5-152">參考不會再出現在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-152">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="a5ef5-153">(您可能需要重建專案，才能看到它已從 **Bin** 資料夾中移除。)</span><span class="sxs-lookup"><span data-stu-id="a5ef5-153">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="a5ef5-154">反轉安裝套件時對 `app.config` 或 `web.config` 所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-154">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="a5ef5-155">如果沒有剩餘的套件使用這些相依性，則移除先前安裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-155">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="a5ef5-156">更新套件</span><span class="sxs-lookup"><span data-stu-id="a5ef5-156">Update a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="a5ef5-157">請參閱 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 與 [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="a5ef5-157">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="a5ef5-158">尋找套件</span><span class="sxs-lookup"><span data-stu-id="a5ef5-158">Find a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="a5ef5-159">請參閱 [Find-Package](../reference/ps-reference/ps-ref-find-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-159">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="a5ef5-160">在 Visual Studio 2013 與更早版本中，請改為使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-160">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="a5ef5-161">主控台的可用性</span><span class="sxs-lookup"><span data-stu-id="a5ef5-161">Availability of the console</span></span>

<span data-ttu-id="a5ef5-162">從 Visual Studio 2017 開始，當您選取任何與 .NET 相關的工作負載時，會自動安裝 NuGet 和 NuGet 套件管理員；您還可以透過檢查 Visual Studio 安裝程式中的 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 選項來個別安裝。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-162">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="a5ef5-163">此外，如果您想在 Visual Studio 2015 和更早版本中使用 NuGet 套件管理員，請查看 [工具] > [擴充功能和更新]，然後搜尋 NuGet 套件管理員擴充功能。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-163">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="a5ef5-164">如果您無法使用 Visual Studio 中的擴充功能安裝程式，您可以直接從下載擴充功能 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-164">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="a5ef5-165">Visual Studio for Mac 目前不提供套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-165">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="a5ef5-166">但是，對等的命令則可透過 [NuGet CLI](../reference/nuget-exe-CLI-reference.md) 取得。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-166">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="a5ef5-167">Visual Studio for Mac 確實有一個用於管理 NuGet 套件的 UI。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-167">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="a5ef5-168">請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-168">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="a5ef5-169">套件管理員主控台未隨附於 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-169">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="a5ef5-170">擴充套件管理員主控台</span><span class="sxs-lookup"><span data-stu-id="a5ef5-170">Extend the Package Manager Console</span></span>

<span data-ttu-id="a5ef5-171">某些套件會為主控台安裝新命令。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-171">Some packages install new commands for the console.</span></span> <span data-ttu-id="a5ef5-172">例如，`MvcScaffolding` 會建立如下所示的 `Scaffold` 命令，以產生 ASP.NET MVC 控制器與檢視：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-172">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![安裝及使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="a5ef5-174">設定 NuGet PowerShell 設定檔</span><span class="sxs-lookup"><span data-stu-id="a5ef5-174">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="a5ef5-175">PowerShell 設定檔可讓您在任何使用 PowerShell 的地方提供常用的命令。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-175">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="a5ef5-176">NuGet 支援 NuGet 專用設定檔，通常位於下列位置：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-176">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="a5ef5-177">若要尋找設定檔，請在主控台中輸入 `$profile`：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-177">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="a5ef5-178">如需詳細資訊，請參閱 [Windows PowerShell 設定檔](/previous-versions//bb613488(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="a5ef5-178">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="a5ef5-179">在主控台中使用 nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="a5ef5-179">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="a5ef5-180">若要讓[ `nuget.exe` CLI](../reference/nuget-exe-cli-reference.md)可在封裝管理員主控台中使用，請從主控台安裝[nuget.exe](https://www.nuget.org/packages/NuGet.CommandLine/)套件：</span><span class="sxs-lookup"><span data-stu-id="a5ef5-180">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
