---
title: 自動完成，NuGet API
description: 搜尋 「 自動完成 」 服務支援互動式尋找的封裝識別碼和版本。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="autocomplete"></a><span data-ttu-id="0cd87-103">自動完成</span><span class="sxs-lookup"><span data-stu-id="0cd87-103">Autocomplete</span></span>

<span data-ttu-id="0cd87-104">它是可以建置的套件識別碼和版本自動完成體驗使用 V3 API。</span><span class="sxs-lookup"><span data-stu-id="0cd87-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="0cd87-105">自動完成查詢所使用之資源是`SearchAutocompleteService`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="0cd87-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="0cd87-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="0cd87-106">Versioning</span></span>

<span data-ttu-id="0cd87-107">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="0cd87-107">The following `@type` values are used:</span></span>

<span data-ttu-id="0cd87-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="0cd87-108">@type value</span></span>                          | <span data-ttu-id="0cd87-109">注意</span><span class="sxs-lookup"><span data-stu-id="0cd87-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="0cd87-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="0cd87-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="0cd87-111">初版</span><span class="sxs-lookup"><span data-stu-id="0cd87-111">The initial release</span></span>
<span data-ttu-id="0cd87-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="0cd87-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="0cd87-113">別名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="0cd87-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="0cd87-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="0cd87-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="0cd87-115">別名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="0cd87-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="0cd87-116">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-116">Base URL</span></span>

<span data-ttu-id="0cd87-117">下列應用程式開發介面的基底 URL 是值`@id`與其中一個先前提及的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="0cd87-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="0cd87-118">下列文件預留位置基底 URL`{@id}`將使用。</span><span class="sxs-lookup"><span data-stu-id="0cd87-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0cd87-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0cd87-119">HTTP Methods</span></span>

<span data-ttu-id="0cd87-120">位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="0cd87-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="0cd87-121">搜尋封裝 Id</span><span class="sxs-lookup"><span data-stu-id="0cd87-121">Search for package IDs</span></span>

<span data-ttu-id="0cd87-122">第一個自動完成應用程式開發介面支援搜尋的套件 ID 字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="0cd87-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="0cd87-123">當您想要提供使用者介面整合在一起的 NuGet 封裝來源中的封裝 typeahead 功能時，這很適合。</span><span class="sxs-lookup"><span data-stu-id="0cd87-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="0cd87-124">只有未列出的版本的封裝不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="0cd87-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="0cd87-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="0cd87-125">Request parameters</span></span>

<span data-ttu-id="0cd87-126">名稱</span><span class="sxs-lookup"><span data-stu-id="0cd87-126">Name</span></span>        | <span data-ttu-id="0cd87-127">In</span><span class="sxs-lookup"><span data-stu-id="0cd87-127">In</span></span>     | <span data-ttu-id="0cd87-128">類型</span><span class="sxs-lookup"><span data-stu-id="0cd87-128">Type</span></span>    | <span data-ttu-id="0cd87-129">必要</span><span class="sxs-lookup"><span data-stu-id="0cd87-129">Required</span></span> | <span data-ttu-id="0cd87-130">注意</span><span class="sxs-lookup"><span data-stu-id="0cd87-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="0cd87-131">q</span><span class="sxs-lookup"><span data-stu-id="0cd87-131">q</span></span>           | <span data-ttu-id="0cd87-132">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-132">URL</span></span>    | <span data-ttu-id="0cd87-133">字串</span><span class="sxs-lookup"><span data-stu-id="0cd87-133">string</span></span>  | <span data-ttu-id="0cd87-134">否</span><span class="sxs-lookup"><span data-stu-id="0cd87-134">no</span></span>       | <span data-ttu-id="0cd87-135">要與封裝識別碼進行比較的字串</span><span class="sxs-lookup"><span data-stu-id="0cd87-135">The string to compare against package IDs</span></span>
<span data-ttu-id="0cd87-136">skip</span><span class="sxs-lookup"><span data-stu-id="0cd87-136">skip</span></span>        | <span data-ttu-id="0cd87-137">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-137">URL</span></span>    | <span data-ttu-id="0cd87-138">整數</span><span class="sxs-lookup"><span data-stu-id="0cd87-138">integer</span></span> | <span data-ttu-id="0cd87-139">否</span><span class="sxs-lookup"><span data-stu-id="0cd87-139">no</span></span>       | <span data-ttu-id="0cd87-140">若要略過，針對分頁的結果數目</span><span class="sxs-lookup"><span data-stu-id="0cd87-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="0cd87-141">take</span><span class="sxs-lookup"><span data-stu-id="0cd87-141">take</span></span>        | <span data-ttu-id="0cd87-142">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-142">URL</span></span>    | <span data-ttu-id="0cd87-143">整數</span><span class="sxs-lookup"><span data-stu-id="0cd87-143">integer</span></span> | <span data-ttu-id="0cd87-144">否</span><span class="sxs-lookup"><span data-stu-id="0cd87-144">no</span></span>       | <span data-ttu-id="0cd87-145">若要傳回，針對分頁的結果數目</span><span class="sxs-lookup"><span data-stu-id="0cd87-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="0cd87-146">發行前版本</span><span class="sxs-lookup"><span data-stu-id="0cd87-146">prerelease</span></span>  | <span data-ttu-id="0cd87-147">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-147">URL</span></span>    | <span data-ttu-id="0cd87-148">boolean</span><span class="sxs-lookup"><span data-stu-id="0cd87-148">boolean</span></span> | <span data-ttu-id="0cd87-149">否</span><span class="sxs-lookup"><span data-stu-id="0cd87-149">no</span></span>       | <span data-ttu-id="0cd87-150">`true` 或`false`決定是否要包含[發行前版本的封裝](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="0cd87-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="0cd87-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="0cd87-151">semVerLevel</span></span> | <span data-ttu-id="0cd87-152">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-152">URL</span></span>    | <span data-ttu-id="0cd87-153">字串</span><span class="sxs-lookup"><span data-stu-id="0cd87-153">string</span></span>  | <span data-ttu-id="0cd87-154">否</span><span class="sxs-lookup"><span data-stu-id="0cd87-154">no</span></span>       | <span data-ttu-id="0cd87-155">SemVer 1.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="0cd87-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="0cd87-156">自動完成查詢`q`剖析的方式，由伺服器實作所定義。</span><span class="sxs-lookup"><span data-stu-id="0cd87-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="0cd87-157">nuget.org 支援來查詢前置詞的封裝識別碼權杖是片段 spliting 所產生的識別碼，原始的 camel 命名法的大小寫和符號字元。</span><span class="sxs-lookup"><span data-stu-id="0cd87-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="0cd87-158">`skip`參數預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="0cd87-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="0cd87-159">`take`參數應該大於零的整數。</span><span class="sxs-lookup"><span data-stu-id="0cd87-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="0cd87-160">伺服器實作可能會造成最大值。</span><span class="sxs-lookup"><span data-stu-id="0cd87-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="0cd87-161">如果`prerelease`未提供，會排除發行前版本的封裝。</span><span class="sxs-lookup"><span data-stu-id="0cd87-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="0cd87-162">`semVerLevel`查詢參數用來選擇加入以[SemVer 2.0.0 封裝](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="0cd87-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="0cd87-163">如果此查詢參數被排除後，將會傳回與 SemVer 1.0.0 相容版本的唯一封裝識別碼 (與[標準的 NuGet 版本控制](../reference/package-versioning.md)警告，例如 4 整數片段具有的版本字串)。</span><span class="sxs-lookup"><span data-stu-id="0cd87-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="0cd87-164">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 相容封裝將會傳回。</span><span class="sxs-lookup"><span data-stu-id="0cd87-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="0cd87-165">請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0cd87-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="0cd87-166">回應</span><span class="sxs-lookup"><span data-stu-id="0cd87-166">Response</span></span>

<span data-ttu-id="0cd87-167">回應是含有最多的 JSON 文件`take`自動完成的結果。</span><span class="sxs-lookup"><span data-stu-id="0cd87-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="0cd87-168">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0cd87-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="0cd87-169">名稱</span><span class="sxs-lookup"><span data-stu-id="0cd87-169">Name</span></span>      | <span data-ttu-id="0cd87-170">類型</span><span class="sxs-lookup"><span data-stu-id="0cd87-170">Type</span></span>             | <span data-ttu-id="0cd87-171">必要</span><span class="sxs-lookup"><span data-stu-id="0cd87-171">Required</span></span> | <span data-ttu-id="0cd87-172">注意</span><span class="sxs-lookup"><span data-stu-id="0cd87-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="0cd87-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="0cd87-173">totalHits</span></span> | <span data-ttu-id="0cd87-174">整數</span><span class="sxs-lookup"><span data-stu-id="0cd87-174">integer</span></span>          | <span data-ttu-id="0cd87-175">是</span><span class="sxs-lookup"><span data-stu-id="0cd87-175">yes</span></span>      | <span data-ttu-id="0cd87-176">總數的比對，正在略過`skip`和 `take`</span><span class="sxs-lookup"><span data-stu-id="0cd87-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="0cd87-177">資料</span><span class="sxs-lookup"><span data-stu-id="0cd87-177">data</span></span>      | <span data-ttu-id="0cd87-178">字串陣列</span><span class="sxs-lookup"><span data-stu-id="0cd87-178">array of strings</span></span> | <span data-ttu-id="0cd87-179">是</span><span class="sxs-lookup"><span data-stu-id="0cd87-179">yes</span></span>      | <span data-ttu-id="0cd87-180">封裝符合所要求的識別碼</span><span class="sxs-lookup"><span data-stu-id="0cd87-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="0cd87-181">範例要求</span><span class="sxs-lookup"><span data-stu-id="0cd87-181">Sample request</span></span>

<span data-ttu-id="0cd87-182">取得 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="0cd87-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="0cd87-183">範例回應</span><span class="sxs-lookup"><span data-stu-id="0cd87-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="0cd87-184">列舉封裝版本</span><span class="sxs-lookup"><span data-stu-id="0cd87-184">Enumerate package versions</span></span>

<span data-ttu-id="0cd87-185">一旦找到套件識別碼使用先前的應用程式開發介面，用戶端可以使用自動完成應用程式開發介面來列舉封裝版本提供的封裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="0cd87-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="0cd87-186">未列出的套件版本不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="0cd87-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="0cd87-187">要求參數</span><span class="sxs-lookup"><span data-stu-id="0cd87-187">Request parameters</span></span>

<span data-ttu-id="0cd87-188">名稱</span><span class="sxs-lookup"><span data-stu-id="0cd87-188">Name</span></span>        | <span data-ttu-id="0cd87-189">In</span><span class="sxs-lookup"><span data-stu-id="0cd87-189">In</span></span>     | <span data-ttu-id="0cd87-190">類型</span><span class="sxs-lookup"><span data-stu-id="0cd87-190">Type</span></span>    | <span data-ttu-id="0cd87-191">必要</span><span class="sxs-lookup"><span data-stu-id="0cd87-191">Required</span></span> | <span data-ttu-id="0cd87-192">注意</span><span class="sxs-lookup"><span data-stu-id="0cd87-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="0cd87-193">id</span><span class="sxs-lookup"><span data-stu-id="0cd87-193">id</span></span>          | <span data-ttu-id="0cd87-194">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-194">URL</span></span>    | <span data-ttu-id="0cd87-195">字串</span><span class="sxs-lookup"><span data-stu-id="0cd87-195">string</span></span>  | <span data-ttu-id="0cd87-196">是</span><span class="sxs-lookup"><span data-stu-id="0cd87-196">yes</span></span>      | <span data-ttu-id="0cd87-197">要擷取的版本的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="0cd87-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="0cd87-198">發行前版本</span><span class="sxs-lookup"><span data-stu-id="0cd87-198">prerelease</span></span>  | <span data-ttu-id="0cd87-199">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-199">URL</span></span>    | <span data-ttu-id="0cd87-200">boolean</span><span class="sxs-lookup"><span data-stu-id="0cd87-200">boolean</span></span> | <span data-ttu-id="0cd87-201">否</span><span class="sxs-lookup"><span data-stu-id="0cd87-201">no</span></span>       | <span data-ttu-id="0cd87-202">`true` 或`false`決定是否要包含[發行前版本的封裝](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="0cd87-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="0cd87-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="0cd87-203">semVerLevel</span></span> | <span data-ttu-id="0cd87-204">URL</span><span class="sxs-lookup"><span data-stu-id="0cd87-204">URL</span></span>    | <span data-ttu-id="0cd87-205">字串</span><span class="sxs-lookup"><span data-stu-id="0cd87-205">string</span></span>  | <span data-ttu-id="0cd87-206">否</span><span class="sxs-lookup"><span data-stu-id="0cd87-206">no</span></span>       | <span data-ttu-id="0cd87-207">SemVer 2.0.0 的版本字串</span><span class="sxs-lookup"><span data-stu-id="0cd87-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="0cd87-208">如果`prerelease`未提供，會排除發行前版本的封裝。</span><span class="sxs-lookup"><span data-stu-id="0cd87-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="0cd87-209">`semVerLevel`查詢參數用來選擇加入以 SemVer 2.0.0 的封裝。</span><span class="sxs-lookup"><span data-stu-id="0cd87-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="0cd87-210">如果此查詢參數被排除後，將會傳回只 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="0cd87-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="0cd87-211">如果`semVerLevel=2.0.0`提供，將傳回 SemVer 1.0.0 和 SemVer 2.0.0 的版本。</span><span class="sxs-lookup"><span data-stu-id="0cd87-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="0cd87-212">請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0cd87-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="0cd87-213">回應</span><span class="sxs-lookup"><span data-stu-id="0cd87-213">Response</span></span>

<span data-ttu-id="0cd87-214">回應是包含所有的篩選指定的查詢參數所提供的封裝識別碼的封裝版本的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="0cd87-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="0cd87-215">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0cd87-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="0cd87-216">名稱</span><span class="sxs-lookup"><span data-stu-id="0cd87-216">Name</span></span>      | <span data-ttu-id="0cd87-217">類型</span><span class="sxs-lookup"><span data-stu-id="0cd87-217">Type</span></span>             | <span data-ttu-id="0cd87-218">必要</span><span class="sxs-lookup"><span data-stu-id="0cd87-218">Required</span></span> | <span data-ttu-id="0cd87-219">注意</span><span class="sxs-lookup"><span data-stu-id="0cd87-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="0cd87-220">資料</span><span class="sxs-lookup"><span data-stu-id="0cd87-220">data</span></span>      | <span data-ttu-id="0cd87-221">字串陣列</span><span class="sxs-lookup"><span data-stu-id="0cd87-221">array of strings</span></span> | <span data-ttu-id="0cd87-222">是</span><span class="sxs-lookup"><span data-stu-id="0cd87-222">yes</span></span>      | <span data-ttu-id="0cd87-223">封裝版本要求所比對</span><span class="sxs-lookup"><span data-stu-id="0cd87-223">The package versions matched by the request</span></span>

<span data-ttu-id="0cd87-224">中的封裝版本`data`陣列可能包含 SemVer 2.0.0 建置中繼資料 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查詢字串中提供。</span><span class="sxs-lookup"><span data-stu-id="0cd87-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0cd87-225">範例要求</span><span class="sxs-lookup"><span data-stu-id="0cd87-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="0cd87-226">範例回應</span><span class="sxs-lookup"><span data-stu-id="0cd87-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
