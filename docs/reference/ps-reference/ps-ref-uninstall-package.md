---
title: NuGet 卸載-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [卸載-封裝 PowerShell] 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327275"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio 套件管理員主控台)

*本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 卸載-封裝命令, 請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

移除專案中的封裝, 並選擇性地移除其相依性。 如果其他封裝相依于此封裝, 除非指定– Force 選項, 否則此命令將會失敗。

## <a name="syntax"></a>語法

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

如果其他封裝相依于此封裝, 除非指定– Force 選項, 否則此命令將會失敗。

## <a name="parameters"></a>參數

| 參數 | 說明 |
| --- | --- |
| ID | 具備要卸載之封裝的識別碼。 -Id 參數本身是選擇性的。 |
| 版本 | 要卸載的封裝版本, 預設為目前安裝的版本。 |
| RemoveDependencies | 卸載套件及其未使用的相依性。 也就是說, 如果任何相依性有另一個依存于它的封裝, 則會略過。 |
| ProjectName | 要從其中卸載封裝的專案, 預設為預設專案。 |
| 使 | 強制卸載套件, 即使其他套件相依于封裝也一樣。 |
| WhatIf | 顯示在執行命令時, 不實際執行卸載所發生的情況。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Uninstall-Package`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
