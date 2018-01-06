---
title: "NuGet Find-package PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f7b8847-8259-4366-98c0-13cab88d6e1b
description: "在 Visual Studio 中的 NuGet 封裝管理員主控台中尋找封裝 PowerShell 命令的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考資料，尋找封裝"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fb55cc71e0d4b8eee28b232e64d2cc42364fc153
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5c4a9-104">尋找套件 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="5c4a9-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5c4a9-105">*3.0 +; 版本本主題描述內的命令[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上的 Visual Studio 中。一般的 PowerShell Find-package 命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="5c4a9-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="5c4a9-106">從套件來源取得具有指定識別碼或關鍵字的遠端套件集。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="5c4a9-107">語法</span><span class="sxs-lookup"><span data-stu-id="5c4a9-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5c4a9-108">參數</span><span class="sxs-lookup"><span data-stu-id="5c4a9-108">Parameters</span></span>

| <span data-ttu-id="5c4a9-109">參數</span><span class="sxs-lookup"><span data-stu-id="5c4a9-109">Parameter</span></span> | <span data-ttu-id="5c4a9-110">描述</span><span class="sxs-lookup"><span data-stu-id="5c4a9-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c4a9-111">識別碼&lt;關鍵字&gt;</span><span class="sxs-lookup"><span data-stu-id="5c4a9-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="5c4a9-112">（必要）若要搜尋的套件來源時使用的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="5c4a9-113">使用 ExactMatch 傳回其封裝識別碼符合關鍵字的套件。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="5c4a9-114">如果不指定任何關鍵字`Find-Package`傳回的前 20 套件下載，或數字的清單所指定的第一次。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="5c4a9-115">請注意，-識別碼是選擇性，並執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="5c4a9-116">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="5c4a9-116">Source</span></span> | <span data-ttu-id="5c4a9-117">要搜尋的封裝來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5c4a9-118">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5c4a9-119">如果省略，`Find-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5c4a9-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="5c4a9-120">AllVersions</span></span> | <span data-ttu-id="5c4a9-121">顯示所有可用的版本，每個封裝而不是最新的版本。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="5c4a9-122">First</span><span class="sxs-lookup"><span data-stu-id="5c4a9-122">First</span></span> | <span data-ttu-id="5c4a9-123">要從清單開頭傳回的套件數目預設為 20。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="5c4a9-124">Skip</span><span class="sxs-lookup"><span data-stu-id="5c4a9-124">Skip</span></span> | <span data-ttu-id="5c4a9-125">省略第一個&lt;int&gt;封裝從顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="5c4a9-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5c4a9-126">IncludePrerelease</span></span> | <span data-ttu-id="5c4a9-127">在結果中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="5c4a9-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="5c4a9-128">ExactMatch</span></span> | <span data-ttu-id="5c4a9-129">指定使用&lt;關鍵字&gt;為區分大小寫的封裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="5c4a9-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="5c4a9-130">StartWith</span></span> | <span data-ttu-id="5c4a9-131">傳回封裝的封裝識別碼的開頭&lt;關鍵字&gt;。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="5c4a9-132">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5c4a9-133">一般參數</span><span class="sxs-lookup"><span data-stu-id="5c4a9-133">Common Parameters</span></span>

<span data-ttu-id="5c4a9-134">`Find-Package`支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="5c4a9-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5c4a9-135">範例</span><span class="sxs-lookup"><span data-stu-id="5c4a9-135">Examples</span></span>

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
