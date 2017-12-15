---
title: "發送和刪除，NuGet API |Microsoft 文件"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "發行服務可讓用戶端對發佈新的套件和 unlist 或刪除現有的封裝。"
keywords: "NuGet API 發送套件，NuGet API 刪除套件，NuGet API unlist 套件，NuGet API 上傳封裝、 NuGet API 建立封裝"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="cb2fb-104">發送和刪除</span><span class="sxs-lookup"><span data-stu-id="cb2fb-104">Push and Delete</span></span>

<span data-ttu-id="cb2fb-105">可推入，並刪除 （或 unlist，不同的伺服器實作） 使用 NuGet V3 API 的封裝。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="cb2fb-106">這兩項作業會為基礎`PackagePublish`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="cb2fb-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="cb2fb-107">Versioning</span></span>

<span data-ttu-id="cb2fb-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="cb2fb-108">The following `@type` value is used:</span></span>

<span data-ttu-id="cb2fb-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="cb2fb-109">@type value</span></span>          | <span data-ttu-id="cb2fb-110">注意</span><span class="sxs-lookup"><span data-stu-id="cb2fb-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="cb2fb-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="cb2fb-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="cb2fb-112">初版</span><span class="sxs-lookup"><span data-stu-id="cb2fb-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="cb2fb-113">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="cb2fb-113">Base URL</span></span>

<span data-ttu-id="cb2fb-114">下列應用程式開發介面的基底 URL 是值`@id`屬性`PackagePublish/2.0.0`封裝來源中的資源[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="cb2fb-115">如下列文件，會使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="cb2fb-116">請考慮`https://www.nuget.org/api/v2/package`做為預留位置`@id`值的索引中找到服務。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="cb2fb-117">請注意，此 URL 指向舊版 V2 推入端點的相同位置因為通訊協定是相同。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cb2fb-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="cb2fb-118">HTTP methods</span></span>

<span data-ttu-id="cb2fb-119">`PUT`和`DELETE`這項資源所支援的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="cb2fb-120">針對每個端點都支援的方法，請參閱下文。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="cb2fb-121">推播封裝</span><span class="sxs-lookup"><span data-stu-id="cb2fb-121">Push a package</span></span>

<span data-ttu-id="cb2fb-122">nuget.org 支援使用下列 API 的推送新套件。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="cb2fb-123">如果提供的識別碼和版本的套件已經存在，nuget.org 將會拒絕推送。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="cb2fb-124">其他封裝來源可能會支援取代現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="cb2fb-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="cb2fb-125">Request parameters</span></span>

<span data-ttu-id="cb2fb-126">名稱</span><span class="sxs-lookup"><span data-stu-id="cb2fb-126">Name</span></span>           | <span data-ttu-id="cb2fb-127">In</span><span class="sxs-lookup"><span data-stu-id="cb2fb-127">In</span></span>     | <span data-ttu-id="cb2fb-128">類型</span><span class="sxs-lookup"><span data-stu-id="cb2fb-128">Type</span></span>   | <span data-ttu-id="cb2fb-129">必要</span><span class="sxs-lookup"><span data-stu-id="cb2fb-129">Required</span></span> | <span data-ttu-id="cb2fb-130">注意</span><span class="sxs-lookup"><span data-stu-id="cb2fb-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="cb2fb-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="cb2fb-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="cb2fb-132">頁首</span><span class="sxs-lookup"><span data-stu-id="cb2fb-132">Header</span></span> | <span data-ttu-id="cb2fb-133">字串</span><span class="sxs-lookup"><span data-stu-id="cb2fb-133">string</span></span> | <span data-ttu-id="cb2fb-134">是</span><span class="sxs-lookup"><span data-stu-id="cb2fb-134">yes</span></span>      | <span data-ttu-id="cb2fb-135">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="cb2fb-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="cb2fb-136">API 金鑰是不透明的字串從套件來源取得的使用者，並設定在用戶端。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="cb2fb-137">託管沒有特定字串的格式，但 API 金鑰的長度應該超過合理的大小，如 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="cb2fb-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="cb2fb-138">Request body</span></span>

<span data-ttu-id="cb2fb-139">要求主體必須有下列形式：</span><span class="sxs-lookup"><span data-stu-id="cb2fb-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="cb2fb-140">多部分表單資料</span><span class="sxs-lookup"><span data-stu-id="cb2fb-140">Multipart form data</span></span>

<span data-ttu-id="cb2fb-141">要求標頭`Content-Type`是`multipart/form-data`和要求主體中的第一個項目會被按下的.nupkg 未經處理位元組。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="cb2fb-142">在多組件主體中的後續項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="cb2fb-143">檔案名稱或其他任何標頭的多組件的項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="cb2fb-144">回應</span><span class="sxs-lookup"><span data-stu-id="cb2fb-144">Response</span></span>

<span data-ttu-id="cb2fb-145">狀態碼</span><span class="sxs-lookup"><span data-stu-id="cb2fb-145">Status Code</span></span> | <span data-ttu-id="cb2fb-146">意義</span><span class="sxs-lookup"><span data-stu-id="cb2fb-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="cb2fb-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="cb2fb-147">201, 202</span></span>    | <span data-ttu-id="cb2fb-148">封裝已成功推入</span><span class="sxs-lookup"><span data-stu-id="cb2fb-148">The package was successfully pushed</span></span>
<span data-ttu-id="cb2fb-149">400</span><span class="sxs-lookup"><span data-stu-id="cb2fb-149">400</span></span>         | <span data-ttu-id="cb2fb-150">提供的封裝無效</span><span class="sxs-lookup"><span data-stu-id="cb2fb-150">The provided package is invalid</span></span>
<span data-ttu-id="cb2fb-151">409</span><span class="sxs-lookup"><span data-stu-id="cb2fb-151">409</span></span>         | <span data-ttu-id="cb2fb-152">提供的識別碼和版本的封裝已經存在</span><span class="sxs-lookup"><span data-stu-id="cb2fb-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="cb2fb-153">當封裝成功推入時傳回成功狀態碼有所不同伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="cb2fb-154">刪除的封裝</span><span class="sxs-lookup"><span data-stu-id="cb2fb-154">Delete a package</span></span>

<span data-ttu-id="cb2fb-155">nuget.org 會解譯為封裝刪除要求的"unlist"。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="cb2fb-156">這表示封裝仍可供現有消費者的封裝，但封裝不會再出現在搜尋結果中或在 web 介面。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="cb2fb-157">如需此作法的詳細資訊，請參閱[刪除封裝](../policies/deleting-packages.md)原則。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="cb2fb-158">其他伺服器實作會解譯為永久刪除這個信號、 虛刪除，或 unlist 可用。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="cb2fb-159">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （只支援較舊的 V2 API 的伺服器實作） 支援處理此要求為 unlist 或永久刪除，根據組態選項。</span><span class="sxs-lookup"><span data-stu-id="cb2fb-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="cb2fb-160">要求參數</span><span class="sxs-lookup"><span data-stu-id="cb2fb-160">Request parameters</span></span>

<span data-ttu-id="cb2fb-161">名稱</span><span class="sxs-lookup"><span data-stu-id="cb2fb-161">Name</span></span>           | <span data-ttu-id="cb2fb-162">In</span><span class="sxs-lookup"><span data-stu-id="cb2fb-162">In</span></span>     | <span data-ttu-id="cb2fb-163">類型</span><span class="sxs-lookup"><span data-stu-id="cb2fb-163">Type</span></span>   | <span data-ttu-id="cb2fb-164">必要</span><span class="sxs-lookup"><span data-stu-id="cb2fb-164">Required</span></span> | <span data-ttu-id="cb2fb-165">注意</span><span class="sxs-lookup"><span data-stu-id="cb2fb-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="cb2fb-166">ID</span><span class="sxs-lookup"><span data-stu-id="cb2fb-166">ID</span></span>             | <span data-ttu-id="cb2fb-167">URL</span><span class="sxs-lookup"><span data-stu-id="cb2fb-167">URL</span></span>    | <span data-ttu-id="cb2fb-168">字串</span><span class="sxs-lookup"><span data-stu-id="cb2fb-168">string</span></span> | <span data-ttu-id="cb2fb-169">是</span><span class="sxs-lookup"><span data-stu-id="cb2fb-169">yes</span></span>      | <span data-ttu-id="cb2fb-170">要刪除的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="cb2fb-170">The ID of the package to delete</span></span>
<span data-ttu-id="cb2fb-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="cb2fb-171">VERSION</span></span>        | <span data-ttu-id="cb2fb-172">URL</span><span class="sxs-lookup"><span data-stu-id="cb2fb-172">URL</span></span>    | <span data-ttu-id="cb2fb-173">字串</span><span class="sxs-lookup"><span data-stu-id="cb2fb-173">string</span></span> | <span data-ttu-id="cb2fb-174">是</span><span class="sxs-lookup"><span data-stu-id="cb2fb-174">yes</span></span>      | <span data-ttu-id="cb2fb-175">若要刪除封裝版本</span><span class="sxs-lookup"><span data-stu-id="cb2fb-175">The version of the package to delete</span></span>
<span data-ttu-id="cb2fb-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="cb2fb-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="cb2fb-177">頁首</span><span class="sxs-lookup"><span data-stu-id="cb2fb-177">Header</span></span> | <span data-ttu-id="cb2fb-178">字串</span><span class="sxs-lookup"><span data-stu-id="cb2fb-178">string</span></span> | <span data-ttu-id="cb2fb-179">是</span><span class="sxs-lookup"><span data-stu-id="cb2fb-179">yes</span></span>      | <span data-ttu-id="cb2fb-180">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="cb2fb-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="cb2fb-181">回應</span><span class="sxs-lookup"><span data-stu-id="cb2fb-181">Response</span></span>

<span data-ttu-id="cb2fb-182">狀態碼</span><span class="sxs-lookup"><span data-stu-id="cb2fb-182">Status Code</span></span> | <span data-ttu-id="cb2fb-183">意義</span><span class="sxs-lookup"><span data-stu-id="cb2fb-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="cb2fb-184">204</span><span class="sxs-lookup"><span data-stu-id="cb2fb-184">204</span></span>         | <span data-ttu-id="cb2fb-185">已刪除封裝</span><span class="sxs-lookup"><span data-stu-id="cb2fb-185">The package was deleted</span></span>
<span data-ttu-id="cb2fb-186">404</span><span class="sxs-lookup"><span data-stu-id="cb2fb-186">404</span></span>         | <span data-ttu-id="cb2fb-187">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="cb2fb-187">No package with the provided `ID` and `VERSION` exists</span></span>
