---
title: NuGet Open-PackagePage PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 PackagePage PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384424"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="ea72b-103">PackagePage （Visual Studio 中的套件管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="ea72b-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ea72b-104">*已在 3.0 + 中淘汰;僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*</span><span class="sxs-lookup"><span data-stu-id="ea72b-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ea72b-105">使用指定封裝的 [專案]、[授權] 或 [報表濫用 URL] 來啟動預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ea72b-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="ea72b-106">語法</span><span class="sxs-lookup"><span data-stu-id="ea72b-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ea72b-107">參數</span><span class="sxs-lookup"><span data-stu-id="ea72b-107">Parameters</span></span>

| <span data-ttu-id="ea72b-108">參數</span><span class="sxs-lookup"><span data-stu-id="ea72b-108">Parameter</span></span> | <span data-ttu-id="ea72b-109">描述</span><span class="sxs-lookup"><span data-stu-id="ea72b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea72b-110">ID</span><span class="sxs-lookup"><span data-stu-id="ea72b-110">Id</span></span> | <span data-ttu-id="ea72b-111">所需套件的封裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="ea72b-111">The package ID of the desired package.</span></span> <span data-ttu-id="ea72b-112">-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="ea72b-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ea72b-113">{2&gt;版本&lt;2}</span><span class="sxs-lookup"><span data-stu-id="ea72b-113">Version</span></span> | <span data-ttu-id="ea72b-114">封裝的版本，預設為最新版本。</span><span class="sxs-lookup"><span data-stu-id="ea72b-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="ea72b-115">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="ea72b-115">Source</span></span> | <span data-ttu-id="ea72b-116">封裝來源，預設為 [來源] 下拉式選單中選取的來源。</span><span class="sxs-lookup"><span data-stu-id="ea72b-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="ea72b-117">使用權</span><span class="sxs-lookup"><span data-stu-id="ea72b-117">License</span></span> | <span data-ttu-id="ea72b-118">將瀏覽器開啟至套件的授權 URL。</span><span class="sxs-lookup"><span data-stu-id="ea72b-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="ea72b-119">如果未指定-License 或-ReportAbuse，瀏覽器會開啟封裝的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="ea72b-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="ea72b-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="ea72b-120">ReportAbuse</span></span> | <span data-ttu-id="ea72b-121">將瀏覽器開啟至套件的報告濫用 URL。</span><span class="sxs-lookup"><span data-stu-id="ea72b-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="ea72b-122">如果未指定-License 或-ReportAbuse，瀏覽器會開啟封裝的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="ea72b-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="ea72b-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="ea72b-123">PassThru</span></span> | <span data-ttu-id="ea72b-124">顯示 URL;使用 with-WhatIf 來隱藏開啟瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ea72b-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="ea72b-125">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="ea72b-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ea72b-126">一般參數</span><span class="sxs-lookup"><span data-stu-id="ea72b-126">Common Parameters</span></span>

<span data-ttu-id="ea72b-127">`Open-PackagePage` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="ea72b-127">`Open-PackagePage` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ea72b-128">範例</span><span class="sxs-lookup"><span data-stu-id="ea72b-128">Examples</span></span>

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