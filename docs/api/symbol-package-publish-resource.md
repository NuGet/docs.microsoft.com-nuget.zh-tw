---
title: 推送符號套件，NuGet API |Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 發行 」 服務可讓用戶端發佈新的符號套件。
keywords: NuGet API 推送符號套件
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580411"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="b835e-104">推送符號套件</span><span class="sxs-lookup"><span data-stu-id="b835e-104">Push Symbol Packages</span></span>

<span data-ttu-id="b835e-105">可將套件推送符號 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="b835e-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="b835e-106">這些作業會為基礎`SymbolPackagePublish`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="b835e-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b835e-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="b835e-107">Versioning</span></span>

<span data-ttu-id="b835e-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="b835e-108">The following `@type` value is used:</span></span>

<span data-ttu-id="b835e-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="b835e-109">@type value</span></span>                 | <span data-ttu-id="b835e-110">注意</span><span class="sxs-lookup"><span data-stu-id="b835e-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="b835e-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="b835e-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="b835e-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="b835e-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="b835e-113">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="b835e-113">Base URL</span></span>

<span data-ttu-id="b835e-114">下列 Api 的基底 URL 是值`@id`的屬性`SymbolPackagePublish/4.9.0`封裝來源中的資源[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="b835e-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="b835e-115">下列文件，會使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="b835e-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="b835e-116">請考慮`https://www.nuget.org/api/v2/symbolpackage`作為預留位置`@id`服務索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="b835e-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b835e-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="b835e-117">HTTP methods</span></span>

<span data-ttu-id="b835e-118">`PUT`這項資源所支援 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="b835e-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="b835e-119">推送符號套件</span><span class="sxs-lookup"><span data-stu-id="b835e-119">Push a symbol package</span></span>

<span data-ttu-id="b835e-120">nuget.org 支援推送新的符號套件格式 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用下列 API。</span><span class="sxs-lookup"><span data-stu-id="b835e-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="b835e-121">具有相同的識別碼和版本的符號套件可以提交多次。</span><span class="sxs-lookup"><span data-stu-id="b835e-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="b835e-122">在下列情況下，將會遭到拒絕符號套件。</span><span class="sxs-lookup"><span data-stu-id="b835e-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="b835e-123">具有相同的識別碼和版本的封裝不存在。</span><span class="sxs-lookup"><span data-stu-id="b835e-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="b835e-124">已推送符號套件具有相同的識別碼和版本，但尚未發行。</span><span class="sxs-lookup"><span data-stu-id="b835e-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="b835e-125">符號套件 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 是無效的 (請參閱[符號套件條件約束](../create-packages/Symbol-Packages-snupkg.md))。</span><span class="sxs-lookup"><span data-stu-id="b835e-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="b835e-126">要求參數</span><span class="sxs-lookup"><span data-stu-id="b835e-126">Request parameters</span></span>

<span data-ttu-id="b835e-127">名稱</span><span class="sxs-lookup"><span data-stu-id="b835e-127">Name</span></span>           | <span data-ttu-id="b835e-128">In</span><span class="sxs-lookup"><span data-stu-id="b835e-128">In</span></span>     | <span data-ttu-id="b835e-129">類型</span><span class="sxs-lookup"><span data-stu-id="b835e-129">Type</span></span>   | <span data-ttu-id="b835e-130">必要</span><span class="sxs-lookup"><span data-stu-id="b835e-130">Required</span></span> | <span data-ttu-id="b835e-131">注意</span><span class="sxs-lookup"><span data-stu-id="b835e-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b835e-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b835e-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b835e-133">頁首</span><span class="sxs-lookup"><span data-stu-id="b835e-133">Header</span></span> | <span data-ttu-id="b835e-134">字串</span><span class="sxs-lookup"><span data-stu-id="b835e-134">string</span></span> | <span data-ttu-id="b835e-135">是</span><span class="sxs-lookup"><span data-stu-id="b835e-135">yes</span></span>      | <span data-ttu-id="b835e-136">例如： `X-NuGet-ApiKey: {USER_API_KEY}` </span><span class="sxs-lookup"><span data-stu-id="b835e-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="b835e-137">API 金鑰是不透明的字串，從套件來源取得的使用者，並在用戶端設定。</span><span class="sxs-lookup"><span data-stu-id="b835e-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="b835e-138">沒有特定字串的格式託管，但 API 金鑰的長度不應超過合理的大小，如 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="b835e-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="b835e-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="b835e-139">Request body</span></span>

<span data-ttu-id="b835e-140">符號發送的要求主體是相同套件的推播要求的要求本文 (請參閱[封裝推送和刪除](package-publish-resource.md))。</span><span class="sxs-lookup"><span data-stu-id="b835e-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="b835e-141">回應</span><span class="sxs-lookup"><span data-stu-id="b835e-141">Response</span></span>

<span data-ttu-id="b835e-142">狀態碼</span><span class="sxs-lookup"><span data-stu-id="b835e-142">Status Code</span></span> | <span data-ttu-id="b835e-143">意義</span><span class="sxs-lookup"><span data-stu-id="b835e-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="b835e-144">201</span><span class="sxs-lookup"><span data-stu-id="b835e-144">201</span></span>         | <span data-ttu-id="b835e-145">已成功推送符號套件。</span><span class="sxs-lookup"><span data-stu-id="b835e-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="b835e-146">400</span><span class="sxs-lookup"><span data-stu-id="b835e-146">400</span></span>         | <span data-ttu-id="b835e-147">提供的符號套件無效。</span><span class="sxs-lookup"><span data-stu-id="b835e-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="b835e-148">401</span><span class="sxs-lookup"><span data-stu-id="b835e-148">401</span></span>         | <span data-ttu-id="b835e-149">使用者未獲授權執行此動作。</span><span class="sxs-lookup"><span data-stu-id="b835e-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="b835e-150">404</span><span class="sxs-lookup"><span data-stu-id="b835e-150">404</span></span>         | <span data-ttu-id="b835e-151">使用提供的識別碼和版本對應的封裝不存在。</span><span class="sxs-lookup"><span data-stu-id="b835e-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="b835e-152">409</span><span class="sxs-lookup"><span data-stu-id="b835e-152">409</span></span>         | <span data-ttu-id="b835e-153">已推送符號套件具有提供的識別碼和版本，但它尚未提供。</span><span class="sxs-lookup"><span data-stu-id="b835e-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="b835e-154">413</span><span class="sxs-lookup"><span data-stu-id="b835e-154">413</span></span>         | <span data-ttu-id="b835e-155">封裝是太大。</span><span class="sxs-lookup"><span data-stu-id="b835e-155">The package is too large.</span></span>

