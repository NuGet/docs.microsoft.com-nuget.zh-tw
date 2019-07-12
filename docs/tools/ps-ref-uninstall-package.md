---
title: NuGet 解除安裝套件的 PowerShell 參考
description: 在 NuGet 套件管理員主控台中，在 Visual Studio 中的封裝解除安裝 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842479"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4dacd-103">Uninstall-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="4dacd-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4dacd-104">*本主題描述內的命令[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。一般的 PowerShell 封裝解除安裝命令中，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="4dacd-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4dacd-105">從專案中，選擇性地移除其相依性移除封裝。</span><span class="sxs-lookup"><span data-stu-id="4dacd-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="4dacd-106">如果其他套件相依於此套件，則命令會失敗，除非選項指定 – Force。</span><span class="sxs-lookup"><span data-stu-id="4dacd-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="4dacd-107">語法</span><span class="sxs-lookup"><span data-stu-id="4dacd-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="4dacd-108">如果其他套件相依於此套件，則命令會失敗，除非選項指定 – Force。</span><span class="sxs-lookup"><span data-stu-id="4dacd-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="4dacd-109">參數</span><span class="sxs-lookup"><span data-stu-id="4dacd-109">Parameters</span></span>

| <span data-ttu-id="4dacd-110">參數</span><span class="sxs-lookup"><span data-stu-id="4dacd-110">Parameter</span></span> | <span data-ttu-id="4dacd-111">描述</span><span class="sxs-lookup"><span data-stu-id="4dacd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4dacd-112">ID</span><span class="sxs-lookup"><span data-stu-id="4dacd-112">Id</span></span> | <span data-ttu-id="4dacd-113">（必要）若要解除安裝封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="4dacd-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="4dacd-114">-識別碼是選擇性參數本身。</span><span class="sxs-lookup"><span data-stu-id="4dacd-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4dacd-115">版本</span><span class="sxs-lookup"><span data-stu-id="4dacd-115">Version</span></span> | <span data-ttu-id="4dacd-116">若要解除安裝，封裝的版本預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="4dacd-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="4dacd-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="4dacd-117">RemoveDependencies</span></span> | <span data-ttu-id="4dacd-118">解除安裝封裝和其未使用的相依性。</span><span class="sxs-lookup"><span data-stu-id="4dacd-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="4dacd-119">也就是說，如果任何相依性有相依於它的另一個封裝，它會略過。</span><span class="sxs-lookup"><span data-stu-id="4dacd-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="4dacd-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4dacd-120">ProjectName</span></span> | <span data-ttu-id="4dacd-121">要從中解除安裝套件，將預設為預設專案的專案。</span><span class="sxs-lookup"><span data-stu-id="4dacd-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="4dacd-122">強制</span><span class="sxs-lookup"><span data-stu-id="4dacd-122">Force</span></span> | <span data-ttu-id="4dacd-123">強制解除安裝，封裝，即使其他封裝依存於此。</span><span class="sxs-lookup"><span data-stu-id="4dacd-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="4dacd-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="4dacd-124">WhatIf</span></span> | <span data-ttu-id="4dacd-125">顯示執行命令，而不實際執行解除安裝時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="4dacd-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="4dacd-126">這些參數都不接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="4dacd-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4dacd-127">一般參數</span><span class="sxs-lookup"><span data-stu-id="4dacd-127">Common Parameters</span></span>

<span data-ttu-id="4dacd-128">`Uninstall-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4dacd-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4dacd-129">範例</span><span class="sxs-lookup"><span data-stu-id="4dacd-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
