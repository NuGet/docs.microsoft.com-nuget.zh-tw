---
title: NuGet Update-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Update-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: af918d11e8f976be962d52084c5eda4d53e382c6
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238032"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e63f7-103">Visual Studio) 中的 Update-Package (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="e63f7-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e63f7-104">*僅適用于 Windows 上 Visual Studio 的 [NuGet 封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內。*</span><span class="sxs-lookup"><span data-stu-id="e63f7-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e63f7-105">將封裝及其相依性或專案中的所有封裝更新為較新的版本。</span><span class="sxs-lookup"><span data-stu-id="e63f7-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="e63f7-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="e63f7-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e63f7-107">在 NuGet 2.8 + 中， `Update-Package` 可以用來將專案中的現有套件降級。</span><span class="sxs-lookup"><span data-stu-id="e63f7-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="e63f7-108">例如，如果您已安裝 5.1.0 rc1，則下列命令會將它降級為5.0.0：</span><span class="sxs-lookup"><span data-stu-id="e63f7-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="e63f7-109">參數</span><span class="sxs-lookup"><span data-stu-id="e63f7-109">Parameters</span></span>

|  <span data-ttu-id="e63f7-110">參數</span><span class="sxs-lookup"><span data-stu-id="e63f7-110">Parameter</span></span> | <span data-ttu-id="e63f7-111">Description</span><span class="sxs-lookup"><span data-stu-id="e63f7-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e63f7-112">Id</span><span class="sxs-lookup"><span data-stu-id="e63f7-112">Id</span></span> | <span data-ttu-id="e63f7-113">要更新之封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e63f7-113">The identifier of the package to update.</span></span> <span data-ttu-id="e63f7-114">如果省略，則會更新所有套件。</span><span class="sxs-lookup"><span data-stu-id="e63f7-114">If omitted, updates all packages.</span></span> <span data-ttu-id="e63f7-115">-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="e63f7-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e63f7-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e63f7-116">IgnoreDependencies</span></span> | <span data-ttu-id="e63f7-117">略過更新套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="e63f7-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="e63f7-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e63f7-118">ProjectName</span></span> | <span data-ttu-id="e63f7-119">包含要更新之封裝的專案名稱，預設為所有專案。</span><span class="sxs-lookup"><span data-stu-id="e63f7-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="e63f7-120">版本</span><span class="sxs-lookup"><span data-stu-id="e63f7-120">Version</span></span> | <span data-ttu-id="e63f7-121">要用於升級的版本，預設為最新版本。</span><span class="sxs-lookup"><span data-stu-id="e63f7-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="e63f7-122">在 NuGet 3.0 + 中，版本值必須是 *最低、最高、HighestMinor* 或 *HighestPatch* 的其中一個 (相當於-Safe) 。</span><span class="sxs-lookup"><span data-stu-id="e63f7-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor* , or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="e63f7-123">保險箱</span><span class="sxs-lookup"><span data-stu-id="e63f7-123">Safe</span></span> | <span data-ttu-id="e63f7-124">將升級限制為只有與目前安裝的套件具有相同主要和次要版本的版本。</span><span class="sxs-lookup"><span data-stu-id="e63f7-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="e63f7-125">來源</span><span class="sxs-lookup"><span data-stu-id="e63f7-125">Source</span></span> | <span data-ttu-id="e63f7-126">要搜尋之套件來源的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="e63f7-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e63f7-127">本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="e63f7-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e63f7-128">如果省略，則會 `Update-Package` 搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="e63f7-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e63f7-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e63f7-129">IncludePrerelease</span></span> | <span data-ttu-id="e63f7-130">包含更新的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="e63f7-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="e63f7-131">重新安裝</span><span class="sxs-lookup"><span data-stu-id="e63f7-131">Reinstall</span></span> | <span data-ttu-id="e63f7-132">使用其目前安裝的版本 Resintalls 封裝。</span><span class="sxs-lookup"><span data-stu-id="e63f7-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="e63f7-133">請參閱 [重新安裝和更新套件](../../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="e63f7-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="e63f7-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e63f7-134">FileConflictAction</span></span> | <span data-ttu-id="e63f7-135">當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="e63f7-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e63f7-136">可能的值為 *覆寫、忽略、無、OverwriteAll* 和 *IgnoreAll* (3.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="e63f7-136">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="e63f7-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e63f7-137">DependencyVersion</span></span> | <span data-ttu-id="e63f7-138">要使用之相依性套件的版本，它可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="e63f7-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e63f7-139">*最低* (預設) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="e63f7-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e63f7-140">*HighestPatch* ：最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="e63f7-140">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e63f7-141">*HighestMinor* ：最低主要、最小次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="e63f7-141">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e63f7-142">不含參數的 Update-Package *最高* (預設值) ：最高版本</span><span class="sxs-lookup"><span data-stu-id="e63f7-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e63f7-143">您可以使用檔案中的設定來設定預設值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="e63f7-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e63f7-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="e63f7-144">ToHighestPatch</span></span> | <span data-ttu-id="e63f7-145">相當於-Safe。</span><span class="sxs-lookup"><span data-stu-id="e63f7-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="e63f7-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="e63f7-146">ToHighestMinor</span></span> | <span data-ttu-id="e63f7-147">將升級限制為只有與目前安裝的套件具有相同主要版本的版本。</span><span class="sxs-lookup"><span data-stu-id="e63f7-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="e63f7-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e63f7-148">WhatIf</span></span> | <span data-ttu-id="e63f7-149">顯示執行命令時會發生什麼事，而不實際執行更新。</span><span class="sxs-lookup"><span data-stu-id="e63f7-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="e63f7-150">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="e63f7-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="e63f7-151">一般參數</span><span class="sxs-lookup"><span data-stu-id="e63f7-151">Common Parameters</span></span>

<span data-ttu-id="e63f7-152">`Update-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e63f7-152">`Update-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="e63f7-153">範例</span><span class="sxs-lookup"><span data-stu-id="e63f7-153">Examples</span></span>

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
