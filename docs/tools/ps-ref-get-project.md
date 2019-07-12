---
title: NuGet 專案 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台的 GetProject PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842272"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="939a7-103">Get-Project (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="939a7-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="939a7-104">*只能在[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="939a7-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="939a7-105">顯示預設值或指定的專案相關資訊。</span><span class="sxs-lookup"><span data-stu-id="939a7-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="939a7-106">`Get-Project` 特別是回到專案的 Visual Studio DTE （開發工具環境） 物件的參照。</span><span class="sxs-lookup"><span data-stu-id="939a7-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="939a7-107">語法</span><span class="sxs-lookup"><span data-stu-id="939a7-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="939a7-108">參數</span><span class="sxs-lookup"><span data-stu-id="939a7-108">Parameters</span></span>

| <span data-ttu-id="939a7-109">參數</span><span class="sxs-lookup"><span data-stu-id="939a7-109">Parameter</span></span> | <span data-ttu-id="939a7-110">描述</span><span class="sxs-lookup"><span data-stu-id="939a7-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="939a7-111">名稱</span><span class="sxs-lookup"><span data-stu-id="939a7-111">Name</span></span> | <span data-ttu-id="939a7-112">指定專案，以顯示，請將預設為選取 套件管理員主控台中的預設專案。</span><span class="sxs-lookup"><span data-stu-id="939a7-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="939a7-113">-Name 參數是選擇性本身。</span><span class="sxs-lookup"><span data-stu-id="939a7-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="939a7-114">All</span><span class="sxs-lookup"><span data-stu-id="939a7-114">All</span></span> | <span data-ttu-id="939a7-115">會顯示解決方案中每個專案的資訊專案的順序不具決定性。</span><span class="sxs-lookup"><span data-stu-id="939a7-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="939a7-116">這些參數都不接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="939a7-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="939a7-117">一般參數</span><span class="sxs-lookup"><span data-stu-id="939a7-117">Common Parameters</span></span>

<span data-ttu-id="939a7-118">`Get-Project` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="939a7-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="939a7-119">範例</span><span class="sxs-lookup"><span data-stu-id="939a7-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```