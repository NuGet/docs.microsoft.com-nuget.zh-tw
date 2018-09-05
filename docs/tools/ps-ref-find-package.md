---
title: NuGet Find-package PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台中尋找封裝 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550974"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5b998-103">Find-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="5b998-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5b998-104">*版本 3.0 + 中;本主題描述內的命令[NuGet 套件管理員主控台](package-manager-console.md)在 Windows 上的 Visual Studio 中。一般的 PowerShell 尋找套件命令，請參閱 < [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="5b998-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="5b998-105">取得具有指定識別碼或關鍵字的遠端封裝一組從套件來源。</span><span class="sxs-lookup"><span data-stu-id="5b998-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="5b998-106">語法</span><span class="sxs-lookup"><span data-stu-id="5b998-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5b998-107">參數</span><span class="sxs-lookup"><span data-stu-id="5b998-107">Parameters</span></span>

| <span data-ttu-id="5b998-108">參數</span><span class="sxs-lookup"><span data-stu-id="5b998-108">Parameter</span></span> | <span data-ttu-id="5b998-109">描述</span><span class="sxs-lookup"><span data-stu-id="5b998-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5b998-110">識別碼&lt;關鍵字&gt;</span><span class="sxs-lookup"><span data-stu-id="5b998-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="5b998-111">（必要）搜尋套件來源時要使用的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="5b998-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="5b998-112">您可以使用-ExactMatch 傳回套件識別碼符合關鍵字的封裝。</span><span class="sxs-lookup"><span data-stu-id="5b998-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="5b998-113">如果不指定任何關鍵字，`Find-Package`傳回下載項目，或數字的前 20 個套件的清單所指定的第一次。</span><span class="sxs-lookup"><span data-stu-id="5b998-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="5b998-114">請注意，-識別碼是選擇性的並執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="5b998-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="5b998-115">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="5b998-115">Source</span></span> | <span data-ttu-id="5b998-116">要搜尋的套件來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="5b998-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5b998-117">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5b998-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5b998-118">如果省略，`Find-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="5b998-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5b998-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="5b998-119">AllVersions</span></span> | <span data-ttu-id="5b998-120">顯示每個封裝，而不是最新版本的所有可用版本。</span><span class="sxs-lookup"><span data-stu-id="5b998-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="5b998-121">First</span><span class="sxs-lookup"><span data-stu-id="5b998-121">First</span></span> | <span data-ttu-id="5b998-122">若要從清單開頭傳回封裝的數目預設值為 20。</span><span class="sxs-lookup"><span data-stu-id="5b998-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="5b998-123">Skip</span><span class="sxs-lookup"><span data-stu-id="5b998-123">Skip</span></span> | <span data-ttu-id="5b998-124">省略第一個&lt;int&gt;套件從顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="5b998-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="5b998-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5b998-125">IncludePrerelease</span></span> | <span data-ttu-id="5b998-126">在結果中包含發行前版本的套件。</span><span class="sxs-lookup"><span data-stu-id="5b998-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="5b998-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="5b998-127">ExactMatch</span></span> | <span data-ttu-id="5b998-128">指定使用&lt;關鍵字&gt;做為區分大小寫的套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="5b998-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="5b998-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="5b998-129">StartWith</span></span> | <span data-ttu-id="5b998-130">傳回封裝的封裝識別碼的開頭&lt;關鍵字&gt;。</span><span class="sxs-lookup"><span data-stu-id="5b998-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="5b998-131">這些參數都不接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="5b998-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5b998-132">一般參數</span><span class="sxs-lookup"><span data-stu-id="5b998-132">Common Parameters</span></span>

<span data-ttu-id="5b998-133">`Find-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="5b998-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5b998-134">範例</span><span class="sxs-lookup"><span data-stu-id="5b998-134">Examples</span></span>

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
