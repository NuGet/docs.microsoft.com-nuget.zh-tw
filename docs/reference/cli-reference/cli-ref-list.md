---
title: NuGet CLI 清單命令
description: Nuget.exe list 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813334"
---
# <a name="list-command-nuget-cli"></a>list 命令（NuGet CLI）

**適用物件：** 套件耗用量、發行 &bullet;**支援的版本：** 全部

顯示來自指定來源的封裝清單。 如果未指定來源，則會使用全域設定檔中所定義的所有來源 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config`。 如果 `NuGet.Config` 未指定來源，則 `list` 會使用預設的摘要（nuget.org）。

## <a name="usage"></a>使用

```cli
nuget list [search terms] [options]
```

選擇性搜尋詞彙會在其中篩選所顯示的清單。 搜尋詞彙會套用至封裝、標記和封裝描述的名稱，就如同在 nuget.org 上使用它們一樣。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| AllVersions | 列出封裝的所有版本。 根據預設，只會顯示最新的套件版本。 |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | *（3.5 +）* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| 說明 | 顯示命令的說明資訊。 |
| IncludeDelisted | *（3.2 +）* 顯示未列出的套件。 |
| 非 | 抑制使用者輸入或確認的提示。 |
| PreRelease | 包含清單中的發行前版本套件。 |
| 原始程式檔 | 指定要搜尋的封裝來源清單。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

列出已設定摘要中的所有套件：
```
nuget list
```
列出與 Azure 相關的套件，詳細資訊如下：
```
nuget list Azure -Verbosity detailed
```
從已設定的摘要列出所有與 Azure 相關的套件版本：
```
nuget list Azure -AllVersions
```
從指定的來源/摘要列出 JSON 相關套件的所有版本：
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
列出來自多個來源/摘要的 JSON 相關套件：
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

