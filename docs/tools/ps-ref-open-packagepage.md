---
title: NuGet 開放 PackagePage PowerShell 參考
description: 在 NuGet 套件管理員主控台中，在 Visual Studio 中開啟 PackagePage PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842271"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="12392-103">Open-PackagePage (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="12392-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="12392-104">*在 3.0 + 中; 已被取代只能在[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="12392-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="12392-105">會啟動預設瀏覽器中使用的專案、 授權或指定封裝的檢舉不當使用 URL。</span><span class="sxs-lookup"><span data-stu-id="12392-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="12392-106">語法</span><span class="sxs-lookup"><span data-stu-id="12392-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="12392-107">參數</span><span class="sxs-lookup"><span data-stu-id="12392-107">Parameters</span></span>

| <span data-ttu-id="12392-108">參數</span><span class="sxs-lookup"><span data-stu-id="12392-108">Parameter</span></span> | <span data-ttu-id="12392-109">說明</span><span class="sxs-lookup"><span data-stu-id="12392-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12392-110">ID</span><span class="sxs-lookup"><span data-stu-id="12392-110">Id</span></span> | <span data-ttu-id="12392-111">所需套件的套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="12392-111">The package ID of the desired package.</span></span> <span data-ttu-id="12392-112">-識別碼是選擇性參數本身。</span><span class="sxs-lookup"><span data-stu-id="12392-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="12392-113">版本</span><span class="sxs-lookup"><span data-stu-id="12392-113">Version</span></span> | <span data-ttu-id="12392-114">將預設為最新版本的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="12392-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="12392-115">Source</span><span class="sxs-lookup"><span data-stu-id="12392-115">Source</span></span> | <span data-ttu-id="12392-116">封裝來源，將預設為來源下拉式清單中選取的來源。</span><span class="sxs-lookup"><span data-stu-id="12392-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="12392-117">使用權</span><span class="sxs-lookup"><span data-stu-id="12392-117">License</span></span> | <span data-ttu-id="12392-118">瀏覽器開啟至套件的授權 URL。</span><span class="sxs-lookup"><span data-stu-id="12392-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="12392-119">如果-授權和-ReportAbuse 都未指定，則瀏覽器會開啟套件的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="12392-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="12392-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="12392-120">ReportAbuse</span></span> | <span data-ttu-id="12392-121">瀏覽器開啟至套件的檢舉不當使用 URL。</span><span class="sxs-lookup"><span data-stu-id="12392-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="12392-122">如果-授權和-ReportAbuse 都未指定，則瀏覽器會開啟套件的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="12392-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="12392-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="12392-123">PassThru</span></span> | <span data-ttu-id="12392-124">顯示的 URL;若要隱藏開啟瀏覽器使用-WhatIf。</span><span class="sxs-lookup"><span data-stu-id="12392-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="12392-125">這些參數都不接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="12392-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="12392-126">一般參數</span><span class="sxs-lookup"><span data-stu-id="12392-126">Common Parameters</span></span>

<span data-ttu-id="12392-127">`Open-PackagePage` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="12392-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="12392-128">範例</span><span class="sxs-lookup"><span data-stu-id="12392-128">Examples</span></span>

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