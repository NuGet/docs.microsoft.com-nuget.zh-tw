---
title: NuGet Install-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Install-Package PowerShell 命令參考。
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 110b41e830636d60741b14292c17840aa5a63dfd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777442"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d4293-103">Visual Studio) 中的 Install-Package (封裝管理員主控台</span><span class="sxs-lookup"><span data-stu-id="d4293-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d4293-104">*本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Install-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*</span><span class="sxs-lookup"><span data-stu-id="d4293-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d4293-105">將封裝及其相依性安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="d4293-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="d4293-106">語法</span><span class="sxs-lookup"><span data-stu-id="d4293-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d4293-107">在 NuGet 2.8 + 中， `Install-Package` 可以在您的專案中降級現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="d4293-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="d4293-108">例如，如果您已安裝 5.1.0 rc1，則下列命令會將它降級為5.0.0：</span><span class="sxs-lookup"><span data-stu-id="d4293-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="d4293-109">參數</span><span class="sxs-lookup"><span data-stu-id="d4293-109">Parameters</span></span>

| <span data-ttu-id="d4293-110">參數</span><span class="sxs-lookup"><span data-stu-id="d4293-110">Parameter</span></span> | <span data-ttu-id="d4293-111">描述</span><span class="sxs-lookup"><span data-stu-id="d4293-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4293-112">識別碼</span><span class="sxs-lookup"><span data-stu-id="d4293-112">Id</span></span> | <span data-ttu-id="d4293-113"> (需要) 要安裝的封裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="d4293-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="d4293-114"> (*3.0 +*) 識別碼可以是檔案或檔案的路徑或 URL `packages.config` `.nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="d4293-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="d4293-115">-Id 參數本身是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="d4293-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d4293-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="d4293-116">IgnoreDependencies</span></span> | <span data-ttu-id="d4293-117">只安裝此套件，而不安裝其相依性。</span><span class="sxs-lookup"><span data-stu-id="d4293-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="d4293-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d4293-118">ProjectName</span></span> | <span data-ttu-id="d4293-119">要在其中安裝封裝的專案，預設為預設專案。</span><span class="sxs-lookup"><span data-stu-id="d4293-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="d4293-120">來源</span><span class="sxs-lookup"><span data-stu-id="d4293-120">Source</span></span> | <span data-ttu-id="d4293-121">要搜尋之套件來源的 URL 或資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="d4293-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="d4293-122">本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="d4293-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d4293-123">如果省略，則會 `Install-Package` 搜尋目前選取的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="d4293-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="d4293-124">版本</span><span class="sxs-lookup"><span data-stu-id="d4293-124">Version</span></span> | <span data-ttu-id="d4293-125">要安裝的套件版本，預設為最新版本。</span><span class="sxs-lookup"><span data-stu-id="d4293-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d4293-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d4293-126">IncludePrerelease</span></span> | <span data-ttu-id="d4293-127">考慮安裝的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="d4293-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="d4293-128">若省略此步驟，則系統只會考慮穩定的封裝。</span><span class="sxs-lookup"><span data-stu-id="d4293-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="d4293-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d4293-129">FileConflictAction</span></span> | <span data-ttu-id="d4293-130">當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="d4293-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d4293-131">可能的值為 *覆寫、忽略、無、OverwriteAll* 和 *(3.0 +)* *IgnoreAll*。</span><span class="sxs-lookup"><span data-stu-id="d4293-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="d4293-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="d4293-132">DependencyVersion</span></span> | <span data-ttu-id="d4293-133">要使用之相依性套件的版本，它可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="d4293-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="d4293-134">*最低* (預設) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="d4293-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="d4293-135">*HighestPatch*：最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="d4293-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="d4293-136">*HighestMinor*：最低主要、最小次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="d4293-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="d4293-137">不含參數的 Update-Package *最高* (預設值) ：最高版本</span><span class="sxs-lookup"><span data-stu-id="d4293-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="d4293-138">您可以使用檔案中的設定來設定預設值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="d4293-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="d4293-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d4293-139">WhatIf</span></span> | <span data-ttu-id="d4293-140">顯示執行命令時會發生什麼事，而不實際執行安裝。</span><span class="sxs-lookup"><span data-stu-id="d4293-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="d4293-141">這些參數都不接受管線輸入或萬用字元。</span><span class="sxs-lookup"><span data-stu-id="d4293-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d4293-142">一般參數</span><span class="sxs-lookup"><span data-stu-id="d4293-142">Common Parameters</span></span>

<span data-ttu-id="d4293-143">`Install-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="d4293-143">`Install-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d4293-144">範例</span><span class="sxs-lookup"><span data-stu-id="d4293-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```