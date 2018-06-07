---
title: NuGet 的同步處理封裝 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台中的同步處理封裝 PowerShell 命令的參考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 92f0d7490dea57a69b5a5cb3cb7165f665f60d44
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818101"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="0b541-103">Sync-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="0b541-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0b541-104">*3.0 +; 版本只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="0b541-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0b541-105">取得從安裝套件的版本指定 （或預設） 專案，並同步處理其餘部分的方案中專案的版本。</span><span class="sxs-lookup"><span data-stu-id="0b541-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="0b541-106">語法</span><span class="sxs-lookup"><span data-stu-id="0b541-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0b541-107">參數</span><span class="sxs-lookup"><span data-stu-id="0b541-107">Parameters</span></span>

| <span data-ttu-id="0b541-108">參數</span><span class="sxs-lookup"><span data-stu-id="0b541-108">Parameter</span></span> | <span data-ttu-id="0b541-109">描述</span><span class="sxs-lookup"><span data-stu-id="0b541-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0b541-110">ID</span><span class="sxs-lookup"><span data-stu-id="0b541-110">Id</span></span> | <span data-ttu-id="0b541-111">（必要）要同步處理之封裝的識別碼。-Id 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="0b541-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="0b541-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="0b541-112">IgnoreDependencies</span></span> | <span data-ttu-id="0b541-113">安裝僅此套件不其相依性。</span><span class="sxs-lookup"><span data-stu-id="0b541-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="0b541-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="0b541-114">ProjectName</span></span> | <span data-ttu-id="0b541-115">要同步處理預設為預設專案，從封裝的專案。</span><span class="sxs-lookup"><span data-stu-id="0b541-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="0b541-116">版本</span><span class="sxs-lookup"><span data-stu-id="0b541-116">Version</span></span> | <span data-ttu-id="0b541-117">若要同步，封裝版本預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="0b541-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="0b541-118">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="0b541-118">Source</span></span> | <span data-ttu-id="0b541-119">要搜尋的封裝來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="0b541-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="0b541-120">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0b541-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="0b541-121">如果省略，`Sync-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="0b541-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="0b541-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="0b541-122">IncludePrerelease</span></span> | <span data-ttu-id="0b541-123">在同步處理包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="0b541-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="0b541-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="0b541-124">FileConflictAction</span></span> | <span data-ttu-id="0b541-125">當詢問您要覆寫或略過專案所參考的現有檔案時要採取動作。</span><span class="sxs-lookup"><span data-stu-id="0b541-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="0b541-126">可能的值為*覆寫，忽略、 None、 OverwriteAll*，和 *（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="0b541-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="0b541-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="0b541-127">DependencyVersion</span></span> | <span data-ttu-id="0b541-128">若要使用，可以是下列其中之一的相依性套件的版本：</span><span class="sxs-lookup"><span data-stu-id="0b541-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="0b541-129">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="0b541-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="0b541-130">*HighestPatch*： 具有最低主要、 次要最低、 最高的修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="0b541-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="0b541-131">*HighestMinor*： 具有最低主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="0b541-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="0b541-132">*最高*（預設值更新套件不含任何參數）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="0b541-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="0b541-133">您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="0b541-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="0b541-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="0b541-134">WhatIf</span></span> | <span data-ttu-id="0b541-135">顯示執行命令，而不需實際執行同步處理時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="0b541-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="0b541-136">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="0b541-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0b541-137">一般參數</span><span class="sxs-lookup"><span data-stu-id="0b541-137">Common Parameters</span></span>

<span data-ttu-id="0b541-138">`Sync-Package` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="0b541-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0b541-139">範例</span><span class="sxs-lookup"><span data-stu-id="0b541-139">Examples</span></span>

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
