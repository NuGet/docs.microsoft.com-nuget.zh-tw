---
title: 套件詳細資料 URL 範本，NuGet API
description: 套件詳細資料 URL 範本可讓用戶端在其 UI 中顯示更多套件詳細資料的 web 連結
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773948"
---
# <a name="package-details-url-template"></a>套件詳細資料 URL 範本

用戶端可以建立一個 URL，讓使用者在網頁瀏覽器中查看更多套件詳細資料。 當套件來源想要顯示可能無法容納 NuGet 用戶端應用程式所顯示之內容約制內之套件的其他資訊時，這會很有用。

用來建立此 URL 的資源是在 `PackageDetailsUriTemplate` [服務索引](service-index.md)中找到的資源。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值                     | 備註
------------------------------- | -----
PackageDetailsUriTemplate/5.1。0 | 初始版本

## <a name="url-template"></a>URL template

下列 API 的 URL 是 `@id` 與上述其中一個資源值相關聯之屬性的值 `@type` 。

## <a name="http-methods"></a>HTTP 方法

雖然用戶端不會代表使用者對套件詳細資料 URL 提出要求，但網頁應該支援 `GET` 方法，以允許在網頁瀏覽器中輕鬆地開啟所選的 url。

## <a name="construct-the-url"></a>建立 URL

假設有已知的封裝識別碼和版本，則用戶端執行可以建立用來存取 web 介面的 URL。 用戶端的執行應該會顯示這個已建立的 URL (或可點選連結) 給使用者，讓他們可以開啟網頁瀏覽器並前往 URL，以及深入瞭解套件。 封裝詳細資料頁面的內容是由伺服器執行所決定。

URL 必須是絕對 URL，且 (通訊協定) 的配置必須是 HTTPS。

`@id`服務索引中的值為 URL 字串，其中包含下列任何預留位置標記：

### <a name="url-placeholders"></a>URL 預留位置

名稱        | 類型    | 必要 | 備註
----------- | ------- | -------- | -----
`{id}`      | 字串  | 不可以       | 要取得其詳細資料的套件識別碼
`{version}` | 字串  | 不可以       | 要取得其詳細資料的套件版本

伺服器應該接受 `{id}` `{version}` 任何大小寫的值。 此外，伺服器應該不區分版本是否 [正規化](../concepts/package-versioning.md#normalized-version-numbers)。 換句話說，伺服器也應接受非正規化的版本。

例如，nuget 的套件詳細資料範本看起來像這樣：

```http
https://www.nuget.org/packages/{id}/{version}
```

如果用戶端執行需要顯示 NuGet 的封裝詳細資料的連結，則會產生下列 URL 並將其提供給使用者：

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
