---
title: 檢舉不當使用 URL 範本，NuGet API
description: 「報告濫用 URL」範本可讓用戶端在其 UI 中顯示「報告不當使用」連結。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775222"
---
# <a name="report-abuse-url-template"></a>報告濫用 URL 範本

用戶端可以建立一個 URL，讓使用者用來回報有關特定套件的濫用。 當套件來源想要啟用所有用戶端體驗 (甚至是協力廠商) 將濫用報表委派給套件來源時，這非常有用。

用來建立此 URL 的資源是在 `ReportAbuseUriTemplate` [服務索引](service-index.md)中找到的資源。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值                       | 備註
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-Beta | 初始版本
ReportAbuseUriTemplate/3.0.0-rc   | 別名 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL template

下列 API 的 URL 是 `@id` 與上述其中一個資源值相關聯之屬性的值 `@type` 。

## <a name="http-methods"></a>HTTP 方法

雖然用戶端不會代表使用者對報告濫用 URL 提出要求，但網頁應該支援 `GET` 方法，以允許在網頁瀏覽器中輕鬆地開啟已按一下的 url。

## <a name="construct-the-url"></a>建立 URL

假設有已知的封裝識別碼和版本，則用戶端執行可以建立用來存取 web 介面的 URL。 用戶端的執行應該會顯示此已建立的 URL (或可按的連結) 給使用者，讓他們能夠將網頁瀏覽器開啟至 URL，並進行任何必要的濫用報告。 「濫用報表」表單的執行是由伺服器執行所決定。

的值 `@id` 是包含下列任何預留位置標記的 URL 字串：

### <a name="url-placeholders"></a>URL 預留位置

名稱        | 類型    | 必要 | 備註
----------- | ------- | -------- | -----
`{id}`      | 字串  | 不可以       | 要報告濫用的套件識別碼
`{version}` | 字串  | 不可以       | 要報告濫用的套件版本

`{id}` `{version}` 伺服器執行所解讀的和值必須區分大小寫，且不區分版本是否正規化。

例如，nuget 的報告濫用範本看起來像這樣：

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

如果用戶端執行需要顯示 NuGet 的報告濫用表單連結，則會產生下列 URL 並將其提供給使用者：

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
