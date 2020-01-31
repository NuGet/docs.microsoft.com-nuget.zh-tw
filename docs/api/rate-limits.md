---
title: 速率限制，NuGet API
description: NuGet Api 會強制執行速率限制，以防止濫用。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813191"
---
# <a name="rate-limits"></a>速率限制

NuGet.org API 會強制執行速率限制，以防止濫用。 超過速率限制的要求會傳回下列錯誤： 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

除了使用速率限制的要求節流以外，某些 Api 也會強制執行配額。 超過配額的要求會傳回下列錯誤：

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

下表列出 NuGet.org API 的速率限制。

## <a name="package-search"></a>封裝搜尋

> [!Note]
> 我們建議使用 NuGet. 組織的[V3 搜尋 api](search-query-service-resource.md) ，因為它目前不受速率限制。 針對 V1 和 V2 搜尋 Api，適用下列限制：

| API | 限制類型 | 限制值 | API usecase |
|:---|:---|:---|:---|
**取得**`/api/v1/Packages` | IP | 1000/分鐘 | 透過 v1 OData `Packages` 收集來查詢 NuGet 套件中繼資料 |
**取得**`/api/v1/Search()` | IP | 3000/分鐘 | 透過 v1 搜尋端點搜尋 NuGet 套件 | 
**取得**`/api/v2/Packages` | IP | 20000/分鐘 | 透過 v2 OData `Packages` 收集來查詢 NuGet 套件中繼資料 | 
**取得**`/api/v2/Packages/$count` | IP | 100/分鐘 | 透過 v2 OData `Packages` 收集來查詢 NuGet 封裝計數 | 

## <a name="package-push-and-unlist"></a>封裝推送和取消列出

| API | 限制類型 | 限制值 | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 金鑰 | 350/小時 | 透過 v2 推播端點上傳新的 NuGet 套件（版本） 
**刪除**`/api/v2/package/{id}/{version}` | API 金鑰 | 250/小時 | 透過 v2 端點取消列出 NuGet 套件（版本） 
