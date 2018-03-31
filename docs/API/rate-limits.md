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
# <a name="rate-limits"></a><span data-ttu-id="4555a-104">速率限制</span><span class="sxs-lookup"><span data-stu-id="4555a-104">Rate Limits</span></span>

<span data-ttu-id="4555a-105">會強制執行 NuGet.org API，以防止不當使用的速率限制。</span><span class="sxs-lookup"><span data-stu-id="4555a-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="4555a-106">超過速率限制的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="4555a-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="4555a-107">下表列出 NuGet.org api 的速率限制。</span><span class="sxs-lookup"><span data-stu-id="4555a-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="4555a-108">封裝搜尋</span><span class="sxs-lookup"><span data-stu-id="4555a-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="4555a-109">我們建議您使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)目前搜尋高效能且沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="4555a-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="4555a-110">V1 和 V2 搜尋應用程式開發介面，followins 限制適用於：</span><span class="sxs-lookup"><span data-stu-id="4555a-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="4555a-111">API</span><span class="sxs-lookup"><span data-stu-id="4555a-111">API</span></span> | <span data-ttu-id="4555a-112">限制類型</span><span class="sxs-lookup"><span data-stu-id="4555a-112">Limit Type</span></span> | <span data-ttu-id="4555a-113">限制值</span><span class="sxs-lookup"><span data-stu-id="4555a-113">Limit Value</span></span> | <span data-ttu-id="4555a-114">應用程式開發介面 usecase</span><span class="sxs-lookup"><span data-stu-id="4555a-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="4555a-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="4555a-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="4555a-116">IP</span><span class="sxs-lookup"><span data-stu-id="4555a-116">IP</span></span> | <span data-ttu-id="4555a-117">1000 / 分</span><span class="sxs-lookup"><span data-stu-id="4555a-117">1000 / minute</span></span> | <span data-ttu-id="4555a-118">查詢 NuGet 套件中繼資料，透過 v1 OData`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="4555a-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="4555a-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="4555a-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="4555a-120">IP</span><span class="sxs-lookup"><span data-stu-id="4555a-120">IP</span></span> | <span data-ttu-id="4555a-121">3000 / 分</span><span class="sxs-lookup"><span data-stu-id="4555a-121">3000 / minute</span></span> | <span data-ttu-id="4555a-122">搜尋 v1 搜尋端點透過 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="4555a-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="4555a-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="4555a-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="4555a-124">IP</span><span class="sxs-lookup"><span data-stu-id="4555a-124">IP</span></span> | <span data-ttu-id="4555a-125">20000 / 分</span><span class="sxs-lookup"><span data-stu-id="4555a-125">20000 / minute</span></span> | <span data-ttu-id="4555a-126">查詢 NuGet 套件中繼資料，透過 v2 OData`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="4555a-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="4555a-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="4555a-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="4555a-128">IP</span><span class="sxs-lookup"><span data-stu-id="4555a-128">IP</span></span> | <span data-ttu-id="4555a-129">100 / 分</span><span class="sxs-lookup"><span data-stu-id="4555a-129">100 / minute</span></span> | <span data-ttu-id="4555a-130">查詢透過 v2 OData 的 NuGet 封裝計數`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="4555a-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="4555a-131">封裝發送和 Unlist</span><span class="sxs-lookup"><span data-stu-id="4555a-131">Package Push and Unlist</span></span>

| <span data-ttu-id="4555a-132">API</span><span class="sxs-lookup"><span data-stu-id="4555a-132">API</span></span> | <span data-ttu-id="4555a-133">限制類型</span><span class="sxs-lookup"><span data-stu-id="4555a-133">Limit Type</span></span> | <span data-ttu-id="4555a-134">限制值</span><span class="sxs-lookup"><span data-stu-id="4555a-134">Limit Value</span></span> | <span data-ttu-id="4555a-135">動力 usecase</span><span class="sxs-lookup"><span data-stu-id="4555a-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="4555a-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="4555a-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="4555a-137">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="4555a-137">API Key</span></span> | <span data-ttu-id="4555a-138">100 / 分</span><span class="sxs-lookup"><span data-stu-id="4555a-138">100 / minute</span></span> | <span data-ttu-id="4555a-139">上傳新的 NuGet 封裝 （版本） 透過 v2 推入端點</span><span class="sxs-lookup"><span data-stu-id="4555a-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="4555a-140">**刪除** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="4555a-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="4555a-141">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="4555a-141">API Key</span></span> | <span data-ttu-id="4555a-142">100 / 分</span><span class="sxs-lookup"><span data-stu-id="4555a-142">100 / minute</span></span> | <span data-ttu-id="4555a-143">Unlist v2 端點透過 NuGet 封裝 （版本）</span><span class="sxs-lookup"><span data-stu-id="4555a-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
