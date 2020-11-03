---
title: NuGet PowerShell 參考
description: 您可以在 Visual Studio 中的 NuGet 封裝管理員主控台取得 PowerShell 命令的完整參考。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 4f8b42847cbc155393fe6d2afbe2e0857b619da3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236876"
---
# <a name="powershell-reference"></a><span data-ttu-id="4a784-103">PowerShell 參考</span><span class="sxs-lookup"><span data-stu-id="4a784-103">PowerShell reference</span></span>

<span data-ttu-id="4a784-104">封裝管理員主控台提供 Windows Visual Studio 內的 PowerShell 介面，可透過下列特定命令與 NuGet 互動。</span><span class="sxs-lookup"><span data-stu-id="4a784-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="4a784-105"> (主控台目前無法在 Visual Studio for Mac 中使用。 ) 如需使用主控台的指南，請參閱 [使用封裝管理員主控台安裝及管理套件](../consume-packages/install-use-packages-powershell.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="4a784-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="4a784-106">所有 PowerShell 命令都只與套件耗用量相關。</span><span class="sxs-lookup"><span data-stu-id="4a784-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="4a784-107">除了套件也可以是其他封裝的取用者之外，沒有任何 PowerShell 命令與建立和發佈套件有關。</span><span class="sxs-lookup"><span data-stu-id="4a784-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="4a784-108">此處所列的命令是 Visual Studio 中的封裝管理員主控台特定的命令，不同于一般 PowerShell 環境中可用的 [套件管理模組命令](/powershell/module/packagemanagement/?view=powershell-6) 。</span><span class="sxs-lookup"><span data-stu-id="4a784-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="4a784-109">具體而言，每個環境都有其他無法使用的命令，而且具有相同名稱的命令在其特定引數中也可能不同。</span><span class="sxs-lookup"><span data-stu-id="4a784-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="4a784-110">當您在 Visual Studio 中使用套件管理主控台時，適用于本主題中記載的命令和引數適用于。</span><span class="sxs-lookup"><span data-stu-id="4a784-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="4a784-111">常見命令</span><span class="sxs-lookup"><span data-stu-id="4a784-111">Common Commands</span></span> | <span data-ttu-id="4a784-112">Description</span><span class="sxs-lookup"><span data-stu-id="4a784-112">Description</span></span> | <span data-ttu-id="4a784-113">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="4a784-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4a784-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="4a784-114">Install-Package</span></span>](ps-reference/ps-ref-install-package.md) | <span data-ttu-id="4a784-115">將封裝及其相依性安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="4a784-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="4a784-116">全部</span><span class="sxs-lookup"><span data-stu-id="4a784-116">All</span></span> |
| [<span data-ttu-id="4a784-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="4a784-117">Update-Package</span></span>](ps-reference/ps-ref-update-package.md) | <span data-ttu-id="4a784-118">更新封裝及其相依性，或專案中的所有套件。</span><span class="sxs-lookup"><span data-stu-id="4a784-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="4a784-119">全部</span><span class="sxs-lookup"><span data-stu-id="4a784-119">All</span></span> |
| [<span data-ttu-id="4a784-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="4a784-120">Find-Package</span></span>](ps-reference/ps-ref-find-package.md) | <span data-ttu-id="4a784-121">使用封裝識別碼或關鍵字搜尋封裝來源。</span><span class="sxs-lookup"><span data-stu-id="4a784-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="4a784-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="4a784-122">3.0+</span></span> |
| [<span data-ttu-id="4a784-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="4a784-123">Get-Package</span></span>](ps-reference/ps-ref-get-package.md) | <span data-ttu-id="4a784-124">抓取本機存放庫中所安裝的套件清單，或列出可從套件來源取得的封裝。</span><span class="sxs-lookup"><span data-stu-id="4a784-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="4a784-125">全部</span><span class="sxs-lookup"><span data-stu-id="4a784-125">All</span></span> |

| <span data-ttu-id="4a784-126">次要命令</span><span class="sxs-lookup"><span data-stu-id="4a784-126">Secondary Commands</span></span> | <span data-ttu-id="4a784-127">Description</span><span class="sxs-lookup"><span data-stu-id="4a784-127">Description</span></span> | <span data-ttu-id="4a784-128">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="4a784-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4a784-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="4a784-129">Add-BindingRedirect</span></span>](ps-reference/ps-ref-add-bindingredirect.md) | <span data-ttu-id="4a784-130">檢查項目輸出路徑內的所有元件，並將系結重新導向加入至 `app.config` 或 `web.config` 需要的位置。</span><span class="sxs-lookup"><span data-stu-id="4a784-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="4a784-131">全部</span><span class="sxs-lookup"><span data-stu-id="4a784-131">All</span></span> |
| [<span data-ttu-id="4a784-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="4a784-132">Get-Project</span></span>](ps-reference/ps-ref-get-project.md) | <span data-ttu-id="4a784-133">顯示預設或指定專案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4a784-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="4a784-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="4a784-134">3.0+</span></span> |
| [<span data-ttu-id="4a784-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="4a784-135">Open-PackagePage</span></span>](ps-reference/ps-ref-open-packagepage.md) | <span data-ttu-id="4a784-136">使用指定封裝的專案、授權或報告濫用 URL 來啟動預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4a784-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="4a784-137">已在 3.0 + 中淘汰</span><span class="sxs-lookup"><span data-stu-id="4a784-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="4a784-138">註冊-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="4a784-138">Register-TabExpansion</span></span>](ps-reference/ps-ref-register-tabexpansion.md) | <span data-ttu-id="4a784-139">註冊命令參數的索引標籤展開，可讓您建立常用參數值的自訂擴充。</span><span class="sxs-lookup"><span data-stu-id="4a784-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="4a784-140">全部</span><span class="sxs-lookup"><span data-stu-id="4a784-140">All</span></span> |
| [<span data-ttu-id="4a784-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="4a784-141">Sync-Package</span></span>](ps-reference/ps-ref-sync-package.md) | <span data-ttu-id="4a784-142">從指定的專案取得已安裝套件的版本，並將版本同步處理至方案中的其餘專案。</span><span class="sxs-lookup"><span data-stu-id="4a784-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="4a784-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="4a784-143">3.0+</span></span> |
| [<span data-ttu-id="4a784-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="4a784-144">Uninstall-Package</span></span>](ps-reference/ps-ref-uninstall-package.md) | <span data-ttu-id="4a784-145">移除專案中的封裝，並選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="4a784-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="4a784-146">全部</span><span class="sxs-lookup"><span data-stu-id="4a784-146">All</span></span> |

<span data-ttu-id="4a784-147">如需主控台內任何這些命令的完整詳細說明，請使用下列命令名稱來執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="4a784-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="4a784-148">所有封裝管理員主控台命令都支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：</span><span class="sxs-lookup"><span data-stu-id="4a784-148">All Package Manager Console commands support the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters):</span></span>

- <span data-ttu-id="4a784-149">偵錯</span><span class="sxs-lookup"><span data-stu-id="4a784-149">Debug</span></span>
- <span data-ttu-id="4a784-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="4a784-150">ErrorAction</span></span>
- <span data-ttu-id="4a784-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="4a784-151">ErrorVariable</span></span>
- <span data-ttu-id="4a784-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="4a784-152">OutBuffer</span></span>
- <span data-ttu-id="4a784-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="4a784-153">OutVariable</span></span>
- <span data-ttu-id="4a784-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="4a784-154">PipelineVariable</span></span>
- <span data-ttu-id="4a784-155">「詳細資訊」</span><span class="sxs-lookup"><span data-stu-id="4a784-155">Verbose</span></span>
- <span data-ttu-id="4a784-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="4a784-156">WarningAction</span></span>
- <span data-ttu-id="4a784-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="4a784-157">WarningVariable</span></span>

<span data-ttu-id="4a784-158">如需詳細資訊，請參閱 PowerShell 檔中的 [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) 。</span><span class="sxs-lookup"><span data-stu-id="4a784-158">For details, refer to [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) in the PowerShell documentation.</span></span>