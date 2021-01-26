---
title: 推送和刪除，NuGet API
description: 發行服務可讓用戶端發佈新的封裝，以及取消列出或刪除現有的封裝。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773922"
---
# <a name="push-and-delete"></a>推送和刪除

您可以根據伺服器的執行) 來推送、刪除 (或取消列出，以及使用 NuGet V3 API 來重新列出封裝。 這些作業是 `PackagePublish` 以 [服務索引](service-index.md)中找到的資源為基礎。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值          | 備註
-------------------- | -----
PackagePublish/2.0。0 | 初始版本

## <a name="base-url"></a>基底 URL

下列 Api 的基底 URL 是 `@id` `PackagePublish/2.0.0` 套件來源之 [服務索引](service-index.md)中資源的屬性值。 針對下列檔，會使用 nuget. org 的 URL。 請考慮 `https://www.nuget.org/api/v2/package` 作為 `@id` 服務索引中找到之值的預留位置。

請注意，此 URL 會指向與舊版 V2 推送端點相同的位置，因為通訊協定相同。

## <a name="http-methods"></a>HTTP 方法

`PUT` `POST` `DELETE` 此資源支援和 HTTP 方法。 針對每個端點支援的方法，請參閱下文。

## <a name="push-a-package"></a>推送套件

> [!Note]
> nuget.org 具有與推送端點互動的 [其他需求](NuGet-Protocols.md) 。

nuget.org 支援使用下列 API 來推送新的封裝。 如果具有所提供識別碼和版本的套件已存在，則 nuget.org 會拒絕推送。 其他套件來源可能會支援取代現有的封裝。

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>要求參數

名稱           | 位於     | 類型   | 必要 | 備註
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 標頭 | 字串 | 是      | 例如， `X-NuGet-ApiKey: {USER_API_KEY}`

API 金鑰是由使用者從套件來源取得並設定為用戶端的不透明字串。 未強制採用任何特定的字串格式，但 API 金鑰的長度不應超過 HTTP 標頭值的合理大小。

### <a name="request-body"></a>要求本文

要求主體的格式必須如下：

#### <a name="multipart-form-data"></a>多部分表單資料

要求標頭 `Content-Type` 為 `multipart/form-data` ，而且要求主體中的第一個專案是所推送之 nupkg 的原始位元組。 系統會忽略多部分主體中的後續專案。 系統會忽略多元件專案的檔案名或其他任何標頭。

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
201、202    | 已成功推送封裝
400         | 提供的套件無效
409         | 具有所提供識別碼和版本的套件已經存在

當封裝成功推送時所傳回的成功狀態碼會有不同的伺服器實施。

## <a name="delete-a-package"></a>刪除套件

nuget.org 會將套件刪除要求解讀為 "取消列出"。 這表示套件仍可供封裝的現有取用者使用，但套件不會再出現在搜尋結果或 web 介面中。 如需這種作法的詳細資訊，請參閱 [已刪除的套件](../nuget-org/policies/deleting-packages.md) 原則。 其他伺服器的執行可以自由地將此信號解讀為實刪除、虛刪除或取消列出。 例如 [， (伺服器執行](https://www.nuget.org/packages/NuGet.Server) 只支援舊版 V2 API，) 支援根據設定選項，以取消列出或實刪除的方式處理此要求。

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>要求參數

名稱           | 位於     | 類型   | 必要 | 備註
-------------- | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要刪除的封裝識別碼
VERSION        | URL    | 字串 | 是      | 要刪除的套件版本
X-NuGet-ApiKey | 標頭 | 字串 | 是      | 例如， `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
204         | 已刪除封裝
404         | 沒有具有所提供 `ID` 和 `VERSION` 存在的套件

## <a name="relist-a-package"></a>重新列出套件

如果未列出套件，則可以使用 "重新列出" 端點，再次在搜尋結果中顯示該套件。 此端點與 [delete (取消列出) 端點](#delete-a-package) 具有相同的圖形，但使用的 `POST` 是 HTTP 方法，而不是 `DELETE` 方法。

如果封裝已列出，要求仍會成功。

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>要求參數

名稱           | 位於     | 類型   | 必要 | 備註
-------------- | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要重新列出的封裝識別碼
VERSION        | URL    | 字串 | 是      | 要重新列出的套件版本
X-NuGet-ApiKey | 標頭 | 字串 | 是      | 例如， `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
200         | 現在會列出套件
404         | 沒有具有所提供 `ID` 和 `VERSION` 存在的套件
