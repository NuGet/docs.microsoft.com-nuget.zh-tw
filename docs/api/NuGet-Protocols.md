---
title: nuget.org 通訊協定
description: 要與 NuGet 用戶端互動的發展 nuget.org 通訊協定。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822574"
---
# <a name="nugetorg-protocols"></a>nuget.org 通訊協定

若要與 nuget.org 互動，用戶端必須遵循特定的通訊協定。 由於這些通訊協定保持進化，用戶端必須識別呼叫特定 nuget.org 應用程式開發介面時，他們使用的通訊協定版本。 這可讓以非中斷的方式引入的變更，舊的用戶端的 nuget.org。

> [!Note]
> 此頁面上記載的 Api 僅供 nuget.org，而且沒有任何其他導入的這些 Api 的 NuGet 伺服器實作預期的情況。 

如需 NuGet 的 API 實作廣泛 NuGet 生態系統資訊，請參閱[API 概觀](overview.md)。

本主題列出各種的通訊協定和當他們回到至存在。

## <a name="nuget-protocol-version-410"></a>4.1.0 的 NuGet 通訊協定版本

4.1.0 通訊協定指定 nuget.org，若要驗證封裝，以針對 nuget.org 帳戶以外的服務互動的驗證領域索引鍵使用方式。 請注意，`4.1.0`版本是不透明的字串，但發生的第一個版本支援此通訊協定的官方 NuGet 用戶端通常會一致。

驗證可確保使用者建立 API 金鑰只會搭配 nuget.org，，和該其他驗證或來自協力廠商服務的驗證透過使用一次驗證領域索引鍵。 這些範圍驗證金鑰可以用來驗證封裝所屬上 nuget.org 的特定使用者 （帳戶）。

### <a name="client-requirement"></a>用戶端需求

用戶端都必須通過下列標頭，當他們完成應用程式開發介面呼叫**發送**nuget.org 的封裝：

    X-NuGet-Protocol-Version: 4.1.0

請注意，`X-NuGet-Client-Version`標頭的語意很類似，但會保留只能由官方 NuGet 用戶端使用。 第三方用戶端應該使用`X-NuGet-Protocol-Version`標頭和值。

**發送**本身的通訊協定所述的文件[`PackagePublish`資源](package-publish-resource.md)。

如果用戶端與外部服務，必須驗證是否屬於特定的使用者 （帳戶） 的封裝互動時，它應該使用下列通訊協定，並使用驗證範圍和不從 nuget.org 的 API 金鑰。

### <a name="api-to-request-a-verify-scope-key"></a>API 要求的驗證領域索引鍵

這個 API 用來取得 nuget.org 作者來驗證所經擁有封裝的驗證領域索引鍵。

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------- | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要求的驗證領域索引鍵封裝 identidier
VERSION        | URL    | 字串 | 否       | 封裝版本
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如：`X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>回應

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>若要驗證的驗證領域索引鍵的 API

這個 API 用來驗證封裝 nuget.org 作者所擁有的驗證領域索引鍵。

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------  | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要求的驗證領域索引鍵的封裝識別碼
VERSION        | URL    | 字串 | 否       | 封裝版本
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如：`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> 此確認範圍 API 金鑰到期日的時間，或在第一次使用時，何者先發生。

#### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
200         | API 金鑰無效
403         | API 金鑰是無效或未獲授權來針對封裝推入
404         | 封裝所參考`ID`和`VERSION`（選擇性） 不存在
