---
title: "封裝的內容，NuGet API |Microsoft 文件"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: ec68b5d1-a684-4995-b1a6-6210dbb24875
description: "封裝的基底位址是一個簡單的介面，以擷取封裝本身。"
keywords: "NuGet 的一般容器、 NuGet 封裝基底地址、 NuGet nupkg API，API NuGet 套件的版本中，NuGet API 未列出的套件，NuGet API 下載 nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: a581f9854410bc1a84d65310b38928a1d889ece2
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="package-content"></a>封裝內容

很可能產生的 URL 來擷取使用 V3 應用程式開發介面的任意套件的內容 （.nupkg 檔案）。 用於擷取套件內容的資源是`PackageBaseAddress`資源中找到[服務索引](service-index.md)。 此資源也可讓封裝時，所列出的所有版本的探索或未列出。

此資源通常稱為為任一個 「 封裝基底位址 」 或 「 一般容器 >。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值              | 注意
------------------------ | -----
PackageBaseAddress/3.0.0 | 初版

## <a name="base-url"></a>基礎 URL

下列應用程式開發介面的基底 URL 是值`@id`上述資源相關聯的屬性`@type`值。 下列文件預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。

## <a name="enumerate-package-versions"></a>列舉封裝版本

如果用戶端知道封裝識別碼，而且想要探索的封裝版本的封裝來源可供使用，用戶端可以建構列舉所有的封裝版本的可預測的 URL。 這份清單會是用來 「 目錄清單 」，如下所述的套件內容 api。

> [!Note]
> 此清單包含兩個列出與未列出的套件版本。

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>要求參數

名稱     | In     | 類型    | 必要 | 注意
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼、 小寫

`LOWER_ID`值是小寫使用所實作的規則所需的封裝識別碼。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>回應

如果套件來源已不提供的封裝識別碼的版本，則會傳回 404 狀態碼。

如果套件來源具有一個或多個版本，則會傳回 200 狀態碼。 回應主體是使用下列屬性的 JSON 物件：

名稱     | 類型             | 必要 | 注意
-------- | ---------------- | -------- | -----
版本 | 字串陣列 | 是      | 封裝識別碼可用

中的字串`versions`所有小寫陣列，[正規化 NuGet 版本字串](../reference/package-versioning.md#normalized-version-numbers)。 版本字串不包含任何 SemVer 2.0.0 建置中繼資料。

其目的是，這個陣列中找到的版本字串可以用於逐字`LOWER_VERSION`下列端點中找到的語彙基元。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>下載封裝內容 (.nupkg)

如果用戶端知道套件識別碼和版本，而且想要下載封裝內容，他們只需要建構下列 URL:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>要求參數

名稱          | In     | 類型   | 必要 | 注意
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | 字串 | 是      | 封裝識別碼、 小寫
LOWER_VERSION | URL    | 字串 | 是      | 封裝版本，正規化和小寫

同時`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

`LOWER_VERSION`所需的封裝版本都是使用 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。 這表示，允許使用 SemVer 2.0.0 規格的建置中繼資料，必須排除在此情況下。

### <a name="response-body"></a>回應本文

如果封裝存在於封裝來源，則會傳回 200 狀態碼。 回應主體會將封裝內容本身。

如果封裝不存在套件來源上，則會傳回 404 狀態碼。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>範例回應

表示如 Newtonsoft.Json 9.0.1.nupkg 二進位資料流。

## <a name="download-package-manifest-nuspec"></a>下載封裝資訊清單 (.nuspec)

如果用戶端知道套件識別碼和版本，而且想要下載的封裝資訊清單，只需要建構下列 URL:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>要求參數

名稱          | In     | 類型    | 必要 | 注意
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | 字串  | 是      | 封裝識別碼、 小寫
LOWER_VERSION | URL    | 整數 | 是      | 封裝版本，正規化和小寫

同時`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

`LOWER_VERSION`所需的封裝版本都是使用 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。 這表示，允許使用 SemVer 2.0.0 規格的建置中繼資料，必須排除在此情況下。

### <a name="response-body"></a>回應本文

如果封裝存在於封裝來源，則會傳回 200 狀態碼。 回應主體會是包含在對應的.nupkg.nuspec 封裝資訊清單。 .nuspec 是 XML 文件。

如果封裝不存在套件來源上，則會傳回 404 狀態碼。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>範例回應

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
