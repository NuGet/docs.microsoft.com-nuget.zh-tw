---
title: 封裝詳細資料 URL 範本，NuGet API
description: 封裝詳細資料 URL 範本可讓用戶端在其 web 連結至多個套件詳細資料的 UI 中顯示
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638069"
---
# <a name="package-details-url-template"></a>封裝詳細資料 URL 範本

就可以建置可供使用者查看網頁瀏覽器中的多個套件詳細資料的 URL 的用戶端。 當想要顯示的 NuGet 用戶端應用程式的顯示範圍內的封裝可能不適合的其他資訊的套件來源，這非常有用。

用來建立此 URL 的資源`PackageDetailsUriTemplate`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                     | 注意
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | 初始版本

## <a name="url-template"></a>URL 範本

下列 API 的 URL 是 windows 7`@id`其中一個先前提及的資源相關聯的屬性`@type`值。

## <a name="http-methods"></a>HTTP 方法

雖然用戶端不是代表使用者對套件詳細資料 URL 的要求，應支援網頁`GET`方法，以允許輕鬆地在網頁瀏覽器中開啟已按下的 URL。

## <a name="construct-the-url"></a>建構的 URL

指定已知的套件識別碼和版本，用戶端實作可以建構 URL，用來存取 web 介面。 用戶端實作應該顯示使用者讓他們開啟網頁瀏覽器的 url，並深入了解封裝這個建構的 URL （或可點選連結）。 套件詳細資料頁面的內容取決於伺服器實作。

此 URL 必須是絕對 URL，並配置 （通訊協定） 必須是 HTTPS。

值`@id`服務中的索引為 URL 字串，包含任何下列預留位置語彙基元：

### <a name="url-placeholders"></a>URL 預留位置

名稱        | 類型    | 必要 | 注意
----------- | ------- | -------- | -----
`{id}`      | 字串  | 否       | 套件識別碼，以取得詳細資料
`{version}` | 字串  | 否       | 套件版本，以取得詳細資料

伺服器應該接受`{id}`和`{version}`任何大小寫的值。 此外，伺服器不能區分版本是否[正規化](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)。 換句話說，伺服器應接受也接受非標準化的版本。

比方說，nuget.org 的套件詳細資料範本看起來像這樣：

    https://www.nuget.org/packages/{id}/{version}

如果用戶端實作需要的 NuGet.Versioning 4.3.0 套件詳細資料，它會產生下列 URL，並提供給使用者：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
