---
title: NuGet Get-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Get-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237227"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="de2e0-103">Visual Studio) 中的 Get-Package (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="de2e0-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="de2e0-104">*本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Get-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="de2e0-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="de2e0-105">抓取本機儲存機制中所安裝的套件清單、列出套件來源中搭配-ListAvailable 參數使用時可使用的封裝，或在搭配-Update 參數使用時，列出可用的更新。</span><span class="sxs-lookup"><span data-stu-id="de2e0-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="de2e0-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="de2e0-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="de2e0-107">如果沒有參數，會 `Get-Package` 顯示安裝在預設專案中的套件清單。</span><span class="sxs-lookup"><span data-stu-id="de2e0-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="de2e0-108">參數</span><span class="sxs-lookup"><span data-stu-id="de2e0-108">Parameters</span></span>

| <span data-ttu-id="de2e0-109">參數</span><span class="sxs-lookup"><span data-stu-id="de2e0-109">Parameter</span></span> | <span data-ttu-id="de2e0-110">描述</span><span class="sxs-lookup"><span data-stu-id="de2e0-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de2e0-111">來源</span><span class="sxs-lookup"><span data-stu-id="de2e0-111">Source</span></span> | <span data-ttu-id="de2e0-112">封裝的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="de2e0-112">The URL or folder path for the package .</span></span> <span data-ttu-id="de2e0-113">本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="de2e0-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="de2e0-114">如果省略，則會 `Get-Package` 搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="de2e0-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="de2e0-115">搭配-ListAvailable 使用時，預設為 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="de2e0-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="de2e0-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="de2e0-116">ListAvailable</span></span> | <span data-ttu-id="de2e0-117">列出可從套件來源取得的封裝，預設為 nuget.org。除非指定-PageSize 和/或-First，否則會顯示50封裝的預設值。</span><span class="sxs-lookup"><span data-stu-id="de2e0-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="de2e0-118">更新</span><span class="sxs-lookup"><span data-stu-id="de2e0-118">Updates</span></span> | <span data-ttu-id="de2e0-119">列出套件來源中有可用更新的套件。</span><span class="sxs-lookup"><span data-stu-id="de2e0-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="de2e0-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="de2e0-120">ProjectName</span></span> | <span data-ttu-id="de2e0-121">要從中取得已安裝封裝的專案。</span><span class="sxs-lookup"><span data-stu-id="de2e0-121">The project from which to get installed packages.</span></span> <span data-ttu-id="de2e0-122">如果省略，則會傳回整個方案的已安裝專案。</span><span class="sxs-lookup"><span data-stu-id="de2e0-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="de2e0-123">Filter</span><span class="sxs-lookup"><span data-stu-id="de2e0-123">Filter</span></span> | <span data-ttu-id="de2e0-124">篩選字串，用來將封裝清單套用至封裝識別碼、描述和標記，以縮小封裝的範圍。</span><span class="sxs-lookup"><span data-stu-id="de2e0-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="de2e0-125">First</span><span class="sxs-lookup"><span data-stu-id="de2e0-125">First</span></span> | <span data-ttu-id="de2e0-126">要從清單開頭返回的封裝數目。</span><span class="sxs-lookup"><span data-stu-id="de2e0-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="de2e0-127">如果未指定，則預設為50。</span><span class="sxs-lookup"><span data-stu-id="de2e0-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="de2e0-128">跳過</span><span class="sxs-lookup"><span data-stu-id="de2e0-128">Skip</span></span> | <span data-ttu-id="de2e0-129">省略 &lt; &gt; 所顯示清單中的第一個 int 封裝。</span><span class="sxs-lookup"><span data-stu-id="de2e0-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="de2e0-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="de2e0-130">AllVersions</span></span> | <span data-ttu-id="de2e0-131">顯示每個套件的所有可用版本，而不是僅限最新版本。</span><span class="sxs-lookup"><span data-stu-id="de2e0-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="de2e0-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="de2e0-132">IncludePrerelease</span></span> | <span data-ttu-id="de2e0-133">在結果中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="de2e0-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="de2e0-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="de2e0-134">PageSize</span></span> | <span data-ttu-id="de2e0-135">*(3.0 +)* 搭配-ListAvailable (所需的) 時，要在提供提示繼續之前列出的封裝數目。</span><span class="sxs-lookup"><span data-stu-id="de2e0-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="de2e0-136">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="de2e0-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="de2e0-137">一般參數</span><span class="sxs-lookup"><span data-stu-id="de2e0-137">Common Parameters</span></span>

<span data-ttu-id="de2e0-138">`Get-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="de2e0-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="de2e0-139">範例</span><span class="sxs-lookup"><span data-stu-id="de2e0-139">Examples</span></span>

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