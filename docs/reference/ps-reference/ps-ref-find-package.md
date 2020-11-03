---
title: NuGet Find-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Find-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 267dd3eb501cae6e419386a5ca5e0c1ab659f807
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238084"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="aece2-103">Visual Studio) 中的 Find-Package (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="aece2-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="aece2-104">*3.0 版 +;本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Find-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="aece2-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="aece2-105">從套件來源取得具有指定識別碼或關鍵字的遠端封裝集合。</span><span class="sxs-lookup"><span data-stu-id="aece2-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="aece2-106">語法</span><span class="sxs-lookup"><span data-stu-id="aece2-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="aece2-107">參數</span><span class="sxs-lookup"><span data-stu-id="aece2-107">Parameters</span></span>

| <span data-ttu-id="aece2-108">參數</span><span class="sxs-lookup"><span data-stu-id="aece2-108">Parameter</span></span> | <span data-ttu-id="aece2-109">Description</span><span class="sxs-lookup"><span data-stu-id="aece2-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aece2-110">識別碼 &lt; 關鍵字&gt;</span><span class="sxs-lookup"><span data-stu-id="aece2-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="aece2-111"> (在搜尋套件來源時，需要使用) 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="aece2-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="aece2-112">使用-ExactMatch 只傳回套件識別碼符合關鍵字的封裝。</span><span class="sxs-lookup"><span data-stu-id="aece2-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="aece2-113">如果未指定任何關鍵字，則會 `Find-Package` 依下載傳回前20個封裝的清單，或依-First 指定的數位。</span><span class="sxs-lookup"><span data-stu-id="aece2-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="aece2-114">請注意，-Id 是選擇性的，且不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="aece2-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="aece2-115">來源</span><span class="sxs-lookup"><span data-stu-id="aece2-115">Source</span></span> | <span data-ttu-id="aece2-116">要搜尋之套件來源的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="aece2-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="aece2-117">本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="aece2-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="aece2-118">如果省略，則會 `Find-Package` 搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="aece2-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="aece2-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="aece2-119">AllVersions</span></span> | <span data-ttu-id="aece2-120">顯示每個套件的所有可用版本，而不是僅限最新版本。</span><span class="sxs-lookup"><span data-stu-id="aece2-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="aece2-121">First</span><span class="sxs-lookup"><span data-stu-id="aece2-121">First</span></span> | <span data-ttu-id="aece2-122">要從清單開頭傳回的封裝數目;預設值為20。</span><span class="sxs-lookup"><span data-stu-id="aece2-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="aece2-123">跳過</span><span class="sxs-lookup"><span data-stu-id="aece2-123">Skip</span></span> | <span data-ttu-id="aece2-124">省略 &lt; &gt; 所顯示清單中的第一個 int 封裝。</span><span class="sxs-lookup"><span data-stu-id="aece2-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="aece2-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="aece2-125">IncludePrerelease</span></span> | <span data-ttu-id="aece2-126">在結果中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="aece2-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="aece2-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="aece2-127">ExactMatch</span></span> | <span data-ttu-id="aece2-128">指定為使用 &lt; 關鍵字 &gt; 做為區分大小寫的套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="aece2-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="aece2-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="aece2-129">StartWith</span></span> | <span data-ttu-id="aece2-130">傳回封裝識別碼開頭為關鍵字的 &lt; 封裝 &gt; 。</span><span class="sxs-lookup"><span data-stu-id="aece2-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="aece2-131">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="aece2-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="aece2-132">一般參數</span><span class="sxs-lookup"><span data-stu-id="aece2-132">Common Parameters</span></span>

<span data-ttu-id="aece2-133">`Find-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="aece2-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="aece2-134">範例</span><span class="sxs-lookup"><span data-stu-id="aece2-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```