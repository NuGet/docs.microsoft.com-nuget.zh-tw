---
title: NuGet 卸載-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [卸載-封裝 PowerShell] 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384411"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7035c-103">卸載-封裝（Visual Studio 中的套件管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="7035c-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7035c-104">*本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 卸載-封裝命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="7035c-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7035c-105">移除專案中的封裝，並選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="7035c-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="7035c-106">若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="7035c-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="7035c-107">語法</span><span class="sxs-lookup"><span data-stu-id="7035c-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="7035c-108">若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="7035c-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="7035c-109">參數</span><span class="sxs-lookup"><span data-stu-id="7035c-109">Parameters</span></span>

| <span data-ttu-id="7035c-110">參數</span><span class="sxs-lookup"><span data-stu-id="7035c-110">Parameter</span></span> | <span data-ttu-id="7035c-111">描述</span><span class="sxs-lookup"><span data-stu-id="7035c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7035c-112">ID</span><span class="sxs-lookup"><span data-stu-id="7035c-112">Id</span></span> | <span data-ttu-id="7035c-113">具備要卸載之封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7035c-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="7035c-114">-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="7035c-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7035c-115">{2&gt;版本&lt;2}</span><span class="sxs-lookup"><span data-stu-id="7035c-115">Version</span></span> | <span data-ttu-id="7035c-116">要卸載的封裝版本，預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="7035c-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="7035c-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="7035c-117">RemoveDependencies</span></span> | <span data-ttu-id="7035c-118">卸載套件及其未使用的相依性。</span><span class="sxs-lookup"><span data-stu-id="7035c-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="7035c-119">也就是說，如果任何相依性有另一個依存于它的封裝，則會略過。</span><span class="sxs-lookup"><span data-stu-id="7035c-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="7035c-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7035c-120">ProjectName</span></span> | <span data-ttu-id="7035c-121">要從其中卸載封裝的專案，預設為預設專案。</span><span class="sxs-lookup"><span data-stu-id="7035c-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="7035c-122">Force</span><span class="sxs-lookup"><span data-stu-id="7035c-122">Force</span></span> | <span data-ttu-id="7035c-123">強制卸載套件，即使其他套件相依于封裝也一樣。</span><span class="sxs-lookup"><span data-stu-id="7035c-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="7035c-124">Whatif</span><span class="sxs-lookup"><span data-stu-id="7035c-124">WhatIf</span></span> | <span data-ttu-id="7035c-125">顯示在執行命令時，不實際執行卸載所發生的情況。</span><span class="sxs-lookup"><span data-stu-id="7035c-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="7035c-126">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="7035c-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7035c-127">一般參數</span><span class="sxs-lookup"><span data-stu-id="7035c-127">Common Parameters</span></span>

<span data-ttu-id="7035c-128">`Uninstall-Package` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="7035c-128">`Uninstall-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7035c-129">範例</span><span class="sxs-lookup"><span data-stu-id="7035c-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
