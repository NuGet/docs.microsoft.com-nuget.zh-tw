---
title: 服務的索引，NuGet API
description: 服務索引是 NuGet HTTP API 進入點，並列舉伺服器的功能。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324717"
---
# <a name="service-index"></a>服務索引

服務索引是 JSON 文件的 NuGet 套件來源的項目點並可讓用戶端實作探索的套件來源的功能。 服務索引是 JSON 物件，具有兩個必要屬性： `version` （服務索引的結構描述版本） 和`resources`（端點或功能的套件來源）。

nuget.org 的服務索引位於`https://api.nuget.org/v3/index.json`。

## <a name="versioning"></a>版本控制

`version`值是表示服務索引的結構描述版本的 SemVer 2.0.0 剖析版本字串。 API 要求的版本字串具有主要版本號碼`3`。 服務索引結構描述會進行非中斷變更，就會增加的版本字串的次要版本。

服務索引中的每個資源是獨立設定版本的服務索引結構描述版本。

目前的結構描述版本是`3.0.0`。 `3.0.0`版本功能上相當於舊版`3.0.0-beta.1`版本但應該是慣用，因為它更清楚地進行通訊的穩定、 定義結構描述。

## <a name="http-methods"></a>HTTP 方法

服務索引是使用 HTTP 方法存取`GET`和`HEAD`。

## <a name="resources"></a>資源

`resources`屬性包含此套件來源所支援的資源陣列。

### <a name="resource"></a>資源

資源是中的物件`resources`陣列。 它代表的套件來源的建立版本功能。 資源具有下列屬性：

名稱          | 類型   | 必要 | 注意
------------- | ------ | -------- | -----
@id           | 字串 | 是      | 資源 URL
@type         | 字串 | 是      | 字串常數，代表資源類型
註解       | 字串 | 否       | 可讀取描述的資源

`@id`是 URL，必須是絕對路徑，且必須是具有 HTTP 或 HTTPS 的結構描述。

`@type`用來識別與資源互動時所要使用的特定通訊協定。 資源的類型是不透明的字串，但通常具有格式：

    {RESOURCE_NAME}/{RESOURCE_VERSION}

用戶端必須硬`@type`他們了解，且這些查閱的套件來源的服務索引中的值。 確切`@type`現今使用的值會列舉中列出的個別資源的參考文件上[API 概觀](overview.md#resources-and-schema)。

本文件中，為了不同資源的相關文件將基本上分組`{RESOURCE_NAME}`相當於依案例分組服務索引中找到。 

沒有每個資源都有唯一的需求`@id`或`@type`。 這是由用戶端實作，以決定要透過另一個偏好使用的資源。 一個可能的實作在於相同或相容的資源`@type`可用以循環配置資源方式發生連線失敗或伺服器錯誤。

### <a name="sample-request"></a>範例要求

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>範例回應

[!code-JSON [service-index.json](./_data/service-index.json)]
