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
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367930"
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

| API | 限制類型 | 限制值 | API 使用案例 |
|:---|:---|:---|:---|
**取得**`/api/v1/Packages` | IP | 1000/分鐘 | 透過 v1 OData 收集來查詢 NuGet 套件中繼資料 `Packages` |
**取得**`/api/v1/Search()` | IP | 3000/分鐘 | 透過 v1 搜尋端點搜尋 NuGet 套件 | 
**取得**`/api/v2/Packages` | IP | 20000/分鐘 | 透過 v2 OData 集合查詢 NuGet 套件中繼資料 `Packages` | 
**取得**`/api/v2/Packages/$count` | IP | 100/分鐘 | 透過 v2 OData 集合查詢 NuGet 封裝計數 `Packages` | 

## <a name="package-push-and-unlist"></a>封裝推送和取消列出

| API | 限制類型 | 限制值 | API 使用案例 | 
|:---|:---|:---|:--- |
**PUT**`/api/v2/package` | API 金鑰 | 350/小時 | 透過 v2 推播端點上傳新的 NuGet 套件（版本） 
**刪除**`/api/v2/package/{id}/{version}` | API 金鑰 | 250/小時 | 透過 v2 端點取消列出 NuGet 套件（版本） 

## <a name="nugetorg-website-page-views"></a>nuget.org 網站頁面流覽

如果您以程式設計方式存取 nuget.org 網頁，請考慮調查我們記載的[V3 api](overview.md)。 這些端點可讓您更輕鬆地存取套件中繼資料和內容。 V3 API 具有更高的可用性，且效能高於存取 NuGet 資源庫網頁（專為網頁瀏覽器互動而設計）。

| API | 限制類型 | 限制值 | API 使用案例 | 
|:---|:---|:---|:--- |
**取得**`/package/{id}/{version}` | IP | 50/分鐘 | 顯示套件（版本）詳細資料頁面。 
