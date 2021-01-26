---
title: 套件內容，NuGet API
description: 封裝基底位址是用來提取封裝本身的簡單介面。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773939"
---
# <a name="package-content"></a>封裝內容

您可以使用 V3 API 來產生 URL，以提取任意封裝的內容 (nupkg 檔案) 。 用來提取套件內容的資源是在 `PackageBaseAddress` [服務索引](service-index.md)中找到的資源。 此資源也可讓您探索所有版本的套件、列出或未列出的套件。

此資源通常稱為「套件基底位址」或「平面容器」。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值              | 備註
------------------------ | -----
PackageBaseAddress/3.0。0 | 初始版本

## <a name="base-url"></a>基底 URL

下列 Api 的基底 URL 是 `@id` 與上述資源值相關聯之屬性的值 `@type` 。 在下列檔中，將會使用預留位置基底 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 Url 都支援 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="enumerate-package-versions"></a>列舉套件版本

如果用戶端知道封裝識別碼，並且想要探索套件來源可使用的套件版本，則用戶端可以建立可預測的 URL 來列舉所有套件版本。 這份清單旨在作為下面所述之套件內容 API 的「目錄清單」。

> [!Note]
> 這份清單包含列出和未列出的套件版本。

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>要求參數

名稱     | 位於     | 類型    | 必要 | 備註
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼，小寫

此 `LOWER_ID` 值是所需的封裝識別碼小寫使用由所執行的規則。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) 方法。

### <a name="response"></a>回應

如果封裝來源沒有提供的套件識別碼版本，則會傳回404狀態碼。

如果封裝來源有一或多個版本，則會傳回200狀態碼。 回應主體是具有下列屬性的 JSON 物件：

名稱     | 類型             | 必要 | 備註
-------- | ---------------- | -------- | -----
versions | 字串陣列 | 是      | 可用的版本

陣列中的字串 `versions` 全都是小寫、 [正規化的 NuGet 版本字串](../concepts/package-versioning.md#normalized-version-numbers)。 版本字串不包含任何 SemVer 2.0.0 組建中繼資料。

其目的是在此陣列中找到的版本字串可以逐字用於 `LOWER_VERSION` 下列端點中的標記。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>下載套件內容 (. nupkg) 

如果用戶端知道套件識別碼和版本，並且想要下載套件內容，則只需要建立下列 URL：

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>要求參數

名稱          | 位於     | 類型   | 必要 | 備註
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | 字串 | 是      | 封裝識別碼，小寫
LOWER_VERSION | URL    | 字串 | 是      | 封裝版本（正規化和小寫）

`LOWER_ID`和 `LOWER_VERSION` 都是使用所執行的規則來小寫。NET[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)
方法。

`LOWER_VERSION`是使用 NuGet 的版本正規化[規則](../concepts/package-versioning.md#normalized-version-numbers)正規化所需的套件版本。 這表示在此案例中，必須排除 SemVer 2.0.0 規格所允許的組建中繼資料。

### <a name="response-body"></a>回應本文

如果封裝存在於套件來源，則會傳回200狀態碼。 回應主體會是套件內容本身。

如果封裝來源不存在封裝，則會傳回404狀態碼。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>範例回應

Nupkg 的二進位資料流程，適用于9.0.1 上的 Newtonsoft.Js。

## <a name="download-package-manifest-nuspec"></a>下載套件資訊清單 (. nuspec) 

如果用戶端知道套件識別碼和版本，並且想要下載套件資訊清單，則只需要建立下列 URL：

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>要求參數

名稱          | 位於     | 類型   | 必要 | 備註
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | 字串 | 是      | 封裝識別碼，小寫
LOWER_VERSION | URL    | 字串 | 是      | 封裝版本（正規化和小寫）

`LOWER_ID`和 `LOWER_VERSION` 都是使用所執行的規則來小寫。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) 方法。

`LOWER_VERSION`是使用 NuGet 的版本正規化[規則](../concepts/package-versioning.md#normalized-version-numbers)正規化所需的套件版本。 這表示在此案例中，必須排除 SemVer 2.0.0 規格所允許的組建中繼資料。

### <a name="response-body"></a>回應本文

如果封裝存在於套件來源，則會傳回200狀態碼。 回應本文將會是套件資訊清單，也就是包含在對應的 nupkg 中的 nuspec。 Nuspec 是一份 XML 檔。

如果封裝來源不存在封裝，則會傳回404狀態碼。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>範例回應

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
