---
title: 自動完成，NuGet API
description: 搜尋自動完成服務支援對套件識別碼和版本進行互動式探索。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292289"
---
# <a name="autocomplete"></a><span data-ttu-id="238fa-103">自動完成</span><span class="sxs-lookup"><span data-stu-id="238fa-103">Autocomplete</span></span>

<span data-ttu-id="238fa-104">您可以使用 V3 API 來建立套件識別碼和版本自動完成體驗。</span><span class="sxs-lookup"><span data-stu-id="238fa-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="238fa-105">用來進行自動完成查詢的資源是 `SearchAutocompleteService` 在[服務索引](service-index.md)中找到的資源。</span><span class="sxs-lookup"><span data-stu-id="238fa-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="238fa-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="238fa-106">Versioning</span></span>

<span data-ttu-id="238fa-107">`@type`會使用下列值：</span><span class="sxs-lookup"><span data-stu-id="238fa-107">The following `@type` values are used:</span></span>

<span data-ttu-id="238fa-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="238fa-108">@type value</span></span>                          | <span data-ttu-id="238fa-109">備註</span><span class="sxs-lookup"><span data-stu-id="238fa-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="238fa-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="238fa-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="238fa-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="238fa-111">The initial release</span></span>
<span data-ttu-id="238fa-112">SearchAutocompleteService/3.0.0-搶鮮版（Beta）</span><span class="sxs-lookup"><span data-stu-id="238fa-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="238fa-113">別名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="238fa-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="238fa-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="238fa-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="238fa-115">別名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="238fa-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="238fa-116">SearchAutocompleteService/3.5。0</span><span class="sxs-lookup"><span data-stu-id="238fa-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="238fa-117">包含 `packageType` 查詢參數的支援</span><span class="sxs-lookup"><span data-stu-id="238fa-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="238fa-118">SearchAutocompleteService/3.5。0</span><span class="sxs-lookup"><span data-stu-id="238fa-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="238fa-119">這個版本導入了 `packageType` 查詢參數的支援，允許依作者定義的套件類型進行篩選。</span><span class="sxs-lookup"><span data-stu-id="238fa-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="238fa-120">它與的查詢完全相容 `SearchAutocompleteService` 。</span><span class="sxs-lookup"><span data-stu-id="238fa-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="238fa-121">基底 URL</span><span class="sxs-lookup"><span data-stu-id="238fa-121">Base URL</span></span>

<span data-ttu-id="238fa-122">下列 Api 的基底 URL 是 `@id` 與上述其中一個資源值相關聯的屬性值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="238fa-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="238fa-123">在下列檔中，將會使用預留位置基底 URL `{@id}` 。</span><span class="sxs-lookup"><span data-stu-id="238fa-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="238fa-124">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="238fa-124">HTTP Methods</span></span>

<span data-ttu-id="238fa-125">在註冊資源中找到的所有 Url 都支援 HTTP 方法 `GET` 和 `HEAD` 。</span><span class="sxs-lookup"><span data-stu-id="238fa-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="238fa-126">搜尋套件識別碼</span><span class="sxs-lookup"><span data-stu-id="238fa-126">Search for package IDs</span></span>

<span data-ttu-id="238fa-127">第一個自動完成 API 支援搜尋封裝識別碼字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="238fa-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="238fa-128">當您想要在與 NuGet 套件來源整合的使用者介面中提供封裝自動提示功能時，這是很好的選擇。</span><span class="sxs-lookup"><span data-stu-id="238fa-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="238fa-129">只有未列出版本的套件不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="238fa-129">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a><span data-ttu-id="238fa-130">要求參數</span><span class="sxs-lookup"><span data-stu-id="238fa-130">Request parameters</span></span>

<span data-ttu-id="238fa-131">Name</span><span class="sxs-lookup"><span data-stu-id="238fa-131">Name</span></span>        | <span data-ttu-id="238fa-132">位於</span><span class="sxs-lookup"><span data-stu-id="238fa-132">In</span></span>     | <span data-ttu-id="238fa-133">類型</span><span class="sxs-lookup"><span data-stu-id="238fa-133">Type</span></span>    | <span data-ttu-id="238fa-134">必要</span><span class="sxs-lookup"><span data-stu-id="238fa-134">Required</span></span> | <span data-ttu-id="238fa-135">備註</span><span class="sxs-lookup"><span data-stu-id="238fa-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="238fa-136">q</span><span class="sxs-lookup"><span data-stu-id="238fa-136">q</span></span>           | <span data-ttu-id="238fa-137">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-137">URL</span></span>    | <span data-ttu-id="238fa-138">字串</span><span class="sxs-lookup"><span data-stu-id="238fa-138">string</span></span>  | <span data-ttu-id="238fa-139">否</span><span class="sxs-lookup"><span data-stu-id="238fa-139">no</span></span>       | <span data-ttu-id="238fa-140">要與套件識別碼比較的字串</span><span class="sxs-lookup"><span data-stu-id="238fa-140">The string to compare against package IDs</span></span>
<span data-ttu-id="238fa-141">skip</span><span class="sxs-lookup"><span data-stu-id="238fa-141">skip</span></span>        | <span data-ttu-id="238fa-142">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-142">URL</span></span>    | <span data-ttu-id="238fa-143">integer</span><span class="sxs-lookup"><span data-stu-id="238fa-143">integer</span></span> | <span data-ttu-id="238fa-144">否</span><span class="sxs-lookup"><span data-stu-id="238fa-144">no</span></span>       | <span data-ttu-id="238fa-145">要略過的結果數目，用於分頁</span><span class="sxs-lookup"><span data-stu-id="238fa-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="238fa-146">take</span><span class="sxs-lookup"><span data-stu-id="238fa-146">take</span></span>        | <span data-ttu-id="238fa-147">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-147">URL</span></span>    | <span data-ttu-id="238fa-148">integer</span><span class="sxs-lookup"><span data-stu-id="238fa-148">integer</span></span> | <span data-ttu-id="238fa-149">否</span><span class="sxs-lookup"><span data-stu-id="238fa-149">no</span></span>       | <span data-ttu-id="238fa-150">要傳回的結果數目，用於分頁</span><span class="sxs-lookup"><span data-stu-id="238fa-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="238fa-151">prerelease</span><span class="sxs-lookup"><span data-stu-id="238fa-151">prerelease</span></span>  | <span data-ttu-id="238fa-152">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-152">URL</span></span>    | <span data-ttu-id="238fa-153">boolean</span><span class="sxs-lookup"><span data-stu-id="238fa-153">boolean</span></span> | <span data-ttu-id="238fa-154">否</span><span class="sxs-lookup"><span data-stu-id="238fa-154">no</span></span>       | <span data-ttu-id="238fa-155">`true`或 `false` 判斷是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="238fa-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="238fa-156">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="238fa-156">semVerLevel</span></span> | <span data-ttu-id="238fa-157">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-157">URL</span></span>    | <span data-ttu-id="238fa-158">字串</span><span class="sxs-lookup"><span data-stu-id="238fa-158">string</span></span>  | <span data-ttu-id="238fa-159">否</span><span class="sxs-lookup"><span data-stu-id="238fa-159">no</span></span>       | <span data-ttu-id="238fa-160">SemVer 1.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="238fa-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="238fa-161">packageType</span><span class="sxs-lookup"><span data-stu-id="238fa-161">packageType</span></span> | <span data-ttu-id="238fa-162">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-162">URL</span></span>    | <span data-ttu-id="238fa-163">字串</span><span class="sxs-lookup"><span data-stu-id="238fa-163">string</span></span>  | <span data-ttu-id="238fa-164">否</span><span class="sxs-lookup"><span data-stu-id="238fa-164">no</span></span>       | <span data-ttu-id="238fa-165">用來篩選封裝的封裝類型（新增于中 `SearchAutocompleteService/3.5.0` ）</span><span class="sxs-lookup"><span data-stu-id="238fa-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="238fa-166">自動完成查詢 `q` 會以伺服器實作為定義的方式進行剖析。</span><span class="sxs-lookup"><span data-stu-id="238fa-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="238fa-167">nuget.org 支援查詢套件識別碼權杖的前置詞，這是由 spliting 原始 by camel 大小寫和符號字元所產生的識別碼片段。</span><span class="sxs-lookup"><span data-stu-id="238fa-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="238fa-168">`skip`參數的預設值為0。</span><span class="sxs-lookup"><span data-stu-id="238fa-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="238fa-169">`take`參數應該是大於零的整數。</span><span class="sxs-lookup"><span data-stu-id="238fa-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="238fa-170">伺服器的執行可能會強加最大值。</span><span class="sxs-lookup"><span data-stu-id="238fa-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="238fa-171">如果 `prerelease` 未提供，則會排除發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="238fa-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="238fa-172">`semVerLevel`查詢參數是用來加入[SemVer 2.0.0 套件](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="238fa-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="238fa-173">如果排除此查詢參數，則只會傳回具有 SemVer 1.0.0 相容版本的套件識別碼（使用[標準 NuGet 版本](../concepts/package-versioning.md)設定注意事項，例如具有4個整數部分的版本字串）。</span><span class="sxs-lookup"><span data-stu-id="238fa-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="238fa-174">如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容的套件。</span><span class="sxs-lookup"><span data-stu-id="238fa-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="238fa-175">如需詳細資訊，請參閱[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="238fa-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="238fa-176">`packageType`參數是用來進一步篩選自動完成結果，只包含至少有一個符合封裝類型名稱之套件類型的封裝。</span><span class="sxs-lookup"><span data-stu-id="238fa-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="238fa-177">如果提供的封裝類型不是[封裝類型檔](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)所定義的有效封裝類型，則會傳回空的結果。</span><span class="sxs-lookup"><span data-stu-id="238fa-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="238fa-178">如果提供的封裝類型是空的，則不會套用任何篩選。</span><span class="sxs-lookup"><span data-stu-id="238fa-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="238fa-179">換句話說，將沒有值傳遞給參數的 `packageType` 行為會如同未傳遞參數一樣。</span><span class="sxs-lookup"><span data-stu-id="238fa-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="238fa-180">回應</span><span class="sxs-lookup"><span data-stu-id="238fa-180">Response</span></span>

<span data-ttu-id="238fa-181">回應是包含最多 `take` 自動完成結果的 JSON 檔。</span><span class="sxs-lookup"><span data-stu-id="238fa-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="238fa-182">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="238fa-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="238fa-183">名稱</span><span class="sxs-lookup"><span data-stu-id="238fa-183">Name</span></span>      | <span data-ttu-id="238fa-184">類型</span><span class="sxs-lookup"><span data-stu-id="238fa-184">Type</span></span>             | <span data-ttu-id="238fa-185">必要</span><span class="sxs-lookup"><span data-stu-id="238fa-185">Required</span></span> | <span data-ttu-id="238fa-186">備註</span><span class="sxs-lookup"><span data-stu-id="238fa-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="238fa-187">totalHits</span><span class="sxs-lookup"><span data-stu-id="238fa-187">totalHits</span></span> | <span data-ttu-id="238fa-188">integer</span><span class="sxs-lookup"><span data-stu-id="238fa-188">integer</span></span>          | <span data-ttu-id="238fa-189">是</span><span class="sxs-lookup"><span data-stu-id="238fa-189">yes</span></span>      | <span data-ttu-id="238fa-190">相符專案總數，忽略 `skip` 和`take`</span><span class="sxs-lookup"><span data-stu-id="238fa-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="238fa-191">data</span><span class="sxs-lookup"><span data-stu-id="238fa-191">data</span></span>      | <span data-ttu-id="238fa-192">字串陣列</span><span class="sxs-lookup"><span data-stu-id="238fa-192">array of strings</span></span> | <span data-ttu-id="238fa-193">是</span><span class="sxs-lookup"><span data-stu-id="238fa-193">yes</span></span>      | <span data-ttu-id="238fa-194">要求所符合的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="238fa-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="238fa-195">範例要求</span><span class="sxs-lookup"><span data-stu-id="238fa-195">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="238fa-196">範例回應</span><span class="sxs-lookup"><span data-stu-id="238fa-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="238fa-197">列舉封裝版本</span><span class="sxs-lookup"><span data-stu-id="238fa-197">Enumerate package versions</span></span>

<span data-ttu-id="238fa-198">一旦使用先前的 API 探索到套件識別碼之後，用戶端就可以使用自動完成 API 來列舉所提供封裝識別碼的套件版本。</span><span class="sxs-lookup"><span data-stu-id="238fa-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="238fa-199">未列出的封裝版本不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="238fa-199">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="238fa-200">要求參數</span><span class="sxs-lookup"><span data-stu-id="238fa-200">Request parameters</span></span>

<span data-ttu-id="238fa-201">Name</span><span class="sxs-lookup"><span data-stu-id="238fa-201">Name</span></span>        | <span data-ttu-id="238fa-202">位於</span><span class="sxs-lookup"><span data-stu-id="238fa-202">In</span></span>     | <span data-ttu-id="238fa-203">類型</span><span class="sxs-lookup"><span data-stu-id="238fa-203">Type</span></span>    | <span data-ttu-id="238fa-204">必要</span><span class="sxs-lookup"><span data-stu-id="238fa-204">Required</span></span> | <span data-ttu-id="238fa-205">備註</span><span class="sxs-lookup"><span data-stu-id="238fa-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="238fa-206">id</span><span class="sxs-lookup"><span data-stu-id="238fa-206">id</span></span>          | <span data-ttu-id="238fa-207">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-207">URL</span></span>    | <span data-ttu-id="238fa-208">字串</span><span class="sxs-lookup"><span data-stu-id="238fa-208">string</span></span>  | <span data-ttu-id="238fa-209">是</span><span class="sxs-lookup"><span data-stu-id="238fa-209">yes</span></span>      | <span data-ttu-id="238fa-210">要為其提取版本的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="238fa-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="238fa-211">prerelease</span><span class="sxs-lookup"><span data-stu-id="238fa-211">prerelease</span></span>  | <span data-ttu-id="238fa-212">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-212">URL</span></span>    | <span data-ttu-id="238fa-213">boolean</span><span class="sxs-lookup"><span data-stu-id="238fa-213">boolean</span></span> | <span data-ttu-id="238fa-214">否</span><span class="sxs-lookup"><span data-stu-id="238fa-214">no</span></span>       | <span data-ttu-id="238fa-215">`true`或 `false` 判斷是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="238fa-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="238fa-216">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="238fa-216">semVerLevel</span></span> | <span data-ttu-id="238fa-217">URL</span><span class="sxs-lookup"><span data-stu-id="238fa-217">URL</span></span>    | <span data-ttu-id="238fa-218">字串</span><span class="sxs-lookup"><span data-stu-id="238fa-218">string</span></span>  | <span data-ttu-id="238fa-219">否</span><span class="sxs-lookup"><span data-stu-id="238fa-219">no</span></span>       | <span data-ttu-id="238fa-220">SemVer 2.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="238fa-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="238fa-221">如果 `prerelease` 未提供，則會排除發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="238fa-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="238fa-222">`semVerLevel`查詢參數是用來加入 SemVer 2.0.0 套件。</span><span class="sxs-lookup"><span data-stu-id="238fa-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="238fa-223">如果排除此查詢參數，則只會傳回 SemVer 1.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="238fa-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="238fa-224">如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="238fa-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="238fa-225">如需詳細資訊，請參閱[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="238fa-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="238fa-226">回應</span><span class="sxs-lookup"><span data-stu-id="238fa-226">Response</span></span>

<span data-ttu-id="238fa-227">回應是 JSON 檔，其中包含所提供封裝識別碼的所有封裝版本，並依指定的查詢參數進行篩選。</span><span class="sxs-lookup"><span data-stu-id="238fa-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="238fa-228">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="238fa-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="238fa-229">名稱</span><span class="sxs-lookup"><span data-stu-id="238fa-229">Name</span></span>      | <span data-ttu-id="238fa-230">類型</span><span class="sxs-lookup"><span data-stu-id="238fa-230">Type</span></span>             | <span data-ttu-id="238fa-231">必要</span><span class="sxs-lookup"><span data-stu-id="238fa-231">Required</span></span> | <span data-ttu-id="238fa-232">備註</span><span class="sxs-lookup"><span data-stu-id="238fa-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="238fa-233">data</span><span class="sxs-lookup"><span data-stu-id="238fa-233">data</span></span>      | <span data-ttu-id="238fa-234">字串陣列</span><span class="sxs-lookup"><span data-stu-id="238fa-234">array of strings</span></span> | <span data-ttu-id="238fa-235">是</span><span class="sxs-lookup"><span data-stu-id="238fa-235">yes</span></span>      | <span data-ttu-id="238fa-236">要求所符合的套件版本</span><span class="sxs-lookup"><span data-stu-id="238fa-236">The package versions matched by the request</span></span>

<span data-ttu-id="238fa-237">如果查詢字串中提供，則陣列中的封裝版本 `data` 可能會包含 SemVer 2.0.0 組建中繼資料（例如 `1.0.0+metadata` ） `semVerLevel=2.0.0` 。</span><span class="sxs-lookup"><span data-stu-id="238fa-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="238fa-238">範例要求</span><span class="sxs-lookup"><span data-stu-id="238fa-238">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="238fa-239">範例回應</span><span class="sxs-lookup"><span data-stu-id="238fa-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
