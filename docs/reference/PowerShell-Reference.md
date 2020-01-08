---
title: NuGet PowerShell 參考
description: Visual Studio 中的 NuGet 套件管理員主控台所提供 PowerShell 命令的完整參考。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 2a82b1977265a8f8a15247759bc3de80a5efe228
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385339"
---
# <a name="powershell-reference"></a><span data-ttu-id="9d311-103">PowerShell 參考</span><span class="sxs-lookup"><span data-stu-id="9d311-103">PowerShell reference</span></span>

<span data-ttu-id="9d311-104">套件管理員主控台會在 Windows Visual Studio 內提供 PowerShell 介面，以透過下列特定命令與 NuGet 互動。</span><span class="sxs-lookup"><span data-stu-id="9d311-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="9d311-105">（目前無法在 Visual Studio for Mac 中使用主控台）。如需使用主控台的指南，請參閱[使用套件管理員主控台安裝和管理套件](../consume-packages/install-use-packages-powershell.md)主題。</span><span class="sxs-lookup"><span data-stu-id="9d311-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="9d311-106">所有 PowerShell 命令都只與套件耗用量相關。</span><span class="sxs-lookup"><span data-stu-id="9d311-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="9d311-107">除了封裝也可以是其他套件取用者的範圍之外，沒有任何 PowerShell 命令與建立和發行封裝有關。</span><span class="sxs-lookup"><span data-stu-id="9d311-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="9d311-108">此處所列的命令是 Visual Studio 中的套件管理員主控台所特有，而且與一般 PowerShell 環境中可用的[套件管理模組命令](/powershell/module/packagemanagement/?view=powershell-6)不同。</span><span class="sxs-lookup"><span data-stu-id="9d311-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="9d311-109">具體而言，每個環境都有其他無法使用的命令，而且具有相同名稱的命令在其特定引數中也可能不同。</span><span class="sxs-lookup"><span data-stu-id="9d311-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="9d311-110">在 Visual Studio 中使用套件管理主控台時，會套用此目前主題中記載的命令和引數。</span><span class="sxs-lookup"><span data-stu-id="9d311-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="9d311-111">一般命令</span><span class="sxs-lookup"><span data-stu-id="9d311-111">Common Commands</span></span> | <span data-ttu-id="9d311-112">描述</span><span class="sxs-lookup"><span data-stu-id="9d311-112">Description</span></span> | <span data-ttu-id="9d311-113">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="9d311-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="9d311-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="9d311-114">Install-Package</span></span>](ps-reference/ps-ref-install-package.md) | <span data-ttu-id="9d311-115">將封裝及其相依性安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="9d311-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="9d311-116">全部</span><span class="sxs-lookup"><span data-stu-id="9d311-116">All</span></span> |
| [<span data-ttu-id="9d311-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="9d311-117">Update-Package</span></span>](ps-reference/ps-ref-update-package.md) | <span data-ttu-id="9d311-118">更新封裝及其相依性，或專案中的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="9d311-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="9d311-119">全部</span><span class="sxs-lookup"><span data-stu-id="9d311-119">All</span></span> |
| [<span data-ttu-id="9d311-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="9d311-120">Find-Package</span></span>](ps-reference/ps-ref-find-package.md) | <span data-ttu-id="9d311-121">使用套件識別碼或關鍵字搜尋封裝來源。</span><span class="sxs-lookup"><span data-stu-id="9d311-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="9d311-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="9d311-122">3.0+</span></span> |
| [<span data-ttu-id="9d311-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="9d311-123">Get-Package</span></span>](ps-reference/ps-ref-get-package.md) | <span data-ttu-id="9d311-124">抓取本機存放庫中安裝的封裝清單，或列出可從封裝來源取得的套件。</span><span class="sxs-lookup"><span data-stu-id="9d311-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="9d311-125">全部</span><span class="sxs-lookup"><span data-stu-id="9d311-125">All</span></span> |

| <span data-ttu-id="9d311-126">次要命令</span><span class="sxs-lookup"><span data-stu-id="9d311-126">Secondary Commands</span></span> | <span data-ttu-id="9d311-127">描述</span><span class="sxs-lookup"><span data-stu-id="9d311-127">Description</span></span> | <span data-ttu-id="9d311-128">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="9d311-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="9d311-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="9d311-129">Add-BindingRedirect</span></span>](ps-reference/ps-ref-add-bindingredirect.md) | <span data-ttu-id="9d311-130">檢查項目輸出路徑中的所有元件，並在必要時將系結重新導向新增至 `app.config` 或 `web.config`。</span><span class="sxs-lookup"><span data-stu-id="9d311-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="9d311-131">全部</span><span class="sxs-lookup"><span data-stu-id="9d311-131">All</span></span> |
| [<span data-ttu-id="9d311-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="9d311-132">Get-Project</span></span>](ps-reference/ps-ref-get-project.md) | <span data-ttu-id="9d311-133">顯示預設或指定專案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9d311-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="9d311-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="9d311-134">3.0+</span></span> |
| [<span data-ttu-id="9d311-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="9d311-135">Open-PackagePage</span></span>](ps-reference/ps-ref-open-packagepage.md) | <span data-ttu-id="9d311-136">使用指定封裝的 [專案]、[授權] 或 [報表濫用 URL] 來啟動預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9d311-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="9d311-137">3\.0 + 中已淘汰</span><span class="sxs-lookup"><span data-stu-id="9d311-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="9d311-138">註冊-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="9d311-138">Register-TabExpansion</span></span>](ps-reference/ps-ref-register-tabexpansion.md) | <span data-ttu-id="9d311-139">為命令的參數註冊 tab 鍵擴充，可讓您為常用的參數值建立自訂的擴充。</span><span class="sxs-lookup"><span data-stu-id="9d311-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="9d311-140">全部</span><span class="sxs-lookup"><span data-stu-id="9d311-140">All</span></span> |
| [<span data-ttu-id="9d311-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="9d311-141">Sync-Package</span></span>](ps-reference/ps-ref-sync-package.md) | <span data-ttu-id="9d311-142">從指定的專案取得已安裝套件的版本，並將版本同步處理至方案中的其餘專案。</span><span class="sxs-lookup"><span data-stu-id="9d311-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="9d311-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="9d311-143">3.0+</span></span> |
| [<span data-ttu-id="9d311-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="9d311-144">Uninstall-Package</span></span>](ps-reference/ps-ref-uninstall-package.md) | <span data-ttu-id="9d311-145">移除專案中的封裝，並選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="9d311-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="9d311-146">全部</span><span class="sxs-lookup"><span data-stu-id="9d311-146">All</span></span> |

<span data-ttu-id="9d311-147">如需有關主控台內任何這些命令的完整詳細說明，請執行下列命令，並提出問題：</span><span class="sxs-lookup"><span data-stu-id="9d311-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="9d311-148">所有套件管理員主控台命令都支援下列[常用的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)：</span><span class="sxs-lookup"><span data-stu-id="9d311-148">All Package Manager Console commands support the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="9d311-149">偵錯</span><span class="sxs-lookup"><span data-stu-id="9d311-149">Debug</span></span>
- <span data-ttu-id="9d311-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="9d311-150">ErrorAction</span></span>
- <span data-ttu-id="9d311-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="9d311-151">ErrorVariable</span></span>
- <span data-ttu-id="9d311-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="9d311-152">OutBuffer</span></span>
- <span data-ttu-id="9d311-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="9d311-153">OutVariable</span></span>
- <span data-ttu-id="9d311-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="9d311-154">PipelineVariable</span></span>
- <span data-ttu-id="9d311-155">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="9d311-155">Verbose</span></span>
- <span data-ttu-id="9d311-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="9d311-156">WarningAction</span></span>
- <span data-ttu-id="9d311-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="9d311-157">WarningVariable</span></span>

<span data-ttu-id="9d311-158">如需詳細資訊，請參閱 PowerShell 檔中的[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216) 。</span><span class="sxs-lookup"><span data-stu-id="9d311-158">For details, refer to [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
