---
title: NuGet Open-PackagePage PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Open-PackagePage PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238058"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="40d39-103">Visual Studio) 中的 Open-PackagePage (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="40d39-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="40d39-104">*3.0 + 中已淘汰;只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*</span><span class="sxs-lookup"><span data-stu-id="40d39-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="40d39-105">使用指定封裝的專案、授權或報告濫用 URL 來啟動預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="40d39-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="40d39-106">語法</span><span class="sxs-lookup"><span data-stu-id="40d39-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="40d39-107">參數</span><span class="sxs-lookup"><span data-stu-id="40d39-107">Parameters</span></span>

| <span data-ttu-id="40d39-108">參數</span><span class="sxs-lookup"><span data-stu-id="40d39-108">Parameter</span></span> | <span data-ttu-id="40d39-109">Description</span><span class="sxs-lookup"><span data-stu-id="40d39-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="40d39-110">Id</span><span class="sxs-lookup"><span data-stu-id="40d39-110">Id</span></span> | <span data-ttu-id="40d39-111">所需封裝的封裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="40d39-111">The package ID of the desired package.</span></span> <span data-ttu-id="40d39-112">-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="40d39-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="40d39-113">版本</span><span class="sxs-lookup"><span data-stu-id="40d39-113">Version</span></span> | <span data-ttu-id="40d39-114">封裝的版本，預設為最新版本。</span><span class="sxs-lookup"><span data-stu-id="40d39-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="40d39-115">來源</span><span class="sxs-lookup"><span data-stu-id="40d39-115">Source</span></span> | <span data-ttu-id="40d39-116">封裝來源，預設為來源下拉式清單中選取的來源。</span><span class="sxs-lookup"><span data-stu-id="40d39-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="40d39-117">授權</span><span class="sxs-lookup"><span data-stu-id="40d39-117">License</span></span> | <span data-ttu-id="40d39-118">開啟瀏覽器並前往封裝的授權 URL。</span><span class="sxs-lookup"><span data-stu-id="40d39-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="40d39-119">如果未指定-License 或-ReportAbuse，瀏覽器會開啟套件的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="40d39-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="40d39-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="40d39-120">ReportAbuse</span></span> | <span data-ttu-id="40d39-121">開啟瀏覽器並前往封裝的檢舉不當使用 URL。</span><span class="sxs-lookup"><span data-stu-id="40d39-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="40d39-122">如果未指定-License 或-ReportAbuse，瀏覽器會開啟套件的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="40d39-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="40d39-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="40d39-123">PassThru</span></span> | <span data-ttu-id="40d39-124">顯示 URL;使用 with-WhatIf 來抑制開啟瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="40d39-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="40d39-125">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="40d39-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="40d39-126">一般參數</span><span class="sxs-lookup"><span data-stu-id="40d39-126">Common Parameters</span></span>

<span data-ttu-id="40d39-127">`Open-PackagePage` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="40d39-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="40d39-128">範例</span><span class="sxs-lookup"><span data-stu-id="40d39-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```