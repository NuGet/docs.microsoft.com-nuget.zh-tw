---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327605"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令 (NuGet CLI)

**適用物件:** 套件耗用量、 &bullet;發行**支援的版本:** 全部

將指定伺服器 URL 的 API 金鑰儲存至`NuGet.Config` , 使其不需要在後續命令中輸入。

## <a name="usage"></a>使用量

```cli
nuget setapikey <key> -Source <url> [options]
```

其中`<source>`識別伺服器, 而`<key>`是要儲存的金鑰或密碼。 如果`<source>`省略, 則會假設為 nuget.org。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
