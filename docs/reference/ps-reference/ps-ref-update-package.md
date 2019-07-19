---
title: NuGet 更新-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的更新套件 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327265"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Visual Studio 套件管理員主控台)

*只能在 Windows 上 Visual Studio 的[NuGet 套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中使用。*

將封裝及其相依性, 或專案中的所有封裝更新為較新的版本。

## <a name="syntax"></a>語法

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 + 中`Update-Package` , 可以用來降級專案中的現有套件。 例如, 如果您已安裝 5.1.0-rc1, 下列命令會將它降級為 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>參數

|  參數 | 描述 |
| --- | --- |
| ID | 要更新之封裝的識別碼。 如果省略, 則會更新所有封裝。 -Id 參數本身是選擇性的。 |
| IgnoreDependencies | 略過更新套件的相依性。 |
| ProjectName | 包含要更新之封裝的專案名稱, 預設為所有專案。 |
| 版本 | 要用於升級的版本, 預設為最新版本。 在 NuGet 3.0 + 中, [版本] 值必須是 [*最低]、[最高]、[HighestMinor*] 或 [ *HighestPatch* ] (相當於安全) 的其中一個。 |
| 進入 | 只會將升級限制為與目前安裝的套件具有相同主要和次要版本的版本。 |
| Source | 要搜尋之封裝來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前的資料夾。 如果省略, `Update-Package`則會搜尋目前選取的封裝來源。 |
| IncludePrerelease | 包含更新的發行前版本套件。 |
| 重新安裝 | 使用目前安裝的版本來 Resintalls 套件。 請參閱[重新安裝和更新套件](../../consume-packages/reinstalling-and-updating-packages.md)。 |
| FileConflictAction | 當系統要求覆寫或忽略專案所參考的現有檔案時, 所要採取的動作。 可能的值為*Overwrite、Ignore、None、OverwriteAll*和*IgnoreAll* (3.0 +)。 |
| DependencyVersion | 要使用的相依性套件版本, 它可以是下列其中一項:<br/><ul><li>*最低*(預設值): 最低版本</li><li>*HighestPatch*: 具有最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*: 具有最低主要、最高次要、最高修補程式的版本</li><li>*最高*(不含參數的更新套件預設值): 最高版本</li></ul>您可以使用檔案[`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config`中的設定來設定預設值。 |
| ToHighestPatch | 相當於-Safe。 |
| ToHighestMinor | 只會將升級限制為與目前安裝之套件具有相同主要版本的版本。 |
| WhatIf | 顯示執行命令時所發生的情況, 而不實際執行更新。 |

這些參數都不接受管線輸入或萬用字元。

### <a name="common-parameters"></a>一般參數

`Update-Package`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

### <a name="examples"></a>範例

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
