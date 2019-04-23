---
title: 存放庫簽章，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存放庫簽章資源可讓用戶端地宣布其簽署功能的存放庫的套件來源。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931848"
---
# <a name="repository-signatures"></a>存放庫簽章

如果套件來源支援新增存放庫簽章，以發佈的封裝，就可以判斷所使用的套件來源的簽章憑證的用戶端。 這項資源可讓用戶端偵測封裝存放庫簽章是否遭到竄改，或有非預期的簽章憑證。

用於擷取此存放庫簽章資訊的資源`RepositorySignatures`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                | 注意
-------------------------- | -----
RepositorySignatures/4.7.0 | 初始版本
RepositorySignatures/4.9.0 | NuGet 4.9 + 用戶端支援
RepositorySignatures/5.0.0 | 可讓啟用`allRepositorySigned`。 NuGet v5.0 + 用戶端支援

## <a name="base-url"></a>基礎 URL

下列 Api 的進入點 URL 是 windows 7`@id`上述的資源相關聯的屬性`@type`值。 本主題使用的預留位置 URL `{@id}`。

請注意，不同於其他資源， `{@id}` URL，才能透過 HTTPS 提供服務。

## <a name="http-methods"></a>HTTP 方法

在存放庫簽章資源支援的 HTTP 方法中找到的所有 Url`GET`和`HEAD`。

## <a name="repository-signatures-index"></a>存放庫簽章索引

存放庫簽章索引包含兩項資訊：

1. 在來源上找到所有的套件是經過此套件來源的儲存機制。
1. 用來簽署套件的套件來源的憑證清單。

在大部分情況下，憑證清單只會將附加到。 先前的簽署憑證已過期，而且若要開始使用新的簽署憑證需要的套件來源時，新的憑證將會新增至清單。 如果憑證從清單中移除，這表示，使用已移除的簽署憑證建立的所有套件簽章應不會再都視為有效用戶端。 在此情況下，封裝簽章 （但不是一定是封裝） 無效。 用戶端原則可能會允許安裝為不帶正負號的套件。

在憑證撤銷 （例如金鑰洩露） 的情況下的套件來源應該重新簽署所有受影響的憑證所簽署的套件。 此外，套件來源應該移除受影響的憑證簽署的憑證清單。

下列要求擷取存放庫簽章索引。

    GET {@id}

存放庫簽章索引是 JSON 文件，其中包含具有下列屬性的物件：

名稱                | 類型             | 必要 | 注意
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | 是      | 必須是`false`4.7.0 和 4.9.0 資源
signingCertificates | 物件的陣列 | 是      | 

`allRepositorySigned`布林值為 false，如果套件來源具有一些套件有沒有存放庫簽章。 如果布林值會設為 true，在所有的封裝來源必須具有存放庫簽章所述的簽章憑證的其中一個產生`signingCertificates`。

> [!Warning]
> `allRepositorySigned`布林值必須為偽 4.7.0 和 4.9.0 資源上。 NuGet v4.7、 v4.8 和 4.9 用戶端無法從來源安裝套件`allRepositorySigned`設為 true。

應該有一或多個中的簽署憑證`signingCertificates`陣列，如果`allRepositorySigned`布林值會設為 true。 如果是空的陣列和`allRepositorySigned`設為 true，所有的封裝來源的資料應視為無效，雖然用戶端原則仍然允許套件耗用量。 此陣列中的每個項目是具有下列屬性的 JSON 物件。

名稱         | 類型   | 必要 | 注意
------------ | ------ | -------- | -----
contentUrl   | 字串 | 是      | DER 編碼的公開憑證的絕對 URL
指紋 | object | 是      |
主旨      | 字串 | 是      | 從憑證主體辨別的名稱
issuer       | 字串 | 是      | 憑證的簽發者的辨別的名稱
notBefore    | 字串 | 是      | 憑證的有效期間的開始時間戳記
notAfter     | 字串 | 是      | 憑證的有效期間結束的時間戳記

請注意，`contentUrl`才能透過 HTTPS 提供服務。 此 URL 有沒有特定的 URL 模式，而且必須動態探索使用此存放庫簽章索引文件。 

這個物件中的所有屬性 (除了來自`contentUrl`) 必須是可從憑證，請參閱衍生`contentUrl`。
為了方便起見，將往返降至最低，會提供這些可衍生的屬性。

`fingerprints`物件具有下列屬性：

名稱                   | 類型   | 必要 | 注意
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | 字串 | 是      | SHA-256 指紋

索引鍵名稱`2.16.840.1.101.3.4.2.1`是 SHA-256 雜湊演算法的 OID。

所有的雜湊值必須是摘要的小寫字母、 十六進位編碼的字串表示的雜湊。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
