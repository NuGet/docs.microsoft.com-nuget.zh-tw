---
title: NuGet 同步-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [同步處理-封裝 PowerShell] 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384899"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>同步-封裝（Visual Studio 中的套件管理員主控台）

*3.0 版 +;僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*

從指定的（或預設）專案取得已安裝封裝的版本，並將版本同步處理至方案中的其餘專案。

## <a name="syntax"></a>語法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | 具備要同步處理之封裝的識別碼。-Id 參數本身是選擇性的。 |
| IgnoreDependencies | 僅安裝此套件，而不是其相依性。 |
| ProjectName | 要同步處理封裝的專案，預設為預設專案。 |
| {2&gt;版本&lt;2} | 要同步處理的封裝版本，預設為目前安裝的版本。 |
| 原始程式檔 | 要搜尋之封裝來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前的資料夾。 如果省略，`Sync-Package` 會搜尋目前選取的封裝來源。 |
| IncludePrerelease | 包含同步處理中的發行前版本套件。 |
| FileConflictAction | 當系統要求覆寫或忽略專案所參考的現有檔案時，所要採取的動作。 可能的值為*Overwrite、Ignore、None、OverwriteAll*和 *（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 要使用的相依性套件版本，它可以是下列其中一項：<br/><ul><li>*最低*（預設值）：最低版本</li><li>*HighestPatch*：具有最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*：具有最低主要、最高次要、最高修補程式的版本</li><li>*最高*（不含參數的更新套件預設值）：最高版本</li></ul>您可以使用 `Nuget.Config` 檔案中的[`dependencyVersion`](../nuget-config-file.md#config-section)設定來設定預設值。 |
| Whatif | 顯示執行命令時，不會實際執行同步處理的情況。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Sync-Package` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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
