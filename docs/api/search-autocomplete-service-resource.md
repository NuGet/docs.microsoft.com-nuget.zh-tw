---
title: 自動完成、 NuGet API
description: 搜尋自動完成服務支援的套件識別碼的互動式探索和版本。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911045"
---
# <a name="autocomplete"></a>自動完成

就可以建置的套件識別碼和版本自動完成體驗使用 V3 API。 用來進行自動完成查詢的資源`SearchAutocompleteService`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                          | 注意
------------------------------------ | -----
SearchAutocompleteService            | 初始版本
SearchAutocompleteService/3.0.0-beta | 別名 `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 別名 `SearchAutocompleteService`

## <a name="base-url"></a>基礎 URL

下列 Api 的基底 URL 是值`@id`其中一個先前提及的資源相關聯的屬性`@type`值。 在下列的文件中的預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

所有 Url 的 HTTP 方法位於註冊資源的支援`GET`和`HEAD`。

## <a name="search-for-package-ids"></a>搜尋套件識別碼

第一個自動完成 API 支援搜尋封裝 ID 字串的一部分。 當您想要提供使用者介面整合在一起的 NuGet 套件來源中的封裝自動提示功能時，這是很棒。

只有未列出的版本的封裝不會出現在結果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求參數

名稱        | In     | 類型    | 必要 | 注意
----------- | ------ | ------- | -------- | -----
q           | URL    | 字串  | 否       | 要相比較的封裝識別碼的字串
skip        | URL    | 整數 | 否       | 若要略過，進行分頁的結果數目
Take        | URL    | 整數 | 否       | 若要傳回，進行分頁的結果數目
發行前版本  | URL    | boolean | 否       | `true` 或是`false`決定是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 1.0.0 版本字串 

自動完成查詢`q`剖析伺服器實作所定義的方式。 nuget.org 支援查詢的套件識別碼權杖中，也就是所產生的分割識別碼的前置詞的原始駝峰式命名法的大小寫和符號字元。

`skip`參數預設值為 0。

`take`參數應該是大於零的整數。 伺服器實作可能會造成最大值。

如果`prerelease`未提供，發行前版本套件中排除。

`semVerLevel`查詢參數用來加入[SemVer 2.0.0 封裝](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查詢參數，則會傳回唯一的套件識別碼與 SemVer 1.0.0 相容版本 (使用[標準的 NuGet 版本控制](../reference/package-versioning.md)需要注意的事項，例如 4 的整數部分的版本字串)。
如果`semVerLevel=2.0.0`提供，將傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容的套件。 請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。

### <a name="response"></a>回應

回應是 JSON 文件最多包含`take`自動完成結果。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 注意
--------- | ---------------- | -------- | -----
totalHits | 整數          | 是      | 總數的相符項目，正在略過`skip`和 `take`
資料      | 字串陣列 | 是      | 封裝符合所要求的識別碼

### <a name="sample-request"></a>範例要求

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>列舉套件版本

一旦找到套件識別碼使用先前的 API，用戶端可以使用自動完成 API 來列舉套件版本提供的套件識別碼。

未列出的套件版本不會出現在結果中。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求參數

名稱        | In     | 類型    | 必要 | 注意
----------- | ------ | ------- | -------- | -----
id          | URL    | 字串  | 是      | 要擷取的版本之封裝 ID
發行前版本  | URL    | boolean | 否       | `true` 或是`false`決定是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 2.0.0 版本字串 

如果`prerelease`未提供，發行前版本套件中排除。

`semVerLevel`查詢參數用來選擇加入的 SemVer 2.0.0 套件。 如果此查詢參數被排除後，就會傳回只 SemVer 1.0.0 版。 如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 版本將會傳回。 請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。

### <a name="response"></a>回應

回應是 JSON 文件包含所有的篩選指定的查詢參數所提供的封裝識別碼的封裝版本。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 注意
--------- | ---------------- | -------- | -----
資料      | 字串陣列 | 是      | 比對要求的套件版本

中的套件版本`data`陣列可能包含 SemVer 2.0.0 組建中繼資料 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`提供查詢字串中。

### <a name="sample-request"></a>範例要求

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
