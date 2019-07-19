---
title: NuGet BindingRedirect PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 BindingRedirect PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327455"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="3cb47-103">Add-BindingRedirect (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="3cb47-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3cb47-104">*僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*</span><span class="sxs-lookup"><span data-stu-id="3cb47-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3cb47-105">檢查項目輸出路徑中的所有元件, 並在必要時將系結重新導向新增至應用程式或 web 設定檔。</span><span class="sxs-lookup"><span data-stu-id="3cb47-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="3cb47-106">安裝套件時, 會自動執行此命令。</span><span class="sxs-lookup"><span data-stu-id="3cb47-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="3cb47-107">如需系結重新導向和其使用原因的詳細資訊, 請參閱 .NET 檔中的重新導向[元件版本](/dotnet/framework/configure-apps/redirect-assembly-versions)。</span><span class="sxs-lookup"><span data-stu-id="3cb47-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="3cb47-108">語法</span><span class="sxs-lookup"><span data-stu-id="3cb47-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3cb47-109">參數</span><span class="sxs-lookup"><span data-stu-id="3cb47-109">Parameters</span></span>

| <span data-ttu-id="3cb47-110">參數</span><span class="sxs-lookup"><span data-stu-id="3cb47-110">Parameter</span></span> | <span data-ttu-id="3cb47-111">描述</span><span class="sxs-lookup"><span data-stu-id="3cb47-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3cb47-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="3cb47-112">ProjectName</span></span> | <span data-ttu-id="3cb47-113">具備要加入系結重新導向的專案。</span><span class="sxs-lookup"><span data-stu-id="3cb47-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="3cb47-114">-專案名稱參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="3cb47-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="3cb47-115">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="3cb47-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3cb47-116">一般參數</span><span class="sxs-lookup"><span data-stu-id="3cb47-116">Common Parameters</span></span>

<span data-ttu-id="3cb47-117">`Add-BindingRedirect`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="3cb47-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3cb47-118">範例</span><span class="sxs-lookup"><span data-stu-id="3cb47-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```