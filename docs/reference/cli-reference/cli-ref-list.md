---
title: NuGet CLI 清單命令
description: Nuget.exe list 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327735"
---
# <a name="list-command-nuget-cli"></a>list 命令 (NuGet CLI)

**適用物件:** 套件耗用量、 &bullet;發行**支援的版本:** 全部

顯示來自指定來源的封裝清單。 如果未指定來源, 則會使用全域設定檔`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`中定義的所有來源。 如果`NuGet.Config`未指定來源, 則`list`會使用預設摘要 (nuget.org)。

## <a name="usage"></a>使用量

```cli
nuget list [search terms] [options]
```

選擇性搜尋詞彙會在其中篩選所顯示的清單。 搜尋詞彙會套用至封裝、標記和封裝描述的名稱, 就如同在 nuget.org 上使用它們一樣。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| AllVersions | 列出封裝的所有版本。 根據預設, 只會顯示最新的套件版本。 |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| IncludeDelisted | *(3.2 +)* 顯示未列出的套件。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| PreRelease | 包含清單中的發行前版本套件。 |
| Source | 指定要搜尋的封裝來源清單。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
