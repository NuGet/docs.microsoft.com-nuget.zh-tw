---
title: NuGet 卸載-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [卸載-封裝 PowerShell] 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327275"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="0c910-103">Uninstall-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="0c910-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0c910-104">*本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 卸載-封裝命令, 請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="0c910-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="0c910-105">移除專案中的封裝, 並選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="0c910-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="0c910-106">如果其他封裝相依于此封裝, 除非指定– Force 選項, 否則此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="0c910-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="0c910-107">語法</span><span class="sxs-lookup"><span data-stu-id="0c910-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="0c910-108">如果其他封裝相依于此封裝, 除非指定– Force 選項, 否則此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="0c910-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="0c910-109">參數</span><span class="sxs-lookup"><span data-stu-id="0c910-109">Parameters</span></span>

| <span data-ttu-id="0c910-110">參數</span><span class="sxs-lookup"><span data-stu-id="0c910-110">Parameter</span></span> | <span data-ttu-id="0c910-111">說明</span><span class="sxs-lookup"><span data-stu-id="0c910-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0c910-112">ID</span><span class="sxs-lookup"><span data-stu-id="0c910-112">Id</span></span> | <span data-ttu-id="0c910-113">具備要卸載之封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0c910-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="0c910-114">-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="0c910-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="0c910-115">版本</span><span class="sxs-lookup"><span data-stu-id="0c910-115">Version</span></span> | <span data-ttu-id="0c910-116">要卸載的封裝版本, 預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="0c910-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="0c910-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="0c910-117">RemoveDependencies</span></span> | <span data-ttu-id="0c910-118">卸載套件及其未使用的相依性。</span><span class="sxs-lookup"><span data-stu-id="0c910-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="0c910-119">也就是說, 如果任何相依性有另一個依存于它的封裝, 則會略過。</span><span class="sxs-lookup"><span data-stu-id="0c910-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="0c910-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="0c910-120">ProjectName</span></span> | <span data-ttu-id="0c910-121">要從其中卸載封裝的專案, 預設為預設專案。</span><span class="sxs-lookup"><span data-stu-id="0c910-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="0c910-122">使</span><span class="sxs-lookup"><span data-stu-id="0c910-122">Force</span></span> | <span data-ttu-id="0c910-123">強制卸載套件, 即使其他套件相依于封裝也一樣。</span><span class="sxs-lookup"><span data-stu-id="0c910-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="0c910-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="0c910-124">WhatIf</span></span> | <span data-ttu-id="0c910-125">顯示在執行命令時, 不實際執行卸載所發生的情況。</span><span class="sxs-lookup"><span data-stu-id="0c910-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="0c910-126">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="0c910-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0c910-127">一般參數</span><span class="sxs-lookup"><span data-stu-id="0c910-127">Common Parameters</span></span>

<span data-ttu-id="0c910-128">`Uninstall-Package`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="0c910-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0c910-129">範例</span><span class="sxs-lookup"><span data-stu-id="0c910-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
