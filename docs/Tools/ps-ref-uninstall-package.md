---
title: "NuGet 解除安裝套件的 PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "在 Visual Studio 中的 NuGet 封裝管理員主控台中的封裝解除安裝的 PowerShell 命令的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考，解除安裝套件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0899198a354a56615a48a1f7f428674a205f386b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="72d5c-104">解除安裝套件 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="72d5c-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="72d5c-105">*本主題描述內的命令[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上的 Visual Studio 中。一般 PowerShell 解除安裝封裝的命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="72d5c-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="72d5c-106">移除封裝在專案中，選擇性地移除其相依性。</span><span class="sxs-lookup"><span data-stu-id="72d5c-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="72d5c-107">如果有其他套件相依於這個套件，此命令會失敗，除非 – 指定的 Force 選項。</span><span class="sxs-lookup"><span data-stu-id="72d5c-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="72d5c-108">語法</span><span class="sxs-lookup"><span data-stu-id="72d5c-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="72d5c-109">如果有其他套件相依於這個套件，此命令會失敗，除非 – 指定的 Force 選項。</span><span class="sxs-lookup"><span data-stu-id="72d5c-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="72d5c-110">參數</span><span class="sxs-lookup"><span data-stu-id="72d5c-110">Parameters</span></span>

| <span data-ttu-id="72d5c-111">參數</span><span class="sxs-lookup"><span data-stu-id="72d5c-111">Parameter</span></span> | <span data-ttu-id="72d5c-112">描述</span><span class="sxs-lookup"><span data-stu-id="72d5c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="72d5c-113">ID</span><span class="sxs-lookup"><span data-stu-id="72d5c-113">Id</span></span> | <span data-ttu-id="72d5c-114">（必要）若要解除安裝封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="72d5c-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="72d5c-115">-Id 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="72d5c-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="72d5c-116">版本</span><span class="sxs-lookup"><span data-stu-id="72d5c-116">Version</span></span> | <span data-ttu-id="72d5c-117">若要解除安裝，封裝版本預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="72d5c-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="72d5c-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="72d5c-118">RemoveDependencies</span></span> | <span data-ttu-id="72d5c-119">解除安裝套件及其未使用相依性。</span><span class="sxs-lookup"><span data-stu-id="72d5c-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="72d5c-120">也就是說，如果任何相依性具有相依於它的另一個封裝，它會略過。</span><span class="sxs-lookup"><span data-stu-id="72d5c-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="72d5c-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="72d5c-121">ProjectName</span></span> | <span data-ttu-id="72d5c-122">要從中解除安裝封裝，將預設為預設專案的專案。</span><span class="sxs-lookup"><span data-stu-id="72d5c-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="72d5c-123">強制</span><span class="sxs-lookup"><span data-stu-id="72d5c-123">Force</span></span> | <span data-ttu-id="72d5c-124">強制解除安裝，封裝，即使有其他套件相依於它。</span><span class="sxs-lookup"><span data-stu-id="72d5c-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="72d5c-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="72d5c-125">WhatIf</span></span> | <span data-ttu-id="72d5c-126">顯示執行命令，而不需實際執行解除安裝時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="72d5c-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="72d5c-127">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="72d5c-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="72d5c-128">一般參數</span><span class="sxs-lookup"><span data-stu-id="72d5c-128">Common Parameters</span></span>

<span data-ttu-id="72d5c-129">`Uninstall-Package`支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="72d5c-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="72d5c-130">範例</span><span class="sxs-lookup"><span data-stu-id="72d5c-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
