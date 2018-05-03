---
title: NuGet Get 專案 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台的 GetProject PowerShell 命令的參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="ea244-103">取得專案 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="ea244-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ea244-104">*只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="ea244-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ea244-105">顯示預設值或指定的專案相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ea244-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="ea244-106">`Get-Project` 特別是傳回專案的 Visual Studio DTE （開發工具環境） 物件參考。</span><span class="sxs-lookup"><span data-stu-id="ea244-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="ea244-107">語法</span><span class="sxs-lookup"><span data-stu-id="ea244-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ea244-108">參數</span><span class="sxs-lookup"><span data-stu-id="ea244-108">Parameters</span></span>

| <span data-ttu-id="ea244-109">參數</span><span class="sxs-lookup"><span data-stu-id="ea244-109">Parameter</span></span> | <span data-ttu-id="ea244-110">描述</span><span class="sxs-lookup"><span data-stu-id="ea244-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea244-111">名稱</span><span class="sxs-lookup"><span data-stu-id="ea244-111">Name</span></span> | <span data-ttu-id="ea244-112">指定要顯示，請將預設為 Package Manager Console 中選取的預設專案。</span><span class="sxs-lookup"><span data-stu-id="ea244-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="ea244-113">-Name 參數是選擇性本身。</span><span class="sxs-lookup"><span data-stu-id="ea244-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="ea244-114">全部</span><span class="sxs-lookup"><span data-stu-id="ea244-114">All</span></span> | <span data-ttu-id="ea244-115">顯示方案; 中的每個專案的資訊專案的順序不具決定性。</span><span class="sxs-lookup"><span data-stu-id="ea244-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="ea244-116">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="ea244-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ea244-117">一般參數</span><span class="sxs-lookup"><span data-stu-id="ea244-117">Common Parameters</span></span>

<span data-ttu-id="ea244-118">`Get-Project` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="ea244-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ea244-119">範例</span><span class="sxs-lookup"><span data-stu-id="ea244-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```