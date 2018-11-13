---
title: 推送符號套件，NuGet API |Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 發行 」 服務可讓用戶端發佈新的符號套件。
keywords: NuGet API 推送符號套件
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580411"
---
# <a name="push-symbol-packages"></a>推送符號套件

可將套件推送符號 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用 NuGet V3 API。
這些作業會為基礎`SymbolPackagePublish`資源中找到[服務索引](service-index.md)。

## <a name="versioning"></a>版本控制

下列`@type`會使用值：

@type 值                 | 注意
--------------------        | -----
SymbolPackagePublish/4.9.0  | 初始版本

## <a name="base-url"></a>基礎 URL

下列 Api 的基底 URL 是值`@id`的屬性`SymbolPackagePublish/4.9.0`封裝來源中的資源[服務索引](service-index.md)。 下列文件，會使用 nuget.org 的 URL。 請考慮`https://www.nuget.org/api/v2/symbolpackage`作為預留位置`@id`服務索引中找到的值。

## <a name="http-methods"></a>HTTP 方法

`PUT`這項資源所支援 HTTP 方法。 

## <a name="push-a-symbol-package"></a>推送符號套件

nuget.org 支援推送新的符號套件格式 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用下列 API。 

    PUT https://www.nuget.org/api/v2/symbolpackage

具有相同的識別碼和版本的符號套件可以提交多次。 在下列情況下，將會遭到拒絕符號套件。
- 具有相同的識別碼和版本的封裝不存在。
- 已推送符號套件具有相同的識別碼和版本，但尚未發行。
- 符號套件 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 是無效的 (請參閱[符號套件條件約束](../create-packages/Symbol-Packages-snupkg.md))。

### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 頁首 | 字串 | 是      | 例如： `X-NuGet-ApiKey: {USER_API_KEY}` 

API 金鑰是不透明的字串，從套件來源取得的使用者，並在用戶端設定。 沒有特定字串的格式託管，但 API 金鑰的長度不應超過合理的大小，如 HTTP 標頭值。

### <a name="request-body"></a>要求本文

符號發送的要求主體是相同套件的推播要求的要求本文 (請參閱[封裝推送和刪除](package-publish-resource.md))。 

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
201         | 已成功推送符號套件。
400         | 提供的符號套件無效。
401         | 使用者未獲授權執行此動作。
404         | 使用提供的識別碼和版本對應的封裝不存在。
409         | 已推送符號套件具有提供的識別碼和版本，但它尚未提供。
413         | 封裝是太大。

