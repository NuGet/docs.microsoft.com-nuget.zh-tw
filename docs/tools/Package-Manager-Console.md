---
title: 安裝和管理 Visual Studio 中使用主控台的 NuGet 套件
description: 使用 Visual Studio 中的 NuGet 套件管理員主控台，使用封裝的指示。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 91ab3859994e5ae738c6637219681ebbfc92d420
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842588"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="627fa-103">安裝和管理封裝與封裝管理員主控台在 Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="627fa-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="627fa-104">NuGet 套件管理員主控台可讓您使用[NuGet PowerShell 命令](../tools/powershell-reference.md)尋找、 安裝、 解除安裝和更新 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="627fa-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="627fa-105">必須在套件管理員 UI 不會提供方法，來執行作業的情況下使用主控台。</span><span class="sxs-lookup"><span data-stu-id="627fa-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="627fa-106">若要使用`nuget.exe`CLI 命令，在主控台中，請參閱[使用 nuget.exe CLI，在主控台中](#using-the-nugetexe-cli-in-the-console)。</span><span class="sxs-lookup"><span data-stu-id="627fa-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="627fa-107">主控台內建在 Windows 上的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="627fa-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="627fa-108">不隨附於 Visual Studio for Mac 或 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="627fa-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="627fa-109">尋找並安裝封裝</span><span class="sxs-lookup"><span data-stu-id="627fa-109">Find and install a package</span></span>

<span data-ttu-id="627fa-110">例如，尋找及安裝套件是使用三個簡單步驟：</span><span class="sxs-lookup"><span data-stu-id="627fa-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="627fa-111">在 Visual Studio 中開啟專案/方案，然後開啟 主控台使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。</span><span class="sxs-lookup"><span data-stu-id="627fa-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="627fa-112">尋找您想要安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="627fa-112">Find the package you want to install.</span></span> <span data-ttu-id="627fa-113">如果您已經知道這個，請跳至步驟 3。</span><span class="sxs-lookup"><span data-stu-id="627fa-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="627fa-114">執行安裝命令：</span><span class="sxs-lookup"><span data-stu-id="627fa-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="627fa-115">在主控台中可用的所有作業也都適用於[NuGet CLI](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="627fa-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="627fa-116">不過，主控台命令的 Visual Studio 和儲存的專案/方案內容中運作，而且通常超過其對等的 CLI 命令完成。</span><span class="sxs-lookup"><span data-stu-id="627fa-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="627fa-117">比方說，安裝套件，以透過主控台將參考加入專案而 CLI 命令則否。</span><span class="sxs-lookup"><span data-stu-id="627fa-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="627fa-118">基於這個理由，通常使用 Visual Studio 中的開發人員會偏好使用 cli 主控台。</span><span class="sxs-lookup"><span data-stu-id="627fa-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="627fa-119">許多的主控台作業取決於 Visual Studio 中開啟具有已知的路徑名稱的解決方案。</span><span class="sxs-lookup"><span data-stu-id="627fa-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="627fa-120">如果您有未儲存的方案或沒有解決方案，您可以看到下列錯誤: 」 方案是未開啟，或未儲存。</span><span class="sxs-lookup"><span data-stu-id="627fa-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="627fa-121">請確定您有開啟且已儲存解決方案。 」</span><span class="sxs-lookup"><span data-stu-id="627fa-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="627fa-122">這表示主控台無法判斷方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="627fa-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="627fa-123">正在儲存未儲存的解決方案，或建立及儲存的解答，如果您還沒有開啟，應該更正錯誤。</span><span class="sxs-lookup"><span data-stu-id="627fa-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="627fa-124">開啟的主控台和主控台控制項</span><span class="sxs-lookup"><span data-stu-id="627fa-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="627fa-125">開啟主控台，在 Visual Studio 中使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。</span><span class="sxs-lookup"><span data-stu-id="627fa-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="627fa-126">「 主控台 」 可以安排在程式碼中，置於您隨心所欲的 Visual Studio 視窗 (請參閱[自訂視窗版面配置，在 Visual Studio 中的](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。</span><span class="sxs-lookup"><span data-stu-id="627fa-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="627fa-127">根據預設，主控台命令對特定的套件來源，以及專案在視窗頂端的控制項中的設定：</span><span class="sxs-lookup"><span data-stu-id="627fa-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![封裝來源和專案的套件管理員主控台控制項](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="627fa-129">選取不同的套件來源及/或專案變更這些預設值，後續的命令。</span><span class="sxs-lookup"><span data-stu-id="627fa-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="627fa-130">若要 overrride 而不需要變更預設值，這些設定大部分的命令支援`-Source`和`-ProjectName`選項。</span><span class="sxs-lookup"><span data-stu-id="627fa-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="627fa-131">若要管理的套件來源，選取齒輪圖示。</span><span class="sxs-lookup"><span data-stu-id="627fa-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="627fa-132">這是捷徑**工具 > 選項 > NuGet 套件管理員 > 套件來源**上所述的對話方塊[套件管理員 UI](package-manager-ui.md#package-sources)頁面。</span><span class="sxs-lookup"><span data-stu-id="627fa-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="627fa-133">此外，右邊的專案選取器控制項清除主控台的內容：</span><span class="sxs-lookup"><span data-stu-id="627fa-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![套件管理員主控台設定和清除控制項](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="627fa-135">最右邊的按鈕時，中斷長時間執行命令。</span><span class="sxs-lookup"><span data-stu-id="627fa-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="627fa-136">例如，執行`Get-Package -ListAvailable -PageSize 500`列出前 500 個封裝上的預設來源 （例如 nuget.org)，這可能需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="627fa-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![套件管理員主控台停止控制項](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="627fa-138">安裝套件</span><span class="sxs-lookup"><span data-stu-id="627fa-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="627fa-139">請參閱[Install-package](../tools/ps-ref-install-package.md)。</span><span class="sxs-lookup"><span data-stu-id="627fa-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="627fa-140">在主控台中安裝的套件執行相同的步驟，在所述[安裝套件時，會發生什麼事](../concepts/package-installation-process.md)，加上下列各項：</span><span class="sxs-lookup"><span data-stu-id="627fa-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="627fa-141">主控台會顯示適用的授權條款，在其視窗中使用隱含的合約。</span><span class="sxs-lookup"><span data-stu-id="627fa-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="627fa-142">如果您不同意這些條款，您應該立即解除安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="627fa-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="627fa-143">套件的參考也會新增至專案檔，而且會出現在**方案總管**下方**參考** 節點，您需要儲存專案，以直接查看專案檔中的變更。</span><span class="sxs-lookup"><span data-stu-id="627fa-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="627fa-144">解除安裝套件</span><span class="sxs-lookup"><span data-stu-id="627fa-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="627fa-145">請參閱[解除安裝封裝](../tools/ps-ref-uninstall-package.md)。</span><span class="sxs-lookup"><span data-stu-id="627fa-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="627fa-146">使用[取得封裝](../tools/ps-ref-get-package.md)，查看目前安裝在預設專案中，如果您要尋找識別項的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="627fa-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="627fa-147">解除安裝套件時，會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="627fa-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="627fa-148">移除參考封裝專案 （及正在使用中的任何管理格式）。</span><span class="sxs-lookup"><span data-stu-id="627fa-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="627fa-149">參考不會再出現在**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="627fa-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="627fa-150">(您可能需要重建專案，以查看它移除了**Bin**資料夾。)</span><span class="sxs-lookup"><span data-stu-id="627fa-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="627fa-151">反轉所做的變更`app.config`或`web.config`安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="627fa-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="627fa-152">如果沒有任何剩餘的套件會使用這些相依性移除先前安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="627fa-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="627fa-153">更新套件</span><span class="sxs-lookup"><span data-stu-id="627fa-153">Updating a package</span></span>

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

<span data-ttu-id="627fa-154">請參閱[取得封裝](../tools/ps-ref-get-package.md)和[更新套件](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="627fa-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="627fa-155">尋找套件</span><span class="sxs-lookup"><span data-stu-id="627fa-155">Finding a package</span></span>

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

<span data-ttu-id="627fa-156">請參閱[Find-package](../tools/ps-ref-find-package.md)。</span><span class="sxs-lookup"><span data-stu-id="627fa-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="627fa-157">在 Visual Studio 2013 和舊版中，使用[取得封裝](../tools/ps-ref-get-package.md)改。</span><span class="sxs-lookup"><span data-stu-id="627fa-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="627fa-158">在主控台的可用性</span><span class="sxs-lookup"><span data-stu-id="627fa-158">Availability of the console</span></span>

<span data-ttu-id="627fa-159">從 Visual Studio 2017，NuGet 和 NuGet 套件管理員會自動安裝時選取任何。NET 相關的工作負載;您也可以安裝其個別檢查**個別元件 > 程式碼工具 > NuGet 套件管理員**Visual Studio 安裝程式中的選項。</span><span class="sxs-lookup"><span data-stu-id="627fa-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="627fa-160">此外，如果您缺少的 NuGet 套件管理員，在 Visual Studio 2015 和更早版本，請檢查**工具 > 擴充功能和更新...** 並搜尋 NuGet 套件管理員延伸模組。</span><span class="sxs-lookup"><span data-stu-id="627fa-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="627fa-161">如果您無法使用 Visual Studio 中的延伸模組安裝程式，您可以下載的擴充功能，直接從[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="627fa-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="627fa-162">套件管理員主控台不是目前使用 Visual Studio for mac。</span><span class="sxs-lookup"><span data-stu-id="627fa-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="627fa-163">對等的命令，不過，都是透過[NuGet CLI](nuget-exe-CLI-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="627fa-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="627fa-164">Visual Studio for Mac 有 UI 來管理 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="627fa-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="627fa-165">請參閱[在專案中的包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="627fa-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="627fa-166">套件管理員主控台不會包含使用 Visual Studio Code 的。</span><span class="sxs-lookup"><span data-stu-id="627fa-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="627fa-167">擴充套件管理員主控台</span><span class="sxs-lookup"><span data-stu-id="627fa-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="627fa-168">有些套件會安裝新的命令主控台。</span><span class="sxs-lookup"><span data-stu-id="627fa-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="627fa-169">例如，`MvcScaffolding`會建立類似的命令`Scaffold`如下所示，如此就會產生 ASP.NET MVC 控制器和檢視：</span><span class="sxs-lookup"><span data-stu-id="627fa-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![安裝和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="627fa-171">設定 NuGet PowerShell 設定檔</span><span class="sxs-lookup"><span data-stu-id="627fa-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="627fa-172">PowerShell 設定檔可讓您無論在何處使用 PowerShell 將常用命令提供。</span><span class="sxs-lookup"><span data-stu-id="627fa-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="627fa-173">NuGet 支援 NuGet 特定設定檔通常位於下列位置找到：</span><span class="sxs-lookup"><span data-stu-id="627fa-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="627fa-174">若要尋找設定檔，請輸入`$profile`在主控台中：</span><span class="sxs-lookup"><span data-stu-id="627fa-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="627fa-175">如需詳細資訊，請參閱[Windows PowerShell 設定檔](https://technet.microsoft.com/library/bb613488.aspx)。</span><span class="sxs-lookup"><span data-stu-id="627fa-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="627fa-176">使用 nuget.exe CLI，在主控台中</span><span class="sxs-lookup"><span data-stu-id="627fa-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="627fa-177">若要讓[ `nuget.exe` CLI](nuget-exe-cli-reference.md)可用在套件管理員主控台中，安裝[NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)從主控台的封裝：</span><span class="sxs-lookup"><span data-stu-id="627fa-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
