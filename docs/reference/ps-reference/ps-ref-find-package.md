---
title: NuGet 尋找-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [尋找套件] PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327385"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="aa49a-103">Find-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="aa49a-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="aa49a-104">*3.0 版 +;本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 的尋找封裝命令, 請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="aa49a-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="aa49a-105">從封裝來源取得具有指定識別碼或關鍵字之遠端封裝的集合。</span><span class="sxs-lookup"><span data-stu-id="aa49a-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="aa49a-106">語法</span><span class="sxs-lookup"><span data-stu-id="aa49a-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="aa49a-107">參數</span><span class="sxs-lookup"><span data-stu-id="aa49a-107">Parameters</span></span>

| <span data-ttu-id="aa49a-108">參數</span><span class="sxs-lookup"><span data-stu-id="aa49a-108">Parameter</span></span> | <span data-ttu-id="aa49a-109">描述</span><span class="sxs-lookup"><span data-stu-id="aa49a-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa49a-110">Id &lt;關鍵字&gt;</span><span class="sxs-lookup"><span data-stu-id="aa49a-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="aa49a-111">具備搜尋封裝來源時要使用的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="aa49a-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="aa49a-112">使用-ExactMatch, 只傳回套件識別碼符合關鍵字的封裝。</span><span class="sxs-lookup"><span data-stu-id="aa49a-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="aa49a-113">如果未指定任何關鍵字, `Find-Package`則會傳回前20個封裝的清單 (依下載), 或由-First 指定的數位。</span><span class="sxs-lookup"><span data-stu-id="aa49a-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="aa49a-114">請注意,-Id 是選擇性的, 也是無 op。</span><span class="sxs-lookup"><span data-stu-id="aa49a-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="aa49a-115">Source</span><span class="sxs-lookup"><span data-stu-id="aa49a-115">Source</span></span> | <span data-ttu-id="aa49a-116">要搜尋之封裝來源的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="aa49a-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="aa49a-117">本機資料夾路徑可以是絕對或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="aa49a-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="aa49a-118">如果省略, `Find-Package`則會搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="aa49a-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="aa49a-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="aa49a-119">AllVersions</span></span> | <span data-ttu-id="aa49a-120">顯示每個套件的所有可用版本, 而不只是最新版本。</span><span class="sxs-lookup"><span data-stu-id="aa49a-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="aa49a-121">第一個</span><span class="sxs-lookup"><span data-stu-id="aa49a-121">First</span></span> | <span data-ttu-id="aa49a-122">要從清單開頭傳回的封裝數目;預設值為20。</span><span class="sxs-lookup"><span data-stu-id="aa49a-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="aa49a-123">Skip</span><span class="sxs-lookup"><span data-stu-id="aa49a-123">Skip</span></span> | <span data-ttu-id="aa49a-124">省略所顯示&lt;清單&gt;中的第一個 int 封裝。</span><span class="sxs-lookup"><span data-stu-id="aa49a-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="aa49a-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="aa49a-125">IncludePrerelease</span></span> | <span data-ttu-id="aa49a-126">在結果中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="aa49a-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="aa49a-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="aa49a-127">ExactMatch</span></span> | <span data-ttu-id="aa49a-128">指定使用&lt;關鍵字&gt;做為區分大小寫的封裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa49a-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="aa49a-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="aa49a-129">StartWith</span></span> | <span data-ttu-id="aa49a-130">傳回封裝識別碼開頭為&lt;關鍵字&gt;的封裝。</span><span class="sxs-lookup"><span data-stu-id="aa49a-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="aa49a-131">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="aa49a-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="aa49a-132">一般參數</span><span class="sxs-lookup"><span data-stu-id="aa49a-132">Common Parameters</span></span>

<span data-ttu-id="aa49a-133">`Find-Package`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="aa49a-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="aa49a-134">範例</span><span class="sxs-lookup"><span data-stu-id="aa49a-134">Examples</span></span>

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
