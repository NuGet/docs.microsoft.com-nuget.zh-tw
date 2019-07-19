---
title: NuGet PowerShell 參考
description: Visual Studio 中的 NuGet 套件管理員主控台所提供 PowerShell 命令的完整參考。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327925"
---
# <a name="powershell-reference"></a>PowerShell 參考

套件管理員主控台會在 Windows Visual Studio 內提供 PowerShell 介面, 以透過下列特定命令與 NuGet 互動。 (目前無法在 Visual Studio for Mac 中使用主控台)。如需使用主控台的指南, 請參閱[使用套件管理員主控台安裝和管理套件](../consume-packages/install-use-packages-powershell.md)主題。

> [!Tip]
> 所有 PowerShell 命令都只與套件耗用量相關。 除了封裝也可以是其他套件取用者的範圍之外, 沒有任何 PowerShell 命令與建立和發行封裝有關。

> [!Important]
> 此處所列的命令是 Visual Studio 中的套件管理員主控台所特有, 而且與一般 PowerShell 環境中可用的[套件管理模組命令](/powershell/module/packagemanagement/?view=powershell-6)不同。 具體而言, 每個環境都有其他無法使用的命令, 而且具有相同名稱的命令在其特定引數中也可能不同。 在 Visual Studio 中使用套件管理主控台時, 會套用此目前主題中記載的命令和引數。

| 一般命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | 將封裝及其相依性安裝到專案中。 | All |
| [Update-Package](ps-reference/ps-ref-update-package.md) | 更新封裝及其相依性, 或專案中的所有封裝。 | All |
| [Find-Package](ps-reference/ps-ref-find-package.md) | 使用套件識別碼或關鍵字搜尋封裝來源。 | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | 抓取本機存放庫中安裝的封裝清單, 或列出可從封裝來源取得的套件。 | All |

| 次要命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | 檢查項目輸出路徑中的所有元件, 並在必要時, 將系`app.config`結`web.config`重新導向新增至或。 | All |
| [Get-Project](ps-reference/ps-ref-get-project.md) | 顯示預設或指定專案的相關資訊。 | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | 使用指定封裝的 [專案]、[授權] 或 [報表濫用 URL] 來啟動預設瀏覽器。 | 3\.0 + 中已淘汰 |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | 為命令的參數註冊 tab 鍵擴充, 可讓您為常用的參數值建立自訂的擴充。 | All |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | 從指定的專案取得已安裝套件的版本, 並將版本同步處理至方案中的其餘專案。 | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | 移除專案中的封裝, 並選擇性地移除其相依性。 | All |

如需有關主控台內任何這些命令的完整詳細說明, 請執行下列命令, 並提出問題:

```ps
Get-Help <command> -full
```

所有套件管理員主控台命令都支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):

- 偵錯
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 詳細資訊
- WarningAction
- WarningVariable

如需詳細資訊, 請參閱 PowerShell 檔中的[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) 。
