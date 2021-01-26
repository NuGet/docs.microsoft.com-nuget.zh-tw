---
title: 推送符號套件，NuGet API |Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 發行服務可讓用戶端發佈新的符號套件。
keywords: NuGet API 推送符號套件
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773893"
---
# <a name="push-symbol-packages"></a>推送符號套件

您可以使用 NuGet V3 API 將符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 推送。
這些作業是 `SymbolPackagePublish` 以 [服務索引](service-index.md)中找到的資源為基礎。

## <a name="versioning"></a>版本控制

使用的 `@type` 值如下：

@type 值                 | 備註
--------------------        | -----
SymbolPackagePublish/4.9。0  | 初始版本

## <a name="base-url"></a>基底 URL

下列 Api 的基底 URL 是 `@id` `SymbolPackagePublish/4.9.0` 套件來源之 [服務索引](service-index.md)中資源的屬性值。 針對下列檔，會使用 nuget. org 的 URL。 請考慮 `https://www.nuget.org/api/v2/symbolpackage` 作為 `@id` 服務索引中找到之值的預留位置。

## <a name="http-methods"></a>HTTP 方法

`PUT`此資源支援 HTTP 方法。 

## <a name="push-a-symbol-package"></a>推送符號套件

nuget.org 支援使用下列 API 來推送新的符號套件格式 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 。 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

具有相同識別碼和版本的符號套件可以提交多次。 在下列情況下，將會拒絕符號套件。
- 具有相同識別碼和版本的套件不存在。
- 已推送具有相同識別碼和版本的符號套件，但尚未發佈。
- 符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 無效 (請參閱 [符號封裝條件約束](../create-packages/Symbol-Packages-snupkg.md)) 。

### <a name="request-parameters"></a>要求參數

名稱           | 位於     | 類型   | 必要 | 備註
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 標頭 | 字串 | 是      | 例如， `X-NuGet-ApiKey: {USER_API_KEY}`

API 金鑰是由使用者從套件來源取得並設定為用戶端的不透明字串。 未強制採用任何特定的字串格式，但 API 金鑰的長度不應超過 HTTP 標頭值的合理大小。

### <a name="request-body"></a>要求本文

符號推送的要求主體與封裝推送要求的要求主體相同 (請參閱 [封裝推送和刪除](package-publish-resource.md)) 。 

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
201         | 已成功推送符號套件。
400         | 提供的符號套件無效。
401         | 使用者未獲授權執行此動作。
404         | 具有所提供識別碼和版本的對應套件不存在。
409         | 已推送具有所提供識別碼和版本的符號套件，但尚未提供。
413         | 封裝太大。

