---
title: NuGet Add-BindingRedirect PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台中的 BindingRedirect PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623119"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="fe221-103">在 Visual Studio 中新增-BindingRedirect (封裝管理員主控台) </span><span class="sxs-lookup"><span data-stu-id="fe221-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fe221-104">*只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*</span><span class="sxs-lookup"><span data-stu-id="fe221-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fe221-105">檢查項目輸出路徑內的所有元件，並在必要時將系結重新導向新增至應用程式或 web 設定檔。</span><span class="sxs-lookup"><span data-stu-id="fe221-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="fe221-106">此命令會在安裝套件時自動執行。</span><span class="sxs-lookup"><span data-stu-id="fe221-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="fe221-107">這僅適用于使用 packages.config 檔案的案例。</span><span class="sxs-lookup"><span data-stu-id="fe221-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="fe221-108">如需詳細資訊，請參閱 [NuGet packages.config 檔案參考](~/reference/packages-config.md)。</span><span class="sxs-lookup"><span data-stu-id="fe221-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="fe221-109">如需系結重新導向及其使用原因的詳細資訊，請參閱 .NET 檔中的重新導向 [元件版本](/dotnet/framework/configure-apps/redirect-assembly-versions) 。</span><span class="sxs-lookup"><span data-stu-id="fe221-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="fe221-110">語法</span><span class="sxs-lookup"><span data-stu-id="fe221-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="fe221-111">參數</span><span class="sxs-lookup"><span data-stu-id="fe221-111">Parameters</span></span>

| <span data-ttu-id="fe221-112">參數</span><span class="sxs-lookup"><span data-stu-id="fe221-112">Parameter</span></span> | <span data-ttu-id="fe221-113">描述</span><span class="sxs-lookup"><span data-stu-id="fe221-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe221-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="fe221-114">ProjectName</span></span> | <span data-ttu-id="fe221-115"> (需要) 要加入系結重新導向的專案。</span><span class="sxs-lookup"><span data-stu-id="fe221-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="fe221-116">-專案參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="fe221-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="fe221-117">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="fe221-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fe221-118">一般參數</span><span class="sxs-lookup"><span data-stu-id="fe221-118">Common Parameters</span></span>

<span data-ttu-id="fe221-119">`Add-BindingRedirect` 支援下列 [常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="fe221-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fe221-120">範例</span><span class="sxs-lookup"><span data-stu-id="fe221-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
