---
title: NuGet 卸載-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [卸載-封裝 PowerShell] 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384411"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>卸載-封裝（Visual Studio 中的套件管理員主控台）

*本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 卸載-封裝命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

移除專案中的封裝，並選擇性地移除其相依性。 若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。

## <a name="syntax"></a>語法

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | 具備要卸載之封裝的識別碼。 -Id 參數本身是選擇性的。 |
| {2&gt;版本&lt;2} | 要卸載的封裝版本，預設為目前安裝的版本。 |
| RemoveDependencies | 卸載套件及其未使用的相依性。 也就是說，如果任何相依性有另一個依存于它的封裝，則會略過。 |
| ProjectName | 要從其中卸載封裝的專案，預設為預設專案。 |
| Force | 強制卸載套件，即使其他套件相依于封裝也一樣。 |
| Whatif | 顯示在執行命令時，不實際執行卸載所發生的情況。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Uninstall-Package` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
