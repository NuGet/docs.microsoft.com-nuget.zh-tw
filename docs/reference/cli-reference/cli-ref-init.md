---
title: NuGet CLI init 命令
description: nuget.exe init 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623080"
---
# <a name="init-command-nuget-cli"></a> (NuGet CLI 的 init 命令) 

**適用物件：** 套件建立 &bullet; **支援的版本：** 3.3 +

使用階層配置，將所有封裝從一般資料夾複製到目的資料夾，如 [新增命令](cli-ref-add.md)所述。 也就是說，使用 `init` 相當於在 `add` 資料夾中的每個封裝上使用命令。

如同 `add` ，目的地必須是本機資料夾或 UNC 路徑。不支援 HTTP 套件存放庫（例如 nuget.org 或私用伺服器）。

## <a name="usage"></a>使用方式

```cli
nuget init <source> <destination> [options]
```

其中 `<source>` 是包含封裝的資料夾，以及 `<destination>` 要將封裝複製到其中的本機資料夾或 UNC 路徑名稱。

## <a name="options"></a>選項。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-Expand`**

  將每個新增至封裝來源的套件中的所有檔案加入。與 `-Expand` `add` 命令相同。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
