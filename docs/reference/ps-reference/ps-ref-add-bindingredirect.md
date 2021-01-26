---
title: NuGet Add-BindingRedirect PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Add-BindingRedirect PowerShell 命令參考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777607"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="71556-103">Visual Studio) 中的 Add-BindingRedirect (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="71556-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="71556-104">*只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*</span><span class="sxs-lookup"><span data-stu-id="71556-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="71556-105">檢查項目輸出路徑內的所有元件，並在必要時將系結重新導向新增至應用程式或 web 設定檔。</span><span class="sxs-lookup"><span data-stu-id="71556-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="71556-106">此命令會在安裝套件時自動執行。</span><span class="sxs-lookup"><span data-stu-id="71556-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="71556-107">這僅適用于使用 packages.config 檔案的案例。</span><span class="sxs-lookup"><span data-stu-id="71556-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="71556-108">如需詳細資訊，請參閱 [NuGet packages.config 檔案參考](~/reference/packages-config.md)。</span><span class="sxs-lookup"><span data-stu-id="71556-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="71556-109">如需系結重新導向及其使用原因的詳細資訊，請參閱 .NET 檔中的重新導向 [元件版本](/dotnet/framework/configure-apps/redirect-assembly-versions) 。</span><span class="sxs-lookup"><span data-stu-id="71556-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="71556-110">語法</span><span class="sxs-lookup"><span data-stu-id="71556-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="71556-111">參數</span><span class="sxs-lookup"><span data-stu-id="71556-111">Parameters</span></span>

| <span data-ttu-id="71556-112">參數</span><span class="sxs-lookup"><span data-stu-id="71556-112">Parameter</span></span> | <span data-ttu-id="71556-113">描述</span><span class="sxs-lookup"><span data-stu-id="71556-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71556-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="71556-114">ProjectName</span></span> | <span data-ttu-id="71556-115"> (需要) 要加入系結重新導向的專案。</span><span class="sxs-lookup"><span data-stu-id="71556-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="71556-116">-專案參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="71556-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="71556-117">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="71556-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="71556-118">一般參數</span><span class="sxs-lookup"><span data-stu-id="71556-118">Common Parameters</span></span>

<span data-ttu-id="71556-119">`Add-BindingRedirect` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="71556-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="71556-120">範例</span><span class="sxs-lookup"><span data-stu-id="71556-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```