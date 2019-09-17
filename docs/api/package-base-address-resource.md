---
title: 套件內容，NuGet API
description: 封裝基底位址是一個簡單的介面，可供提取封裝本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488225"
---
# <a name="package-content"></a>封裝內容

您可以使用 V3 API 來產生 URL，以提取任意套件的內容（nupkg 檔案）。 用來提取封裝內容的資源是`PackageBaseAddress`在[服務索引](service-index.md)中找到的資源。 此資源也可讓您探索已列出或未列出的所有套件版本。

這項資源通常稱為「套件基底位址」或「平面容器」。

## <a name="versioning"></a>版本控制

會使用`@type`下列值：

@type 值              | 注意
------------------------ | -----
PackageBaseAddress/3.0.0 | 初始版本

## <a name="base-url"></a>基礎 URL

下列 api 的基底 URL 是與上述資源`@id` `@type`值相關聯的屬性值。 在下列檔中，將會使用預留位置`{@id}`基底 URL。

## <a name="http-methods"></a>HTTP 方法

在註冊資源中找到的所有 url 都支援 HTTP `GET`方法`HEAD`和。

## <a name="enumerate-package-versions"></a>列舉封裝版本

如果用戶端知道套件識別碼，而且想要探索封裝來源可用的封裝版本，用戶端可以建立可預測的 URL 來列舉所有套件版本。 這份清單應該是下面所述套件內容 API 的「目錄清單」。

> [!Note]
> 這份清單同時包含列出和未列出的套件版本。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求參數

名稱     | In     | 類型    | 必要 | 注意
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼，小寫

`LOWER_ID`值是所需的套件識別碼小寫，使用由所執行的規則。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>回應

如果封裝來源沒有提供的套件識別碼版本，則會傳回404狀態碼。

如果封裝來源有一或多個版本，則會傳回200狀態碼。 回應主體是具有下列屬性的 JSON 物件：

名稱     | 類型             | 必要 | 注意
-------- | ---------------- | -------- | -----
版本 | 字串陣列 | 是      | 可用的套件識別碼

`versions`陣列中的字串都是小寫、[正規化的 NuGet 版本字串](../concepts/package-versioning.md#normalized-version-numbers)。 版本字串不包含任何 SemVer 的2.0.0 組建中繼資料。

其目的是在此陣列中找到的版本字串可以逐字用於下列端點中`LOWER_VERSION`找到的權杖。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>下載套件內容（. nupkg）

如果用戶端知道套件識別碼和版本，而且想要下載封裝內容，則只需要建立下列 URL：

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>要求參數

名稱          | In     | 類型   | 必要 | 注意
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | 字串 | 是      | 封裝識別碼，小寫
LOWER_VERSION | URL    | 字串 | 是      | 封裝版本，正規化和小寫

`LOWER_ID` 和`LOWER_VERSION`都是使用所執行的規則小寫。NET[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
方法。

`LOWER_VERSION` 是使用 NuGet 版本[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)標準化的所需套件版本。 這表示在此情況下，必須排除 SemVer 2.0.0 規格所允許的組建中繼資料。

### <a name="response-body"></a>回應本文

如果封裝存在於套件來源上，則會傳回200狀態碼。 回應主體將會是封裝內容本身。

如果封裝不存在於套件來源上，則會傳回404狀態碼。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>範例回應

二進位資料流程，也就是 Newtonsoft 的 nupkg。

## <a name="download-package-manifest-nuspec"></a>下載套件資訊清單（. nuspec）

如果用戶端知道套件識別碼和版本，而且想要下載套件資訊清單，他們只需要建立下列 URL：

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>要求參數

名稱          | In     | 類型   | 必要 | 注意
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | 字串 | 是      | 封裝識別碼，小寫
LOWER_VERSION | URL    | 字串 | 是      | 封裝版本，正規化和小寫

`LOWER_ID` 和`LOWER_VERSION`都是使用所執行的規則小寫。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

`LOWER_VERSION` 是使用 NuGet 版本[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)標準化的所需套件版本。 這表示在此情況下，必須排除 SemVer 2.0.0 規格所允許的組建中繼資料。

### <a name="response-body"></a>回應本文

如果封裝存在於套件來源上，則會傳回200狀態碼。 回應主體將會是封裝資訊清單，也就是包含在對應 nupkg 中的 nuspec。 Nuspec 是一份 XML 檔。

如果封裝不存在於套件來源上，則會傳回404狀態碼。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>範例回應

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
