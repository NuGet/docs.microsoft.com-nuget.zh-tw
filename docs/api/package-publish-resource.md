---
title: 推送與刪除，NuGet API
description: 發行 」 服務可讓用戶端來發佈新的套件，並取消列出或刪除現有的封裝。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547517"
---
# <a name="push-and-delete"></a><span data-ttu-id="2bb5b-103">推送與刪除</span><span class="sxs-lookup"><span data-stu-id="2bb5b-103">Push and Delete</span></span>

<span data-ttu-id="2bb5b-104">您可將推播、 刪除 （或取消列出，根據伺服器實作） 和重新列出封裝使用 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="2bb5b-105">這些作業會為基礎`PackagePublish`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2bb5b-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="2bb5b-106">Versioning</span></span>

<span data-ttu-id="2bb5b-107">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="2bb5b-107">The following `@type` value is used:</span></span>

<span data-ttu-id="2bb5b-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="2bb5b-108">@type value</span></span>          | <span data-ttu-id="2bb5b-109">注意</span><span class="sxs-lookup"><span data-stu-id="2bb5b-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="2bb5b-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="2bb5b-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="2bb5b-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="2bb5b-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2bb5b-112">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="2bb5b-112">Base URL</span></span>

<span data-ttu-id="2bb5b-113">下列 Api 的基底 URL 是值`@id`的屬性`PackagePublish/2.0.0`封裝來源中的資源[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="2bb5b-114">下列文件，會使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="2bb5b-115">請考慮`https://www.nuget.org/api/v2/package`作為預留位置`@id`服務索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="2bb5b-116">請注意，此 URL 會指向與舊版的 V2 推播端點位於相同位置因為通訊協定相同。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2bb5b-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2bb5b-117">HTTP methods</span></span>

<span data-ttu-id="2bb5b-118">`PUT`，`POST`和`DELETE`這項資源所支援 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="2bb5b-119">針對每個端點上支援何種方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="2bb5b-120">將封裝推送</span><span class="sxs-lookup"><span data-stu-id="2bb5b-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="2bb5b-121">nuget.org 已[其他需求](NuGet-Protocols.md)與推播端點互動。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="2bb5b-122">nuget.org 支援使用下列 API 推送新的套件。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="2bb5b-123">如果提供的識別碼和版本的套件已經存在，nuget.org 會拒絕推送。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="2bb5b-124">其他套件來源可能會支援取代現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="2bb5b-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="2bb5b-125">Request parameters</span></span>

<span data-ttu-id="2bb5b-126">名稱</span><span class="sxs-lookup"><span data-stu-id="2bb5b-126">Name</span></span>           | <span data-ttu-id="2bb5b-127">In</span><span class="sxs-lookup"><span data-stu-id="2bb5b-127">In</span></span>     | <span data-ttu-id="2bb5b-128">類型</span><span class="sxs-lookup"><span data-stu-id="2bb5b-128">Type</span></span>   | <span data-ttu-id="2bb5b-129">必要</span><span class="sxs-lookup"><span data-stu-id="2bb5b-129">Required</span></span> | <span data-ttu-id="2bb5b-130">注意</span><span class="sxs-lookup"><span data-stu-id="2bb5b-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2bb5b-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2bb5b-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2bb5b-132">頁首</span><span class="sxs-lookup"><span data-stu-id="2bb5b-132">Header</span></span> | <span data-ttu-id="2bb5b-133">字串</span><span class="sxs-lookup"><span data-stu-id="2bb5b-133">string</span></span> | <span data-ttu-id="2bb5b-134">是</span><span class="sxs-lookup"><span data-stu-id="2bb5b-134">yes</span></span>      | <span data-ttu-id="2bb5b-135">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2bb5b-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="2bb5b-136">API 金鑰是不透明的字串，從套件來源取得的使用者，並在用戶端設定。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="2bb5b-137">沒有特定字串的格式託管，但 API 金鑰的長度不應超過合理的大小，如 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="2bb5b-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="2bb5b-138">Request body</span></span>

<span data-ttu-id="2bb5b-139">要求本文必須有下列形式：</span><span class="sxs-lookup"><span data-stu-id="2bb5b-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="2bb5b-140">多部分表單資料</span><span class="sxs-lookup"><span data-stu-id="2bb5b-140">Multipart form data</span></span>

<span data-ttu-id="2bb5b-141">要求標頭`Content-Type`是`multipart/form-data`和要求本文中的第一個項目會被推入.nupkg 檔案的未經處理位元組。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="2bb5b-142">在多組件的主體中的後續項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="2bb5b-143">會忽略的檔案名稱或任何其他標頭的多組件的項目。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="2bb5b-144">回應</span><span class="sxs-lookup"><span data-stu-id="2bb5b-144">Response</span></span>

<span data-ttu-id="2bb5b-145">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2bb5b-145">Status Code</span></span> | <span data-ttu-id="2bb5b-146">意義</span><span class="sxs-lookup"><span data-stu-id="2bb5b-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="2bb5b-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="2bb5b-147">201, 202</span></span>    | <span data-ttu-id="2bb5b-148">已成功推送套件</span><span class="sxs-lookup"><span data-stu-id="2bb5b-148">The package was successfully pushed</span></span>
<span data-ttu-id="2bb5b-149">400</span><span class="sxs-lookup"><span data-stu-id="2bb5b-149">400</span></span>         | <span data-ttu-id="2bb5b-150">提供的套件無效</span><span class="sxs-lookup"><span data-stu-id="2bb5b-150">The provided package is invalid</span></span>
<span data-ttu-id="2bb5b-151">409</span><span class="sxs-lookup"><span data-stu-id="2bb5b-151">409</span></span>         | <span data-ttu-id="2bb5b-152">使用提供的識別碼和版本的封裝已經存在</span><span class="sxs-lookup"><span data-stu-id="2bb5b-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="2bb5b-153">伺服器實作會傳回已成功推送套件時的成功狀態碼而有所不同。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="2bb5b-154">刪除套件</span><span class="sxs-lookup"><span data-stu-id="2bb5b-154">Delete a package</span></span>

<span data-ttu-id="2bb5b-155">nuget.org 會解譯為套件刪除要求的 「 取消列出 」。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="2bb5b-156">這表示封裝是仍然可供現有的取用者的封裝，但是封裝不會再出現在搜尋結果中或 web 介面中。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="2bb5b-157">如需有關此做法的詳細資訊，請參閱[刪除套件](../policies/deleting-packages.md)原則。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="2bb5b-158">其他伺服器實作會解譯為永久刪除此訊號、 虛刪除，或取消列出免費的。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="2bb5b-159">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （只支援較舊的 V2 API 的伺服器實作） 支援處理此要求以取消列出或永久刪除根據組態選項。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="2bb5b-160">要求參數</span><span class="sxs-lookup"><span data-stu-id="2bb5b-160">Request parameters</span></span>

<span data-ttu-id="2bb5b-161">名稱</span><span class="sxs-lookup"><span data-stu-id="2bb5b-161">Name</span></span>           | <span data-ttu-id="2bb5b-162">In</span><span class="sxs-lookup"><span data-stu-id="2bb5b-162">In</span></span>     | <span data-ttu-id="2bb5b-163">類型</span><span class="sxs-lookup"><span data-stu-id="2bb5b-163">Type</span></span>   | <span data-ttu-id="2bb5b-164">必要</span><span class="sxs-lookup"><span data-stu-id="2bb5b-164">Required</span></span> | <span data-ttu-id="2bb5b-165">注意</span><span class="sxs-lookup"><span data-stu-id="2bb5b-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2bb5b-166">識別碼</span><span class="sxs-lookup"><span data-stu-id="2bb5b-166">ID</span></span>             | <span data-ttu-id="2bb5b-167">URL</span><span class="sxs-lookup"><span data-stu-id="2bb5b-167">URL</span></span>    | <span data-ttu-id="2bb5b-168">字串</span><span class="sxs-lookup"><span data-stu-id="2bb5b-168">string</span></span> | <span data-ttu-id="2bb5b-169">是</span><span class="sxs-lookup"><span data-stu-id="2bb5b-169">yes</span></span>      | <span data-ttu-id="2bb5b-170">要刪除的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="2bb5b-170">The ID of the package to delete</span></span>
<span data-ttu-id="2bb5b-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="2bb5b-171">VERSION</span></span>        | <span data-ttu-id="2bb5b-172">URL</span><span class="sxs-lookup"><span data-stu-id="2bb5b-172">URL</span></span>    | <span data-ttu-id="2bb5b-173">字串</span><span class="sxs-lookup"><span data-stu-id="2bb5b-173">string</span></span> | <span data-ttu-id="2bb5b-174">是</span><span class="sxs-lookup"><span data-stu-id="2bb5b-174">yes</span></span>      | <span data-ttu-id="2bb5b-175">若要刪除封裝的版本</span><span class="sxs-lookup"><span data-stu-id="2bb5b-175">The version of the package to delete</span></span>
<span data-ttu-id="2bb5b-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2bb5b-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2bb5b-177">頁首</span><span class="sxs-lookup"><span data-stu-id="2bb5b-177">Header</span></span> | <span data-ttu-id="2bb5b-178">字串</span><span class="sxs-lookup"><span data-stu-id="2bb5b-178">string</span></span> | <span data-ttu-id="2bb5b-179">是</span><span class="sxs-lookup"><span data-stu-id="2bb5b-179">yes</span></span>      | <span data-ttu-id="2bb5b-180">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2bb5b-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="2bb5b-181">回應</span><span class="sxs-lookup"><span data-stu-id="2bb5b-181">Response</span></span>

<span data-ttu-id="2bb5b-182">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2bb5b-182">Status Code</span></span> | <span data-ttu-id="2bb5b-183">意義</span><span class="sxs-lookup"><span data-stu-id="2bb5b-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="2bb5b-184">204</span><span class="sxs-lookup"><span data-stu-id="2bb5b-184">204</span></span>         | <span data-ttu-id="2bb5b-185">已刪除的套件</span><span class="sxs-lookup"><span data-stu-id="2bb5b-185">The package was deleted</span></span>
<span data-ttu-id="2bb5b-186">404</span><span class="sxs-lookup"><span data-stu-id="2bb5b-186">404</span></span>         | <span data-ttu-id="2bb5b-187">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="2bb5b-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="2bb5b-188">重新列出封裝</span><span class="sxs-lookup"><span data-stu-id="2bb5b-188">Relist a package</span></span>

<span data-ttu-id="2bb5b-189">如果未列出的封裝，就能夠顯示該套件一次一次使用 「 重新列出 」 端點的搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="2bb5b-190">此端點具有一樣[刪除 （取消列出） 端點](#delete-a-package)使用，但`POST`HTTP 方法，而非`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="2bb5b-191">如果已列出的封裝，請要求仍然會成功。</span><span class="sxs-lookup"><span data-stu-id="2bb5b-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="2bb5b-192">要求參數</span><span class="sxs-lookup"><span data-stu-id="2bb5b-192">Request parameters</span></span>

<span data-ttu-id="2bb5b-193">名稱</span><span class="sxs-lookup"><span data-stu-id="2bb5b-193">Name</span></span>           | <span data-ttu-id="2bb5b-194">In</span><span class="sxs-lookup"><span data-stu-id="2bb5b-194">In</span></span>     | <span data-ttu-id="2bb5b-195">類型</span><span class="sxs-lookup"><span data-stu-id="2bb5b-195">Type</span></span>   | <span data-ttu-id="2bb5b-196">必要</span><span class="sxs-lookup"><span data-stu-id="2bb5b-196">Required</span></span> | <span data-ttu-id="2bb5b-197">注意</span><span class="sxs-lookup"><span data-stu-id="2bb5b-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2bb5b-198">識別碼</span><span class="sxs-lookup"><span data-stu-id="2bb5b-198">ID</span></span>             | <span data-ttu-id="2bb5b-199">URL</span><span class="sxs-lookup"><span data-stu-id="2bb5b-199">URL</span></span>    | <span data-ttu-id="2bb5b-200">字串</span><span class="sxs-lookup"><span data-stu-id="2bb5b-200">string</span></span> | <span data-ttu-id="2bb5b-201">是</span><span class="sxs-lookup"><span data-stu-id="2bb5b-201">yes</span></span>      | <span data-ttu-id="2bb5b-202">要重新列出封裝的識別碼</span><span class="sxs-lookup"><span data-stu-id="2bb5b-202">The ID of the package to relist</span></span>
<span data-ttu-id="2bb5b-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="2bb5b-203">VERSION</span></span>        | <span data-ttu-id="2bb5b-204">URL</span><span class="sxs-lookup"><span data-stu-id="2bb5b-204">URL</span></span>    | <span data-ttu-id="2bb5b-205">字串</span><span class="sxs-lookup"><span data-stu-id="2bb5b-205">string</span></span> | <span data-ttu-id="2bb5b-206">是</span><span class="sxs-lookup"><span data-stu-id="2bb5b-206">yes</span></span>      | <span data-ttu-id="2bb5b-207">若要重新列出封裝的版本</span><span class="sxs-lookup"><span data-stu-id="2bb5b-207">The version of the package to relist</span></span>
<span data-ttu-id="2bb5b-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2bb5b-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2bb5b-209">頁首</span><span class="sxs-lookup"><span data-stu-id="2bb5b-209">Header</span></span> | <span data-ttu-id="2bb5b-210">字串</span><span class="sxs-lookup"><span data-stu-id="2bb5b-210">string</span></span> | <span data-ttu-id="2bb5b-211">是</span><span class="sxs-lookup"><span data-stu-id="2bb5b-211">yes</span></span>      | <span data-ttu-id="2bb5b-212">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2bb5b-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="2bb5b-213">回應</span><span class="sxs-lookup"><span data-stu-id="2bb5b-213">Response</span></span>

<span data-ttu-id="2bb5b-214">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2bb5b-214">Status Code</span></span> | <span data-ttu-id="2bb5b-215">意義</span><span class="sxs-lookup"><span data-stu-id="2bb5b-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="2bb5b-216">200</span><span class="sxs-lookup"><span data-stu-id="2bb5b-216">200</span></span>         | <span data-ttu-id="2bb5b-217">現在會列出封裝</span><span class="sxs-lookup"><span data-stu-id="2bb5b-217">The package is now listed</span></span>
<span data-ttu-id="2bb5b-218">404</span><span class="sxs-lookup"><span data-stu-id="2bb5b-218">404</span></span>         | <span data-ttu-id="2bb5b-219">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="2bb5b-219">No package with the provided `ID` and `VERSION` exists</span></span>
