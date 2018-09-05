---
title: 報告不當使用 URL 範本，NuGet API
description: 報告不當使用 URL 範本可讓用戶端在其 UI 中顯示的報表內容粗俗的文章連結。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549335"
---
# <a name="report-abuse-url-template"></a>報告不當使用 URL 範本

就可以建置可供使用者特定封裝的相關檢舉不當使用 URL 的用戶端。 當想要啟用委派到套件來源的濫用報告所有的用戶端體驗 （甚至是第 3 個合作對象） 的套件來源，這非常有用。

用來建立此 URL 的資源`ReportAbuseUriTemplate`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                       | 注意
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 初始版本
ReportAbuseUriTemplate/3.0.0-rc   | 別名 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 範本

下列 API 的 URL 是 windows 7`@id`其中一個先前提及的資源相關聯的屬性`@type`值。

## <a name="http-methods"></a>HTTP 方法

雖然用戶端不是代表使用者對檢舉不當使用 URL 的要求，應支援網頁`GET`方法，以允許輕鬆地在網頁瀏覽器中開啟已按下的 URL。

## <a name="construct-the-url"></a>建構的 URL

指定已知的套件識別碼和版本，用戶端實作可以建構 URL，用來存取 web 介面。 用戶端實作應該顯示此建構的 URL （或可點選連結） 給使用者，讓他們開啟網頁瀏覽器的 url，並進行任何必要的濫用報告。 不當使用的報表格式的實作取決於伺服器實作。

值`@id`是 URL 的字串，包含任何下列預留位置語彙基元：

### <a name="url-placeholders"></a>URL 預留位置

名稱        | 類型    | 必要 | 注意
----------- | ------- | -------- | -----
`{id}`      | 字串  | 否       | 檢舉不當使用的套件識別碼
`{version}` | 字串  | 否       | 若要檢舉不當使用的套件版本

`{id}`和`{version}`解譯伺服器實作的值必須是不區分大小寫，並不容易受到版本是否已標準化。

比方說，nuget.org 的報表內容粗俗的文章範本看起來像這樣：

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

如果客戶端實現需要顯示NuGet.Versioning 4.3.0的報告濫用形式的鏈接，則會生成以下URL並將其提供給用戶：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
