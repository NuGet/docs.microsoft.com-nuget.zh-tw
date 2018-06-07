---
title: NuGet 的暫存器 TabExpansion PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台中的暫存器 TabExpansion PowerShell 命令的參考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818409"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="689d0-103">暫存器 TabExpansion （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="689d0-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="689d0-104">*只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="689d0-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="689d0-105">註冊 tab 鍵擴充參數指定的命令，使得索引標籤使用時輸入命令時，擴充的值會顯示為可用的選項有問題的參數。</span><span class="sxs-lookup"><span data-stu-id="689d0-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="689d0-106">會覆寫任何先前的展開命令。</span><span class="sxs-lookup"><span data-stu-id="689d0-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="689d0-107">語法</span><span class="sxs-lookup"><span data-stu-id="689d0-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="689d0-108">參數</span><span class="sxs-lookup"><span data-stu-id="689d0-108">Parameters</span></span>

| <span data-ttu-id="689d0-109">參數</span><span class="sxs-lookup"><span data-stu-id="689d0-109">Parameter</span></span> | <span data-ttu-id="689d0-110">描述</span><span class="sxs-lookup"><span data-stu-id="689d0-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="689d0-111">名稱</span><span class="sxs-lookup"><span data-stu-id="689d0-111">Name</span></span> | <span data-ttu-id="689d0-112">（必要）要用來註冊擴充的命令。</span><span class="sxs-lookup"><span data-stu-id="689d0-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="689d0-113">-Name 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="689d0-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="689d0-114">定義</span><span class="sxs-lookup"><span data-stu-id="689d0-114">Definition</span></span> | <span data-ttu-id="689d0-115">（必要）物件，描述語法中的引數`@{'<parameter>' = {'<value1>', '<value2>', ...}}`其中`<parameter>`是要修改的參數和每個名稱`<value>`提供特定的擴充。</span><span class="sxs-lookup"><span data-stu-id="689d0-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="689d0-116">接受單引號與雙引號引號。</span><span class="sxs-lookup"><span data-stu-id="689d0-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="689d0-117">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="689d0-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="689d0-118">一般參數</span><span class="sxs-lookup"><span data-stu-id="689d0-118">Common Parameters</span></span>

<span data-ttu-id="689d0-119">`Register-TabExpansion` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="689d0-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="689d0-120">範例</span><span class="sxs-lookup"><span data-stu-id="689d0-120">Examples</span></span>

<span data-ttu-id="689d0-121">請考慮包含三個專案名稱 EventManager、 公用程式及 SpecialParser 的方案。</span><span class="sxs-lookup"><span data-stu-id="689d0-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="689d0-122">開發人員經常使用`Update-Package`命令在不同的時間，與每個這些專案。</span><span class="sxs-lookup"><span data-stu-id="689d0-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="689d0-123">她發現方便`Update-Package`命令提供的自動完成擴充功能`-ProjectName`引數，因此她不需要每次出專案名稱輸入。</span><span class="sxs-lookup"><span data-stu-id="689d0-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="689d0-124">下列命令，然後註冊這些三個專案的名稱為擴充的`-ProjectName`參數：</span><span class="sxs-lookup"><span data-stu-id="689d0-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="689d0-125">開發人員可以再輸入`Update-Package -ProjectName `、 按 tab 鍵，並請參閱，以自動完成選項的展開：</span><span class="sxs-lookup"><span data-stu-id="689d0-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![使用暫存器 TabExpansion 的範例](media/Register-TabExpansion-Example.png)
