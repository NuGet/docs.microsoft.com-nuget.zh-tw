---
title: "自動完成，NuGet API |Microsoft 文件"
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
description: "搜尋 「 自動完成 」 服務支援互動式尋找的封裝識別碼和版本。"
keywords: "NuGet 自動完成應用程式開發介面、 NuGet 搜尋封裝識別碼、 子字串的套件識別碼"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a>自動完成

它是可以建置的套件識別碼和版本自動完成體驗使用 V3 API。 自動完成查詢所使用之資源是`SearchAutocompleteService`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                          | 注意
------------------------------------ | -----
SearchAutocompleteService            | 初版
SearchAutocompleteService/3.0.0-beta | 別名`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 別名`SearchAutocompleteService`

## <a name="base-url"></a>基礎 URL

下列應用程式開發介面的基底 URL 是值`@id`與其中一個先前提及的資源相關聯的屬性`@type`值。 下列文件預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。

## <a name="search-for-package-ids"></a>搜尋封裝 Id

第一個自動完成應用程式開發介面支援搜尋的套件 ID 字串的一部分。 當您想要提供使用者介面整合在一起的 NuGet 封裝來源中的封裝 typeahead 功能時，這很適合。

只有未列出的版本的封裝不會出現在結果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求參數

名稱        | In     | 類型    | 必要 | 注意
----------- | ------ | ------- | -------- | -----
q           | URL    | 字串  | 否       | 要與封裝識別碼進行比較的字串
skip        | URL    | 整數 | 否       | 若要略過，針對分頁的結果數目
take        | URL    | 整數 | 否       | 若要傳回，針對分頁的結果數目
發行前版本  | URL    | boolean | 否       | `true`或`false`決定是否要包含[發行前版本的封裝](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 1.0.0 版本字串 

自動完成查詢`q`剖析的方式，由伺服器實作所定義。 nuget.org 支援來查詢前置詞的封裝識別碼權杖是片段 spliting 所產生的識別碼，原始的 camel 命名法的大小寫和符號字元。

`skip`參數預設值為 0。

`take`參數應該大於零的整數。 伺服器實作可能會造成最大值。

如果`prerelease`未提供，會排除發行前版本的封裝。

`semVerLevel`查詢參數用來選擇加入以[SemVer 2.0.0 封裝](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果此查詢參數被排除後，將會傳回與 SemVer 1.0.0 相容版本的唯一封裝識別碼 (與[標準的 NuGet 版本控制](../reference/package-versioning.md)警告，例如 4 整數片段具有的版本字串)。
如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 相容封裝將會傳回。 請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。

### <a name="response"></a>回應

回應是含有最多的 JSON 文件`take`自動完成的結果。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 注意
--------- | ---------------- | -------- | -----
totalHits | 整數          | 是      | 總數的比對，正在略過`skip`和`take`
資料      | 字串陣列 | 是      | 封裝符合所要求的識別碼

### <a name="sample-request"></a>範例要求

GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>列舉封裝版本

一旦找到套件識別碼使用先前的應用程式開發介面，用戶端可以使用自動完成應用程式開發介面來列舉封裝版本提供的封裝識別碼。

未列出的套件版本不會出現在結果中。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求參數

名稱        | In     | 類型    | 必要 | 注意
----------- | ------ | ------- | -------- | -----
id          | URL    | 字串  | 是      | 要擷取的版本的套件識別碼
發行前版本  | URL    | boolean | 否       | `true`或`false`決定是否要包含[發行前版本的封裝](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字串  | 否       | SemVer 2.0.0 的版本字串 

如果`prerelease`未提供，會排除發行前版本的封裝。

`semVerLevel`查詢參數用來選擇加入以 SemVer 2.0.0 的封裝。 如果此查詢參數被排除後，將會傳回只 SemVer 1.0.0 版本。 如果`semVerLevel=2.0.0`提供，將傳回 SemVer 1.0.0 和 SemVer 2.0.0 的版本。 請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。

### <a name="response"></a>回應

回應是包含所有的篩選指定的查詢參數所提供的封裝識別碼的封裝版本的 JSON 文件。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要 | 注意
--------- | ---------------- | -------- | -----
資料      | 字串陣列 | 是      | 封裝版本要求所比對

中的封裝版本`data`陣列可能包含 SemVer 2.0.0 建置中繼資料 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查詢字串中提供。

### <a name="sample-request"></a>範例要求

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>範例回應

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
