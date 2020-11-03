---
title: NuGet Sync-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Sync-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238045"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c6222-103">Visual Studio) 中的 Sync-Package (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="c6222-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c6222-104">*3.0 版 +;只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*</span><span class="sxs-lookup"><span data-stu-id="c6222-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c6222-105">從指定的 (或預設) 專案取得已安裝套件的版本，並將版本同步處理至方案中的其餘專案。</span><span class="sxs-lookup"><span data-stu-id="c6222-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="c6222-106">語法</span><span class="sxs-lookup"><span data-stu-id="c6222-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c6222-107">參數</span><span class="sxs-lookup"><span data-stu-id="c6222-107">Parameters</span></span>

| <span data-ttu-id="c6222-108">參數</span><span class="sxs-lookup"><span data-stu-id="c6222-108">Parameter</span></span> | <span data-ttu-id="c6222-109">Description</span><span class="sxs-lookup"><span data-stu-id="c6222-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6222-110">Id</span><span class="sxs-lookup"><span data-stu-id="c6222-110">Id</span></span> | <span data-ttu-id="c6222-111"> (需要) 要同步的封裝識別碼。-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="c6222-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c6222-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="c6222-112">IgnoreDependencies</span></span> | <span data-ttu-id="c6222-113">只安裝此套件，而不安裝其相依性。</span><span class="sxs-lookup"><span data-stu-id="c6222-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="c6222-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c6222-114">ProjectName</span></span> | <span data-ttu-id="c6222-115">要同步處理封裝的專案，預設為預設專案。</span><span class="sxs-lookup"><span data-stu-id="c6222-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="c6222-116">版本</span><span class="sxs-lookup"><span data-stu-id="c6222-116">Version</span></span> | <span data-ttu-id="c6222-117">要同步處理的封裝版本，預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c6222-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="c6222-118">來源</span><span class="sxs-lookup"><span data-stu-id="c6222-118">Source</span></span> | <span data-ttu-id="c6222-119">要搜尋之套件來源的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="c6222-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="c6222-120">本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="c6222-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c6222-121">如果省略，則會 `Sync-Package` 搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="c6222-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="c6222-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c6222-122">IncludePrerelease</span></span> | <span data-ttu-id="c6222-123">在同步處理中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="c6222-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="c6222-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c6222-124">FileConflictAction</span></span> | <span data-ttu-id="c6222-125">當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="c6222-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c6222-126">可能的值為 *覆寫、忽略、無、OverwriteAll* 和 *(3.0 +)* *IgnoreAll* 。</span><span class="sxs-lookup"><span data-stu-id="c6222-126">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll* .</span></span> |
| <span data-ttu-id="c6222-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="c6222-127">DependencyVersion</span></span> | <span data-ttu-id="c6222-128">要使用之相依性套件的版本，它可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="c6222-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="c6222-129">*最低* (預設) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="c6222-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="c6222-130">*HighestPatch* ：最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="c6222-130">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="c6222-131">*HighestMinor* ：最低主要、最小次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="c6222-131">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="c6222-132">不含參數的 Update-Package *最高* (預設值) ：最高版本</span><span class="sxs-lookup"><span data-stu-id="c6222-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="c6222-133">您可以使用檔案中的設定來設定預設值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="c6222-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="c6222-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c6222-134">WhatIf</span></span> | <span data-ttu-id="c6222-135">顯示執行命令時所發生的狀況，而不實際執行同步處理。</span><span class="sxs-lookup"><span data-stu-id="c6222-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="c6222-136">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="c6222-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c6222-137">一般參數</span><span class="sxs-lookup"><span data-stu-id="c6222-137">Common Parameters</span></span>

<span data-ttu-id="c6222-138">`Sync-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="c6222-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c6222-139">範例</span><span class="sxs-lookup"><span data-stu-id="c6222-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```