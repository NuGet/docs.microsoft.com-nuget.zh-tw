---
title: 套件中繼資料，NuGet API
description: 套件註冊基底 URL 可讓您擷取有關封裝的中繼資料。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 19a1f48164f65f1ff805e036e55abb110247aa72
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324860"
---
# <a name="package-metadata"></a>套件中繼資料

就可以擷取有關可用之封裝的中繼資料上使用 NuGet V3 API 的套件來源。 此中繼資料可以使用提取`RegistrationsBaseUrl`資源中找到[服務索引](service-index.md)。

下找到的文件集合`RegistrationsBaseUrl`通常稱為 「 註冊 」 或 「 註冊 blob 」。 下一個文件集`RegistrationsBaseUrl`稱為 「 登錄 hive 」。 將登錄 hive 控制檔包含有關每個可用套件的套件來源上的所有中繼資料。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                     | 注意
------------------------------- | -----
RegistrationsBaseUrl            | 初始版本
RegistrationsBaseUrl/3.0.0-beta | 別名 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 別名 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip 回應
RegistrationsBaseUrl/3.6.0      | 包含 SemVer 2.0.0 套件

這表示可供各種用戶端版本的三個相異的登錄 hive。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

未壓縮這些註冊 (這表示它們會使用隱含`Content-Encoding: identity`)。 SemVer 2.0.0 套件**排除**從這個 hive。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

使用壓縮這些註冊`Content-Encoding: gzip`。 SemVer 2.0.0 套件**排除**從這個 hive。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

使用壓縮這些註冊`Content-Encoding: gzip`。 SemVer 2.0.0 套件**包含**此區中。
如需有關 SemVer 2.0.0 的詳細資訊，請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基礎 URL

下列 Api 的基底 URL 是值`@id`上述的資源相關聯的屬性`@type`值。 在下列的文件中的預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

所有 Url 的 HTTP 方法位於註冊資源的支援`GET`和`HEAD`。

## <a name="registration-index"></a>註冊索引

註冊資源群組封裝中繼資料的封裝識別碼。 您不可能一次取得多個套件識別碼的相關資料。 此資源會提供任何方法可探索的封裝識別碼。 而是用戶端會假設已經知道所需的封裝識別碼。 每個套件版本的相關可用的中繼資料會因伺服器實作。 封裝註冊 blob 會有下列的階層式結構：

- **索引**： 共用相同的封裝識別碼。 具有來源上的所有套件的套件中繼資料的進入點
- **頁面**： 封裝版本的群組。 在頁面中的封裝版本數目是由伺服器實作定義。
- **分葉**： 單一封裝的版本特定的文件。

註冊索引的 URL 是可預測，並判斷所指定的封裝識別碼和註冊資源的用戶端`@id`從服務索引的值。 藉由檢查註冊索引探索到註冊頁面並保留的 Url。

### <a name="registration-pages-and-leaves"></a>註冊頁面和分葉

雖然它並非絕對必要的伺服器實作，來儲存註冊葉子個別註冊 頁面的文件中，它會是建議的作法，以節省用戶端記憶體。 而不是內嵌這所有註冊會保留在索引或立即儲存在頁面的文件中的 分葉、 建議的伺服器實作定義的套件版本號碼為基礎的兩種方法之間做選擇某個啟發學習法或離開封裝的累計大小。

儲存所有的套件版本 （分葉） 註冊索引儲存 HTTP 要求的數目才能擷取套件中繼資料，但必須下載較大的文件和必須配置更多的用戶端記憶體的表示。 相反地，如果伺服器實作立即儲存在另一個頁面上的文件中的註冊分葉，用戶端必須執行更多的 HTTP 要求，以取得所需的資訊。

Nuget.org 會使用如下所示的啟發學習法： 如果有 128 個或多個封裝的版本，則將分葉分成頁面大小為 64。 如果有 128 個版本，所有內嵌都離開至註冊的索引。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求參數

名稱     | In     | 類型    | 必要 | 注意
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼、 小寫

`LOWER_ID`值是小寫使用規則實作所需的套件識別碼。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>回應

回應是 JSON 文件有根物件，具有下列屬性：

名稱  | 類型             | 必要 | 注意
----- | ---------------- | -------- | -----
count | 整數          | 是      | 在索引中的註冊頁面數目
項目 | 物件的陣列 | 是      | 陣列的註冊頁面

在索引物件的每個項目`items`陣列是 JSON 物件，代表註冊頁面。

#### <a name="registration-page-object"></a>註冊頁面物件

註冊索引中找到的註冊頁面物件具有下列屬性：

名稱   | 類型             | 必要 | 注意
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 註冊頁面 URL
count  | 整數          | 是      | 離開頁面中的註冊數目
項目  | 物件的陣列 | 否       | 註冊分葉和其關聯的中繼資料的陣列
較低  | 字串           | 是      | （含） 頁面中最低的 SemVer 2.0.0 版本
父代 | 字串           | 否       | 要註冊索引 URL
上限  | 字串           | 是      | （含） 頁面中最高的 SemVer 2.0.0 版本

`lower`和`upper`時需要特定的頁面版本中繼資料的頁面物件的界限很有用。
這些繫結可用來擷取所需的唯一註冊頁面。 版本字串遵守[NuGet 版本規則](../reference/package-versioning.md)。 正規化的版本字串，並不包含組建中繼資料。 NuGet 生態系統中的所有版本，版本字串的比較是實作使用[SemVer 2.0.0's 版本優先順序規則](http://semver.org/spec/v2.0.0.html#spec-item-11)。

`parent`屬性才會顯示註冊頁面物件具有`items`屬性。

如果`items`屬性不存在於註冊頁面物件，在指定的 URL`@id`必須用來擷取個別的套件版本的相關中繼資料。 `items`陣列有時排除的頁面物件，做為最佳化。 如果在單一套件識別碼的版本數目非常大，則註冊索引文件會大量且浪費只關心特定版本或小範圍版本的用戶端的程序。

請注意，如果`items`屬性已存在，`@id`屬性不需使用，因為所有的頁面資料已內嵌在`items`屬性。

在頁面物件的每個項目`items`陣列是 JSON 物件，代表註冊分葉和與其相關聯的中繼資料。

#### <a name="registration-leaf-object-in-a-page"></a>註冊頁面中的分葉物件

在註冊頁面中找到註冊分葉物件具有下列屬性：

名稱           | 類型   | 必要 | 注意
-------------- | ------ | -------- | -----
@id            | 字串 | 是      | 要註冊的分葉的 URL
catalogEntry   | object | 是      | 包含套件中繼資料的類別目錄項目
packageContent | 字串 | 是      | 封裝內容 (.nupkg) URL

每個註冊的分葉物件代表與單一的套件版本相關聯的資料。

#### <a name="catalog-entry"></a>目錄項目

`catalogEntry`註冊分葉物件中的屬性具有下列屬性：

名稱                     | 類型                       | 必要 | 注意
------------------------ | -------------------------- | -------- | -----
@id                      | 字串                     | 是      | 要用來產生這個物件的文件的 URL
authors                  | 字串或字串陣列 | 否       | 
dependencyGroups         | 物件的陣列           | 否       | 封裝中，依目標 framework 的相依性
描述              | 字串                     | 否       | 
iconUrl                  | 字串                     | 否       | 
id                       | 字串                     | 是      | 封裝的識別碼
licenseUrl               | 字串                     | 否       |
licenseExpression        | 字串                     | 否       | 
列出的                   | boolean                    | 否       | 應視為列出如果不存在
minClientVersion         | 字串                     | 否       | 
projectUrl               | 字串                     | 否       | 
發行                | 字串                     | 否       | 字串，包含 ISO 8601 時間戳記的已發行套件
requireLicenseAcceptance | boolean                    | 否       | 
摘要                  | 字串                     | 否       | 
標記                     | 字串或字串陣列  | 否       | 
標題                    | 字串                     | 否       | 
版本                  | 字串                     | 是      | 正規化之後，完整的版本字串

封裝`version`屬性正規化後是完整的版本字串。 也就是說，SemVer 2.0.0 組建資料可能包含以下項目。

`dependencyGroups`屬性是代表套件中，依目標 framework 的相依性物件的陣列。 如果封裝有沒有相依性，`dependencyGroups`屬性遺漏，空的陣列，或`dependencies`的所有群組的屬性是空的或遺漏。

值`licenseExpression`屬性符合[NuGet 授權運算式語法](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)。

#### <a name="package-dependency-group"></a>封裝相依性群組

相依性群組的每個物件具有下列屬性：

名稱            | 類型             | 必要 | 注意
--------------- | ---------------- | -------- | -----
targetFramework | 字串           | 否       | 這些相依性都適用於目標 framework
相依性    | 物件的陣列 | 否       |

`targetFramework`字串會使用 NuGet 的.NET 程式庫所實作的格式[NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)。 如果沒有`targetFramework`指定，則套用至所有目標架構的相依性群組。

`dependencies`屬性是物件的陣列，每個都代表目前封裝的封裝相依性。

#### <a name="package-dependency"></a>封裝相依性

每個套件相依性具有下列屬性：

名稱         | 類型   | 必要 | 注意
------------ | ------ | -------- | -----
id           | 字串 | 是      | 封裝相依性識別碼
range        | object | 否       | 允許[版本範圍](../reference/package-versioning.md#version-ranges-and-wildcards)相依性
註冊 | 字串 | 否       | 此相依性的註冊索引 URL

如果`range`屬性已被排除，或空字串，用戶端應該預設版本範圍`(, )`。 也就被允許任何版本的相依性。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在此案例中，註冊索引會有內嵌的 [註冊] 頁面，因此若要擷取個別的套件版本的相關中繼資料所不需的任何額外的要求。

## <a name="registration-page"></a>註冊頁面

[註冊] 頁面包含註冊分葉。 要擷取註冊頁面的 URL 由`@id`中的屬性[註冊頁面物件](#registration-page-object)先前所述。

當`items`陣列中註冊索引未提供，HTTP GET 要求的`@id`值會傳回 JSON 文件有做為根物件。 物件具有下列屬性：

名稱   | 類型             | 必要 | 注意
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 註冊頁面 URL
count  | 整數          | 是      | 離開頁面中的註冊數目
項目  | 物件的陣列 | 是      | 註冊分葉和其關聯的中繼資料的陣列
較低  | 字串           | 是      | （含） 頁面中最低的 SemVer 2.0.0 版本
父代 | 字串           | 是      | 要註冊索引 URL
上限  | 字串           | 是      | （含） 頁面中最高的 SemVer 2.0.0 版本

註冊分葉物件的形狀是註冊索引相同[上述](#registration-leaf-object-in-a-page)。

## <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>註冊分葉

註冊分葉會包含為特定的套件識別碼和版本的相關資訊。 無法使用這份文件中的特定版本的相關中繼資料。 套件中繼資料應從提取[註冊索引](#registration-index)或[註冊頁面](#registration-page)（這使用探索到的註冊索引）。

擷取註冊分葉的 URL 取自`@id`註冊分葉物件註冊索引或註冊頁面中的屬性。

註冊分葉是與根物件具有下列屬性的 JSON 文件：

名稱           | 類型    | 必要 | 注意
-------------- | ------- | -------- | -----
@id            | 字串  | 是      | 要註冊的分葉的 URL
catalogEntry   | 字串  | 否       | 產生這些分葉的類別目錄項目 URL
列出的         | boolean | 否       | 應視為列出如果不存在
packageContent | 字串  | 否       | 封裝內容 (.nupkg) URL
發行      | 字串  | 否       | 字串，包含 ISO 8601 時間戳記的已發行套件
註冊   | 字串  | 否       | 要註冊索引 URL

> [!Note]
> 在 nuget.org 上，`published`值設定為當套件很未列出的 1900 年。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
