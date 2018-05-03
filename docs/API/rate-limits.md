---
title: 速率限制，NuGet API
description: NuGet 的 Api 將會強制執行速率限制，以防止不當使用。
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 3aaebef8fff670759c6484a5a8f90a2f4dd58c66
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="rate-limits"></a><span data-ttu-id="79dd5-103">速率限制</span><span class="sxs-lookup"><span data-stu-id="79dd5-103">Rate Limits</span></span>

<span data-ttu-id="79dd5-104">會強制執行 NuGet.org API，以防止不當使用的速率限制。</span><span class="sxs-lookup"><span data-stu-id="79dd5-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="79dd5-105">超過速率限制的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="79dd5-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="79dd5-106">下表列出 NuGet.org api 的速率限制。</span><span class="sxs-lookup"><span data-stu-id="79dd5-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="79dd5-107">封裝搜尋</span><span class="sxs-lookup"><span data-stu-id="79dd5-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="79dd5-108">我們建議您使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)目前搜尋高效能且沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="79dd5-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="79dd5-109">V1 和 V2 搜尋應用程式開發介面，followins 限制適用於：</span><span class="sxs-lookup"><span data-stu-id="79dd5-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="79dd5-110">API</span><span class="sxs-lookup"><span data-stu-id="79dd5-110">API</span></span> | <span data-ttu-id="79dd5-111">限制類型</span><span class="sxs-lookup"><span data-stu-id="79dd5-111">Limit Type</span></span> | <span data-ttu-id="79dd5-112">限制值</span><span class="sxs-lookup"><span data-stu-id="79dd5-112">Limit Value</span></span> | <span data-ttu-id="79dd5-113">應用程式開發介面 usecase</span><span class="sxs-lookup"><span data-stu-id="79dd5-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="79dd5-114">**取得** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="79dd5-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="79dd5-115">IP</span><span class="sxs-lookup"><span data-stu-id="79dd5-115">IP</span></span> | <span data-ttu-id="79dd5-116">1000 / 分</span><span class="sxs-lookup"><span data-stu-id="79dd5-116">1000 / minute</span></span> | <span data-ttu-id="79dd5-117">查詢 NuGet 套件中繼資料，透過 v1 OData`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="79dd5-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="79dd5-118">**取得** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="79dd5-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="79dd5-119">IP</span><span class="sxs-lookup"><span data-stu-id="79dd5-119">IP</span></span> | <span data-ttu-id="79dd5-120">3000 / 分</span><span class="sxs-lookup"><span data-stu-id="79dd5-120">3000 / minute</span></span> | <span data-ttu-id="79dd5-121">搜尋 v1 搜尋端點透過 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="79dd5-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="79dd5-122">**取得** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="79dd5-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="79dd5-123">IP</span><span class="sxs-lookup"><span data-stu-id="79dd5-123">IP</span></span> | <span data-ttu-id="79dd5-124">20000 / 分</span><span class="sxs-lookup"><span data-stu-id="79dd5-124">20000 / minute</span></span> | <span data-ttu-id="79dd5-125">查詢 NuGet 套件中繼資料，透過 v2 OData`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="79dd5-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="79dd5-126">**取得** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="79dd5-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="79dd5-127">IP</span><span class="sxs-lookup"><span data-stu-id="79dd5-127">IP</span></span> | <span data-ttu-id="79dd5-128">100 / 分</span><span class="sxs-lookup"><span data-stu-id="79dd5-128">100 / minute</span></span> | <span data-ttu-id="79dd5-129">查詢透過 v2 OData 的 NuGet 封裝計數`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="79dd5-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="79dd5-130">封裝發送和 Unlist</span><span class="sxs-lookup"><span data-stu-id="79dd5-130">Package Push and Unlist</span></span>

| <span data-ttu-id="79dd5-131">API</span><span class="sxs-lookup"><span data-stu-id="79dd5-131">API</span></span> | <span data-ttu-id="79dd5-132">限制類型</span><span class="sxs-lookup"><span data-stu-id="79dd5-132">Limit Type</span></span> | <span data-ttu-id="79dd5-133">限制值</span><span class="sxs-lookup"><span data-stu-id="79dd5-133">Limit Value</span></span> | <span data-ttu-id="79dd5-134">動力 usecase</span><span class="sxs-lookup"><span data-stu-id="79dd5-134">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="79dd5-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="79dd5-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="79dd5-136">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="79dd5-136">API Key</span></span> | <span data-ttu-id="79dd5-137">100 / 分</span><span class="sxs-lookup"><span data-stu-id="79dd5-137">100 / minute</span></span> | <span data-ttu-id="79dd5-138">上傳新的 NuGet 封裝 （版本） 透過 v2 推入端點</span><span class="sxs-lookup"><span data-stu-id="79dd5-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="79dd5-139">**刪除** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="79dd5-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="79dd5-140">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="79dd5-140">API Key</span></span> | <span data-ttu-id="79dd5-141">100 / 分</span><span class="sxs-lookup"><span data-stu-id="79dd5-141">100 / minute</span></span> | <span data-ttu-id="79dd5-142">Unlist v2 端點透過 NuGet 封裝 （版本）</span><span class="sxs-lookup"><span data-stu-id="79dd5-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
