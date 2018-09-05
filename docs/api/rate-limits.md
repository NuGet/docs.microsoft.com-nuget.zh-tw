---
title: 速率限制，NuGet API
description: NuGet Api 將會強制執行以避免不當使用的速率限制。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548673"
---
# <a name="rate-limits"></a>速率限制

NuGet.org API 會強制執行以避免不當使用的速率限制。 超過速率限制的要求會傳回下列錯誤： 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

除了要求節流使用速率限制，某些 Api 也會強制執行配額。 超過配額的要求會傳回下列錯誤：

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

下表列出 NuGet.org API 速率限制。

## <a name="package-search"></a>套件搜尋

> [!Note]
> 我們建議使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)目前搜尋的效能，而且沒有任何限制。 V1 和 V2 搜尋 Api、 followins 限制適用於：


| API | 限制類型 | 限制值 | API usecase |
|:---|:---|:---|:---|
**取得** `/api/v1/Packages` | IP | 1000 / 分鐘 | 查詢 NuGet 套件中繼資料，透過 v1 OData`Packages`集合 |
**取得** `/api/v1/Search()` | IP | 3000 / 分鐘 | 搜尋 NuGet 套件透過 v1 搜尋端點 | 
**取得** `/api/v2/Packages` | IP | 20000 / 分鐘 | 查詢 NuGet 套件中繼資料，透過 v2 OData`Packages`集合 | 
**取得** `/api/v2/Packages/$count` | IP | 100 / 分鐘 | 查詢透過 v2 OData 的 NuGet 套件數目`Packages`集合 | 

## <a name="package-push-and-unlist"></a>封裝將推送，並取消列出

| API | 限制類型 | 限制值 | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 金鑰 | 250 / 小時 | 上傳新的 NuGet 封裝 （版本） 透過 v2 推播端點 
**刪除** `/api/v2/package/{id}/{version}` | API 金鑰 | 250 / 小時 | 取消列出透過 v2 端點的 NuGet 套件 （版本） 
