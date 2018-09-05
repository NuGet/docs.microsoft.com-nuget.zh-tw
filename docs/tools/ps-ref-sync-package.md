---
title: 同步處理-Nuget PowerShell 參考
description: 在 NuGet 套件管理員主控台中，在 Visual Studio 中的同步處理封裝的 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547990"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a146a-103">Sync-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="a146a-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a146a-104">*版本 3.0 + 中;只能在[NuGet 套件管理員主控台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="a146a-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a146a-105">取得從已安裝封裝的版本指定 （或預設） 專案，並同步處理到其他方案中專案的版本。</span><span class="sxs-lookup"><span data-stu-id="a146a-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="a146a-106">語法</span><span class="sxs-lookup"><span data-stu-id="a146a-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a146a-107">參數</span><span class="sxs-lookup"><span data-stu-id="a146a-107">Parameters</span></span>

| <span data-ttu-id="a146a-108">參數</span><span class="sxs-lookup"><span data-stu-id="a146a-108">Parameter</span></span> | <span data-ttu-id="a146a-109">描述</span><span class="sxs-lookup"><span data-stu-id="a146a-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a146a-110">ID</span><span class="sxs-lookup"><span data-stu-id="a146a-110">Id</span></span> | <span data-ttu-id="a146a-111">（必要）要同步處理之封裝的識別碼。-識別碼是選擇性參數本身。</span><span class="sxs-lookup"><span data-stu-id="a146a-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="a146a-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="a146a-112">IgnoreDependencies</span></span> | <span data-ttu-id="a146a-113">安裝只需將此套件不及其相依性。</span><span class="sxs-lookup"><span data-stu-id="a146a-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="a146a-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="a146a-114">ProjectName</span></span> | <span data-ttu-id="a146a-115">要同步處理預設為預設專案，封裝的專案。</span><span class="sxs-lookup"><span data-stu-id="a146a-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="a146a-116">版本</span><span class="sxs-lookup"><span data-stu-id="a146a-116">Version</span></span> | <span data-ttu-id="a146a-117">若要同步，封裝的版本預設為目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="a146a-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="a146a-118">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="a146a-118">Source</span></span> | <span data-ttu-id="a146a-119">要搜尋的套件來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="a146a-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="a146a-120">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a146a-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a146a-121">如果省略，`Sync-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="a146a-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="a146a-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="a146a-122">IncludePrerelease</span></span> | <span data-ttu-id="a146a-123">包含發行前版本套件中的同步處理。</span><span class="sxs-lookup"><span data-stu-id="a146a-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="a146a-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="a146a-124">FileConflictAction</span></span> | <span data-ttu-id="a146a-125">當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="a146a-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="a146a-126">可能的值為*覆寫，忽略、 None、 OverwriteAll*，並 *（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="a146a-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="a146a-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="a146a-127">DependencyVersion</span></span> | <span data-ttu-id="a146a-128">若要使用，相依性套件可以是下列其中一種版本：</span><span class="sxs-lookup"><span data-stu-id="a146a-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="a146a-129">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="a146a-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="a146a-130">*HighestPatch*： 具有最低的主要、 次要最低、 最高的修補程式版本</span><span class="sxs-lookup"><span data-stu-id="a146a-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="a146a-131">*HighestMinor*： 具有最低的主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="a146a-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="a146a-132">*最高*（預設值更新套件不含任何參數）： 最高版本</span><span class="sxs-lookup"><span data-stu-id="a146a-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="a146a-133">您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="a146a-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="a146a-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="a146a-134">WhatIf</span></span> | <span data-ttu-id="a146a-135">顯示執行命令，而不實際執行的同步處理時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="a146a-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="a146a-136">這些參數都不接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="a146a-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a146a-137">一般參數</span><span class="sxs-lookup"><span data-stu-id="a146a-137">Common Parameters</span></span>

<span data-ttu-id="a146a-138">`Sync-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="a146a-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a146a-139">範例</span><span class="sxs-lookup"><span data-stu-id="a146a-139">Examples</span></span>

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
