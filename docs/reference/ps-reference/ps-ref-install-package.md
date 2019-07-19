---
title: NuGet 安裝-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 Install-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327335"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio 套件管理員主控台)

*本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 安裝-Package 命令, 請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

將封裝及其相依性安裝到專案中。

## <a name="syntax"></a>語法

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 + 中`Install-Package` , 可以降級專案中的現有套件。 例如, 如果您已安裝 5.1.0-rc1, 下列命令會將它降級為 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>參數

| 參數 | 說明 |
| --- | --- |
| ID | 具備要安裝之封裝的識別碼。 (*3.0 +* )此識別碼可以是檔案`packages.config` `.nupkg`或檔案的路徑或 URL。 -Id 參數本身是選擇性的。 |
| IgnoreDependencies | 僅安裝此套件, 而不是其相依性。 |
| ProjectName | 要在其中安裝封裝的專案, 預設為預設專案。 |
| Source | 要搜尋之封裝來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前的資料夾。 如果省略, `Install-Package`則會搜尋目前選取的封裝來源。 |
| 版本 | 要安裝的封裝版本, 預設為最新版本。 |
| IncludePrerelease | 考慮安裝的發行前版本套件。 如果省略此參數, 則只會考慮穩定的封裝。 |
| FileConflictAction | 當系統要求覆寫或忽略專案所參考的現有檔案時, 所要採取的動作。 可能的值為*Overwrite、Ignore、None、OverwriteAll*和 *(3.0 +)* *IgnoreAll*。 |
| DependencyVersion | 要使用的相依性套件版本, 它可以是下列其中一項:<br/><ul><li>*最低*(預設值): 最低版本</li><li>*HighestPatch*: 具有最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*: 具有最低主要、最高次要、最高修補程式的版本</li><li>*最高*(不含參數的更新套件預設值): 最高版本</li></ul>您可以使用檔案[`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config`中的設定來設定預設值。 |
| WhatIf | 顯示執行命令時所發生的情況, 而不實際執行安裝。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Install-Package`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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
