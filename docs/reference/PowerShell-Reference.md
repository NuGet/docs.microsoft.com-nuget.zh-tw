---
title: NuGet PowerShell 參考
description: 您可以在 Visual Studio 中的 NuGet 封裝管理員主控台取得 PowerShell 命令的完整參考。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 4f8b42847cbc155393fe6d2afbe2e0857b619da3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236876"
---
# <a name="powershell-reference"></a>PowerShell 參考

封裝管理員主控台提供 Windows Visual Studio 內的 PowerShell 介面，可透過下列特定命令與 NuGet 互動。  (主控台目前無法在 Visual Studio for Mac 中使用。 ) 如需使用主控台的指南，請參閱 [使用封裝管理員主控台安裝及管理套件](../consume-packages/install-use-packages-powershell.md) 主題。

> [!Tip]
> 所有 PowerShell 命令都只與套件耗用量相關。 除了套件也可以是其他封裝的取用者之外，沒有任何 PowerShell 命令與建立和發佈套件有關。

> [!Important]
> 此處所列的命令是 Visual Studio 中的封裝管理員主控台特定的命令，不同于一般 PowerShell 環境中可用的 [套件管理模組命令](/powershell/module/packagemanagement/?view=powershell-6) 。 具體而言，每個環境都有其他無法使用的命令，而且具有相同名稱的命令在其特定引數中也可能不同。 當您在 Visual Studio 中使用套件管理主控台時，適用于本主題中記載的命令和引數適用于。

| 常見命令 | Description | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | 將封裝及其相依性安裝到專案中。 | 全部 |
| [Update-Package](ps-reference/ps-ref-update-package.md) | 更新封裝及其相依性，或專案中的所有套件。 | 全部 |
| [Find-Package](ps-reference/ps-ref-find-package.md) | 使用封裝識別碼或關鍵字搜尋封裝來源。 | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | 抓取本機存放庫中所安裝的套件清單，或列出可從套件來源取得的封裝。 | 全部 |

| 次要命令 | Description | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | 檢查項目輸出路徑內的所有元件，並將系結重新導向加入至 `app.config` 或 `web.config` 需要的位置。 | 全部 |
| [Get-Project](ps-reference/ps-ref-get-project.md) | 顯示預設或指定專案的相關資訊。 | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | 使用指定封裝的專案、授權或報告濫用 URL 來啟動預設瀏覽器。 | 已在 3.0 + 中淘汰 |
| [註冊-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | 註冊命令參數的索引標籤展開，可讓您建立常用參數值的自訂擴充。 | 全部 |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | 從指定的專案取得已安裝套件的版本，並將版本同步處理至方案中的其餘專案。 | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | 移除專案中的封裝，並選擇性地移除其相依性。 | 全部 |

如需主控台內任何這些命令的完整詳細說明，請使用下列命令名稱來執行下列命令：

```ps
Get-Help <command> -full
```

所有封裝管理員主控台命令都支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：

- 偵錯
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 「詳細資訊」
- WarningAction
- WarningVariable

如需詳細資訊，請參閱 PowerShell 檔中的 [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) 。