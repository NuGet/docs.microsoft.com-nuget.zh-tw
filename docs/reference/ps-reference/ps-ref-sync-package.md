---
title: NuGet Sync-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Sync-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238045"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Sync-Package (封裝管理員主控台

*3.0 版 +;只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*

從指定的 (或預設) 專案取得已安裝套件的版本，並將版本同步處理至方案中的其餘專案。

## <a name="syntax"></a>語法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | Description |
| --- | --- |
| Id |  (需要) 要同步的封裝識別碼。-Id 參數本身是選擇性的。 |
| IgnoreDependencies | 只安裝此套件，而不安裝其相依性。 |
| ProjectName | 要同步處理封裝的專案，預設為預設專案。 |
| 版本 | 要同步處理的封裝版本，預設為目前安裝的版本。 |
| 來源 | 要搜尋之套件來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。 如果省略，則會 `Sync-Package` 搜尋目前選取的封裝來源。 |
| IncludePrerelease | 在同步處理中包含發行前版本套件。 |
| FileConflictAction | 當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。 可能的值為 *覆寫、忽略、無、OverwriteAll* 和 *(3.0 +)* *IgnoreAll* 。 |
| DependencyVersion | 要使用之相依性套件的版本，它可以是下列其中一項：<br/><ul><li>*最低* (預設) ：最低版本</li><li>*HighestPatch* ：最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor* ：最低主要、最小次要、最高修補程式的版本</li><li>不含參數的 Update-Package *最高* (預設值) ：最高版本</li></ul>您可以使用檔案中的設定來設定預設值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。 |
| WhatIf | 顯示執行命令時所發生的狀況，而不實際執行同步處理。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Sync-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```