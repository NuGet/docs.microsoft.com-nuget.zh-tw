---
title: NuGet 解除安裝套件的 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台中的封裝解除安裝的 PowerShell 命令的參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d4a24-103">解除安裝套件 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="d4a24-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d4a24-104">*本主題描述內的命令[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。一般 PowerShell 解除安裝封裝的命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="d4a24-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d4a24-105">移除封裝在專案中，選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="d4a24-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="d4a24-106">如果有其他套件相依於這個套件，此命令會失敗，除非 – 指定的 Force 選項。</span><span class="sxs-lookup"><span data-stu-id="d4a24-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="d4a24-107">語法</span><span class="sxs-lookup"><span data-stu-id="d4a24-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d4a24-108">如果有其他套件相依於這個套件，此命令會失敗，除非 – 指定的 Force 選項。</span><span class="sxs-lookup"><span data-stu-id="d4a24-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="d4a24-109">參數</span><span class="sxs-lookup"><span data-stu-id="d4a24-109">Parameters</span></span>

| <span data-ttu-id="d4a24-110">參數</span><span class="sxs-lookup"><span data-stu-id="d4a24-110">Parameter</span></span> | <span data-ttu-id="d4a24-111">描述</span><span class="sxs-lookup"><span data-stu-id="d4a24-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4a24-112">ID</span><span class="sxs-lookup"><span data-stu-id="d4a24-112">Id</span></span> | <span data-ttu-id="d4a24-113">（必要）若要解除安裝封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d4a24-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="d4a24-114">-Id 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="d4a24-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d4a24-115">版本</span><span class="sxs-lookup"><span data-stu-id="d4a24-115">Version</span></span> | <span data-ttu-id="d4a24-116">若要解除安裝，封裝版本預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="d4a24-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="d4a24-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="d4a24-117">RemoveDependencies</span></span> | <span data-ttu-id="d4a24-118">解除安裝套件及其未使用相依性。</span><span class="sxs-lookup"><span data-stu-id="d4a24-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="d4a24-119">也就是說，如果任何相依性具有相依於它的另一個封裝，它會略過。</span><span class="sxs-lookup"><span data-stu-id="d4a24-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="d4a24-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d4a24-120">ProjectName</span></span> | <span data-ttu-id="d4a24-121">要從中解除安裝封裝，將預設為預設專案的專案。</span><span class="sxs-lookup"><span data-stu-id="d4a24-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="d4a24-122">強制</span><span class="sxs-lookup"><span data-stu-id="d4a24-122">Force</span></span> | <span data-ttu-id="d4a24-123">強制解除安裝，封裝，即使有其他套件相依於它。</span><span class="sxs-lookup"><span data-stu-id="d4a24-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="d4a24-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d4a24-124">WhatIf</span></span> | <span data-ttu-id="d4a24-125">顯示執行命令，而不需實際執行解除安裝時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="d4a24-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="d4a24-126">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="d4a24-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d4a24-127">一般參數</span><span class="sxs-lookup"><span data-stu-id="d4a24-127">Common Parameters</span></span>

<span data-ttu-id="d4a24-128">`Uninstall-Package` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="d4a24-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d4a24-129">範例</span><span class="sxs-lookup"><span data-stu-id="d4a24-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
