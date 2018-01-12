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
ms.openlocfilehash: 5fbcd82b09ebd56ae21103640e7c39b482059525
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="b9fb5-104">發送和刪除</span><span class="sxs-lookup"><span data-stu-id="b9fb5-104">Push and Delete</span></span>

<span data-ttu-id="b9fb5-105">可推入、 刪除 （或 unlist，視伺服器實作而定），和 relist 使用 NuGet V3 API 的封裝。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="b9fb5-106">這些作業會為基礎`PackagePublish`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b9fb5-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="b9fb5-107">Versioning</span></span>

<span data-ttu-id="b9fb5-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="b9fb5-108">The following `@type` value is used:</span></span>

<span data-ttu-id="b9fb5-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="b9fb5-109">@type value</span></span>          | <span data-ttu-id="b9fb5-110">注意</span><span class="sxs-lookup"><span data-stu-id="b9fb5-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="b9fb5-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="b9fb5-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="b9fb5-112">初版</span><span class="sxs-lookup"><span data-stu-id="b9fb5-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="b9fb5-113">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="b9fb5-113">Base URL</span></span>

<span data-ttu-id="b9fb5-114">下列應用程式開發介面的基底 URL 是值`@id`屬性`PackagePublish/2.0.0`封裝來源中的資源[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="b9fb5-115">如下列文件，會使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="b9fb5-116">請考慮`https://www.nuget.org/api/v2/package`做為預留位置`@id`值的索引中找到服務。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="b9fb5-117">請注意，此 URL 指向舊版 V2 推入端點的相同位置因為通訊協定是相同。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b9fb5-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="b9fb5-118">HTTP methods</span></span>

<span data-ttu-id="b9fb5-119">`PUT`，`POST`和`DELETE`這項資源所支援的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="b9fb5-120">針對每個端點都支援的方法，請參閱下文。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="b9fb5-121">推播封裝</span><span class="sxs-lookup"><span data-stu-id="b9fb5-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="b9fb5-122">具有 nuget.org[其他需求](NuGet-Protocols.md)與推入端點互動。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="b9fb5-123">nuget.org 支援使用下列 API 的推送新套件。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="b9fb5-124">如果提供的識別碼和版本的套件已經存在，nuget.org 將會拒絕推送。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="b9fb5-125">其他封裝來源可能會支援取代現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="b9fb5-126">要求參數</span><span class="sxs-lookup"><span data-stu-id="b9fb5-126">Request parameters</span></span>

<span data-ttu-id="b9fb5-127">名稱</span><span class="sxs-lookup"><span data-stu-id="b9fb5-127">Name</span></span>           | <span data-ttu-id="b9fb5-128">In</span><span class="sxs-lookup"><span data-stu-id="b9fb5-128">In</span></span>     | <span data-ttu-id="b9fb5-129">類型</span><span class="sxs-lookup"><span data-stu-id="b9fb5-129">Type</span></span>   | <span data-ttu-id="b9fb5-130">必要</span><span class="sxs-lookup"><span data-stu-id="b9fb5-130">Required</span></span> | <span data-ttu-id="b9fb5-131">注意</span><span class="sxs-lookup"><span data-stu-id="b9fb5-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b9fb5-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b9fb5-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b9fb5-133">頁首</span><span class="sxs-lookup"><span data-stu-id="b9fb5-133">Header</span></span> | <span data-ttu-id="b9fb5-134">字串</span><span class="sxs-lookup"><span data-stu-id="b9fb5-134">string</span></span> | <span data-ttu-id="b9fb5-135">是</span><span class="sxs-lookup"><span data-stu-id="b9fb5-135">yes</span></span>      | <span data-ttu-id="b9fb5-136">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b9fb5-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="b9fb5-137">API 金鑰是不透明的字串從套件來源取得的使用者，並設定在用戶端。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="b9fb5-138">託管沒有特定字串的格式，但 API 金鑰的長度應該超過合理的大小，如 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="b9fb5-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="b9fb5-139">Request body</span></span>

<span data-ttu-id="b9fb5-140">要求主體必須有下列形式：</span><span class="sxs-lookup"><span data-stu-id="b9fb5-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="b9fb5-141">多部分表單資料</span><span class="sxs-lookup"><span data-stu-id="b9fb5-141">Multipart form data</span></span>

<span data-ttu-id="b9fb5-142">要求標頭`Content-Type`是`multipart/form-data`和要求主體中的第一個項目會被按下的.nupkg 未經處理位元組。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="b9fb5-143">在多組件主體中的後續項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="b9fb5-144">檔案名稱或其他任何標頭的多組件的項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="b9fb5-145">回應</span><span class="sxs-lookup"><span data-stu-id="b9fb5-145">Response</span></span>

<span data-ttu-id="b9fb5-146">狀態碼</span><span class="sxs-lookup"><span data-stu-id="b9fb5-146">Status Code</span></span> | <span data-ttu-id="b9fb5-147">意義</span><span class="sxs-lookup"><span data-stu-id="b9fb5-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="b9fb5-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="b9fb5-148">201, 202</span></span>    | <span data-ttu-id="b9fb5-149">封裝已成功推入</span><span class="sxs-lookup"><span data-stu-id="b9fb5-149">The package was successfully pushed</span></span>
<span data-ttu-id="b9fb5-150">400</span><span class="sxs-lookup"><span data-stu-id="b9fb5-150">400</span></span>         | <span data-ttu-id="b9fb5-151">提供的封裝無效</span><span class="sxs-lookup"><span data-stu-id="b9fb5-151">The provided package is invalid</span></span>
<span data-ttu-id="b9fb5-152">409</span><span class="sxs-lookup"><span data-stu-id="b9fb5-152">409</span></span>         | <span data-ttu-id="b9fb5-153">提供的識別碼和版本的封裝已經存在</span><span class="sxs-lookup"><span data-stu-id="b9fb5-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="b9fb5-154">當封裝成功推入時傳回成功狀態碼有所不同伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="b9fb5-155">刪除的封裝</span><span class="sxs-lookup"><span data-stu-id="b9fb5-155">Delete a package</span></span>

<span data-ttu-id="b9fb5-156">nuget.org 會解譯為封裝刪除要求的"unlist"。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="b9fb5-157">這表示封裝仍可供現有消費者的封裝，但封裝不會再出現在搜尋結果中或在 web 介面。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="b9fb5-158">如需此作法的詳細資訊，請參閱[刪除封裝](../policies/deleting-packages.md)原則。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="b9fb5-159">其他伺服器實作會解譯為永久刪除這個信號、 虛刪除，或 unlist 可用。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="b9fb5-160">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （只支援較舊的 V2 API 的伺服器實作） 支援處理此要求為 unlist 或永久刪除，根據組態選項。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="b9fb5-161">要求參數</span><span class="sxs-lookup"><span data-stu-id="b9fb5-161">Request parameters</span></span>

<span data-ttu-id="b9fb5-162">名稱</span><span class="sxs-lookup"><span data-stu-id="b9fb5-162">Name</span></span>           | <span data-ttu-id="b9fb5-163">In</span><span class="sxs-lookup"><span data-stu-id="b9fb5-163">In</span></span>     | <span data-ttu-id="b9fb5-164">類型</span><span class="sxs-lookup"><span data-stu-id="b9fb5-164">Type</span></span>   | <span data-ttu-id="b9fb5-165">必要</span><span class="sxs-lookup"><span data-stu-id="b9fb5-165">Required</span></span> | <span data-ttu-id="b9fb5-166">注意</span><span class="sxs-lookup"><span data-stu-id="b9fb5-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b9fb5-167">識別碼</span><span class="sxs-lookup"><span data-stu-id="b9fb5-167">ID</span></span>             | <span data-ttu-id="b9fb5-168">URL</span><span class="sxs-lookup"><span data-stu-id="b9fb5-168">URL</span></span>    | <span data-ttu-id="b9fb5-169">字串</span><span class="sxs-lookup"><span data-stu-id="b9fb5-169">string</span></span> | <span data-ttu-id="b9fb5-170">是</span><span class="sxs-lookup"><span data-stu-id="b9fb5-170">yes</span></span>      | <span data-ttu-id="b9fb5-171">要刪除的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="b9fb5-171">The ID of the package to delete</span></span>
<span data-ttu-id="b9fb5-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="b9fb5-172">VERSION</span></span>        | <span data-ttu-id="b9fb5-173">URL</span><span class="sxs-lookup"><span data-stu-id="b9fb5-173">URL</span></span>    | <span data-ttu-id="b9fb5-174">字串</span><span class="sxs-lookup"><span data-stu-id="b9fb5-174">string</span></span> | <span data-ttu-id="b9fb5-175">是</span><span class="sxs-lookup"><span data-stu-id="b9fb5-175">yes</span></span>      | <span data-ttu-id="b9fb5-176">若要刪除封裝版本</span><span class="sxs-lookup"><span data-stu-id="b9fb5-176">The version of the package to delete</span></span>
<span data-ttu-id="b9fb5-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b9fb5-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b9fb5-178">頁首</span><span class="sxs-lookup"><span data-stu-id="b9fb5-178">Header</span></span> | <span data-ttu-id="b9fb5-179">字串</span><span class="sxs-lookup"><span data-stu-id="b9fb5-179">string</span></span> | <span data-ttu-id="b9fb5-180">是</span><span class="sxs-lookup"><span data-stu-id="b9fb5-180">yes</span></span>      | <span data-ttu-id="b9fb5-181">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b9fb5-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b9fb5-182">回應</span><span class="sxs-lookup"><span data-stu-id="b9fb5-182">Response</span></span>

<span data-ttu-id="b9fb5-183">狀態碼</span><span class="sxs-lookup"><span data-stu-id="b9fb5-183">Status Code</span></span> | <span data-ttu-id="b9fb5-184">意義</span><span class="sxs-lookup"><span data-stu-id="b9fb5-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="b9fb5-185">204</span><span class="sxs-lookup"><span data-stu-id="b9fb5-185">204</span></span>         | <span data-ttu-id="b9fb5-186">已刪除封裝</span><span class="sxs-lookup"><span data-stu-id="b9fb5-186">The package was deleted</span></span>
<span data-ttu-id="b9fb5-187">404</span><span class="sxs-lookup"><span data-stu-id="b9fb5-187">404</span></span>         | <span data-ttu-id="b9fb5-188">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="b9fb5-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="b9fb5-189">Relist 封裝</span><span class="sxs-lookup"><span data-stu-id="b9fb5-189">Relist a package</span></span>

<span data-ttu-id="b9fb5-190">如果封裝未列出，很可能要在搜尋結果中使用 「 relist 」 端點再次顯示該封裝。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="b9fb5-191">此端點都有相同的圖形做為[刪除 (unlist) 端點](#delete-a-package)但使用`POST`HTTP 方法，而非`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="b9fb5-192">如果已列出封裝，請要求仍然會成功。</span><span class="sxs-lookup"><span data-stu-id="b9fb5-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="b9fb5-193">要求參數</span><span class="sxs-lookup"><span data-stu-id="b9fb5-193">Request parameters</span></span>

<span data-ttu-id="b9fb5-194">名稱</span><span class="sxs-lookup"><span data-stu-id="b9fb5-194">Name</span></span>           | <span data-ttu-id="b9fb5-195">In</span><span class="sxs-lookup"><span data-stu-id="b9fb5-195">In</span></span>     | <span data-ttu-id="b9fb5-196">類型</span><span class="sxs-lookup"><span data-stu-id="b9fb5-196">Type</span></span>   | <span data-ttu-id="b9fb5-197">必要</span><span class="sxs-lookup"><span data-stu-id="b9fb5-197">Required</span></span> | <span data-ttu-id="b9fb5-198">注意</span><span class="sxs-lookup"><span data-stu-id="b9fb5-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b9fb5-199">識別碼</span><span class="sxs-lookup"><span data-stu-id="b9fb5-199">ID</span></span>             | <span data-ttu-id="b9fb5-200">URL</span><span class="sxs-lookup"><span data-stu-id="b9fb5-200">URL</span></span>    | <span data-ttu-id="b9fb5-201">字串</span><span class="sxs-lookup"><span data-stu-id="b9fb5-201">string</span></span> | <span data-ttu-id="b9fb5-202">是</span><span class="sxs-lookup"><span data-stu-id="b9fb5-202">yes</span></span>      | <span data-ttu-id="b9fb5-203">要 relist 封裝的識別碼</span><span class="sxs-lookup"><span data-stu-id="b9fb5-203">The ID of the package to relist</span></span>
<span data-ttu-id="b9fb5-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="b9fb5-204">VERSION</span></span>        | <span data-ttu-id="b9fb5-205">URL</span><span class="sxs-lookup"><span data-stu-id="b9fb5-205">URL</span></span>    | <span data-ttu-id="b9fb5-206">字串</span><span class="sxs-lookup"><span data-stu-id="b9fb5-206">string</span></span> | <span data-ttu-id="b9fb5-207">是</span><span class="sxs-lookup"><span data-stu-id="b9fb5-207">yes</span></span>      | <span data-ttu-id="b9fb5-208">若要 relist 封裝版本</span><span class="sxs-lookup"><span data-stu-id="b9fb5-208">The version of the package to relist</span></span>
<span data-ttu-id="b9fb5-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b9fb5-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b9fb5-210">頁首</span><span class="sxs-lookup"><span data-stu-id="b9fb5-210">Header</span></span> | <span data-ttu-id="b9fb5-211">字串</span><span class="sxs-lookup"><span data-stu-id="b9fb5-211">string</span></span> | <span data-ttu-id="b9fb5-212">是</span><span class="sxs-lookup"><span data-stu-id="b9fb5-212">yes</span></span>      | <span data-ttu-id="b9fb5-213">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b9fb5-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b9fb5-214">回應</span><span class="sxs-lookup"><span data-stu-id="b9fb5-214">Response</span></span>

<span data-ttu-id="b9fb5-215">狀態碼</span><span class="sxs-lookup"><span data-stu-id="b9fb5-215">Status Code</span></span> | <span data-ttu-id="b9fb5-216">意義</span><span class="sxs-lookup"><span data-stu-id="b9fb5-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="b9fb5-217">200</span><span class="sxs-lookup"><span data-stu-id="b9fb5-217">200</span></span>         | <span data-ttu-id="b9fb5-218">現在會列出封裝</span><span class="sxs-lookup"><span data-stu-id="b9fb5-218">The package is now listed</span></span>
<span data-ttu-id="b9fb5-219">404</span><span class="sxs-lookup"><span data-stu-id="b9fb5-219">404</span></span>         | <span data-ttu-id="b9fb5-220">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="b9fb5-220">No package with the provided `ID` and `VERSION` exists</span></span>
