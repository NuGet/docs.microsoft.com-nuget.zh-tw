---
title: NuGet 安裝套件的 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台的安裝套件的 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842505"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="139dc-103">Install-Package (Visual Studio 套件管理員主控台)</span><span class="sxs-lookup"><span data-stu-id="139dc-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="139dc-104">*本主題描述內的命令[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。一般的 PowerShell Install-package 命令，請參閱 < [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="139dc-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="139dc-105">會封裝及其相依性安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="139dc-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="139dc-106">語法</span><span class="sxs-lookup"><span data-stu-id="139dc-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="139dc-107">Nuget 2.8 +`Install-Package`降級您的專案中現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="139dc-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="139dc-108">比方說，如果您有安裝 Microsoft.AspNet.MVC 5.1.0-rc1，下列命令會降級至 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="139dc-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="139dc-109">參數</span><span class="sxs-lookup"><span data-stu-id="139dc-109">Parameters</span></span>

| <span data-ttu-id="139dc-110">參數</span><span class="sxs-lookup"><span data-stu-id="139dc-110">Parameter</span></span> | <span data-ttu-id="139dc-111">說明</span><span class="sxs-lookup"><span data-stu-id="139dc-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="139dc-112">ID</span><span class="sxs-lookup"><span data-stu-id="139dc-112">Id</span></span> | <span data-ttu-id="139dc-113">（必要）若要安裝封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="139dc-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="139dc-114">(*3.0 +* ) 的識別碼可以是路徑或 URL`packages.config`檔案或`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="139dc-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="139dc-115">-識別碼是選擇性參數本身。</span><span class="sxs-lookup"><span data-stu-id="139dc-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="139dc-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="139dc-116">IgnoreDependencies</span></span> | <span data-ttu-id="139dc-117">安裝只需將此套件不及其相依性。</span><span class="sxs-lookup"><span data-stu-id="139dc-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="139dc-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="139dc-118">ProjectName</span></span> | <span data-ttu-id="139dc-119">要安裝套件，將預設為預設專案的專案。</span><span class="sxs-lookup"><span data-stu-id="139dc-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="139dc-120">Source</span><span class="sxs-lookup"><span data-stu-id="139dc-120">Source</span></span> | <span data-ttu-id="139dc-121">要搜尋的套件來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="139dc-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="139dc-122">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="139dc-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="139dc-123">如果省略，`Install-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="139dc-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="139dc-124">版本</span><span class="sxs-lookup"><span data-stu-id="139dc-124">Version</span></span> | <span data-ttu-id="139dc-125">若要安裝，封裝的版本預設為最新版本。</span><span class="sxs-lookup"><span data-stu-id="139dc-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="139dc-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="139dc-126">IncludePrerelease</span></span> | <span data-ttu-id="139dc-127">會視為發行前版本套件進行安裝。</span><span class="sxs-lookup"><span data-stu-id="139dc-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="139dc-128">如果省略，則會被視為穩定的封裝。</span><span class="sxs-lookup"><span data-stu-id="139dc-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="139dc-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="139dc-129">FileConflictAction</span></span> | <span data-ttu-id="139dc-130">當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="139dc-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="139dc-131">可能的值為*覆寫，忽略、 None、 OverwriteAll*，並 *（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="139dc-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="139dc-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="139dc-132">DependencyVersion</span></span> | <span data-ttu-id="139dc-133">若要使用，相依性套件可以是下列其中一種版本：</span><span class="sxs-lookup"><span data-stu-id="139dc-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="139dc-134">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="139dc-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="139dc-135">*HighestPatch*： 具有最低的主要、 次要最低、 最高的修補程式版本</span><span class="sxs-lookup"><span data-stu-id="139dc-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="139dc-136">*HighestMinor*： 具有最低的主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="139dc-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="139dc-137">*最高*（預設值更新套件不含任何參數）： 最高版本</span><span class="sxs-lookup"><span data-stu-id="139dc-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="139dc-138">您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="139dc-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="139dc-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="139dc-139">WhatIf</span></span> | <span data-ttu-id="139dc-140">顯示執行命令，而不實際執行安裝時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="139dc-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="139dc-141">這些參數都不接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="139dc-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="139dc-142">一般參數</span><span class="sxs-lookup"><span data-stu-id="139dc-142">Common Parameters</span></span>

<span data-ttu-id="139dc-143">`Install-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="139dc-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="139dc-144">範例</span><span class="sxs-lookup"><span data-stu-id="139dc-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
