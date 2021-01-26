---
title: 自動完成，NuGet API
description: 搜尋自動完成服務支援封裝識別碼和版本的互動式探索。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773955"
---
# <a name="autocomplete"></a><span data-ttu-id="e1731-103">自動完成</span><span class="sxs-lookup"><span data-stu-id="e1731-103">Autocomplete</span></span>

<span data-ttu-id="e1731-104">您可以使用 V3 API 建立套件識別碼和版本自動完成體驗。</span><span class="sxs-lookup"><span data-stu-id="e1731-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="e1731-105">用來進行自動完成查詢的資源是在 `SearchAutocompleteService` [服務索引](service-index.md)中找到的資源。</span><span class="sxs-lookup"><span data-stu-id="e1731-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e1731-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="e1731-106">Versioning</span></span>

<span data-ttu-id="e1731-107">使用的 `@type` 值如下：</span><span class="sxs-lookup"><span data-stu-id="e1731-107">The following `@type` values are used:</span></span>

<span data-ttu-id="e1731-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="e1731-108">@type value</span></span>                          | <span data-ttu-id="e1731-109">備註</span><span class="sxs-lookup"><span data-stu-id="e1731-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="e1731-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="e1731-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="e1731-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="e1731-111">The initial release</span></span>
<span data-ttu-id="e1731-112">SearchAutocompleteService/3.0.0-Beta</span><span class="sxs-lookup"><span data-stu-id="e1731-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="e1731-113">別名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e1731-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="e1731-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="e1731-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="e1731-115">別名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e1731-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="e1731-116">SearchAutocompleteService/3.5。0</span><span class="sxs-lookup"><span data-stu-id="e1731-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="e1731-117">包含 `packageType` 查詢參數的支援</span><span class="sxs-lookup"><span data-stu-id="e1731-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="e1731-118">SearchAutocompleteService/3.5。0</span><span class="sxs-lookup"><span data-stu-id="e1731-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="e1731-119">此版本導入了 `packageType` 查詢參數的支援，允許依作者定義的套件類型進行篩選。</span><span class="sxs-lookup"><span data-stu-id="e1731-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="e1731-120">它與的查詢完全相容 `SearchAutocompleteService` 。</span><span class="sxs-lookup"><span data-stu-id="e1731-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="e1731-121">基底 URL</span><span class="sxs-lookup"><span data-stu-id="e1731-121">Base URL</span></span>

<span data-ttu-id="e1731-122">下列 Api 的基底 URL 是 `@id` 與上述其中一個資源值相關聯之屬性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="e1731-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="e1731-123">在下列檔中，將會使用預留位置基底 URL `{@id}` 。</span><span class="sxs-lookup"><span data-stu-id="e1731-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e1731-124">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="e1731-124">HTTP Methods</span></span>

<span data-ttu-id="e1731-125">在註冊資源中找到的所有 Url 都支援 HTTP 方法 `GET` 和 `HEAD` 。</span><span class="sxs-lookup"><span data-stu-id="e1731-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="e1731-126">搜尋套件識別碼</span><span class="sxs-lookup"><span data-stu-id="e1731-126">Search for package IDs</span></span>

<span data-ttu-id="e1731-127">第一個自動完成 API 支援搜尋套件識別碼字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="e1731-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="e1731-128">當您想要在與 NuGet 套件來源整合的使用者介面中提供封裝自動提示功能時，這是很好的選擇。</span><span class="sxs-lookup"><span data-stu-id="e1731-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="e1731-129">只有未列出的版本的套件不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="e1731-129">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a><span data-ttu-id="e1731-130">要求參數</span><span class="sxs-lookup"><span data-stu-id="e1731-130">Request parameters</span></span>

<span data-ttu-id="e1731-131">名稱</span><span class="sxs-lookup"><span data-stu-id="e1731-131">Name</span></span>        | <span data-ttu-id="e1731-132">位於</span><span class="sxs-lookup"><span data-stu-id="e1731-132">In</span></span>     | <span data-ttu-id="e1731-133">類型</span><span class="sxs-lookup"><span data-stu-id="e1731-133">Type</span></span>    | <span data-ttu-id="e1731-134">必要</span><span class="sxs-lookup"><span data-stu-id="e1731-134">Required</span></span> | <span data-ttu-id="e1731-135">備註</span><span class="sxs-lookup"><span data-stu-id="e1731-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e1731-136">q</span><span class="sxs-lookup"><span data-stu-id="e1731-136">q</span></span>           | <span data-ttu-id="e1731-137">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-137">URL</span></span>    | <span data-ttu-id="e1731-138">字串</span><span class="sxs-lookup"><span data-stu-id="e1731-138">string</span></span>  | <span data-ttu-id="e1731-139">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-139">no</span></span>       | <span data-ttu-id="e1731-140">要與封裝識別碼比較的字串</span><span class="sxs-lookup"><span data-stu-id="e1731-140">The string to compare against package IDs</span></span>
<span data-ttu-id="e1731-141">skip</span><span class="sxs-lookup"><span data-stu-id="e1731-141">skip</span></span>        | <span data-ttu-id="e1731-142">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-142">URL</span></span>    | <span data-ttu-id="e1731-143">整數</span><span class="sxs-lookup"><span data-stu-id="e1731-143">integer</span></span> | <span data-ttu-id="e1731-144">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-144">no</span></span>       | <span data-ttu-id="e1731-145">要跳過的結果數目（分頁）</span><span class="sxs-lookup"><span data-stu-id="e1731-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="e1731-146">take</span><span class="sxs-lookup"><span data-stu-id="e1731-146">take</span></span>        | <span data-ttu-id="e1731-147">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-147">URL</span></span>    | <span data-ttu-id="e1731-148">整數</span><span class="sxs-lookup"><span data-stu-id="e1731-148">integer</span></span> | <span data-ttu-id="e1731-149">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-149">no</span></span>       | <span data-ttu-id="e1731-150">要傳回的結果數目，用於分頁</span><span class="sxs-lookup"><span data-stu-id="e1731-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="e1731-151">prerelease</span><span class="sxs-lookup"><span data-stu-id="e1731-151">prerelease</span></span>  | <span data-ttu-id="e1731-152">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-152">URL</span></span>    | <span data-ttu-id="e1731-153">boolean</span><span class="sxs-lookup"><span data-stu-id="e1731-153">boolean</span></span> | <span data-ttu-id="e1731-154">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-154">no</span></span>       | <span data-ttu-id="e1731-155">`true` 或 `false` 判斷是否包含 [發行前版本的套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e1731-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e1731-156">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e1731-156">semVerLevel</span></span> | <span data-ttu-id="e1731-157">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-157">URL</span></span>    | <span data-ttu-id="e1731-158">字串</span><span class="sxs-lookup"><span data-stu-id="e1731-158">string</span></span>  | <span data-ttu-id="e1731-159">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-159">no</span></span>       | <span data-ttu-id="e1731-160">SemVer 1.0.0 版字串</span><span class="sxs-lookup"><span data-stu-id="e1731-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="e1731-161">packageType</span><span class="sxs-lookup"><span data-stu-id="e1731-161">packageType</span></span> | <span data-ttu-id="e1731-162">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-162">URL</span></span>    | <span data-ttu-id="e1731-163">字串</span><span class="sxs-lookup"><span data-stu-id="e1731-163">string</span></span>  | <span data-ttu-id="e1731-164">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-164">no</span></span>       | <span data-ttu-id="e1731-165">用來篩選封裝 (在) 中新增的封裝類型 `SearchAutocompleteService/3.5.0`</span><span class="sxs-lookup"><span data-stu-id="e1731-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="e1731-166">自動完成查詢 `q` 會以伺服器執行所定義的方式進行剖析。</span><span class="sxs-lookup"><span data-stu-id="e1731-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="e1731-167">nuget.org 支援查詢封裝識別碼權杖的前置詞，這是由分割原始的識別碼和符號字元所產生的識別碼片段。</span><span class="sxs-lookup"><span data-stu-id="e1731-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="e1731-168">`skip`參數的預設值為0。</span><span class="sxs-lookup"><span data-stu-id="e1731-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="e1731-169">`take`參數必須是大於零的整數。</span><span class="sxs-lookup"><span data-stu-id="e1731-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="e1731-170">伺服器的執行可能會強加最大值。</span><span class="sxs-lookup"><span data-stu-id="e1731-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="e1731-171">如果 `prerelease` 未提供，則會排除發行前版本的套件。</span><span class="sxs-lookup"><span data-stu-id="e1731-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e1731-172">`semVerLevel`查詢參數是用來加入[SemVer 2.0.0 套件](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="e1731-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="e1731-173">如果排除此查詢參數，則只會傳回具有 SemVer 1.0.0 版相容版本的套件識別碼， (有 [標準 NuGet 版本](../concepts/package-versioning.md) 設定注意事項，例如具有4個整數部分) 的版本字串。</span><span class="sxs-lookup"><span data-stu-id="e1731-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="e1731-174">如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容套件。</span><span class="sxs-lookup"><span data-stu-id="e1731-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="e1731-175">如需詳細資訊，請參閱 [nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="e1731-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="e1731-176">`packageType`參數是用來進一步將自動完成結果篩選為至少有一個套件類型符合套件類型名稱的封裝。</span><span class="sxs-lookup"><span data-stu-id="e1731-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="e1731-177">如果提供的封裝類型不是 [封裝類型檔](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)所定義的有效封裝類型，則會傳回空的結果。</span><span class="sxs-lookup"><span data-stu-id="e1731-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="e1731-178">如果提供的封裝類型是空的，則不會套用任何篩選。</span><span class="sxs-lookup"><span data-stu-id="e1731-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="e1731-179">換句話說，傳遞沒有值給 `packageType` 參數的行為會如同未傳遞參數。</span><span class="sxs-lookup"><span data-stu-id="e1731-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="e1731-180">回應</span><span class="sxs-lookup"><span data-stu-id="e1731-180">Response</span></span>

<span data-ttu-id="e1731-181">回應是包含最多 `take` 自動完成結果的 JSON 檔。</span><span class="sxs-lookup"><span data-stu-id="e1731-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="e1731-182">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e1731-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="e1731-183">名稱</span><span class="sxs-lookup"><span data-stu-id="e1731-183">Name</span></span>      | <span data-ttu-id="e1731-184">類型</span><span class="sxs-lookup"><span data-stu-id="e1731-184">Type</span></span>             | <span data-ttu-id="e1731-185">必要</span><span class="sxs-lookup"><span data-stu-id="e1731-185">Required</span></span> | <span data-ttu-id="e1731-186">備註</span><span class="sxs-lookup"><span data-stu-id="e1731-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e1731-187">totalHits</span><span class="sxs-lookup"><span data-stu-id="e1731-187">totalHits</span></span> | <span data-ttu-id="e1731-188">整數</span><span class="sxs-lookup"><span data-stu-id="e1731-188">integer</span></span>          | <span data-ttu-id="e1731-189">是</span><span class="sxs-lookup"><span data-stu-id="e1731-189">yes</span></span>      | <span data-ttu-id="e1731-190">相符專案的總數，並忽略 `skip` 和 `take`</span><span class="sxs-lookup"><span data-stu-id="e1731-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="e1731-191">data</span><span class="sxs-lookup"><span data-stu-id="e1731-191">data</span></span>      | <span data-ttu-id="e1731-192">字串陣列</span><span class="sxs-lookup"><span data-stu-id="e1731-192">array of strings</span></span> | <span data-ttu-id="e1731-193">是</span><span class="sxs-lookup"><span data-stu-id="e1731-193">yes</span></span>      | <span data-ttu-id="e1731-194">符合要求的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="e1731-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="e1731-195">範例要求</span><span class="sxs-lookup"><span data-stu-id="e1731-195">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="e1731-196">範例回應</span><span class="sxs-lookup"><span data-stu-id="e1731-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="e1731-197">列舉套件版本</span><span class="sxs-lookup"><span data-stu-id="e1731-197">Enumerate package versions</span></span>

<span data-ttu-id="e1731-198">使用先前的 API 探索到套件識別碼之後，用戶端就可以使用自動完成 API 來列舉所提供封裝識別碼的套件版本。</span><span class="sxs-lookup"><span data-stu-id="e1731-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="e1731-199">未列出的套件版本不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="e1731-199">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="e1731-200">要求參數</span><span class="sxs-lookup"><span data-stu-id="e1731-200">Request parameters</span></span>

<span data-ttu-id="e1731-201">名稱</span><span class="sxs-lookup"><span data-stu-id="e1731-201">Name</span></span>        | <span data-ttu-id="e1731-202">位於</span><span class="sxs-lookup"><span data-stu-id="e1731-202">In</span></span>     | <span data-ttu-id="e1731-203">類型</span><span class="sxs-lookup"><span data-stu-id="e1731-203">Type</span></span>    | <span data-ttu-id="e1731-204">必要</span><span class="sxs-lookup"><span data-stu-id="e1731-204">Required</span></span> | <span data-ttu-id="e1731-205">注意</span><span class="sxs-lookup"><span data-stu-id="e1731-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e1731-206">id</span><span class="sxs-lookup"><span data-stu-id="e1731-206">id</span></span>          | <span data-ttu-id="e1731-207">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-207">URL</span></span>    | <span data-ttu-id="e1731-208">字串</span><span class="sxs-lookup"><span data-stu-id="e1731-208">string</span></span>  | <span data-ttu-id="e1731-209">是</span><span class="sxs-lookup"><span data-stu-id="e1731-209">yes</span></span>      | <span data-ttu-id="e1731-210">要提取版本的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="e1731-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="e1731-211">prerelease</span><span class="sxs-lookup"><span data-stu-id="e1731-211">prerelease</span></span>  | <span data-ttu-id="e1731-212">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-212">URL</span></span>    | <span data-ttu-id="e1731-213">boolean</span><span class="sxs-lookup"><span data-stu-id="e1731-213">boolean</span></span> | <span data-ttu-id="e1731-214">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-214">no</span></span>       | <span data-ttu-id="e1731-215">`true` 或 `false` 判斷是否包含 [發行前版本的套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e1731-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e1731-216">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e1731-216">semVerLevel</span></span> | <span data-ttu-id="e1731-217">URL</span><span class="sxs-lookup"><span data-stu-id="e1731-217">URL</span></span>    | <span data-ttu-id="e1731-218">字串</span><span class="sxs-lookup"><span data-stu-id="e1731-218">string</span></span>  | <span data-ttu-id="e1731-219">不可以</span><span class="sxs-lookup"><span data-stu-id="e1731-219">no</span></span>       | <span data-ttu-id="e1731-220">SemVer 2.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="e1731-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="e1731-221">如果 `prerelease` 未提供，則會排除發行前版本的套件。</span><span class="sxs-lookup"><span data-stu-id="e1731-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e1731-222">`semVerLevel`查詢參數是用來加入 SemVer 2.0.0 套件。</span><span class="sxs-lookup"><span data-stu-id="e1731-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="e1731-223">如果排除此查詢參數，則只會傳回 SemVer 1.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="e1731-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="e1731-224">如果 `semVerLevel=2.0.0` 提供，則會傳回 SemVer 1.0.0 和 SemVer 2.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="e1731-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="e1731-225">如需詳細資訊，請參閱 [nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。</span><span class="sxs-lookup"><span data-stu-id="e1731-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e1731-226">回應</span><span class="sxs-lookup"><span data-stu-id="e1731-226">Response</span></span>

<span data-ttu-id="e1731-227">回應是 JSON 檔，其中包含所提供封裝識別碼的所有套件版本，並依指定的查詢參數進行篩選。</span><span class="sxs-lookup"><span data-stu-id="e1731-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="e1731-228">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e1731-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="e1731-229">名稱</span><span class="sxs-lookup"><span data-stu-id="e1731-229">Name</span></span>      | <span data-ttu-id="e1731-230">類型</span><span class="sxs-lookup"><span data-stu-id="e1731-230">Type</span></span>             | <span data-ttu-id="e1731-231">必要</span><span class="sxs-lookup"><span data-stu-id="e1731-231">Required</span></span> | <span data-ttu-id="e1731-232">備註</span><span class="sxs-lookup"><span data-stu-id="e1731-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e1731-233">data</span><span class="sxs-lookup"><span data-stu-id="e1731-233">data</span></span>      | <span data-ttu-id="e1731-234">字串陣列</span><span class="sxs-lookup"><span data-stu-id="e1731-234">array of strings</span></span> | <span data-ttu-id="e1731-235">是</span><span class="sxs-lookup"><span data-stu-id="e1731-235">yes</span></span>      | <span data-ttu-id="e1731-236">要求符合的套件版本</span><span class="sxs-lookup"><span data-stu-id="e1731-236">The package versions matched by the request</span></span>

<span data-ttu-id="e1731-237">陣列中的套件版本 `data` 可能包含 SemVer 2.0.0 組建中繼資料 (例如 `1.0.0+metadata`) 是否 `semVerLevel=2.0.0` 在查詢字串中提供。</span><span class="sxs-lookup"><span data-stu-id="e1731-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e1731-238">範例要求</span><span class="sxs-lookup"><span data-stu-id="e1731-238">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="e1731-239">範例回應</span><span class="sxs-lookup"><span data-stu-id="e1731-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
