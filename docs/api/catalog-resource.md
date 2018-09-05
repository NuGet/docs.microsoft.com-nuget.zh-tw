---
title: 目錄資源，而 NuGet V3 API
description: 目錄是建立和刪除在 nuget.org 上的所有封裝的索引。
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d4c13200494ed3c6fa897ce0083a52c13688b44b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547389"
---
# <a name="catalog"></a>Catalog

**目錄**是記錄上的套件來源，例如建立和刪除作業的所有封裝作業的資源。 目錄資源有`Catalog`中輸入[服務索引](service-index.md)。

> [!Note]
> 目錄不官方 NuGet 用戶端使用，因為並非所有的套件來源實作類別目錄。

> [!Note]
> 目前，nuget.org 目錄不在中國推出。 如需詳細資訊，請參閱 < [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值   | 注意
------------- | -----
Catalog/3.0.0 | 初始版本

## <a name="base-url"></a>基礎 URL

下列 Api 的進入點 URL 是 windows 7`@id`上述的資源相關聯的屬性`@type`值。 本主題使用的預留位置 URL `{@id}`。

## <a name="http-methods"></a>HTTP 方法

只有 HTTP 方法位於目錄資源支援的所有 Url`GET`和`HEAD`。

## <a name="catalog-index"></a>類別目錄索引

類別目錄索引是有一份類別目錄項目，按照時間順序排列的已知位置中的文件。 它是目錄資源的進入點。

索引是由目錄頁面所組成。 每個類別目錄 頁面包含類別目錄項目。 每個類別目錄項目表示有關單一封裝的某一點的時間的事件。 類別目錄項目可以代表已建立、 未列出、 重新列入或刪除從套件來源的封裝。 藉由處理類別目錄項目，依時間先後順序，用戶端可以建置 V3 封裝來源上存在的每個封裝的最新檢視。

簡單地說，類別目錄的 blob 會有下列的階層式結構：

- **索引**： 類別目錄的進入點。
- **頁面**： 類別目錄項目的群組。
- **分葉**： 表示目錄項目，也就是單一封裝的狀態的快照集的文件。

每個目錄物件具有名`commitTimeStamp`代表項目已新增至目錄。 類別目錄項目會加入稱為認可的批次中的類別目錄 頁面。 在相同認可中的所有類別目錄項目有相同的認可時間戳記 (`commitTimeStamp`) 並認可 ID (`commitId`)。 放在相同的認可中的類別目錄項目代表相同的點同時間發生的套件來源的事件。 目錄認可中沒有順序。

每個套件識別碼和版本是唯一的因為會永遠不會有一個以上的類別目錄項目中認可。 這可確保，單一封裝的類別目錄項目可以一律會明確地排序認可時間戳記。

沒有絕對不會以每個類別目錄的多個認可`commitTimeStamp`。 亦即`commitId`是多餘的`commitTimeStamp`。

相對於[套件中繼資料資源](registration-base-url-resource.md)、 其編製索引封裝識別碼、 類別目錄可索引 （和可查詢） 只依時間。

類別目錄項目會固定加入到單純遞增、 依時間先後順序中的類別目錄中。 這表示，如果在時間 X 加入目錄認可則沒有任何目錄認可會不斷新增時間小於或等於 x。

下列要求擷取目錄索引。

    GET {@id}

類別目錄索引是 JSON 文件，其中包含具有下列屬性的物件：

名稱            | 類型             | 必要 | 注意
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 使用最新認可相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 最新的認可時間戳記
count           | 整數          | 是      | 在索引中的頁面數目
項目           | 物件的陣列 | 是      | 物件的陣列，每個物件，表示頁面

在每個項目`items`陣列是具有一些關於每個頁面的最少詳細資料的物件。 這些頁面物件不包含目錄分葉 （項目）。 未定義此陣列中項目的順序。 頁面可以依照中的記憶體使用的用戶端來排序其`commitTimeStamp`屬性。

引入新的頁面，`count`會遞增，而新的物件會出現在`items`陣列。

當項目新增至 「 類別目錄 」 索引的`commitId`會變更和`commitTimeStamp`會增加。 這兩個屬性對所有的頁面會摘要基本上`commitId`並`commitTimeStamp`中的值`items`陣列。

### <a name="catalog-page-object-in-the-index"></a>在索引中的目錄頁面物件

類別目錄頁面上找到的物件類別目錄索引中`items`屬性具有下列屬性：

名稱            | 類型    | 必要 | 注意
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | 要擷取類別目錄 頁面的 URL
commitId        | 字串  | 是      | 使用此頁面中的最新認可相關聯的唯一識別碼
commitTimeStamp | 字串  | 是      | 在此頁面中的最新的認可時間戳記
count           | 整數 | 是      | 在 [目錄] 頁面中的項目數

相對於[套件中繼資料資源](registration-base-url-resource.md)在某些情況下，內嵌離開的索引、 目錄分葉會永遠不會內嵌於索引，並一律必須使用頁面提取`@id`URL。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>類別目錄 頁面

[目錄] 頁面是類別目錄項目的集合。 擷取使用其中一種文件`@id`目錄索引中找到的值。 類別目錄 頁面的 URL 不是有可預測性，以及應該使用類別目錄索引中找到。

只能搭配最高的認可時間戳記類別目錄索引中的頁面，或到新的頁面，會加入新的類別目錄項目。 一旦具有較高的認可時間戳記的頁面新增至目錄時，較舊的頁面永遠不會加入或變更。

類別目錄頁的文件是 JSON 物件，具有下列屬性：

名稱            | 類型             | 必要 | 注意
--------------- | ---------------- | -------- | -----
commitId        | 字串           | 是      | 使用此頁面中的最新認可相關聯的唯一識別碼
commitTimeStamp | 字串           | 是      | 在此頁面中的最新的認可時間戳記
count           | 整數          | 是      | 在頁面中的項目數
項目           | 物件的陣列 | 是      | 在此頁面中的類別目錄項目
父代          | 字串           | 是      | 類別目錄索引 URL

在每個項目`items`陣列是具有一些最小類別目錄項目詳細資料的物件。 這些項目物件並包含所有目錄項目的資料。 在頁面中的項目順序`items`陣列未定義。 項目可以依照中的記憶體使用的用戶端來排序其`commitTimeStamp`屬性。

在頁面中的類別目錄項目數目是由伺服器實作定義。 對於 nuget.org，最多 550 中沒有項目每個頁面上，不過實際數目的時間可能會更小，某些頁面，在下一步 認可批次的大小而定。

引入新的項目，`count`是遞增的和新的類別目錄項目物件會出現在`items`陣列。

當項目加入至頁面上，`commitId`變更和`commitTimeStamp`會增加。 這兩個屬性會摘要基本上所有`commitId`並`commitTimeStamp`中的值`items`陣列。

### <a name="catalog-item-object-in-a-page"></a>目錄項目頁面中的物件

在 [目錄] 頁面中找到的類別目錄項目物件`items`屬性具有下列屬性：

名稱            | 類型    | 必要 | 注意
--------------- | ------- | -------- | -----
@id             | 字串  | 是      | URL，以擷取目錄項目
@type           | 字串  | 是      | 類別目錄項目類型
commitId        | 字串  | 是      | 此類別目錄項目相關聯的認可識別碼
commitTimeStamp | 字串  | 是      | 這個類別目錄項目的認可時間戳記
nuget:id        | 字串  | 是      | 這個分葉與套件識別碼
nuget:version   | 字串  | 是      | 與這個分葉套件版本

`@type`值將會是下列兩個值之一：

1. `nuget:PackageDetails`： 這會對應至`PackageDetails`目錄分葉文件中的型別。
1. `nuget:PackageDelete`： 這會對應至`PackageDelete`目錄分葉文件中的型別。

如需詳細資訊，每個類型所代表的意義，請參閱[對應項目型別](#item-types)如下。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>目錄分葉

目錄分葉會包含特定的套件識別碼和版本，在某個時間點的相關中繼資料的時間。 它是使用文件`@id`類別目錄 頁面中找到的值。 目錄分葉的 URL 不是有可預測性，而且應該使用只有類別目錄 頁面中找到。

目錄分葉文件是 JSON 物件，具有下列屬性：

名稱                    | 類型                       | 必要 | 注意
----------------------- | -------------------------- | -------- | -----
@type                   | 字串或字串陣列 | 是      | 目錄項目的型別
catalog:commitId        | 字串                     | 是      | 此類別目錄項目相關聯的認可識別碼
catalog:commitTimeStamp | 字串                     | 是      | 這個類別目錄項目的認可時間戳記
id                      | 字串                     | 是      | 類別目錄項目之封裝 ID
發行               | 字串                     | 是      | 封裝的目錄項目的發佈的日期
版本                 | 字串                     | 是      | 封裝版本的類別目錄項目

### <a name="item-types"></a>項目類型

`@type`屬性是字串陣列。 為了方便起見，如果`@type`值是字串，它應該會被視為一個大小的任何陣列。 並非所有可能的值，如`@type`記載。 不過，每個類別目錄項目有一個是兩個下列字串類型值：

1. `PackageDetails`： 代表套件中繼資料的快照集
1. `PackageDelete`： 表示已刪除的套件

### <a name="package-details-catalog-items"></a>套件詳細資料類別目錄項目

類別目錄項目類型`PackageDetails`包含特定套件 （識別碼和版本組合） 的套件中繼資料的快照集。 當封裝來源中遇到下列情況下，則會產生套件詳細資料的類別目錄項目：

1. 封裝是**推送**。
1. 封裝是**列出**。
1. 封裝是**未列出**。
1. 封裝是**reflowed**。

封裝自動重排是基本上會產生封裝本身而不需變更現有封裝的假發送系統管理動作。 在 nuget.org 上，自動重排之後修正 bug，其中一個背景工作使用的目錄中使用。

用戶端使用的目錄項目不應該嘗試判斷哪一種案例所產生的類別目錄項目。 相反地，用戶端應該只需維護或的任何檢視索引以更新類別目錄項目中包含的中繼資料。 此外，重複或冗餘的類別目錄項目應該會正常地處理 （以等冪方式）。

封裝詳細資料的目錄項目具有下列屬性以外[包含在所有的目錄分葉](#catalog-leaf)。

名稱                    | 類型                       | 必要 | 注意
----------------------- | -------------------------- | -------- | -----
authors                 | 字串                     | 否       |
created                 | 字串                     | 否       | 第一次建立封裝時的時間戳記。 後援屬性： `published`。
dependencyGroups        | 物件的陣列           | 否       | 相同的格式設定為[套件中繼資料資源](registration-base-url-resource.md#package-dependency-group)
描述             | 字串                     | 否       |
iconUrl                 | 字串                     | 否       |
isPrerelease            | boolean                    | 否       | Zda bude 封裝版本是發行前版本。 可以偵測到從`version`。
語言                | 字串                     | 否       |
licenseUrl              | 字串                     | 否       |
列出的                  | boolean                    | 否       | 與封裝是否列出
minClientVersion        | 字串                     | 否       |
packageHash             | 字串                     | 是      | 封裝，使用編碼的雜湊[標準的 base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | 字串                     | 是      |
packageSize             | 整數                    | 是      | 套件.nupkg，以位元組為單位的大小
projectUrl              | 字串                     | 否       |
releaseNotes            | 字串                     | 否       |
requireLicenseAgreement | boolean                    | 否       | 假設`false`如果排除
摘要                 | 字串                     | 否       |
標記                    | 字串陣列           | 否       |
標題                   | 字串                     | 否       |
verbatimVersion         | 字串                     | 否       | 版本字串，因為它原本位於.nuspec

封裝`version`屬性是完整的正規化版本字串。 也就是說，SemVer 2.0.0 組建資料可能包含以下項目。

`created`封裝來源，通常是短時間類別目錄項目的認可時間戳記之前先收到封裝時，時間戳記。

`packageHashAlgorithm`是伺服器實作，其代表用來產生的雜湊演算法所定義的字串`packageHash`。 一律會使用 nuget.org`packageHashAlgorithm`的值`SHA512`。

`published`時間戳記是上次列出封裝時的時間。

> [!Note]
> 在 nuget.org 上，`published`值設定為當套件很未列出的 1900 年。

#### <a name="sample-request"></a>範例要求

取得 https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>套件刪除目錄項目

類別目錄項目類型`PackageDelete`包含資訊指出目錄用戶端封裝已從套件來源中刪除，而且已無法再使用 （例如還原） 的任何封裝作業的最少。

> [!Note]
> 很可能要刪除的套件和更新版本發佈使用相同的套件識別碼和版本。 在 nuget.org 上，這是非常罕見的情況下，中斷套件識別碼和版本代表特定的套件內容的官方用戶端的假設。 在 nuget.org 上刪除封裝的相關資訊，請參閱[我們的原則](../policies/deleting-packages.md)。

套件刪除目錄項目沒有任何額外的屬性，除了[包含在所有的目錄分葉](#catalog-leaf)。

`version`屬性是封裝.nuspec 中找到的原始版本字串。

`published`屬性是封裝已刪除時，通常是做為類別目錄項目的認可時間戳記之前的短時間的時間。

#### <a name="sample-request"></a>範例要求

取得 https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>範例回應

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>總覽

本節說明一種用戶端的概念，雖然不一定是託管的通訊協定，但應該是任何實用的類別目錄的用戶端實作的一部分。

因為目錄是依時間編制索引的僅附加的資料結構，所以應該儲存在用戶端**游標**最多哪個時間點的用戶端已在本機處理類別目錄項目。 請注意，永遠不會使用用戶端的電腦時鐘會產生此資料指標的值。 相反地，值應該來自於目錄物件的`commitTimestamp`值。

每次用戶端想要處理封裝來源上的新事件，它需要查詢類別目錄的認可時間戳記的所有目錄項目大於其預存的資料指標。 用戶端已順利處理所有新的類別目錄項目之後，它會記錄只處理做為其新的資料指標值的類別目錄項目的最新的認可時間戳記。

使用這個方法，用戶端可以確定永遠不會錯過任何發生的套件來源的封裝事件。
此外，用戶端永遠不會有重新處理資料指標的已錄製的認可時間戳記之前的舊事件。

資料指標的這個功能強大的概念用於許多 nuget.org 背景工作和用來保持 V3 API 本身。 

### <a name="initial-value"></a>Initial value

當目錄用戶端正在開始第一次 （也因此沒有資料指標的值） 時，它應該使用預設資料指標的值。NET 的`System.DateTimeOffset.MinValue`或最小的可代表時間戳記的這類類似概念。

### <a name="iterating-over-catalog-items"></a>逐一查看目錄項目

若要查詢的下一個要處理的目錄項目集，用戶端應該：

1. 從本機存放區擷取記錄的資料指標的值。
1. 下載並還原序列化的類別目錄索引。
1. 尋找所有目錄頁面認可時間戳記*大於*資料指標。
1. 宣告空白的處理的類別目錄項目清單。
1. 每個類別目錄 頁面的比對在步驟 3:
   1. 下載並還原序列化 [目錄] 頁面。
   1. 尋找所有類別目錄項目，認可時間戳記*大於*資料指標。
   1. 加入在步驟 4 中宣告的清單中的所有相符的目錄項目。
1. 認可時間戳記排序目錄項目清單。
1. 依序處理每個類別目錄項目：
   1. 下載並還原序列化的類別目錄項目。
   1. 類別目錄項目的型別來做出適當回應。
   1. 處理目錄項目文件，以用戶端特定的方式。
1. 記錄最後一個類別目錄項目認可時間戳記做為新的資料指標值。

使用此基本的演算法，用戶端實作可以建置套件來源的完整檢視可用的所有封裝。 用戶端只需要執行此演算法會定期一律留意套件來源的最新變更。

> [!Note]
> 這是此演算法的 nuget.org 用以保存[套件中繼資料](registration-base-url-resource.md)，[套件內容](package-base-address-resource.md)，[搜尋](search-query-service-resource.md)並[自動完成](search-autocomplete-service-resource.md)最新的資源。

### <a name="dependent-cursors"></a>相依的資料指標

假設有兩個具有固有的相依性，其中一部用戶端的輸出取決於另一個用戶端的輸出目錄用戶端。 

#### <a name="example"></a>範例

比方說，在 nuget.org 上的新發行的封裝不應該出現在搜尋資源之前它會出現在套件中繼資料資源。 這是因為在官方的 NuGet 用戶端執行的 「 還原 」 作業會使用套件中繼資料資源。 如果客戶會發現使用搜尋服務套件，它們應該能夠成功還原該套件，套件中繼資料資源。 也就是說，搜尋資源套件中繼資料資源而定。 每個資源都更新該資源的類別目錄的用戶端背景工作。 每個用戶端有它自己的資料指標。

因為這兩個資源是從類別目錄中，更新搜尋資源的類別目錄用戶端資料指標*必須不超過*套件中繼資料目錄用戶端資料指標。

#### <a name="algorithm"></a>演算法

若要實作這項限制，只需修改為上述的演算法：

1. 從本機存放區擷取記錄的資料指標的值。
1. 下載並還原序列化的類別目錄索引。
1. 尋找所有目錄頁面認可時間戳記*大於*游標**小於或等於相依性的資料指標。**
1. 宣告空白的處理的類別目錄項目清單。
1. 每個類別目錄 頁面的比對在步驟 3:
   1. 下載並還原序列化 [目錄] 頁面。
   1. 尋找所有類別目錄項目，認可時間戳記*大於*游標**小於或等於相依性的資料指標。**
   1. 加入在步驟 4 中宣告的清單中的所有相符的目錄項目。
1. 認可時間戳記排序目錄項目清單。
1. 依序處理每個類別目錄項目：
   1. 下載並還原序列化的類別目錄項目。
   1. 類別目錄項目的型別來做出適當回應。
   1. 處理目錄項目文件，以用戶端特定的方式。
1. 記錄最後一個類別目錄項目認可時間戳記做為新的資料指標值。

使用這個修改過的演算法，您可以建立一個系統相依的類別目錄的用戶端的所有產生自己的特定索引、 成品等。
