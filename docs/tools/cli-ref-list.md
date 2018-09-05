---
title: NuGet CLI list 命令
description: Nuget.exe list 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549797"
---
# <a name="list-command-nuget-cli"></a>列出命令 (NuGet CLI)

**適用於：** 套件耗用量、 發行&bullet;**支援的版本：** 所有

顯示從指定來源的封裝清單。 如果未不指定任何來源，所有來源檔案中定義全域設定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`，會使用。 如果`NuGet.Config`不指定任何來源，然後`list`會使用預設的摘要 (nuget.org)。

## <a name="usage"></a>使用量

```cli
nuget list [search terms] [options]
```

其中選擇性的搜尋條件會篩選顯示的清單。 就如同它們在 nuget.org 上使用它們時，搜尋字詞會套用至封裝、 標籤及封裝描述的名稱。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| AllVersions | 列出所有版本的封裝。 根據預設，會顯示最新套件版本。 |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| IncludeDelisted | *（3.2 +)* 顯示未列出的套件。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 發行前版本 | 包含發行前版本套件清單中。 |
| 原始程式檔 | 指定要搜尋的封裝來源清單。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
