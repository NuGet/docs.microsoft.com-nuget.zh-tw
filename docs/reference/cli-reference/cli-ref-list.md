---
title: NuGet CLI 清單命令
description: nuget.exe list 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238162"
---
# <a name="list-command-nuget-cli"></a>列出命令 (NuGet CLI) 

**適用于：** 套件耗用量、發佈 &bullet; **支援的版本：** 全部

顯示指定來源的套件清單。 如果未指定任何來源，則會使用全域設定檔中定義的所有來源 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` ）。 如果 `NuGet.Config` 未指定來源，則會 `list` 使用預設摘要 (nuget.org) 。

## <a name="usage"></a>使用方式

```cli
nuget list [search terms] [options]
```

選擇性搜尋詞彙將篩選所顯示的清單。 [搜尋詞彙](../../consume-packages/finding-and-choosing-packages.md#search-syntax) 會套用至套件、標籤和套件描述的名稱，就像在 nuget.org 上使用它們時一樣。 

## <a name="options"></a>選項

- **`-AllVersions`**

  列出套件的所有版本。 依預設，只會顯示最新的套件版本。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-IncludeDelisted`**

  *(3.2 +)* 顯示未列出的套件。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-PreRelease`**

  在清單中包含發行前版本套件。

- **`-Source`**

  指定要搜尋的套件來源清單。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

從設定的摘要列出所有套件：
```
nuget list
```
列出具有詳細詳細資訊的 Azure 相關套件：
```
nuget list Azure -Verbosity detailed
```
從設定的摘要列出 Azure 相關套件的所有版本：
```
nuget list Azure -AllVersions
```
從指定的來源/摘要列出 JSON 相關封裝的所有版本：
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
列出來自多個來源/摘要的 JSON 相關套件：
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```