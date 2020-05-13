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
# <a name="rate-limits"></a><span data-ttu-id="157da-103">速率限制</span><span class="sxs-lookup"><span data-stu-id="157da-103">Rate Limits</span></span>

<span data-ttu-id="157da-104">NuGet.org API 會強制執行速率限制，以防止濫用。</span><span class="sxs-lookup"><span data-stu-id="157da-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="157da-105">超過速率限制的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="157da-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="157da-106">除了使用速率限制的要求節流以外，某些 Api 也會強制執行配額。</span><span class="sxs-lookup"><span data-stu-id="157da-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="157da-107">超過配額的要求會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="157da-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="157da-108">下表列出 NuGet.org API 的速率限制。</span><span class="sxs-lookup"><span data-stu-id="157da-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="157da-109">封裝搜尋</span><span class="sxs-lookup"><span data-stu-id="157da-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="157da-110">我們建議使用 NuGet. 組織的[V3 搜尋 api](search-query-service-resource.md) ，因為它目前不受速率限制。</span><span class="sxs-lookup"><span data-stu-id="157da-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="157da-111">針對 V1 和 V2 搜尋 Api，適用下列限制：</span><span class="sxs-lookup"><span data-stu-id="157da-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="157da-112">API</span><span class="sxs-lookup"><span data-stu-id="157da-112">API</span></span> | <span data-ttu-id="157da-113">限制類型</span><span class="sxs-lookup"><span data-stu-id="157da-113">Limit Type</span></span> | <span data-ttu-id="157da-114">限制值</span><span class="sxs-lookup"><span data-stu-id="157da-114">Limit Value</span></span> | <span data-ttu-id="157da-115">API 使用案例</span><span class="sxs-lookup"><span data-stu-id="157da-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="157da-116">**取得**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="157da-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="157da-117">IP</span><span class="sxs-lookup"><span data-stu-id="157da-117">IP</span></span> | <span data-ttu-id="157da-118">1000/分鐘</span><span class="sxs-lookup"><span data-stu-id="157da-118">1000 / minute</span></span> | <span data-ttu-id="157da-119">透過 v1 OData 收集來查詢 NuGet 套件中繼資料 `Packages`</span><span class="sxs-lookup"><span data-stu-id="157da-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="157da-120">**取得**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="157da-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="157da-121">IP</span><span class="sxs-lookup"><span data-stu-id="157da-121">IP</span></span> | <span data-ttu-id="157da-122">3000/分鐘</span><span class="sxs-lookup"><span data-stu-id="157da-122">3000 / minute</span></span> | <span data-ttu-id="157da-123">透過 v1 搜尋端點搜尋 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="157da-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="157da-124">**取得**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="157da-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="157da-125">IP</span><span class="sxs-lookup"><span data-stu-id="157da-125">IP</span></span> | <span data-ttu-id="157da-126">20000/分鐘</span><span class="sxs-lookup"><span data-stu-id="157da-126">20000 / minute</span></span> | <span data-ttu-id="157da-127">透過 v2 OData 集合查詢 NuGet 套件中繼資料 `Packages`</span><span class="sxs-lookup"><span data-stu-id="157da-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="157da-128">**取得**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="157da-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="157da-129">IP</span><span class="sxs-lookup"><span data-stu-id="157da-129">IP</span></span> | <span data-ttu-id="157da-130">100/分鐘</span><span class="sxs-lookup"><span data-stu-id="157da-130">100 / minute</span></span> | <span data-ttu-id="157da-131">透過 v2 OData 集合查詢 NuGet 封裝計數 `Packages`</span><span class="sxs-lookup"><span data-stu-id="157da-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="157da-132">封裝推送和取消列出</span><span class="sxs-lookup"><span data-stu-id="157da-132">Package Push and Unlist</span></span>

| <span data-ttu-id="157da-133">API</span><span class="sxs-lookup"><span data-stu-id="157da-133">API</span></span> | <span data-ttu-id="157da-134">限制類型</span><span class="sxs-lookup"><span data-stu-id="157da-134">Limit Type</span></span> | <span data-ttu-id="157da-135">限制值</span><span class="sxs-lookup"><span data-stu-id="157da-135">Limit Value</span></span> | <span data-ttu-id="157da-136">API 使用案例</span><span class="sxs-lookup"><span data-stu-id="157da-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="157da-137">**PUT**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="157da-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="157da-138">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="157da-138">API Key</span></span> | <span data-ttu-id="157da-139">350/小時</span><span class="sxs-lookup"><span data-stu-id="157da-139">350 / hour</span></span> | <span data-ttu-id="157da-140">透過 v2 推播端點上傳新的 NuGet 套件（版本）</span><span class="sxs-lookup"><span data-stu-id="157da-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="157da-141">**刪除**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="157da-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="157da-142">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="157da-142">API Key</span></span> | <span data-ttu-id="157da-143">250/小時</span><span class="sxs-lookup"><span data-stu-id="157da-143">250 / hour</span></span> | <span data-ttu-id="157da-144">透過 v2 端點取消列出 NuGet 套件（版本）</span><span class="sxs-lookup"><span data-stu-id="157da-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="157da-145">nuget.org 網站頁面流覽</span><span class="sxs-lookup"><span data-stu-id="157da-145">nuget.org website page views</span></span>

<span data-ttu-id="157da-146">如果您以程式設計方式存取 nuget.org 網頁，請考慮調查我們記載的[V3 api](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="157da-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="157da-147">這些端點可讓您更輕鬆地存取套件中繼資料和內容。</span><span class="sxs-lookup"><span data-stu-id="157da-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="157da-148">V3 API 具有更高的可用性，且效能高於存取 NuGet 資源庫網頁（專為網頁瀏覽器互動而設計）。</span><span class="sxs-lookup"><span data-stu-id="157da-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="157da-149">API</span><span class="sxs-lookup"><span data-stu-id="157da-149">API</span></span> | <span data-ttu-id="157da-150">限制類型</span><span class="sxs-lookup"><span data-stu-id="157da-150">Limit Type</span></span> | <span data-ttu-id="157da-151">限制值</span><span class="sxs-lookup"><span data-stu-id="157da-151">Limit Value</span></span> | <span data-ttu-id="157da-152">API 使用案例</span><span class="sxs-lookup"><span data-stu-id="157da-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="157da-153">**取得**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="157da-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="157da-154">IP</span><span class="sxs-lookup"><span data-stu-id="157da-154">IP</span></span> | <span data-ttu-id="157da-155">50/分鐘</span><span class="sxs-lookup"><span data-stu-id="157da-155">50 / minute</span></span> | <span data-ttu-id="157da-156">顯示套件（版本）詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="157da-156">Display package (version) details page.</span></span> 
