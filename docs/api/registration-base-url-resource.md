---
title: 套件中繼資料，NuGet API
description: 套件註冊基底 URL 可讓您提取封裝的相關中繼資料。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 403686de42bf4dc1fa94b9dd92ca6d33f3be2183
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775296"
---
# <a name="package-metadata"></a>套件中繼資料

您可以使用 NuGet V3 API 來提取套件來源上可用套件的相關中繼資料。 您可以使用在 `RegistrationsBaseUrl` [服務索引](service-index.md)中找到的資源來提取此中繼資料。

在下方找到的檔集合 `RegistrationsBaseUrl` 通常稱為「註冊」或「註冊 blob」。 單一的檔集 `RegistrationsBaseUrl` 稱為「註冊 hive」。 註冊 hive 包含套件來源上可用之每個套件的所有中繼資料。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值                     | 備註
------------------------------- | -----
RegistrationsBaseUrl            | 初始版本
RegistrationsBaseUrl/3.0.0-Beta | 別名 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 別名 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4。0      | Gzipped 回應
RegistrationsBaseUrl/3.6。0      | 包括 SemVer 2.0.0 套件

這代表適用于各種用戶端版本的三個不同註冊 hive。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

這些註冊不會被壓縮 (也就是說，它們會使用隱含的 `Content-Encoding: identity`) 。 此 hive 會 **排除** SemVer 2.0.0 套件。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4。0

這些註冊會使用壓縮 `Content-Encoding: gzip` 。 此 hive 會 **排除** SemVer 2.0.0 套件。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6。0

這些註冊會使用壓縮 `Content-Encoding: gzip` 。 SemVer 2.0.0 封裝 **包含** 在此 hive 中。
如需 SemVer 2.0.0 的詳細資訊，請參閱 [nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基底 URL

下列 Api 的基底 URL 是 `@id` 與上述資源值相關聯之屬性的值 `@type` 。 在下列檔中，將會使用預留位置基底 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 Url 都支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="registration-index"></a>註冊索引

註冊資源會依封裝識別碼分組封裝中繼資料。 您無法一次取得多個封裝識別碼的相關資料。 此資源不會提供探索套件識別碼的方式。 相反地，用戶端會假設已經知道所需的套件識別碼。 每個套件版本的可用中繼資料會隨著伺服器的執行而有所不同。 套件註冊 blob 具有下列階層式結構：

- **Index**：套件中繼資料的進入點，由具有相同封裝識別碼之來源上的所有封裝所共用。
- **頁面**：套件版本的群組。 頁面中的套件版本數目是由伺服器執行所定義。
- 分 **葉**：適用于單一套件版本的檔。

註冊索引的 URL 是可預測的，且可由用戶端指定服務索引的封裝識別碼和註冊資源的 `@id` 值來決定。 註冊頁面和離開的 Url 會藉由檢查註冊索引來進行探索。

### <a name="registration-pages-and-leaves"></a>註冊頁面和離開

雖然將註冊葉子儲存在不同的註冊分頁檔中並非絕對必要，但為了節省用戶端的記憶體，建議您不要這麼做。 建議伺服器執行根據封裝版本的數目或封裝的累計大小，在這兩種方法之間進行選擇，而不是將所有註冊保留在索引中或立即儲存在分頁檔中。

將所有套件版本儲存 () 在註冊索引中，會節省提取套件中繼資料所需的 HTTP 要求數目，但表示必須下載較大的檔，而且必須配置更多的用戶端記憶體。 另一方面，如果伺服器實行立即將登錄保留在不同的分頁檔中，用戶端就必須執行更多的 HTTP 要求，才能取得所需的資訊。

Nuget.org 使用的啟發學習法如下：如果有128或更多版本的套件，請將分葉分成大小64的頁面。 如果版本低於128，則內嵌全都會放入註冊索引中。 請注意，這表示具有65至127版本的套件在索引中會有兩個頁面，但這兩個頁面將會內嵌。

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>要求參數

名稱     | 位於     | 類型    | 必要 | 備註
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼，小寫

此 `LOWER_ID` 值是所需的封裝識別碼小寫使用由所執行的規則。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) 方法。

### <a name="response"></a>回應

回應是 JSON 檔，其中包含具有下列屬性的根物件：

名稱  | 類型             | 必要 | 備註
----- | ---------------- | -------- | -----
count | 整數          | 是      | 索引中的註冊頁面數目
項目 | 物件的陣列 | 是      | 註冊頁面的陣列

索引物件陣列中的每個專案 `items` 都是代表註冊頁面的 JSON 物件。

#### <a name="registration-page-object"></a>註冊頁面物件

在註冊索引中找到的註冊頁面物件具有下列屬性：

名稱   | 類型             | 必要 | 備註
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 註冊頁面的 URL
count  | 整數          | 是      | 頁面中的註冊保留數目
項目  | 物件的陣列 | 不可以       | 註冊保留的陣列及其關聯中繼資料
lower  | 字串           | 是      | 頁面中最低的 SemVer 2.0.0 版本 (內含) 
父系 (parent) | 字串           | 不可以       | 註冊索引的 URL
upper  | 字串           | 是      | 頁面中最高的 SemVer 2.0.0 版本 (內含) 

`lower` `upper` 當需要特定頁面版本的中繼資料時，頁面物件的和界限會很有用。
這些界限可以用來提取唯一需要的註冊頁面。 版本字串會遵循 [NuGet 的版本規則](../concepts/package-versioning.md)。 版本字串是正規化的，不包含組建中繼資料。 如同 NuGet 生態系統中的所有版本，系統會使用 [SemVer 2.0.0 的版本優先順序規則](https://semver.org/spec/v2.0.0.html#spec-item-11)來執行版本字串的比較。

`parent`只有當註冊頁面物件具有屬性時，才會顯示此屬性 `items` 。

如果這個 `items` 屬性不存在於註冊頁面物件中，則必須使用在中指定的 URL `@id` 來提取個別套件版本的中繼資料。 `items`陣列有時會從頁面物件排除為優化。 如果單一封裝識別碼的版本數目很大，則註冊索引檔將會很龐大，而且對於只在意特定版本或較小版本的用戶端來說，將會浪費大量處理。

請注意，如果 `items` 屬性存在，就 `@id` 不需要使用屬性，因為所有的頁面資料都已經內嵌在 `items` 屬性中。

頁面物件之陣列中的每個專案 `items` 都是一個 JSON 物件，代表註冊分葉及其相關聯的中繼資料。

#### <a name="registration-leaf-object-in-a-page"></a>頁面中的註冊分葉物件

註冊頁面中找到的註冊分葉物件具有下列屬性：

名稱           | 類型   | 必要 | 備註
-------------- | ------ | -------- | -----
@id            | 字串 | 是      | 註冊分葉的 URL
catalogEntry   | 物件 (object) | 是      | 包含套件中繼資料的類別目錄專案
packageContent | 字串 | 是      | 封裝內容的 URL (. nupkg) 

每個註冊分葉物件都代表與單一套件版本相關聯的資料。

#### <a name="catalog-entry"></a>類別目錄專案

`catalogEntry`註冊分葉物件中的屬性具有下列屬性：

名稱                     | 類型                       | 必要 | 備註
------------------------ | -------------------------- | -------- | -----
@id                      | 字串                     | 是      | 用來產生此物件之檔的 URL
authors                  | 字串或字串陣列 | 不可以       | 
dependencyGroups         | 物件的陣列           | 不可以       | 封裝的相依性，依目標 framework 分組
折舊              | 物件 (object)                     | 不可以       | 與封裝相關聯的淘汰
description              | 字串                     | 不可以       | 
iconUrl                  | 字串                     | 不可以       | 
id                       | 字串                     | 是      | 封裝的識別碼
licenseUrl               | 字串                     | 不可以       |
licenseExpression        | 字串                     | 不可以       | 
列出的                   | boolean                    | 不可以       | 如果不存在，應視為已列出
minClientVersion         | 字串                     | 不可以       | 
projectUrl               | 字串                     | 不可以       | 
published                | 字串                     | 不可以       | 字串，包含發行套件時的 ISO 8601 時間戳記
requireLicenseAcceptance | boolean                    | 不可以       | 
總結                  | 字串                     | 不可以       | 
tags                     | 字串或字串陣列  | 不可以       | 
title                    | 字串                     | 不可以       | 
version                  | 字串                     | 是      | 正規化之後的完整版本字串

封裝 `version` 屬性是正規化之後的完整版本字串。 這表示 SemVer 2.0.0 組建資料可以包含在此。

`dependencyGroups`屬性是物件的陣列，代表封裝的相依性（依目標 framework 分組）。 如果封裝沒有相依性，則會 `dependencyGroups` 遺漏屬性、空的陣列，或 `dependencies` 所有群組的屬性是空的或遺失。

屬性的值 `licenseExpression` 符合 [NuGet 授權運算式語法](../reference/nuspec.md#license)。

> [!Note]
> 在 nuget.org 上， `published` 當封裝未列出時，此值會設定為1900年。

#### <a name="package-dependency-group"></a>套件相依性群組

每個相依性群組物件都具有下列屬性：

名稱            | 類型             | 必要 | 備註
--------------- | ---------------- | -------- | -----
targetFramework | 字串           | 不可以       | 這些相依性適用的目標 framework
相依性    | 物件的陣列 | 不可以       |

此 `targetFramework` 字串使用 nuget 的 .net 程式庫 [nuget](https://www.nuget.org/packages/NuGet.Frameworks/)所實行的格式。 如果未 `targetFramework` 指定，則會將相依性群組套用至所有目標 framework。

`dependencies`屬性是物件的陣列，每個物件都代表目前封裝的封裝相依性。

#### <a name="package-dependency"></a>套件相依性

每個套件相依性都有下列屬性：

名稱         | 類型   | 必要 | 注意
------------ | ------ | -------- | -----
id           | 字串 | 是      | 套件相依性的識別碼
range        | 物件 (object) | 不可以       | 允許的相依性[版本範圍](../concepts/package-versioning.md#version-ranges)
註冊 | 字串 | 不可以       | 此相依性之註冊索引的 URL

如果 `range` 屬性已排除或空白字串，用戶端應該預設為版本範圍 `(, )` 。 亦即，允許任何版本的相依性。 `*`屬性不允許的值 `range` 。

#### <a name="package-deprecation"></a>套件淘汰

每個套件淘汰都有下列屬性：

名稱             | 類型             | 必要 | 備註
---------------- | ---------------- | -------- | -----
原因          | 字串陣列 | 是      | 套件淘汰的原因
message          | 字串           | 不可以       | 此淘汰的其他詳細資料
alternatePackage | 物件 (object)           | 不可以       | 應改為使用的替代套件

`reasons`屬性必須包含至少一個字串，且只能包含下表中的字串：

原因       | 描述             
------------ | -----------
舊版       | 不再維護套件
CriticalBugs | 封裝有 bug，使其不適合使用
其他        | 因為此清單中沒有原因，所以套件已淘汰

如果 `reasons` 屬性包含的字串不是來自已知的集合，則應該予以忽略。 字串不區分大小寫，因此 `legacy` 應該將視為相同 `Legacy` 。 陣列上沒有順序限制，因此可以任意順序排列字串。 此外，如果屬性只包含不是來自已知集合的字串，則應該將它視為只包含 "Other" 字串。

#### <a name="alternate-package"></a>替代套件

替代封裝物件具有下列屬性：

名稱         | 類型   | 必要 | 注意
------------ | ------ | -------- | -----
id           | 字串 | 是      | 替代套件的識別碼
range        | 物件 (object) | 不可以       | 允許的 [版本範圍](../concepts/package-versioning.md#version-ranges)，或 `*` 允許的任何版本

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在此特定案例中，註冊索引會內嵌註冊頁面，因此不需要額外的要求來提取個別套件版本的相關中繼資料。

## <a name="registration-page"></a>[註冊] 窗格

註冊頁面包含註冊離開。 提取註冊頁面的 URL 取決於 `@id` 上述 [註冊頁面物件](#registration-page-object) 中的屬性。 URL 不能是可預測的，且應該一律透過索引檔來探索。

> [!Warning]
> 在 nuget.org 上，註冊分頁檔剛好的 URL 會包含頁面的下限和上限。 不過，用戶端永遠不應該這麼做，因為只要索引檔有有效的連結，伺服器執行就可以自由變更 URL 的形狀。

當 `items` 註冊索引中未提供陣列時，值的 HTTP GET 要求 `@id` 會傳回 JSON 檔，該檔的物件為其根目錄。 此物件具有下列屬性：

名稱   | 類型             | 必要 | 備註
------ | ---------------- | -------- | -----
@id    | 字串           | 是      | 註冊頁面的 URL
count  | 整數          | 是      | 頁面中的註冊保留數目
項目  | 物件的陣列 | 是      | 註冊保留的陣列及其關聯中繼資料
lower  | 字串           | 是      | 頁面中最低的 SemVer 2.0.0 版本 (內含) 
父系 (parent) | 字串           | 是      | 註冊索引的 URL
upper  | 字串           | 是      | 頁面中最高的 SemVer 2.0.0 版本 (內含) 

註冊分葉物件的形狀與 [上述](#registration-leaf-object-in-a-page)註冊索引中的形狀相同。

## <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json
```

## <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>註冊分葉

註冊分葉包含特定封裝識別碼和版本的相關資訊。 有關特定版本的中繼資料可能無法在本檔中使用。 封裝中繼資料應該從 [註冊索引](#registration-index) 或 [註冊頁面](#registration-page) 中提取， (使用註冊索引) 來探索。

提取註冊分葉的 URL 是從 `@id` 註冊索引或註冊頁面的註冊分葉物件的屬性取得。 和分頁檔一樣。 URL 不能是可預測的，且應該一律透過註冊頁面物件來探索。

> [!Warning]
> 在 nuget.org 上，註冊分葉檔剛好的 URL 會包含套件版本。 不過，用戶端永遠不應該這麼做，因為只要父檔有有效的連結，伺服器執行就可以自由變更 URL 的形狀。 

註冊分葉是 JSON 檔，其中包含具有下列屬性的根物件：

名稱           | 類型    | 必要 | 備註
-------------- | ------- | -------- | -----
@id            | 字串  | 是      | 註冊分葉的 URL
catalogEntry   | 字串  | 不可以       | 產生這些分葉的目錄專案 URL
列出的         | boolean | 不可以       | 如果不存在，應視為已列出
packageContent | 字串  | 不可以       | 封裝內容的 URL (. nupkg) 
published      | 字串  | 不可以       | 字串，包含發行套件時的 ISO 8601 時間戳記
註冊   | 字串  | 不可以       | 註冊索引的 URL

> [!Note]
> 在 nuget.org 上， `published` 當封裝未列出時，此值會設定為1900年。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
