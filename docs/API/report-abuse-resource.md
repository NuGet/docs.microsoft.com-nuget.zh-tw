---
title: 報告濫用的 URL 範本，NuGet API
description: 報表濫用的 URL 範本可讓用戶端在其 UI 中顯示報表濫用連結。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="report-abuse-url-template"></a>報表濫用的 URL 範本

您可讓用戶端建立可供使用者有關的特定套件回報濫用的 URL。 封裝來源想要啟用所有用戶端經驗 （即使第 3 個合作對象） 委派濫用套件來源的報表時，這非常有用。

用於擷取套件內容的資源是`ReportAbuseUriTemplate`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                       | 注意
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 初版
ReportAbuseUriTemplate/3.0.0-rc   | 別名 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 範本

下列 api 的 URL 是值`@id`與其中一個先前提及的資源相關聯的屬性`@type`值。

## <a name="http-methods"></a>HTTP 方法

雖然用戶端不代表使用者對報表濫用的 URL 的要求，應支援網頁`GET`方法，以允許使用按的 URL，輕鬆地在網頁瀏覽器中開啟。

## <a name="construct-the-url"></a>建構 URL

根據給定的已知的封裝識別碼和版本，用戶端實作可以建構用來存取 web 介面的 URL。 用戶端實作應該給使用者讓他們，以便開啟網頁瀏覽器的 url，並進行任何必要的不當使用報表會顯示這個建構的 URL （或可點按的連結）。 濫用報表表單的實作取決於伺服器實作。

值`@id`為 URL 字串，包含任何下列預留位置語彙基元：

### <a name="url-placeholders"></a>URL 預留位置

名稱        | 類型    | 必要 | 注意
----------- | ------- | -------- | -----
`{id}`      | 字串  | 否       | 要為回報不當使用的套件識別碼
`{version}` | 字串  | 否       | 回報不當使用的封裝版本

`{id}`和`{version}`解譯伺服器實作的值必須是不區分大小寫並不容易版本是否會正規化。

例如，nuget.org 的報表濫用範本看起來像這樣：

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

如果客戶端實現需要顯示NuGet.Versioning 4.3.0的報告濫用形式的鏈接，則會生成以下URL並將其提供給用戶：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
