---
title: NuGet PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台中可用的 PowerShell 命令來完成的參考。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 425ba736eba4609ebd6b5185ae3f1f976ab07a67
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842569"
---
# <a name="powershell-reference"></a>PowerShell 參考

套件管理員主控台提供如下所示的 PowerShell 介面，以透過特定的命令與 NuGet 互動的 Windows 上的 Visual Studio 內。 （[] 主控台不是目前可在 Visual Studio for mac）如需使用主控台的指南，請參閱[安裝和管理套件使用 Package Manager Console](../tools/package-manager-console.md)主題。

> [!Tip]
> 所有的 PowerShell 命令只與套件耗用量。 建立及發行套件以外，封裝也可以是其他套件的取用者，與不相關任何 PowerShell 命令。

> [!Important]
> 此處所列的命令是專用的 Package Manager Console，在 Visual Studio 中，而且不同於[套件管理模組命令](/powershell/module/packagemanagement/?view=powershell-6)所提供的一般的 PowerShell 環境。 具體來說，每個環境都不在另一個，可用的命令和其特定的引數具有相同名稱的命令可能也有不同。 當使用 Visual Studio 中的 [套件管理] 主控台，目前的這個主題所述的引數與命令套用。

| 常用命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | 會封裝及其相依性安裝到專案中。 | All |
| [Update-Package](ps-ref-update-package.md) | 更新套件和其相依性或在專案中的所有封裝。 | All |
| [Find-Package](ps-ref-find-package.md) | 搜尋套件來源使用的封裝識別碼或關鍵字。 | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | 擷取安裝在本機的存放庫中的套件清單，或列出可用的封裝，從套件來源。 | All |

| 第二個命令 | 描述 | NuGet 版本 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | 會檢查專案的輸出路徑中的所有組件，並新增至繫結重新導向`app.config`或`web.config`在必要時。 | All |
| [Get-Project](ps-ref-get-project.md) | 顯示預設值或指定的專案相關資訊。 | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | 會啟動預設瀏覽器中使用的專案、 授權或指定封裝的檢舉不當使用 URL。 | 3\.0 + 中已被取代 |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | 註冊命令，讓您能夠建立常用的參數值的自訂擴充功能的參數索引標籤展開。 | All |
| [Sync-Package](ps-ref-sync-package.md) | 取得的版本已安裝的套件從指定專案，並同步處理到其他方案中專案的版本。 | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | 從專案中，選擇性地移除其相依性移除封裝。 | All |

如需這些命令的主控台內的任何完整而詳細說明，只要有問題的命令名稱與執行下列命令：

```ps
Get-Help <command> -full
```

所有的套件管理員主控台命令支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):

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
