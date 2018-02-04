---
title: "搜尋、 NuGet API |Microsoft 文件"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "搜尋服務可讓用戶端封裝關鍵字的查詢以及在封裝中的特定欄位上的篩選結果。"
keywords: "NuGet 搜尋 API，NuGet 探索 API 來查詢的 NuGet 封裝 API，以瀏覽 NuGet 套件的套件"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 612ce0f46b654335a29bb36a64b27525994162ed
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="search"></a>搜尋

很可能要搜尋封裝來源使用 V3 API 上可用的封裝。 用於搜尋的資源是`SearchQueryService`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                   | 注意
----------------------------- | -----
SearchQueryService            | 初版
SearchQueryService/3.0.0-beta | 別名`SearchQueryService`
SearchQueryService/3.0.0-rc   | 別名`SearchQueryService`

## <a name="base-url"></a>基礎 URL

下列應用程式開發介面的基底 URL 是值`@id`與其中一個先前提及的資源相關聯的屬性`@type`值。 下列文件預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。

## <a name="search-for-packages"></a>搜尋的封裝

搜尋應用程式開發介面可讓封裝符合指定的搜尋查詢的頁面查詢用戶端。 搜尋查詢 （例如搜尋詞彙的 token 化） 的解譯取決於伺服器實作，但一般預期是搜尋查詢，用於比對的封裝識別碼、 標題、 描述和標記。 也可能會視為其他封裝的中繼資料欄位。

未列出的封裝應永遠不會出現在搜尋結果。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求參數

名稱        | In     | 類型    | 必要 | 注意
----------- | ------ | ------- | -------- | -----
q           | URL    | 字串  | 否       | 搜尋詞彙，以用來篩選器套件
skip        | URL    | 整數 | 否       | 若要略過，針對分頁的結果數目
take        | URL    | 整數 | 否       | 若要傳回，針對分頁的結果數目
發行前版本  | URL    | boolean | 否       | `true`或`false`決定是否要包含[發行前版本的封裝](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 1.0.0 版本字串 

搜尋查詢`q`剖析的方式，由伺服器實作所定義。 nuget.org 支援基本篩選[的各種欄位](../consume-packages/finding-and-choosing-packages.md#search-syntax)。 如果沒有`q`提供所有套件應該都傳回，skip 和 take 所加諸之界限內。 這可讓 Visual Studio 經驗的 [瀏覽] 索引標籤。

`skip`參數預設值為 0。

`take`參數應該大於零的整數。 伺服器實作可能會造成最大值。

如果`prerelease`未提供，會排除發行前版本的封裝。

`semVerLevel`查詢參數用來選擇加入以[SemVer 2.0.0 封裝](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果此查詢參數被排除後，僅限與 SemVer 1.0.0 相容版本的套件將會傳回 (與[標準的 NuGet 版本控制](../reference/package-versioning.md)警告，例如 4 整數片段具有的版本字串)。
如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 相容封裝將會傳回。 請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。

### <a name="response"></a>回應

回應是含有最多的 JSON 文件`take`搜尋結果。 搜尋結果會依照封裝識別碼。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 注意
--------- | ---------------- | -------- | -----
totalHits | 整數          | 是      | 總數的比對，正在略過`skip`和`take`
資料      | 物件的陣列 | 是      | 要求所符合的搜尋結果

### <a name="search-result"></a>搜尋結果

每個項目`data`陣列是一群共用相同的封裝識別碼的封裝版本所組成的 JSON 物件
物件具有下列屬性：

名稱           | 類型                       | 必要 | 注意
-------------- | -------------------------- | -------- | -----
id             | 字串                     | 是      | 相符的套件的識別碼
版本        | 字串                     | 是      | 完整的 SemVer 2.0.0 的版本字串，封裝 （可能包含建置中繼資料）
描述    | 字串                     | 否       | 
版本       | 物件的陣列           | 是      | 所有的相符的封裝版本`prerelease`參數
authors        | 字串或字串陣列 | 否       | 
iconUrl        | 字串                     | 否       | 
licenseUrl     | 字串                     | 否       | 
owners         | 字串或字串陣列 | 否       | 
projectUrl     | 字串                     | 否       | 
註冊   | 字串                     | 否       | 相關聯的絕對 URL[註冊索引](registration-base-url-resource.md#registration-index)
摘要        | 字串                     | 否       | 
標記           | 字串或字串陣列 | 否       | 
標題          | 字串                     | 否       | 
totalDownloads | 整數                    | 否       | 這個值可以推斷下載中的總和`versions`陣列
驗證       | boolean                    | 否       | JSON 布林值，指出封裝是否[驗證](../reference/id-prefix-reservation.md)

在 nuget.org，已驗證的封裝指的是已保留的識別碼前置詞比對的封裝識別碼和擁有者保留的命名空間擁有者之一。 如需詳細資訊，請參閱[識別碼前置詞保留項目相關的文件](../reference/id-prefix-reservation.md)。

搜尋結果物件中包含的中繼資料是來自最新的封裝版本。 每個項目`versions`陣列是 JSON 物件具有下列屬性：

名稱      | 類型    | 必要 | 注意
--------- | ------- | -------- | -----
@id       | 字串  | 是      | 相關聯的絕對 URL[註冊分葉](registration-base-url-resource.md#registration-leaf)
版本   | 字串  | 是      | 完整的 SemVer 2.0.0 的版本字串，封裝 （可能包含建置中繼資料）
下載 | 整數 | 是      | 如需此特定的封裝版本的下載的數目

### <a name="sample-request"></a>範例要求

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>範例回應

[!code-JSON [search-result.json](./_data/search-result.json)]
