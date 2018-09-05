---
title: NuGet 解除安裝套件的 PowerShell 參考
description: 在 NuGet 套件管理員主控台中，在 Visual Studio 中的封裝解除安裝 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551639"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio 套件管理員主控台)

*本主題描述內的命令[NuGet 套件管理員主控台](package-manager-console.md)在 Windows 上的 Visual Studio 中。一般的 PowerShell 封裝解除安裝命令中，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

從專案中，選擇性地移除其相依性移除封裝。 如果其他套件相依於此套件，則命令會失敗，除非選項指定 – Force。

## <a name="syntax"></a>語法

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

如果其他套件相依於此套件，則命令會失敗，除非選項指定 – Force。

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | （必要）若要解除安裝封裝的識別碼。 -識別碼是選擇性參數本身。 |
| 版本 | 若要解除安裝，封裝的版本預設為目前安裝的版本。 |
| RemoveDependencies | 解除安裝封裝和其未使用的相依性。 也就是說，如果任何相依性有相依於它的另一個封裝，它會略過。 |
| ProjectName | 要從中解除安裝套件，將預設為預設專案的專案。 |
| 強制 | 強制解除安裝，封裝，即使其他封裝依存於此。 |
| WhatIf | 顯示執行命令，而不實際執行解除安裝時，會發生什麼情況。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Uninstall-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
