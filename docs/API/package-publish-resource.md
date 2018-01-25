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
description: "發行服務可讓用戶端對發佈新的套件和 unlist 或刪除現有的封裝。"
keywords: "NuGet API 發送套件，NuGet API 刪除套件，NuGet API unlist 套件，NuGet API 上傳封裝、 NuGet API 建立封裝"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: f8051ca57fccae77917567d8c9f2f8a120a8d884
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="1b752-104">發送和刪除</span><span class="sxs-lookup"><span data-stu-id="1b752-104">Push and Delete</span></span>

<span data-ttu-id="1b752-105">可推入、 刪除 （或 unlist，視伺服器實作而定），和 relist 使用 NuGet V3 API 的封裝。</span><span class="sxs-lookup"><span data-stu-id="1b752-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="1b752-106">這些作業會為基礎`PackagePublish`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="1b752-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="1b752-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="1b752-107">Versioning</span></span>

<span data-ttu-id="1b752-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="1b752-108">The following `@type` value is used:</span></span>

<span data-ttu-id="1b752-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="1b752-109">@type value</span></span>          | <span data-ttu-id="1b752-110">注意</span><span class="sxs-lookup"><span data-stu-id="1b752-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="1b752-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="1b752-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="1b752-112">初版</span><span class="sxs-lookup"><span data-stu-id="1b752-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="1b752-113">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="1b752-113">Base URL</span></span>

<span data-ttu-id="1b752-114">下列應用程式開發介面的基底 URL 是值`@id`屬性`PackagePublish/2.0.0`封裝來源中的資源[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="1b752-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="1b752-115">如下列文件，會使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="1b752-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="1b752-116">請考慮`https://www.nuget.org/api/v2/package`做為預留位置`@id`值的索引中找到服務。</span><span class="sxs-lookup"><span data-stu-id="1b752-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="1b752-117">請注意，此 URL 指向舊版 V2 推入端點的相同位置因為通訊協定是相同。</span><span class="sxs-lookup"><span data-stu-id="1b752-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1b752-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1b752-118">HTTP methods</span></span>

<span data-ttu-id="1b752-119">`PUT`，`POST`和`DELETE`這項資源所支援的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="1b752-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="1b752-120">針對每個端點都支援的方法，請參閱下文。</span><span class="sxs-lookup"><span data-stu-id="1b752-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="1b752-121">推播封裝</span><span class="sxs-lookup"><span data-stu-id="1b752-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="1b752-122">具有 nuget.org[其他需求](NuGet-Protocols.md)與推入端點互動。</span><span class="sxs-lookup"><span data-stu-id="1b752-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="1b752-123">nuget.org 支援使用下列 API 的推送新套件。</span><span class="sxs-lookup"><span data-stu-id="1b752-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="1b752-124">如果提供的識別碼和版本的套件已經存在，nuget.org 將會拒絕推送。</span><span class="sxs-lookup"><span data-stu-id="1b752-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="1b752-125">其他封裝來源可能會支援取代現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="1b752-125">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="1b752-126">要求參數</span><span class="sxs-lookup"><span data-stu-id="1b752-126">Request parameters</span></span>

<span data-ttu-id="1b752-127">名稱</span><span class="sxs-lookup"><span data-stu-id="1b752-127">Name</span></span>           | <span data-ttu-id="1b752-128">In</span><span class="sxs-lookup"><span data-stu-id="1b752-128">In</span></span>     | <span data-ttu-id="1b752-129">類型</span><span class="sxs-lookup"><span data-stu-id="1b752-129">Type</span></span>   | <span data-ttu-id="1b752-130">必要</span><span class="sxs-lookup"><span data-stu-id="1b752-130">Required</span></span> | <span data-ttu-id="1b752-131">注意</span><span class="sxs-lookup"><span data-stu-id="1b752-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1b752-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1b752-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1b752-133">頁首</span><span class="sxs-lookup"><span data-stu-id="1b752-133">Header</span></span> | <span data-ttu-id="1b752-134">字串</span><span class="sxs-lookup"><span data-stu-id="1b752-134">string</span></span> | <span data-ttu-id="1b752-135">是</span><span class="sxs-lookup"><span data-stu-id="1b752-135">yes</span></span>      | <span data-ttu-id="1b752-136">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1b752-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="1b752-137">API 金鑰是不透明的字串從套件來源取得的使用者，並設定在用戶端。</span><span class="sxs-lookup"><span data-stu-id="1b752-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="1b752-138">託管沒有特定字串的格式，但 API 金鑰的長度應該超過合理的大小，如 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="1b752-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="1b752-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="1b752-139">Request body</span></span>

<span data-ttu-id="1b752-140">要求主體必須有下列形式：</span><span class="sxs-lookup"><span data-stu-id="1b752-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="1b752-141">多部分表單資料</span><span class="sxs-lookup"><span data-stu-id="1b752-141">Multipart form data</span></span>

<span data-ttu-id="1b752-142">要求標頭`Content-Type`是`multipart/form-data`和要求主體中的第一個項目會被按下的.nupkg 未經處理位元組。</span><span class="sxs-lookup"><span data-stu-id="1b752-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="1b752-143">在多組件主體中的後續項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="1b752-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="1b752-144">檔案名稱或其他任何標頭的多組件的項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="1b752-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="1b752-145">回應</span><span class="sxs-lookup"><span data-stu-id="1b752-145">Response</span></span>

<span data-ttu-id="1b752-146">狀態碼</span><span class="sxs-lookup"><span data-stu-id="1b752-146">Status Code</span></span> | <span data-ttu-id="1b752-147">意義</span><span class="sxs-lookup"><span data-stu-id="1b752-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="1b752-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="1b752-148">201, 202</span></span>    | <span data-ttu-id="1b752-149">封裝已成功推入</span><span class="sxs-lookup"><span data-stu-id="1b752-149">The package was successfully pushed</span></span>
<span data-ttu-id="1b752-150">400</span><span class="sxs-lookup"><span data-stu-id="1b752-150">400</span></span>         | <span data-ttu-id="1b752-151">提供的封裝無效</span><span class="sxs-lookup"><span data-stu-id="1b752-151">The provided package is invalid</span></span>
<span data-ttu-id="1b752-152">409</span><span class="sxs-lookup"><span data-stu-id="1b752-152">409</span></span>         | <span data-ttu-id="1b752-153">提供的識別碼和版本的封裝已經存在</span><span class="sxs-lookup"><span data-stu-id="1b752-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="1b752-154">當封裝成功推入時傳回成功狀態碼有所不同伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="1b752-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="1b752-155">刪除的封裝</span><span class="sxs-lookup"><span data-stu-id="1b752-155">Delete a package</span></span>

<span data-ttu-id="1b752-156">nuget.org 會解譯為封裝刪除要求的"unlist"。</span><span class="sxs-lookup"><span data-stu-id="1b752-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="1b752-157">這表示封裝仍可供現有消費者的封裝，但封裝不會再出現在搜尋結果中或在 web 介面。</span><span class="sxs-lookup"><span data-stu-id="1b752-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="1b752-158">如需此作法的詳細資訊，請參閱[刪除封裝](../policies/deleting-packages.md)原則。</span><span class="sxs-lookup"><span data-stu-id="1b752-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="1b752-159">其他伺服器實作會解譯為永久刪除這個信號、 虛刪除，或 unlist 可用。</span><span class="sxs-lookup"><span data-stu-id="1b752-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="1b752-160">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （只支援較舊的 V2 API 的伺服器實作） 支援處理此要求為 unlist 或永久刪除，根據組態選項。</span><span class="sxs-lookup"><span data-stu-id="1b752-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="1b752-161">要求參數</span><span class="sxs-lookup"><span data-stu-id="1b752-161">Request parameters</span></span>

<span data-ttu-id="1b752-162">名稱</span><span class="sxs-lookup"><span data-stu-id="1b752-162">Name</span></span>           | <span data-ttu-id="1b752-163">In</span><span class="sxs-lookup"><span data-stu-id="1b752-163">In</span></span>     | <span data-ttu-id="1b752-164">類型</span><span class="sxs-lookup"><span data-stu-id="1b752-164">Type</span></span>   | <span data-ttu-id="1b752-165">必要</span><span class="sxs-lookup"><span data-stu-id="1b752-165">Required</span></span> | <span data-ttu-id="1b752-166">注意</span><span class="sxs-lookup"><span data-stu-id="1b752-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1b752-167">識別碼</span><span class="sxs-lookup"><span data-stu-id="1b752-167">ID</span></span>             | <span data-ttu-id="1b752-168">URL</span><span class="sxs-lookup"><span data-stu-id="1b752-168">URL</span></span>    | <span data-ttu-id="1b752-169">字串</span><span class="sxs-lookup"><span data-stu-id="1b752-169">string</span></span> | <span data-ttu-id="1b752-170">是</span><span class="sxs-lookup"><span data-stu-id="1b752-170">yes</span></span>      | <span data-ttu-id="1b752-171">要刪除的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="1b752-171">The ID of the package to delete</span></span>
<span data-ttu-id="1b752-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="1b752-172">VERSION</span></span>        | <span data-ttu-id="1b752-173">URL</span><span class="sxs-lookup"><span data-stu-id="1b752-173">URL</span></span>    | <span data-ttu-id="1b752-174">字串</span><span class="sxs-lookup"><span data-stu-id="1b752-174">string</span></span> | <span data-ttu-id="1b752-175">是</span><span class="sxs-lookup"><span data-stu-id="1b752-175">yes</span></span>      | <span data-ttu-id="1b752-176">若要刪除封裝版本</span><span class="sxs-lookup"><span data-stu-id="1b752-176">The version of the package to delete</span></span>
<span data-ttu-id="1b752-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1b752-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1b752-178">頁首</span><span class="sxs-lookup"><span data-stu-id="1b752-178">Header</span></span> | <span data-ttu-id="1b752-179">字串</span><span class="sxs-lookup"><span data-stu-id="1b752-179">string</span></span> | <span data-ttu-id="1b752-180">是</span><span class="sxs-lookup"><span data-stu-id="1b752-180">yes</span></span>      | <span data-ttu-id="1b752-181">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1b752-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1b752-182">回應</span><span class="sxs-lookup"><span data-stu-id="1b752-182">Response</span></span>

<span data-ttu-id="1b752-183">狀態碼</span><span class="sxs-lookup"><span data-stu-id="1b752-183">Status Code</span></span> | <span data-ttu-id="1b752-184">意義</span><span class="sxs-lookup"><span data-stu-id="1b752-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="1b752-185">204</span><span class="sxs-lookup"><span data-stu-id="1b752-185">204</span></span>         | <span data-ttu-id="1b752-186">已刪除封裝</span><span class="sxs-lookup"><span data-stu-id="1b752-186">The package was deleted</span></span>
<span data-ttu-id="1b752-187">404</span><span class="sxs-lookup"><span data-stu-id="1b752-187">404</span></span>         | <span data-ttu-id="1b752-188">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="1b752-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="1b752-189">Relist 封裝</span><span class="sxs-lookup"><span data-stu-id="1b752-189">Relist a package</span></span>

<span data-ttu-id="1b752-190">如果封裝未列出，很可能要在搜尋結果中使用 「 relist 」 端點再次顯示該封裝。</span><span class="sxs-lookup"><span data-stu-id="1b752-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="1b752-191">此端點都有相同的圖形做為[刪除 (unlist) 端點](#delete-a-package)但使用`POST`HTTP 方法，而非`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="1b752-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="1b752-192">如果已列出封裝，請要求仍然會成功。</span><span class="sxs-lookup"><span data-stu-id="1b752-192">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="1b752-193">要求參數</span><span class="sxs-lookup"><span data-stu-id="1b752-193">Request parameters</span></span>

<span data-ttu-id="1b752-194">名稱</span><span class="sxs-lookup"><span data-stu-id="1b752-194">Name</span></span>           | <span data-ttu-id="1b752-195">In</span><span class="sxs-lookup"><span data-stu-id="1b752-195">In</span></span>     | <span data-ttu-id="1b752-196">類型</span><span class="sxs-lookup"><span data-stu-id="1b752-196">Type</span></span>   | <span data-ttu-id="1b752-197">必要</span><span class="sxs-lookup"><span data-stu-id="1b752-197">Required</span></span> | <span data-ttu-id="1b752-198">注意</span><span class="sxs-lookup"><span data-stu-id="1b752-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1b752-199">識別碼</span><span class="sxs-lookup"><span data-stu-id="1b752-199">ID</span></span>             | <span data-ttu-id="1b752-200">URL</span><span class="sxs-lookup"><span data-stu-id="1b752-200">URL</span></span>    | <span data-ttu-id="1b752-201">字串</span><span class="sxs-lookup"><span data-stu-id="1b752-201">string</span></span> | <span data-ttu-id="1b752-202">是</span><span class="sxs-lookup"><span data-stu-id="1b752-202">yes</span></span>      | <span data-ttu-id="1b752-203">要 relist 封裝的識別碼</span><span class="sxs-lookup"><span data-stu-id="1b752-203">The ID of the package to relist</span></span>
<span data-ttu-id="1b752-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="1b752-204">VERSION</span></span>        | <span data-ttu-id="1b752-205">URL</span><span class="sxs-lookup"><span data-stu-id="1b752-205">URL</span></span>    | <span data-ttu-id="1b752-206">字串</span><span class="sxs-lookup"><span data-stu-id="1b752-206">string</span></span> | <span data-ttu-id="1b752-207">是</span><span class="sxs-lookup"><span data-stu-id="1b752-207">yes</span></span>      | <span data-ttu-id="1b752-208">若要 relist 封裝版本</span><span class="sxs-lookup"><span data-stu-id="1b752-208">The version of the package to relist</span></span>
<span data-ttu-id="1b752-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1b752-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1b752-210">頁首</span><span class="sxs-lookup"><span data-stu-id="1b752-210">Header</span></span> | <span data-ttu-id="1b752-211">字串</span><span class="sxs-lookup"><span data-stu-id="1b752-211">string</span></span> | <span data-ttu-id="1b752-212">是</span><span class="sxs-lookup"><span data-stu-id="1b752-212">yes</span></span>      | <span data-ttu-id="1b752-213">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1b752-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1b752-214">回應</span><span class="sxs-lookup"><span data-stu-id="1b752-214">Response</span></span>

<span data-ttu-id="1b752-215">狀態碼</span><span class="sxs-lookup"><span data-stu-id="1b752-215">Status Code</span></span> | <span data-ttu-id="1b752-216">意義</span><span class="sxs-lookup"><span data-stu-id="1b752-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="1b752-217">200</span><span class="sxs-lookup"><span data-stu-id="1b752-217">200</span></span>         | <span data-ttu-id="1b752-218">現在會列出封裝</span><span class="sxs-lookup"><span data-stu-id="1b752-218">The package is now listed</span></span>
<span data-ttu-id="1b752-219">404</span><span class="sxs-lookup"><span data-stu-id="1b752-219">404</span></span>         | <span data-ttu-id="1b752-220">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="1b752-220">No package with the provided `ID` and `VERSION` exists</span></span>
