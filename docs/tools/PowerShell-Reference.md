---
title: NuGet PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台中可用的 PowerShell 命令來完成的參考。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 425ba736eba4609ebd6b5185ae3f1f976ab07a67
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842569"
---
# <a name="powershell-reference"></a><span data-ttu-id="77ee0-103">PowerShell 參考</span><span class="sxs-lookup"><span data-stu-id="77ee0-103">PowerShell reference</span></span>

<span data-ttu-id="77ee0-104">套件管理員主控台提供如下所示的 PowerShell 介面，以透過特定的命令與 NuGet 互動的 Windows 上的 Visual Studio 內。</span><span class="sxs-lookup"><span data-stu-id="77ee0-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="77ee0-105">（[] 主控台不是目前可在 Visual Studio for mac）如需使用主控台的指南，請參閱[安裝和管理套件使用 Package Manager Console](../tools/package-manager-console.md)主題。</span><span class="sxs-lookup"><span data-stu-id="77ee0-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using the Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="77ee0-106">所有的 PowerShell 命令只與套件耗用量。</span><span class="sxs-lookup"><span data-stu-id="77ee0-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="77ee0-107">建立及發行套件以外，封裝也可以是其他套件的取用者，與不相關任何 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="77ee0-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="77ee0-108">此處所列的命令是專用的 Package Manager Console，在 Visual Studio 中，而且不同於[套件管理模組命令](/powershell/module/packagemanagement/?view=powershell-6)所提供的一般的 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="77ee0-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="77ee0-109">具體來說，每個環境都不在另一個，可用的命令和其特定的引數具有相同名稱的命令可能也有不同。</span><span class="sxs-lookup"><span data-stu-id="77ee0-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="77ee0-110">當使用 Visual Studio 中的 [套件管理] 主控台，目前的這個主題所述的引數與命令套用。</span><span class="sxs-lookup"><span data-stu-id="77ee0-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="77ee0-111">常用命令</span><span class="sxs-lookup"><span data-stu-id="77ee0-111">Common Commands</span></span> | <span data-ttu-id="77ee0-112">描述</span><span class="sxs-lookup"><span data-stu-id="77ee0-112">Description</span></span> | <span data-ttu-id="77ee0-113">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="77ee0-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="77ee0-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="77ee0-114">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="77ee0-115">會封裝及其相依性安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="77ee0-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="77ee0-116">All</span><span class="sxs-lookup"><span data-stu-id="77ee0-116">All</span></span> |
| [<span data-ttu-id="77ee0-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="77ee0-117">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="77ee0-118">更新套件和其相依性或在專案中的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="77ee0-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="77ee0-119">All</span><span class="sxs-lookup"><span data-stu-id="77ee0-119">All</span></span> |
| [<span data-ttu-id="77ee0-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="77ee0-120">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="77ee0-121">搜尋套件來源使用的封裝識別碼或關鍵字。</span><span class="sxs-lookup"><span data-stu-id="77ee0-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="77ee0-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="77ee0-122">3.0+</span></span> |
| [<span data-ttu-id="77ee0-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="77ee0-123">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="77ee0-124">擷取安裝在本機的存放庫中的套件清單，或列出可用的封裝，從套件來源。</span><span class="sxs-lookup"><span data-stu-id="77ee0-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="77ee0-125">All</span><span class="sxs-lookup"><span data-stu-id="77ee0-125">All</span></span> |

| <span data-ttu-id="77ee0-126">第二個命令</span><span class="sxs-lookup"><span data-stu-id="77ee0-126">Secondary Commands</span></span> | <span data-ttu-id="77ee0-127">描述</span><span class="sxs-lookup"><span data-stu-id="77ee0-127">Description</span></span> | <span data-ttu-id="77ee0-128">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="77ee0-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="77ee0-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="77ee0-129">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="77ee0-130">會檢查專案的輸出路徑中的所有組件，並新增至繫結重新導向`app.config`或`web.config`在必要時。</span><span class="sxs-lookup"><span data-stu-id="77ee0-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="77ee0-131">All</span><span class="sxs-lookup"><span data-stu-id="77ee0-131">All</span></span> |
| [<span data-ttu-id="77ee0-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="77ee0-132">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="77ee0-133">顯示預設值或指定的專案相關資訊。</span><span class="sxs-lookup"><span data-stu-id="77ee0-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="77ee0-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="77ee0-134">3.0+</span></span> |
| [<span data-ttu-id="77ee0-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="77ee0-135">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="77ee0-136">會啟動預設瀏覽器中使用的專案、 授權或指定封裝的檢舉不當使用 URL。</span><span class="sxs-lookup"><span data-stu-id="77ee0-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="77ee0-137">3\.0 + 中已被取代</span><span class="sxs-lookup"><span data-stu-id="77ee0-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="77ee0-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="77ee0-138">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="77ee0-139">註冊命令，讓您能夠建立常用的參數值的自訂擴充功能的參數索引標籤展開。</span><span class="sxs-lookup"><span data-stu-id="77ee0-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="77ee0-140">All</span><span class="sxs-lookup"><span data-stu-id="77ee0-140">All</span></span> |
| [<span data-ttu-id="77ee0-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="77ee0-141">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="77ee0-142">取得的版本已安裝的套件從指定專案，並同步處理到其他方案中專案的版本。</span><span class="sxs-lookup"><span data-stu-id="77ee0-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="77ee0-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="77ee0-143">3.0+</span></span> |
| [<span data-ttu-id="77ee0-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="77ee0-144">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="77ee0-145">從專案中，選擇性地移除其相依性移除封裝。</span><span class="sxs-lookup"><span data-stu-id="77ee0-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="77ee0-146">All</span><span class="sxs-lookup"><span data-stu-id="77ee0-146">All</span></span> |

<span data-ttu-id="77ee0-147">如需這些命令的主控台內的任何完整而詳細說明，只要有問題的命令名稱與執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="77ee0-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="77ee0-148">所有的套件管理員主控台命令支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="77ee0-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="77ee0-149">偵錯</span><span class="sxs-lookup"><span data-stu-id="77ee0-149">Debug</span></span>
- <span data-ttu-id="77ee0-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="77ee0-150">ErrorAction</span></span>
- <span data-ttu-id="77ee0-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="77ee0-151">ErrorVariable</span></span>
- <span data-ttu-id="77ee0-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="77ee0-152">OutBuffer</span></span>
- <span data-ttu-id="77ee0-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="77ee0-153">OutVariable</span></span>
- <span data-ttu-id="77ee0-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="77ee0-154">PipelineVariable</span></span>
- <span data-ttu-id="77ee0-155">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="77ee0-155">Verbose</span></span>
- <span data-ttu-id="77ee0-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="77ee0-156">WarningAction</span></span>
- <span data-ttu-id="77ee0-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="77ee0-157">WarningVariable</span></span>

<span data-ttu-id="77ee0-158">如需詳細資訊，請參閱[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 文件中。</span><span class="sxs-lookup"><span data-stu-id="77ee0-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
