---
title: "NuGet 的同步處理封裝 PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1b980b93-fa58-430c-b663-78ce069b1603
description: "在 Visual Studio 中的 NuGet 封裝管理員主控台中的同步處理封裝 PowerShell 命令的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考資料，同步處理封裝"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dc542714f14f0e6d3e827292f8fce06561fe270
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="dc56f-104">同步處理封裝 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="dc56f-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="dc56f-105">*3.0 +; 版本只能在[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="dc56f-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="dc56f-106">取得從安裝套件的版本指定 （或預設） 專案，並同步處理其餘部分的方案中專案的版本。</span><span class="sxs-lookup"><span data-stu-id="dc56f-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="dc56f-107">語法</span><span class="sxs-lookup"><span data-stu-id="dc56f-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="dc56f-108">參數</span><span class="sxs-lookup"><span data-stu-id="dc56f-108">Parameters</span></span>

| <span data-ttu-id="dc56f-109">參數</span><span class="sxs-lookup"><span data-stu-id="dc56f-109">Parameter</span></span> | <span data-ttu-id="dc56f-110">說明</span><span class="sxs-lookup"><span data-stu-id="dc56f-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc56f-111">ID</span><span class="sxs-lookup"><span data-stu-id="dc56f-111">Id</span></span> | <span data-ttu-id="dc56f-112">（必要）要同步處理之封裝的識別碼。-Id 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="dc56f-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="dc56f-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="dc56f-113">IgnoreDependencies</span></span> | <span data-ttu-id="dc56f-114">安裝僅此套件不其相依性。</span><span class="sxs-lookup"><span data-stu-id="dc56f-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="dc56f-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="dc56f-115">ProjectName</span></span> | <span data-ttu-id="dc56f-116">要同步處理預設為預設專案，從封裝的專案。</span><span class="sxs-lookup"><span data-stu-id="dc56f-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="dc56f-117">版本</span><span class="sxs-lookup"><span data-stu-id="dc56f-117">Version</span></span> | <span data-ttu-id="dc56f-118">若要同步，封裝版本預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="dc56f-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="dc56f-119">來源</span><span class="sxs-lookup"><span data-stu-id="dc56f-119">Source</span></span> | <span data-ttu-id="dc56f-120">要搜尋的封裝來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="dc56f-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="dc56f-121">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="dc56f-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="dc56f-122">如果省略，`Sync-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="dc56f-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="dc56f-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="dc56f-123">IncludePrerelease</span></span> | <span data-ttu-id="dc56f-124">在同步處理包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="dc56f-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="dc56f-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="dc56f-125">FileConflictAction</span></span> | <span data-ttu-id="dc56f-126">當詢問您要覆寫或略過專案所參考的現有檔案時要採取動作。</span><span class="sxs-lookup"><span data-stu-id="dc56f-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="dc56f-127">可能的值為*覆寫，忽略、 None、 OverwriteAll*，和*（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="dc56f-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="dc56f-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="dc56f-128">DependencyVersion</span></span> | <span data-ttu-id="dc56f-129">若要使用，可以是下列其中之一的相依性套件的版本：</span><span class="sxs-lookup"><span data-stu-id="dc56f-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="dc56f-130">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="dc56f-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="dc56f-131">*HighestPatch*： 具有最低主要、 次要最低、 最高的修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="dc56f-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="dc56f-132">*HighestMinor*： 具有最低主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="dc56f-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="dc56f-133">*最高*（預設值更新套件不含任何參數）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="dc56f-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="dc56f-134">您可以設定預設值使用[ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="dc56f-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="dc56f-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="dc56f-135">WhatIf</span></span> | <span data-ttu-id="dc56f-136">顯示執行命令，而不需實際執行同步處理時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="dc56f-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="dc56f-137">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="dc56f-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="dc56f-138">一般參數</span><span class="sxs-lookup"><span data-stu-id="dc56f-138">Common Parameters</span></span>

<span data-ttu-id="dc56f-139">`Sync-Package`支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="dc56f-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="dc56f-140">範例</span><span class="sxs-lookup"><span data-stu-id="dc56f-140">Examples</span></span>

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
