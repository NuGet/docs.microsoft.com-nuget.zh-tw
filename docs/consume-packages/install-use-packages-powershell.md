---
title: 在 Visual Studio 中使用主控台安裝及管理 NuGet 套件
description: 在 Visual Studio 中使用 NuGet 套件管理員主控台來處理套件的指示。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 8b23b6cc22eff5413e317fbe619edd3d4f4716ee
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237396"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="a9855-103">在 Visual Studio 中使用套件管理員主控台安裝及管理套件 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a9855-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="a9855-104">Nuget 套件管理員主控台可讓您使用 [NuGet PowerShell 命令](../reference/powershell-reference.md)來尋找、安裝、解除安裝及更新 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a9855-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="a9855-105">在套件管理員 UI 無法執行作業的情況下，則必須使用主控台。</span><span class="sxs-lookup"><span data-stu-id="a9855-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="a9855-106">若要在主控台中使用 `nuget.exe` CLI 命令，請參閱[在主控台中使用 nuget.exe CLI](#use-the-nugetexe-cli-in-the-console)。</span><span class="sxs-lookup"><span data-stu-id="a9855-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="a9855-107">主控台內建於 Windows 上的 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="a9855-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="a9855-108">它不包含在 Visual Studio for Mac 或 Visual Studio Code 中。</span><span class="sxs-lookup"><span data-stu-id="a9855-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="a9855-109">尋找並安裝套件</span><span class="sxs-lookup"><span data-stu-id="a9855-109">Find and install a package</span></span>

<span data-ttu-id="a9855-110">例如，尋找並安裝套件是透過三個簡單的步驟來完成：</span><span class="sxs-lookup"><span data-stu-id="a9855-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="a9855-111">在 Visual Studio 中開啟專案/方案，然後使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台] 命令來開啟主控台。</span><span class="sxs-lookup"><span data-stu-id="a9855-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="a9855-112">尋找您要安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="a9855-112">Find the package you want to install.</span></span> <span data-ttu-id="a9855-113">如果您已經知道這一點，請跳到步驟 3。</span><span class="sxs-lookup"><span data-stu-id="a9855-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="a9855-114">執行安裝命令：</span><span class="sxs-lookup"><span data-stu-id="a9855-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="a9855-115">主控台中可用的所有作業也可以使用 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 來完成。</span><span class="sxs-lookup"><span data-stu-id="a9855-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="a9855-116">不過，主控台命令會在 Visual Studio 內容與已儲存的專案/解決方案中運作，而且通常會比對等的 CLI 命令完成更多操作。</span><span class="sxs-lookup"><span data-stu-id="a9855-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="a9855-117">例如，透過主控台安裝套件會將參考新增至專案，而 CLI 命令則不會。</span><span class="sxs-lookup"><span data-stu-id="a9855-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="a9855-118">基於這個理由，使用 Visual Studio 的開發人員通常更喜歡使用主控台而不是 CLI。</span><span class="sxs-lookup"><span data-stu-id="a9855-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="a9855-119">許多主控台作業都取決於在 Visual Studio 中使用已知的路徑名稱開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="a9855-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="a9855-120">如果您有未儲存的解決方案或是沒有解決方案，則會看到錯誤「未開啟或儲存方案。</span><span class="sxs-lookup"><span data-stu-id="a9855-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="a9855-121">請確定您有已開啟和已儲存的方案。」</span><span class="sxs-lookup"><span data-stu-id="a9855-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="a9855-122">這表示主控台無法判斷解決方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="a9855-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="a9855-123">儲存未儲存的方案，或建立並儲存方案 (如果您沒有開啟的方案)，應該可以更正錯誤。</span><span class="sxs-lookup"><span data-stu-id="a9855-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="a9855-124">開啟主控台與主控台控制項</span><span class="sxs-lookup"><span data-stu-id="a9855-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="a9855-125">在 Visual Studio 中，使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台] 命令來開啟主控台。</span><span class="sxs-lookup"><span data-stu-id="a9855-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="a9855-126">主控台是一個 Visual Studio 視窗，可依您的需要進行排列和定位 (請參閱[在 Visual Studio 中自訂視窗版面配置](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。</span><span class="sxs-lookup"><span data-stu-id="a9855-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="a9855-127">根據預設，主控台命令會針對視窗頂端的控制項中設定的特定套件來源與專案進行操作：</span><span class="sxs-lookup"><span data-stu-id="a9855-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![套件來源與專案的套件管理員主控台控制項](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="a9855-129">選取不同的套件來源和/或專案會變更後續命令的預設值。</span><span class="sxs-lookup"><span data-stu-id="a9855-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="a9855-130">若要在不變更預設值的情況下覆寫這些設定，大部分的命令都支援 `-Source` 與 `-ProjectName` 選項。</span><span class="sxs-lookup"><span data-stu-id="a9855-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="a9855-131">若要管理套件來源，請選取齒輪圖示。</span><span class="sxs-lookup"><span data-stu-id="a9855-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="a9855-132">這是 [工具] > [選項] > [NuGet 套件管理員] > [套件來源] 對話方塊的捷徑，如[套件管理員 UI](install-use-packages-visual-studio.md#package-sources) 頁面所述。</span><span class="sxs-lookup"><span data-stu-id="a9855-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="a9855-133">此外，專案選取器右側的控制項可清除主控台的內容：</span><span class="sxs-lookup"><span data-stu-id="a9855-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![套件管理員主控台設定與清除控制項](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="a9855-135">最右邊的按鈕會中斷長時間執行的命令。</span><span class="sxs-lookup"><span data-stu-id="a9855-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="a9855-136">例如，執行 `Get-Package -ListAvailable -PageSize 500` 會列出預設來源 (例如 nuget.org) 上的前 500 個套件，這可能需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="a9855-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![套件管理員主控台停止控制項](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="a9855-138">安裝套件</span><span class="sxs-lookup"><span data-stu-id="a9855-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="a9855-139">請參閱 [Install-Package](../reference/ps-reference/ps-ref-install-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a9855-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="a9855-140">在主控台中安裝套件時執行的步驟，與[安裝套件時會發生什麼事](../concepts/package-installation-process.md)中所述相同，此外還會：</span><span class="sxs-lookup"><span data-stu-id="a9855-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="a9855-141">主控台會在其視窗中顯示適用的授權條款，並附帶隱含的合約。</span><span class="sxs-lookup"><span data-stu-id="a9855-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="a9855-142">如果您不同意這些條款，則應該立即將套件解除安裝。</span><span class="sxs-lookup"><span data-stu-id="a9855-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="a9855-143">此外，對套件的參考也會加入至專案檔中，並顯示在 [方案總管] 中的 [參考] 節點下，您必須儲存專案才能直接查看專案檔中的變更。</span><span class="sxs-lookup"><span data-stu-id="a9855-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="a9855-144">解除安裝套件</span><span class="sxs-lookup"><span data-stu-id="a9855-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="a9855-145">請參閱 [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a9855-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="a9855-146">如果您需要尋找識別碼，請使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 來查看目前安裝在預設專案中的所有套件。</span><span class="sxs-lookup"><span data-stu-id="a9855-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="a9855-147">解除安裝套件會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="a9855-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="a9855-148">從專案中移除套件的參考 (以及任何使用中的管理格式)。</span><span class="sxs-lookup"><span data-stu-id="a9855-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="a9855-149">參考不會再出現在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="a9855-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="a9855-150">(您可能需要重建專案，才能看到它已從 **Bin** 資料夾中移除。)</span><span class="sxs-lookup"><span data-stu-id="a9855-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="a9855-151">反轉安裝套件時對 `app.config` 或 `web.config` 所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="a9855-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="a9855-152">如果沒有剩餘的套件使用這些相依性，則移除先前安裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="a9855-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="a9855-153">更新套件</span><span class="sxs-lookup"><span data-stu-id="a9855-153">Update a package</span></span>

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

<span data-ttu-id="a9855-154">請參閱 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 與 [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="a9855-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="a9855-155">尋找套件</span><span class="sxs-lookup"><span data-stu-id="a9855-155">Find a package</span></span>

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

<span data-ttu-id="a9855-156">請參閱 [Find-Package](../reference/ps-reference/ps-ref-find-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a9855-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="a9855-157">在 Visual Studio 2013 與更早版本中，請改為使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a9855-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="a9855-158">主控台的可用性</span><span class="sxs-lookup"><span data-stu-id="a9855-158">Availability of the console</span></span>

<span data-ttu-id="a9855-159">從 Visual Studio 2017 開始，當您選取任何與 .NET 相關的工作負載時，會自動安裝 NuGet 和 NuGet 套件管理員；您還可以透過檢查 Visual Studio 安裝程式中的 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 選項來個別安裝。</span><span class="sxs-lookup"><span data-stu-id="a9855-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="a9855-160">此外，如果您想在 Visual Studio 2015 和更早版本中使用 NuGet 套件管理員，請查看 [工具] > [擴充功能和更新]，然後搜尋 NuGet 套件管理員擴充功能。</span><span class="sxs-lookup"><span data-stu-id="a9855-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="a9855-161">如果您無法使用 Visual Studio 中的擴充功能安裝程式，您可以直接從下載擴充功能 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 。</span><span class="sxs-lookup"><span data-stu-id="a9855-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="a9855-162">Visual Studio for Mac 目前不提供套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="a9855-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="a9855-163">但是，對等的命令則可透過 [NuGet CLI](../reference/nuget-exe-CLI-reference.md) 取得。</span><span class="sxs-lookup"><span data-stu-id="a9855-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="a9855-164">Visual Studio for Mac 確實有一個用於管理 NuGet 套件的 UI。</span><span class="sxs-lookup"><span data-stu-id="a9855-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="a9855-165">請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="a9855-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="a9855-166">套件管理員主控台未隨附於 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="a9855-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="a9855-167">擴充套件管理員主控台</span><span class="sxs-lookup"><span data-stu-id="a9855-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="a9855-168">某些套件會為主控台安裝新命令。</span><span class="sxs-lookup"><span data-stu-id="a9855-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="a9855-169">例如，`MvcScaffolding` 會建立如下所示的 `Scaffold` 命令，以產生 ASP.NET MVC 控制器與檢視：</span><span class="sxs-lookup"><span data-stu-id="a9855-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![安裝及使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="a9855-171">設定 NuGet PowerShell 設定檔</span><span class="sxs-lookup"><span data-stu-id="a9855-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="a9855-172">PowerShell 設定檔可讓您在任何使用 PowerShell 的地方提供常用的命令。</span><span class="sxs-lookup"><span data-stu-id="a9855-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="a9855-173">NuGet 支援 NuGet 專用設定檔，通常位於下列位置：</span><span class="sxs-lookup"><span data-stu-id="a9855-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="a9855-174">若要尋找設定檔，請在主控台中輸入 `$profile`：</span><span class="sxs-lookup"><span data-stu-id="a9855-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="a9855-175">如需詳細資訊，請參閱 [Windows PowerShell 設定檔](/previous-versions//bb613488(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="a9855-175">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="a9855-176">在主控台中使用 nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="a9855-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="a9855-177">若要讓[ `nuget.exe` CLI](../reference/nuget-exe-cli-reference.md)可在封裝管理員主控台中使用，請從主控台安裝[nuget.exe](https://www.nuget.org/packages/NuGet.CommandLine/)套件：</span><span class="sxs-lookup"><span data-stu-id="a9855-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```