---
title: NuGet Update-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Update-Package PowerShell 命令參考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 159817e56d978d6432e989d2027907c0d2445222
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777385"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Update-Package (封裝管理員主控台

*僅適用于 Windows 上 Visual Studio 的 [NuGet 封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內。*

將封裝及其相依性或專案中的所有封裝更新為較新的版本。

## <a name="syntax"></a>語法

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 + 中， `Update-Package` 可以用來將專案中的現有套件降級。 例如，如果您已安裝 5.1.0 rc1，則下列命令會將它降級為5.0.0：

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>參數

|  參數 | 描述 |
| --- | --- |
| 識別碼 | 要更新之封裝的識別碼。 如果省略，則會更新所有套件。 -Id 參數本身是選擇性的。 |
| IgnoreDependencies | 略過更新套件的相依性。 |
| ProjectName | 包含要更新之封裝的專案名稱，預設為所有專案。 |
| 版本 | 要用於升級的版本，預設為最新版本。 在 NuGet 3.0 + 中，版本值必須是 *最低、最高、HighestMinor* 或 *HighestPatch* 的其中一個 (相當於-Safe) 。 |
| 保險箱 | 將升級限制為只有與目前安裝的套件具有相同主要和次要版本的版本。 |
| 來源 | 要搜尋之套件來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。 如果省略，則會 `Update-Package` 搜尋目前選取的封裝來源。 |
| IncludePrerelease | 包含更新的發行前版本套件。 |
| 重新安裝 | 使用其目前安裝的版本 Resintalls 封裝。 請參閱 [重新安裝和更新套件](../../consume-packages/reinstalling-and-updating-packages.md)。 |
| FileConflictAction | 當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。 可能的值為 *覆寫、忽略、無、OverwriteAll* 和 *IgnoreAll* (3.0 +) 。 |
| DependencyVersion | 要使用之相依性套件的版本，它可以是下列其中一項：<br/><ul><li>*最低* (預設) ：最低版本</li><li>*HighestPatch*：最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*：最低主要、最小次要、最高修補程式的版本</li><li>不含參數的 Update-Package *最高* (預設值) ：最高版本</li></ul>您可以使用檔案中的設定來設定預設值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。 |
| ToHighestPatch | 相當於-Safe。 |
| ToHighestMinor | 將升級限制為只有與目前安裝的套件具有相同主要版本的版本。 |
| WhatIf | 顯示執行命令時會發生什麼事，而不實際執行更新。 |

這些參數都不接受管線輸入或萬用字元。

### <a name="common-parameters"></a>一般參數

`Update-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
