---
title: nuget.org 通訊協定
description: 與 NuGet 用戶端互動的不斷演進 nuget.org 通訊協定。
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773973"
---
# <a name="nugetorg-protocols"></a>nuget.org 通訊協定

若要與 nuget.org 互動，用戶端必須遵循特定的通訊協定。 因為這些通訊協定會持續演進，所以用戶端必須識別在呼叫特定 nuget.org Api 時所使用的通訊協定版本。 這可讓 nuget.org 針對舊版用戶端以不間斷的方式引進變更。

> [!Note]
> 此頁面上記載的 Api 是 nuget.org 專屬的，而且不會預期其他 NuGet 伺服器的開發人員會引入這些 Api。 

如需有關跨 NuGet 生態系統廣泛執行之 NuGet API 的詳細資訊，請參閱 [API 總覽](overview.md)。

本主題將列出各種不同的通訊協定，以及它們是否存在。

## <a name="nuget-protocol-version-410"></a>NuGet 通訊協定版本4.1。0

4.1.0 通訊協定會指定驗證範圍金鑰的使用方式，以與 nuget.org 以外的服務進行互動，以針對 nuget.org 帳戶驗證套件。 請注意， `4.1.0` 版本號碼是不透明的字串，但會與支援此通訊協定的正式 NuGet 用戶端的第一個版本相符。

驗證可確保使用者建立的 API 金鑰只會與 nuget.org 搭配使用，而協力廠商服務的其他驗證或驗證則是透過一次性使用驗證範圍金鑰來處理。 這些驗證範圍金鑰可以用來驗證封裝是否屬於 nuget.org 上的特定使用者 (帳戶) 。

### <a name="client-requirement"></a>用戶端需求

用戶端進行 API 呼叫以將套件 **推送** 至 nuget.org 時，必須傳遞下列標頭：

```
X-NuGet-Protocol-Version: 4.1.0
```

請注意， `X-NuGet-Client-Version` 標頭具有類似的語法，但只保留給官方 NuGet 用戶端使用。 協力廠商用戶端應該使用 `X-NuGet-Protocol-Version` 標頭和值。

[ `PackagePublish` 資源](package-publish-resource.md)的檔中說明了 **推** 播通訊協定本身。

如果用戶端與外部服務互動，而且需要驗證封裝是否屬於特定使用者 (帳戶) ，則應該使用下列通訊協定，並使用驗證範圍金鑰，而不是 nuget.org 的 API 金鑰。

### <a name="api-to-request-a-verify-scope-key"></a>要求驗證範圍金鑰的 API

此 API 可用來取得 nuget.org 作者的驗證範圍金鑰，以驗證其擁有的套件。

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>要求參數

名稱           | 位於     | 類型   | 必要 | 備註
-------------- | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要求驗證範圍金鑰的封裝 identidier
VERSION        | URL    | 字串 | 不可以       | 套件版本
X-NuGet-ApiKey | 標頭 | 字串 | 是      | 例如， `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>回應

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>驗證驗證範圍金鑰的 API

此 API 可用來驗證 nuget.org 作者所擁有之套件的驗證範圍金鑰。

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>要求參數

名稱           | 位於     | 類型   | 必要 | 備註
-------------  | ------ | ------ | -------- | -----
識別碼             | URL    | 字串 | 是      | 要求驗證範圍金鑰的套件識別碼
VERSION        | URL    | 字串 | 不可以       | 套件版本
X-NuGet-ApiKey | 標頭 | 字串 | 是      | 例如， `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> 此驗證範圍 API 金鑰會在一天內到期，或在第一次使用時到期（以先發生者為准）。

#### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
200         | API 金鑰有效
403         | API 金鑰無效或未獲授權可針對套件進行推送
404         | 所參考的封裝 `ID` 和 `VERSION` (選擇性) 不存在
