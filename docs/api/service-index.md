---
title: 服務索引，NuGet API
description: 服務索引是 NuGet HTTP API 的進入點，而且會列舉伺服器的功能。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775356"
---
# <a name="service-index"></a>服務索引

服務索引是一個 JSON 檔，它是 NuGet 套件來源的進入點，可讓用戶端執行探索套件來源的功能。 服務索引是具有兩個必要屬性的 JSON 物件： `version` (服務索引的架構版本) 和 `resources`  (套件來源) 的端點或功能。

nuget.exe 的服務索引位於 `https://api.nuget.org/v3/index.json` 。

## <a name="versioning"></a>版本控制

`version`值是 SemVer 2.0.0 剖析或是版本字串，表示服務索引的架構版本。 API 會要求版本字串具有的主要版本號碼 `3` 。 對服務索引架構進行非中斷的變更時，將會增加版本字串的次要版本。

服務索引中的每個資源都會與服務索引架構版本分開建立版本。

目前的架構版本是 `3.0.0` 。 `3.0.0`版本的功能等同于較舊的 `3.0.0-beta.1` 版本，但應優先于更明確地傳達穩定的已定義架構。

## <a name="http-methods"></a>HTTP 方法

您可以使用 HTTP 方法和來存取服務索引 `GET` `HEAD` 。

## <a name="resources"></a>資源

`resources`屬性包含此封裝來源所支援的資源陣列。

### <a name="resource"></a>資源

資源是陣列中的物件 `resources` 。 它代表套件來源的已建立版本功能。 資源具有下列屬性：

名稱          | 類型   | 必要 | 備註
------------- | ------ | -------- | -----
@id           | 字串 | 是      | 資源的 URL
@type         | 字串 | 是      | 代表資源類型的字串常數。
comment       | 字串 | 不可以       | 人們看得懂的資源描述

`@id`是必須是絕對的 URL，而且必須有 HTTP 或 HTTPS 架構。

`@type`用來識別與資源互動時要使用的特定通訊協定。 資源的類型是不透明的字串，但其格式通常為：

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

用戶端預期會將其瞭解的值硬編碼， `@type` 並在套件來源的服務索引中查詢它們。 `@type`目前使用的確切值會列舉在[API 總覽](overview.md#resources-and-schema)中列出的個別資源參考檔上。

基於本檔的目的，有關不同資源的檔基本上會依在 `{RESOURCE_NAME}` 服務索引中找到的分組，類似于依案例分組。 

不需要每個資源都有唯一的 `@id` 或 `@type` 。 用戶端會決定要使用哪一種資源。 其中一個可能的執行，就是 `@type` 當連接失敗或伺服器錯誤時，可以使用迴圈配置資源的方式來使用相同或相容的資源。

### <a name="sample-request"></a>範例要求

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>範例回應

[!code-JSON [service-index.json](./_data/service-index.json)]
