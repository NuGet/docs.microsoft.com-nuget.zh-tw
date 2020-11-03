---
title: NuGet Install-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Install-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5bda888e0fb526faca79e88da93b0ceb9aff5348
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237201"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Install-Package (封裝管理員主控台

*本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Install-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

將封裝及其相依性安裝到專案中。

## <a name="syntax"></a>Syntax

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 + 中， `Install-Package` 可以在您的專案中降級現有的封裝。 例如，如果您已安裝 5.1.0 rc1，則下列命令會將它降級為5.0.0：

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>參數

| 參數 | Description |
| --- | --- |
| Id |  (需要) 要安裝的封裝識別碼。  ( *3.0 +* ) 識別碼可以是檔案或檔案的路徑或 URL `packages.config` `.nupkg` 。 -Id 參數本身是選擇性的。 |
| IgnoreDependencies | 只安裝此套件，而不安裝其相依性。 |
| ProjectName | 要在其中安裝封裝的專案，預設為預設專案。 |
| 來源 | 要搜尋之套件來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。 如果省略，則會 `Install-Package` 搜尋目前選取的封裝來源。 |
| 版本 | 要安裝的套件版本，預設為最新版本。 |
| IncludePrerelease | 考慮安裝的發行前版本套件。 若省略此步驟，則系統只會考慮穩定的封裝。 |
| FileConflictAction | 當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。 可能的值為 *覆寫、忽略、無、OverwriteAll* 和 *(3.0 +)* *IgnoreAll* 。 |
| DependencyVersion | 要使用之相依性套件的版本，它可以是下列其中一項：<br/><ul><li>*最低* (預設) ：最低版本</li><li>*HighestPatch* ：最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor* ：最低主要、最小次要、最高修補程式的版本</li><li>不含參數的 Update-Package *最高* (預設值) ：最高版本</li></ul>您可以使用檔案中的設定來設定預設值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。 |
| WhatIf | 顯示執行命令時會發生什麼事，而不實際執行安裝。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Install-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

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