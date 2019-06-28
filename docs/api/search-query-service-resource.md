---
title: 搜尋服務中，NuGet API
description: 搜尋服務可讓用戶端封裝關鍵字的查詢以及在封裝中的特定欄位上的篩選結果。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d462b289c39c2dd1418304dabcad47d0d4217f82
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426737"
---
# <a name="search"></a>搜尋

您可搜尋的套件來源使用 V3 API 上可用的套件。 用來搜尋的資源`SearchQueryService`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                   | 注意
----------------------------- | -----
SearchQueryService            | 初始版本
SearchQueryService/3.0.0-beta | 別名 `SearchQueryService`
SearchQueryService/3.0.0-rc   | 別名 `SearchQueryService`

## <a name="base-url"></a>基礎 URL

下列 API 的基底 URL 是值`@id`其中一個先前提及的資源相關聯的屬性`@type`值。 在下列的文件中的預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

所有 Url 的 HTTP 方法位於註冊資源的支援`GET`和`HEAD`。

## <a name="search-for-packages"></a>搜尋套件

搜尋 API 可讓用戶端查詢，封裝符合指定的搜尋查詢的頁面。 搜尋查詢 （例如搜尋詞彙的 token 化） 的解譯取決於伺服器實作，但一般的期望，是搜尋查詢用來比對的封裝識別碼、 標題、 描述和標記。 可能也會視為其他套件中繼資料欄位。

未列出的套件應該永遠不會出現在搜尋結果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求參數

名稱        | In     | 類型    | 必要 | 注意
----------- | ------ | ------- | -------- | -----
q           | URL    | 字串  | 否       | 搜尋詞彙，以用來篩選器套件
skip        | URL    | 整數 | 否       | 若要略過，進行分頁的結果數目
Take        | URL    | 整數 | 否       | 若要傳回，進行分頁的結果數目
發行前版本  | URL    | boolean | 否       | `true` 或是`false`決定是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 1.0.0 版本字串 

搜尋查詢`q`剖析伺服器實作所定義的方式。 nuget.org 支援基本篩選[的各種欄位](../consume-packages/finding-and-choosing-packages.md#search-syntax)。 如果沒有`q`提供所有套件應該會都傳回，skip 和 take 所加諸的界限內。 這可讓 NuGet Visual Studio 經驗的 [瀏覽] 索引標籤。

`skip`參數預設值為 0。

`take`參數應該是大於零的整數。 伺服器實作可能會造成最大值。

如果`prerelease`未提供，發行前版本套件中排除。

`semVerLevel`查詢參數用來加入[SemVer 2.0.0 封裝](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查詢參數時，會傳回唯一的套件與 SemVer 1.0.0 相容版本 (使用[標準的 NuGet 版本控制](../reference/package-versioning.md)需要注意的事項，例如 4 的整數部分的版本字串)。
如果`semVerLevel=2.0.0`提供，將傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容的套件。 請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。

### <a name="response"></a>回應

回應是 JSON 文件最多包含`take`搜尋結果。 搜尋結果會依封裝識別碼。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 注意
--------- | ---------------- | -------- | -----
totalHits | 整數          | 是      | 總數的相符項目，正在略過`skip`和 `take`
資料      | 物件的陣列 | 是      | 搜尋結果要求所比對

### <a name="search-result"></a>搜尋結果

在每個項目`data`陣列是一群共用相同的封裝識別碼。 套件版本所組成的 JSON 物件
物件具有下列屬性：

名稱           | 類型                       | 必要 | 注意
-------------- | -------------------------- | -------- | -----
id             | 字串                     | 是      | 相符的套件識別碼
版本        | 字串                     | 是      | 完整的 SemVer 2.0.0 版本字串 （可能包含組建中繼資料） 的套件
描述    | 字串                     | 否       | 
版本       | 物件的陣列           | 是      | 所有的套件符合版本`prerelease`參數
authors        | 字串或字串陣列 | 否       | 
iconUrl        | 字串                     | 否       | 
licenseUrl     | 字串                     | 否       | 
owners         | 字串或字串陣列 | 否       | 
projectUrl     | 字串                     | 否       | 
註冊   | 字串                     | 否       | 相關聯的絕對 URL[註冊索引](registration-base-url-resource.md#registration-index)
摘要        | 字串                     | 否       | 
標記           | 字串或字串陣列 | 否       | 
標題          | 字串                     | 否       | 
totalDownloads | 整數                    | 否       | 此值來推斷的下載項目中的總和`versions`陣列
驗證       | boolean                    | 否       | JSON 布林值，指出封裝是否[驗證](../nuget-org/id-prefix-reservation.md)

在 nuget.org 上，已驗證的套件是一種比對的保留的識別碼前置詞的套件識別碼和保留的前置詞的擁有者所擁有。 如需詳細資訊，請參閱 <<c0> [ 識別碼首碼保留項目相關的文件](../reference/id-prefix-reservation.md)。

在搜尋結果物件中包含的中繼資料是來自最新的套件版本。 在每個項目`versions`陣列是具有下列屬性的 JSON 物件：

名稱      | 類型    | 必要 | 注意
--------- | ------- | -------- | -----
@id       | 字串  | 是      | 相關聯的絕對 URL[註冊分葉](registration-base-url-resource.md#registration-leaf)
版本   | 字串  | 是      | 完整的 SemVer 2.0.0 版本字串 （可能包含組建中繼資料） 的套件
下載項目 | 整數 | 是      | 如需此特定套件版本的下載的數目

### <a name="sample-request"></a>範例要求

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>範例回應

[!code-JSON [search-result.json](./_data/search-result.json)]
