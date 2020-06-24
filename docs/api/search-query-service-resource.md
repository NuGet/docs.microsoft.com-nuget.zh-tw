---
title: 搜尋，NuGet API
description: 搜尋服務可讓用戶端依關鍵字查詢封裝，以及篩選特定封裝欄位的結果。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aed591ceba00f1820a573eacf312112db0a1c69e
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292266"
---
# <a name="search"></a>搜尋

您可以使用 V3 API 搜尋封裝來源上可用的套件。 用於搜尋的資源是 `SearchQueryService` 在[服務索引](service-index.md)中找到的資源。

## <a name="versioning"></a>版本控制

`@type`會使用下列值：

@type 值                   | 備註
----------------------------- | -----
SearchQueryService            | 初始版本
SearchQueryService/3.0.0-搶鮮版（Beta） | 別名`SearchQueryService`
SearchQueryService/3.0.0-rc   | 別名`SearchQueryService`
SearchQueryService/3.5。0      | 包含 `packageType` 查詢參數的支援

### <a name="searchqueryservice350"></a>SearchQueryService/3.5。0
這個版本導入了 `packageType` 查詢參數和 `packageTypes` 回應屬性的支援，允許依作者定義的套件類型進行篩選。 它與的查詢完全相容 `SearchQueryService` 。

## <a name="base-url"></a>基底 URL

下列 API 的基底 URL 是 `@id` 與上述其中一個資源值相關聯的屬性值 `@type` 。 在下列檔中，將會使用預留位置基底 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 Url 都支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="search-for-packages"></a>搜尋套件

搜尋 API 可讓用戶端查詢符合指定搜尋查詢的套件頁面。 搜尋查詢的轉譯（例如搜尋詞彙的 token）是由伺服器的執行所決定，但一般的預期是搜尋查詢是用來比對封裝識別碼、標題、描述和標記。 也可以考慮其他套件元資料欄位。

未列出的套件應該永遠不會出現在搜尋結果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>要求參數

Name        | 位於     | 類型    | 必要 | 備註
----------- | ------ | ------- | -------- | -----
q           | URL    | 字串  | 否       | 用來篩選封裝的搜尋字詞
skip        | URL    | integer | 否       | 要略過的結果數目，用於分頁
take        | URL    | integer | 否       | 要傳回的結果數目，用於分頁
prerelease  | URL    | boolean | 否       | `true`或 `false` 判斷是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 1.0.0 版本字串 
packageType | URL    | 字串  | 否       | 用來篩選封裝的封裝類型（新增于中 `SearchQueryService/3.5.0` ）

搜尋查詢 `q` 會以伺服器實作為定義的方式進行剖析。 nuget.org 支援[各種欄位](../consume-packages/finding-and-choosing-packages.md#search-syntax)的基本篩選。 如果未 `q` 提供，則應該在 skip 和 take 強加的界限內傳回所有套件。 這會啟用 NuGet Visual Studio 體驗中的 [流覽] 索引標籤。

`skip`參數的預設值為0。

`take`參數應該是大於零的整數。 伺服器的執行可能會強加最大值。

如果 `prerelease` 未提供，則會排除發行前版本套件。

`semVerLevel`查詢參數是用來加入[SemVer 2.0.0 套件](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查詢參數，則只會傳回具有 SemVer 1.0.0 相容版本的套件（具有[標準 NuGet 版本](../concepts/package-versioning.md)設定注意事項，例如具有4個整數部分的版本字串）。
如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容的套件。 如需詳細資訊，請參閱[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

`packageType`參數是用來進一步篩選搜尋結果，只包含至少有一個符合封裝類型名稱的套件類型的封裝。
如果提供的封裝類型不是[封裝類型檔](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)所定義的有效封裝類型，則會傳回空的結果。
如果提供的封裝類型是空的，則不會套用任何篩選。 換句話說，將沒有值傳遞給 packageType 參數的行為會如同未傳遞參數一樣。

### <a name="response"></a>回應

回應是包含最多搜尋結果的 JSON 檔 `take` 。 搜尋結果會依套件識別碼分組。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 備註
--------- | ---------------- | -------- | -----
totalHits | integer          | 是      | 相符專案總數，忽略 `skip` 和`take`
data      | 物件的陣列 | 是      | 要求所符合的搜尋結果

### <a name="search-result"></a>搜尋結果

陣列中的每個專案 `data` 都是由一組共用相同封裝識別碼的套件版本所組成的 JSON 物件。
此物件具有下列屬性：

Name           | 類型                       | 必要 | 備註
-------------- | -------------------------- | -------- | -----
id             | 字串                     | 是      | 相符封裝的識別碼
version        | 字串                     | 是      | 封裝的完整 SemVer 2.0.0 版本字串（可能包含組建中繼資料）
description    | 字串                     | 否       | 
versions       | 物件的陣列           | 是      | 符合參數的所有套件版本 `prerelease`
authors        | 字串或字串陣列 | 否       | 
iconUrl        | 字串                     | 否       | 
licenseUrl     | 字串                     | 否       | 
owners         | 字串或字串陣列 | 否       | 
projectUrl     | 字串                     | 否       | 
註冊   | 字串                     | 否       | 相關聯[註冊索引](registration-base-url-resource.md#registration-index)的絕對 URL
summary        | 字串                     | 否       | 
tags           | 字串或字串陣列 | 否       | 
title          | 字串                     | 否       | 
totalDownloads | integer                    | 否       | 這個值可以由陣列中的下載總和來推斷。 `versions`
之後       | boolean                    | 否       | 指出是否已[驗證](../nuget-org/id-prefix-reservation.md)套件的 JSON 布林值
packageTypes   | 物件的陣列           | 是      | 封裝作者定義的套件類型（新增于 `SearchQueryService/3.5.0` ）

在 nuget.org 上，已驗證的套件是其中一個套件識別碼符合保留的識別碼前置詞，並由其中一個保留的前置詞擁有者所擁有。 如需詳細資訊，請參閱[識別碼前置詞保留的相關檔](../reference/id-prefix-reservation.md)。

搜尋結果物件中包含的中繼資料是從最新的封裝版本取得。 陣列中的每個專案 `versions` 都是具有下列屬性的 JSON 物件：

Name      | 類型    | 必要 | 備註
--------- | ------- | -------- | -----
@id       | 字串  | 是      | 相關聯[註冊分葉](registration-base-url-resource.md#registration-leaf)的絕對 URL
version   | 字串  | 是      | 封裝的完整 SemVer 2.0.0 版本字串（可能包含組建中繼資料）
下載 | integer | 是      | 此特定套件版本的下載次數

`packageTypes`陣列一律會包含至少一個（1）個專案。 指定封裝識別碼的套件類型會被視為套件類型，是由套件的最新版本所定義（相對於其他搜尋參數）。 陣列中的每個專案 `packageTypes` 都是具有下列屬性的 JSON 物件：

Name      | 類型    | 必要 | 注意
--------- | ------- | -------- | -----
NAME      | 字串  | 是      | 封裝類型的名稱。

### <a name="sample-request"></a>範例要求

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>範例回應

[!code-JSON [search-result.json](./_data/search-result.json)]
