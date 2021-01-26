---
title: 探索 nuget.exe 版本的 tools.js
description: 的端點
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773814"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>探索 nuget.exe 版本的 tools.js

現在，有幾種方式可在電腦上以可編寫腳本的方式取得最新版本的 nuget.exe。 例如，您可以從 nuget.org 下載並解壓縮 [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) 套件。這會有一些複雜性，因為它需要您已經有) 的 nuget.exe (， `nuget.exe install` 或是您必須使用基本的解壓縮工具解壓縮 nupkg，然後在內部尋找二進位檔。

如果您已經有 nuget.exe，也可以使用 `nuget.exe update -self` ，不過這也需要現有的 nuget.exe 複本。 這種方法也會將您更新至最新版本。 不允許使用特定版本。

`tools.json`端點可用於解決啟動載入問題，並提供您所下載之 nuget.exe 版本的控制權。 這可用於 CI/CD 環境或自訂腳本，以探索並下載任何已發行的 nuget.exe 版本。

您 `tools.json` 可以使用未經驗證的 HTTP (要求來提取端點，例如 `Invoke-WebRequest` 在 PowerShell 或 `wget`) 中。 您可以使用 JSON 還原序列化來剖析它，後續 nuget.exe 下載 Url 也可以使用未驗證的 HTTP 要求來提取。

您可以使用方法來提取端點 `GET` ：

```
GET https://dist.nuget.org/tools.json
```

您可以在這裡找到端點的 [JSON 架構](https://json-schema.org/) ：

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>回應

回應是 JSON 檔，其中包含所有可用的 nuget.exe 版本。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要
--------- | ---------------- | --------
nuget.exe | 物件的陣列 | 是

陣列中的每個物件 `nuget.exe` 都有下列屬性：

名稱     | 類型   | 必要 | 備註
-------- | ------ | -------- | -----
version  | 字串 | 是      | SemVer 2.0.0 字串
url      | 字串 | 是      | 下載此版本 nuget.exe 的絕對 URL
stage (階段)    | 字串 | 是      | 列舉字串
上傳 | 字串 | 是      | 當版本可供使用時的大約 ISO 8601 時間戳記

陣列中的專案將會以遞減的 SemVer 2.0.0 順序排序。 這項保證的目的是要降低對最高版本號碼有興趣之用戶端的負擔。 不過這表示清單不是依時間順序排序。 例如，如果較低的主要版本在晚于較高主要版本的日期提供服務，此服務版本將不會出現在清單的頂端。 如果您想要以 *時間戳記* 發行的最新版本，只要依字串排序陣列即可 `uploaded` 。 這是有效的，因為 `uploaded` 時間戳記的格式為 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) ，可以使用字典排序來依時間順序排序 (例如，簡單的字串排序) 。

`stage`屬性工作表示此工具版本的通過。 

階段              | 意義
------------------ | ------
EarlyAccessPreview | 尚未在 [下載網頁](https://www.nuget.org/downloads) 上顯示，應該由夥伴進行驗證
已發行           | 在下載網站上提供，但不建議用於寬範圍耗用量
ReleasedAndBlessed | 可在下載網站上取得，並建議用於耗用量

具有最新的建議版本的一個簡單方法是，採用清單中具有值的第一個版本 `stage` `ReleasedAndBlessed` 。 這是有效的，因為版本會以 SemVer 2.0.0 順序排序。

`NuGet.CommandLine`Nuget.org 上的封裝通常只會以 `ReleasedAndBlessed` 版本更新。

### <a name="sample-request"></a>範例要求

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [tools-json.json](./_data/tools-json.json)]
