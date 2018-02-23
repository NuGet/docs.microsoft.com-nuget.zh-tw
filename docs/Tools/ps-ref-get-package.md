---
title: "NuGet 取得封裝的 PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "取得封裝 PowerShell 命令，在 Visual Studio 中的 NuGet 封裝管理員主控台中的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考資料，取得封裝"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 01a874ce9ae59dcaeb696a45f23cc5e9f2cfa251
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="921c3-104">取得封裝 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="921c3-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="921c3-105">*本主題描述內的命令[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。一般 PowerShell 取得封裝的命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="921c3-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="921c3-106">擷取安裝在本機儲存機制中的封裝清單，列出可用的封裝，從套件來源時使用-ListAvailable 參數或列出可用的更新，當搭配-Update 參數。</span><span class="sxs-lookup"><span data-stu-id="921c3-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="921c3-107">語法</span><span class="sxs-lookup"><span data-stu-id="921c3-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="921c3-108">使用任何參數，`Get-Package`顯示的預設專案中安裝的封裝清單。</span><span class="sxs-lookup"><span data-stu-id="921c3-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="921c3-109">參數</span><span class="sxs-lookup"><span data-stu-id="921c3-109">Parameters</span></span>

| <span data-ttu-id="921c3-110">參數</span><span class="sxs-lookup"><span data-stu-id="921c3-110">Parameter</span></span> | <span data-ttu-id="921c3-111">描述</span><span class="sxs-lookup"><span data-stu-id="921c3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="921c3-112">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="921c3-112">Source</span></span> | <span data-ttu-id="921c3-113">封裝的 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="921c3-113">The URL or folder path for the package .</span></span> <span data-ttu-id="921c3-114">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="921c3-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="921c3-115">如果省略，`Get-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="921c3-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="921c3-116">當搭配使用-ListAvailable，預設為 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="921c3-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="921c3-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="921c3-117">ListAvailable</span></span> | <span data-ttu-id="921c3-118">列出可用的封裝，從套件來源，將預設為 nuget.org。除非已指定-PageSize 及/或-第一個會顯示預設值是 50 的封裝。</span><span class="sxs-lookup"><span data-stu-id="921c3-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="921c3-119">更新</span><span class="sxs-lookup"><span data-stu-id="921c3-119">Updates</span></span> | <span data-ttu-id="921c3-120">列出從套件來源中有可用更新的封裝。</span><span class="sxs-lookup"><span data-stu-id="921c3-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="921c3-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="921c3-121">ProjectName</span></span> | <span data-ttu-id="921c3-122">要從中取得已安裝的套件的專案。</span><span class="sxs-lookup"><span data-stu-id="921c3-122">The project from which to get installed packages.</span></span> <span data-ttu-id="921c3-123">如果省略，則傳回安裝整個方案的專案。</span><span class="sxs-lookup"><span data-stu-id="921c3-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="921c3-124">篩選器</span><span class="sxs-lookup"><span data-stu-id="921c3-124">Filter</span></span> | <span data-ttu-id="921c3-125">篩選條件字串，用來縮小的封裝清單，將它套用到封裝識別碼、 描述和標記。</span><span class="sxs-lookup"><span data-stu-id="921c3-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="921c3-126">First</span><span class="sxs-lookup"><span data-stu-id="921c3-126">First</span></span> | <span data-ttu-id="921c3-127">要從清單開頭傳回的套件數目。</span><span class="sxs-lookup"><span data-stu-id="921c3-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="921c3-128">如果未指定，預設值為 50。</span><span class="sxs-lookup"><span data-stu-id="921c3-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="921c3-129">Skip</span><span class="sxs-lookup"><span data-stu-id="921c3-129">Skip</span></span> | <span data-ttu-id="921c3-130">省略第一個&lt;int&gt;封裝從顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="921c3-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="921c3-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="921c3-131">AllVersions</span></span> | <span data-ttu-id="921c3-132">顯示所有可用的版本，每個封裝而不是最新的版本。</span><span class="sxs-lookup"><span data-stu-id="921c3-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="921c3-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="921c3-133">IncludePrerelease</span></span> | <span data-ttu-id="921c3-134">在結果中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="921c3-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="921c3-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="921c3-135">PageSize</span></span> | <span data-ttu-id="921c3-136">*（3.0 +)*時搭配使用-ListAvailable （必要），封裝的數目，列出要繼續的提示之前。</span><span class="sxs-lookup"><span data-stu-id="921c3-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="921c3-137">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="921c3-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="921c3-138">一般參數</span><span class="sxs-lookup"><span data-stu-id="921c3-138">Common Parameters</span></span>

<span data-ttu-id="921c3-139">`Get-Package` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="921c3-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="921c3-140">範例</span><span class="sxs-lookup"><span data-stu-id="921c3-140">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
