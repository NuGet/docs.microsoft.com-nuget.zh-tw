---
title: NuGet CLI 來源命令
description: nuget.exe 來源命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622586"
---
# <a name="sources-command-nuget-cli"></a>NuGet CLI (的來源命令) 

**適用于：** 套件耗用量、發佈 &bullet; **支援的版本：** 全部

管理位於使用者範圍設定檔或指定設定檔中的來源清單。 使用者範圍設定檔位於 `%appdata%\NuGet\NuGet.Config` (Windows) 和 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 。

請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。

## <a name="usage"></a>使用方式

```cli
nuget sources <operation> -Name <name> -Source <source>
```

其中 `<operation>` 一個 *清單、新增、移除、啟用、停* 用或 *更新* `<name>` 是來源的名稱，而 `<source>` 是來源的 URL。 您一次只能在一個來源上操作。

## <a name="options"></a>選項。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-Format`**

  適用于 `list` 動作，而且可以 `Detailed` (預設) 或 `Short` 。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-Name`**

  來源的名稱。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Password`**

  指定用來驗證來源的密碼。

- **`-src|-Source`**

  封裝 (s) 來源的路徑。

- **`-StorePasswordInClearText`**

  表示以未加密的文字儲存密碼，而不是儲存加密表單的預設行為。

- **`-UserName`**

  指定要向來源進行驗證的使用者名稱。

- **`-ValidAuthenticationTypes`**

  此來源的有效驗證類型清單（以逗號分隔）。 依預設，所有驗證類型都有效。 範例： `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

> [!Note]
> 請務必在與稍後用來存取套件來源的 nuget.exe 相同的使用者內容下新增來源的密碼。 密碼會以加密方式儲存在設定檔中，而且只能在其加密時于相同的使用者內容中進行解密。 因此，例如，當您使用組建伺服器還原 NuGet 套件時，必須使用組建伺服器工作將執行所在的相同 Windows 使用者來加密密碼。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
