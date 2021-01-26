---
title: 目錄資源，NuGet V3 API
description: 目錄是在 nuget.org 上建立和刪除的所有套件的索引。
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 11485f583d6993919f6bb8acabcc87d9e4261975
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774158"
---
# <a name="catalog"></a>目錄

**目錄** 是記錄套件來源上所有封裝作業的資源，例如建立和刪除。 目錄資源在 `Catalog` [服務索引](service-index.md)中有型別。 您可以使用此資源來 [查詢所有已發行的封裝](../guides/api/query-for-all-published-packages.md)。

> [!Note]
> 因為官方 NuGet 用戶端不使用目錄，所以並非所有套件來源都能執行目錄。

> [!Note]
> 目前，中國未提供 nuget.org 目錄。 如需詳細資訊，請參閱 [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949)。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值   | 備註
------------- | -----
Catalog/3.0。0 | 初始版本

## <a name="base-url"></a>基底 URL

下列 Api 的進入點 URL 是 `@id` 與上述資源值相關聯之屬性的值 `@type` 。 本主題使用預留位置 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

目錄資源中找到的所有 Url 都只支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="catalog-index"></a>目錄索引

目錄索引是已知位置中的檔，其中有依時間順序排序的目錄專案清單。 這是目錄資源的進入點。

索引是由目錄頁面所組成。 每個目錄頁面都包含類別目錄專案。 每個類別目錄專案代表一個在某個時間點與單一封裝相關的事件。 類別目錄專案可以代表從套件來源建立、未列出、重新列入或刪除的封裝。 藉由依時間連續處理類別目錄專案，用戶端就可以針對存在於 V3 套件來源的每個套件建立最新的觀點。

簡單來說，目錄 blob 的階層式結構如下：

- **Index**：目錄的進入點。
- **頁面**：類別目錄專案的群組。
- 分 **葉**：代表類別目錄專案的檔，這是單一套件狀態的快照集。

每個目錄物件都有一個名為的屬性，它會在 `commitTimeStamp` 專案新增至目錄時表示。 類別目錄專案會以批次的方式新增至目錄頁面，稱為「認可」。 相同認可中的所有目錄專案都有相同的認可時間戳記 (`commitTimeStamp`) 和認可識別碼 (`commitId`) 。 放在相同認可中的類別目錄專案代表在套件來源的相同時間點周圍發生的事件。 目錄認可內沒有任何順序。

因為每個封裝識別碼和版本都是唯一的，所以認可中永遠不會有一個以上的類別目錄專案。 這可確保單一套件的類別目錄專案一律可以明確地依據認可時間戳記來排序。

每個目錄永遠不會有一個以上的認可 `commitTimeStamp` 。 換句話說， `commitId` 是的多餘 `commitTimeStamp` 。

相較于依封裝識別碼編制索引的 [封裝中繼資料資源](registration-base-url-resource.md)，目錄 (編制索引，而且只能依時間進行查詢) 。

類別目錄專案一律會以單純遞增的時間順序新增至目錄。 這表示，如果在時間 X 新增了目錄認可，則不會在一開始就新增任何目錄認可，且時間小於或等於 X。

下列要求會提取目錄索引。

```
GET {@id}
```

目錄索引是 JSON 檔，其中包含具有下列屬性的物件：

名稱            | 類型             | 必要 | 備註
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 與最近認可相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 最近認可的時間戳記
count           | 整數          | 是      | 索引中的頁面數目
項目           | 物件的陣列 | 是      | 物件的陣列，每個物件都代表一個頁面

陣列中的每個元素 `items` 都是物件，每個頁面都有一些最基本的詳細資料。 這些頁面物件不包含目錄 (專案) 。 此陣列中的元素順序未定義。 您可以使用屬性，在記憶體中的用戶端排列頁面的順序 `commitTimeStamp` 。

引進新的頁面時， `count` 將會遞增，而新的物件將會出現在 `items` 陣列中。

當專案加入至目錄時，索引的 `commitId` 將會變更，而且 `commitTimeStamp` 會增加。 這兩個屬性基本上是陣列中所有頁面 `commitId` 和 `commitTimeStamp` 值的摘要 `items` 。

### <a name="catalog-page-object-in-the-index"></a>索引中的類別目錄頁面物件

在目錄索引的屬性中找到的類別目錄頁面物件 `items` 具有下列屬性：

名稱            | 類型    | 必要 | 備註
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | 要提取目錄頁面的 URL
commitId        | 字串  | 是      | 與此頁面中最新認可相關聯的唯一識別碼
commitTimeStamp | 字串  | 是      | 此頁面中最新認可的時間戳記
count           | 整數 | 是      | 目錄頁面中的專案數

與 [套件中繼資料資源](registration-base-url-resource.md) 不同的是，在某些情況下，內嵌會保留在索引中，而目錄離開永遠不會內嵌到索引中，而且一律必須使用頁面的 URL 來提取 `@id` 。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>目錄頁面

目錄頁面是目錄專案的集合。 這是使用 `@id` 目錄索引中找到的其中一個值所提取的檔。 目錄頁面的 URL 不能是可預測的，且應該僅使用目錄索引來探索。

新的類別目錄專案只會以最高的認可時間戳記或新頁面新增至目錄索引中的頁面。 一旦將具有較高認可時間戳記的頁面新增至目錄之後，就不會將舊頁面新增至或變更。

目錄分頁檔是具有下列屬性的 JSON 物件：

名稱            | 類型             | 必要 | 備註
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 與此頁面中最新認可相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 此頁面中最新認可的時間戳記
count           | 整數          | 是      | 頁面中的專案數
項目           | 物件的陣列 | 是      | 此頁面中的類別目錄專案
父系 (parent)          | 字串           | 是      | 目錄索引的 URL

陣列中的每個 `items` 專案都是一個物件，其中包含有關類別目錄專案的最小詳細資料。 這些專案物件不包含目錄專案的所有資料。 未定義頁面的陣列中專案的順序 `items` 。 您可以使用物件的屬性，以記憶體中的用戶端來排序專案 `commitTimeStamp` 。

頁面中的目錄專案數目是由伺服器執行所定義。 針對 nuget.org，每個頁面中最多會有550個專案，但某些頁面的實際數目可能較小，這取決於下一次認可批次的大小。

引進新的專案時， `count` 會遞增，並將新的類別目錄專案物件顯示在 `items` 陣列中。

當專案加入至頁面時， `commitId` 變更和 `commitTimeStamp` 增加。 這兩個屬性基本上是 `commitId` 陣列中所有和 `commitTimeStamp` 值的摘要 `items` 。

### <a name="catalog-item-object-in-a-page"></a>頁面中的類別目錄專案物件

在目錄頁面的屬性中找到的類別目錄專案物件 `items` 具有下列屬性：

名稱            | 類型    | 必要 | 備註
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | 提取類別目錄專案的 URL
@type           | 字串  | 是      | 類別目錄專案的類型
commitId        | 字串  | 是      | 與此目錄專案相關聯的認可識別碼
commitTimeStamp | 字串  | 是      | 此類別目錄專案的認可時間戳記
nuget： id        | 字串  | 是      | 這個分葉相關的套件識別碼
nuget：版本   | 字串  | 是      | 這個分葉相關的套件版本

`@type`值會是下列兩個值的其中一個：

1. `nuget:PackageDetails`：這會對應到 `PackageDetails` 目錄分葉檔中的型別。
1. `nuget:PackageDelete`：這會對應到 `PackageDelete` 目錄分葉檔中的型別。

如需每個類型所代表之意義的詳細資訊，請參閱下列 [對應的專案類型](#item-types) 。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>目錄分葉

目錄分葉包含特定封裝識別碼與版本在某個時間點的相關中繼資料。 這是使用 `@id` 在目錄頁面中找到的值所提取的檔。 目錄分葉的 URL 不能是可預測的，且應該僅使用類別目錄頁面來探索。

目錄分葉檔是具有下列屬性的 JSON 物件：

名稱                    | 類型                       | 必要 | 備註
----------------------- | -------------------------- | -------- | -----
@type                   | 字串或字串陣列 | 是      | 類別目錄專案)  (s
目錄： commitId        | 字串                     | 是      | 與此目錄專案相關聯的認可識別碼
目錄： commitTimeStamp | 字串                     | 是      | 此類別目錄專案的認可時間戳記
id                      | 字串                     | 是      | 目錄專案的封裝識別碼
published               | 字串                     | 是      | 封裝類別目錄專案的發行日期
version                 | 字串                     | 是      | 類別目錄專案的封裝版本

### <a name="item-types"></a>專案類型

`@type`屬性是字串或字串陣列。 為了方便起見，如果 `@type` 值為字串，則應該將它視為任何大小為1的陣列。 並非所有可能的值 `@type` 都記載。 不過，每個類別目錄專案都有下列兩個字串類型值的其中一個：

1. `PackageDetails`：表示封裝中繼資料的快照集
1. `PackageDelete`：代表已刪除的封裝

### <a name="package-details-catalog-items"></a>封裝詳細資料類別目錄專案

具有類型的類別目錄專案 `PackageDetails` 包含特定封裝的封裝中繼資料的快照集 (識別碼和版本組合) 。 當套件來源遇到下列任何情況時，就會產生套件詳細資料類別目錄專案：

1. 已 **推送** 套件。
1. **列出** 套件。
1. 未 **列出** 套件。
1. 封裝是 **reflowed**。

封裝重新排列是一種系統管理手勢，基本上會產生未變更套件本身的現有封裝的假推送。 在 nuget.org 上，在使用類別目錄的其中一個背景工作中修正 bug 之後，會使用重新排列。

取用類別目錄專案的用戶端不應嘗試判斷哪些案例會產生類別目錄專案。 相反地，用戶端應該只使用類別目錄專案中包含的中繼資料來更新任何已維護的 view 或 index。 此外， (不斷) ，應妥善處理重複或重複的類別目錄專案。

套件詳細資料類別目錄專案除了 [包含在所有目錄離開](#catalog-leaf)的屬性之外，還具有下列屬性。

名稱                    | 類型                       | 必要 | 備註
----------------------- | -------------------------- | -------- | -----
authors                 | 字串                     | 不可以       |
created                 | 字串                     | 不可以       | 第一次建立封裝的時間戳記。 Fallback 屬性： `published` 。
dependencyGroups        | 物件的陣列           | 不可以       | 封裝的相依性（依目標 framework 分組） (與 [套件中繼資料資源相同的格式](registration-base-url-resource.md#package-dependency-group)) 
折舊             | 物件 (object)                     | 不可以       | 與封裝相關聯的取代 (與 [套件中繼資料資源相同的格式](registration-base-url-resource.md#package-deprecation)) 
description             | 字串                     | 不可以       |
iconUrl                 | 字串                     | 不可以       |
isPrerelease            | boolean                    | 不可以       | 套件版本是否為發行前版本。 可以從偵測到 `version` 。
語言                | 字串                     | 不可以       |
licenseUrl              | 字串                     | 不可以       |
列出的                  | boolean                    | 不可以       | 是否列出套件
minClientVersion        | 字串                     | 不可以       |
packageHash             | 字串                     | 是      | 封裝的雜湊，使用[標準基底 64](https://tools.ietf.org/html/rfc4648#section-4)進行編碼
packageHashAlgorithm    | 字串                     | 是      |
packageSize             | 整數                    | 是      | 封裝的大小。 nupkg （以位元組為單位）
packageTypes            | 物件的陣列           | 不可以       | 作者指定的封裝類型。
projectUrl              | 字串                     | 不可以       |
releaseNotes            | 字串                     | 不可以       |
requireLicenseAgreement | boolean                    | 不可以       | 假設 `false` 排除
總結                 | 字串                     | 不可以       |
tags                    | 字串陣列           | 不可以       |
title                   | 字串                     | 不可以       |
verbatimVersion         | 字串                     | 不可以       | 最初在 nuspec 中找到的版本字串。

封裝 `version` 屬性是正規化之後的完整版本字串。 這表示 SemVer 2.0.0 組建資料可以包含在此。

`created`時間戳記是套件來源第一次收到套件時，通常是在目錄專案的認可時間戳記之前的短時間。

`packageHashAlgorithm`是伺服器執行所定義的字串，表示用來產生的雜湊演算法 `packageHash` 。 nuget.org 一律使用的 `packageHashAlgorithm` 值 `SHA512` 。

`packageTypes`只有當作者指定了封裝類型時，才會顯示此屬性。 如果存在，則一律會有至少一個 (1) 專案。 陣列中的每個專案 `packageTypes` 都是具有下列屬性的 JSON 物件：

名稱      | 類型    | 必要 | 注意
--------- | ------- | -------- | -----
NAME      | 字串  | 是      | 封裝類型的名稱。
version    | 字串  | 不可以       | 封裝類型的版本。 只有當作者在 nuspec 中明確指定版本時，才會出現。

`published`時間戳記是上次列出封裝的時間。

> [!Note]
> 在 nuget.org 上， `published` 當封裝未列出時，此值會設定為1900年。

#### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>封裝刪除目錄專案

型別為的類別目錄專案 `PackageDelete` 包含一組最基本的資訊，指出已從套件來源刪除封裝，且不再提供任何封裝作業 (例如還原) 。

> [!NOTE]
> 您可以使用相同的套件識別碼和版本來刪除封裝，並于稍後重新發行。 在 nuget.org 上，這是非常罕見的情況，因為它會破壞官方用戶端假設套件識別碼和版本表示特定的封裝內容。 如需在 nuget.org 上刪除封裝的詳細資訊，請參閱 [我們的原則](../nuget-org/policies/deleting-packages.md)。

套件刪除目錄專案除了 [包含在所有目錄離開](#catalog-leaf)的屬性之外，還沒有其他屬性。

`version`屬性是在 nuspec 中找到的原始版本字串。

`published`屬性是刪除封裝的時間，通常是在目錄專案的認可時間戳記之前的短時間。

#### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>資料指標

### <a name="overview"></a>概觀

本節說明的用戶端概念（雖然不一定是由通訊協定強制執行）應該是任何實際目錄用戶端執行的一部分。

因為目錄是依時間編制索引的僅附加資料結構，用戶端應該將資料 **指標** 儲存在本機，表示用戶端處理類別目錄專案的時間點。 請注意，此資料指標值絕對不應該使用用戶端的機器時鐘來產生。 相反地，此值應該來自目錄物件的 `commitTimestamp` 值。

每次用戶端想要處理套件來源上的新事件時，它只需要查詢目錄，就會有認可時間戳記大於其儲存資料指標的所有目錄專案。 在用戶端成功處理所有新的類別目錄專案之後，它會記錄剛剛處理的目錄專案的最新認可時間戳記，做為新的資料指標值。

使用這種方法，用戶端可以確保永遠不會錯過任何在套件來源上發生的封裝事件。
此外，用戶端永遠不需要在資料指標記錄的認可時間戳記之前重新處理舊的事件。

這項強大的資料指標概念用於許多 nuget.org 背景工作，可用來將 V3 API 本身保持在最新狀態。 

### <a name="initial-value"></a>初始值

當目錄用戶端第一次啟動時 (，因此沒有任何資料指標值) ，它應該使用的預設資料指標值。NET 的 `System.DateTimeOffset.MinValue` 或一些類似的最小表示時間戳記的概念。

### <a name="iterating-over-catalog-items"></a>反覆運算類別目錄專案

若要查詢下一組要處理的類別目錄專案，用戶端應該：

1. 從本機存放區提取記錄的資料指標值。
1. 下載並還原序列化目錄索引。
1. 尋找認可時間戳記 *大於* 資料指標的所有目錄頁面。
1. 宣告要處理之類別目錄專案的空白清單。
1. 在步驟3中符合的每個目錄頁面：
   1. 下載並還原序列化目錄頁面。
   1. 尋找認可時間戳記 *大於* 資料指標的所有目錄專案。
   1. 將所有相符的目錄專案加入至步驟4中所宣告的清單。
1. 依認可時間戳記排序類別目錄專案清單。
1. 依序處理每個類別目錄專案：
   1. 下載並還原序列化類別目錄專案。
   1. 適當地回應類別目錄專案的類型。
   1. 以用戶端特定的方式處理類別目錄專案檔案。
1. 記錄最後一個類別目錄專案的認可時間戳記，做為新的資料指標值。

使用這個基本演算法，用戶端執行可以建立封裝來源上所有可用套件的完整觀點。 用戶端只需要定期執行此演算法，就能隨時留意到套件來源的最新變更。

> [!Note]
> 這是 nuget.org 用來讓 [套件中繼資料](registration-base-url-resource.md)、 [封裝內容](package-base-address-resource.md)、 [搜尋](search-query-service-resource.md) 和 [自動完成](search-autocomplete-service-resource.md) 資源保持在最新狀態的演算法。

### <a name="dependent-cursors"></a>相依資料指標

假設有兩個目錄用戶端具有固有的相依性，其中一個用戶端的輸出相依于另一個用戶端的輸出。 

#### <a name="example"></a>範例

例如，在 nuget.org 上，新發佈的套件不應該出現在搜尋資源中，就會出現在套件中繼資料資源中。 這是因為官方 NuGet 用戶端所執行的「還原」作業會使用套件中繼資料資源。 如果客戶使用搜尋服務探索套件，則應該能夠使用套件中繼資料資源成功還原該套件。 換句話說，搜尋資源取決於封裝中繼資料資源。 每個資源都有目錄用戶端背景工作更新該資源。 每個用戶端都有自己的資料指標。

由於這兩個資源都是從目錄建立的，因此更新搜尋資源之目錄用戶端的資料指標 *不能超過* 套件中繼資料目錄用戶端的資料指標。

#### <a name="algorithm"></a>演算法

若要執行這種限制，只要將上述演算法修改為：

1. 從本機存放區提取記錄的資料指標值。
1. 下載並還原序列化目錄索引。
1. 尋找認可時間戳記 *大於***或等於** 相依性資料指標的所有目錄頁面。
1. 宣告要處理之類別目錄專案的空白清單。
1. 在步驟3中符合的每個目錄頁面：
   1. 下載並還原序列化目錄頁面。
   1. 尋找認可時間戳記 *大於***或等於** 相依性資料指標的所有目錄專案。
   1. 將所有相符的目錄專案加入至步驟4中所宣告的清單。
1. 依認可時間戳記排序類別目錄專案清單。
1. 依序處理每個類別目錄專案：
   1. 下載並還原序列化類別目錄專案。
   1. 適當地回應類別目錄專案的類型。
   1. 以用戶端特定的方式處理類別目錄專案檔案。
1. 記錄最後一個類別目錄專案的認可時間戳記，做為新的資料指標值。

使用這個修改過的演算法，您可以建立相依目錄用戶端的系統，這些用戶端會產生自己的特定索引、成品等等。
