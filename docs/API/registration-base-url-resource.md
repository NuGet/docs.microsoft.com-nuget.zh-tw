---
title: "封裝中繼資料，NuGet API |Microsoft 文件"
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
description: "封裝註冊基底 URL 可讓您擷取有關封裝的中繼資料。"
keywords: "NuGet 的 API 套件中繼資料、 NuGet API 註冊，NuGet API 未列出的封裝"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c098d70d58011bad7f9829f0c95c87c1339dd362
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="package-metadata"></a>套件中繼資料

您可使用 NuGet V3 應用程式開發介面的套件來源上的 擷取可用的封裝的相關中繼資料。 此中繼資料可使用擷取`RegistrationsBaseUrl`資源中找到[服務索引](service-index.md)。

下找到的文件集合`RegistrationsBaseUrl`通常稱為 「 註冊 」 或 「 註冊 blob"。 在單一文件集`RegistrationsBaseUrl`稱為 「 登錄 hive"。 將登錄 hive 控制檔包含有關每個封裝可用套件來源上的所有中繼資料。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                     | 注意
------------------------------- | -----
RegistrationsBaseUrl            | 初版
RegistrationsBaseUrl/3.0.0-beta | 別名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 別名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzipped 回應
RegistrationsBaseUrl/3.6.0      | 包含 SemVer 2.0.0 的封裝

這代表三個相異的登錄 hive 控制檔適用於各種用戶端版本。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

不會壓縮這些註冊 (這表示會使用隱含`Content-Encoding: identity`)。 SemVer 2.0.0 的套件**排除**從此登錄區。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

使用壓縮這些註冊`Content-Encoding: gzip`。 SemVer 2.0.0 的套件**排除**從此登錄區。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

使用壓縮這些註冊`Content-Encoding: gzip`。 SemVer 2.0.0 的套件**包含**此登錄區中。
如需 SemVer 2.0.0 的詳細資訊，請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基礎 URL

下列應用程式開發介面的基底 URL 是值`@id`上述資源相關聯的屬性`@type`值。 下列文件預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。

## <a name="registration-index"></a>登錄索引

登錄資源群組封裝中繼資料的封裝識別碼。 您不可能要一次取得多個封裝識別碼的相關資料。 此資源會提供任何方法來探索的封裝識別碼。 而是用戶端會假設已經知道所需的封裝識別碼。 可用每個套件版本相關的中繼資料會因伺服器實作。 封裝註冊 blob 會有下列的階層式結構：

- **索引**： 套件中繼資料，並提供相同的封裝識別碼。 在來源上的所有封裝都共用的進入點
- **頁面**： 封裝版本的群組。 在網頁中的封裝版本的數目是由伺服器實作所定義。
- **分葉**： 特有的單一封裝版本的文件。

登錄索引的 URL 是可預測，並可判斷給定的封裝識別碼和註冊資源的用戶端`@id`從服務之索引的值。 註冊頁面和保留的 Url 會藉由檢查註冊索引探索。

### <a name="registration-pages-and-leaves"></a>註冊頁面和保留

雖然它不完全具有需要註冊分葉中個別登錄頁數的文件來儲存伺服器實作，它是建議的作法，以節省記憶體用戶端。 而不是內嵌的所有註冊會保留在索引或立即儲存分葉頁數的文件中，我們建議您的伺服器實作定義某個啟發學習法選擇在兩種方法為基礎的封裝版本數目或離開封裝的累計大小。

儲存所有的封裝版本 （分葉） 註冊索引會儲存在 HTTP 要求數不必擷取封裝中繼資料，但表示必須下載較大的文件，而且必須配置更多的用戶端記憶體。 相反地，如果伺服器實作立即儲存註冊保留，另一個頁面上的文件中，用戶端必須執行多個 HTTP 要求，以取得所需的資訊。

Nuget.org 使用如下所示的啟發學習法： 128 或多個版本的封裝時，中斷分葉頁面大小為 64。 如果有少於 128 個版本，所有內嵌都離開的登錄索引。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求參數

名稱     | In     | 類型    | 必要 | 注意
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼、 小寫

`LOWER_ID`值是小寫使用所實作的規則所需的封裝識別碼。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>回應

回應是 JSON 文件具有根物件，具有下列屬性：

名稱  | 類型             | 必要 | 注意
----- | ---------------- | -------- | -----
count | 整數          | 是      | 在索引中的註冊頁面數目
項目 | 物件的陣列 | 是      | 陣列的註冊頁面

索引物件的每個項目`items`陣列是代表註冊頁面的 JSON 物件。

#### <a name="registration-page-object"></a>註冊頁面物件

登錄索引中找到的註冊頁面物件具有下列屬性：

名稱   | 類型             | 必要 | 注意
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 要註冊頁面的 URL
count  | 整數          | 是      | 離開頁面中的註冊數目
項目  | 物件的陣列 | 否       | 註冊分葉和其關聯的中繼資料的陣列
較低  | 字串           | 是      | 最低 SemVer 2.0.0 版 （含） 頁面中
父代 | 字串           | 否       | 登錄索引 URL
上限  | 字串           | 是      | 最高 SemVer 2.0.0 版 （含） 頁面中

`lower`和`upper`時需要的特定頁面版本中繼資料的頁面物件的界限很有用。
這些界限可以用來擷取所需的唯一註冊頁面。 版本字串遵守[NuGet 的版本規則](../reference/package-versioning.md)。 正規化的版本字串，並不包含建置中繼資料。 NuGet 生態系統中的所有版本，版本字串的比較是實作使用[SemVer 2.0.0's 版本優先順序規則](http://semver.org/spec/v2.0.0.html#spec-item-11)。

`parent`屬性才會顯示註冊頁面物件具有`items`屬性。

如果`items`中註冊 page 物件沒有屬性，指定的 URL`@id`必須用來擷取個別的封裝版本的相關中繼資料。 `items`陣列有時排除最佳化的頁面物件。 如果在單一封裝識別碼的版本數目非常大，則登錄索引文件會大量且浪費只關心特定版本或版本的小範圍的用戶端的程序。

請注意，如果`items`屬性已存在，`@id`屬性不需使用，因為所有的頁面資料已內嵌在`items`屬性。

在頁面上物件的每個項目`items`陣列是一個代表登錄分葉的 JSON 物件與它相關聯的中繼資料。

#### <a name="registration-leaf-object-in-a-page"></a>註冊頁面中的分葉物件

註冊頁面中找到註冊分葉物件具有下列屬性：

名稱           | 類型   | 必要 | 注意
-------------- | ------ | -------- | -----
@id            | 字串 | 是      | 要註冊的分葉的 URL
catalogEntry   | object | 是      | 包含封裝的中繼資料的類別目錄項目
packageContent | 字串 | 是      | 封裝內容 (.nupkg) URL

每個註冊分葉物件表示的單一封裝版本相關聯的資料。

#### <a name="catalog-entry"></a>目錄項目

`catalogEntry`註冊分葉物件中的屬性具有下列屬性：

名稱                     | 類型                       | 必要 | 注意
------------------------ | -------------------------- | -------- | -----
@id                      | 字串                     | 是      | 要用來產生這個物件的文件的 URL
authors                  | 字串或字串陣列 | 否       | 
dependencyGroups         | 物件的陣列           | 否       | 封裝內容 (.nupkg) URL
描述              | 字串                     | 否       | 
iconUrl                  | 字串                     | 否       | 
id                       | 字串                     | 是      | 封裝的識別碼
licenseUrl               | 字串                     | 否       | 
列出的                   | boolean                    | 否       | 應視為列出如果不存在
minClientVersion         | 字串                     | 否       | 
projectUrl               | 字串                     | 否       | 
發行                | 字串                     | 否       | 字串，包含 ISO 8601 時間戳記的發佈封裝時
requireLicenseAcceptance | boolean                    | 否       | 
摘要                  | 字串                     | 否       | 
標記                     | 字串或字串陣列  | 否       | 
標題                    | 字串                     | 否       | 
版本                  | 字串                     | 是      | 封裝版本

`dependencyGroups`屬性是一個代表封裝中，依 目標 framework 的相依性物件的陣列。 如果封裝沒有相依性，`dependencyGroups`屬性遺漏，空的陣列，或`dependencies`的所有群組的屬性是空的或遺漏。

#### <a name="package-dependency-group"></a>封裝相依性群組

相依性群組的每個物件具有下列屬性：

名稱            | 類型             | 必要 | 注意
--------------- | ---------------- | -------- | -----
targetFramework | 字串           | 否       | 這些相依性適用於目標 framework
相依性    | 物件的陣列 | 否       |

`targetFramework`字串使用 NuGet 的.NET 程式庫所實作的格式[NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)。 如果沒有`targetFramework`指定，則適用於所有的目標架構的相依性群組。

`dependencies`屬性是物件的陣列，每個都代表目前封裝的封裝相依性。

#### <a name="package-dependency"></a>封裝的相依性

每個封裝相依性具有下列屬性：

名稱         | 類型   | 必要 | 注意
------------ | ------ | -------- | -----
id           | 字串 | 是      | 封裝相依性的識別碼
range        | object | 否       | 允許[版本範圍](../reference/package-versioning.md#version-ranges-and-wildcards)相依性
註冊 | 字串 | 否       | 此相依性的登錄索引 URL

如果`range`排除屬性或空字串，用戶端應該預設為版本範圍`(, )`。 也就被允許任何版本的相依性。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在此特定情況下，登錄索引都有內嵌的 [註冊] 頁面，因此不需要任何額外的要求使用來擷取個別的封裝版本的相關中繼資料。

## <a name="registration-page"></a>註冊頁面

[註冊] 頁面包含登錄的分葉。 要擷取註冊頁面的 URL 由`@id`屬性[註冊 page 物件](#registration-page-object)上面所述。

當`items`陣列未提供註冊索引中，HTTP GET 要求的`@id`會傳回 JSON 文件有做為根物件的值。 物件具有下列屬性：

名稱   | 類型             | 必要 | 注意
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 要註冊頁面的 URL
count  | 整數          | 是      | 離開頁面中的註冊數目
項目  | 物件的陣列 | 是      | 註冊分葉和其關聯的中繼資料的陣列
較低  | 字串           | 是      | 最低 SemVer 2.0.0 版 （含） 頁面中
父代 | 字串           | 是      | 登錄索引 URL
上限  | 字串           | 是      | 最高 SemVer 2.0.0 版 （含） 頁面中

註冊分葉物件的形狀是以相同的登錄索引[上方](#registration-leaf-object-in-a-page)。

## <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>註冊分葉

註冊分葉包含特定的封裝識別碼和版本資訊。 可能無法使用這份文件中的特定版本的相關中繼資料。 套件中繼資料應從提取[註冊索引](#registration-index)或[註冊頁面](#registration-page)（這使用探索到的登錄索引）。

擷取註冊分葉 URL 取自`@id`註冊分葉物件註冊索引或註冊頁面中的屬性。

註冊分葉是 JSON 文件的根物件，具有下列屬性：

名稱           | 類型    | 必要 | 注意
-------------- | ------- | -------- | -----
@id            | 字串  | 是      | 要註冊的分葉的 URL
catalogEntry   | 字串  | 否       | 產生這些分葉的類別目錄項目 URL
列出的         | boolean | 否       | 應視為列出如果不存在
packageContent | 字串  | 否       | 封裝內容 (.nupkg) URL
發行      | 字串  | 否       | 字串，包含 ISO 8601 時間戳記的發佈封裝時
註冊   | 字串  | 否       | 登錄索引 URL

> [!Note]
> 在 nuget.org，`published`值設為 1900 當套件很未列出的年份。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
