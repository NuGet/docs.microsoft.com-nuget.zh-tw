---
title: 用來探索 nuget.exe 版本的工具. json
description: 的端點
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611024"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>用來探索 nuget.exe 版本的工具. json

今天，有幾種方式可讓您以腳本的方式，在您的電腦上取得最新版本的 nuget.exe。 例如，您可以從 nuget.org 下載並解壓縮[`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/)套件。這有一些複雜性，因為它需要您已經有 nuget.exe （適用于 `nuget.exe install`），或者您必須使用基本的解壓縮工具來解壓縮 nupkg，並在裡面尋找二進位檔。

如果您已經有 nuget.exe，也可以使用 `nuget.exe update -self`，不過這也需要有一個現有的 nuget.exe 複本。 此方法也會將您更新為最新版本。 它不允許使用特定版本。

`tools.json` 端點可用來解決啟動載入問題，並提供您下載的 nuget.exe 版本的控制權。 這可用於 CI/CD 環境或自訂腳本，以探索並下載任何已發行的 nuget.exe 版本。

`tools.json` 端點可以使用未經驗證的 HTTP 要求來提取（例如，在 PowerShell 或 `wget`中 `Invoke-WebRequest`）。 它可以使用 JSON 還原序列化進行剖析，而後續的 nuget.exe 下載 Url 也可以使用未經驗證的 HTTP 要求來提取。

您可以使用 `GET` 方法來提取端點：

    GET https://dist.nuget.org/tools.json

端點的[JSON 架構](https://json-schema.org/)可在這裡取得：

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>回應

回應是 JSON 檔，其中包含所有可用的 nuget.exe 版本。

根 JSON 物件具有下列屬性：

[屬性]      | 輸入             | 必要項
--------- | ---------------- | --------
nuget.exe | 物件的陣列 | 是

`nuget.exe` 陣列中的每個物件都具有下列屬性：

[屬性]     | 輸入   | 必要項 | 備註
-------- | ------ | -------- | -----
version  | 字串 | 是      | SemVer 2.0.0 字串
URL      | 字串 | 是      | 下載此版本 nuget.exe 的絕對 URL
階段    | 字串 | 是      | 列舉字串
#b0 | 字串 | 是      | 提供版本時的大約 ISO 8601 時間戳記

陣列中的專案將會以遞減的 SemVer 2.0.0 順序排序。 這項保證的目的是要降低用戶端對最高版本號碼感興趣的負擔。 不過，這表示清單不會依時間順序排序。 例如，如果在較高主要版本的日期之後提供較低的主要版本，則此服務版本將不會出現在清單的頂端。 如果您想要由*時間戳記*發行的最新版本，只要依 `uploaded` 字串排序陣列即可。 這是因為 `uploaded` 時間戳記是[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式，可以使用字典排序（也就是簡單字串排序）依時間順序排序。

`stage` 屬性指出此工具版本的通過方式。 

階段              | 意義
------------------ | ------
EarlyAccessPreview | 尚未在[下載網頁](https://www.nuget.org/downloads)上顯示，應由合作夥伴驗證
已發行           | 可在下載網站上取得，但不建議用於廣泛散佈的耗用量
ReleasedAndBlessed | 可在下載網站上取得，建議用於耗用量

有最新的建議版本的一個簡單方法，就是採用清單中具有 `ReleasedAndBlessed``stage` 值的第一個版本。 這是可行的，因為版本會以 SemVer 2.0.0 順序排序。

Nuget.org 上的 `NuGet.CommandLine` 套件通常只會以 `ReleasedAndBlessed` 版本進行更新。

### <a name="sample-request"></a>範例要求

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>範例回應

[!code-JSON [tools-json.json](./_data/tools-json.json)]
