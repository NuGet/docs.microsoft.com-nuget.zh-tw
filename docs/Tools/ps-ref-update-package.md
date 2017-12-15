---
title: "NuGet 的更新套件的 PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b4aa92a9-ce47-4d23-ae51-d5683e08a9d5
description: "在 Visual Studio 中的 NuGet 封裝管理員主控台的更新套件的 PowerShell 命令的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考資料，更新套件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 71f5cd7061e0f765d8808db8a3798657a941ba14
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="0576b-104">更新套件 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="0576b-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0576b-105">*只能在[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="0576b-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0576b-106">更新為較新版本的封裝和其相依性或在專案中，所有封裝。</span><span class="sxs-lookup"><span data-stu-id="0576b-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="0576b-107">語法</span><span class="sxs-lookup"><span data-stu-id="0576b-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="0576b-108">在 NuGet 2.8 +`Update-Package`可用降級專案中現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="0576b-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="0576b-109">例如，如果您有安裝 Microsoft.AspNet.MVC 5.1.0-rc1，下列命令會降級 5.0.0 來：</span><span class="sxs-lookup"><span data-stu-id="0576b-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="0576b-110">2.7 及更早版本的 NuGet 提供的錯誤訊息已安裝較新版本。</span><span class="sxs-lookup"><span data-stu-id="0576b-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>

## <a name="parameters"></a><span data-ttu-id="0576b-111">參數</span><span class="sxs-lookup"><span data-stu-id="0576b-111">Parameters</span></span>

|  <span data-ttu-id="0576b-112">參數</span><span class="sxs-lookup"><span data-stu-id="0576b-112">Parameter</span></span> | <span data-ttu-id="0576b-113">說明</span><span class="sxs-lookup"><span data-stu-id="0576b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0576b-114">ID</span><span class="sxs-lookup"><span data-stu-id="0576b-114">Id</span></span> | <span data-ttu-id="0576b-115">要更新之封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0576b-115">The identifier of the package to update.</span></span> <span data-ttu-id="0576b-116">如果省略，更新所有封裝。</span><span class="sxs-lookup"><span data-stu-id="0576b-116">If omitted, updates all packages.</span></span> <span data-ttu-id="0576b-117">-Id 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="0576b-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="0576b-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="0576b-118">IgnoreDependencies</span></span> | <span data-ttu-id="0576b-119">略過更新封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="0576b-119">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="0576b-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="0576b-120">ProjectName</span></span> | <span data-ttu-id="0576b-121">包含要更新的封裝，將預設為所有專案的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="0576b-121">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="0576b-122">版本</span><span class="sxs-lookup"><span data-stu-id="0576b-122">Version</span></span> | <span data-ttu-id="0576b-123">要用於升級，將預設為最新版本的版本。</span><span class="sxs-lookup"><span data-stu-id="0576b-123">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="0576b-124">在 NuGet 3.0 + 版本的值必須是其中一個*Lowest、 最高、 HighestMinor*，或*HighestPatch* （相當於-安全）。</span><span class="sxs-lookup"><span data-stu-id="0576b-124">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="0576b-125">安全</span><span class="sxs-lookup"><span data-stu-id="0576b-125">Safe</span></span> | <span data-ttu-id="0576b-126">限制升級至具有相同主要和次要版本與目前已安裝封裝的唯一版本。</span><span class="sxs-lookup"><span data-stu-id="0576b-126">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="0576b-127">來源</span><span class="sxs-lookup"><span data-stu-id="0576b-127">Source</span></span> | <span data-ttu-id="0576b-128">要搜尋的封裝來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="0576b-128">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="0576b-129">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0576b-129">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="0576b-130">如果省略，`Uninstall-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="0576b-130">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="0576b-131">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="0576b-131">IncludePrerelease</span></span> | <span data-ttu-id="0576b-132">包含套件發行前版本的更新。</span><span class="sxs-lookup"><span data-stu-id="0576b-132">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="0576b-133">重新安裝</span><span class="sxs-lookup"><span data-stu-id="0576b-133">Reinstall</span></span> | <span data-ttu-id="0576b-134">Resintalls 封裝使用其目前已安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="0576b-134">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="0576b-135">請參閱[重新安裝及更新封裝](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="0576b-135">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="0576b-136">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="0576b-136">FileConflictAction</span></span> | <span data-ttu-id="0576b-137">當詢問您要覆寫或略過專案所參考的現有檔案時要採取動作。</span><span class="sxs-lookup"><span data-stu-id="0576b-137">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="0576b-138">可能的值為*覆寫，忽略、 None、 OverwriteAll*，和*IgnoreAll* （3.0 +）。</span><span class="sxs-lookup"><span data-stu-id="0576b-138">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="0576b-139">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="0576b-139">DependencyVersion</span></span> | <span data-ttu-id="0576b-140">若要使用，可以是下列其中之一的相依性套件的版本：</span><span class="sxs-lookup"><span data-stu-id="0576b-140">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="0576b-141">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="0576b-141">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="0576b-142">*HighestPatch*： 具有最低主要、 次要最低、 最高的修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="0576b-142">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="0576b-143">*HighestMinor*： 具有最低主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="0576b-143">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="0576b-144">*最高*（預設值更新套件不含任何參數）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="0576b-144">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="0576b-145">您可以設定預設值使用[ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="0576b-145">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="0576b-146">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="0576b-146">ToHighestPatch</span></span> | <span data-ttu-id="0576b-147">限制升級至只具有相同的次要版本與目前已安裝封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="0576b-147">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="0576b-148">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="0576b-148">ToHighestMinor</span></span> | <span data-ttu-id="0576b-149">限制升級至只具有相同主要版本與目前已安裝封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="0576b-149">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="0576b-150">WhatIf</span><span class="sxs-lookup"><span data-stu-id="0576b-150">WhatIf</span></span> | <span data-ttu-id="0576b-151">顯示執行命令，而不需實際執行更新時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="0576b-151">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="0576b-152">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="0576b-152">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="0576b-153">一般參數</span><span class="sxs-lookup"><span data-stu-id="0576b-153">Common Parameters</span></span>

<span data-ttu-id="0576b-154">`Update-Package`支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="0576b-154">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="0576b-155">範例</span><span class="sxs-lookup"><span data-stu-id="0576b-155">Examples</span></span>

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