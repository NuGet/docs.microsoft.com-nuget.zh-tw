---
title: NuGet Get-Project PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台中的 GetProject PowerShell 命令參考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777469"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="b527d-103">Visual Studio) 中的 Get-Project (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="b527d-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b527d-104">*只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*</span><span class="sxs-lookup"><span data-stu-id="b527d-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b527d-105">顯示預設或指定專案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b527d-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="b527d-106">`Get-Project` 特別針對專案的 Visual Studio DTE (開發工具環境) 物件，傳回對的引用。</span><span class="sxs-lookup"><span data-stu-id="b527d-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="b527d-107">語法</span><span class="sxs-lookup"><span data-stu-id="b527d-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b527d-108">參數</span><span class="sxs-lookup"><span data-stu-id="b527d-108">Parameters</span></span>

| <span data-ttu-id="b527d-109">參數</span><span class="sxs-lookup"><span data-stu-id="b527d-109">Parameter</span></span> | <span data-ttu-id="b527d-110">描述</span><span class="sxs-lookup"><span data-stu-id="b527d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b527d-111">名稱</span><span class="sxs-lookup"><span data-stu-id="b527d-111">Name</span></span> | <span data-ttu-id="b527d-112">指定要顯示的專案，預設為在封裝管理員主控台中選取的預設專案。</span><span class="sxs-lookup"><span data-stu-id="b527d-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="b527d-113">-Name 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="b527d-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="b527d-114">全部</span><span class="sxs-lookup"><span data-stu-id="b527d-114">All</span></span> | <span data-ttu-id="b527d-115">顯示方案中每個專案的資訊;專案的順序不具決定性。</span><span class="sxs-lookup"><span data-stu-id="b527d-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="b527d-116">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="b527d-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b527d-117">一般參數</span><span class="sxs-lookup"><span data-stu-id="b527d-117">Common Parameters</span></span>

<span data-ttu-id="b527d-118">`Get-Project` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="b527d-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b527d-119">範例</span><span class="sxs-lookup"><span data-stu-id="b527d-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```