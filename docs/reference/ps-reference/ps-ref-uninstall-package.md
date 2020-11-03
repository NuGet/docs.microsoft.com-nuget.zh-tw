---
title: NuGet Uninstall-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Uninstall-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237123"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Uninstall-Package (封裝管理員主控台

*本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Uninstall-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

移除專案中的封裝，並選擇性地移除其相依性。 若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

若是其他封裝與此封裝有相依性，則必須指定 –Force 選項，否則此命令將會失敗。

## <a name="parameters"></a>參數

| 參數 | Description |
| --- | --- |
| Id |  (需要) 要卸載之套件的識別碼。 -Id 參數本身是選擇性的。 |
| 版本 | 要卸載的套件版本，預設為目前安裝的版本。 |
| RemoveDependencies | 卸載封裝及其未使用的相依性。 也就是說，如果任何相依性有另一個相依的封裝，則會略過它。 |
| ProjectName | 要從其中卸載封裝的專案，預設為預設專案。 |
| Force | 強制卸載套件，即使其他封裝相依于封裝也是如此。 |
| WhatIf | 顯示執行命令時會發生什麼事，而不實際執行卸載。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Uninstall-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```