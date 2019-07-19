---
title: NuGet CLI help 命令
description: Nuget.exe help 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327795"
---
# <a name="help-or--command-nuget-cli"></a>help or ? 命令 (NuGet CLI)

**適用于:** 所有&bullet; **支援的版本**: 全部

顯示特定命令的一般說明資訊和說明資訊。

## <a name="usage"></a>使用量

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

其中 [command] 識別要顯示說明的特定命令。

> [!Warning]
> 使用一些命令時, 請注意先  指定說明, 如同`nuget help install`, 因為 nuget.org 上有一個名為 "help" 的套件。如果您提供命令`nuget install help`, 就不會取得安裝命令的說明, 而是會安裝名為 [說明] 的套件。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| All | 列印所有可用命令的詳細說明;如果指定了特定的命令, 則會忽略。 |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示 help 命令本身的說明資訊。 |
| Markdown | 當搭配使用時, `-All`列印 markdown 格式的詳細說明。 否則會予以忽略。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
