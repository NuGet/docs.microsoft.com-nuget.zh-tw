---
title: NuGet CLI 搜尋命令
description: nuget.exe 搜尋命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323657"
---
# <a name="search-command-nuget-cli"></a> (NuGet CLI 的搜尋命令) 

**適用物件：** 套件耗用量 &bullet; **支援的版本：** 5.8 +

使用提供的查詢字串來搜尋指定的來源。 如果未指定任何來源，則會使用% AppData% \NuGet\NuGet.Config 中定義的所有來源。

## <a name="usage"></a>使用方式

```cli
nuget search [search terms] [options]
```

搜尋詞彙會套用至套件、標籤和套件描述的名稱，就像在 nuget.org 上使用它們時一樣。

## <a name="options"></a>選項

| 名稱 | 描述 | 使用方式 |
| ---  |     ---     |  :-:  |
| 發佈 | 預設不會包含發行前版本的封裝，但可以使用此引數來包含 | -發行前版本 |
| 來源 | 特定套件來源 (s) 進行搜尋，而不是在 __nuget.config__ 中查詢預設來源 | -來源 `<Source URL>`|
| Take | 要傳回的結果數目。 預設值為 20。 | -Take `<positive integer>` |
| 詳細程度 | 要在輸出中顯示的詳細資料層級。 預設值為 _normal_。  (請參閱下面的附注)   | -詳細資訊 `<quiet|normal|detailed>` |
| Help | 顯示命令的說明資訊 | -Help |

另請參閱 [環境變數](cli-ref-environment-variables.md)

> [!NOTE] 
> 詳細資訊層級：
> * 無訊息套件識別碼，版本
> * _一般_ 套件識別碼、版本、下載、描述預覽
> * _詳細_ 封裝識別碼、版本、下載、完整描述、其他資訊（例如查詢 URL）

## <a name="examples"></a>範例

從預設來源搜尋 *記錄* 相關的套件：
```
nuget search logging
```
使用詳細的詳細資訊搜尋 *記錄* 相關套件：
```
nuget search logging -Verbosity detailed
```
搜尋 *記錄* 相關的套件，並只顯示前5個結果：
```
nuget search logging -Take 5
```
從指定的來源/摘要搜尋 *JSON* 相關封裝，包括發行前版本：
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
從多個來源/摘要搜尋 *JSON* 相關套件：
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
