---
title: NuGet CLI 說明 命令
description: Nuget.exe 的 [說明] 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546559"
---
# <a name="help-or--command-nuget-cli"></a>help or ? 命令 (NuGet CLI)

**適用於：** 所有&bullet;**支援的版本**： 所有

顯示一般說明資訊，以及說明特定命令的相關資訊。

## <a name="usage"></a>使用量

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

其中 [command] 會識別特定的命令要顯示的說明。

> [!Warning]
> 一些命令，以留意指定*幫助*第一次，以使用`nuget help install`，因為有在 nuget.org 上名為 「 說明 」 的套件。如果您提供命令`nuget install help`，您將不會取得安裝命令的說明，但會改為安裝說明的套件。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| 全部 | 列印所有可用的命令; 的詳細的說明如果有特定的命令，則會忽略。 |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明資訊本身的 [說明] 命令。 |
| Markdown | 列印與搭配使用時的 markdown 格式的詳細的說明`-All`。 否則會忽略。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
