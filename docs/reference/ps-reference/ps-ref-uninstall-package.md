---
title: NuGet Uninstall-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Uninstall-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237123"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="db6c3-103">Visual Studio) 中的 Uninstall-Package (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="db6c3-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="db6c3-104">*本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Uninstall-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="db6c3-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="db6c3-105">移除專案中的封裝，並選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="db6c3-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="db6c3-106">若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="db6c3-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="db6c3-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="db6c3-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="db6c3-108">若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="db6c3-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="db6c3-109">參數</span><span class="sxs-lookup"><span data-stu-id="db6c3-109">Parameters</span></span>

| <span data-ttu-id="db6c3-110">參數</span><span class="sxs-lookup"><span data-stu-id="db6c3-110">Parameter</span></span> | <span data-ttu-id="db6c3-111">Description</span><span class="sxs-lookup"><span data-stu-id="db6c3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="db6c3-112">Id</span><span class="sxs-lookup"><span data-stu-id="db6c3-112">Id</span></span> | <span data-ttu-id="db6c3-113"> (需要) 要卸載之套件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="db6c3-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="db6c3-114">-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="db6c3-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="db6c3-115">版本</span><span class="sxs-lookup"><span data-stu-id="db6c3-115">Version</span></span> | <span data-ttu-id="db6c3-116">要卸載的套件版本，預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="db6c3-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="db6c3-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="db6c3-117">RemoveDependencies</span></span> | <span data-ttu-id="db6c3-118">卸載封裝及其未使用的相依性。</span><span class="sxs-lookup"><span data-stu-id="db6c3-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="db6c3-119">也就是說，如果任何相依性有另一個相依的封裝，則會略過它。</span><span class="sxs-lookup"><span data-stu-id="db6c3-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="db6c3-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="db6c3-120">ProjectName</span></span> | <span data-ttu-id="db6c3-121">要從其中卸載封裝的專案，預設為預設專案。</span><span class="sxs-lookup"><span data-stu-id="db6c3-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="db6c3-122">Force</span><span class="sxs-lookup"><span data-stu-id="db6c3-122">Force</span></span> | <span data-ttu-id="db6c3-123">強制卸載套件，即使其他封裝相依于封裝也是如此。</span><span class="sxs-lookup"><span data-stu-id="db6c3-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="db6c3-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="db6c3-124">WhatIf</span></span> | <span data-ttu-id="db6c3-125">顯示執行命令時會發生什麼事，而不實際執行卸載。</span><span class="sxs-lookup"><span data-stu-id="db6c3-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="db6c3-126">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="db6c3-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="db6c3-127">一般參數</span><span class="sxs-lookup"><span data-stu-id="db6c3-127">Common Parameters</span></span>

<span data-ttu-id="db6c3-128">`Uninstall-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="db6c3-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="db6c3-129">範例</span><span class="sxs-lookup"><span data-stu-id="db6c3-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```