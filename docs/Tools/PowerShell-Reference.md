---
title: NuGet PowerShell 參考
description: Visual Studio 中的 NuGet 封裝管理員主控台中可用的 PowerShell 命令的完整參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 455787d3c8701f5275ace4ed0dcb605213bfbf29
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="powershell-reference"></a>PowerShell 參考

Package Manager Console 提供下面所列的過特定的命令與 NuGet 互動的 Windows 上的 Visual Studio 中的 PowerShell 介面。 （[] 主控台不是目前可用在 Visual Studio for mac。）使用主控台的指引，請參閱[Package Manager Console](../tools/package-manager-console.md)主題。

> [!Tip]
> 所有的 PowerShell 命令僅與封裝耗用量。 建立和發佈封裝以外，封裝也可以是其他封裝的消費者，與沒有 PowerShell 命令。

> [!Important]
> 此處所列的命令專屬於在 Visual Studio 中，在 Package Manager Console 而不同[封裝管理模組命令](/powershell/module/packagemanagement/?view=powershell-6)可在一般的 PowerShell 環境中。 具體來說，每個環境有不適用於其他的命令，並在其特定的引數中，可能也不同命令具有相同名稱。 當使用 Visual Studio 中的封裝管理主控台，指令及引數有本文所述套用。

| 常見命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | 在專案中安裝封裝及其相依性。 | 全部 |
| [Update-Package](ps-ref-update-package.md) | 更新封裝和其相依性或在專案中的所有封裝。 | 全部 |
| [Find-Package](ps-ref-find-package.md) | 搜尋使用的封裝識別碼或關鍵字的封裝來源。 | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | 擷取安裝在本機儲存機制中，封裝的清單，或列出可用的封裝，從套件來源。 | 全部 |

| 第二個命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | 檢查專案的輸出路徑內的所有組件，並將繫結重新導向至`app.config`或`web.config`在需要時。 | 全部 |
| [Get-Project](ps-ref-get-project.md) | 顯示預設值或指定的專案相關資訊。 | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | 啟動預設瀏覽器中使用專案、 授權或指定之封裝的報表濫用 URL。 | 在 3.0 + 已被取代 |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | 登錄參數的命令，可讓您建立的常用的參數值的自訂擴充功能的 tab 鍵擴充。 | 全部 |
| [Sync-Package](ps-ref-sync-package.md) | 取得已安裝的版本封裝從指定專案和同步到解決方案中專案的其餘部分的版本。 | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | 移除封裝在專案中，選擇性地移除其相依性。 | 全部 |

如需這些命令主控台內的任何完整的詳細說明，只要有問題的命令名稱與執行下列命令：

```ps
Get-Help <command> -full
```

所有套件管理器主控台命令都支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):

- 偵錯
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 詳細資訊
- WarningAction
- WarningVariable

如需詳細資訊，請參閱[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 文件中。
