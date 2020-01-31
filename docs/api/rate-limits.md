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
# <a name="rate-limits"></a><span data-ttu-id="784f0-103">速率限制</span><span class="sxs-lookup"><span data-stu-id="784f0-103">Rate Limits</span></span>

<span data-ttu-id="784f0-104">NuGet.org API 會強制執行速率限制，以防止濫用。</span><span class="sxs-lookup"><span data-stu-id="784f0-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="784f0-105">超過速率限制的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="784f0-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="784f0-106">除了使用速率限制的要求節流以外，某些 Api 也會強制執行配額。</span><span class="sxs-lookup"><span data-stu-id="784f0-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="784f0-107">超過配額的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="784f0-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="784f0-108">下表列出 NuGet.org API 的速率限制。</span><span class="sxs-lookup"><span data-stu-id="784f0-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="784f0-109">封裝搜尋</span><span class="sxs-lookup"><span data-stu-id="784f0-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="784f0-110">我們建議使用 NuGet. 組織的[V3 搜尋 api](search-query-service-resource.md) ，因為它目前不受速率限制。</span><span class="sxs-lookup"><span data-stu-id="784f0-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="784f0-111">針對 V1 和 V2 搜尋 Api，適用下列限制：</span><span class="sxs-lookup"><span data-stu-id="784f0-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="784f0-112">API</span><span class="sxs-lookup"><span data-stu-id="784f0-112">API</span></span> | <span data-ttu-id="784f0-113">限制類型</span><span class="sxs-lookup"><span data-stu-id="784f0-113">Limit Type</span></span> | <span data-ttu-id="784f0-114">限制值</span><span class="sxs-lookup"><span data-stu-id="784f0-114">Limit Value</span></span> | <span data-ttu-id="784f0-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="784f0-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="784f0-116">**取得**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="784f0-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="784f0-117">IP</span><span class="sxs-lookup"><span data-stu-id="784f0-117">IP</span></span> | <span data-ttu-id="784f0-118">1000/分鐘</span><span class="sxs-lookup"><span data-stu-id="784f0-118">1000 / minute</span></span> | <span data-ttu-id="784f0-119">透過 v1 OData `Packages` 收集來查詢 NuGet 套件中繼資料</span><span class="sxs-lookup"><span data-stu-id="784f0-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="784f0-120">**取得**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="784f0-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="784f0-121">IP</span><span class="sxs-lookup"><span data-stu-id="784f0-121">IP</span></span> | <span data-ttu-id="784f0-122">3000/分鐘</span><span class="sxs-lookup"><span data-stu-id="784f0-122">3000 / minute</span></span> | <span data-ttu-id="784f0-123">透過 v1 搜尋端點搜尋 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="784f0-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="784f0-124">**取得**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="784f0-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="784f0-125">IP</span><span class="sxs-lookup"><span data-stu-id="784f0-125">IP</span></span> | <span data-ttu-id="784f0-126">20000/分鐘</span><span class="sxs-lookup"><span data-stu-id="784f0-126">20000 / minute</span></span> | <span data-ttu-id="784f0-127">透過 v2 OData `Packages` 收集來查詢 NuGet 套件中繼資料</span><span class="sxs-lookup"><span data-stu-id="784f0-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="784f0-128">**取得**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="784f0-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="784f0-129">IP</span><span class="sxs-lookup"><span data-stu-id="784f0-129">IP</span></span> | <span data-ttu-id="784f0-130">100/分鐘</span><span class="sxs-lookup"><span data-stu-id="784f0-130">100 / minute</span></span> | <span data-ttu-id="784f0-131">透過 v2 OData `Packages` 收集來查詢 NuGet 封裝計數</span><span class="sxs-lookup"><span data-stu-id="784f0-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="784f0-132">封裝推送和取消列出</span><span class="sxs-lookup"><span data-stu-id="784f0-132">Package Push and Unlist</span></span>

| <span data-ttu-id="784f0-133">API</span><span class="sxs-lookup"><span data-stu-id="784f0-133">API</span></span> | <span data-ttu-id="784f0-134">限制類型</span><span class="sxs-lookup"><span data-stu-id="784f0-134">Limit Type</span></span> | <span data-ttu-id="784f0-135">限制值</span><span class="sxs-lookup"><span data-stu-id="784f0-135">Limit Value</span></span> | <span data-ttu-id="784f0-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="784f0-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="784f0-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="784f0-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="784f0-138">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="784f0-138">API Key</span></span> | <span data-ttu-id="784f0-139">350/小時</span><span class="sxs-lookup"><span data-stu-id="784f0-139">350 / hour</span></span> | <span data-ttu-id="784f0-140">透過 v2 推播端點上傳新的 NuGet 套件（版本）</span><span class="sxs-lookup"><span data-stu-id="784f0-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="784f0-141">**刪除**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="784f0-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="784f0-142">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="784f0-142">API Key</span></span> | <span data-ttu-id="784f0-143">250/小時</span><span class="sxs-lookup"><span data-stu-id="784f0-143">250 / hour</span></span> | <span data-ttu-id="784f0-144">透過 v2 端點取消列出 NuGet 套件（版本）</span><span class="sxs-lookup"><span data-stu-id="784f0-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
