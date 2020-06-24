---
title: 目錄資源，NuGet V3 API
description: 目錄是在 nuget.org 上建立和刪除的所有套件的索引。
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ffbcb8dc18542f39c32a6d84b279c8eccaf98fc3
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292305"
---
# <a name="catalog"></a>目錄

**目錄**是記錄封裝來源上所有封裝作業的資源，例如建立和刪除。 目錄資源在 `Catalog` [服務索引](service-index.md)中具有類型。 您可以使用此資源來[查詢所有已發行的封裝](../guides/api/query-for-all-published-packages.md)。

> [!Note]
> 因為官方 NuGet 用戶端不會使用此目錄，所以並非所有的封裝來源都會執行目錄。

> [!Note]
> 目前，nuget.org 目錄無法在中國使用。 如需詳細資訊，請參閱[NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949)。

## <a name="versioning"></a>版本控制

`@type`會使用下列值：

@type 值   | 備註
------------- | -----
目錄/3.0。0 | 初始版本

## <a name="base-url"></a>基底 URL

下列 Api 的進入點 URL 是 `@id` 與上述資源值相關聯的屬性值 `@type` 。 本主題使用預留位置 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

在目錄資源中找到的所有 Url 僅支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="catalog-index"></a>目錄索引

目錄索引是已知位置中的一份檔，其中包含類別目錄專案的清單，並依序排序。 這是目錄資源的進入點。

索引是由目錄頁面所組成。 每個類別目錄頁面都包含類別目錄專案。 每個類別目錄專案代表一個時間點的單一封裝相關事件。 類別目錄專案可以代表從封裝來源建立、列出、重新列入或刪除的封裝。 藉由依時間連續處理類別目錄專案，用戶端可以建立在 V3 套件來源上的每個套件的最新觀點。

簡言之，目錄 blob 具有下列階層式結構：

- **Index**：目錄的進入點。
- **Page**：目錄專案的群組。
- 分**葉**：代表類別目錄專案的檔，這是單一封裝狀態的快照集。

每個目錄物件都有一個稱為的屬性， `commitTimeStamp` 代表將專案新增至目錄的時間。 類別目錄專案會以批次的方式新增至目錄頁面，稱為 commit。 相同認可中的所有目錄專案都具有相同的認可時間戳記（ `commitTimeStamp` ）和認可識別碼（ `commitId` ）。 放在相同認可中的類別目錄專案代表在封裝來源上的相同時間點所發生的事件。 目錄認可中沒有排序。

因為每個套件識別碼和版本都是唯一的，所以在認可中永遠不會有一個以上的目錄專案。 這可確保單一封裝的類別目錄專案一律可以根據認可時間戳記明確地排序。

針對每個目錄，一律不會有一個以上的認可 `commitTimeStamp` 。 換句話說， `commitId` 是的多餘的 `commitTimeStamp` 。

相較于套件識別碼所編制索引的[封裝中繼資料資源](registration-base-url-resource.md)，目錄只會依時間編制索引（並可查詢）。

類別目錄專案一律會以單純遞增的時間順序新增至目錄。 這表示，如果在時間 X 加入目錄認可，則不會在時間小於或等於 X 時加入任何目錄認可。

下列要求會提取目錄索引。

    GET {@id}

目錄索引是一份 JSON 檔，其中包含具有下列屬性的物件：

名稱            | 類型             | 必要 | 備註
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 與最近認可相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 最近認可的時間戳記
count           | integer          | 是      | 索引中的頁面數目
項目           | 物件的陣列 | 是      | 物件的陣列，每個物件都代表一個頁面

陣列中的每個元素 `items` 都是一個物件，其中每個頁面都有一些最小的詳細資料。 這些頁面物件不包含目錄離開（items）。 未定義此陣列中的元素順序。 頁面可以使用其屬性，以記憶體中的用戶端排序 `commitTimeStamp` 。

引進新的頁面時， `count` 將會遞增，而且陣列中會出現新的物件 `items` 。

當專案加入至目錄時，索引的 `commitId` 會變更，而且 `commitTimeStamp` 將會增加。 這兩個屬性基本上是陣列中所有頁面 `commitId` 和 `commitTimeStamp` 值的摘要 `items` 。

### <a name="catalog-page-object-in-the-index"></a>索引中的類別目錄頁面物件

在目錄索引的屬性中找到的目錄頁面物件 `items` 具有下列屬性：

名稱            | 類型    | 必要 | 備註
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | [抓取目錄的 URL] 頁面
commitId        | 字串  | 是      | 與此頁面中最新認可相關聯的唯一識別碼
commitTimeStamp | 字串  | 是      | 此頁面中最新認可的時間戳記
count           | integer | 是      | [目錄] 頁面中的專案數

與[套件中繼資料資源](registration-base-url-resource.md)不同的是，在某些情況下，內嵌會保留在索引中，目錄保留永遠不會內嵌到索引中，而且一律必須使用頁面的 URL 來提取 `@id` 。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>目錄頁面

[類別目錄] 頁面是目錄專案的集合。 這是使用 `@id` 目錄索引中找到的其中一個值所提取的檔。 目錄頁面的 URL 不適合作為可預測，而且應該只使用目錄索引來探索。

新的類別目錄專案會以最高的認可時間戳記或新的頁面，新增至目錄索引中的頁面。 一旦將具有較高認可時間戳記的頁面加入至目錄，就永遠不會新增或變更較舊的頁面。

目錄分頁檔是具有下列屬性的 JSON 物件：

名稱            | 類型             | 必要 | 備註
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 與此頁面中最新認可相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 此頁面中最新認可的時間戳記
count           | integer          | 是      | 頁面中的專案數
項目           | 物件的陣列 | 是      | 此頁面中的類別目錄專案
父系 (parent)          | 字串           | 是      | 目錄索引的 URL

陣列中的每個元素 `items` 都是一個物件，其中包含有關目錄專案的一些最少詳細資料。 這些專案物件不包含所有目錄專案的資料。 未定義頁面陣列中的專案順序 `items` 。 專案可以使用其屬性，以記憶體中的用戶端排序 `commitTimeStamp` 。

頁面中的目錄專案數是由伺服器執行所定義。 在 nuget.org 中，每個頁面中最多有550個專案，但某些頁面的實際數目可能會較小，這取決於時間點下一個認可批次的大小。

引進新的專案時， `count` 會遞增，而且陣列中會出現新的類別目錄專案物件 `items` 。

當專案加入至頁面時，所 `commitId` 做的變更和 `commitTimeStamp` 都會增加。 這兩個屬性基本上是 `commitId` 陣列中所有和 `commitTimeStamp` 值的摘要 `items` 。

### <a name="catalog-item-object-in-a-page"></a>頁面中的類別目錄專案物件

在 [類別目錄] 頁面的屬性中找到的類別目錄專案物件 `items` 具有下列屬性：

名稱            | 類型    | 必要 | 備註
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | 用來提取目錄專案的 URL
@type           | 字串  | 是      | 目錄專案的類型
commitId        | 字串  | 是      | 與此目錄專案相關聯的認可識別碼
commitTimeStamp | 字串  | 是      | 此類別目錄專案的認可時間戳記
nuget：識別碼        | 字串  | 是      | 此分葉相關的封裝識別碼
nuget：版本   | 字串  | 是      | 此分葉相關的封裝版本

`@type`值會是下列兩個值的其中一個：

1. `nuget:PackageDetails`：這會對應到 `PackageDetails` 目錄分葉檔中的類型。
1. `nuget:PackageDelete`：這會對應到 `PackageDelete` 目錄分葉檔中的類型。

如需每種類型意義的詳細資訊，請參閱下面的[對應專案類型](#item-types)。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>目錄分葉

目錄分葉包含特定封裝識別碼和版本在某個時間點的相關中繼資料。 這是使用 `@id` 在目錄頁面中找到的值所提取的檔。 目錄分葉的 URL 不適合做為可預測，而且應該只使用目錄頁面來探索。

目錄分葉檔是具有下列屬性的 JSON 物件：

名稱                    | 類型                       | 必要 | 備註
----------------------- | -------------------------- | -------- | -----
@type                   | 字串或字串陣列 | 是      | 類別目錄專案的類型
目錄： commitId        | 字串                     | 是      | 與此目錄專案相關聯的認可識別碼
目錄： commitTimeStamp | 字串                     | 是      | 此類別目錄專案的認可時間戳記
id                      | 字串                     | 是      | 目錄專案的封裝識別碼
published               | 字串                     | 是      | 封裝目錄專案的發行日期
version                 | 字串                     | 是      | 目錄專案的封裝版本

### <a name="item-types"></a>專案類型

`@type`屬性是字串或字串陣列。 為了方便起見，如果此 `@type` 值為字串，則應該將它視為任何大小為1的陣列。 並非所有的可能值 `@type` 都會記載。 不過，每個類別目錄專案都只有下列兩個字串類型值的其中一個：

1. `PackageDetails`：代表封裝中繼資料的快照集
1. `PackageDelete`：代表已刪除的封裝

### <a name="package-details-catalog-items"></a>封裝詳細資料目錄專案

類型為的類別目錄專案 `PackageDetails` 包含特定封裝（識別碼和版本組合）之套件中繼資料的快照集。 封裝詳細資料目錄專案會在封裝來源遇到下列任何案例時產生：

1. 封裝已**推送**。
1. 會**列出**封裝。
1. 封裝未**列出**。
1. 封裝為**reflowed**。

套件重新排列是一種系統管理手勢，基本上會產生現有封裝的假推送，而不會變更封裝本身。 在 nuget.org 上，在使用類別目錄的其中一個背景工作中修正 bug 之後，會使用「重排」。

使用類別目錄專案的用戶端不應該嘗試判斷哪些情況會產生類別目錄專案。 相反地，用戶端應該只使用目錄專案中包含的中繼資料來更新任何維護的 view 或 index。 此外，您應該以正常方式處理重複或多餘的類別目錄專案（不斷）。

除了[所有目錄中包含](#catalog-leaf)的屬性以外，套件詳細資料類別目錄專案還有下列屬性。

名稱                    | 類型                       | 必要 | 備註
----------------------- | -------------------------- | -------- | -----
authors                 | 字串                     | 否       |
created                 | 字串                     | 否       | 第一次建立封裝時的時間戳記。 Fallback 屬性： `published` 。
dependencyGroups        | 物件的陣列           | 否       | 封裝的相依性，依目標 framework （與[套件中繼資料資源相同的格式](registration-base-url-resource.md#package-dependency-group)）分組
取代             | 物件 (object)                     | 否       | 與封裝相關聯的取代（與[套件中繼資料資源相同的格式](registration-base-url-resource.md#package-deprecation)）
description             | 字串                     | 否       |
iconUrl                 | 字串                     | 否       |
isPrerelease            | boolean                    | 否       | 封裝版本是否為發行前版本。 可以從偵測到 `version` 。
語言                | 字串                     | 否       |
licenseUrl              | 字串                     | 否       |
列出的                  | boolean                    | 否       | 是否列出封裝
minClientVersion        | 字串                     | 否       |
packageHash             | 字串                     | 是      | 封裝的雜湊，使用[標準基底 64](https://tools.ietf.org/html/rfc4648#section-4)進行編碼
packageHashAlgorithm    | 字串                     | 是      |
packageSize             | integer                    | 是      | 封裝的大小。 nupkg （位元組）
packageTypes            | 物件的陣列           | 否       | 作者指定的封裝類型。
projectUrl              | 字串                     | 否       |
releaseNotes            | 字串                     | 否       |
requireLicenseAgreement | boolean                    | 否       | 假設 `false` 是否已排除
summary                 | 字串                     | 否       |
tags                    | 字串陣列           | 否       |
title                   | 字串                     | 否       |
verbatimVersion         | 字串                     | 否       | 原始在 nuspec 中找到的版本字串。

在正規化 `version` 之後，package 屬性是完整的版本字串。 這表示您可以在此包含 SemVer 2.0.0 組建資料。

`created`時間戳記是封裝來源第一次收到套件時，通常是在目錄專案的認可時間戳記之前的短時間。

`packageHashAlgorithm`是伺服器執行所定義的字串，代表用來產生的雜湊演算法 `packageHash` 。 nuget.org 一律使用的 `packageHashAlgorithm` 值 `SHA512` 。

`packageTypes`只有當作者指定了套件類型時，才會出現屬性。 如果存在，則一律會有至少一個（1）專案。 陣列中的每個專案 `packageTypes` 都是具有下列屬性的 JSON 物件：

Name      | 類型    | 必要 | 注意
--------- | ------- | -------- | -----
NAME      | 字串  | 是      | 封裝類型的名稱。
version    | 字串  | 否       | 封裝類型的版本。 只有在作者明確指定了 nuspec 中的版本時才會出現。

`published`時間戳記是上次列出封裝的時間。

> [!Note]
> 在 nuget.org 上， `published` 當封裝未列出時，此值會設定為1900年。

#### <a name="sample-request"></a>範例要求

GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>封裝刪除類別目錄專案

類型為的類別目錄專案 `PackageDelete` 包含一組最小的資訊，指出已從封裝來源刪除封裝，且不再適用于任何封裝作業（例如還原）的用戶端類別目錄。

> [!NOTE]
> 封裝可能會遭到刪除，並在稍後使用相同的套件識別碼和版本重新發佈。 在 nuget.org 上，這是非常罕見的情況，因為它會違反官方用戶端的假設套件識別碼和版本代表特定的套件內容。 如需在 nuget.org 上刪除套件的詳細資訊，請參閱[我們的原則](../nuget-org/policies/deleting-packages.md)。

除了[所有目錄中包含](#catalog-leaf)的屬性以外，套件刪除類別目錄專案還沒有任何額外的屬性。

`version`屬性是在 nuspec 中找到的原始版本字串。

`published`屬性是刪除封裝的時間，通常是在目錄專案的認可時間戳記之前的短時間。

#### <a name="sample-request"></a>範例要求

GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>資料指標

### <a name="overview"></a>概觀

本節說明的用戶端概念（雖然不一定是由通訊協定強制執行）應該屬於任何實際的目錄用戶端。

因為目錄是依時間編制索引的附加資料結構，所以用戶端應該在本機儲存**游標**，表示用戶端處理目錄專案的時間點。 請注意，此資料指標的值絕不能使用用戶端的電腦時鐘來產生。 相反地，此值應該來自于目錄物件的 `commitTimestamp` 值。

每次用戶端想要處理封裝來源上的新事件時，它只需要針對認可時間戳記大於其儲存資料指標的所有目錄專案查詢目錄。 在用戶端成功處理所有新的類別目錄專案之後，它會將剛剛處理的類別目錄專案的最新認可時間戳記記錄為新的資料指標值。

使用這種方法，用戶端就一定不會錯過封裝來源上發生的任何套件事件。
此外，用戶端永遠不需要在資料指標記錄的認可時間戳記之前，重新處理舊的事件。

這項功能強大的資料指標概念用於許多 nuget.org 背景工作，可用來將 V3 API 本身保持在最新狀態。 

### <a name="initial-value"></a>初始值

當目錄用戶端第一次啟動（因此沒有資料指標值）時，應該使用的預設資料指標值。NET 的 `System.DateTimeOffset.MinValue` 或一些類似的最小表示時間戳記概念。

### <a name="iterating-over-catalog-items"></a>逐一查看類別目錄專案

若要查詢下一組要處理的類別目錄專案，用戶端應該：

1. 從本機存放區提取記錄的資料指標值。
1. 下載和還原序列化目錄索引。
1. 尋找認可時間戳記*大於*資料指標的所有目錄頁面。
1. 宣告要處理之類別目錄專案的空白清單。
1. 針對在步驟3中符合的每個目錄頁面：
   1. 下載和還原序列化目錄頁面。
   1. 尋找認可時間戳記*大於*資料指標的所有目錄專案。
   1. 將所有相符的目錄專案新增至步驟4中所宣告的清單。
1. 依認可時間戳記排序目錄專案清單。
1. 依序處理每個目錄專案：
   1. 下載和還原序列化類別目錄專案。
   1. 適當地回應目錄專案的類型。
   1. 以用戶端特定的方式處理目錄專案檔案。
1. 將最後一個目錄專案的認可時間戳記記錄為新的資料指標值。

使用此基本演算法，用戶端執行可以建立套件來源上所有可用套件的完整觀點。 用戶端只需要定期執行此演算法，即可一律留意封裝來源的最新變更。

> [!Note]
> 這是 nuget.org 用來將[套件中繼資料](registration-base-url-resource.md)、[封裝內容](package-base-address-resource.md)、[搜尋](search-query-service-resource.md)和[自動完成](search-autocomplete-service-resource.md)資源保持在最新狀態的演算法。

### <a name="dependent-cursors"></a>相依資料指標

假設有兩個類別目錄用戶端具有固有的相依性，其中一個用戶端的輸出取決於另一個用戶端的輸出。 

#### <a name="example"></a>範例

例如，在 nuget.org 中，新發佈的封裝不應該出現在 [搜尋] 資源中，就會出現在套件中繼資料資源中。 這是因為官方 NuGet 用戶端所執行的「還原」作業會使用套件中繼資料資源。 如果客戶使用搜尋服務探索套件，他們應該能夠使用套件中繼資料資源成功還原該套件。 換句話說，搜尋資源取決於套件中繼資料資源。 每個資源都有更新該資源的目錄用戶端背景作業。 每個用戶端都有自己的資料指標。

由於這兩個資源都是以目錄為基礎，因此更新搜尋資源的目錄用戶端的游標*不得超過*封裝中繼資料目錄用戶端的游標。

#### <a name="algorithm"></a>演算法

若要執行這種限制，只要將上述演算法修改為：

1. 從本機存放區提取記錄的資料指標值。
1. 下載和還原序列化目錄索引。
1. 尋找認可時間戳記*大於***或等於**相依性資料指標的所有目錄頁面。
1. 宣告要處理之類別目錄專案的空白清單。
1. 針對在步驟3中符合的每個目錄頁面：
   1. 下載和還原序列化目錄頁面。
   1. 尋找認可時間戳記*大於***或等於**相依性資料指標的所有目錄專案。
   1. 將所有相符的目錄專案新增至步驟4中所宣告的清單。
1. 依認可時間戳記排序目錄專案清單。
1. 依序處理每個目錄專案：
   1. 下載和還原序列化類別目錄專案。
   1. 適當地回應目錄專案的類型。
   1. 以用戶端特定的方式處理目錄專案檔案。
1. 將最後一個目錄專案的認可時間戳記記錄為新的資料指標值。

使用這個修改過的演算法，您可以建立相依目錄用戶端的系統，所有專案都會產生自己的特定索引、成品等等。
