---
title: "NuGet CLI list 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe list 命令的參考"
keywords: "nuget 清單參考，列出封裝命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="list-command-nuget-cli"></a>列出命令 (NuGet CLI)

**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有

顯示從指定的來源封裝的清單。 如果未不指定任何來源，所有來源檔案中定義全域設定， `%AppData%\NuGet\NuGet.Config`，所使用。 如果`NuGet.Config`不指定任何來源，然後`list`會使用預設的摘要 (nuget.org)。

## <a name="usage"></a>使用量

```cli
nuget list [search terms] [options]
```

其中選擇性的搜尋詞彙會篩選顯示的清單。 搜尋字詞會套用至封裝、 標記，以及封裝描述的名稱。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| AllVersions | 列出所有封裝的版本。 根據預設，會顯示只有最新的封裝版本。 |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| IncludeDelisted | *（3.2 +)*顯示未列出的封裝。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 發行前版本 | 在清單中包含套件發行前版本。 |
| 原始程式檔 | 指定要搜尋的套件來源清單。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
