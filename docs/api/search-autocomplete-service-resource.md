---
title: 自動完成，NuGet API
description: 搜尋自動完成服務支援封裝識別碼和版本的互動式探索。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773955"
---
# <a name="autocomplete"></a>自動完成

您可以使用 V3 API 建立套件識別碼和版本自動完成體驗。 用來進行自動完成查詢的資源是在 `SearchAutocompleteService` [服務索引](service-index.md)中找到的資源。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值                          | 備註
------------------------------------ | -----
SearchAutocompleteService            | 初始版本
SearchAutocompleteService/3.0.0-Beta | 別名 `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 別名 `SearchAutocompleteService`
SearchAutocompleteService/3.5。0      | 包含 `packageType` 查詢參數的支援

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5。0
此版本導入了 `packageType` 查詢參數的支援，允許依作者定義的套件類型進行篩選。 它與的查詢完全相容 `SearchAutocompleteService` 。

## <a name="base-url"></a>基底 URL

下列 Api 的基底 URL 是 `@id` 與上述其中一個資源值相關聯之屬性的值 `@type` 。 在下列檔中，將會使用預留位置基底 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 Url 都支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="search-for-package-ids"></a>搜尋套件識別碼

第一個自動完成 API 支援搜尋套件識別碼字串的一部分。 當您想要在與 NuGet 套件來源整合的使用者介面中提供封裝自動提示功能時，這是很好的選擇。

只有未列出的版本的套件不會出現在結果中。

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>要求參數

名稱        | 位於     | 類型    | 必要 | 備註
----------- | ------ | ------- | -------- | -----
q           | URL    | 字串  | 不可以       | 要與封裝識別碼比較的字串
skip        | URL    | 整數 | 不可以       | 要跳過的結果數目（分頁）
take        | URL    | 整數 | 不可以       | 要傳回的結果數目，用於分頁
prerelease  | URL    | boolean | 不可以       | `true` 或 `false` 判斷是否包含 [發行前版本的套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 不可以       | SemVer 1.0.0 版字串 
packageType | URL    | 字串  | 不可以       | 用來篩選封裝 (在) 中新增的封裝類型 `SearchAutocompleteService/3.5.0`

自動完成查詢 `q` 會以伺服器執行所定義的方式進行剖析。 nuget.org 支援查詢封裝識別碼權杖的前置詞，這是由分割原始的識別碼和符號字元所產生的識別碼片段。

`skip`參數的預設值為0。

`take`參數必須是大於零的整數。 伺服器的執行可能會強加最大值。

如果 `prerelease` 未提供，則會排除發行前版本的套件。

`semVerLevel`查詢參數是用來加入[SemVer 2.0.0 套件](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查詢參數，則只會傳回具有 SemVer 1.0.0 版相容版本的套件識別碼， (有 [標準 NuGet 版本](../concepts/package-versioning.md) 設定注意事項，例如具有4個整數部分) 的版本字串。
如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容套件。 如需詳細資訊，請參閱 [nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

`packageType`參數是用來進一步將自動完成結果篩選為至少有一個套件類型符合套件類型名稱的封裝。
如果提供的封裝類型不是 [封裝類型檔](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)所定義的有效封裝類型，則會傳回空的結果。
如果提供的封裝類型是空的，則不會套用任何篩選。 換句話說，傳遞沒有值給 `packageType` 參數的行為會如同未傳遞參數。

### <a name="response"></a>回應

回應是包含最多 `take` 自動完成結果的 JSON 檔。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 備註
--------- | ---------------- | -------- | -----
totalHits | 整數          | 是      | 相符專案的總數，並忽略 `skip` 和 `take`
data      | 字串陣列 | 是      | 符合要求的套件識別碼

### <a name="sample-request"></a>範例要求

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>列舉套件版本

使用先前的 API 探索到套件識別碼之後，用戶端就可以使用自動完成 API 來列舉所提供封裝識別碼的套件版本。

未列出的套件版本不會出現在結果中。

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>要求參數

名稱        | 位於     | 類型    | 必要 | 注意
----------- | ------ | ------- | -------- | -----
id          | URL    | 字串  | 是      | 要提取版本的套件識別碼
prerelease  | URL    | boolean | 不可以       | `true` 或 `false` 判斷是否包含 [發行前版本的套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 不可以       | SemVer 2.0.0 版本字串 

如果 `prerelease` 未提供，則會排除發行前版本的套件。

`semVerLevel`查詢參數是用來加入 SemVer 2.0.0 套件。 如果排除此查詢參數，則只會傳回 SemVer 1.0.0 版。 如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 版本。 如需詳細資訊，請參閱 [nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

### <a name="response"></a>回應

回應是 JSON 檔，其中包含所提供封裝識別碼的所有套件版本，並依指定的查詢參數進行篩選。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 備註
--------- | ---------------- | -------- | -----
data      | 字串陣列 | 是      | 要求符合的套件版本

陣列中的套件版本 `data` 可能包含 SemVer 2.0.0 組建中繼資料 (例如 `1.0.0+metadata`) 是否 `semVerLevel=2.0.0` 在查詢字串中提供。

### <a name="sample-request"></a>範例要求

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
