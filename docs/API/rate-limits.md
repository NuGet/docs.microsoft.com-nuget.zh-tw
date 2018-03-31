---
title: 速率限制 |Microsoft 文件
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet 的 Api 將會強制執行速率限制，以防止不當使用。
keywords: NuGet 的 API，速率限制
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a>速率限制

會強制執行 NuGet.org API，以防止不當使用的速率限制。 超過速率限制的要求會傳回下列錯誤： 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

下表列出 NuGet.org api 的速率限制。

## <a name="package-search"></a>封裝搜尋

> [!Note]
> 我們建議您使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)目前搜尋高效能且沒有任何限制。 V1 和 V2 搜尋應用程式開發介面，followins 限制適用於：


| API | 限制類型 | 限制值 | 應用程式開發介面 usecase |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 / 分 | 查詢 NuGet 套件中繼資料，透過 v1 OData`Packages`集合 |
**GET** `/api/v1/Search()` | IP | 3000 / 分 | 搜尋 v1 搜尋端點透過 NuGet 封裝 | 
**GET** `/api/v2/Packages` | IP | 20000 / 分 | 查詢 NuGet 套件中繼資料，透過 v2 OData`Packages`集合 | 
**GET** `/api/v2/Packages/$count` | IP | 100 / 分 | 查詢透過 v2 OData 的 NuGet 封裝計數`Packages`集合 | 

## <a name="package-push-and-unlist"></a>封裝發送和 Unlist

| API | 限制類型 | 限制值 | 動力 usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 金鑰 | 100 / 分 | 上傳新的 NuGet 封裝 （版本） 透過 v2 推入端點 
**刪除** `/api/v2/package/{id}/{version}` | API 金鑰 | 100 / 分 | Unlist v2 端點透過 NuGet 封裝 （版本） 
