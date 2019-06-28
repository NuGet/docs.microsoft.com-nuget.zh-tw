---
title: 推送與刪除，NuGet API
description: 發行 」 服務可讓用戶端來發佈新的套件，並取消列出或刪除現有的封裝。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426728"
---
# <a name="push-and-delete"></a><span data-ttu-id="2caa6-103">推送與刪除</span><span class="sxs-lookup"><span data-stu-id="2caa6-103">Push and Delete</span></span>

<span data-ttu-id="2caa6-104">您可將推播、 刪除 （或取消列出，根據伺服器實作） 和重新列出封裝使用 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="2caa6-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="2caa6-105">這些作業會為基礎`PackagePublish`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2caa6-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2caa6-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="2caa6-106">Versioning</span></span>

<span data-ttu-id="2caa6-107">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="2caa6-107">The following `@type` value is used:</span></span>

<span data-ttu-id="2caa6-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="2caa6-108">@type value</span></span>          | <span data-ttu-id="2caa6-109">注意</span><span class="sxs-lookup"><span data-stu-id="2caa6-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="2caa6-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="2caa6-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="2caa6-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="2caa6-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2caa6-112">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="2caa6-112">Base URL</span></span>

<span data-ttu-id="2caa6-113">下列 Api 的基底 URL 是值`@id`的屬性`PackagePublish/2.0.0`封裝來源中的資源[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2caa6-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="2caa6-114">下列文件，會使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="2caa6-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="2caa6-115">請考慮`https://www.nuget.org/api/v2/package`作為預留位置`@id`服務索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="2caa6-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="2caa6-116">請注意，此 URL 會指向與舊版的 V2 推播端點位於相同位置因為通訊協定相同。</span><span class="sxs-lookup"><span data-stu-id="2caa6-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2caa6-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2caa6-117">HTTP methods</span></span>

<span data-ttu-id="2caa6-118">`PUT`，`POST`和`DELETE`這項資源所支援 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="2caa6-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="2caa6-119">針對每個端點上支援何種方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2caa6-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="2caa6-120">將封裝推送</span><span class="sxs-lookup"><span data-stu-id="2caa6-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="2caa6-121">nuget.org 已[其他需求](NuGet-Protocols.md)與推播端點互動。</span><span class="sxs-lookup"><span data-stu-id="2caa6-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="2caa6-122">nuget.org 支援使用下列 API 推送新的套件。</span><span class="sxs-lookup"><span data-stu-id="2caa6-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="2caa6-123">如果提供的識別碼和版本的套件已經存在，nuget.org 會拒絕推送。</span><span class="sxs-lookup"><span data-stu-id="2caa6-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="2caa6-124">其他套件來源可能會支援取代現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="2caa6-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="2caa6-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="2caa6-125">Request parameters</span></span>

<span data-ttu-id="2caa6-126">名稱</span><span class="sxs-lookup"><span data-stu-id="2caa6-126">Name</span></span>           | <span data-ttu-id="2caa6-127">In</span><span class="sxs-lookup"><span data-stu-id="2caa6-127">In</span></span>     | <span data-ttu-id="2caa6-128">類型</span><span class="sxs-lookup"><span data-stu-id="2caa6-128">Type</span></span>   | <span data-ttu-id="2caa6-129">必要</span><span class="sxs-lookup"><span data-stu-id="2caa6-129">Required</span></span> | <span data-ttu-id="2caa6-130">注意</span><span class="sxs-lookup"><span data-stu-id="2caa6-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2caa6-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2caa6-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2caa6-132">標頭</span><span class="sxs-lookup"><span data-stu-id="2caa6-132">Header</span></span> | <span data-ttu-id="2caa6-133">字串</span><span class="sxs-lookup"><span data-stu-id="2caa6-133">string</span></span> | <span data-ttu-id="2caa6-134">是</span><span class="sxs-lookup"><span data-stu-id="2caa6-134">yes</span></span>      | <span data-ttu-id="2caa6-135">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2caa6-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="2caa6-136">API 金鑰是不透明的字串，從套件來源取得的使用者，並在用戶端設定。</span><span class="sxs-lookup"><span data-stu-id="2caa6-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="2caa6-137">沒有特定字串的格式託管，但 API 金鑰的長度不應超過合理的大小，如 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="2caa6-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="2caa6-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="2caa6-138">Request body</span></span>

<span data-ttu-id="2caa6-139">要求本文必須有下列形式：</span><span class="sxs-lookup"><span data-stu-id="2caa6-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="2caa6-140">多部分表單資料</span><span class="sxs-lookup"><span data-stu-id="2caa6-140">Multipart form data</span></span>

<span data-ttu-id="2caa6-141">要求標頭`Content-Type`是`multipart/form-data`和要求本文中的第一個項目會被推入.nupkg 檔案的未經處理位元組。</span><span class="sxs-lookup"><span data-stu-id="2caa6-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="2caa6-142">在多組件的主體中的後續項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="2caa6-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="2caa6-143">會忽略的檔案名稱或任何其他標頭的多組件的項目。</span><span class="sxs-lookup"><span data-stu-id="2caa6-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="2caa6-144">回應</span><span class="sxs-lookup"><span data-stu-id="2caa6-144">Response</span></span>

<span data-ttu-id="2caa6-145">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2caa6-145">Status Code</span></span> | <span data-ttu-id="2caa6-146">意義</span><span class="sxs-lookup"><span data-stu-id="2caa6-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="2caa6-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="2caa6-147">201, 202</span></span>    | <span data-ttu-id="2caa6-148">已成功推送套件</span><span class="sxs-lookup"><span data-stu-id="2caa6-148">The package was successfully pushed</span></span>
<span data-ttu-id="2caa6-149">400</span><span class="sxs-lookup"><span data-stu-id="2caa6-149">400</span></span>         | <span data-ttu-id="2caa6-150">提供的套件無效</span><span class="sxs-lookup"><span data-stu-id="2caa6-150">The provided package is invalid</span></span>
<span data-ttu-id="2caa6-151">409</span><span class="sxs-lookup"><span data-stu-id="2caa6-151">409</span></span>         | <span data-ttu-id="2caa6-152">使用提供的識別碼和版本的封裝已經存在</span><span class="sxs-lookup"><span data-stu-id="2caa6-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="2caa6-153">伺服器實作會傳回已成功推送套件時的成功狀態碼而有所不同。</span><span class="sxs-lookup"><span data-stu-id="2caa6-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="2caa6-154">刪除套件</span><span class="sxs-lookup"><span data-stu-id="2caa6-154">Delete a package</span></span>

<span data-ttu-id="2caa6-155">nuget.org 會解譯為套件刪除要求的 「 取消列出 」。</span><span class="sxs-lookup"><span data-stu-id="2caa6-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="2caa6-156">這表示封裝是仍然可供現有的取用者的封裝，但是封裝不會再出現在搜尋結果中或 web 介面中。</span><span class="sxs-lookup"><span data-stu-id="2caa6-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="2caa6-157">如需有關此做法的詳細資訊，請參閱[刪除套件](../nuget-org/policies/deleting-packages.md)原則。</span><span class="sxs-lookup"><span data-stu-id="2caa6-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="2caa6-158">其他伺服器實作會解譯為永久刪除此訊號、 虛刪除，或取消列出免費的。</span><span class="sxs-lookup"><span data-stu-id="2caa6-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="2caa6-159">例如， [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) （只支援較舊的 V2 API 的伺服器實作） 支援處理此要求以取消列出或永久刪除根據組態選項。</span><span class="sxs-lookup"><span data-stu-id="2caa6-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="2caa6-160">要求參數</span><span class="sxs-lookup"><span data-stu-id="2caa6-160">Request parameters</span></span>

<span data-ttu-id="2caa6-161">名稱</span><span class="sxs-lookup"><span data-stu-id="2caa6-161">Name</span></span>           | <span data-ttu-id="2caa6-162">In</span><span class="sxs-lookup"><span data-stu-id="2caa6-162">In</span></span>     | <span data-ttu-id="2caa6-163">類型</span><span class="sxs-lookup"><span data-stu-id="2caa6-163">Type</span></span>   | <span data-ttu-id="2caa6-164">必要</span><span class="sxs-lookup"><span data-stu-id="2caa6-164">Required</span></span> | <span data-ttu-id="2caa6-165">注意</span><span class="sxs-lookup"><span data-stu-id="2caa6-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2caa6-166">識別碼</span><span class="sxs-lookup"><span data-stu-id="2caa6-166">ID</span></span>             | <span data-ttu-id="2caa6-167">URL</span><span class="sxs-lookup"><span data-stu-id="2caa6-167">URL</span></span>    | <span data-ttu-id="2caa6-168">字串</span><span class="sxs-lookup"><span data-stu-id="2caa6-168">string</span></span> | <span data-ttu-id="2caa6-169">是</span><span class="sxs-lookup"><span data-stu-id="2caa6-169">yes</span></span>      | <span data-ttu-id="2caa6-170">要刪除的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="2caa6-170">The ID of the package to delete</span></span>
<span data-ttu-id="2caa6-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="2caa6-171">VERSION</span></span>        | <span data-ttu-id="2caa6-172">URL</span><span class="sxs-lookup"><span data-stu-id="2caa6-172">URL</span></span>    | <span data-ttu-id="2caa6-173">字串</span><span class="sxs-lookup"><span data-stu-id="2caa6-173">string</span></span> | <span data-ttu-id="2caa6-174">是</span><span class="sxs-lookup"><span data-stu-id="2caa6-174">yes</span></span>      | <span data-ttu-id="2caa6-175">若要刪除封裝的版本</span><span class="sxs-lookup"><span data-stu-id="2caa6-175">The version of the package to delete</span></span>
<span data-ttu-id="2caa6-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2caa6-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2caa6-177">標頭</span><span class="sxs-lookup"><span data-stu-id="2caa6-177">Header</span></span> | <span data-ttu-id="2caa6-178">字串</span><span class="sxs-lookup"><span data-stu-id="2caa6-178">string</span></span> | <span data-ttu-id="2caa6-179">是</span><span class="sxs-lookup"><span data-stu-id="2caa6-179">yes</span></span>      | <span data-ttu-id="2caa6-180">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2caa6-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="2caa6-181">回應</span><span class="sxs-lookup"><span data-stu-id="2caa6-181">Response</span></span>

<span data-ttu-id="2caa6-182">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2caa6-182">Status Code</span></span> | <span data-ttu-id="2caa6-183">意義</span><span class="sxs-lookup"><span data-stu-id="2caa6-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="2caa6-184">204</span><span class="sxs-lookup"><span data-stu-id="2caa6-184">204</span></span>         | <span data-ttu-id="2caa6-185">已刪除的套件</span><span class="sxs-lookup"><span data-stu-id="2caa6-185">The package was deleted</span></span>
<span data-ttu-id="2caa6-186">404</span><span class="sxs-lookup"><span data-stu-id="2caa6-186">404</span></span>         | <span data-ttu-id="2caa6-187">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="2caa6-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="2caa6-188">重新列出封裝</span><span class="sxs-lookup"><span data-stu-id="2caa6-188">Relist a package</span></span>

<span data-ttu-id="2caa6-189">如果未列出的封裝，就能夠顯示該套件一次一次使用 「 重新列出 」 端點的搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="2caa6-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="2caa6-190">此端點具有一樣[刪除 （取消列出） 端點](#delete-a-package)使用，但`POST`HTTP 方法，而非`DELETE`方法。</span><span class="sxs-lookup"><span data-stu-id="2caa6-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="2caa6-191">如果已列出的封裝，請要求仍然會成功。</span><span class="sxs-lookup"><span data-stu-id="2caa6-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="2caa6-192">要求參數</span><span class="sxs-lookup"><span data-stu-id="2caa6-192">Request parameters</span></span>

<span data-ttu-id="2caa6-193">名稱</span><span class="sxs-lookup"><span data-stu-id="2caa6-193">Name</span></span>           | <span data-ttu-id="2caa6-194">In</span><span class="sxs-lookup"><span data-stu-id="2caa6-194">In</span></span>     | <span data-ttu-id="2caa6-195">類型</span><span class="sxs-lookup"><span data-stu-id="2caa6-195">Type</span></span>   | <span data-ttu-id="2caa6-196">必要</span><span class="sxs-lookup"><span data-stu-id="2caa6-196">Required</span></span> | <span data-ttu-id="2caa6-197">注意</span><span class="sxs-lookup"><span data-stu-id="2caa6-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2caa6-198">識別碼</span><span class="sxs-lookup"><span data-stu-id="2caa6-198">ID</span></span>             | <span data-ttu-id="2caa6-199">URL</span><span class="sxs-lookup"><span data-stu-id="2caa6-199">URL</span></span>    | <span data-ttu-id="2caa6-200">字串</span><span class="sxs-lookup"><span data-stu-id="2caa6-200">string</span></span> | <span data-ttu-id="2caa6-201">是</span><span class="sxs-lookup"><span data-stu-id="2caa6-201">yes</span></span>      | <span data-ttu-id="2caa6-202">要重新列出封裝的識別碼</span><span class="sxs-lookup"><span data-stu-id="2caa6-202">The ID of the package to relist</span></span>
<span data-ttu-id="2caa6-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="2caa6-203">VERSION</span></span>        | <span data-ttu-id="2caa6-204">URL</span><span class="sxs-lookup"><span data-stu-id="2caa6-204">URL</span></span>    | <span data-ttu-id="2caa6-205">字串</span><span class="sxs-lookup"><span data-stu-id="2caa6-205">string</span></span> | <span data-ttu-id="2caa6-206">是</span><span class="sxs-lookup"><span data-stu-id="2caa6-206">yes</span></span>      | <span data-ttu-id="2caa6-207">若要重新列出封裝的版本</span><span class="sxs-lookup"><span data-stu-id="2caa6-207">The version of the package to relist</span></span>
<span data-ttu-id="2caa6-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2caa6-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2caa6-209">標頭</span><span class="sxs-lookup"><span data-stu-id="2caa6-209">Header</span></span> | <span data-ttu-id="2caa6-210">字串</span><span class="sxs-lookup"><span data-stu-id="2caa6-210">string</span></span> | <span data-ttu-id="2caa6-211">是</span><span class="sxs-lookup"><span data-stu-id="2caa6-211">yes</span></span>      | <span data-ttu-id="2caa6-212">例如： `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2caa6-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="2caa6-213">回應</span><span class="sxs-lookup"><span data-stu-id="2caa6-213">Response</span></span>

<span data-ttu-id="2caa6-214">狀態碼</span><span class="sxs-lookup"><span data-stu-id="2caa6-214">Status Code</span></span> | <span data-ttu-id="2caa6-215">意義</span><span class="sxs-lookup"><span data-stu-id="2caa6-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="2caa6-216">200</span><span class="sxs-lookup"><span data-stu-id="2caa6-216">200</span></span>         | <span data-ttu-id="2caa6-217">現在會列出封裝</span><span class="sxs-lookup"><span data-stu-id="2caa6-217">The package is now listed</span></span>
<span data-ttu-id="2caa6-218">404</span><span class="sxs-lookup"><span data-stu-id="2caa6-218">404</span></span>         | <span data-ttu-id="2caa6-219">使用提供的封裝`ID`和`VERSION`存在</span><span class="sxs-lookup"><span data-stu-id="2caa6-219">No package with the provided `ID` and `VERSION` exists</span></span>
