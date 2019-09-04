---
title: 推送符號套件, NuGet API |Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 發行服務可讓用戶端發佈新的符號套件。
keywords: NuGet API 推送符號套件
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235102"
---
# <a name="push-symbol-packages"></a>推送符號套件

您可以使用 NuGet V3 API 推送符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md))。
這些作業是以[服務索引](service-index.md)中`SymbolPackagePublish`找到的資源為基礎。

## <a name="versioning"></a>版本控制

會使用`@type`下列值:

@type 值                 | 注意
--------------------        | -----
SymbolPackagePublish/4.9。0  | 初始版本

## <a name="base-url"></a>基礎 URL

下列 api 的基底 URL 是封裝來源之`@id` [服務索引](service-index.md)中`SymbolPackagePublish/4.9.0`資源的屬性值。 下列檔中會使用 nuget. org 的 URL。 請`https://www.nuget.org/api/v2/symbolpackage`考慮當做服務索引中`@id`找到之值的預留位置。

## <a name="http-methods"></a>HTTP 方法

此資源支援 HTTP 方法。 `PUT` 

## <a name="push-a-symbol-package"></a>推送符號套件

nuget.org 支援使用下列 API 來推送新的符號套件格式 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md))。 

    PUT https://www.nuget.org/api/v2/symbolpackage

具有相同識別碼和版本的符號套件可以多次提交。 在下列情況下, 將會拒絕符號套件。
- 具有相同識別碼和版本的封裝不存在。
- 已推送具有相同識別碼和版本的符號套件, 但尚未發行。
- 符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 無效 (請參閱[符號封裝條件約束](../create-packages/Symbol-Packages-snupkg.md))。

### <a name="request-parameters"></a>要求參數

名稱           | In     | 類型   | 必要 | 注意
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 標頭 | 字串 | 是      | 例如： `X-NuGet-ApiKey: {USER_API_KEY}`

API 金鑰是由使用者從封裝來源取得的不透明字串, 並設定在用戶端中。 不會強制使用特定的字串格式, 但 API 金鑰的長度不應該超過 HTTP 標頭值的合理大小。

### <a name="request-body"></a>要求本文

符號推送的要求本文與套件推播要求的要求本文相同 (請參閱[封裝推送和刪除](package-publish-resource.md))。 

### <a name="response"></a>回應

狀態碼 | 意義
----------- | -------
201         | 已成功推送符號套件。
400         | 提供的符號套件無效。
401         | 使用者未獲授權, 無法執行此動作。
404         | 具有所提供識別碼和版本的對應封裝不存在。
409         | 已推送具有所提供識別碼和版本的符號套件, 但尚未提供。
413         | 封裝太大。

