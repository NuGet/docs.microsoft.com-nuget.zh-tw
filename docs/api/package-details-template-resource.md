---
title: 套件詳細資料 URL 範本，NuGet API
description: '[套件詳細資料 URL] 範本可讓用戶端在其 UI 中顯示更多套件詳細資料的 web 連結'
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610949"
---
# <a name="package-details-url-template"></a>套件詳細資料 URL 範本

用戶端可以建立 URL，讓使用者用來在網頁瀏覽器中查看更多套件詳細資料。 當套件來源想要顯示可能無法符合 NuGet 用戶端應用程式顯示之範圍內的套件的其他資訊時，這會很有用。

用來建立此 URL 的資源是在[服務索引](service-index.md)中找到的 `PackageDetailsUriTemplate` 資源。

## <a name="versioning"></a>版本控制

會使用下列 `@type` 值：

@type 值                     | 備註
------------------------------- | -----
PackageDetailsUriTemplate/5.1。0 | 初始版本

## <a name="url-template"></a>URL 範本

下列 API 的 URL 是與上述其中一個資源 `@type` 值相關聯 `@id` 屬性的值。

## <a name="http-methods"></a>HTTP 方法

雖然用戶端不會代表使用者對封裝詳細資料 URL 提出要求，但網頁應支援 `GET` 方法，以便在網頁瀏覽器中輕鬆地開啟已按一下的 URL。

## <a name="construct-the-url"></a>結構 URL

假設有已知的封裝識別碼和版本，則用戶端執行可以建立用來存取 web 介面的 URL。 用戶端的執行應該會將此結構化的 URL （或可點按的連結）顯示給使用者，讓他們可以將網頁瀏覽器開啟至 URL，並深入瞭解封裝。 封裝詳細資料頁面的內容是由伺服器的執行所決定。

URL 必須是絕對 URL，而配置（通訊協定）必須是 HTTPS。

服務索引中的 `@id` 值是 URL 字串，其中包含下列任何預留位置權杖：

### <a name="url-placeholders"></a>URL 預留位置

[屬性]        | 輸入    | 必要項 | 備註
----------- | ------- | -------- | -----
`{id}`      | 字串  | 否       | 要取得詳細資料的套件識別碼
`{version}` | 字串  | 否       | 要取得詳細資料的套件版本

伺服器應該接受 `{id}`，並 `{version}` 任何大小寫的值。 此外，伺服器應該不會區分版本是否[正規化](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)。 換句話說，伺服器也應該接受非正規化版本。

例如，nuget 的 [套件詳細資料] 範本如下所示：

    https://www.nuget.org/packages/{id}/{version}

如果用戶端執行需要顯示 NuGet 的封裝詳細資料連結，則會產生下列 URL，並將其提供給使用者：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
