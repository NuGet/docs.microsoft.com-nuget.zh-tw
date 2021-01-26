---
title: 存放庫簽章，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存放庫簽章資源可讓用戶端套件來源宣佈其存放庫簽署功能。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775337"
---
# <a name="repository-signatures"></a>存放庫簽章

如果封裝來源支援將存放庫簽章新增至已發佈的封裝，則用戶端可能會判斷套件來源所使用的簽署憑證。 此資源可讓用戶端偵測存放庫簽署的套件是否已遭篡改，或是否有未預期的簽署憑證。

用來提取此存放庫簽章資訊的資源是在 `RepositorySignatures` [服務索引](service-index.md)中找到的資源。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值                | 備註
-------------------------- | -----
RepositorySignatures/4.7。0 | 初始版本
RepositorySignatures/4.9。0 | NuGet v 4.9 + 用戶端支援
RepositorySignatures/5.0。0 | 允許啟用 `allRepositorySigned` 。 NuGet v 5.0 + 用戶端支援

## <a name="base-url"></a>基底 URL

下列 Api 的進入點 URL 是 `@id` 與上述資源值相關聯之屬性的值 `@type` 。 本主題使用預留位置 URL `{@id}` 。

請注意，與其他資源不同的是， `{@id}` 必須透過 HTTPS 提供 URL。

## <a name="http-methods"></a>HTTP 方法

存放庫簽章資源中找到的所有 Url 都只支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="repository-signatures-index"></a>存放庫簽章索引

存放庫簽章索引包含兩項資訊：

1. 來源上找到的所有套件是否都是由這個套件來源簽署的儲存機制。
1. 封裝來源用來簽署套件的憑證清單。

在大部分情況下，憑證清單只會附加至。 當先前的簽署憑證已過期，且套件來源需要開始使用新的簽署憑證時，就會將新的憑證新增至清單中。 如果從清單中移除憑證，這表示用戶端不應再將使用移除的簽署憑證所建立的所有封裝簽章視為有效。 在此情況下，封裝簽章 (但不一定是封裝) 無效。 用戶端原則可能會允許將套件安裝為未簽署。

在憑證撤銷的情況下 (例如金鑰洩漏) ，套件來源應該要重新簽署受影響之憑證簽署的所有套件。 此外，套件來源應該從簽署憑證清單中移除受影響的憑證。

下列要求會提取存放庫簽章索引。

```
GET {@id}
```

存放庫簽章索引是 JSON 檔，其中包含具有下列屬性的物件：

名稱                | 類型             | 必要 | 備註
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | 是      | 必須 `false` 在4.7.0 和4.9.0 資源上
signingCertificates | 物件的陣列 | 是      | 

`allRepositorySigned`如果封裝來源有一些沒有存放庫簽章的封裝，則布林值設定為 false。 如果布林值設定為 true，則來源上的所有可用封裝都必須有中所述的其中一個簽署憑證所產生的存放庫簽章 `signingCertificates` 。

> [!Warning]
> `allRepositorySigned`4.7.0 和4.9.0 資源上的布林值必須為 false。 NuGet 4.7、4.8 和 v 4.9 用戶端無法從已設定為 true 的來源安裝套件 `allRepositorySigned` 。

`signingCertificates`如果 `allRepositorySigned` 布林值設定為 true，陣列中應該有一或多個簽署憑證。 如果陣列是空的，而且 `allRepositorySigned` 設定為 true，則來源的所有套件都應視為無效，雖然用戶端原則仍允許使用套件。 此陣列中的每個元素都是具有下列屬性的 JSON 物件。

名稱         | 類型   | 必要 | 備註
------------ | ------ | -------- | -----
contentUrl   | 字串 | 是      | DER 編碼公開憑證的絕對 URL
指紋 | 物件 (object) | 是      |
subject      | 字串 | 是      | 憑證中的主體辨別名稱
簽發者       | 字串 | 是      | 憑證簽發者的辨別名稱
notBefore    | 字串 | 是      | 憑證有效期間的開始時間戳
notAfter     | 字串 | 是      | 憑證有效期間的結束時間戳記

請注意， `contentUrl` 必須透過 HTTPS 來提供。 此 URL 沒有特定的 URL 模式，必須使用此存放庫簽章索引檔來動態探索。 

此物件中)  (的所有屬性都 `contentUrl` 必須從找到的憑證可 `contentUrl` 。
提供這些可屬性是為了方便將往返次數降至最低。

`fingerprints` 物件具有下列屬性：

名稱                   | 類型   | 必要 | 備註
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | 字串 | 是      | SHA-256 指紋

索引鍵名稱 `2.16.840.1.101.3.4.2.1` 是 SHA-256 雜湊演算法的 OID。

所有雜湊值都必須是雜湊摘要的小寫、十六進位編碼的字串表示。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
