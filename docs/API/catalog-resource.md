---
title: "類別目錄、 NuGet V3 API |Microsoft 文件"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "目錄是所有的封裝，建立以及在 nuget.org 刪除索引。"
keywords: "NuGet V3 API 類別目錄，nuget.org 的交易記錄，複寫 NuGet.org，clone NuGet.org，NuGet.org 的附加專用的記錄"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: d1a24be68a60085a40361c374ffb34dc221f09c4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="catalog"></a>Catalog

**目錄**是記錄上的封裝來源，例如建立和刪除的所有封裝作業的資源。 目錄資源有`Catalog`輸入[服務索引](service-index.md)。

> [!Note]
> 目錄不是由官方 NuGet 用戶端，因為並非所有的封裝來源實作的類別目錄。

> [!Note]
> 目前，nuget.org 目錄不是可在中國使用。 如需詳細資訊，請參閱[NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值   | 注意
------------- | -----
Catalog/3.0.0 | 初版

## <a name="base-url"></a>基礎 URL

下列應用程式開發介面的進入點 URL 是值`@id`上述資源相關聯的屬性`@type`值。 本主題會使用預留位置 URL `{@id}`。

## <a name="http-methods"></a>HTTP 方法

只有 HTTP 方法位於類別目錄資源支援的所有 Url`GET`和`HEAD`。

## <a name="catalog-index"></a>類別目錄索引

類別目錄索引是文件中有一份類別目錄項目，排序 cronologically 的已知位置。 它是目錄資源的進入點。

索引被組成類別目錄網頁。 每個類別目錄 頁面包含類別目錄項目。 每個類別目錄項目代表有關時間點的單一封裝的事件。 類別目錄項目可以代表已建立、 未列出，relisted，或刪除從套件來源的封裝。 藉由處理類別目錄中的項目依時間先後順序，用戶端可以建置 V3 套件來源上存在每個套件的最新檢視。

簡單地說，類別目錄的 blob 會有下列的階層式結構：

- **索引**： 類別目錄的進入點。
- **頁面**： 類別目錄項目的群組。
- **分葉**： 文件表示為類別目錄項目，也就是在單一封裝狀態的快照。

每個類別目錄物件具有名`commitTimeStamp`代表項目加入至目錄時。 類別目錄項目加入至類別目錄中的頁面稱為認可的批次。 在相同的認可的所有類別目錄項目具有相同的認可時間戳記 (`commitTimeStamp`) 和認可 ID (`commitId`)。 放在相同的認可中的類別目錄項目代表相同的點同時間發生的套件來源的事件。 目錄認可內沒有順序。

因為每個套件識別碼和版本是唯一的會永遠不會有一個以上的類別目錄項目認可中。 這可確保，在單一封裝的類別目錄項目可以永遠會明確地排序認可時間戳記。

沒有絕對不會以每個類別目錄的多個認可`commitTimeStamp`。 換句話說，`commitId`是多餘的`commitTimeStamp`。

相對於[套件中繼資料資源](registration-base-url-resource.md)、 索引的會按封裝識別碼、 類別目錄位於索引 （queryable） 只依時間。

類別目錄項目會固定加入到開始的單純遞增、 依時間先後順序中的類別目錄中。 這表示，如果 X 次加入目錄認可，則沒有目錄認可會不斷加入時間小於或等於 X。

下列要求會擷取類別目錄索引。

    GET {@id}

類別目錄索引是 JSON 文件，其中包含的物件具有下列屬性：

名稱            | 類型             | 必要 | 注意
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 最新的認可與相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 最新的認可時間戳記
count           | 整數          | 是      | 在索引中的頁面數目
項目           | 物件的陣列 | 是      | 物件的陣列，每個物件，表示頁面

在每個項目`items`陣列是具有最少每一頁相關詳細資料的物件。 這些頁面的物件不包含類別目錄保留 （項目）。 未定義此陣列中項目的順序。 網頁可以依照使用記憶體中的用戶端來排序其`commitTimeStamp`屬性。

引入新的頁面，`count`會遞增，而新的物件會出現在`items`陣列。

當項目加入至類別目錄，索引的`commitId`會變更和`commitTimeStamp`會增加。 這兩個屬性會透過所有頁面基本上摘要`commitId`和`commitTimeStamp`值`items`陣列。

### <a name="catalog-page-object-in-the-index"></a>目錄索引中的頁面物件

類別目錄 頁面找到的物件類別目錄索引中`items`屬性具有下列屬性：

名稱            | 類型    | 必要 | 注意
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | 要擷取類別目錄 頁面的 URL
commitId        | 字串  | 是      | 此頁面中的最新認可與相關聯的唯一識別碼
commitTimeStamp | 字串  | 是      | 在這個頁面中的最新的認可時間戳記
count           | 整數 | 是      | 在 [類別目錄] 頁面中的項目數

相對於[套件中繼資料資源](registration-base-url-resource.md)這在某些情況下內嵌離開插入索引內，類別目錄保留永遠不會內嵌於索引一律必須使用的頁面讀取`@id`URL。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>類別目錄 頁面

類別目錄 頁面是類別目錄項目的集合。 這是提取使用其中一種文件`@id`目錄索引中找到的值。 類別目錄 頁面的 URL 不是有可預測性，應該使用類別目錄索引探索。

新的類別目錄項目會加入至最高的認可時間戳記只能與類別目錄索引中頁面或新的頁面。 一旦有較高的認可時間戳記的頁面加入至目錄時，較舊的分頁會永遠不會加入或變更。

類別目錄頁文件是具有下列屬性的 JSON 物件：

名稱            | 類型             | 必要 | 注意
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 此頁面中的最新認可與相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 在這個頁面中的最新的認可時間戳記
count           | 整數          | 是      | 在頁面中的項目數
項目           | 物件的陣列 | 是      | 在這個頁面中的類別目錄項目
父代          | 字串           | 是      | 類別目錄索引 URL

在每個項目`items`陣列是具有類別目錄項目某些最少詳細資料的物件。 這些項目物件不包含所有類別目錄項目的資料。 頁面的項目順序`items`陣列未定義。 項目可以依照使用記憶體中的用戶端來排序其`commitTimeStamp`屬性。

在網頁中的類別目錄項目數目是由伺服器實作所定義。 Nuget.org，最多 550 項目中有每個頁面上，雖然實際數目的時間可能較小的點在下一步的認可批次大小某些網頁 dependong。

引入新的項目，`count`是遞增的和新的類別目錄項目物件會出現在`items`陣列。

當項目加入至頁面上，`commitId`變更和`commitTimeStamp`會增加。 這兩個屬性會透過所有基本上摘要`commitId`和`commitTimeStamp`值`items`陣列。

### <a name="catalog-item-object-in-a-page"></a>目錄項目在網頁中的物件

類別目錄 頁面中找到的類別目錄項目物件`items`屬性具有下列屬性：

名稱            | 類型    | 必要 | 注意
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | 擷取目錄項目之 URL
@type           | 字串  | 是      | 類別目錄項目類型
commitId        | 字串  | 是      | 此類別目錄項目相關聯的認可 ID
commitTimeStamp | 字串  | 是      | 此類別目錄項目的認可時間戳記
nuget:id        | 字串  | 是      | 這個分葉與封裝識別碼
nuget:version   | 字串  | 是      | 與這個分葉封裝版本

`@type`值將會是下列兩個值之一：

1. `nuget:PackageDetails`： 這會對應至`PackageDetails`目錄分葉文件中的類型。
1. `nuget:PackageDelete`： 這會對應至`PackageDelete`目錄分葉文件中的類型。

如需詳細資訊表示每個型別，請參閱[對應項目類型](#item-types)下方。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>類別目錄的分葉

類別目錄的分葉包含特定的封裝識別碼和版本，在某個時間點的相關中繼資料的時間。 它是使用文件`@id`類別目錄 頁面中找到的值。 類別目錄的分葉的 URL 不是要 predictedable，應該使用類別目錄頁探索。

目錄的分葉文件是具有下列屬性的 JSON 物件：

名稱                    | 類型                       | 必要 | 注意
----------------------- | -------------------------- | -------- | -----
@type                   | 字串或字串陣列 | 是      | 目錄項目的型別
catalog:commitId        | 字串                     | 是      | 與這個類別目錄項目相關聯的認可 ID
catalog:commitTimeStamp | 字串                     | 是      | 此類別目錄項目的認可時間戳記
id                      | 字串                     | 是      | 封裝識別碼的類別目錄項目
發行               | 字串                     | 是      | 封裝的類別目錄項目發行的日期
版本                 | 字串                     | 是      | 封裝版本的類別目錄項目

### <a name="item-types"></a>項目類型

`@type`屬性是字串陣列。 為了方便起見，如果`@type`值是字串，它應該會被視為一個大小的任何陣列。 並非所有可能值`@type`記載。 不過，每個類別目錄項目有正好一個的兩個下列字串類型值：

1. `PackageDetails`： 表示封裝中繼資料的快照集
1. `PackageDelete`： 表示已刪除的封裝

### <a name="package-details-catalog-items"></a>封裝詳細資料類別目錄項目

類別目錄項目型別`PackageDetails`包含 （識別碼和版本組合） 的特定套件的套件中繼資料的快照。 當封裝來源遇到下列任何案例，則會產生套件詳細資料的類別目錄項目：

1. 封裝是**推入**。
1. 封裝是**列出**。
1. 封裝是**未列出**。
1. 封裝是**reflowed**。

封裝重新排列為基本上會產生假封裝本身發送不變更現有封裝的系統管理動作。 重新排列 nuget.org，會使用其中一種適用的類別目錄的背景工作在修正 bug 之後。

用戶端使用的類別目錄項目不應嘗試判斷哪一種案例所產生的類別目錄項目。 相反地，用戶端應該只需更新的任何維護的檢視或索引與類別目錄項目中包含的中繼資料。 此外，重複或多餘的類別目錄項目應該可正常地處理 （不斷地）。

封裝詳細資料的類別目錄項目具有下列屬性除了[包含在所有的類別目錄保留](#catalog-leaf)。

名稱                    | 類型                       | 必要 | 注意
----------------------- | -------------------------- | -------- | -----
authors                 | 字串                     | 否       |
created                 | 字串                     | 是      | 第一次建立封裝時的時間戳記
dependencyGroups        | 物件的陣列           | 否       | 相同格式化為[套件中繼資料資源](registration-base-url-resource.md#package-dependency-group)
描述             | 字串                     | 否       |
iconUrl                 | 字串                     | 否       |
isPrerelease            | boolean                    | 是      | 封裝版本是否在發行前版本
語言                | 字串                     | 否       |
licenseUrl              | 字串                     | 否       |
列出的                  | boolean                    | 否       | 與封裝是否列出
minClientVersion        | 字串                     | 否       |
packageHash             | 字串                     | 是      | 封裝中，使用編碼的雜湊[標準 base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | 字串                     | 是      |
packageSize             | 整數                    | 是      | 封裝.nupkg，以位元組為單位的大小
projectUrl              | 字串                     | 否       |
releaseNotes            | 字串                     | 否       |
requireLicenseAgreement | boolean                    | 否       | 假設`false`如果排除
摘要                 | 字串                     | 否       |
標記                    | 字串陣列           | 否       |
標題                   | 字串                     | 否       |
verbatimVersion         | 字串                     | 否       | 版本字串，因為它原先位於.nuspec

封裝`version`屬性是完整的正規化版本字串。 這表示，SemVer 2.0.0 的組建資料可能會包含此處。

`created`封裝來源，而這通常是短時間類別目錄項目的認可時間戳記之前先收到封裝時，時間戳記。

`packageHashAlgorithm`是由伺服器實作 represeting 定義字串的雜湊演算法，用來產生`packageHash`。 一律使用 nuget.org`packageHashAlgorithm`值`SHA512`。

`published`時間戳記是上次列出封裝時的時間。

> [!Note]
> 在 nuget.org，`published`值設為 1900 當套件很未列出的年份。

#### <a name="sample-request"></a>範例要求

GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>封裝刪除類別目錄項目

類別目錄項目型別`PackageDelete`包含資訊指出類別目錄用戶端封裝已從套件來源中刪除，而且已無法再使用 （例如還原） 的任何封裝作業的最少。

> [!Note]
> 它可能會被刪除的封裝，稍後重新發佈使用相同的封裝識別碼和版本。 上 nuget.org，這是非常少見的情況，因為它會破壞套件識別碼和版本，表示為特定的封裝內容的官方用戶端的假設。 如需 nuget.org 要刪除封裝的相關詳細資訊，請參閱[我們原則](../policies/deleting-packages.md)。

封裝刪除類別目錄項目沒有任何額外的屬性，除了[包含在所有的類別目錄保留](#catalog-leaf)。

`version`屬性是封裝.nuspec 中找到的原始版本字串。

`published`屬性是封裝刪除時，通常是做為短時間類別目錄項目的認可時間戳記之前的時間。

#### <a name="sample-request"></a>範例要求

取得 https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>總覽

本章節描述一種用戶端概念，雖然不一定是託管的通訊協定，但應該是任何實用的類別目錄用戶端實作的一部分。

因為此目錄是以時間編製索引的僅附加的資料結構，應儲存在用戶端**游標**代表最多哪個時間點的用戶端已在本機處理類別目錄項目。 請注意，永遠不會使用用戶端的電腦時鐘會產生此資料指標的值。 相反地，值應該來自於目錄物件的`commitTimestamp`值。

每次用戶端想要處理新的套件來源上的事件，它需要查詢類別目錄的所有類別目錄項目，認可時間戳記大於其預存的資料指標。 用戶端已順利處理所有新的類別目錄項目之後，它會記錄只會處理做為其新的資料指標值的類別目錄項目的最新的認可時間戳記。

使用這個方法，用戶端可以確定永遠不會遺漏任何發生的封裝來源的封裝事件。
此外，用戶端永遠不會有重新處理資料指標的記錄的認可時間戳記之前的舊事件。

資料指標的強大概念用於許多 nuget.org 背景工作，用來保持 V3 API 本身。 

### <a name="initial-value"></a>Initial value

當目錄用戶端第一次正在啟動 （並因此會有任何資料指標的值） 時，它應該使用的預設資料指標的值。網路的`System.DateTimeOffset.MinValue`或這類類似可顯示的最小時間戳記的概念。

### <a name="iterating-over-catalog-items"></a>逐一查看目錄項目

若要查詢的下一個要處理的類別目錄項目集，用戶端應該：

1. 從本機存放區擷取記錄的資料指標的值。
1. 下載及還原序列化的類別目錄的索引。
1. 尋找所有目錄頁面認可時間戳記*大於*資料指標。
1. 宣告空白處理的類別目錄項目的清單。
1. 針對每個類別目錄 頁面中比對步驟 3:
   1. 下載及還原序列化的類別目錄 頁面。
   1. 尋找所有類別目錄項目，認可時間戳記*大於*資料指標。
   1. 將所有相符的類別目錄項目加入至在步驟 4 中宣告的清單。
1. 認可時間戳記排序類別目錄項目清單。
1. 依序處理每個類別目錄項目：
   1. 下載及還原序列化的類別目錄項目。
   1. 適當地回應類別目錄項目的型別。
   1. 處理類別目錄項目文件，以用戶端特定的方式。
1. 記錄最後一個類別目錄項目認可時間戳記做為新的資料指標值。

利用這個基本的演算法，用戶端實作可以建置的套件來源的完整檢視所有可用的封裝。 用戶端只需要在執行定期為永遠在 封裝來源的最近變更了解此演算法。

> [!Note]
> 這是此演算法的 nuget.org 用以保存[套件中繼資料](registration-base-url-resource.md)，[封裝內容](package-base-address-resource.md)，[搜尋](search-query-service-resource.md)和[自動完成](search-autocomplete-service-resource.md)資源的最新狀態。

### <a name="dependent-cursors"></a>相依的資料指標

假設有兩個類別目錄用戶端具有 inherant 的相依性，其中一個用戶端的輸出取決於另一個用戶端的輸出。 

#### <a name="example"></a>範例

例如，在 nuget.org 新發行的封裝不應該出現在搜尋資源之前它會出現在封裝的中繼資料資源。 這是因為官方 NuGet 用戶端所執行的 「 還原 」 作業會使用套件中繼資料資源。 如果客戶發現封裝使用的搜尋服務，它們應該能夠順利還原該套件，套件中繼資料資源。 換句話說，搜尋資源套件中繼資料資源而定。 每個資源都有更新該資源的類別目錄用戶端背景工作。 每個用戶端有它自己的資料指標。

因為這兩個資源會建置類別目錄更新搜尋資源的類別目錄用戶端資料指標從*必須不超過*封裝中繼資料類別目錄用戶端資料指標。

#### <a name="algorithm"></a>演算法

若要實作這項限制，簡單修改上述是演算法：

1. 從本機存放區擷取記錄的資料指標的值。
1. 下載及還原序列化的類別目錄的索引。
1. 尋找所有目錄頁面認可時間戳記*大於*游標**小於或等於其相依性資料指標。**
1. 宣告空白處理的類別目錄項目的清單。
1. 針對每個類別目錄 頁面中比對步驟 3:
   1. 下載及還原序列化的類別目錄 頁面。
   1. 尋找所有類別目錄項目，認可時間戳記*大於*游標**小於或等於其相依性資料指標。**
   1. 將所有相符的類別目錄項目加入至在步驟 4 中宣告的清單。
1. 認可時間戳記排序類別目錄項目清單。
1. 依序處理每個類別目錄項目：
   1. 下載及還原序列化的類別目錄項目。
   1. 適當地回應類別目錄項目的型別。
   1. 處理類別目錄項目文件，以用戶端特定的方式。
1. 記錄最後一個類別目錄項目認可時間戳記做為新的資料指標值。

使用這個修改過的演算法，您可以建立一個系統相依的類別目錄用戶端的所有產生自己的特定索引、 成品等等。
