---
title: nuget.org 通訊協定
description: 要與 NuGet 用戶端互動的發展 nuget.org 通訊協定。
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547269"
---
# <a name="nugetorg-protocols"></a>nuget.org 通訊協定

若要與 nuget.org 互動，用戶端必須遵循特定通訊協定。 這些通訊協定將持續進化的因為用戶端必須找出呼叫特定 nuget.org 的 Api 時，他們使用的通訊協定版本。 這可讓以非中斷的方式會造成變更，舊的用戶端的 nuget.org。

> [!Note]
> 在此頁面上記載的 Api 特有 nuget.org 還有不會預期其他介紹這些 Api 的 NuGet 伺服器實作。 

廣泛實作橫跨 NuGet 生態系統的 NuGet API 的相關資訊，請參閱[API 概觀](overview.md)。

本主題列出各種通訊協定，當它們再存在。

## <a name="nuget-protocol-version-410"></a>NuGet 4.1.0 的通訊協定版本

4.1.0 通訊協定指定驗證範圍 nuget.org，若要驗證套件的 nuget.org 帳戶以外的服務進行互動的金鑰使用方式。 請注意，`4.1.0`是不透明的字串，但剛好符合官方 NuGet 用戶端支援此通訊協定的第一個版本的版本。

驗證可確保使用者建立 API 金鑰只會搭配 nuget.org，，和該其他驗證或從協力廠商服務的驗證透過使用一次驗證領域索引鍵。 這些驗證範圍金鑰可用來驗證封裝所屬 nuget.org 上的特定使用者 （帳戶）。

### <a name="client-requirement"></a>用戶端需求

用戶端都必須通過下列標頭，當它們進行 API 呼叫來**推播**至 nuget.org 的套件：

    X-NuGet-Protocol-Version: 4.1.0

請注意，`X-NuGet-Client-Version`標頭的語意很類似，但會保留僅供官方 NuGet 用戶端。 協力廠商用戶端應該使用`X-NuGet-Protocol-Version`標頭和值。

**推播**通訊協定本身所述的文件[`PackagePublish`資源](package-publish-resource.md)。

如果用戶端與外部服務，且必須驗證是否屬於特定使用者 （帳戶） 的封裝互動時，它應該使用下列通訊協定，並使用的驗證領域索引鍵和不從 nuget.org 的 API 金鑰。

### <a name="api-to-request-a-verify-scope-key"></a>若要確認範圍金鑰的 API

此 API 用來取得驗證領域金鑰來驗證封裝，其所擁有的 nuget.org 作者。

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------- | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要求的驗證領域索引鍵封裝 identidier
VERSION        | URL    | 字串 | 否       | 套件版本
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如：`X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>回應

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>若要驗證的驗證領域索引鍵的 API

此 API 用來驗證套件 nuget.org 作者所擁有的驗證領域索引鍵。

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------  | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要求的驗證領域索引鍵的套件識別碼
VERSION        | URL    | 字串 | 否       | 套件版本
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如：`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> 此驗證範圍的 API 金鑰將於一天的時間到期，或在第一次使用時，何者先發生。

#### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
200         | API 金鑰無效
403         | API 金鑰不正確或未獲授權，以針對封裝推送
404         | 所參考封裝`ID`和`VERSION`（選擇性） 不存在
