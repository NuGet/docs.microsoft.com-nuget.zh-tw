---
title: 自動完成, NuGet API
description: 搜尋自動完成服務支援對套件識別碼和版本進行互動式探索。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488298"
---
# <a name="autocomplete"></a><span data-ttu-id="d427d-103">自動完成</span><span class="sxs-lookup"><span data-stu-id="d427d-103">Autocomplete</span></span>

<span data-ttu-id="d427d-104">您可以使用 V3 API 來建立套件識別碼和版本自動完成體驗。</span><span class="sxs-lookup"><span data-stu-id="d427d-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d427d-105">用來進行自動完成查詢的資源是`SearchAutocompleteService`在[服務索引](service-index.md)中找到的資源。</span><span class="sxs-lookup"><span data-stu-id="d427d-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d427d-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="d427d-106">Versioning</span></span>

<span data-ttu-id="d427d-107">會使用`@type`下列值:</span><span class="sxs-lookup"><span data-stu-id="d427d-107">The following `@type` values are used:</span></span>

<span data-ttu-id="d427d-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="d427d-108">@type value</span></span>                          | <span data-ttu-id="d427d-109">注意</span><span class="sxs-lookup"><span data-stu-id="d427d-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d427d-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d427d-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="d427d-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="d427d-111">The initial release</span></span>
<span data-ttu-id="d427d-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d427d-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d427d-113">別名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d427d-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d427d-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d427d-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d427d-115">別名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d427d-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="d427d-116">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="d427d-116">Base URL</span></span>

<span data-ttu-id="d427d-117">下列 api 的基底 URL 是與上述其中一個資源`@id` `@type`值相關聯的屬性值。</span><span class="sxs-lookup"><span data-stu-id="d427d-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d427d-118">在下列檔中, 將會使用預留位置`{@id}`基底 URL。</span><span class="sxs-lookup"><span data-stu-id="d427d-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d427d-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="d427d-119">HTTP Methods</span></span>

<span data-ttu-id="d427d-120">在註冊資源中找到的所有 url 都支援 HTTP `GET`方法`HEAD`和。</span><span class="sxs-lookup"><span data-stu-id="d427d-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d427d-121">搜尋套件識別碼</span><span class="sxs-lookup"><span data-stu-id="d427d-121">Search for package IDs</span></span>

<span data-ttu-id="d427d-122">第一個自動完成 API 支援搜尋封裝識別碼字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="d427d-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d427d-123">當您想要在與 NuGet 套件來源整合的使用者介面中提供封裝自動提示功能時, 這是很好的選擇。</span><span class="sxs-lookup"><span data-stu-id="d427d-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d427d-124">只有未列出版本的套件不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="d427d-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d427d-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="d427d-125">Request parameters</span></span>

<span data-ttu-id="d427d-126">名稱</span><span class="sxs-lookup"><span data-stu-id="d427d-126">Name</span></span>        | <span data-ttu-id="d427d-127">In</span><span class="sxs-lookup"><span data-stu-id="d427d-127">In</span></span>     | <span data-ttu-id="d427d-128">類型</span><span class="sxs-lookup"><span data-stu-id="d427d-128">Type</span></span>    | <span data-ttu-id="d427d-129">必要</span><span class="sxs-lookup"><span data-stu-id="d427d-129">Required</span></span> | <span data-ttu-id="d427d-130">附註</span><span class="sxs-lookup"><span data-stu-id="d427d-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d427d-131">q</span><span class="sxs-lookup"><span data-stu-id="d427d-131">q</span></span>           | <span data-ttu-id="d427d-132">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-132">URL</span></span>    | <span data-ttu-id="d427d-133">字串</span><span class="sxs-lookup"><span data-stu-id="d427d-133">string</span></span>  | <span data-ttu-id="d427d-134">否</span><span class="sxs-lookup"><span data-stu-id="d427d-134">no</span></span>       | <span data-ttu-id="d427d-135">要與套件識別碼比較的字串</span><span class="sxs-lookup"><span data-stu-id="d427d-135">The string to compare against package IDs</span></span>
<span data-ttu-id="d427d-136">skip</span><span class="sxs-lookup"><span data-stu-id="d427d-136">skip</span></span>        | <span data-ttu-id="d427d-137">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-137">URL</span></span>    | <span data-ttu-id="d427d-138">integer</span><span class="sxs-lookup"><span data-stu-id="d427d-138">integer</span></span> | <span data-ttu-id="d427d-139">否</span><span class="sxs-lookup"><span data-stu-id="d427d-139">no</span></span>       | <span data-ttu-id="d427d-140">要略過的結果數目, 用於分頁</span><span class="sxs-lookup"><span data-stu-id="d427d-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d427d-141">採取</span><span class="sxs-lookup"><span data-stu-id="d427d-141">take</span></span>        | <span data-ttu-id="d427d-142">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-142">URL</span></span>    | <span data-ttu-id="d427d-143">integer</span><span class="sxs-lookup"><span data-stu-id="d427d-143">integer</span></span> | <span data-ttu-id="d427d-144">否</span><span class="sxs-lookup"><span data-stu-id="d427d-144">no</span></span>       | <span data-ttu-id="d427d-145">要傳回的結果數目, 用於分頁</span><span class="sxs-lookup"><span data-stu-id="d427d-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="d427d-146">版</span><span class="sxs-lookup"><span data-stu-id="d427d-146">prerelease</span></span>  | <span data-ttu-id="d427d-147">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-147">URL</span></span>    | <span data-ttu-id="d427d-148">boolean</span><span class="sxs-lookup"><span data-stu-id="d427d-148">boolean</span></span> | <span data-ttu-id="d427d-149">否</span><span class="sxs-lookup"><span data-stu-id="d427d-149">no</span></span>       | <span data-ttu-id="d427d-150">`true`或`false`判斷是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d427d-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d427d-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d427d-151">semVerLevel</span></span> | <span data-ttu-id="d427d-152">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-152">URL</span></span>    | <span data-ttu-id="d427d-153">字串</span><span class="sxs-lookup"><span data-stu-id="d427d-153">string</span></span>  | <span data-ttu-id="d427d-154">否</span><span class="sxs-lookup"><span data-stu-id="d427d-154">no</span></span>       | <span data-ttu-id="d427d-155">SemVer 1.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="d427d-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d427d-156">自動完成查詢`q`會以伺服器實作為定義的方式進行剖析。</span><span class="sxs-lookup"><span data-stu-id="d427d-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d427d-157">nuget.org 支援查詢套件識別碼權杖的前置詞, 這是由 spliting 原始 by camel 大小寫和符號字元所產生的識別碼片段。</span><span class="sxs-lookup"><span data-stu-id="d427d-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d427d-158">參數`skip`的預設值為0。</span><span class="sxs-lookup"><span data-stu-id="d427d-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d427d-159">`take`參數應該是大於零的整數。</span><span class="sxs-lookup"><span data-stu-id="d427d-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d427d-160">伺服器的執行可能會強加最大值。</span><span class="sxs-lookup"><span data-stu-id="d427d-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d427d-161">如果`prerelease`未提供, 則會排除發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="d427d-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d427d-162">查詢參數是用來加入[SemVer 2.0.0 套件。](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`</span><span class="sxs-lookup"><span data-stu-id="d427d-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d427d-163">如果排除此查詢參數, 則只會傳回具有 SemVer 1.0.0 相容版本的套件識別碼 (使用[標準 NuGet 版本](../concepts/package-versioning.md)設定注意事項, 例如具有4個整數部分的版本字串)。</span><span class="sxs-lookup"><span data-stu-id="d427d-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d427d-164">如果`semVerLevel=2.0.0`提供, 則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容的套件。</span><span class="sxs-lookup"><span data-stu-id="d427d-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d427d-165">如需詳細資訊, 請參閱[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="d427d-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d427d-166">回應</span><span class="sxs-lookup"><span data-stu-id="d427d-166">Response</span></span>

<span data-ttu-id="d427d-167">回應是包含最多`take`自動完成結果的 JSON 檔。</span><span class="sxs-lookup"><span data-stu-id="d427d-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d427d-168">根 JSON 物件具有下列屬性:</span><span class="sxs-lookup"><span data-stu-id="d427d-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d427d-169">名稱</span><span class="sxs-lookup"><span data-stu-id="d427d-169">Name</span></span>      | <span data-ttu-id="d427d-170">類型</span><span class="sxs-lookup"><span data-stu-id="d427d-170">Type</span></span>             | <span data-ttu-id="d427d-171">必要</span><span class="sxs-lookup"><span data-stu-id="d427d-171">Required</span></span> | <span data-ttu-id="d427d-172">注意</span><span class="sxs-lookup"><span data-stu-id="d427d-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d427d-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="d427d-173">totalHits</span></span> | <span data-ttu-id="d427d-174">integer</span><span class="sxs-lookup"><span data-stu-id="d427d-174">integer</span></span>          | <span data-ttu-id="d427d-175">是</span><span class="sxs-lookup"><span data-stu-id="d427d-175">yes</span></span>      | <span data-ttu-id="d427d-176">相符專案總數, `skip`忽略和`take`</span><span class="sxs-lookup"><span data-stu-id="d427d-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d427d-177">資料</span><span class="sxs-lookup"><span data-stu-id="d427d-177">data</span></span>      | <span data-ttu-id="d427d-178">字串陣列</span><span class="sxs-lookup"><span data-stu-id="d427d-178">array of strings</span></span> | <span data-ttu-id="d427d-179">是</span><span class="sxs-lookup"><span data-stu-id="d427d-179">yes</span></span>      | <span data-ttu-id="d427d-180">要求所符合的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="d427d-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d427d-181">範例要求</span><span class="sxs-lookup"><span data-stu-id="d427d-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d427d-182">範例回應</span><span class="sxs-lookup"><span data-stu-id="d427d-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d427d-183">列舉封裝版本</span><span class="sxs-lookup"><span data-stu-id="d427d-183">Enumerate package versions</span></span>

<span data-ttu-id="d427d-184">一旦使用先前的 API 探索到套件識別碼之後, 用戶端就可以使用自動完成 API 來列舉所提供封裝識別碼的套件版本。</span><span class="sxs-lookup"><span data-stu-id="d427d-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d427d-185">未列出的封裝版本不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="d427d-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d427d-186">要求參數</span><span class="sxs-lookup"><span data-stu-id="d427d-186">Request parameters</span></span>

<span data-ttu-id="d427d-187">名稱</span><span class="sxs-lookup"><span data-stu-id="d427d-187">Name</span></span>        | <span data-ttu-id="d427d-188">In</span><span class="sxs-lookup"><span data-stu-id="d427d-188">In</span></span>     | <span data-ttu-id="d427d-189">類型</span><span class="sxs-lookup"><span data-stu-id="d427d-189">Type</span></span>    | <span data-ttu-id="d427d-190">必要</span><span class="sxs-lookup"><span data-stu-id="d427d-190">Required</span></span> | <span data-ttu-id="d427d-191">附註</span><span class="sxs-lookup"><span data-stu-id="d427d-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d427d-192">id</span><span class="sxs-lookup"><span data-stu-id="d427d-192">id</span></span>          | <span data-ttu-id="d427d-193">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-193">URL</span></span>    | <span data-ttu-id="d427d-194">字串</span><span class="sxs-lookup"><span data-stu-id="d427d-194">string</span></span>  | <span data-ttu-id="d427d-195">是</span><span class="sxs-lookup"><span data-stu-id="d427d-195">yes</span></span>      | <span data-ttu-id="d427d-196">要為其提取版本的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="d427d-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="d427d-197">版</span><span class="sxs-lookup"><span data-stu-id="d427d-197">prerelease</span></span>  | <span data-ttu-id="d427d-198">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-198">URL</span></span>    | <span data-ttu-id="d427d-199">boolean</span><span class="sxs-lookup"><span data-stu-id="d427d-199">boolean</span></span> | <span data-ttu-id="d427d-200">否</span><span class="sxs-lookup"><span data-stu-id="d427d-200">no</span></span>       | <span data-ttu-id="d427d-201">`true`或`false`判斷是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d427d-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d427d-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d427d-202">semVerLevel</span></span> | <span data-ttu-id="d427d-203">URL</span><span class="sxs-lookup"><span data-stu-id="d427d-203">URL</span></span>    | <span data-ttu-id="d427d-204">字串</span><span class="sxs-lookup"><span data-stu-id="d427d-204">string</span></span>  | <span data-ttu-id="d427d-205">否</span><span class="sxs-lookup"><span data-stu-id="d427d-205">no</span></span>       | <span data-ttu-id="d427d-206">SemVer 2.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="d427d-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d427d-207">如果`prerelease`未提供, 則會排除發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="d427d-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d427d-208">`semVerLevel`查詢參數是用來加入 SemVer 2.0.0 套件。</span><span class="sxs-lookup"><span data-stu-id="d427d-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d427d-209">如果排除此查詢參數, 則只會傳回 SemVer 1.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="d427d-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d427d-210">如果`semVerLevel=2.0.0`提供, 則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="d427d-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d427d-211">如需詳細資訊, 請參閱[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="d427d-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d427d-212">回應</span><span class="sxs-lookup"><span data-stu-id="d427d-212">Response</span></span>

<span data-ttu-id="d427d-213">回應是 JSON 檔, 其中包含所提供封裝識別碼的所有封裝版本, 並依指定的查詢參數進行篩選。</span><span class="sxs-lookup"><span data-stu-id="d427d-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d427d-214">根 JSON 物件具有下列屬性:</span><span class="sxs-lookup"><span data-stu-id="d427d-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="d427d-215">名稱</span><span class="sxs-lookup"><span data-stu-id="d427d-215">Name</span></span>      | <span data-ttu-id="d427d-216">類型</span><span class="sxs-lookup"><span data-stu-id="d427d-216">Type</span></span>             | <span data-ttu-id="d427d-217">必要</span><span class="sxs-lookup"><span data-stu-id="d427d-217">Required</span></span> | <span data-ttu-id="d427d-218">附註</span><span class="sxs-lookup"><span data-stu-id="d427d-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d427d-219">資料</span><span class="sxs-lookup"><span data-stu-id="d427d-219">data</span></span>      | <span data-ttu-id="d427d-220">字串陣列</span><span class="sxs-lookup"><span data-stu-id="d427d-220">array of strings</span></span> | <span data-ttu-id="d427d-221">是</span><span class="sxs-lookup"><span data-stu-id="d427d-221">yes</span></span>      | <span data-ttu-id="d427d-222">要求所符合的套件版本</span><span class="sxs-lookup"><span data-stu-id="d427d-222">The package versions matched by the request</span></span>

<span data-ttu-id="d427d-223">如果`1.0.0+metadata` `data` 查詢字串中提供,則陣列中的封裝版本可能會包含SemVer2.0.0組建中繼資料(例如)。`semVerLevel=2.0.0`</span><span class="sxs-lookup"><span data-stu-id="d427d-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d427d-224">範例要求</span><span class="sxs-lookup"><span data-stu-id="d427d-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d427d-225">範例回應</span><span class="sxs-lookup"><span data-stu-id="d427d-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
