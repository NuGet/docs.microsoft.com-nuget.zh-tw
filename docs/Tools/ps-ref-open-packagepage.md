---
title: "NuGet 開啟 PackagePage PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: e9f84530-6b3d-43b0-a832-0acb2997f6fc
description: "在 Visual Studio 中的 NuGet 封裝管理員主控台中開啟 PackagePage PowerShell 命令的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，開啟 PackagePage NuGet Powershell 參考"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ec4310ea9d13926b1cb3b227b17016742a70bc16
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="553dd-104">開啟 PackagePage （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="553dd-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="553dd-105">*3.0 +; 中已被取代只能在[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="553dd-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="553dd-106">啟動預設瀏覽器中使用專案、 授權或指定之封裝的報表濫用 URL。</span><span class="sxs-lookup"><span data-stu-id="553dd-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="553dd-107">語法</span><span class="sxs-lookup"><span data-stu-id="553dd-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="553dd-108">參數</span><span class="sxs-lookup"><span data-stu-id="553dd-108">Parameters</span></span>

| <span data-ttu-id="553dd-109">參數</span><span class="sxs-lookup"><span data-stu-id="553dd-109">Parameter</span></span> | <span data-ttu-id="553dd-110">說明</span><span class="sxs-lookup"><span data-stu-id="553dd-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="553dd-111">ID</span><span class="sxs-lookup"><span data-stu-id="553dd-111">Id</span></span> | <span data-ttu-id="553dd-112">所要封裝之封裝 ID。</span><span class="sxs-lookup"><span data-stu-id="553dd-112">The package ID of the desired package.</span></span> <span data-ttu-id="553dd-113">-Id 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="553dd-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="553dd-114">版本</span><span class="sxs-lookup"><span data-stu-id="553dd-114">Version</span></span> | <span data-ttu-id="553dd-115">預設為最新版本的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="553dd-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="553dd-116">來源</span><span class="sxs-lookup"><span data-stu-id="553dd-116">Source</span></span> | <span data-ttu-id="553dd-117">封裝來源，將預設為 [來源] 下拉式清單中選取的來源。</span><span class="sxs-lookup"><span data-stu-id="553dd-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="553dd-118">使用權</span><span class="sxs-lookup"><span data-stu-id="553dd-118">License</span></span> | <span data-ttu-id="553dd-119">瀏覽器開啟至封裝的授權 URL。</span><span class="sxs-lookup"><span data-stu-id="553dd-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="553dd-120">如果指定-授權都-ReportAbuse，瀏覽器會開啟封裝的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="553dd-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="553dd-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="553dd-121">ReportAbuse</span></span> | <span data-ttu-id="553dd-122">瀏覽器開啟至套件的報表濫用的 URL。</span><span class="sxs-lookup"><span data-stu-id="553dd-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="553dd-123">如果指定-授權都-ReportAbuse，瀏覽器會開啟封裝的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="553dd-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="553dd-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="553dd-124">PassThru</span></span> | <span data-ttu-id="553dd-125">顯示的 URL。您可以使用與-WhatIf 隱藏開啟瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="553dd-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="553dd-126">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="553dd-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="553dd-127">一般參數</span><span class="sxs-lookup"><span data-stu-id="553dd-127">Common Parameters</span></span>

<span data-ttu-id="553dd-128">`Open-PackagePage`支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="553dd-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="553dd-129">範例</span><span class="sxs-lookup"><span data-stu-id="553dd-129">Examples</span></span>

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