---
title: 推送符號套件, NuGet API |Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 發行服務可讓用戶端發佈新的符號套件。
keywords: NuGet API 推送符號套件
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235102"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="2dbb7-104">推送符號套件</span><span class="sxs-lookup"><span data-stu-id="2dbb7-104">Push Symbol Packages</span></span>

<span data-ttu-id="2dbb7-105">您可以使用 NuGet V3 API 推送符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md))。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="2dbb7-106">這些作業是以[服務索引](service-index.md)中`SymbolPackagePublish`找到的資源為基礎。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2dbb7-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="2dbb7-107">Versioning</span></span>

<span data-ttu-id="2dbb7-108">會使用`@type`下列值:</span><span class="sxs-lookup"><span data-stu-id="2dbb7-108">The following `@type` value is used:</span></span>

<span data-ttu-id="2dbb7-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="2dbb7-109">@type value</span></span>                 | <span data-ttu-id="2dbb7-110">注意</span><span class="sxs-lookup"><span data-stu-id="2dbb7-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="2dbb7-111">SymbolPackagePublish/4.9。0</span><span class="sxs-lookup"><span data-stu-id="2dbb7-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="2dbb7-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="2dbb7-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2dbb7-113">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="2dbb7-113">Base URL</span></span>

<span data-ttu-id="2dbb7-114">下列 api 的基底 URL 是封裝來源之`@id` [服務索引](service-index.md)中`SymbolPackagePublish/4.9.0`資源的屬性值。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="2dbb7-115">下列檔中會使用 nuget. org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="2dbb7-116">請`https://www.nuget.org/api/v2/symbolpackage`考慮當做服務索引中`@id`找到之值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2dbb7-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2dbb7-117">HTTP methods</span></span>

<span data-ttu-id="2dbb7-118">此資源支援 HTTP 方法。 `PUT`</span><span class="sxs-lookup"><span data-stu-id="2dbb7-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="2dbb7-119">推送符號套件</span><span class="sxs-lookup"><span data-stu-id="2dbb7-119">Push a symbol package</span></span>

<span data-ttu-id="2dbb7-120">nuget.org 支援使用下列 API 來推送新的符號套件格式 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md))。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="2dbb7-121">具有相同識別碼和版本的符號套件可以多次提交。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="2dbb7-122">在下列情況下, 將會拒絕符號套件。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="2dbb7-123">具有相同識別碼和版本的封裝不存在。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="2dbb7-124">已推送具有相同識別碼和版本的符號套件, 但尚未發行。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="2dbb7-125">符號套件 ([.snupkg](../create-packages/Symbol-Packages-snupkg.md)) 無效 (請參閱[符號封裝條件約束](../create-packages/Symbol-Packages-snupkg.md))。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="2dbb7-126">要求參數</span><span class="sxs-lookup"><span data-stu-id="2dbb7-126">Request parameters</span></span>

<span data-ttu-id="2dbb7-127">名稱</span><span class="sxs-lookup"><span data-stu-id="2dbb7-127">Name</span></span>           | <span data-ttu-id="2dbb7-128">In</span><span class="sxs-lookup"><span data-stu-id="2dbb7-128">In</span></span>     | <span data-ttu-id="2dbb7-129">類型</span><span class="sxs-lookup"><span data-stu-id="2dbb7-129">Type</span></span>   | <span data-ttu-id="2dbb7-130">必要</span><span class="sxs-lookup"><span data-stu-id="2dbb7-130">Required</span></span> | <span data-ttu-id="2dbb7-131">注意</span><span class="sxs-lookup"><span data-stu-id="2dbb7-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2dbb7-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2dbb7-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2dbb7-133">標頭</span><span class="sxs-lookup"><span data-stu-id="2dbb7-133">Header</span></span> | <span data-ttu-id="2dbb7-134">字串</span><span class="sxs-lookup"><span data-stu-id="2dbb7-134">string</span></span> | <span data-ttu-id="2dbb7-135">是</span><span class="sxs-lookup"><span data-stu-id="2dbb7-135">yes</span></span>      | <span data-ttu-id="2dbb7-136">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2dbb7-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="2dbb7-137">API 金鑰是由使用者從封裝來源取得的不透明字串, 並設定在用戶端中。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="2dbb7-138">不會強制使用特定的字串格式, 但 API 金鑰的長度不應該超過 HTTP 標頭值的合理大小。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="2dbb7-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="2dbb7-139">Request body</span></span>

<span data-ttu-id="2dbb7-140">符號推送的要求本文與套件推播要求的要求本文相同 (請參閱[封裝推送和刪除](package-publish-resource.md))。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="2dbb7-141">回應</span><span class="sxs-lookup"><span data-stu-id="2dbb7-141">Response</span></span>

<span data-ttu-id="2dbb7-142">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2dbb7-142">Status Code</span></span> | <span data-ttu-id="2dbb7-143">意義</span><span class="sxs-lookup"><span data-stu-id="2dbb7-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="2dbb7-144">201</span><span class="sxs-lookup"><span data-stu-id="2dbb7-144">201</span></span>         | <span data-ttu-id="2dbb7-145">已成功推送符號套件。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="2dbb7-146">400</span><span class="sxs-lookup"><span data-stu-id="2dbb7-146">400</span></span>         | <span data-ttu-id="2dbb7-147">提供的符號套件無效。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="2dbb7-148">401</span><span class="sxs-lookup"><span data-stu-id="2dbb7-148">401</span></span>         | <span data-ttu-id="2dbb7-149">使用者未獲授權, 無法執行此動作。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="2dbb7-150">404</span><span class="sxs-lookup"><span data-stu-id="2dbb7-150">404</span></span>         | <span data-ttu-id="2dbb7-151">具有所提供識別碼和版本的對應封裝不存在。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="2dbb7-152">409</span><span class="sxs-lookup"><span data-stu-id="2dbb7-152">409</span></span>         | <span data-ttu-id="2dbb7-153">已推送具有所提供識別碼和版本的符號套件, 但尚未提供。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="2dbb7-154">413</span><span class="sxs-lookup"><span data-stu-id="2dbb7-154">413</span></span>         | <span data-ttu-id="2dbb7-155">封裝太大。</span><span class="sxs-lookup"><span data-stu-id="2dbb7-155">The package is too large.</span></span>

