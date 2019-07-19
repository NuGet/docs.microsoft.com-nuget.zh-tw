---
title: NuGet 取得套件 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [取得封裝 PowerShell 的參考] 命令。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327345"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="88c1b-103">Get-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="88c1b-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="88c1b-104">*本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 的「取得封裝」命令, 請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="88c1b-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="88c1b-105">抓取本機存放庫中安裝的套件清單、在搭配-ListAvailable 參數使用時, 列出封裝來源中可用的套件, 或在搭配-Update 參數使用時, 列出可用的更新。</span><span class="sxs-lookup"><span data-stu-id="88c1b-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="88c1b-106">語法</span><span class="sxs-lookup"><span data-stu-id="88c1b-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="88c1b-107">如果沒有參數, `Get-Package`則會顯示安裝在預設專案中的封裝清單。</span><span class="sxs-lookup"><span data-stu-id="88c1b-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="88c1b-108">參數</span><span class="sxs-lookup"><span data-stu-id="88c1b-108">Parameters</span></span>

| <span data-ttu-id="88c1b-109">參數</span><span class="sxs-lookup"><span data-stu-id="88c1b-109">Parameter</span></span> | <span data-ttu-id="88c1b-110">描述</span><span class="sxs-lookup"><span data-stu-id="88c1b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88c1b-111">Source</span><span class="sxs-lookup"><span data-stu-id="88c1b-111">Source</span></span> | <span data-ttu-id="88c1b-112">封裝的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="88c1b-112">The URL or folder path for the package .</span></span> <span data-ttu-id="88c1b-113">本機資料夾路徑可以是絕對或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="88c1b-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="88c1b-114">如果省略, `Get-Package`則會搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="88c1b-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="88c1b-115">與-ListAvailable 搭配使用時, 預設為 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="88c1b-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="88c1b-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="88c1b-116">ListAvailable</span></span> | <span data-ttu-id="88c1b-117">列出可從封裝來源取得的套件, 預設為 nuget.org。除非指定了-PageSize 和/或-First, 否則會顯示50套件的預設值。</span><span class="sxs-lookup"><span data-stu-id="88c1b-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="88c1b-118">更新</span><span class="sxs-lookup"><span data-stu-id="88c1b-118">Updates</span></span> | <span data-ttu-id="88c1b-119">列出具有可從封裝來源取得更新的套件。</span><span class="sxs-lookup"><span data-stu-id="88c1b-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="88c1b-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="88c1b-120">ProjectName</span></span> | <span data-ttu-id="88c1b-121">要從其中取得已安裝封裝的專案。</span><span class="sxs-lookup"><span data-stu-id="88c1b-121">The project from which to get installed packages.</span></span> <span data-ttu-id="88c1b-122">如果省略, 則會傳回整個方案的已安裝專案。</span><span class="sxs-lookup"><span data-stu-id="88c1b-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="88c1b-123">篩選器</span><span class="sxs-lookup"><span data-stu-id="88c1b-123">Filter</span></span> | <span data-ttu-id="88c1b-124">用來縮小封裝清單的篩選字串, 方法是將它套用至套件識別碼、描述和標記。</span><span class="sxs-lookup"><span data-stu-id="88c1b-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="88c1b-125">第一個</span><span class="sxs-lookup"><span data-stu-id="88c1b-125">First</span></span> | <span data-ttu-id="88c1b-126">要從清單開頭傳回的封裝數目。</span><span class="sxs-lookup"><span data-stu-id="88c1b-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="88c1b-127">如果未指定, 則預設為50。</span><span class="sxs-lookup"><span data-stu-id="88c1b-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="88c1b-128">Skip</span><span class="sxs-lookup"><span data-stu-id="88c1b-128">Skip</span></span> | <span data-ttu-id="88c1b-129">省略所顯示&lt;清單&gt;中的第一個 int 封裝。</span><span class="sxs-lookup"><span data-stu-id="88c1b-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="88c1b-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="88c1b-130">AllVersions</span></span> | <span data-ttu-id="88c1b-131">顯示每個套件的所有可用版本, 而不只是最新版本。</span><span class="sxs-lookup"><span data-stu-id="88c1b-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="88c1b-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="88c1b-132">IncludePrerelease</span></span> | <span data-ttu-id="88c1b-133">在結果中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="88c1b-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="88c1b-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="88c1b-134">PageSize</span></span> | <span data-ttu-id="88c1b-135">*(3.0 +)* 與-ListAvailable (必要) 搭配使用時, 要列出的封裝數目, 再讓提示繼續進行。</span><span class="sxs-lookup"><span data-stu-id="88c1b-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="88c1b-136">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="88c1b-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="88c1b-137">一般參數</span><span class="sxs-lookup"><span data-stu-id="88c1b-137">Common Parameters</span></span>

<span data-ttu-id="88c1b-138">`Get-Package`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="88c1b-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="88c1b-139">範例</span><span class="sxs-lookup"><span data-stu-id="88c1b-139">Examples</span></span>

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
