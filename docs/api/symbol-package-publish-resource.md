---
title: 推送符號套件，NuGet API |Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 發行服務可讓用戶端發佈新的符號套件。
keywords: NuGet API 推送符號套件
ms.reviewer: karann
ms.openlocfilehash: bd4a10cc976c9d0775a63cfe61c35327c196065c
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738873"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="bd823-104">推送符號套件</span><span class="sxs-lookup"><span data-stu-id="bd823-104">Push Symbol Packages</span></span>

<span data-ttu-id="bd823-105">您可以使用 NuGet V3 API 將符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 推送。</span><span class="sxs-lookup"><span data-stu-id="bd823-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="bd823-106">這些作業是 `SymbolPackagePublish` 以 [服務索引](service-index.md)中找到的資源為基礎。</span><span class="sxs-lookup"><span data-stu-id="bd823-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="bd823-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="bd823-107">Versioning</span></span>

<span data-ttu-id="bd823-108">使用的 `@type` 值如下：</span><span class="sxs-lookup"><span data-stu-id="bd823-108">The following `@type` value is used:</span></span>

<span data-ttu-id="bd823-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="bd823-109">@type value</span></span>                 | <span data-ttu-id="bd823-110">備註</span><span class="sxs-lookup"><span data-stu-id="bd823-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="bd823-111">SymbolPackagePublish/4.9。0</span><span class="sxs-lookup"><span data-stu-id="bd823-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="bd823-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="bd823-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="bd823-113">基底 URL</span><span class="sxs-lookup"><span data-stu-id="bd823-113">Base URL</span></span>

<span data-ttu-id="bd823-114">下列 Api 的基底 URL 是 `@id` `SymbolPackagePublish/4.9.0` 套件來源之 [服務索引](service-index.md)中資源的屬性值。</span><span class="sxs-lookup"><span data-stu-id="bd823-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="bd823-115">針對下列檔，會使用 nuget. org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="bd823-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="bd823-116">請考慮 `https://www.nuget.org/api/v2/symbolpackage` 作為 `@id` 服務索引中找到之值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="bd823-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="bd823-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="bd823-117">HTTP methods</span></span>

<span data-ttu-id="bd823-118">`PUT`此資源支援 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="bd823-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="bd823-119">推送符號套件</span><span class="sxs-lookup"><span data-stu-id="bd823-119">Push a symbol package</span></span>

<span data-ttu-id="bd823-120">nuget.org 支援使用下列 API 來推送新的符號套件格式 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 。</span><span class="sxs-lookup"><span data-stu-id="bd823-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="bd823-121">具有相同識別碼和版本的符號套件可以提交多次。</span><span class="sxs-lookup"><span data-stu-id="bd823-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="bd823-122">在下列情況下，將會拒絕符號套件。</span><span class="sxs-lookup"><span data-stu-id="bd823-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="bd823-123">具有相同識別碼和版本的套件不存在。</span><span class="sxs-lookup"><span data-stu-id="bd823-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="bd823-124">已推送具有相同識別碼和版本的符號套件，但尚未發佈。</span><span class="sxs-lookup"><span data-stu-id="bd823-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="bd823-125">符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 無效 (請參閱 [符號封裝條件約束](../create-packages/Symbol-Packages-snupkg.md)) 。</span><span class="sxs-lookup"><span data-stu-id="bd823-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="bd823-126">要求參數</span><span class="sxs-lookup"><span data-stu-id="bd823-126">Request parameters</span></span>

<span data-ttu-id="bd823-127">名稱</span><span class="sxs-lookup"><span data-stu-id="bd823-127">Name</span></span>           | <span data-ttu-id="bd823-128">位於</span><span class="sxs-lookup"><span data-stu-id="bd823-128">In</span></span>     | <span data-ttu-id="bd823-129">類型</span><span class="sxs-lookup"><span data-stu-id="bd823-129">Type</span></span>   | <span data-ttu-id="bd823-130">必要</span><span class="sxs-lookup"><span data-stu-id="bd823-130">Required</span></span> | <span data-ttu-id="bd823-131">備註</span><span class="sxs-lookup"><span data-stu-id="bd823-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="bd823-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="bd823-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="bd823-133">標頭</span><span class="sxs-lookup"><span data-stu-id="bd823-133">Header</span></span> | <span data-ttu-id="bd823-134">字串</span><span class="sxs-lookup"><span data-stu-id="bd823-134">string</span></span> | <span data-ttu-id="bd823-135">是</span><span class="sxs-lookup"><span data-stu-id="bd823-135">yes</span></span>      | <span data-ttu-id="bd823-136">例如， `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="bd823-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="bd823-137">API 金鑰是由使用者從套件來源取得並設定為用戶端的不透明字串。</span><span class="sxs-lookup"><span data-stu-id="bd823-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="bd823-138">未強制採用任何特定的字串格式，但 API 金鑰的長度不應超過 HTTP 標頭值的合理大小。</span><span class="sxs-lookup"><span data-stu-id="bd823-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="bd823-139">Request body</span><span class="sxs-lookup"><span data-stu-id="bd823-139">Request body</span></span>

<span data-ttu-id="bd823-140">符號推送的要求主體與封裝推送要求的要求主體相同 (請參閱 [封裝推送和刪除](package-publish-resource.md)) 。</span><span class="sxs-lookup"><span data-stu-id="bd823-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="bd823-141">回應</span><span class="sxs-lookup"><span data-stu-id="bd823-141">Response</span></span>

<span data-ttu-id="bd823-142">狀態碼</span><span class="sxs-lookup"><span data-stu-id="bd823-142">Status Code</span></span> | <span data-ttu-id="bd823-143">意義</span><span class="sxs-lookup"><span data-stu-id="bd823-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="bd823-144">201</span><span class="sxs-lookup"><span data-stu-id="bd823-144">201</span></span>         | <span data-ttu-id="bd823-145">已成功推送符號套件。</span><span class="sxs-lookup"><span data-stu-id="bd823-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="bd823-146">400</span><span class="sxs-lookup"><span data-stu-id="bd823-146">400</span></span>         | <span data-ttu-id="bd823-147">提供的符號套件無效。</span><span class="sxs-lookup"><span data-stu-id="bd823-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="bd823-148">401</span><span class="sxs-lookup"><span data-stu-id="bd823-148">401</span></span>         | <span data-ttu-id="bd823-149">使用者未獲授權執行此動作。</span><span class="sxs-lookup"><span data-stu-id="bd823-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="bd823-150">404</span><span class="sxs-lookup"><span data-stu-id="bd823-150">404</span></span>         | <span data-ttu-id="bd823-151">具有所提供識別碼和版本的對應套件不存在。</span><span class="sxs-lookup"><span data-stu-id="bd823-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="bd823-152">409</span><span class="sxs-lookup"><span data-stu-id="bd823-152">409</span></span>         | <span data-ttu-id="bd823-153">已推送具有所提供識別碼和版本的符號套件，但尚未提供。</span><span class="sxs-lookup"><span data-stu-id="bd823-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="bd823-154">413</span><span class="sxs-lookup"><span data-stu-id="bd823-154">413</span></span>         | <span data-ttu-id="bd823-155">封裝太大。</span><span class="sxs-lookup"><span data-stu-id="bd823-155">The package is too large.</span></span>

