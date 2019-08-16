---
title: 套件中繼資料, NuGet API
description: 套件註冊基底 URL 可讓您提取有關封裝的中繼資料。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488309"
---
# <a name="package-metadata"></a>套件中繼資料

您可以使用 NuGet V3 API, 提取封裝來源上可用套件的相關中繼資料。 您可以使用在[服務索引](service-index.md)中`RegistrationsBaseUrl`找到的資源來提取此中繼資料。

在`RegistrationsBaseUrl`底下找到的檔集合通常稱為「註冊」或「註冊 blob」。 單一`RegistrationsBaseUrl`的檔集稱為「註冊 hive」。 註冊 hive 包含封裝來源上可用之每個套件的所有中繼資料。

## <a name="versioning"></a>版本控制

會使用`@type`下列值:

@type 值                     | 附註
------------------------------- | -----
RegistrationsBaseUrl            | 初始版本
RegistrationsBaseUrl/3.0.0-beta | 別名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 別名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzipped 回應
RegistrationsBaseUrl/3.6.0      | 包含 SemVer 2.0.0 套件

這代表適用于各種用戶端版本的三個不同註冊 hive。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

這些註冊不會壓縮 (也就是說, 它們會使用`Content-Encoding: identity`隱含的)。 此 hive 會**排除**SemVer 2.0.0 套件。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

這些註冊會使用`Content-Encoding: gzip`進行壓縮。 此 hive 會**排除**SemVer 2.0.0 套件。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

這些註冊會使用`Content-Encoding: gzip`進行壓縮。 SemVer 2.0.0 套件**包含**在此 hive 中。
如需 SemVer 2.0.0 的詳細資訊, 請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基礎 URL

下列 api 的基底 URL 是與上述資源`@id` `@type`值相關聯的屬性值。 在下列檔中, 將會使用預留位置`{@id}`基底 URL。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 url 都支援 HTTP `GET`方法`HEAD`和。

## <a name="registration-index"></a>註冊索引

註冊資源會依套件識別碼將套件中繼資料分組。 您一次無法取得一個以上套件識別碼的資料。 此資源不提供探索封裝識別碼的方式。 相反地, 用戶端會假設為已知道所需的套件識別碼。 有關每個套件版本的可用中繼資料會因伺服器的執行而異。 套件註冊 blob 具有下列階層式結構:

- **索引**: 套件中繼資料的進入點, 由來源上具有相同封裝識別碼的所有封裝共用。
- **Page**: 封裝版本的群組。 頁面中的封裝版本數目是由伺服器執行所定義。
- 分**葉**: 單一封裝版本特定的檔。

註冊索引的 URL 是可預測的, 而且可以由用戶端根據提供的套件識別碼和註冊資源的`@id`值, 由服務索引來決定。 藉由檢查註冊索引, 即可探索註冊頁面和葉子的 Url。

### <a name="registration-pages-and-leaves"></a>註冊頁面和離職

雖然伺服器執行不一定要將註冊葉子儲存在個別的註冊分頁檔中, 但建議您保留用戶端記憶體。 建議伺服器執行根據封裝版本的數目, 在兩種方法之間進行選擇, 而不是內嵌所有註冊, 或立即將葉儲存在分頁檔中。封裝保留的累計大小。

將所有套件版本 (葉子) 儲存在註冊索引中, 可節省提取套件中繼資料所需的 HTTP 要求數, 但也表示必須下載較大的檔, 而且必須配置更多的用戶端記憶體。 另一方面, 如果伺服器的執行會立即將註冊保存在個別的分頁檔中, 則用戶端必須執行更多的 HTTP 要求, 以取得所需的資訊。

Nuget.org 使用的啟發學習法如下: 如果有128或更多版本的封裝, 請將該分葉分成大小為64的頁面。 如果版本小於 128, 則內嵌全部都會留在註冊索引中。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求參數

名稱     | In     | 類型    | 必要 | 附註
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼, 小寫

`LOWER_ID`值是所需的套件識別碼小寫, 使用由所執行的規則。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>回應

回應是 JSON 檔, 其具有具有下列屬性的根物件:

名稱  | 類型             | 必要 | 附註
----- | ---------------- | -------- | -----
count | integer          | 是      | 索引中的註冊頁面數目
items | 物件的陣列 | 是      | 註冊頁面的陣列

索引物件`items`陣列中的每個專案都是代表註冊頁面的 JSON 物件。

#### <a name="registration-page-object"></a>註冊頁面物件

在註冊索引中找到的註冊頁面物件具有下列屬性:

名稱   | 類型             | 必要 | 附註
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 註冊頁面的 URL
count  | integer          | 是      | 頁面中的註冊保留數目
items  | 物件的陣列 | 否       | 註冊的陣列和其相關聯的中繼資料
零下  | 字串           | 是      | 頁面中最低的 SemVer 2.0.0 版本 (含)
父 | 字串           | 否       | 註冊索引的 URL
臨界  | 字串           | 是      | 頁面中最高的 SemVer 2.0.0 版本 (含)

當`lower`需要`upper`特定頁面版本的中繼資料時, page 物件的和界限會很有用。
這些界限可以用來提取唯一需要的註冊頁面。 版本字串會遵循[NuGet 的版本規則](../concepts/package-versioning.md)。 版本字串已正規化, 且不包含組建中繼資料。 與 NuGet 生態系統中的所有版本相同, 版本字串的比較會使用[SemVer 2.0.0 的版本優先順序規則](http://semver.org/spec/v2.0.0.html#spec-item-11)來執行。

只有`parent`在註冊頁面物件`items`具有屬性時, 才會出現屬性。

如果屬性不存在於註冊頁物件中, 則必須使用中指定的 URL `@id`來提取有關個別封裝版本的中繼資料。 `items` `items`陣列有時會從頁面物件排除以做為優化。 如果單一封裝識別碼的版本數目非常大, 則註冊索引檔對於只關心特定版本或小型版本的用戶端來說, 將會很龐大且浪費。

請注意, 如果`items`屬性存在, 則`@id`不需要使用屬性, 因為所有頁面資料`items`都已經內嵌在屬性中。

Page 物件`items`陣列中的每個專案都是一個 JSON 物件, 代表一個註冊分葉及其相關聯的中繼資料。

#### <a name="registration-leaf-object-in-a-page"></a>頁面中的註冊分葉物件

在註冊頁面中找到的註冊分葉物件具有下列屬性:

名稱           | 類型   | 必要 | 附註
-------------- | ------ | -------- | -----
@id            | 字串 | 是      | 註冊分葉的 URL
catalogEntry   | 物件 (object) | 是      | 包含封裝中繼資料的目錄專案
packageContent | 字串 | 是      | 封裝內容的 URL (. nupkg)

每個註冊分葉物件都代表與單一封裝版本相關聯的資料。

#### <a name="catalog-entry"></a>類別目錄專案

註冊`catalogEntry`分葉物件中的屬性具有下列屬性:

名稱                     | 類型                       | 必要 | 附註
------------------------ | -------------------------- | -------- | -----
@id                      | 字串                     | 是      | 用來產生此物件的檔 URL
authors                  | 字串或字串陣列 | 否       | 
dependencyGroups         | 物件的陣列           | 否       | 封裝的相依性 (依目標架構分組)
取代              | 物件 (object)                     | 否       | 與封裝相關聯的取代
描述              | 字串                     | 否       | 
iconUrl                  | 字串                     | 否       | 
id                       | 字串                     | 是      | 封裝的識別碼
licenseUrl               | 字串                     | 否       |
licenseExpression        | 字串                     | 否       | 
列出的                   | boolean                    | 否       | 如果不存在, 應視為列出
minClientVersion         | 字串                     | 否       | 
projectUrl               | 字串                     | 否       | 
發佈                | 字串                     | 否       | 字串, 包含發行封裝時的 ISO 8601 時間戳記
requireLicenseAcceptance | boolean                    | 否       | 
摘要                  | 字串                     | 否       | 
標記                     | 字串或字串陣列  | 否       | 
標題                    | 字串                     | 否       | 
版本                  | 字串                     | 是      | 正規化後的完整版本字串

在正規化`version`之後, package 屬性是完整的版本字串。 這表示您可以在此包含 SemVer 2.0.0 組建資料。

`dependencyGroups`屬性是物件的陣列, 代表封裝的相依性 (依目標 framework 分組)。 如果封裝沒有相依性, `dependencyGroups`就會遺漏屬性、空陣列, 或所有群組的`dependencies`屬性是空的或遺失。

`licenseExpression`屬性的值符合[NuGet 授權運算式語法](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)。

#### <a name="package-dependency-group"></a>封裝相依性群組

每個相依性群組物件都具有下列屬性:

名稱            | 類型             | 必要 | 注意
--------------- | ---------------- | -------- | -----
targetFramework | 字串           | 否       | 這些相依性適用的目標 framework
相依性    | 物件的陣列 | 否       |

此`targetFramework`字串會使用 nuget 的 .net 程式庫 nuget 所實作為的格式[。](https://www.nuget.org/packages/NuGet.Frameworks/) 如果未`targetFramework`指定, 則相依性群組會套用至所有目標 framework。

`dependencies`屬性是物件的陣列, 每個都代表目前封裝的封裝相依性。

#### <a name="package-dependency"></a>封裝相依性

每個封裝相依性都具有下列屬性:

名稱         | 類型   | 必要 | 附註
------------ | ------ | -------- | -----
id           | 字串 | 是      | 封裝相依性的識別碼
range        | 物件 (object) | 否       | 相關性的允許[版本範圍](../concepts/package-versioning.md#version-ranges-and-wildcards)
註冊 | 字串 | 否       | 此相依性的註冊索引 URL

如果已`range`排除此屬性或空字串, 則用戶端應該預設為版本範圍。 `(, )` 也就是允許任何版本的相依性。

#### <a name="package-deprecation"></a>套件淘汰

每個套件淘汰都具有下列屬性:

名稱             | 類型             | 必要 | 附註
---------------- | ---------------- | -------- | -----
描述          | 字串陣列 | 是      | 封裝被取代的原因
訊息          | 字串           | 否       | 此取代的其他詳細資料
alternatePackage | 物件 (object)           | 否       | 應改為使用的封裝相依性

`reasons`屬性必須包含至少一個字串, 而且應該只包含下表中的字串:

原因       | 說明             
------------ | -----------
舊版       | 不再維護封裝
CriticalBugs | 套件有 bug, 使其不適合使用
其他        | 套件因此清單中的原因而被取代

`reasons`如果屬性包含的字串不是來自已知的集合, 則應該予以忽略。 字串不區分大小寫, 因此`legacy`應視為與`Legacy`相同。 陣列上沒有排序限制, 因此可以任意順序排列字串。 此外, 如果屬性只包含不是來自已知集合的字串, 則應該將它視為只包含 "Other" 字串。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在此特殊情況下, 註冊索引會內嵌註冊頁面, 因此不需要額外的要求來取得個別封裝版本的中繼資料。

## <a name="registration-page"></a>註冊頁面

註冊頁面包含註冊保留。 提取註冊頁面的 URL 是由前述`@id` [註冊頁面物件](#registration-page-object)中的屬性所決定。

當註冊索引中未提供`@id` 陣列時,值的HTTPGET要求會傳回JSON檔,其中包含物件做為其根。`items` 物件具有下列屬性:

名稱   | 類型             | 必要 | 附註
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 註冊頁面的 URL
count  | integer          | 是      | 頁面中的註冊保留數目
items  | 物件的陣列 | 是      | 註冊的陣列和其相關聯的中繼資料
零下  | 字串           | 是      | 頁面中最低的 SemVer 2.0.0 版本 (含)
父 | 字串           | 是      | 註冊索引的 URL
臨界  | 字串           | 是      | 頁面中最高的 SemVer 2.0.0 版本 (含)

註冊分葉物件的形狀與[上述](#registration-leaf-object-in-a-page)註冊索引中的相同。

## <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>註冊分葉

註冊分葉包含特定套件識別碼和版本的相關資訊。 本檔中可能不會提供有關特定版本的中繼資料。 套件中繼資料應該從[註冊索引](#registration-index)或[註冊頁面](#registration-page)(使用註冊索引來探索) 提取。

提取註冊分葉的 URL 是從註冊索引或`@id`註冊頁面中註冊分葉物件的屬性取得。

註冊分葉是 JSON 檔, 具有具有下列屬性的根物件:

名稱           | 類型    | 必要 | 附註
-------------- | ------- | -------- | -----
@id            | 字串  | 是      | 註冊分葉的 URL
catalogEntry   | 字串  | 否       | 產生這些分葉之類別目錄專案的 URL
列出的         | boolean | 否       | 如果不存在, 應視為列出
packageContent | 字串  | 否       | 封裝內容的 URL (. nupkg)
發佈      | 字串  | 否       | 字串, 包含發行封裝時的 ISO 8601 時間戳記
註冊   | 字串  | 否       | 註冊索引的 URL

> [!Note]
> 在 nuget.org 上, `published`當封裝未列出時, 此值會設定為 year 1900。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
