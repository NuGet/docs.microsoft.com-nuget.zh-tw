---
title: NuGet 的同步處理封裝 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台中的同步處理封裝 PowerShell 命令的參考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 92f0d7490dea57a69b5a5cb3cb7165f665f60d44
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818101"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio 套件管理員主控台)

*3.0 +; 版本只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*

取得從安裝套件的版本指定 （或預設） 專案，並同步處理其餘部分的方案中專案的版本。

## <a name="syntax"></a>語法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | （必要）要同步處理之封裝的識別碼。-Id 參數是選擇性的。 |
| IgnoreDependencies | 安裝僅此套件不其相依性。 |
| ProjectName | 要同步處理預設為預設專案，從封裝的專案。 |
| 版本 | 若要同步，封裝版本預設為目前安裝的版本。 |
| 原始程式檔 | 要搜尋的封裝來源 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Sync-Package`搜尋目前選取的套件來源。 |
| IncludePrerelease | 在同步處理包含套件發行前版本。 |
| FileConflictAction | 當詢問您要覆寫或略過專案所參考的現有檔案時要採取動作。 可能的值為*覆寫，忽略、 None、 OverwriteAll*，和 *（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 若要使用，可以是下列其中之一的相依性套件的版本：<br/><ul><li>*最低*（預設值）： 最低版本</li><li>*HighestPatch*： 具有最低主要、 次要最低、 最高的修補程式的版本</li><li>*HighestMinor*： 具有最低主要版本、 最小、 最高的修補程式</li><li>*最高*（預設值更新套件不含任何參數）： 最高的版本</li></ul>您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。 |
| WhatIf | 顯示執行命令，而不需實際執行同步處理時，會發生什麼情況。 |

這些參數接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Sync-Package` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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
