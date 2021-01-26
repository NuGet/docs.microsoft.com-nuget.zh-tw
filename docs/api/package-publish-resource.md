---
title: 推送和刪除，NuGet API
description: 發行服務可讓用戶端發佈新的封裝，以及取消列出或刪除現有的封裝。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773922"
---
# <a name="push-and-delete"></a><span data-ttu-id="236c9-103">推送和刪除</span><span class="sxs-lookup"><span data-stu-id="236c9-103">Push and Delete</span></span>

<span data-ttu-id="236c9-104">您可以根據伺服器的執行) 來推送、刪除 (或取消列出，以及使用 NuGet V3 API 來重新列出封裝。</span><span class="sxs-lookup"><span data-stu-id="236c9-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="236c9-105">這些作業是 `PackagePublish` 以 [服務索引](service-index.md)中找到的資源為基礎。</span><span class="sxs-lookup"><span data-stu-id="236c9-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="236c9-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="236c9-106">Versioning</span></span>

<span data-ttu-id="236c9-107">使用的 `@type` 值如下：</span><span class="sxs-lookup"><span data-stu-id="236c9-107">The following `@type` value is used:</span></span>

<span data-ttu-id="236c9-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="236c9-108">@type value</span></span>          | <span data-ttu-id="236c9-109">備註</span><span class="sxs-lookup"><span data-stu-id="236c9-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="236c9-110">PackagePublish/2.0。0</span><span class="sxs-lookup"><span data-stu-id="236c9-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="236c9-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="236c9-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="236c9-112">基底 URL</span><span class="sxs-lookup"><span data-stu-id="236c9-112">Base URL</span></span>

<span data-ttu-id="236c9-113">下列 Api 的基底 URL 是 `@id` `PackagePublish/2.0.0` 套件來源之 [服務索引](service-index.md)中資源的屬性值。</span><span class="sxs-lookup"><span data-stu-id="236c9-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="236c9-114">針對下列檔，會使用 nuget. org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="236c9-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="236c9-115">請考慮 `https://www.nuget.org/api/v2/package` 作為 `@id` 服務索引中找到之值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="236c9-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="236c9-116">請注意，此 URL 會指向與舊版 V2 推送端點相同的位置，因為通訊協定相同。</span><span class="sxs-lookup"><span data-stu-id="236c9-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="236c9-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="236c9-117">HTTP methods</span></span>

<span data-ttu-id="236c9-118">`PUT` `POST` `DELETE` 此資源支援和 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="236c9-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="236c9-119">針對每個端點支援的方法，請參閱下文。</span><span class="sxs-lookup"><span data-stu-id="236c9-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="236c9-120">推送套件</span><span class="sxs-lookup"><span data-stu-id="236c9-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="236c9-121">nuget.org 具有與推送端點互動的 [其他需求](NuGet-Protocols.md) 。</span><span class="sxs-lookup"><span data-stu-id="236c9-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="236c9-122">nuget.org 支援使用下列 API 來推送新的封裝。</span><span class="sxs-lookup"><span data-stu-id="236c9-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="236c9-123">如果具有所提供識別碼和版本的套件已存在，則 nuget.org 會拒絕推送。</span><span class="sxs-lookup"><span data-stu-id="236c9-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="236c9-124">其他套件來源可能會支援取代現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="236c9-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="236c9-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="236c9-125">Request parameters</span></span>

<span data-ttu-id="236c9-126">名稱</span><span class="sxs-lookup"><span data-stu-id="236c9-126">Name</span></span>           | <span data-ttu-id="236c9-127">位於</span><span class="sxs-lookup"><span data-stu-id="236c9-127">In</span></span>     | <span data-ttu-id="236c9-128">類型</span><span class="sxs-lookup"><span data-stu-id="236c9-128">Type</span></span>   | <span data-ttu-id="236c9-129">必要</span><span class="sxs-lookup"><span data-stu-id="236c9-129">Required</span></span> | <span data-ttu-id="236c9-130">備註</span><span class="sxs-lookup"><span data-stu-id="236c9-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="236c9-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="236c9-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="236c9-132">標頭</span><span class="sxs-lookup"><span data-stu-id="236c9-132">Header</span></span> | <span data-ttu-id="236c9-133">字串</span><span class="sxs-lookup"><span data-stu-id="236c9-133">string</span></span> | <span data-ttu-id="236c9-134">是</span><span class="sxs-lookup"><span data-stu-id="236c9-134">yes</span></span>      | <span data-ttu-id="236c9-135">例如， `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="236c9-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="236c9-136">API 金鑰是由使用者從套件來源取得並設定為用戶端的不透明字串。</span><span class="sxs-lookup"><span data-stu-id="236c9-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="236c9-137">未強制採用任何特定的字串格式，但 API 金鑰的長度不應超過 HTTP 標頭值的合理大小。</span><span class="sxs-lookup"><span data-stu-id="236c9-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="236c9-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="236c9-138">Request body</span></span>

<span data-ttu-id="236c9-139">要求主體的格式必須如下：</span><span class="sxs-lookup"><span data-stu-id="236c9-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="236c9-140">多部分表單資料</span><span class="sxs-lookup"><span data-stu-id="236c9-140">Multipart form data</span></span>

<span data-ttu-id="236c9-141">要求標頭 `Content-Type` 為 `multipart/form-data` ，而且要求主體中的第一個專案是所推送之 nupkg 的原始位元組。</span><span class="sxs-lookup"><span data-stu-id="236c9-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="236c9-142">系統會忽略多部分主體中的後續專案。</span><span class="sxs-lookup"><span data-stu-id="236c9-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="236c9-143">系統會忽略多元件專案的檔案名或其他任何標頭。</span><span class="sxs-lookup"><span data-stu-id="236c9-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="236c9-144">回應</span><span class="sxs-lookup"><span data-stu-id="236c9-144">Response</span></span>

<span data-ttu-id="236c9-145">狀態碼</span><span class="sxs-lookup"><span data-stu-id="236c9-145">Status Code</span></span> | <span data-ttu-id="236c9-146">意義</span><span class="sxs-lookup"><span data-stu-id="236c9-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="236c9-147">201、202</span><span class="sxs-lookup"><span data-stu-id="236c9-147">201, 202</span></span>    | <span data-ttu-id="236c9-148">已成功推送封裝</span><span class="sxs-lookup"><span data-stu-id="236c9-148">The package was successfully pushed</span></span>
<span data-ttu-id="236c9-149">400</span><span class="sxs-lookup"><span data-stu-id="236c9-149">400</span></span>         | <span data-ttu-id="236c9-150">提供的套件無效</span><span class="sxs-lookup"><span data-stu-id="236c9-150">The provided package is invalid</span></span>
<span data-ttu-id="236c9-151">409</span><span class="sxs-lookup"><span data-stu-id="236c9-151">409</span></span>         | <span data-ttu-id="236c9-152">具有所提供識別碼和版本的套件已經存在</span><span class="sxs-lookup"><span data-stu-id="236c9-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="236c9-153">當封裝成功推送時所傳回的成功狀態碼會有不同的伺服器實施。</span><span class="sxs-lookup"><span data-stu-id="236c9-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="236c9-154">刪除套件</span><span class="sxs-lookup"><span data-stu-id="236c9-154">Delete a package</span></span>

<span data-ttu-id="236c9-155">nuget.org 會將套件刪除要求解讀為 "取消列出"。</span><span class="sxs-lookup"><span data-stu-id="236c9-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="236c9-156">這表示套件仍可供封裝的現有取用者使用，但套件不會再出現在搜尋結果或 web 介面中。</span><span class="sxs-lookup"><span data-stu-id="236c9-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="236c9-157">如需這種作法的詳細資訊，請參閱 [已刪除的套件](../nuget-org/policies/deleting-packages.md) 原則。</span><span class="sxs-lookup"><span data-stu-id="236c9-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="236c9-158">其他伺服器的執行可以自由地將此信號解讀為實刪除、虛刪除或取消列出。</span><span class="sxs-lookup"><span data-stu-id="236c9-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="236c9-159">例如 [， (伺服器執行](https://www.nuget.org/packages/NuGet.Server) 只支援舊版 V2 API，) 支援根據設定選項，以取消列出或實刪除的方式處理此要求。</span><span class="sxs-lookup"><span data-stu-id="236c9-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="236c9-160">要求參數</span><span class="sxs-lookup"><span data-stu-id="236c9-160">Request parameters</span></span>

<span data-ttu-id="236c9-161">名稱</span><span class="sxs-lookup"><span data-stu-id="236c9-161">Name</span></span>           | <span data-ttu-id="236c9-162">位於</span><span class="sxs-lookup"><span data-stu-id="236c9-162">In</span></span>     | <span data-ttu-id="236c9-163">類型</span><span class="sxs-lookup"><span data-stu-id="236c9-163">Type</span></span>   | <span data-ttu-id="236c9-164">必要</span><span class="sxs-lookup"><span data-stu-id="236c9-164">Required</span></span> | <span data-ttu-id="236c9-165">備註</span><span class="sxs-lookup"><span data-stu-id="236c9-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="236c9-166">識別碼</span><span class="sxs-lookup"><span data-stu-id="236c9-166">ID</span></span>             | <span data-ttu-id="236c9-167">URL</span><span class="sxs-lookup"><span data-stu-id="236c9-167">URL</span></span>    | <span data-ttu-id="236c9-168">字串</span><span class="sxs-lookup"><span data-stu-id="236c9-168">string</span></span> | <span data-ttu-id="236c9-169">是</span><span class="sxs-lookup"><span data-stu-id="236c9-169">yes</span></span>      | <span data-ttu-id="236c9-170">要刪除的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="236c9-170">The ID of the package to delete</span></span>
<span data-ttu-id="236c9-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="236c9-171">VERSION</span></span>        | <span data-ttu-id="236c9-172">URL</span><span class="sxs-lookup"><span data-stu-id="236c9-172">URL</span></span>    | <span data-ttu-id="236c9-173">字串</span><span class="sxs-lookup"><span data-stu-id="236c9-173">string</span></span> | <span data-ttu-id="236c9-174">是</span><span class="sxs-lookup"><span data-stu-id="236c9-174">yes</span></span>      | <span data-ttu-id="236c9-175">要刪除的套件版本</span><span class="sxs-lookup"><span data-stu-id="236c9-175">The version of the package to delete</span></span>
<span data-ttu-id="236c9-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="236c9-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="236c9-177">標頭</span><span class="sxs-lookup"><span data-stu-id="236c9-177">Header</span></span> | <span data-ttu-id="236c9-178">字串</span><span class="sxs-lookup"><span data-stu-id="236c9-178">string</span></span> | <span data-ttu-id="236c9-179">是</span><span class="sxs-lookup"><span data-stu-id="236c9-179">yes</span></span>      | <span data-ttu-id="236c9-180">例如， `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="236c9-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="236c9-181">回應</span><span class="sxs-lookup"><span data-stu-id="236c9-181">Response</span></span>

<span data-ttu-id="236c9-182">狀態碼</span><span class="sxs-lookup"><span data-stu-id="236c9-182">Status Code</span></span> | <span data-ttu-id="236c9-183">意義</span><span class="sxs-lookup"><span data-stu-id="236c9-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="236c9-184">204</span><span class="sxs-lookup"><span data-stu-id="236c9-184">204</span></span>         | <span data-ttu-id="236c9-185">已刪除封裝</span><span class="sxs-lookup"><span data-stu-id="236c9-185">The package was deleted</span></span>
<span data-ttu-id="236c9-186">404</span><span class="sxs-lookup"><span data-stu-id="236c9-186">404</span></span>         | <span data-ttu-id="236c9-187">沒有具有所提供 `ID` 和 `VERSION` 存在的套件</span><span class="sxs-lookup"><span data-stu-id="236c9-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="236c9-188">重新列出套件</span><span class="sxs-lookup"><span data-stu-id="236c9-188">Relist a package</span></span>

<span data-ttu-id="236c9-189">如果未列出套件，則可以使用 "重新列出" 端點，再次在搜尋結果中顯示該套件。</span><span class="sxs-lookup"><span data-stu-id="236c9-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="236c9-190">此端點與 [delete (取消列出) 端點](#delete-a-package) 具有相同的圖形，但使用的 `POST` 是 HTTP 方法，而不是 `DELETE` 方法。</span><span class="sxs-lookup"><span data-stu-id="236c9-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="236c9-191">如果封裝已列出，要求仍會成功。</span><span class="sxs-lookup"><span data-stu-id="236c9-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="236c9-192">要求參數</span><span class="sxs-lookup"><span data-stu-id="236c9-192">Request parameters</span></span>

<span data-ttu-id="236c9-193">名稱</span><span class="sxs-lookup"><span data-stu-id="236c9-193">Name</span></span>           | <span data-ttu-id="236c9-194">位於</span><span class="sxs-lookup"><span data-stu-id="236c9-194">In</span></span>     | <span data-ttu-id="236c9-195">類型</span><span class="sxs-lookup"><span data-stu-id="236c9-195">Type</span></span>   | <span data-ttu-id="236c9-196">必要</span><span class="sxs-lookup"><span data-stu-id="236c9-196">Required</span></span> | <span data-ttu-id="236c9-197">備註</span><span class="sxs-lookup"><span data-stu-id="236c9-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="236c9-198">識別碼</span><span class="sxs-lookup"><span data-stu-id="236c9-198">ID</span></span>             | <span data-ttu-id="236c9-199">URL</span><span class="sxs-lookup"><span data-stu-id="236c9-199">URL</span></span>    | <span data-ttu-id="236c9-200">字串</span><span class="sxs-lookup"><span data-stu-id="236c9-200">string</span></span> | <span data-ttu-id="236c9-201">是</span><span class="sxs-lookup"><span data-stu-id="236c9-201">yes</span></span>      | <span data-ttu-id="236c9-202">要重新列出的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="236c9-202">The ID of the package to relist</span></span>
<span data-ttu-id="236c9-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="236c9-203">VERSION</span></span>        | <span data-ttu-id="236c9-204">URL</span><span class="sxs-lookup"><span data-stu-id="236c9-204">URL</span></span>    | <span data-ttu-id="236c9-205">字串</span><span class="sxs-lookup"><span data-stu-id="236c9-205">string</span></span> | <span data-ttu-id="236c9-206">是</span><span class="sxs-lookup"><span data-stu-id="236c9-206">yes</span></span>      | <span data-ttu-id="236c9-207">要重新列出的套件版本</span><span class="sxs-lookup"><span data-stu-id="236c9-207">The version of the package to relist</span></span>
<span data-ttu-id="236c9-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="236c9-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="236c9-209">標頭</span><span class="sxs-lookup"><span data-stu-id="236c9-209">Header</span></span> | <span data-ttu-id="236c9-210">字串</span><span class="sxs-lookup"><span data-stu-id="236c9-210">string</span></span> | <span data-ttu-id="236c9-211">是</span><span class="sxs-lookup"><span data-stu-id="236c9-211">yes</span></span>      | <span data-ttu-id="236c9-212">例如， `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="236c9-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="236c9-213">回應</span><span class="sxs-lookup"><span data-stu-id="236c9-213">Response</span></span>

<span data-ttu-id="236c9-214">狀態碼</span><span class="sxs-lookup"><span data-stu-id="236c9-214">Status Code</span></span> | <span data-ttu-id="236c9-215">意義</span><span class="sxs-lookup"><span data-stu-id="236c9-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="236c9-216">200</span><span class="sxs-lookup"><span data-stu-id="236c9-216">200</span></span>         | <span data-ttu-id="236c9-217">現在會列出套件</span><span class="sxs-lookup"><span data-stu-id="236c9-217">The package is now listed</span></span>
<span data-ttu-id="236c9-218">404</span><span class="sxs-lookup"><span data-stu-id="236c9-218">404</span></span>         | <span data-ttu-id="236c9-219">沒有具有所提供 `ID` 和 `VERSION` 存在的套件</span><span class="sxs-lookup"><span data-stu-id="236c9-219">No package with the provided `ID` and `VERSION` exists</span></span>
