---
title: "NuGet Get 專案 PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 09c10ea3-ba26-4bfa-999e-de5350e6e920
description: "在 Visual Studio 中的 NuGet 封裝管理員主控台的 GetProject PowerShell 命令的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考，Get 專案"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40c986164c3f6bd6a02877e15827541aae77d8ad
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="2d660-104">取得專案 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="2d660-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2d660-105">*只能在[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="2d660-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2d660-106">顯示預設值或指定的專案相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2d660-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="2d660-107">`Get-Project`特別是傳回專案的 Visual Studio DTE （開發工具環境） 物件參考。</span><span class="sxs-lookup"><span data-stu-id="2d660-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="2d660-108">語法</span><span class="sxs-lookup"><span data-stu-id="2d660-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2d660-109">參數</span><span class="sxs-lookup"><span data-stu-id="2d660-109">Parameters</span></span>

| <span data-ttu-id="2d660-110">參數</span><span class="sxs-lookup"><span data-stu-id="2d660-110">Parameter</span></span> | <span data-ttu-id="2d660-111">說明</span><span class="sxs-lookup"><span data-stu-id="2d660-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d660-112">名稱</span><span class="sxs-lookup"><span data-stu-id="2d660-112">Name</span></span> | <span data-ttu-id="2d660-113">指定要顯示，請將預設為 Package Manager Console 中選取的預設專案。</span><span class="sxs-lookup"><span data-stu-id="2d660-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="2d660-114">-Name 參數是選擇性本身。</span><span class="sxs-lookup"><span data-stu-id="2d660-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="2d660-115">全部</span><span class="sxs-lookup"><span data-stu-id="2d660-115">All</span></span> | <span data-ttu-id="2d660-116">顯示方案; 中的每個專案的資訊專案的順序不具決定性。</span><span class="sxs-lookup"><span data-stu-id="2d660-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="2d660-117">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="2d660-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2d660-118">一般參數</span><span class="sxs-lookup"><span data-stu-id="2d660-118">Common Parameters</span></span>

<span data-ttu-id="2d660-119">`Get-Project`支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="2d660-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2d660-120">範例</span><span class="sxs-lookup"><span data-stu-id="2d660-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```