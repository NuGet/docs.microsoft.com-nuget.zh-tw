---
title: 自動完成、 NuGet API
description: 搜尋自動完成服務支援的套件識別碼的互動式探索和版本。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2d2b20c1ea439ec0a3225cf983d9a4d2eedb0333
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324756"
---
# <a name="autocomplete"></a><span data-ttu-id="e1252-103">自動完成</span><span class="sxs-lookup"><span data-stu-id="e1252-103">Autocomplete</span></span>

<span data-ttu-id="e1252-104">就可以建置的套件識別碼和版本自動完成體驗使用 V3 API。</span><span class="sxs-lookup"><span data-stu-id="e1252-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="e1252-105">用來進行自動完成查詢的資源`SearchAutocompleteService`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="e1252-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e1252-106">版本控制</span><span class="sxs-lookup"><span data-stu-id="e1252-106">Versioning</span></span>

<span data-ttu-id="e1252-107">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="e1252-107">The following `@type` values are used:</span></span>

<span data-ttu-id="e1252-108">@type 值</span><span class="sxs-lookup"><span data-stu-id="e1252-108">@type value</span></span>                          | <span data-ttu-id="e1252-109">注意</span><span class="sxs-lookup"><span data-stu-id="e1252-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="e1252-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="e1252-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="e1252-111">初始版本</span><span class="sxs-lookup"><span data-stu-id="e1252-111">The initial release</span></span>
<span data-ttu-id="e1252-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="e1252-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="e1252-113">別名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e1252-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="e1252-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="e1252-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="e1252-115">別名 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e1252-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="e1252-116">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="e1252-116">Base URL</span></span>

<span data-ttu-id="e1252-117">下列 Api 的基底 URL 是值`@id`其中一個先前提及的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="e1252-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="e1252-118">在下列的文件中的預留位置基底 URL`{@id}`將使用。</span><span class="sxs-lookup"><span data-stu-id="e1252-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e1252-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="e1252-119">HTTP Methods</span></span>

<span data-ttu-id="e1252-120">所有 Url 的 HTTP 方法位於註冊資源的支援`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="e1252-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="e1252-121">搜尋套件識別碼</span><span class="sxs-lookup"><span data-stu-id="e1252-121">Search for package IDs</span></span>

<span data-ttu-id="e1252-122">第一個自動完成 API 支援搜尋封裝 ID 字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="e1252-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="e1252-123">當您想要提供使用者介面整合在一起的 NuGet 套件來源中的封裝自動提示功能時，這是很棒。</span><span class="sxs-lookup"><span data-stu-id="e1252-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="e1252-124">只有未列出的版本的封裝不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="e1252-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e1252-125">要求參數</span><span class="sxs-lookup"><span data-stu-id="e1252-125">Request parameters</span></span>

<span data-ttu-id="e1252-126">名稱</span><span class="sxs-lookup"><span data-stu-id="e1252-126">Name</span></span>        | <span data-ttu-id="e1252-127">In</span><span class="sxs-lookup"><span data-stu-id="e1252-127">In</span></span>     | <span data-ttu-id="e1252-128">類型</span><span class="sxs-lookup"><span data-stu-id="e1252-128">Type</span></span>    | <span data-ttu-id="e1252-129">必要</span><span class="sxs-lookup"><span data-stu-id="e1252-129">Required</span></span> | <span data-ttu-id="e1252-130">注意</span><span class="sxs-lookup"><span data-stu-id="e1252-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e1252-131">q</span><span class="sxs-lookup"><span data-stu-id="e1252-131">q</span></span>           | <span data-ttu-id="e1252-132">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-132">URL</span></span>    | <span data-ttu-id="e1252-133">字串</span><span class="sxs-lookup"><span data-stu-id="e1252-133">string</span></span>  | <span data-ttu-id="e1252-134">否</span><span class="sxs-lookup"><span data-stu-id="e1252-134">no</span></span>       | <span data-ttu-id="e1252-135">要相比較的封裝識別碼的字串</span><span class="sxs-lookup"><span data-stu-id="e1252-135">The string to compare against package IDs</span></span>
<span data-ttu-id="e1252-136">skip</span><span class="sxs-lookup"><span data-stu-id="e1252-136">skip</span></span>        | <span data-ttu-id="e1252-137">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-137">URL</span></span>    | <span data-ttu-id="e1252-138">整數</span><span class="sxs-lookup"><span data-stu-id="e1252-138">integer</span></span> | <span data-ttu-id="e1252-139">否</span><span class="sxs-lookup"><span data-stu-id="e1252-139">no</span></span>       | <span data-ttu-id="e1252-140">若要略過，進行分頁的結果數目</span><span class="sxs-lookup"><span data-stu-id="e1252-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="e1252-141">Take</span><span class="sxs-lookup"><span data-stu-id="e1252-141">take</span></span>        | <span data-ttu-id="e1252-142">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-142">URL</span></span>    | <span data-ttu-id="e1252-143">整數</span><span class="sxs-lookup"><span data-stu-id="e1252-143">integer</span></span> | <span data-ttu-id="e1252-144">否</span><span class="sxs-lookup"><span data-stu-id="e1252-144">no</span></span>       | <span data-ttu-id="e1252-145">若要傳回，進行分頁的結果數目</span><span class="sxs-lookup"><span data-stu-id="e1252-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="e1252-146">發行前版本</span><span class="sxs-lookup"><span data-stu-id="e1252-146">prerelease</span></span>  | <span data-ttu-id="e1252-147">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-147">URL</span></span>    | <span data-ttu-id="e1252-148">boolean</span><span class="sxs-lookup"><span data-stu-id="e1252-148">boolean</span></span> | <span data-ttu-id="e1252-149">否</span><span class="sxs-lookup"><span data-stu-id="e1252-149">no</span></span>       | <span data-ttu-id="e1252-150">`true` 或是`false`決定是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e1252-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e1252-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e1252-151">semVerLevel</span></span> | <span data-ttu-id="e1252-152">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-152">URL</span></span>    | <span data-ttu-id="e1252-153">字串</span><span class="sxs-lookup"><span data-stu-id="e1252-153">string</span></span>  | <span data-ttu-id="e1252-154">否</span><span class="sxs-lookup"><span data-stu-id="e1252-154">no</span></span>       | <span data-ttu-id="e1252-155">SemVer 1.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="e1252-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="e1252-156">自動完成查詢`q`剖析伺服器實作所定義的方式。</span><span class="sxs-lookup"><span data-stu-id="e1252-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="e1252-157">nuget.org 支援查詢的套件識別碼權杖中，也就是所產生的分割識別碼的前置詞的原始駝峰式命名法的大小寫和符號字元。</span><span class="sxs-lookup"><span data-stu-id="e1252-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="e1252-158">`skip`參數預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="e1252-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="e1252-159">`take`參數應該是大於零的整數。</span><span class="sxs-lookup"><span data-stu-id="e1252-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="e1252-160">伺服器實作可能會造成最大值。</span><span class="sxs-lookup"><span data-stu-id="e1252-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="e1252-161">如果`prerelease`未提供，發行前版本套件中排除。</span><span class="sxs-lookup"><span data-stu-id="e1252-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e1252-162">`semVerLevel`查詢參數用來加入[SemVer 2.0.0 封裝](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="e1252-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="e1252-163">如果排除此查詢參數，則會傳回唯一的套件識別碼與 SemVer 1.0.0 相容版本 (使用[標準的 NuGet 版本控制](../reference/package-versioning.md)需要注意的事項，例如 4 的整數部分的版本字串)。</span><span class="sxs-lookup"><span data-stu-id="e1252-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="e1252-164">如果`semVerLevel=2.0.0`提供，將傳回 SemVer 1.0.0 和 SemVer 2.0.0 相容的套件。</span><span class="sxs-lookup"><span data-stu-id="e1252-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="e1252-165">請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e1252-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e1252-166">回應</span><span class="sxs-lookup"><span data-stu-id="e1252-166">Response</span></span>

<span data-ttu-id="e1252-167">回應是 JSON 文件最多包含`take`自動完成結果。</span><span class="sxs-lookup"><span data-stu-id="e1252-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="e1252-168">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e1252-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="e1252-169">名稱</span><span class="sxs-lookup"><span data-stu-id="e1252-169">Name</span></span>      | <span data-ttu-id="e1252-170">類型</span><span class="sxs-lookup"><span data-stu-id="e1252-170">Type</span></span>             | <span data-ttu-id="e1252-171">必要</span><span class="sxs-lookup"><span data-stu-id="e1252-171">Required</span></span> | <span data-ttu-id="e1252-172">注意</span><span class="sxs-lookup"><span data-stu-id="e1252-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e1252-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="e1252-173">totalHits</span></span> | <span data-ttu-id="e1252-174">整數</span><span class="sxs-lookup"><span data-stu-id="e1252-174">integer</span></span>          | <span data-ttu-id="e1252-175">是</span><span class="sxs-lookup"><span data-stu-id="e1252-175">yes</span></span>      | <span data-ttu-id="e1252-176">總數的相符項目，正在略過`skip`和 `take`</span><span class="sxs-lookup"><span data-stu-id="e1252-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="e1252-177">資料</span><span class="sxs-lookup"><span data-stu-id="e1252-177">data</span></span>      | <span data-ttu-id="e1252-178">字串陣列</span><span class="sxs-lookup"><span data-stu-id="e1252-178">array of strings</span></span> | <span data-ttu-id="e1252-179">是</span><span class="sxs-lookup"><span data-stu-id="e1252-179">yes</span></span>      | <span data-ttu-id="e1252-180">封裝符合所要求的識別碼</span><span class="sxs-lookup"><span data-stu-id="e1252-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="e1252-181">範例要求</span><span class="sxs-lookup"><span data-stu-id="e1252-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e1252-182">範例回應</span><span class="sxs-lookup"><span data-stu-id="e1252-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="e1252-183">列舉套件版本</span><span class="sxs-lookup"><span data-stu-id="e1252-183">Enumerate package versions</span></span>

<span data-ttu-id="e1252-184">一旦找到套件識別碼使用先前的 API，用戶端可以使用自動完成 API 來列舉套件版本提供的套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1252-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="e1252-185">未列出的套件版本不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="e1252-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e1252-186">要求參數</span><span class="sxs-lookup"><span data-stu-id="e1252-186">Request parameters</span></span>

<span data-ttu-id="e1252-187">名稱</span><span class="sxs-lookup"><span data-stu-id="e1252-187">Name</span></span>        | <span data-ttu-id="e1252-188">In</span><span class="sxs-lookup"><span data-stu-id="e1252-188">In</span></span>     | <span data-ttu-id="e1252-189">類型</span><span class="sxs-lookup"><span data-stu-id="e1252-189">Type</span></span>    | <span data-ttu-id="e1252-190">必要</span><span class="sxs-lookup"><span data-stu-id="e1252-190">Required</span></span> | <span data-ttu-id="e1252-191">注意</span><span class="sxs-lookup"><span data-stu-id="e1252-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e1252-192">id</span><span class="sxs-lookup"><span data-stu-id="e1252-192">id</span></span>          | <span data-ttu-id="e1252-193">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-193">URL</span></span>    | <span data-ttu-id="e1252-194">字串</span><span class="sxs-lookup"><span data-stu-id="e1252-194">string</span></span>  | <span data-ttu-id="e1252-195">是</span><span class="sxs-lookup"><span data-stu-id="e1252-195">yes</span></span>      | <span data-ttu-id="e1252-196">要擷取的版本之封裝 ID</span><span class="sxs-lookup"><span data-stu-id="e1252-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="e1252-197">發行前版本</span><span class="sxs-lookup"><span data-stu-id="e1252-197">prerelease</span></span>  | <span data-ttu-id="e1252-198">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-198">URL</span></span>    | <span data-ttu-id="e1252-199">boolean</span><span class="sxs-lookup"><span data-stu-id="e1252-199">boolean</span></span> | <span data-ttu-id="e1252-200">否</span><span class="sxs-lookup"><span data-stu-id="e1252-200">no</span></span>       | <span data-ttu-id="e1252-201">`true` 或是`false`決定是否要包含[發行前版本套件](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e1252-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e1252-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e1252-202">semVerLevel</span></span> | <span data-ttu-id="e1252-203">URL</span><span class="sxs-lookup"><span data-stu-id="e1252-203">URL</span></span>    | <span data-ttu-id="e1252-204">字串</span><span class="sxs-lookup"><span data-stu-id="e1252-204">string</span></span>  | <span data-ttu-id="e1252-205">否</span><span class="sxs-lookup"><span data-stu-id="e1252-205">no</span></span>       | <span data-ttu-id="e1252-206">SemVer 2.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="e1252-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="e1252-207">如果`prerelease`未提供，發行前版本套件中排除。</span><span class="sxs-lookup"><span data-stu-id="e1252-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e1252-208">`semVerLevel`查詢參數用來選擇加入的 SemVer 2.0.0 套件。</span><span class="sxs-lookup"><span data-stu-id="e1252-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="e1252-209">如果此查詢參數被排除後，就會傳回只 SemVer 1.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="e1252-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="e1252-210">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 版本將會傳回。</span><span class="sxs-lookup"><span data-stu-id="e1252-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="e1252-211">請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e1252-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e1252-212">回應</span><span class="sxs-lookup"><span data-stu-id="e1252-212">Response</span></span>

<span data-ttu-id="e1252-213">回應是 JSON 文件包含所有的篩選指定的查詢參數所提供的封裝識別碼的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="e1252-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="e1252-214">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e1252-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="e1252-215">名稱</span><span class="sxs-lookup"><span data-stu-id="e1252-215">Name</span></span>      | <span data-ttu-id="e1252-216">類型</span><span class="sxs-lookup"><span data-stu-id="e1252-216">Type</span></span>             | <span data-ttu-id="e1252-217">必要</span><span class="sxs-lookup"><span data-stu-id="e1252-217">Required</span></span> | <span data-ttu-id="e1252-218">注意</span><span class="sxs-lookup"><span data-stu-id="e1252-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e1252-219">資料</span><span class="sxs-lookup"><span data-stu-id="e1252-219">data</span></span>      | <span data-ttu-id="e1252-220">字串陣列</span><span class="sxs-lookup"><span data-stu-id="e1252-220">array of strings</span></span> | <span data-ttu-id="e1252-221">是</span><span class="sxs-lookup"><span data-stu-id="e1252-221">yes</span></span>      | <span data-ttu-id="e1252-222">比對要求的套件版本</span><span class="sxs-lookup"><span data-stu-id="e1252-222">The package versions matched by the request</span></span>

<span data-ttu-id="e1252-223">中的套件版本`data`陣列可能包含 SemVer 2.0.0 組建中繼資料 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`提供查詢字串中。</span><span class="sxs-lookup"><span data-stu-id="e1252-223">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e1252-224">範例要求</span><span class="sxs-lookup"><span data-stu-id="e1252-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e1252-225">範例回應</span><span class="sxs-lookup"><span data-stu-id="e1252-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
