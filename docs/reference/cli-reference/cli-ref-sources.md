---
title: NuGet CLI 來源命令
description: Nuget.exe 來源命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327595"
---
# <a name="sources-command-nuget-cli"></a>sources 命令 (NuGet CLI)

**適用物件:** 套件耗用量、 &bullet;發行**支援的版本:** 全部

管理位於使用者範圍設定檔或指定的設定檔中的來源清單。 使用者範圍設定檔位於`%appdata%\NuGet\NuGet.Config` (Windows) 和`~/.nuget/NuGet/NuGet.Config` (Mac/Linux)。

請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。

## <a name="usage"></a>使用量

```cli
nuget sources <operation> -Name <name> -Source <source>
```

其中`<operation>` , 是*清單、新增、移除、啟用、停*用或*更新* `<name>`其中之一, 是來源的名稱, 而`<source>`是來源的 URL。 您一次只能在一個來源上操作。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| 格式 | 適用于`Detailed` `Short`動作, 而且可以是 (預設值) 或。 `list` |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| 密碼 | 指定用來驗證來源的密碼。 |
| StorePasswordInClearText | 表示將密碼儲存為未加密的文字, 而不是儲存加密格式的預設行為。 |
| 使用者名稱 | 指定用來驗證來源的使用者名稱。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

> [!Note]
> 請務必在與 nuget.exe 相同的使用者內容下新增來源的密碼, 以供稍後用來存取封裝來源。 密碼會以加密方式儲存在設定檔中, 而且只能在加密的相同使用者內容中進行解密。 例如, 當您使用組建伺服器來還原 NuGet 套件時, 必須使用組建伺服器工作執行所在的相同 Windows 使用者來加密密碼。

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
