---
title: NuGet PowerShell 參考
description: Visual Studio 中的 NuGet 封裝管理員主控台中可用的 PowerShell 命令的完整參考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: ba9f5dc2b570298d9011f62a081631ec31623701
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816986"
---
# <a name="powershell-reference"></a><span data-ttu-id="027cc-103">PowerShell 參考</span><span class="sxs-lookup"><span data-stu-id="027cc-103">PowerShell reference</span></span>

<span data-ttu-id="027cc-104">Package Manager Console 提供下面所列的過特定的命令與 NuGet 互動的 Windows 上的 Visual Studio 中的 PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="027cc-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="027cc-105">（[] 主控台不是目前可用在 Visual Studio for mac。）使用主控台的指引，請參閱[Package Manager Console](../tools/package-manager-console.md)主題。</span><span class="sxs-lookup"><span data-stu-id="027cc-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="027cc-106">所有的 PowerShell 命令僅與封裝耗用量。</span><span class="sxs-lookup"><span data-stu-id="027cc-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="027cc-107">建立和發佈封裝以外，封裝也可以是其他封裝的消費者，與沒有 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="027cc-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="027cc-108">此處所列的命令專屬於在 Visual Studio 中，在 Package Manager Console 而不同[封裝管理模組命令](/powershell/module/packagemanagement/?view=powershell-6)可在一般的 PowerShell 環境中。</span><span class="sxs-lookup"><span data-stu-id="027cc-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="027cc-109">具體來說，每個環境有不適用於其他的命令，並在其特定的引數中，可能也不同命令具有相同名稱。</span><span class="sxs-lookup"><span data-stu-id="027cc-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="027cc-110">當使用 Visual Studio 中的封裝管理主控台，指令及引數有本文所述套用。</span><span class="sxs-lookup"><span data-stu-id="027cc-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="027cc-111">常見命令</span><span class="sxs-lookup"><span data-stu-id="027cc-111">Common Commands</span></span> | <span data-ttu-id="027cc-112">描述</span><span class="sxs-lookup"><span data-stu-id="027cc-112">Description</span></span> | <span data-ttu-id="027cc-113">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="027cc-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="027cc-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="027cc-114">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="027cc-115">在專案中安裝封裝及其相依性。</span><span class="sxs-lookup"><span data-stu-id="027cc-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="027cc-116">全部</span><span class="sxs-lookup"><span data-stu-id="027cc-116">All</span></span> |
| [<span data-ttu-id="027cc-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="027cc-117">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="027cc-118">更新封裝和其相依性或在專案中的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="027cc-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="027cc-119">全部</span><span class="sxs-lookup"><span data-stu-id="027cc-119">All</span></span> |
| [<span data-ttu-id="027cc-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="027cc-120">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="027cc-121">搜尋使用的封裝識別碼或關鍵字的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="027cc-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="027cc-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="027cc-122">3.0+</span></span> |
| [<span data-ttu-id="027cc-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="027cc-123">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="027cc-124">擷取安裝在本機儲存機制中，封裝的清單，或列出可用的封裝，從套件來源。</span><span class="sxs-lookup"><span data-stu-id="027cc-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="027cc-125">全部</span><span class="sxs-lookup"><span data-stu-id="027cc-125">All</span></span> |

| <span data-ttu-id="027cc-126">第二個命令</span><span class="sxs-lookup"><span data-stu-id="027cc-126">Secondary Commands</span></span> | <span data-ttu-id="027cc-127">描述</span><span class="sxs-lookup"><span data-stu-id="027cc-127">Description</span></span> | <span data-ttu-id="027cc-128">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="027cc-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="027cc-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="027cc-129">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="027cc-130">檢查專案的輸出路徑內的所有組件，並將繫結重新導向至`app.config`或`web.config`在需要時。</span><span class="sxs-lookup"><span data-stu-id="027cc-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="027cc-131">全部</span><span class="sxs-lookup"><span data-stu-id="027cc-131">All</span></span> |
| [<span data-ttu-id="027cc-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="027cc-132">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="027cc-133">顯示預設值或指定的專案相關資訊。</span><span class="sxs-lookup"><span data-stu-id="027cc-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="027cc-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="027cc-134">3.0+</span></span> |
| [<span data-ttu-id="027cc-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="027cc-135">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="027cc-136">啟動預設瀏覽器中使用專案、 授權或指定之封裝的報表濫用 URL。</span><span class="sxs-lookup"><span data-stu-id="027cc-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="027cc-137">在 3.0 + 已被取代</span><span class="sxs-lookup"><span data-stu-id="027cc-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="027cc-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="027cc-138">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="027cc-139">登錄參數的命令，可讓您建立的常用的參數值的自訂擴充功能的 tab 鍵擴充。</span><span class="sxs-lookup"><span data-stu-id="027cc-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="027cc-140">全部</span><span class="sxs-lookup"><span data-stu-id="027cc-140">All</span></span> |
| [<span data-ttu-id="027cc-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="027cc-141">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="027cc-142">取得已安裝的版本封裝從指定專案和同步到解決方案中專案的其餘部分的版本。</span><span class="sxs-lookup"><span data-stu-id="027cc-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="027cc-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="027cc-143">3.0+</span></span> |
| [<span data-ttu-id="027cc-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="027cc-144">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="027cc-145">移除封裝在專案中，選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="027cc-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="027cc-146">全部</span><span class="sxs-lookup"><span data-stu-id="027cc-146">All</span></span> |

<span data-ttu-id="027cc-147">如需這些命令主控台內的任何完整的詳細說明，只要有問題的命令名稱與執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="027cc-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="027cc-148">所有套件管理器主控台命令都支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="027cc-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="027cc-149">偵錯</span><span class="sxs-lookup"><span data-stu-id="027cc-149">Debug</span></span>
- <span data-ttu-id="027cc-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="027cc-150">ErrorAction</span></span>
- <span data-ttu-id="027cc-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="027cc-151">ErrorVariable</span></span>
- <span data-ttu-id="027cc-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="027cc-152">OutBuffer</span></span>
- <span data-ttu-id="027cc-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="027cc-153">OutVariable</span></span>
- <span data-ttu-id="027cc-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="027cc-154">PipelineVariable</span></span>
- <span data-ttu-id="027cc-155">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="027cc-155">Verbose</span></span>
- <span data-ttu-id="027cc-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="027cc-156">WarningAction</span></span>
- <span data-ttu-id="027cc-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="027cc-157">WarningVariable</span></span>

<span data-ttu-id="027cc-158">如需詳細資訊，請參閱[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 文件中。</span><span class="sxs-lookup"><span data-stu-id="027cc-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
