---
title: NuGet 同步-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [同步處理-封裝 PowerShell] 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384899"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7de42-103">同步-封裝（Visual Studio 中的套件管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="7de42-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7de42-104">*3.0 版 +;僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*</span><span class="sxs-lookup"><span data-stu-id="7de42-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7de42-105">從指定的（或預設）專案取得已安裝封裝的版本，並將版本同步處理至方案中的其餘專案。</span><span class="sxs-lookup"><span data-stu-id="7de42-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="7de42-106">語法</span><span class="sxs-lookup"><span data-stu-id="7de42-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7de42-107">參數</span><span class="sxs-lookup"><span data-stu-id="7de42-107">Parameters</span></span>

| <span data-ttu-id="7de42-108">參數</span><span class="sxs-lookup"><span data-stu-id="7de42-108">Parameter</span></span> | <span data-ttu-id="7de42-109">描述</span><span class="sxs-lookup"><span data-stu-id="7de42-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7de42-110">ID</span><span class="sxs-lookup"><span data-stu-id="7de42-110">Id</span></span> | <span data-ttu-id="7de42-111">具備要同步處理之封裝的識別碼。-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="7de42-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7de42-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="7de42-112">IgnoreDependencies</span></span> | <span data-ttu-id="7de42-113">僅安裝此套件，而不是其相依性。</span><span class="sxs-lookup"><span data-stu-id="7de42-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="7de42-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7de42-114">ProjectName</span></span> | <span data-ttu-id="7de42-115">要同步處理封裝的專案，預設為預設專案。</span><span class="sxs-lookup"><span data-stu-id="7de42-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="7de42-116">{2&gt;版本&lt;2}</span><span class="sxs-lookup"><span data-stu-id="7de42-116">Version</span></span> | <span data-ttu-id="7de42-117">要同步處理的封裝版本，預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="7de42-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="7de42-118">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="7de42-118">Source</span></span> | <span data-ttu-id="7de42-119">要搜尋之封裝來源的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="7de42-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="7de42-120">本機資料夾路徑可以是絕對或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7de42-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="7de42-121">如果省略，`Sync-Package` 會搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="7de42-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="7de42-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="7de42-122">IncludePrerelease</span></span> | <span data-ttu-id="7de42-123">包含同步處理中的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="7de42-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="7de42-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="7de42-124">FileConflictAction</span></span> | <span data-ttu-id="7de42-125">當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="7de42-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="7de42-126">可能的值為*Overwrite、Ignore、None、OverwriteAll*和 *（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="7de42-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="7de42-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="7de42-127">DependencyVersion</span></span> | <span data-ttu-id="7de42-128">要使用的相依性套件版本，它可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="7de42-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="7de42-129">*最低*（預設值）：最低版本</span><span class="sxs-lookup"><span data-stu-id="7de42-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="7de42-130">*HighestPatch*：具有最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="7de42-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="7de42-131">*HighestMinor*：具有最低主要、最高次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="7de42-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="7de42-132">*最高*（不含參數的更新套件預設值）：最高版本</span><span class="sxs-lookup"><span data-stu-id="7de42-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="7de42-133">您可以使用 `Nuget.Config` 檔案中的[`dependencyVersion`](../nuget-config-file.md#config-section)設定來設定預設值。</span><span class="sxs-lookup"><span data-stu-id="7de42-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="7de42-134">Whatif</span><span class="sxs-lookup"><span data-stu-id="7de42-134">WhatIf</span></span> | <span data-ttu-id="7de42-135">顯示執行命令時，不會實際執行同步處理的情況。</span><span class="sxs-lookup"><span data-stu-id="7de42-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="7de42-136">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="7de42-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7de42-137">一般參數</span><span class="sxs-lookup"><span data-stu-id="7de42-137">Common Parameters</span></span>

<span data-ttu-id="7de42-138">`Sync-Package` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="7de42-138">`Sync-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7de42-139">範例</span><span class="sxs-lookup"><span data-stu-id="7de42-139">Examples</span></span>

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
