---
title: "NuGet CLI 說明命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 的 [說明] 命令的參考"
keywords: "nuget 說明參考，幫助命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 97f72e1be0df6e97f8b06696b2b3861800e4ea08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="help-or--command-nuget-cli"></a>協助或嗎？ 命令 (NuGet CLI)

**適用於：**所有&bullet;**支援的版本，**： 所有

顯示一般說明資訊，以及說明特定命令的相關資訊。

## <a name="usage"></a>使用量

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

其中 [的命令] 識別要顯示說明的特定命令。

> [!Warning]
> 有些命令，以留意指定*協助*第一個，做為與`nuget help install`，因為封裝 nuget.org 上名為 「 說明 」。如果您提供命令`nuget install help`，您不會取得 [說明] 的安裝指令，但會改為安裝說明的套件。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| 全部 | 列印所有可用的命令; 的詳細的說明如果特定命令提供，則會忽略。 |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示的說明說明命令本身的資訊。 |
| Markdown | 列印詳細的說明，以搭配使用時的 markdown 格式`-All`。 否則會忽略。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
