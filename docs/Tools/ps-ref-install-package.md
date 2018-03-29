---
title: NuGet 安裝套件的 PowerShell 參考 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台的安裝套件的 PowerShell 命令的參考。
keywords: NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考，安裝套件
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99c965c2f8c12c7a59ee48e270172b719c1482ea
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="36177-104">安裝套件 （在 Visual Studio 中的封裝管理員主控台）</span><span class="sxs-lookup"><span data-stu-id="36177-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="36177-105">*本主題描述內的命令[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。一般 PowerShell 安裝套件的命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="36177-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="36177-106">在專案中安裝封裝及其相依性。</span><span class="sxs-lookup"><span data-stu-id="36177-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="36177-107">語法</span><span class="sxs-lookup"><span data-stu-id="36177-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="36177-108">在 NuGet 2.8 +`Install-Package`降級專案中現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="36177-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="36177-109">例如，如果您有安裝 Microsoft.AspNet.MVC 5.1.0-rc1，下列命令會降級 5.0.0 來：</span><span class="sxs-lookup"><span data-stu-id="36177-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="36177-110">參數</span><span class="sxs-lookup"><span data-stu-id="36177-110">Parameters</span></span>

| <span data-ttu-id="36177-111">參數</span><span class="sxs-lookup"><span data-stu-id="36177-111">Parameter</span></span> | <span data-ttu-id="36177-112">描述</span><span class="sxs-lookup"><span data-stu-id="36177-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36177-113">ID</span><span class="sxs-lookup"><span data-stu-id="36177-113">Id</span></span> | <span data-ttu-id="36177-114">（必要）若要安裝封裝的識別碼。</span><span class="sxs-lookup"><span data-stu-id="36177-114">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="36177-115">(*3.0 +*) 路徑或 URL，此識別碼可以是`packages.config`檔案或`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="36177-115">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="36177-116">-Id 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="36177-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="36177-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="36177-117">IgnoreDependencies</span></span> | <span data-ttu-id="36177-118">安裝僅此套件不其相依性。</span><span class="sxs-lookup"><span data-stu-id="36177-118">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="36177-119">ProjectName</span><span class="sxs-lookup"><span data-stu-id="36177-119">ProjectName</span></span> | <span data-ttu-id="36177-120">要安裝套件，將預設專案的預設專案。</span><span class="sxs-lookup"><span data-stu-id="36177-120">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="36177-121">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="36177-121">Source</span></span> | <span data-ttu-id="36177-122">要搜尋的封裝來源 URL 或資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="36177-122">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="36177-123">本機資料夾路徑可以是絕對的或相對於目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="36177-123">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="36177-124">如果省略，`Install-Package`搜尋目前選取的套件來源。</span><span class="sxs-lookup"><span data-stu-id="36177-124">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="36177-125">版本</span><span class="sxs-lookup"><span data-stu-id="36177-125">Version</span></span> | <span data-ttu-id="36177-126">若要安裝，封裝版本預設為最新版本。</span><span class="sxs-lookup"><span data-stu-id="36177-126">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="36177-127">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="36177-127">IncludePrerelease</span></span> | <span data-ttu-id="36177-128">考慮套件發行前版本的安裝。</span><span class="sxs-lookup"><span data-stu-id="36177-128">Considers prerelease packages for the install.</span></span> <span data-ttu-id="36177-129">如果省略，則會視為穩定的套件。</span><span class="sxs-lookup"><span data-stu-id="36177-129">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="36177-130">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="36177-130">FileConflictAction</span></span> | <span data-ttu-id="36177-131">當詢問您要覆寫或略過專案所參考的現有檔案時要採取動作。</span><span class="sxs-lookup"><span data-stu-id="36177-131">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="36177-132">可能的值為*覆寫，忽略、 None、 OverwriteAll*，和*（3.0 +）* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="36177-132">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="36177-133">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="36177-133">DependencyVersion</span></span> | <span data-ttu-id="36177-134">若要使用，可以是下列其中之一的相依性套件的版本：</span><span class="sxs-lookup"><span data-stu-id="36177-134">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="36177-135">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="36177-135">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="36177-136">*HighestPatch*： 具有最低主要、 次要最低、 最高的修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="36177-136">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="36177-137">*HighestMinor*： 具有最低主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="36177-137">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="36177-138">*最高*（預設值更新套件不含任何參數）： 最高的版本</span><span class="sxs-lookup"><span data-stu-id="36177-138">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="36177-139">您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="36177-139">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="36177-140">WhatIf</span><span class="sxs-lookup"><span data-stu-id="36177-140">WhatIf</span></span> | <span data-ttu-id="36177-141">顯示執行命令，而不需實際執行安裝時，會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="36177-141">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="36177-142">這些參數接受管線輸入或萬用字元的字元。</span><span class="sxs-lookup"><span data-stu-id="36177-142">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="36177-143">一般參數</span><span class="sxs-lookup"><span data-stu-id="36177-143">Common Parameters</span></span>

<span data-ttu-id="36177-144">`Install-Package` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="36177-144">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="36177-145">範例</span><span class="sxs-lookup"><span data-stu-id="36177-145">Examples</span></span>

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
