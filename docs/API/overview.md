---
title: "概觀、 NuGet API |Microsoft 文件"
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
description: "NuGet API 是一組可用來下載套件、 擷取中繼資料，發佈新的封裝、 等等的 HTTP 端點。"
keywords: "NuGet V3 API、 NuGet V2 API、 NuGet JSON、 NuGet 登錄應用程式開發介面，NuGet API 一般容器、 NuGet nupkg API、 NuGet 中繼資料 API、 NuGet 搜尋應用程式開發介面、 NuGet 推入應用程式開發介面，NuGe 發佈 API、 NuGet 刪除應用程式開發介面、 NuGet unlist API 的 NuGet 通訊協定"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c28b0912be6dbccab06078100cb71821c3658e08
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-api"></a><span data-ttu-id="f653f-104">NuGet 的 API</span><span class="sxs-lookup"><span data-stu-id="f653f-104">NuGet API</span></span>

<span data-ttu-id="f653f-105">NuGet API 是一組可用來下載的封裝、 擷取中繼資料、 發行新的封裝，並執行大部分官方 NuGet 用戶端中提供其他作業的 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="f653f-105">The NuGet API is a set of HTTP endpoints that can be used to download packages, fetch metadata, publish new packages, and perform most other operations available in the official NuGet clients.</span></span>

<span data-ttu-id="f653f-106">這個 API 用於在 Visual Studio、 nuget.exe 和.NET CLI NuGet 用戶端執行 NuGet 作業，例如[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)，在 Visual Studio UI 中，搜尋和[ `nuget.exe push` ](../tools/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="f653f-106">This API is used by the NuGet client in Visual Studio, nuget.exe, and the .NET CLI to perform NuGet operations such as [`dotnet restore`](/dotnet/articles/core/preview3/tools/dotnet-restore), search in the Visual Studio UI, and [`nuget.exe push`](../tools/cli-ref-push.md).</span></span>

<span data-ttu-id="f653f-107">請注意，在某些情況下中, nuget.org 有額外的需求不會強制執行由其他封裝來源。</span><span class="sxs-lookup"><span data-stu-id="f653f-107">Note in some cases, nuget.org has additional requirements that are not enforced by other package sources.</span></span> <span data-ttu-id="f653f-108">這些差異皆記錄由[nuget.org 通訊協定](nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="f653f-108">These differences are documented by the [nuget.org Protocols](nuget-protocols.md).</span></span>

## <a name="service-index"></a><span data-ttu-id="f653f-109">服務索引</span><span class="sxs-lookup"><span data-stu-id="f653f-109">Service index</span></span>

<span data-ttu-id="f653f-110">應用程式開發介面的進入點是 JSON 文件中的已知位置。</span><span class="sxs-lookup"><span data-stu-id="f653f-110">The entry point for the API is a JSON document in a well known location.</span></span> <span data-ttu-id="f653f-111">這份文件稱為**服務索引**。</span><span class="sxs-lookup"><span data-stu-id="f653f-111">This document is called the **service index**.</span></span>
<span data-ttu-id="f653f-112">Nuget.org 的服務索引的位置是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="f653f-112">The location of the service index for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

<span data-ttu-id="f653f-113">此 JSON 文件包含一份*資源*提供不同的功能以及滿足不同使用案例。</span><span class="sxs-lookup"><span data-stu-id="f653f-113">This JSON document contains a list of *resources* which provide different functionality and fulfill different use cases.</span></span>

<span data-ttu-id="f653f-114">支援 API 的用戶端應接受一或多個這些服務索引 URL 做為連接到個別的套件來源的方法。</span><span class="sxs-lookup"><span data-stu-id="f653f-114">Clients that support the API should accept one or more of these service index URL as the means of connecting to the respective package sources.</span></span>

<span data-ttu-id="f653f-115">如需服務索引的詳細資訊，請參閱[其應用程式開發介面參考](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="f653f-115">For more information about the service index, see [its API reference](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="f653f-116">版本控制</span><span class="sxs-lookup"><span data-stu-id="f653f-116">Versioning</span></span>

<span data-ttu-id="f653f-117">應用程式開發介面是 NuGet 的 HTTP 通訊協定第 3 版。</span><span class="sxs-lookup"><span data-stu-id="f653f-117">The API is version 3 of NuGet's HTTP protocol.</span></span> <span data-ttu-id="f653f-118">此通訊協定有時稱為 「 V3 API。 」</span><span class="sxs-lookup"><span data-stu-id="f653f-118">This protocol is sometimes referred to as "the V3 API."</span></span> <span data-ttu-id="f653f-119">這個版本的通訊協定會參考這些參考文件簡稱為 「 應用程式開發介面。 」</span><span class="sxs-lookup"><span data-stu-id="f653f-119">These reference documents will refer to this version of the protocol simply as "the API."</span></span>

<span data-ttu-id="f653f-120">服務索引結構描述版本會以`version`服務索引中的屬性。</span><span class="sxs-lookup"><span data-stu-id="f653f-120">The service index schema version is indicated by the `version` property in the service index.</span></span> <span data-ttu-id="f653f-121">API 要求的版本字串的主要版本號碼`3`。</span><span class="sxs-lookup"><span data-stu-id="f653f-121">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="f653f-122">服務索引結構描述會進行非中斷變更，就會增加的版本字串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="f653f-122">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="f653f-123">舊版的用戶端 (例如 nuget.exe 2.x) 不支援 V3 API，僅支援 舊 V2 API，這裡不記錄。</span><span class="sxs-lookup"><span data-stu-id="f653f-123">Older clients (such as nuget.exe 2.x) do not support the V3 API and only support the older V2 API, which is not documented here.</span></span>

<span data-ttu-id="f653f-124">NuGet V3 API 名為在這種情況，所以 V2 API 的後置項已正式 NuGet 用戶端的 2.x 版本所實作的 OData 型通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f653f-124">The NuGet V3 API is named as such because it's the successor of the V2 API, which was the OData-based protocol implemented by the 2.x version of the official NuGet client.</span></span> <span data-ttu-id="f653f-125">3.0 版的官方 NuGet 用戶端第一次支援 V3 API，而且仍然的最新的主要通訊協定版本支援 NuGet 用戶端，4.0，在。</span><span class="sxs-lookup"><span data-stu-id="f653f-125">The V3 API was first supported by the 3.0 version of the official NuGet client and is still the latest major protocol version supported by the NuGet client, 4.0 and on.</span></span> 

<span data-ttu-id="f653f-126">第一次發行以來已經對 API 進行非重大通訊協定變更。</span><span class="sxs-lookup"><span data-stu-id="f653f-126">Non-breaking protocol changes have been made to the API since it was first release.</span></span>

## <a name="resources-and-schema"></a><span data-ttu-id="f653f-127">資源和結構描述</span><span class="sxs-lookup"><span data-stu-id="f653f-127">Resources and schema</span></span>

<span data-ttu-id="f653f-128">**服務索引**描述各種資源。</span><span class="sxs-lookup"><span data-stu-id="f653f-128">The **service index** describes a variety of resources.</span></span> <span data-ttu-id="f653f-129">目前的支援的資源集，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f653f-129">The current set of supported resources are as follows:</span></span>

<span data-ttu-id="f653f-130">資源名稱</span><span class="sxs-lookup"><span data-stu-id="f653f-130">Resource name</span></span>                                                          | <span data-ttu-id="f653f-131">必要</span><span class="sxs-lookup"><span data-stu-id="f653f-131">Required</span></span> | <span data-ttu-id="f653f-132">描述</span><span class="sxs-lookup"><span data-stu-id="f653f-132">Description</span></span>
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | <span data-ttu-id="f653f-133">是</span><span class="sxs-lookup"><span data-stu-id="f653f-133">yes</span></span>      | <span data-ttu-id="f653f-134">推入和刪除 （或 unlist） 封裝。</span><span class="sxs-lookup"><span data-stu-id="f653f-134">Push and delete (or unlist) packages.</span></span>
[`SearchQueryService`](search-query-service-resource.md)               | <span data-ttu-id="f653f-135">是</span><span class="sxs-lookup"><span data-stu-id="f653f-135">yes</span></span>      | <span data-ttu-id="f653f-136">篩選並依關鍵字搜尋的封裝。</span><span class="sxs-lookup"><span data-stu-id="f653f-136">Filter and search for packages by keyword.</span></span>
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | <span data-ttu-id="f653f-137">是</span><span class="sxs-lookup"><span data-stu-id="f653f-137">yes</span></span>      | <span data-ttu-id="f653f-138">取得封裝的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f653f-138">Get package metadata.</span></span>
[`PackageBaseAddress`](package-base-address-resource.md)               | <span data-ttu-id="f653f-139">是</span><span class="sxs-lookup"><span data-stu-id="f653f-139">yes</span></span>      | <span data-ttu-id="f653f-140">取得封裝的內容 (.nupkg)。</span><span class="sxs-lookup"><span data-stu-id="f653f-140">Get package content (.nupkg).</span></span>
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | <span data-ttu-id="f653f-141">否</span><span class="sxs-lookup"><span data-stu-id="f653f-141">no</span></span>       | <span data-ttu-id="f653f-142">探索的子字串的封裝識別碼和版本。</span><span class="sxs-lookup"><span data-stu-id="f653f-142">Discover package IDs and versions by substring.</span></span>
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | <span data-ttu-id="f653f-143">否</span><span class="sxs-lookup"><span data-stu-id="f653f-143">no</span></span>       | <span data-ttu-id="f653f-144">建構存取 「 檢舉不當使用 「 web 網頁的 URL。</span><span class="sxs-lookup"><span data-stu-id="f653f-144">Construct a URL to access a "report abuse" web page.</span></span>
[`Catalog`](catalog-resource.md)                                       | <span data-ttu-id="f653f-145">否</span><span class="sxs-lookup"><span data-stu-id="f653f-145">no</span></span>       | <span data-ttu-id="f653f-146">完整記錄的所有封裝事件。</span><span class="sxs-lookup"><span data-stu-id="f653f-146">Full record of all package events.</span></span>

<span data-ttu-id="f653f-147">一般情況下，應用程式開發介面資源所傳回的所有非二進位資料會使用 JSON 序列化的。</span><span class="sxs-lookup"><span data-stu-id="f653f-147">In general, all non-binary data returned by a API resource are serialized using JSON.</span></span> <span data-ttu-id="f653f-148">服務索引中每項資源所傳回的回應結構描述是個別定義該資源。</span><span class="sxs-lookup"><span data-stu-id="f653f-148">The response schema returned by each resource in the service index is defined individually for that resource.</span></span> <span data-ttu-id="f653f-149">如需有關每個資源的詳細資訊，請參閱上面所列的主題。</span><span class="sxs-lookup"><span data-stu-id="f653f-149">For more information about each resource, see the topics listed above.</span></span>

> [!Note]
> <span data-ttu-id="f653f-150">當來源未實作`SearchAutocompleteService`應該依正常程序停用任何自動完成行為。</span><span class="sxs-lookup"><span data-stu-id="f653f-150">When a source does not implement `SearchAutocompleteService` any autocomplete behavior should be disabled gracefully.</span></span> <span data-ttu-id="f653f-151">當`ReportAbuseUriTemplate`未實作，正式的 NuGet 用戶端會回到 nuget.org 的報表濫用的 URL (所追蹤[NuGet/首頁 #4924](https://github.com/NuGet/Home/issues/4924))。</span><span class="sxs-lookup"><span data-stu-id="f653f-151">When `ReportAbuseUriTemplate` is not implemented, the official NuGet client falls back to nuget.org's report abuse URL (tracked by [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)).</span></span> <span data-ttu-id="f653f-152">其他用戶端也可以選擇只要不向使用者顯示報表濫用的 URL。</span><span class="sxs-lookup"><span data-stu-id="f653f-152">Other clients may opt to simply not show a report abuse URL to the user.</span></span>

## <a name="timestamps"></a><span data-ttu-id="f653f-153">時間戳記</span><span class="sxs-lookup"><span data-stu-id="f653f-153">Timestamps</span></span>

<span data-ttu-id="f653f-154">所有 API 所傳回的時間戳記是 UTC，或未指定使用[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表示法。</span><span class="sxs-lookup"><span data-stu-id="f653f-154">All timestamps returned by the API are UTC or are otherwise specified using [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representation.</span></span> 

## <a name="http-methods"></a><span data-ttu-id="f653f-155">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="f653f-155">HTTP methods</span></span>

<span data-ttu-id="f653f-156">動詞命令</span><span class="sxs-lookup"><span data-stu-id="f653f-156">Verb</span></span>   | <span data-ttu-id="f653f-157">使用</span><span class="sxs-lookup"><span data-stu-id="f653f-157">Use</span></span>
------ | -----------
<span data-ttu-id="f653f-158">GET</span><span class="sxs-lookup"><span data-stu-id="f653f-158">GET</span></span>    | <span data-ttu-id="f653f-159">執行唯讀作業，通常擷取資料。</span><span class="sxs-lookup"><span data-stu-id="f653f-159">Performs a read-only operation, typically retrieving data.</span></span>
<span data-ttu-id="f653f-160">HEAD</span><span class="sxs-lookup"><span data-stu-id="f653f-160">HEAD</span></span>   | <span data-ttu-id="f653f-161">擷取對應的回應標頭`GET`要求。</span><span class="sxs-lookup"><span data-stu-id="f653f-161">Fetches the response headers for the corresponding `GET` request.</span></span>
<span data-ttu-id="f653f-162">PUT</span><span class="sxs-lookup"><span data-stu-id="f653f-162">PUT</span></span>    | <span data-ttu-id="f653f-163">建立不存在，或如果檔案存在，會更新它的資源。</span><span class="sxs-lookup"><span data-stu-id="f653f-163">Creates a resource that doesn't exist or, if it does exist, updates it.</span></span> <span data-ttu-id="f653f-164">有些資源可能不支援更新。</span><span class="sxs-lookup"><span data-stu-id="f653f-164">Some resources may not support update.</span></span>
<span data-ttu-id="f653f-165">DELETE</span><span class="sxs-lookup"><span data-stu-id="f653f-165">DELETE</span></span> | <span data-ttu-id="f653f-166">刪除或 unlists 資源。</span><span class="sxs-lookup"><span data-stu-id="f653f-166">Deletes or unlists a resource.</span></span>

## <a name="http-status-codes"></a><span data-ttu-id="f653f-167">HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="f653f-167">HTTP status codes</span></span>

<span data-ttu-id="f653f-168">程式碼</span><span class="sxs-lookup"><span data-stu-id="f653f-168">Code</span></span> | <span data-ttu-id="f653f-169">描述</span><span class="sxs-lookup"><span data-stu-id="f653f-169">Description</span></span>
---- | -----
<span data-ttu-id="f653f-170">200</span><span class="sxs-lookup"><span data-stu-id="f653f-170">200</span></span>  | <span data-ttu-id="f653f-171">如果成功，而且沒有回應主體。</span><span class="sxs-lookup"><span data-stu-id="f653f-171">Success, and there is a response body.</span></span>
<span data-ttu-id="f653f-172">201</span><span class="sxs-lookup"><span data-stu-id="f653f-172">201</span></span>  | <span data-ttu-id="f653f-173">已建立成功時，與資源。</span><span class="sxs-lookup"><span data-stu-id="f653f-173">Success, and the resource was created.</span></span>
<span data-ttu-id="f653f-174">202</span><span class="sxs-lookup"><span data-stu-id="f653f-174">202</span></span>  | <span data-ttu-id="f653f-175">成功時，要求已接受，但是某些工作可能仍然會在不完整而且已完成以非同步的方式。</span><span class="sxs-lookup"><span data-stu-id="f653f-175">Success, the request has been accepted but some work may still be incomplete and completed asynchronously.</span></span>
<span data-ttu-id="f653f-176">204</span><span class="sxs-lookup"><span data-stu-id="f653f-176">204</span></span>  | <span data-ttu-id="f653f-177">如果成功，但不會有回應主體。</span><span class="sxs-lookup"><span data-stu-id="f653f-177">Success, but there is no response body.</span></span>
<span data-ttu-id="f653f-178">301</span><span class="sxs-lookup"><span data-stu-id="f653f-178">301</span></span>  | <span data-ttu-id="f653f-179">永久重新導向。</span><span class="sxs-lookup"><span data-stu-id="f653f-179">A permanent redirect.</span></span>
<span data-ttu-id="f653f-180">302</span><span class="sxs-lookup"><span data-stu-id="f653f-180">302</span></span>  | <span data-ttu-id="f653f-181">暫時重新導向。</span><span class="sxs-lookup"><span data-stu-id="f653f-181">A temporary redirect.</span></span>
<span data-ttu-id="f653f-182">400</span><span class="sxs-lookup"><span data-stu-id="f653f-182">400</span></span>  | <span data-ttu-id="f653f-183">在 URL 或要求主體中的參數不是有效的。</span><span class="sxs-lookup"><span data-stu-id="f653f-183">The parameters in the URL or in the request body aren't valid.</span></span>
<span data-ttu-id="f653f-184">401</span><span class="sxs-lookup"><span data-stu-id="f653f-184">401</span></span>  | <span data-ttu-id="f653f-185">提供的認證不正確。</span><span class="sxs-lookup"><span data-stu-id="f653f-185">The provided credentials are invalid.</span></span>
<span data-ttu-id="f653f-186">403</span><span class="sxs-lookup"><span data-stu-id="f653f-186">403</span></span>  | <span data-ttu-id="f653f-187">此動作不允許指定所提供的認證。</span><span class="sxs-lookup"><span data-stu-id="f653f-187">The action is not allowed given the provided credentials.</span></span>
<span data-ttu-id="f653f-188">404</span><span class="sxs-lookup"><span data-stu-id="f653f-188">404</span></span>  | <span data-ttu-id="f653f-189">要求的資源不存在。</span><span class="sxs-lookup"><span data-stu-id="f653f-189">The requested resource doesn't exist.</span></span>
<span data-ttu-id="f653f-190">409</span><span class="sxs-lookup"><span data-stu-id="f653f-190">409</span></span>  | <span data-ttu-id="f653f-191">與現有資源的要求衝突。</span><span class="sxs-lookup"><span data-stu-id="f653f-191">The request conflicts with an existing resource.</span></span>
<span data-ttu-id="f653f-192">500</span><span class="sxs-lookup"><span data-stu-id="f653f-192">500</span></span>  | <span data-ttu-id="f653f-193">服務發生未預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f653f-193">The service has encountered an unexpected error.</span></span>
<span data-ttu-id="f653f-194">503</span><span class="sxs-lookup"><span data-stu-id="f653f-194">503</span></span>  | <span data-ttu-id="f653f-195">此服務暫時無法使用。</span><span class="sxs-lookup"><span data-stu-id="f653f-195">The service is temporarily unavailable.</span></span>

<span data-ttu-id="f653f-196">任何`GET`對 API 端點的要求可能會傳回 HTTP 重新導向 （301 或 302）。</span><span class="sxs-lookup"><span data-stu-id="f653f-196">Any `GET` request made to a API endpoint may return an HTTP redirect (301 or 302).</span></span> <span data-ttu-id="f653f-197">用戶端應妥善處理這類的重新導向觀察`Location`標頭和後續發出`GET`。</span><span class="sxs-lookup"><span data-stu-id="f653f-197">Clients should gracefully handle such redirects by observing the `Location` header and issueing a subsequent `GET`.</span></span> <span data-ttu-id="f653f-198">關於特定端點的文件不會明確呼叫時可能會使用重新導向。</span><span class="sxs-lookup"><span data-stu-id="f653f-198">Documentation concerning specific endpoints will not explicitly call out where redirects may be used.</span></span>

<span data-ttu-id="f653f-199">在 500 層級狀態程式碼中，用戶端可以實作合理的重試機制。</span><span class="sxs-lookup"><span data-stu-id="f653f-199">In the case of a 500-level status code, the client can implement a reasonable retry mechanism.</span></span> <span data-ttu-id="f653f-200">官方 NuGet 用戶端重試三次時遇到任何 500 層級狀態程式碼或 TCP/DNS 錯誤。</span><span class="sxs-lookup"><span data-stu-id="f653f-200">The official NuGet client retries three times when encountering any 500-level status code or TCP/DNS error.</span></span>

## <a name="http-request-headers"></a><span data-ttu-id="f653f-201">HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="f653f-201">HTTP request headers</span></span>

<span data-ttu-id="f653f-202">名稱</span><span class="sxs-lookup"><span data-stu-id="f653f-202">Name</span></span>                     | <span data-ttu-id="f653f-203">描述</span><span class="sxs-lookup"><span data-stu-id="f653f-203">Description</span></span>
------------------------ | -----------
<span data-ttu-id="f653f-204">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="f653f-204">X-NuGet-ApiKey</span></span>           | <span data-ttu-id="f653f-205">所需推入和刪除，請參閱[`PackagePublish`資源](package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="f653f-205">Required for push and delete, see [`PackagePublish` resource](package-publish-resource.md)</span></span>
<span data-ttu-id="f653f-206">X-NuGet-Client-Version</span><span class="sxs-lookup"><span data-stu-id="f653f-206">X-NuGet-Client-Version</span></span>   | <span data-ttu-id="f653f-207">**已被取代**而被取代`X-NuGet-Protocol-Version`</span><span class="sxs-lookup"><span data-stu-id="f653f-207">**Deprecated** and replaced by `X-NuGet-Protocol-Version`</span></span>
<span data-ttu-id="f653f-208">X-NuGet-Protocol-Version</span><span class="sxs-lookup"><span data-stu-id="f653f-208">X-NuGet-Protocol-Version</span></span> | <span data-ttu-id="f653f-209">在某些情況下，只在 nuget.org 的需要，請參閱[nuget.org 通訊協定](NuGet-Protocols.md)</span><span class="sxs-lookup"><span data-stu-id="f653f-209">Required in certain cases only on nuget.org, see [nuget.org protocols](NuGet-Protocols.md)</span></span>

## <a name="authentication"></a><span data-ttu-id="f653f-210">驗證</span><span class="sxs-lookup"><span data-stu-id="f653f-210">Authentication</span></span>

<span data-ttu-id="f653f-211">驗證會保持最多要定義的封裝來源實作。</span><span class="sxs-lookup"><span data-stu-id="f653f-211">Authentication is left up to the package source implementation to define.</span></span> <span data-ttu-id="f653f-212">只有 nuget.org 的`PackagePublish`的資源需要驗證，透過特殊的 API 金鑰標頭。</span><span class="sxs-lookup"><span data-stu-id="f653f-212">For nuget.org, only the `PackagePublish` resource requires authentication via a special API key header.</span></span> <span data-ttu-id="f653f-213">請參閱[`PackagePublish`資源](package-publish-resource.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f653f-213">See [`PackagePublish` resource](package-publish-resource.md) for details.</span></span>
