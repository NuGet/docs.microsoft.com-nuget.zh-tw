---
title: 發送和刪除，NuGet API
description: 發行服務可讓用戶端對發佈新的套件和 unlist 或刪除現有的封裝。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="d9d93-103">發送和刪除</span><span class="sxs-lookup"><span data-stu-id="d9d93-103">Push and Delete</span></span>

<span data-ttu-id="d9d93-104">可推入、 刪除 （或 unlist，視伺服器實作而定），和 relist 使用 NuGet V3 API 的封裝。</span><span class="sxs-lookup"><span data-stu-id="d9d93-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="d9d93-105">這些作業會為基礎`PackagePublish`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d93-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d9d93-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="d9d93-106">Versioning</span></span>

<span data-ttu-id="d9d93-107">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="d9d93-107">The following `@type` value is used:</span></span>

<span data-ttu-id="d9d93-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="d9d93-108">@type value</span></span>          | <span data-ttu-id="d9d93-109">注意</span><span class="sxs-lookup"><span data-stu-id="d9d93-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="d9d93-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9d93-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="d9d93-111">初版</span><span class="sxs-lookup"><span data-stu-id="d9d93-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d9d93-112">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="d9d93-112">Base URL</span></span>

<span data-ttu-id="d9d93-113">下列應用程式開發介面的基底 URL 是值`@id`屬性`PackagePublish/2.0.0`封裝來源中的資源[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d93-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="d9d93-114">如下列文件，會使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="d9d93-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="d9d93-115">請考慮`https://www.nuget.org/api/v2/package`做為預留位置`@id`值的索引中找到服務。</span><span class="sxs-lookup"><span data-stu-id="d9d93-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="d9d93-116">請注意，此 URL 指向舊版 V2 推入端點的相同位置因為通訊協定是相同。</span><span class="sxs-lookup"><span data-stu-id="d9d93-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d9d93-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="d9d93-117">HTTP methods</span></span>

<span data-ttu-id="d9d93-118">`PUT`，`POST`和`DELETE`這項資源所支援的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="d9d93-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="d9d93-119">針對每個端點都支援的方法，請參閱下文。</span><span class="sxs-lookup"><span data-stu-id="d9d93-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="d9d93-120">推播封裝</span><span class="sxs-lookup"><span data-stu-id="d9d93-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="d9d93-121">具有 nuget.org[其他需求](NuGet-Protocols.md)與推入端點互動。</span><span class="sxs-lookup"><span data-stu-id="d9d93-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="d9d93-122">nuget.org 支援使用下列 API 的推送新套件。</span><span class="sxs-lookup"><span data-stu-id="d9d93-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="d9d93-123">如果提供的識別碼和版本的套件已經存在，nuget.org 將會拒絕推送。</span><span class="sxs-lookup"><span data-stu-id="d9d93-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="d9d93-124">其他封裝來源可能會支援取代現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="d9d93-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="d9d93-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="d9d93-125">Request parameters</span></span>

<span data-ttu-id="d9d93-126">名稱</span><span class="sxs-lookup"><span data-stu-id="d9d93-126">Name</span></span>           | <span data-ttu-id="d9d93-127">In</span><span class="sxs-lookup"><span data-stu-id="d9d93-127">In</span></span>     | <span data-ttu-id="d9d93-128">類型</span><span class="sxs-lookup"><span data-stu-id="d9d93-128">Type</span></span>   | <span data-ttu-id="d9d93-129">必要</span><span class="sxs-lookup"><span data-stu-id="d9d93-129">Required</span></span> | <span data-ttu-id="d9d93-130">注意</span><span class="sxs-lookup"><span data-stu-id="d9d93-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d9d93-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d9d93-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d9d93-132">頁首</span><span class="sxs-lookup"><span data-stu-id="d9d93-132">Header</span></span> | <span data-ttu-id="d9d93-133">字串</span><span class="sxs-lookup"><span data-stu-id="d9d93-133">string</span></span> | <span data-ttu-id="d9d93-134">是</span><span class="sxs-lookup"><span data-stu-id="d9d93-134">yes</span></span>      | <span data-ttu-id="d9d93-135">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="d9d93-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="d9d93-136">API 金鑰是不透明的字串從套件來源取得的使用者，並設定在用戶端。</span><span class="sxs-lookup"><span data-stu-id="d9d93-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="d9d93-137">託管沒有特定字串的格式，但 API 金鑰的長度應該超過合理的大小，如 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="d9d93-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="d9d93-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="d9d93-138">Request body</span></span>

<span data-ttu-id="d9d93-139">要求主體必須有下列形式：</span><span class="sxs-lookup"><span data-stu-id="d9d93-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="d9d93-140">多部分表單資料</span><span class="sxs-lookup"><span data-stu-id="d9d93-140">Multipart form data</span></span>

<span data-ttu-id="d9d93-141">要求標頭`Content-Type`是`multipart/form-data`和要求主體中的第一個項目會被按下的.nupkg 未經處理位元組。</span><span class="sxs-lookup"><span data-stu-id="d9d93-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="d9d93-142">在多組件主體中的後續項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="d9d93-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="d9d93-143">檔案名稱或其他任何標頭的多組件的項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="d9d93-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="d9d93-144">回應</span><span class="sxs-lookup"><span data-stu-id="d9d93-144">Response</span></span>

<span data-ttu-id="d9d93-145">狀態碼</span><span class="sxs-lookup"><span data-stu-id="d9d93-145">Status Code</span></span> | <span data-ttu-id="d9d93-146">意義</span><span class="sxs-lookup"><span data-stu-id="d9d93-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="d9d93-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="d9d93-147">201, 202</span></span>    | <span data-ttu-id="d9d93-148">封裝已成功推入</span><span class="sxs-lookup"><span data-stu-id="d9d93-148">The package was successfully pushed</span></span>
<span data-ttu-id="d9d93-149">400</span><span class="sxs-lookup"><span data-stu-id="d9d93-149">400</span></span>         | <span data-ttu-id="d9d93-150">提供的封裝無效</span><span class="sxs-lookup"><span data-stu-id="d9d93-150">The provided package is invalid</span></span>
<span data-ttu-id="d9d93-151">409</span><span class="sxs-lookup"><span data-stu-id="d9d93-151">409</span></span>         | <span data-ttu-id="d9d93-152">提供的識別碼和版本的封裝已經存在</span><span class="sxs-lookup"><span data-stu-id="d9d93-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="d9d93-153">當封裝成功推入時傳回成功狀態碼有所不同伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="d9d93-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="d9d93-154">刪除的封裝</span><span class="sxs-lookup"><span data-stu-id="d9d93-154">Delete a package</span></span>

<span data-ttu-id="d9d93-155">nuget.org 會解譯為封裝刪除要求的"unlist"。</span><span class="sxs-lookup"><span data-stu-id="d9d93-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="d9d93-156">這表示封裝仍可供現有消費者的封裝，但封裝不會再出現在搜尋結果中或在 web 介面。</span><span class="sxs-lookup"><span data-stu-id="d9d93-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="d9d93-157">如需此作法的詳細資訊，請參閱[刪除封裝](../policies/deleting-packages.md)原則。</span><span class="sxs-lookup"><span data-stu-id="d9d93-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="d9d93-158">其他伺服器實作會解譯為永久刪除這個信號、 虛刪除，或 unlist 可用。</span><span class="sxs-lookup"><span data-stu-id="d9d93-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="d9d93-159">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （只支援較舊的 V2 API 的伺服器實作） 支援處理此要求為 unlist 或永久刪除，根據組態選項。</span><span class="sxs-lookup"><span data-stu-id="d9d93-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="d9d93-160">要求參數</span><span class="sxs-lookup"><span data-stu-id="d9d93-160">Request parameters</span></span>

<span data-ttu-id="d9d93-161">名稱</span><span class="sxs-lookup"><span data-stu-id="d9d93-161">Name</span></span>           | <span data-ttu-id="d9d93-162">In</span><span class="sxs-lookup"><span data-stu-id="d9d93-162">In</span></span>     | <span data-ttu-id="d9d93-163">類型</span><span class="sxs-lookup"><span data-stu-id="d9d93-163">Type</span></span>   | <span data-ttu-id="d9d93-164">必要</span><span class="sxs-lookup"><span data-stu-id="d9d93-164">Required</span></span> | <span data-ttu-id="d9d93-165">注意</span><span class="sxs-lookup"><span data-stu-id="d9d93-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d9d93-166">識別碼</span><span class="sxs-lookup"><span data-stu-id="d9d93-166">ID</span></span>             | <span data-ttu-id="d9d93-167">URL</span><span class="sxs-lookup"><span data-stu-id="d9d93-167">URL</span></span>    | <span data-ttu-id="d9d93-168">字串</span><span class="sxs-lookup"><span data-stu-id="d9d93-168">string</span></span> | <span data-ttu-id="d9d93-169">是</span><span class="sxs-lookup"><span data-stu-id="d9d93-169">yes</span></span>      | <span data-ttu-id="d9d93-170">要刪除的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="d9d93-170">The ID of the package to delete</span></span>
<span data-ttu-id="d9d93-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="d9d93-171">VERSION</span></span>        | <span data-ttu-id="d9d93-172">URL</span><span class="sxs-lookup"><span data-stu-id="d9d93-172">URL</span></span>    | <span data-ttu-id="d9d93-173">字串</span><span class="sxs-lookup"><span data-stu-id="d9d93-173">string</span></span> | <span data-ttu-id="d9d93-174">是</span><span class="sxs-lookup"><span data-stu-id="d9d93-174">yes</span></span>      | <span data-ttu-id="d9d93-175">若要刪除封裝版本</span><span class="sxs-lookup"><span data-stu-id="d9d93-175">The version of the package to delete</span></span>
<span data-ttu-id="d9d93-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d9d93-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d9d93-177">頁首</span><span class="sxs-lookup"><span data-stu-id="d9d93-177">Header</span></span> | <span data-ttu-id="d9d93-178">字串</span><span class="sxs-lookup"><span data-stu-id="d9d93-178">string</span></span> | <span data-ttu-id="d9d93-179">是</span><span class="sxs-lookup"><span data-stu-id="d9d93-179">yes</span></span>      | <span data-ttu-id="d9d93-180">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="d9d93-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="d9d93-181">回應</span><span class="sxs-lookup"><span data-stu-id="d9d93-181">Response</span></span>

<span data-ttu-id="d9d93-182">狀態碼</span><span class="sxs-lookup"><span data-stu-id="d9d93-182">Status Code</span></span> | <span data-ttu-id="d9d93-183">意義</span><span class="sxs-lookup"><span data-stu-id="d9d93-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="d9d93-184">204</span><span class="sxs-lookup"><span data-stu-id="d9d93-184">204</span></span>         | <span data-ttu-id="d9d93-185">已刪除封裝</span><span class="sxs-lookup"><span data-stu-id="d9d93-185">The package was deleted</span></span>
<span data-ttu-id="d9d93-186">404</span><span class="sxs-lookup"><span data-stu-id="d9d93-186">404</span></span>         | <span data-ttu-id="d9d93-187">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="d9d93-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="d9d93-188">Relist 封裝</span><span class="sxs-lookup"><span data-stu-id="d9d93-188">Relist a package</span></span>

<span data-ttu-id="d9d93-189">如果封裝未列出，很可能要在搜尋結果中使用 「 relist 」 端點再次顯示該封裝。</span><span class="sxs-lookup"><span data-stu-id="d9d93-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="d9d93-190">此端點都有相同的圖形做為[刪除 (unlist) 端點](#delete-a-package)但使用`POST`HTTP 方法，而非`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="d9d93-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="d9d93-191">如果已列出封裝，請要求仍然會成功。</span><span class="sxs-lookup"><span data-stu-id="d9d93-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="d9d93-192">要求參數</span><span class="sxs-lookup"><span data-stu-id="d9d93-192">Request parameters</span></span>

<span data-ttu-id="d9d93-193">名稱</span><span class="sxs-lookup"><span data-stu-id="d9d93-193">Name</span></span>           | <span data-ttu-id="d9d93-194">In</span><span class="sxs-lookup"><span data-stu-id="d9d93-194">In</span></span>     | <span data-ttu-id="d9d93-195">類型</span><span class="sxs-lookup"><span data-stu-id="d9d93-195">Type</span></span>   | <span data-ttu-id="d9d93-196">必要</span><span class="sxs-lookup"><span data-stu-id="d9d93-196">Required</span></span> | <span data-ttu-id="d9d93-197">注意</span><span class="sxs-lookup"><span data-stu-id="d9d93-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d9d93-198">識別碼</span><span class="sxs-lookup"><span data-stu-id="d9d93-198">ID</span></span>             | <span data-ttu-id="d9d93-199">URL</span><span class="sxs-lookup"><span data-stu-id="d9d93-199">URL</span></span>    | <span data-ttu-id="d9d93-200">字串</span><span class="sxs-lookup"><span data-stu-id="d9d93-200">string</span></span> | <span data-ttu-id="d9d93-201">是</span><span class="sxs-lookup"><span data-stu-id="d9d93-201">yes</span></span>      | <span data-ttu-id="d9d93-202">要 relist 封裝的識別碼</span><span class="sxs-lookup"><span data-stu-id="d9d93-202">The ID of the package to relist</span></span>
<span data-ttu-id="d9d93-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="d9d93-203">VERSION</span></span>        | <span data-ttu-id="d9d93-204">URL</span><span class="sxs-lookup"><span data-stu-id="d9d93-204">URL</span></span>    | <span data-ttu-id="d9d93-205">字串</span><span class="sxs-lookup"><span data-stu-id="d9d93-205">string</span></span> | <span data-ttu-id="d9d93-206">是</span><span class="sxs-lookup"><span data-stu-id="d9d93-206">yes</span></span>      | <span data-ttu-id="d9d93-207">若要 relist 封裝版本</span><span class="sxs-lookup"><span data-stu-id="d9d93-207">The version of the package to relist</span></span>
<span data-ttu-id="d9d93-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d9d93-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d9d93-209">頁首</span><span class="sxs-lookup"><span data-stu-id="d9d93-209">Header</span></span> | <span data-ttu-id="d9d93-210">字串</span><span class="sxs-lookup"><span data-stu-id="d9d93-210">string</span></span> | <span data-ttu-id="d9d93-211">是</span><span class="sxs-lookup"><span data-stu-id="d9d93-211">yes</span></span>      | <span data-ttu-id="d9d93-212">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="d9d93-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="d9d93-213">回應</span><span class="sxs-lookup"><span data-stu-id="d9d93-213">Response</span></span>

<span data-ttu-id="d9d93-214">狀態碼</span><span class="sxs-lookup"><span data-stu-id="d9d93-214">Status Code</span></span> | <span data-ttu-id="d9d93-215">意義</span><span class="sxs-lookup"><span data-stu-id="d9d93-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="d9d93-216">200</span><span class="sxs-lookup"><span data-stu-id="d9d93-216">200</span></span>         | <span data-ttu-id="d9d93-217">現在會列出封裝</span><span class="sxs-lookup"><span data-stu-id="d9d93-217">The package is now listed</span></span>
<span data-ttu-id="d9d93-218">404</span><span class="sxs-lookup"><span data-stu-id="d9d93-218">404</span></span>         | <span data-ttu-id="d9d93-219">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="d9d93-219">No package with the provided `ID` and `VERSION` exists</span></span>
