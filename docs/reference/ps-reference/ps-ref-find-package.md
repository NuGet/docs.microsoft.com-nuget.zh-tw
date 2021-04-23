---
title: NuGet Find-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Find-Package PowerShell 命令參考。
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901755"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e48cb-103">Visual Studio) 中的 Find-Package (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="e48cb-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e48cb-104">*3.0 版 +;本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Find-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement)。*</span><span class="sxs-lookup"><span data-stu-id="e48cb-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="e48cb-105">從套件來源取得具有指定識別碼或關鍵字的遠端封裝集合。</span><span class="sxs-lookup"><span data-stu-id="e48cb-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="e48cb-106">語法</span><span class="sxs-lookup"><span data-stu-id="e48cb-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e48cb-107">參數</span><span class="sxs-lookup"><span data-stu-id="e48cb-107">Parameters</span></span>

| <span data-ttu-id="e48cb-108">參數</span><span class="sxs-lookup"><span data-stu-id="e48cb-108">Parameter</span></span> | <span data-ttu-id="e48cb-109">Description</span><span class="sxs-lookup"><span data-stu-id="e48cb-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e48cb-110">識別碼 &lt; 關鍵字&gt;</span><span class="sxs-lookup"><span data-stu-id="e48cb-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="e48cb-111"> (在搜尋套件來源時，需要使用) 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="e48cb-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="e48cb-112">使用-ExactMatch 只傳回套件識別碼符合關鍵字的封裝。</span><span class="sxs-lookup"><span data-stu-id="e48cb-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="e48cb-113">如果未指定任何關鍵字，則會 `Find-Package` 依下載傳回前20個封裝的清單，或依-First 指定的數位。</span><span class="sxs-lookup"><span data-stu-id="e48cb-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="e48cb-114">請注意，-Id 是選擇性的，且不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="e48cb-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="e48cb-115">來源</span><span class="sxs-lookup"><span data-stu-id="e48cb-115">Source</span></span> | <span data-ttu-id="e48cb-116">要搜尋之套件來源的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="e48cb-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e48cb-117">本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="e48cb-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e48cb-118">如果省略，則會 `Find-Package` 搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="e48cb-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e48cb-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="e48cb-119">AllVersions</span></span> | <span data-ttu-id="e48cb-120">顯示每個套件的所有可用版本，而不是僅限最新版本。</span><span class="sxs-lookup"><span data-stu-id="e48cb-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="e48cb-121">First</span><span class="sxs-lookup"><span data-stu-id="e48cb-121">First</span></span> | <span data-ttu-id="e48cb-122">要從清單開頭傳回的封裝數目;預設值為20。</span><span class="sxs-lookup"><span data-stu-id="e48cb-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="e48cb-123">跳過</span><span class="sxs-lookup"><span data-stu-id="e48cb-123">Skip</span></span> | <span data-ttu-id="e48cb-124">省略 &lt; &gt; 所顯示清單中的第一個 int 封裝。</span><span class="sxs-lookup"><span data-stu-id="e48cb-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="e48cb-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e48cb-125">IncludePrerelease</span></span> | <span data-ttu-id="e48cb-126">在結果中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="e48cb-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="e48cb-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="e48cb-127">ExactMatch</span></span> | <span data-ttu-id="e48cb-128">指定為使用 &lt; 關鍵字 &gt; 做為區分大小寫的套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="e48cb-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="e48cb-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="e48cb-129">StartWith</span></span> | <span data-ttu-id="e48cb-130">傳回封裝識別碼開頭為關鍵字的 &lt; 封裝 &gt; 。</span><span class="sxs-lookup"><span data-stu-id="e48cb-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="e48cb-131">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="e48cb-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e48cb-132">一般參數</span><span class="sxs-lookup"><span data-stu-id="e48cb-132">Common Parameters</span></span>

<span data-ttu-id="e48cb-133">`Find-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e48cb-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e48cb-134">範例</span><span class="sxs-lookup"><span data-stu-id="e48cb-134">Examples</span></span>

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