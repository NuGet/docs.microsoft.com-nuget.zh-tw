---
title: 推送與刪除，NuGet API
description: 發行 」 服務可讓用戶端來發佈新的套件，並取消列出或刪除現有的封裝。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547517"
---
# <a name="push-and-delete"></a>推送與刪除

您可將推播、 刪除 （或取消列出，根據伺服器實作） 和重新列出封裝使用 NuGet V3 API。 這些作業會為基礎`PackagePublish`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值          | 注意
-------------------- | -----
PackagePublish/2.0.0 | 初始版本

## <a name="base-url"></a>基礎 URL

下列 Api 的基底 URL 是值`@id`的屬性`PackagePublish/2.0.0`封裝來源中的資源[服務索引](service-index.md)。 下列文件，會使用 nuget.org 的 URL。 請考慮`https://www.nuget.org/api/v2/package`作為預留位置`@id`服務索引中找到的值。

請注意，此 URL 會指向與舊版的 V2 推播端點位於相同位置因為通訊協定相同。

## <a name="http-methods"></a>HTTP 方法

`PUT`，`POST`和`DELETE`這項資源所支援 HTTP 方法。 針對每個端點上支援何種方法，如下所示。

## <a name="push-a-package"></a>將封裝推送

> [!Note]
> nuget.org 已[其他需求](NuGet-Protocols.md)與推播端點互動。

nuget.org 支援使用下列 API 推送新的套件。 如果提供的識別碼和版本的套件已經存在，nuget.org 會拒絕推送。 其他套件來源可能會支援取代現有的封裝。

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如：`X-NuGet-ApiKey: {USER_API_KEY}`

API 金鑰是不透明的字串，從套件來源取得的使用者，並在用戶端設定。 沒有特定字串的格式託管，但 API 金鑰的長度不應超過合理的大小，如 HTTP 標頭值。

### <a name="request-body"></a>要求本文

要求本文必須有下列形式：

#### <a name="multipart-form-data"></a>多部分表單資料

要求標頭`Content-Type`是`multipart/form-data`和要求本文中的第一個項目會被推入.nupkg 檔案的未經處理位元組。 在多組件的主體中的後續項目都會被忽略。 會忽略的檔案名稱或任何其他標頭的多組件的項目。

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
201, 202    | 已成功推送套件
400         | 提供的套件無效
409         | 使用提供的識別碼和版本的封裝已經存在

伺服器實作會傳回已成功推送套件時的成功狀態碼而有所不同。

## <a name="delete-a-package"></a>刪除套件

nuget.org 會解譯為套件刪除要求的 「 取消列出 」。 這表示封裝是仍然可供現有的取用者的封裝，但是封裝不會再出現在搜尋結果中或 web 介面中。 如需有關此做法的詳細資訊，請參閱[刪除套件](../policies/deleting-packages.md)原則。 其他伺服器實作會解譯為永久刪除此訊號、 虛刪除，或取消列出免費的。 例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （只支援較舊的 V2 API 的伺服器實作） 支援處理此要求以取消列出或永久刪除根據組態選項。

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------- | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要刪除的套件識別碼
VERSION        | URL    | 字串 | 是      | 若要刪除封裝的版本
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如：`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
204         | 已刪除的套件
404         | 使用提供的封裝`ID`和`VERSION`存在

## <a name="relist-a-package"></a>重新列出封裝

如果未列出的封裝，就能夠顯示該套件一次一次使用 「 重新列出 」 端點的搜尋結果中。 此端點具有一樣[刪除 （取消列出） 端點](#delete-a-package)使用，但`POST`HTTP 方法，而非`DELETE`方法。

如果已列出的封裝，請要求仍然會成功。

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------- | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要重新列出封裝的識別碼
VERSION        | URL    | 字串 | 是      | 若要重新列出封裝的版本
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如：`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
200         | 現在會列出封裝
404         | 使用提供的封裝`ID`和`VERSION`存在
