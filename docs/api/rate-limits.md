---
title: 速率限制，NuGet API
description: NuGet Api 將會強制執行以避免不當使用的速率限制。
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: a55eb49318b766028d1579a4d33618617bbd8801
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508123"
---
# <a name="rate-limits"></a><span data-ttu-id="5dbe4-103">速率限制</span><span class="sxs-lookup"><span data-stu-id="5dbe4-103">Rate Limits</span></span>

<span data-ttu-id="5dbe4-104">NuGet.org API 會強制執行以避免不當使用的速率限制。</span><span class="sxs-lookup"><span data-stu-id="5dbe4-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="5dbe4-105">超過速率限制的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="5dbe4-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="5dbe4-106">除了要求節流使用速率限制，某些 Api 也會強制執行配額。</span><span class="sxs-lookup"><span data-stu-id="5dbe4-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="5dbe4-107">超過配額的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="5dbe4-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="5dbe4-108">下表列出 NuGet.org API 速率限制。</span><span class="sxs-lookup"><span data-stu-id="5dbe4-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="5dbe4-109">套件搜尋</span><span class="sxs-lookup"><span data-stu-id="5dbe4-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="5dbe4-110">我們建議使用 NuGet.org 的[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)目前搜尋的效能，而且沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="5dbe4-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="5dbe4-111">V1 和 V2 搜尋 Api、 followins 限制適用於：</span><span class="sxs-lookup"><span data-stu-id="5dbe4-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="5dbe4-112">API</span><span class="sxs-lookup"><span data-stu-id="5dbe4-112">API</span></span> | <span data-ttu-id="5dbe4-113">限制類型</span><span class="sxs-lookup"><span data-stu-id="5dbe4-113">Limit Type</span></span> | <span data-ttu-id="5dbe4-114">限制值</span><span class="sxs-lookup"><span data-stu-id="5dbe4-114">Limit Value</span></span> | <span data-ttu-id="5dbe4-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="5dbe4-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="5dbe4-116">**取得** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="5dbe4-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="5dbe4-117">IP</span><span class="sxs-lookup"><span data-stu-id="5dbe4-117">IP</span></span> | <span data-ttu-id="5dbe4-118">1000 / 分鐘</span><span class="sxs-lookup"><span data-stu-id="5dbe4-118">1000 / minute</span></span> | <span data-ttu-id="5dbe4-119">查詢 NuGet 套件中繼資料，透過 v1 OData`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="5dbe4-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="5dbe4-120">**取得** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="5dbe4-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="5dbe4-121">IP</span><span class="sxs-lookup"><span data-stu-id="5dbe4-121">IP</span></span> | <span data-ttu-id="5dbe4-122">3000 / 分鐘</span><span class="sxs-lookup"><span data-stu-id="5dbe4-122">3000 / minute</span></span> | <span data-ttu-id="5dbe4-123">搜尋 NuGet 套件透過 v1 搜尋端點</span><span class="sxs-lookup"><span data-stu-id="5dbe4-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="5dbe4-124">**取得** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="5dbe4-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="5dbe4-125">IP</span><span class="sxs-lookup"><span data-stu-id="5dbe4-125">IP</span></span> | <span data-ttu-id="5dbe4-126">20000 / 分鐘</span><span class="sxs-lookup"><span data-stu-id="5dbe4-126">20000 / minute</span></span> | <span data-ttu-id="5dbe4-127">查詢 NuGet 套件中繼資料，透過 v2 OData`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="5dbe4-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="5dbe4-128">**取得** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="5dbe4-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="5dbe4-129">IP</span><span class="sxs-lookup"><span data-stu-id="5dbe4-129">IP</span></span> | <span data-ttu-id="5dbe4-130">100 / 分鐘</span><span class="sxs-lookup"><span data-stu-id="5dbe4-130">100 / minute</span></span> | <span data-ttu-id="5dbe4-131">查詢透過 v2 OData 的 NuGet 套件數目`Packages`集合</span><span class="sxs-lookup"><span data-stu-id="5dbe4-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="5dbe4-132">封裝將推送，並取消列出</span><span class="sxs-lookup"><span data-stu-id="5dbe4-132">Package Push and Unlist</span></span>

| <span data-ttu-id="5dbe4-133">API</span><span class="sxs-lookup"><span data-stu-id="5dbe4-133">API</span></span> | <span data-ttu-id="5dbe4-134">限制類型</span><span class="sxs-lookup"><span data-stu-id="5dbe4-134">Limit Type</span></span> | <span data-ttu-id="5dbe4-135">限制值</span><span class="sxs-lookup"><span data-stu-id="5dbe4-135">Limit Value</span></span> | <span data-ttu-id="5dbe4-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="5dbe4-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="5dbe4-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="5dbe4-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="5dbe4-138">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="5dbe4-138">API Key</span></span> | <span data-ttu-id="5dbe4-139">250 / 小時</span><span class="sxs-lookup"><span data-stu-id="5dbe4-139">250 / hour</span></span> | <span data-ttu-id="5dbe4-140">上傳新的 NuGet 封裝 （版本） 透過 v2 推播端點</span><span class="sxs-lookup"><span data-stu-id="5dbe4-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="5dbe4-141">**刪除** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="5dbe4-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="5dbe4-142">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="5dbe4-142">API Key</span></span> | <span data-ttu-id="5dbe4-143">250 / 小時</span><span class="sxs-lookup"><span data-stu-id="5dbe4-143">250 / hour</span></span> | <span data-ttu-id="5dbe4-144">取消列出透過 v2 端點的 NuGet 套件 （版本）</span><span class="sxs-lookup"><span data-stu-id="5dbe4-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
