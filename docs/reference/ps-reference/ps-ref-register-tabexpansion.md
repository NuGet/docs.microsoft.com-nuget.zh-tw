---
title: NuGet 註冊-TabExpansion PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 TabExpansion PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384450"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="feb9f-103">TabExpansion （Visual Studio 中的套件管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="feb9f-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="feb9f-104">*僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*</span><span class="sxs-lookup"><span data-stu-id="feb9f-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="feb9f-105">為指定命令的參數註冊 tab 鍵擴充，讓您在輸入命令時使用 Tab 鍵時，展開的值會顯示為有問題之參數的可用選項。</span><span class="sxs-lookup"><span data-stu-id="feb9f-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="feb9f-106">系統會覆寫命令的任何先前的擴充。</span><span class="sxs-lookup"><span data-stu-id="feb9f-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="feb9f-107">語法</span><span class="sxs-lookup"><span data-stu-id="feb9f-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="feb9f-108">參數</span><span class="sxs-lookup"><span data-stu-id="feb9f-108">Parameters</span></span>

| <span data-ttu-id="feb9f-109">參數</span><span class="sxs-lookup"><span data-stu-id="feb9f-109">Parameter</span></span> | <span data-ttu-id="feb9f-110">描述</span><span class="sxs-lookup"><span data-stu-id="feb9f-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="feb9f-111">Name</span><span class="sxs-lookup"><span data-stu-id="feb9f-111">Name</span></span> | <span data-ttu-id="feb9f-112">具備要對其註冊擴充的命令。</span><span class="sxs-lookup"><span data-stu-id="feb9f-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="feb9f-113">-Name 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="feb9f-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="feb9f-114">定義</span><span class="sxs-lookup"><span data-stu-id="feb9f-114">Definition</span></span> | <span data-ttu-id="feb9f-115">具備物件，描述語法中的引數 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 其中 `<parameter>` 是要修改的參數名稱，而每個 `<value>` 提供特定的擴充。</span><span class="sxs-lookup"><span data-stu-id="feb9f-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="feb9f-116">只接受單引號和雙引號。</span><span class="sxs-lookup"><span data-stu-id="feb9f-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="feb9f-117">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="feb9f-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="feb9f-118">一般參數</span><span class="sxs-lookup"><span data-stu-id="feb9f-118">Common Parameters</span></span>

<span data-ttu-id="feb9f-119">`Register-TabExpansion` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="feb9f-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="feb9f-120">範例</span><span class="sxs-lookup"><span data-stu-id="feb9f-120">Examples</span></span>

<span data-ttu-id="feb9f-121">假設有一個包含三個專案的方案： EventManager、公用程式和 SpecialParser。</span><span class="sxs-lookup"><span data-stu-id="feb9f-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="feb9f-122">開發人員經常會在每個專案的不同時間使用 `Update-Package` 命令。</span><span class="sxs-lookup"><span data-stu-id="feb9f-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="feb9f-123">她發現，讓 `Update-Package` 命令為 `-ProjectName` 引數提供自動完成擴充，讓她不需要每次都輸入專案名稱。</span><span class="sxs-lookup"><span data-stu-id="feb9f-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="feb9f-124">然後，下列命令會將這三個專案名稱註冊為 `-ProjectName` 參數的擴充：</span><span class="sxs-lookup"><span data-stu-id="feb9f-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="feb9f-125">開發人員接著可以輸入 `Update-Package -ProjectName `，按 Tab 鍵，並查看作為自動完成選項提供的擴充功能：</span><span class="sxs-lookup"><span data-stu-id="feb9f-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![使用 Register-TabExpansion 的範例](media/Register-TabExpansion-Example.png)
