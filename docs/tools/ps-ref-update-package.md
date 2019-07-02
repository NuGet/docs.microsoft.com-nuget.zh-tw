---
title: NuGet 更新套件的 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台的更新套件的 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496483"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4fc17-103">Update-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="4fc17-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4fc17-104">*只能在[NuGet 套件管理員主控台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="4fc17-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4fc17-105">更新為較新版本的封裝和其相依性或在專案中，所有的封裝。</span><span class="sxs-lookup"><span data-stu-id="4fc17-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="4fc17-106">語法</span><span class="sxs-lookup"><span data-stu-id="4fc17-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="4fc17-107">Nuget 2.8 +`Update-Package`可用降級您的專案中現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="4fc17-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="4fc17-108">比方說，如果您有安裝 Microsoft.AspNet.MVC 5.1.0-rc1，下列命令會降級至 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="4fc17-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="4fc17-109">參數</span><span class="sxs-lookup"><span data-stu-id="4fc17-109">Parameters</span></span>

|  <span data-ttu-id="4fc17-110">參數</span><span class="sxs-lookup"><span data-stu-id="4fc17-110">Parameter</span></span> | <span data-ttu-id="4fc17-111">描述</span><span class="sxs-lookup"><span data-stu-id="4fc17-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4fc17-112">ID</span><span class="sxs-lookup"><span data-stu-id="4fc17-112">Id</span></span> | <span data-ttu-id="4fc17-113">若要更新封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="4fc17-113">The identifier of the package to update.</span></span> <span data-ttu-id="4fc17-114">如果省略，會更新所有封裝。</span><span class="sxs-lookup"><span data-stu-id="4fc17-114">If omitted, updates all packages.</span></span> <span data-ttu-id="4fc17-115">-識別碼是選擇性參數本身。</span><span class="sxs-lookup"><span data-stu-id="4fc17-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4fc17-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="4fc17-116">IgnoreDependencies</span></span> | <span data-ttu-id="4fc17-117">略過更新套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="4fc17-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="4fc17-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4fc17-118">ProjectName</span></span> | <span data-ttu-id="4fc17-119">專案包含要更新的封裝，將預設為所有專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="4fc17-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="4fc17-120">版本</span><span class="sxs-lookup"><span data-stu-id="4fc17-120">Version</span></span> | <span data-ttu-id="4fc17-121">要用於升級，將預設為最新版本的版本。</span><span class="sxs-lookup"><span data-stu-id="4fc17-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="4fc17-122">在 NuGet 3.0 + 中，版本值必須是其中一個*Lowest、 最高、 HighestMinor*，或*HighestPatch* （相當於-安全）。</span><span class="sxs-lookup"><span data-stu-id="4fc17-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="4fc17-123">安全</span><span class="sxs-lookup"><span data-stu-id="4fc17-123">Safe</span></span> | <span data-ttu-id="4fc17-124">限制升級至相同的主要和次要版本與目前已安裝封裝的唯一版本。</span><span class="sxs-lookup"><span data-stu-id="4fc17-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="4fc17-125">Source</span><span class="sxs-lookup"><span data-stu-id="4fc17-125">Source</span></span> | <span data-ttu-id="4fc17-126">要搜尋的套件來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="4fc17-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="4fc17-127">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="4fc17-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="4fc17-128">如果省略，`Update-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="4fc17-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="4fc17-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="4fc17-129">IncludePrerelease</span></span> | <span data-ttu-id="4fc17-130">包含更新的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="4fc17-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="4fc17-131">重新安裝</span><span class="sxs-lookup"><span data-stu-id="4fc17-131">Reinstall</span></span> | <span data-ttu-id="4fc17-132">Resintalls 封裝，使用其目前安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="4fc17-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="4fc17-133">請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="4fc17-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="4fc17-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="4fc17-134">FileConflictAction</span></span> | <span data-ttu-id="4fc17-135">當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="4fc17-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="4fc17-136">可能的值為*覆寫，忽略、 None、 OverwriteAll*，並*IgnoreAll* （3.0 +）。</span><span class="sxs-lookup"><span data-stu-id="4fc17-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="4fc17-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="4fc17-137">DependencyVersion</span></span> | <span data-ttu-id="4fc17-138">若要使用，相依性套件可以是下列其中一種版本：</span><span class="sxs-lookup"><span data-stu-id="4fc17-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="4fc17-139">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="4fc17-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="4fc17-140">*HighestPatch*： 具有最低的主要、 次要最低、 最高的修補程式版本</span><span class="sxs-lookup"><span data-stu-id="4fc17-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="4fc17-141">*HighestMinor*： 具有最低的主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="4fc17-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="4fc17-142">*最高*（預設值更新套件不含任何參數）： 最高版本</span><span class="sxs-lookup"><span data-stu-id="4fc17-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="4fc17-143">您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="4fc17-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="4fc17-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="4fc17-144">ToHighestPatch</span></span> | <span data-ttu-id="4fc17-145">相當於-安全。</span><span class="sxs-lookup"><span data-stu-id="4fc17-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="4fc17-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="4fc17-146">ToHighestMinor</span></span> | <span data-ttu-id="4fc17-147">限制升級至相同主要版本與目前安裝的套件的版本。</span><span class="sxs-lookup"><span data-stu-id="4fc17-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="4fc17-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="4fc17-148">WhatIf</span></span> | <span data-ttu-id="4fc17-149">顯示執行命令，而不實際執行更新時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="4fc17-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="4fc17-150">這些參數都不接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="4fc17-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="4fc17-151">一般參數</span><span class="sxs-lookup"><span data-stu-id="4fc17-151">Common Parameters</span></span>

<span data-ttu-id="4fc17-152">`Update-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4fc17-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="4fc17-153">範例</span><span class="sxs-lookup"><span data-stu-id="4fc17-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
