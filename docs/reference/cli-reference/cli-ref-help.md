---
title: NuGet CLI help 命令
description: nuget.exe help 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779360"
---
# <a name="help-or--command-nuget-cli"></a>help 或 ?  (NuGet CLI 的命令) 

**適用于：** 所有 &bullet; **支援的版本**：全部

顯示有關特定命令的一般說明資訊和說明資訊。

## <a name="usage"></a>使用方式

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

where [command] 識別要顯示說明的特定命令。

> [!Warning]
> 使用一些命令時，請注意先 *指定說明* ， `nuget help install` 因為 nuget.org 上有一個名為 "help" 的封裝。如果您指定命令 `nuget install help` ，就不會取得安裝命令的說明，而是會安裝名為 help 的封裝。

## <a name="options"></a>選項。

- **`-All`**

  列印所有可用命令的詳細說明;如果指定了特定命令，則會予以忽略。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-Markdown`**

  搭配使用時，請列印 markdown 格式的詳細說明 `-All` 。 否則會予以忽略。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
