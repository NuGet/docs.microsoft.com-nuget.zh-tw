---
title: 同步處理-Nuget PowerShell 參考
description: 在 NuGet 套件管理員主控台中，在 Visual Studio 中的同步處理封裝的 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842254"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio 套件管理員主控台)

*版本 3.0 + 中;只能在[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

取得從已安裝封裝的版本指定 （或預設） 專案，並同步處理到其他方案中專案的版本。

## <a name="syntax"></a>語法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | （必要）要同步處理之封裝的識別碼。-識別碼是選擇性參數本身。 |
| IgnoreDependencies | 安裝只需將此套件不及其相依性。 |
| ProjectName | 要同步處理預設為預設專案，封裝的專案。 |
| 版本 | 若要同步，封裝的版本預設為目前安裝的版本。 |
| Source | 要搜尋的套件來源 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Sync-Package`搜尋目前選取的套件來源。 |
| IncludePrerelease | 包含發行前版本套件中的同步處理。 |
| FileConflictAction | 當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。 可能的值為*覆寫，忽略、 None、 OverwriteAll*，並 *（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 若要使用，相依性套件可以是下列其中一種版本：<br/><ul><li>*最低*（預設值）： 最低版本</li><li>*HighestPatch*： 具有最低的主要、 次要最低、 最高的修補程式版本</li><li>*HighestMinor*： 具有最低的主要版本、 最小、 最高的修補程式</li><li>*最高*（預設值更新套件不含任何參數）： 最高版本</li></ul>您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。 |
| WhatIf | 顯示執行命令，而不實際執行的同步處理時，會發生什麼情況。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Sync-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。

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
