---
title: NuGet Get-Project PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台中的 GetProject PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238071"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="575d9-103">Visual Studio) 中的 Get-Project (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="575d9-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="575d9-104">*只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*</span><span class="sxs-lookup"><span data-stu-id="575d9-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="575d9-105">顯示預設或指定專案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="575d9-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="575d9-106">`Get-Project` 特別針對專案的 Visual Studio DTE (開發工具環境) 物件，傳回對的引用。</span><span class="sxs-lookup"><span data-stu-id="575d9-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="575d9-107">語法</span><span class="sxs-lookup"><span data-stu-id="575d9-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="575d9-108">參數</span><span class="sxs-lookup"><span data-stu-id="575d9-108">Parameters</span></span>

| <span data-ttu-id="575d9-109">參數</span><span class="sxs-lookup"><span data-stu-id="575d9-109">Parameter</span></span> | <span data-ttu-id="575d9-110">描述</span><span class="sxs-lookup"><span data-stu-id="575d9-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="575d9-111">Name</span><span class="sxs-lookup"><span data-stu-id="575d9-111">Name</span></span> | <span data-ttu-id="575d9-112">指定要顯示的專案，預設為在封裝管理員主控台中選取的預設專案。</span><span class="sxs-lookup"><span data-stu-id="575d9-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="575d9-113">-Name 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="575d9-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="575d9-114">全部</span><span class="sxs-lookup"><span data-stu-id="575d9-114">All</span></span> | <span data-ttu-id="575d9-115">顯示方案中每個專案的資訊;專案的順序不具決定性。</span><span class="sxs-lookup"><span data-stu-id="575d9-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="575d9-116">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="575d9-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="575d9-117">一般參數</span><span class="sxs-lookup"><span data-stu-id="575d9-117">Common Parameters</span></span>

<span data-ttu-id="575d9-118">`Get-Project` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="575d9-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="575d9-119">範例</span><span class="sxs-lookup"><span data-stu-id="575d9-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```