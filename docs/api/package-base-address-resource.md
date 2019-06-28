---
title: 封裝內容，NuGet API
description: 封裝的基底位址是一個簡單的介面，以擷取封裝本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426758"
---
# <a name="package-content"></a>封裝內容

可以產生 URL，以擷取使用 V3 API 的任意套件的內容 （.nupkg 檔案）。 用於擷取套件內容資源`PackageBaseAddress`資源中找到[服務索引](service-index.md)。 此資源也可讓封裝時，所列出的所有版本的探索或未列出。

此資源統稱為 「 封裝基底位址 」 或 「 一般容器 」。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值              | 注意
------------------------ | -----
PackageBaseAddress/3.0.0 | 初始版本

## <a name="base-url"></a>基礎 URL

下列 Api 的基底 URL 是值`@id`上述的資源相關聯的屬性`@type`值。 在下列的文件中的預留位置基底 URL`{@id}`將使用。

## <a name="http-methods"></a>HTTP 方法

所有 Url 的 HTTP 方法位於註冊資源的支援`GET`和`HEAD`。

## <a name="enumerate-package-versions"></a>列舉套件版本

如果用戶端知道的封裝識別碼，並想要探索的封裝版本的封裝來源可用，用戶端可以建構可預測的 URL 來列舉所有的套件版本。 這份清單會是用來 「 目錄清單 」，如下所述的套件內容 api。

> [!Note]
> 此清單包含兩個列出與未列出的套件版本。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求參數

名稱     | In     | 類型    | 必要 | 注意
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字串  | 是      | 封裝識別碼、 小寫字母

`LOWER_ID`值是小寫使用規則實作所需的套件識別碼。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>回應

如果套件來源不具有提供的套件識別碼的任何版本，則會傳回 404 狀態碼。

如果套件來源具有一個或多個版本，則會傳回 200 狀態碼。 回應主體是具有下列屬性的 JSON 物件：

名稱     | 類型             | 必要 | 注意
-------- | ---------------- | -------- | -----
版本 | 字串陣列 | 是      | 封裝識別碼可用

中的字串`versions`全部小寫陣列，[正規化 NuGet 版本字串](../reference/package-versioning.md#normalized-version-numbers)。 版本字串不包含任何的 SemVer 2.0.0 組建中繼資料。

其目的是，此陣列中找到的版本字串可以用於逐字`LOWER_VERSION`下列端點中找到的語彙基元。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>下載套件內容 (.nupkg)

如果用戶端知道的套件識別碼和版本，而且想要下載套件內容，他們只需要建構下列 URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>要求參數

名稱          | In     | 類型   | 必要 | 注意
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | 字串 | 是      | 封裝識別碼、 小寫字母
LOWER_VERSION | URL    | 字串 | 是      | 套件版本，並以標準化小寫

兩者`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
方法。

`LOWER_VERSION`所需的套件版本使用標準化 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。 這表示必須在此情況下排除組建中繼資料所允許的 SemVer 2.0.0 規格。

### <a name="response-body"></a>回應本文

如果封裝存在於封裝來源，則會傳回 200 狀態碼。 回應主體會封裝內容本身。

如果封裝不存在套件來源，則會傳回 404 狀態碼。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>範例回應

二進位資料流是.nupkg Newtonsoft.Json 9.0.1 （英文)。

## <a name="download-package-manifest-nuspec"></a>下載封裝資訊清單 (.nuspec)

如果用戶端知道的套件識別碼和版本，而且想要下載的封裝資訊清單，他們只需要建構下列 URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>要求參數

名稱          | In     | 類型   | 必要 | 注意
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | 字串 | 是      | 封裝識別碼、 小寫字母
LOWER_VERSION | URL    | 字串 | 是      | 套件版本，並以標準化小寫

兩者`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

`LOWER_VERSION`所需的套件版本使用標準化 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。 這表示必須在此情況下排除組建中繼資料所允許的 SemVer 2.0.0 規格。

### <a name="response-body"></a>回應本文

如果封裝存在於封裝來源，則會傳回 200 狀態碼。 回應主體會是包含在對應的.nupkg.nuspec 套件資訊清單。 .nuspec 是 XML 文件。

如果封裝不存在套件來源，則會傳回 404 狀態碼。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>範例回應

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
