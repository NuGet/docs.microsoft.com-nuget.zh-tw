---
title: NuGet 封裝管理員主控台指南
description: 使用 Visual Studio 中的 NuGet 封裝管理員主控台，使用封裝的指示。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 06c525cab2dac61c92c4596533173f1d93493d9a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817654"
---
# <a name="package-manager-console"></a><span data-ttu-id="e4a58-103">套件管理員主控台</span><span class="sxs-lookup"><span data-stu-id="e4a58-103">Package Manager Console</span></span>

<span data-ttu-id="e4a58-104">NuGet 封裝管理員主控台內建在 Windows 2012 及更新版本的 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="e4a58-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="e4a58-105">（它不包含在 Visual Studio for Mac 或 Visual Studio 程式碼）。</span><span class="sxs-lookup"><span data-stu-id="e4a58-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="e4a58-106">在主控台可讓您使用[NuGet PowerShell 命令](../tools/powershell-reference.md)尋找、 安裝、 解除安裝和更新 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="e4a58-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="e4a58-107">在 「 封裝管理員 」 UI 不提供方法來執行作業的情況下，必須使用主控台。</span><span class="sxs-lookup"><span data-stu-id="e4a58-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="e4a58-108">若要使用`nuget.exe`命令在主控台中，請參閱[使用主控台中的 nuget.exe CLI](#using-the-nugetexe-cli-in-the-console)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="e4a58-109">例如，尋找和安裝封裝是使用三個簡單步驟完成：</span><span class="sxs-lookup"><span data-stu-id="e4a58-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="e4a58-110">在 Visual Studio 中，開啟 專案/方案，並開啟主控台使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。</span><span class="sxs-lookup"><span data-stu-id="e4a58-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="e4a58-111">尋找您想要安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="e4a58-111">Find the package you want to install.</span></span> <span data-ttu-id="e4a58-112">如果您已經知道這個，請跳至步驟 3。</span><span class="sxs-lookup"><span data-stu-id="e4a58-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="e4a58-113">執行安裝命令：</span><span class="sxs-lookup"><span data-stu-id="e4a58-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="e4a58-114">也可以使用完成所有作業都可在主控台[NuGet CLI](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="e4a58-115">不過，主控台命令的 Visual Studio，並儲存的專案/方案內容中運作，而且通常超過其對等的 CLI 命令完成。</span><span class="sxs-lookup"><span data-stu-id="e4a58-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="e4a58-116">比方說，安裝套件，以透過主控台將參考加入專案而不 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="e4a58-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="e4a58-117">基於這個理由，通常使用 Visual Studio 中的開發人員會習慣使用 CLI 至主控台。</span><span class="sxs-lookup"><span data-stu-id="e4a58-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="e4a58-118">許多的主控台作業取決於 Visual Studio 中開啟具有已知的路徑名稱的解決方案。</span><span class="sxs-lookup"><span data-stu-id="e4a58-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="e4a58-119">如果您有未儲存的方案或沒有解決方案，您可以看到下列錯誤:"是未開啟或儲存方案。</span><span class="sxs-lookup"><span data-stu-id="e4a58-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="e4a58-120">請確定您有已開啟和已儲存的方案。 」</span><span class="sxs-lookup"><span data-stu-id="e4a58-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="e4a58-121">這表示主控台無法判斷方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="e4a58-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="e4a58-122">儲存未儲存的方案，或建立及儲存方案，如果您還沒有開啟，應該更正錯誤。</span><span class="sxs-lookup"><span data-stu-id="e4a58-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="e4a58-123">開啟的主控台和主控台控制項</span><span class="sxs-lookup"><span data-stu-id="e4a58-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="e4a58-124">開啟主控台，在 Visual Studio 使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。</span><span class="sxs-lookup"><span data-stu-id="e4a58-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="e4a58-125">主控台的 Visual Studio 視窗可以排列和定位不過嗎 (請參閱[自訂 Visual Studio 中的視窗配置](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。</span><span class="sxs-lookup"><span data-stu-id="e4a58-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="e4a58-126">根據預設，主控台命令做為針對特定的封裝來源和專案集合中的控制項視窗的頂端：</span><span class="sxs-lookup"><span data-stu-id="e4a58-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![封裝來源和專案的封裝管理員主控台控制項](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="e4a58-128">選取不同的封裝來源及/或專案就會變更後續命令的這些預設值。</span><span class="sxs-lookup"><span data-stu-id="e4a58-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="e4a58-129">若要 overrride 而不需要變更預設值，這些設定大部分的命令支援`-Source`和`-ProjectName`選項。</span><span class="sxs-lookup"><span data-stu-id="e4a58-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="e4a58-130">若要管理的封裝來源，請選取齒輪圖示。</span><span class="sxs-lookup"><span data-stu-id="e4a58-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="e4a58-131">這是捷徑**工具 > 選項 > NuGet 套件管理員 > 的封裝來源**對話方塊上所述[封裝管理員 UI](package-manager-ui.md#package-sources)頁面。</span><span class="sxs-lookup"><span data-stu-id="e4a58-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="e4a58-132">此外，右邊的專案選擇器控制項清除主控台的內容：</span><span class="sxs-lookup"><span data-stu-id="e4a58-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![封裝管理員主控台設定和清除控制項](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="e4a58-134">最右邊的按鈕會中斷長時間執行命令。</span><span class="sxs-lookup"><span data-stu-id="e4a58-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="e4a58-135">例如，執行`Get-Package -ListAvailable -PageSize 500`列出的前 500 套件上的預設來源 （例如 nuget.org)，這可能需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="e4a58-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![封裝管理員主控台停止控制](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="e4a58-137">安裝封裝</span><span class="sxs-lookup"><span data-stu-id="e4a58-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="e4a58-138">請參閱[Install-package](../tools/ps-ref-install-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="e4a58-139">安裝封裝，在主控台中執行相同的步驟，如下所述[安裝封裝時，會發生什麼事](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed)，具有下列功能：</span><span class="sxs-lookup"><span data-stu-id="e4a58-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="e4a58-140">主控台會顯示適用之授權條款，其使用隱含協議 視窗中。</span><span class="sxs-lookup"><span data-stu-id="e4a58-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="e4a58-141">如果您不同意這些條款，您應該立即解除安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="e4a58-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="e4a58-142">封裝的參考也會加入至專案檔，而且會出現在**方案總管 中**下**參考** 節點，您需要儲存專案以直接查看專案檔中的變更。</span><span class="sxs-lookup"><span data-stu-id="e4a58-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="e4a58-143">解除安裝封裝</span><span class="sxs-lookup"><span data-stu-id="e4a58-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="e4a58-144">請參閱[解除安裝封裝](../tools/ps-ref-uninstall-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="e4a58-145">使用[Get 封裝](../tools/ps-ref-get-package.md)，查看目前安裝在預設專案中，如果您要尋找識別項的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="e4a58-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="e4a58-146">解除安裝封裝，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e4a58-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="e4a58-147">移除參考封裝專案 （及管理的格式是使用中）。</span><span class="sxs-lookup"><span data-stu-id="e4a58-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="e4a58-148">參考不再出現於**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="e4a58-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="e4a58-149">(您可能需要重建專案，以查看它從移除**Bin**資料夾。)</span><span class="sxs-lookup"><span data-stu-id="e4a58-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="e4a58-150">反轉所做的變更`app.config`或`web.config`已經安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="e4a58-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="e4a58-151">如果沒有剩餘的封裝，請使用這些依存性移除先前安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="e4a58-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="e4a58-152">更新封裝</span><span class="sxs-lookup"><span data-stu-id="e4a58-152">Updating a package</span></span>

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

<span data-ttu-id="e4a58-153">請參閱[Get 封裝](../tools/ps-ref-get-package.md)和[更新套件](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="e4a58-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="e4a58-154">尋找封裝</span><span class="sxs-lookup"><span data-stu-id="e4a58-154">Finding a package</span></span>

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

<span data-ttu-id="e4a58-155">請參閱[Find-package](../tools/ps-ref-find-package.md)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="e4a58-156">在 Visual Studio 2013 和舊版中，使用[Get 封裝](../tools/ps-ref-get-package.md)改為。</span><span class="sxs-lookup"><span data-stu-id="e4a58-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="e4a58-157">在主控台的可用性</span><span class="sxs-lookup"><span data-stu-id="e4a58-157">Availability of the console</span></span>

<span data-ttu-id="e4a58-158">在 Visual Studio 2017，NuGet 和 NuGet 套件管理員會自動安裝時選取任何。網路相關的工作負載;您也可以安裝它個別藉由檢查**個別元件 > 程式碼工具 > NuGet 套件管理員**選項在 Visual Studio 2017 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="e4a58-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="e4a58-159">此外，如果您遺漏的 NuGet 封裝管理員 Visual Studio 2015 中及更早版本，請檢查**工具 > 擴充功能和更新...** ，並搜尋 NuGet 套件管理員擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e4a58-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="e4a58-160">如果您無法使用 Visual Studio 中的擴充功能安裝程式，您可以下載擴充功能直接從[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="e4a58-161">Package Manager Console 不是目前適用於 Visual Studio for mac。</span><span class="sxs-lookup"><span data-stu-id="e4a58-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="e4a58-162">對等的命令，不過，可透過[NuGet CLI](nuget-exe-CLI-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="e4a58-163">Visual Studio for Mac 並沒有使用者介面來管理 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="e4a58-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="e4a58-164">請參閱[您的專案中包括的 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="e4a58-165">Package Manager Console 未隨附於 Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e4a58-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="e4a58-166">延伸封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="e4a58-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="e4a58-167">有些封裝安裝主控台的新命令。</span><span class="sxs-lookup"><span data-stu-id="e4a58-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="e4a58-168">例如，`MvcScaffolding`建立類似的命令`Scaffold`如下所示，如此就會產生 ASP.NET MVC 控制器和檢視：</span><span class="sxs-lookup"><span data-stu-id="e4a58-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![安裝和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="e4a58-170">NuGet PowerShell 設定檔設定</span><span class="sxs-lookup"><span data-stu-id="e4a58-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="e4a58-171">PowerShell 設定檔可讓您開放常用的命令使用，只要您使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e4a58-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="e4a58-172">NuGet 支援特定的 NuGet 設定檔，通常在下列位置找到：</span><span class="sxs-lookup"><span data-stu-id="e4a58-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="e4a58-173">若要尋找的設定檔，請輸入`$profile`主控台中：</span><span class="sxs-lookup"><span data-stu-id="e4a58-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="e4a58-174">如需詳細資訊，請參閱[Windows PowerShell 設定檔](https://technet.microsoft.com/library/bb613488.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e4a58-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="e4a58-175">使用主控台中的 nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="e4a58-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="e4a58-176">若要讓[ `nuget.exe` CLI](nuget-exe-cli-reference.md)可用在封裝管理員主控台中，安裝[NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)封裝從主控台：</span><span class="sxs-lookup"><span data-stu-id="e4a58-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
