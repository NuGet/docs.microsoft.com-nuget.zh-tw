---
title: 自動完成，NuGet API
description: 搜尋自動完成服務支援對套件識別碼和版本進行互動式探索。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292289"
---
# <a name="autocomplete"></a>自動完成

您可以使用 V3 API 來建立套件識別碼和版本自動完成體驗。 用來進行自動完成查詢的資源是 `SearchAutocompleteService` 在[服務索引](service-index.md)中找到的資源。

## <a name="versioning"></a>版本控制

`@type`會使用下列值：

@type 值                          | 備註
------------------------------------ | -----
SearchAutocompleteService            | 初始版本
SearchAutocompleteService/3.0.0-搶鮮版（Beta） | 別名`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 別名`SearchAutocompleteService`
SearchAutocompleteService/3.5。0      | 包含 `packageType` 查詢參數的支援

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5。0
這個版本導入了 `packageType` 查詢參數的支援，允許依作者定義的套件類型進行篩選。 它與的查詢完全相容 `SearchAutocompleteService` 。

## <a name="base-url"></a>基底 URL

下列 Api 的基底 URL 是 `@id` 與上述其中一個資源值相關聯的屬性值 `@type` 。 在下列檔中，將會使用預留位置基底 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 Url 都支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="search-for-package-ids"></a>搜尋套件識別碼

第一個自動完成 API 支援搜尋封裝識別碼字串的一部分。 當您想要在與 NuGet 套件來源整合的使用者介面中提供封裝自動提示功能時，這是很好的選擇。

只有未列出版本的套件不會出現在結果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>要求參數

Name        | 位於     | 類型    | 必要 | 備註
----------- | ------ | ------- | -------- | -----
q           | URL    | 字串  | 否       | 要與套件識別碼比較的字串
skip        | URL    | integer | 否       | 要略過的結果數目，用於分頁
take        | URL    | integer | 否       | 要傳回的結果數目，用於分頁
prerelease  | URL    | boolean | 否       | `true`或 `false` 判斷是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 1.0.0 版本字串 
packageType | URL    | 字串  | 否       | 用來篩選封裝的封裝類型（新增于中 `SearchAutocompleteService/3.5.0` ）

自動完成查詢 `q` 會以伺服器實作為定義的方式進行剖析。 nuget.org 支援查詢套件識別碼權杖的前置詞，這是由 spliting 原始 by camel 大小寫和符號字元所產生的識別碼片段。

`skip`參數的預設值為0。

`take`參數應該是大於零的整數。 伺服器的執行可能會強加最大值。

如果 `prerelease` 未提供，則會排除發行前版本套件。

`semVerLevel`查詢參數是用來加入[SemVer 2.0.0 套件](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查詢參數，則只會傳回具有 SemVer 1.0.0 相容版本的套件識別碼（使用[標準 NuGet 版本](../concepts/package-versioning.md)設定注意事項，例如具有4個整數部分的版本字串）。
如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容的套件。 如需詳細資訊，請參閱[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

`packageType`參數是用來進一步篩選自動完成結果，只包含至少有一個符合封裝類型名稱之套件類型的封裝。
如果提供的封裝類型不是[封裝類型檔](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)所定義的有效封裝類型，則會傳回空的結果。
如果提供的封裝類型是空的，則不會套用任何篩選。 換句話說，將沒有值傳遞給參數的 `packageType` 行為會如同未傳遞參數一樣。

### <a name="response"></a>回應

回應是包含最多 `take` 自動完成結果的 JSON 檔。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 備註
--------- | ---------------- | -------- | -----
totalHits | integer          | 是      | 相符專案總數，忽略 `skip` 和`take`
data      | 字串陣列 | 是      | 要求所符合的套件識別碼

### <a name="sample-request"></a>範例要求

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>列舉封裝版本

一旦使用先前的 API 探索到套件識別碼之後，用戶端就可以使用自動完成 API 來列舉所提供封裝識別碼的套件版本。

未列出的封裝版本不會出現在結果中。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求參數

Name        | 位於     | 類型    | 必要 | 備註
----------- | ------ | ------- | -------- | -----
id          | URL    | 字串  | 是      | 要為其提取版本的封裝識別碼
prerelease  | URL    | boolean | 否       | `true`或 `false` 判斷是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 2.0.0 版本字串 

如果 `prerelease` 未提供，則會排除發行前版本套件。

`semVerLevel`查詢參數是用來加入 SemVer 2.0.0 套件。 如果排除此查詢參數，則只會傳回 SemVer 1.0.0 版。 如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 版本。 如需詳細資訊，請參閱[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

### <a name="response"></a>回應

回應是 JSON 檔，其中包含所提供封裝識別碼的所有封裝版本，並依指定的查詢參數進行篩選。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 備註
--------- | ---------------- | -------- | -----
data      | 字串陣列 | 是      | 要求所符合的套件版本

如果查詢字串中提供，則陣列中的封裝版本 `data` 可能會包含 SemVer 2.0.0 組建中繼資料（例如 `1.0.0+metadata` ） `semVerLevel=2.0.0` 。

### <a name="sample-request"></a>範例要求

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
