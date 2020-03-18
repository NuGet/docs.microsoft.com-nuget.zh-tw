---
title: 套件中繼資料，NuGet API
description: 套件註冊基底 URL 可讓您提取有關封裝的中繼資料。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 852dca8c70b09d941e844b1f7cd03b38e2192481
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428727"
---
# <a name="package-metadata"></a>套件中繼資料

您可以使用 NuGet V3 API，提取封裝來源上可用套件的相關中繼資料。 您可以使用在[服務索引](service-index.md)中找到的 `RegistrationsBaseUrl` 資源來提取此中繼資料。

在 `RegistrationsBaseUrl` 下找到的檔集合通常稱為「註冊」或「註冊 blob」。 單一 `RegistrationsBaseUrl` 下的檔集稱為「註冊 hive」。 註冊 hive 包含封裝來源上可用之每個套件的所有中繼資料。

## <a name="versioning"></a>版本控制

會使用下列 `@type` 值：

@type 值                     | 注意事項
------------------------------- | -----
RegistrationsBaseUrl            | 初始版本
RegistrationsBaseUrl/3.0.0-搶鮮版（Beta） | `RegistrationsBaseUrl` 的別名
RegistrationsBaseUrl/3.0.0-rc   | `RegistrationsBaseUrl` 的別名
RegistrationsBaseUrl/3.4。0      | Gzipped 回應
RegistrationsBaseUrl/3.6。0      | 包含 SemVer 2.0.0 套件

這代表適用于各種用戶端版本的三個不同註冊 hive。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

這些註冊不會壓縮（表示它們使用隱含的 `Content-Encoding: identity`）。 此 hive 會**排除**SemVer 2.0.0 套件。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4。0

這些註冊會使用 `Content-Encoding: gzip`進行壓縮。 此 hive 會**排除**SemVer 2.0.0 套件。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6。0

這些註冊會使用 `Content-Encoding: gzip`進行壓縮。 SemVer 2.0.0 套件**包含**在此 hive 中。
如需 SemVer 2.0.0 的詳細資訊，請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基礎 URL

下列 Api 的基底 URL 是與前述資源 `@type` 值相關聯 `@id` 屬性的值。 在下列檔中，將會使用預留位置基底 URL `{@id}`。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 Url 都支援 `GET` 和 `HEAD`的 HTTP 方法。

## <a name="registration-index"></a>註冊索引

註冊資源會依套件識別碼將套件中繼資料分組。 您一次無法取得一個以上套件識別碼的資料。 此資源不提供探索封裝識別碼的方式。 相反地，用戶端會假設為已知道所需的套件識別碼。 有關每個套件版本的可用中繼資料會因伺服器的執行而異。 套件註冊 blob 具有下列階層式結構：

- **索引**：套件中繼資料的進入點，由來源上具有相同封裝識別碼的所有封裝共用。
- **Page**：封裝版本的群組。 頁面中的封裝版本數目是由伺服器執行所定義。
- 分**葉**：單一封裝版本特定的檔。

註冊索引的 URL 是可預測的，而且可以由用戶端根據服務索引中的「套件識別碼」和「註冊資源」 `@id` 值來判斷。 藉由檢查註冊索引，即可探索註冊頁面和葉子的 Url。

### <a name="registration-pages-and-leaves"></a>註冊頁面和離職

雖然伺服器執行不一定要將註冊葉子儲存在個別的註冊分頁檔中，但建議您保留用戶端記憶體。 建議伺服器執行根據封裝版本的數目，在兩種方法之間進行選擇，而不是內嵌所有註冊，或立即將葉儲存在分頁檔中。封裝保留的累計大小。

將所有套件版本（葉子）儲存在註冊索引中，可節省提取套件中繼資料所需的 HTTP 要求數，但也表示必須下載較大的檔，而且必須配置更多的用戶端記憶體。 另一方面，如果伺服器的執行會立即將註冊保存在個別的分頁檔中，則用戶端必須執行更多的 HTTP 要求，以取得所需的資訊。

Nuget.org 使用的啟發學習法如下：如果有128或更多版本的封裝，請將該分葉分成大小為64的頁面。 如果版本小於128，則內嵌全部都會留在註冊索引中。 請注意，這表示具有65到127版本的套件會在索引中有兩個頁面，但這兩個頁面將會內嵌。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求參數

名稱     | 在     | 類型    | 必要項 | 注意事項
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 是      | 封裝識別碼，小寫

`LOWER_ID` 值是使用所執行之規則所需的套件識別碼小寫。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>回應

回應是 JSON 檔，其具有具有下列屬性的根物件：

名稱  | 類型             | 必要項 | 注意事項
----- | ---------------- | -------- | -----
count | integer          | 是      | 索引中的註冊頁面數目
項目 | 物件的陣列 | 是      | 註冊頁面的陣列

索引物件的 `items` 陣列中的每個專案都是代表註冊頁面的 JSON 物件。

#### <a name="registration-page-object"></a>註冊頁面物件

在註冊索引中找到的註冊頁面物件具有下列屬性：

名稱   | 類型             | 必要項 | 注意事項
------ | ---------------- | -------- | -----
@id    | string           | 是      | 註冊頁面的 URL
count  | integer          | 是      | 頁面中的註冊保留數目
項目  | 物件的陣列 | no       | 註冊的陣列和其相關聯的中繼資料
lower  | string           | 是      | 頁面中最低的 SemVer 2.0.0 版本（含）
父系 (parent) | string           | no       | 註冊索引的 URL
upper  | string           | 是      | 頁面中最高的 SemVer 2.0.0 版本（含）

當需要特定頁面版本的中繼資料時，page 物件的 `lower` 和 `upper` 界限會很有用。
這些界限可以用來提取唯一需要的註冊頁面。 版本字串會遵循[NuGet 的版本規則](../concepts/package-versioning.md)。 版本字串已正規化，且不包含組建中繼資料。 與 NuGet 生態系統中的所有版本相同，版本字串的比較會使用[SemVer 2.0.0 的版本優先順序規則](https://semver.org/spec/v2.0.0.html#spec-item-11)來執行。

只有當註冊頁面物件具有 `items` 屬性時，才會出現 `parent` 屬性。

如果 `items` 屬性不存在於註冊頁物件中，則必須使用 `@id` 中指定的 URL 來提取有關個別封裝版本的中繼資料。 從頁面物件中，有時會將 `items` 陣列排除為優化。 如果單一封裝識別碼的版本數目非常大，則註冊索引檔對於只關心特定版本或小型版本的用戶端來說，將會很龐大且浪費。

請注意，如果 `items` 屬性存在，就不需要使用 `@id` 屬性，因為所有頁面資料都已經內嵌在 `items` 屬性中。

Page 物件的 `items` 陣列中的每個專案都是一個 JSON 物件，代表一個註冊分葉及其相關聯的中繼資料。

#### <a name="registration-leaf-object-in-a-page"></a>頁面中的註冊分葉物件

在註冊頁面中找到的註冊分葉物件具有下列屬性：

名稱           | 類型   | 必要項 | 注意事項
-------------- | ------ | -------- | -----
@id            | string | 是      | 註冊分葉的 URL
catalogEntry   | object | 是      | 包含封裝中繼資料的目錄專案
packageContent | string | 是      | 封裝內容的 URL （. nupkg）

每個註冊分葉物件都代表與單一封裝版本相關聯的資料。

#### <a name="catalog-entry"></a>類別目錄專案

註冊分葉物件中的 `catalogEntry` 屬性具有下列屬性：

名稱                     | 類型                       | 必要項 | 注意事項
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | 是      | 用來產生此物件之檔的 URL
authors                  | 字串或字串陣列 | no       | 
dependencyGroups         | 物件的陣列           | no       | 封裝的相依性（依目標架構分組）
取代              | object                     | no       | 與封裝相關聯的取代
description              | string                     | no       | 
iconUrl                  | string                     | no       | 
id                       | string                     | 是      | 封裝的識別碼
licenseUrl               | string                     | no       |
licenseExpression        | string                     | no       | 
列出的                   | boolean                    | no       | 如果不存在，應視為列出
minClientVersion         | string                     | no       | 
projectUrl               | string                     | no       | 
published                | string                     | no       | 字串，包含發行封裝時的 ISO 8601 時間戳記
requireLicenseAcceptance | boolean                    | no       | 
摘要                  | string                     | no       | 
tags                     | 字串或字串陣列  | no       | 
title                    | string                     | no       | 
版本                  | string                     | 是      | 正規化後的完整版本字串

封裝 `version` 屬性是正規化之後的完整版本字串。 這表示您可以在此包含 SemVer 2.0.0 組建資料。

`dependencyGroups` 屬性是物件的陣列，代表封裝的相依性（依目標 framework 分組）。 如果封裝沒有相依性，就會遺漏 `dependencyGroups` 屬性、空陣列，或所有群組的 `dependencies` 屬性是空的或遺失。

`licenseExpression` 屬性的值符合[NuGet 授權運算式語法](../reference/nuspec.md#license)。

> [!Note]
> 在 nuget.org 上，當封裝未列出時，`published` 值會設為 year 1900。

#### <a name="package-dependency-group"></a>封裝相依性群組

每個相依性群組物件都具有下列屬性：

名稱            | 類型             | 必要項 | 注意事項
--------------- | ---------------- | -------- | -----
targetFramework | string           | no       | 這些相依性適用的目標 framework
相依性    | 物件的陣列 | no       |

`targetFramework` 字串使用 NuGet 的 .NET 程式庫 Nuget 所實的格式[。 framework](https://www.nuget.org/packages/NuGet.Frameworks/)。 如果未指定 `targetFramework`，則相依性群組會套用至所有目標 framework。

`dependencies` 屬性是物件的陣列，每個都代表目前封裝的封裝相依性。

#### <a name="package-dependency"></a>封裝相依性

每個封裝相依性都具有下列屬性：

名稱         | 類型   | 必要項 | 注意事項
------------ | ------ | -------- | -----
id           | string | 是      | 封裝相依性的識別碼
range        | object | no       | 相關性的允許[版本範圍](../concepts/package-versioning.md#version-ranges)
註冊 | string | no       | 此相依性的註冊索引 URL

如果 `range` 屬性已排除或為空字串，則用戶端應該預設為 `(, )`的版本範圍。 也就是允許任何版本的相依性。 `range` 屬性不允許 `*` 的值。

#### <a name="package-deprecation"></a>套件淘汰

每個套件淘汰都具有下列屬性：

名稱             | 類型             | 必要項 | 注意事項
---------------- | ---------------- | -------- | -----
描述          | 字串的陣列 | 是      | 封裝被取代的原因
message          | string           | no       | 此取代的其他詳細資料
alternatePackage | object           | no       | 應改為使用的替代套件

`reasons` 屬性必須包含至少一個字串，而且應該只包含下表中的字串：

原因       | 描述             
------------ | -----------
舊版       | 不再維護封裝
CriticalBugs | 套件有 bug，使其不適合使用
其他        | 套件因此清單中的原因而被取代

如果 `reasons` 屬性包含的字串不是來自已知的集合，則應該予以忽略。 字串不區分大小寫，因此 `legacy` 的處理方式應該與 `Legacy`相同。 陣列上沒有排序限制，因此可以任意順序排列字串。 此外，如果屬性只包含不是來自已知集合的字串，則應該將它視為只包含 "Other" 字串。

#### <a name="alternate-package"></a>替代套件

替代封裝物件具有下列屬性：

名稱         | 類型   | 必要項 | 注意事項
------------ | ------ | -------- | -----
id           | string | 是      | 替代套件的識別碼
range        | object | no       | 允許的[版本範圍](../concepts/package-versioning.md#version-ranges)，或 `*` （如果允許任何版本）

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在此特殊情況下，註冊索引會內嵌註冊頁面，因此不需要額外的要求來取得個別封裝版本的中繼資料。

## <a name="registration-page"></a>[註冊] 窗格

註冊頁面包含註冊保留。 提取註冊頁面的 URL 是由前述[註冊頁面物件](#registration-page-object)中的 `@id` 屬性所決定。 此 URL 不應該是可預測的，而且應該一律透過索引檔來探索。

> [!Warning]
> 在 nuget.org 上，註冊分頁檔且剛好的 URL 包含頁面的下限和上限。 不過，這項假設永遠不會由用戶端進行，因為只要索引檔有有效的連結，伺服器可自由變更 URL 的形狀。

當註冊索引中未提供 `items` 陣列時，`@id` 值的 HTTP GET 要求會傳回 JSON 檔，其中包含物件做為其根。 物件具有下列屬性：

名稱   | 類型             | 必要項 | 注意事項
------ | ---------------- | -------- | -----
@id    | string           | 是      | 註冊頁面的 URL
count  | integer          | 是      | 頁面中的註冊保留數目
項目  | 物件的陣列 | 是      | 註冊的陣列和其相關聯的中繼資料
lower  | string           | 是      | 頁面中最低的 SemVer 2.0.0 版本（含）
父系 (parent) | string           | 是      | 註冊索引的 URL
upper  | string           | 是      | 頁面中最高的 SemVer 2.0.0 版本（含）

註冊分葉物件的形狀與[上述](#registration-leaf-object-in-a-page)註冊索引中的相同。

## <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>註冊分葉

註冊分葉包含特定套件識別碼和版本的相關資訊。 本檔中可能不會提供有關特定版本的中繼資料。 套件中繼資料應該從[註冊索引](#registration-index)或[註冊頁面](#registration-page)（使用註冊索引來探索）提取。

提取註冊分葉的 URL 是從註冊索引或註冊頁面中註冊分葉物件的 `@id` 屬性取得。 如同分頁檔。 此 URL 不應該是可預測的，而且應該一律透過註冊頁面物件來探索。

> [!Warning]
> 在 nuget.org 上，註冊分葉檔且剛好的 URL 會包含套件版本。 不過，這項假設永遠不會由用戶端進行，因為只要父檔具有有效的連結，伺服器的執行就可以自由變更 URL 的形狀。 

註冊分葉是 JSON 檔，具有具有下列屬性的根物件：

名稱           | 類型    | 必要項 | 注意事項
-------------- | ------- | -------- | -----
@id            | string  | 是      | 註冊分葉的 URL
catalogEntry   | string  | no       | 產生這些分葉之類別目錄專案的 URL
列出的         | boolean | no       | 如果不存在，應視為列出
packageContent | string  | no       | 封裝內容的 URL （. nupkg）
published      | string  | no       | 字串，包含發行封裝時的 ISO 8601 時間戳記
註冊   | string  | no       | 註冊索引的 URL

> [!Note]
> 在 nuget.org 上，當封裝未列出時，`published` 值會設為 year 1900。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
