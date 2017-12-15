---
title: "自動完成，NuGet API |Microsoft 文件"
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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "搜尋 「 自動完成 」 服務支援互動式尋找的封裝識別碼和版本。"
keywords: "NuGet 自動完成應用程式開發介面、 NuGet 搜尋封裝識別碼、 子字串的套件識別碼"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a><span data-ttu-id="d9978-104">自動完成</span><span class="sxs-lookup"><span data-stu-id="d9978-104">Autocomplete</span></span>

<span data-ttu-id="d9978-105">它是可以建置的套件識別碼和版本自動完成體驗使用 V3 API。</span><span class="sxs-lookup"><span data-stu-id="d9978-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d9978-106">自動完成查詢所使用之資源是`SearchAutocompleteService`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="d9978-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d9978-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="d9978-107">Versioning</span></span>

<span data-ttu-id="d9978-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="d9978-108">The following `@type` values are used:</span></span>

<span data-ttu-id="d9978-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="d9978-109">@type value</span></span>                          | <span data-ttu-id="d9978-110">注意</span><span class="sxs-lookup"><span data-stu-id="d9978-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d9978-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d9978-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="d9978-112">初版</span><span class="sxs-lookup"><span data-stu-id="d9978-112">The initial release</span></span>
<span data-ttu-id="d9978-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d9978-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d9978-114">別名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d9978-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d9978-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d9978-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d9978-116">別名`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d9978-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="d9978-117">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="d9978-117">Base URL</span></span>

<span data-ttu-id="d9978-118">下列應用程式開發介面的基底 URL 是值`@id`與其中一個先前提及的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="d9978-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d9978-119">下列文件預留位置基底 URL`{@id}`將使用。</span><span class="sxs-lookup"><span data-stu-id="d9978-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d9978-120">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="d9978-120">HTTP Methods</span></span>

<span data-ttu-id="d9978-121">位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="d9978-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d9978-122">搜尋封裝 Id</span><span class="sxs-lookup"><span data-stu-id="d9978-122">Search for package IDs</span></span>

<span data-ttu-id="d9978-123">第一個自動完成應用程式開發介面支援搜尋的套件 ID 字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="d9978-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d9978-124">當您想要提供使用者介面整合在一起的 NuGet 封裝來源中的封裝 typeahead 功能時，這很適合。</span><span class="sxs-lookup"><span data-stu-id="d9978-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d9978-125">只有未列出的版本的封裝不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="d9978-125">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="d9978-126">要求參數</span><span class="sxs-lookup"><span data-stu-id="d9978-126">Request parameters</span></span>

<span data-ttu-id="d9978-127">名稱</span><span class="sxs-lookup"><span data-stu-id="d9978-127">Name</span></span>        | <span data-ttu-id="d9978-128">In</span><span class="sxs-lookup"><span data-stu-id="d9978-128">In</span></span>     | <span data-ttu-id="d9978-129">類型</span><span class="sxs-lookup"><span data-stu-id="d9978-129">Type</span></span>    | <span data-ttu-id="d9978-130">必要</span><span class="sxs-lookup"><span data-stu-id="d9978-130">Required</span></span> | <span data-ttu-id="d9978-131">注意</span><span class="sxs-lookup"><span data-stu-id="d9978-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d9978-132">q</span><span class="sxs-lookup"><span data-stu-id="d9978-132">q</span></span>           | <span data-ttu-id="d9978-133">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-133">URL</span></span>    | <span data-ttu-id="d9978-134">字串</span><span class="sxs-lookup"><span data-stu-id="d9978-134">string</span></span>  | <span data-ttu-id="d9978-135">no</span><span class="sxs-lookup"><span data-stu-id="d9978-135">no</span></span>       | <span data-ttu-id="d9978-136">要與封裝識別碼進行比較的字串</span><span class="sxs-lookup"><span data-stu-id="d9978-136">The string to compare against package IDs</span></span>
<span data-ttu-id="d9978-137">skip</span><span class="sxs-lookup"><span data-stu-id="d9978-137">skip</span></span>        | <span data-ttu-id="d9978-138">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-138">URL</span></span>    | <span data-ttu-id="d9978-139">整數</span><span class="sxs-lookup"><span data-stu-id="d9978-139">integer</span></span> | <span data-ttu-id="d9978-140">no</span><span class="sxs-lookup"><span data-stu-id="d9978-140">no</span></span>       | <span data-ttu-id="d9978-141">若要略過，針對分頁的結果數目</span><span class="sxs-lookup"><span data-stu-id="d9978-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d9978-142">take</span><span class="sxs-lookup"><span data-stu-id="d9978-142">take</span></span>        | <span data-ttu-id="d9978-143">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-143">URL</span></span>    | <span data-ttu-id="d9978-144">整數</span><span class="sxs-lookup"><span data-stu-id="d9978-144">integer</span></span> | <span data-ttu-id="d9978-145">no</span><span class="sxs-lookup"><span data-stu-id="d9978-145">no</span></span>       | <span data-ttu-id="d9978-146">若要傳回，針對分頁的結果數目</span><span class="sxs-lookup"><span data-stu-id="d9978-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="d9978-147">發行前版本</span><span class="sxs-lookup"><span data-stu-id="d9978-147">prerelease</span></span>  | <span data-ttu-id="d9978-148">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-148">URL</span></span>    | <span data-ttu-id="d9978-149">boolean</span><span class="sxs-lookup"><span data-stu-id="d9978-149">boolean</span></span> | <span data-ttu-id="d9978-150">no</span><span class="sxs-lookup"><span data-stu-id="d9978-150">no</span></span>       | <span data-ttu-id="d9978-151">`true`或`false`決定是否要包含[發行前版本的封裝](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d9978-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d9978-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d9978-152">semVerLevel</span></span> | <span data-ttu-id="d9978-153">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-153">URL</span></span>    | <span data-ttu-id="d9978-154">字串</span><span class="sxs-lookup"><span data-stu-id="d9978-154">string</span></span>  | <span data-ttu-id="d9978-155">no</span><span class="sxs-lookup"><span data-stu-id="d9978-155">no</span></span>       | <span data-ttu-id="d9978-156">SemVer 1.0.0 版本字串</span><span class="sxs-lookup"><span data-stu-id="d9978-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d9978-157">自動完成查詢`q`剖析的方式，由伺服器實作所定義。</span><span class="sxs-lookup"><span data-stu-id="d9978-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d9978-158">nuget.org 支援來查詢前置詞的封裝識別碼權杖是片段 spliting 所產生的識別碼，原始的 camel 命名法的大小寫和符號字元。</span><span class="sxs-lookup"><span data-stu-id="d9978-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d9978-159">`skip`參數預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="d9978-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d9978-160">`take`參數應該大於零的整數。</span><span class="sxs-lookup"><span data-stu-id="d9978-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d9978-161">伺服器實作可能會造成最大值。</span><span class="sxs-lookup"><span data-stu-id="d9978-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d9978-162">如果`prerelease`未提供，會排除發行前版本的封裝。</span><span class="sxs-lookup"><span data-stu-id="d9978-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d9978-163">`semVerLevel`查詢參數用來選擇加入以[SemVer 2.0.0 封裝](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。</span><span class="sxs-lookup"><span data-stu-id="d9978-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d9978-164">如果此查詢參數被排除後，將會傳回與 SemVer 1.0.0 相容版本的唯一封裝識別碼 (與[標準的 NuGet 版本控制](../reference/package-versioning.md)警告，例如 4 整數片段具有的版本字串)。</span><span class="sxs-lookup"><span data-stu-id="d9978-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d9978-165">如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 相容封裝將會傳回。</span><span class="sxs-lookup"><span data-stu-id="d9978-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d9978-166">請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d9978-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d9978-167">回應</span><span class="sxs-lookup"><span data-stu-id="d9978-167">Response</span></span>

<span data-ttu-id="d9978-168">回應是含有最多的 JSON 文件`take`自動完成的結果。</span><span class="sxs-lookup"><span data-stu-id="d9978-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d9978-169">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="d9978-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d9978-170">名稱</span><span class="sxs-lookup"><span data-stu-id="d9978-170">Name</span></span>      | <span data-ttu-id="d9978-171">類型</span><span class="sxs-lookup"><span data-stu-id="d9978-171">Type</span></span>             | <span data-ttu-id="d9978-172">必要</span><span class="sxs-lookup"><span data-stu-id="d9978-172">Required</span></span> | <span data-ttu-id="d9978-173">注意</span><span class="sxs-lookup"><span data-stu-id="d9978-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d9978-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="d9978-174">totalHits</span></span> | <span data-ttu-id="d9978-175">整數</span><span class="sxs-lookup"><span data-stu-id="d9978-175">integer</span></span>          | <span data-ttu-id="d9978-176">是</span><span class="sxs-lookup"><span data-stu-id="d9978-176">yes</span></span>      | <span data-ttu-id="d9978-177">總數的比對，正在略過`skip`和`take`</span><span class="sxs-lookup"><span data-stu-id="d9978-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d9978-178">資料</span><span class="sxs-lookup"><span data-stu-id="d9978-178">data</span></span>      | <span data-ttu-id="d9978-179">字串陣列</span><span class="sxs-lookup"><span data-stu-id="d9978-179">array of strings</span></span> | <span data-ttu-id="d9978-180">是</span><span class="sxs-lookup"><span data-stu-id="d9978-180">yes</span></span>      | <span data-ttu-id="d9978-181">封裝符合所要求的識別碼</span><span class="sxs-lookup"><span data-stu-id="d9978-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d9978-182">範例要求</span><span class="sxs-lookup"><span data-stu-id="d9978-182">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="d9978-183">範例回應</span><span class="sxs-lookup"><span data-stu-id="d9978-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d9978-184">列舉封裝版本</span><span class="sxs-lookup"><span data-stu-id="d9978-184">Enumerate package versions</span></span>

<span data-ttu-id="d9978-185">一旦找到套件識別碼使用先前的應用程式開發介面，用戶端可以使用自動完成應用程式開發介面來列舉封裝版本提供的封裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="d9978-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d9978-186">未列出的套件版本不會出現在結果中。</span><span class="sxs-lookup"><span data-stu-id="d9978-186">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="d9978-187">要求參數</span><span class="sxs-lookup"><span data-stu-id="d9978-187">Request parameters</span></span>

<span data-ttu-id="d9978-188">名稱</span><span class="sxs-lookup"><span data-stu-id="d9978-188">Name</span></span>        | <span data-ttu-id="d9978-189">In</span><span class="sxs-lookup"><span data-stu-id="d9978-189">In</span></span>     | <span data-ttu-id="d9978-190">類型</span><span class="sxs-lookup"><span data-stu-id="d9978-190">Type</span></span>    | <span data-ttu-id="d9978-191">必要</span><span class="sxs-lookup"><span data-stu-id="d9978-191">Required</span></span> | <span data-ttu-id="d9978-192">注意</span><span class="sxs-lookup"><span data-stu-id="d9978-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d9978-193">id</span><span class="sxs-lookup"><span data-stu-id="d9978-193">id</span></span>          | <span data-ttu-id="d9978-194">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-194">URL</span></span>    | <span data-ttu-id="d9978-195">字串</span><span class="sxs-lookup"><span data-stu-id="d9978-195">string</span></span>  | <span data-ttu-id="d9978-196">是</span><span class="sxs-lookup"><span data-stu-id="d9978-196">yes</span></span>      | <span data-ttu-id="d9978-197">要擷取的版本的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="d9978-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="d9978-198">發行前版本</span><span class="sxs-lookup"><span data-stu-id="d9978-198">prerelease</span></span>  | <span data-ttu-id="d9978-199">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-199">URL</span></span>    | <span data-ttu-id="d9978-200">boolean</span><span class="sxs-lookup"><span data-stu-id="d9978-200">boolean</span></span> | <span data-ttu-id="d9978-201">no</span><span class="sxs-lookup"><span data-stu-id="d9978-201">no</span></span>       | <span data-ttu-id="d9978-202">`true`或`false`決定是否要包含[發行前版本的封裝](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d9978-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d9978-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d9978-203">semVerLevel</span></span> | <span data-ttu-id="d9978-204">URL</span><span class="sxs-lookup"><span data-stu-id="d9978-204">URL</span></span>    | <span data-ttu-id="d9978-205">字串</span><span class="sxs-lookup"><span data-stu-id="d9978-205">string</span></span>  | <span data-ttu-id="d9978-206">no</span><span class="sxs-lookup"><span data-stu-id="d9978-206">no</span></span>       | <span data-ttu-id="d9978-207">SemVer 2.0.0 的版本字串</span><span class="sxs-lookup"><span data-stu-id="d9978-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d9978-208">如果`prerelease`未提供，會排除發行前版本的封裝。</span><span class="sxs-lookup"><span data-stu-id="d9978-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d9978-209">`semVerLevel`查詢參數用來選擇加入以 SemVer 2.0.0 的封裝。</span><span class="sxs-lookup"><span data-stu-id="d9978-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d9978-210">如果此查詢參數被排除後，將會傳回只 SemVer 1.0.0 版本。</span><span class="sxs-lookup"><span data-stu-id="d9978-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d9978-211">如果`semVerLevel=2.0.0`提供，將傳回 SemVer 1.0.0 和 SemVer 2.0.0 的版本。</span><span class="sxs-lookup"><span data-stu-id="d9978-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d9978-212">請參閱[nuget.org 的 SemVer 2.0.0 支援](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d9978-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d9978-213">回應</span><span class="sxs-lookup"><span data-stu-id="d9978-213">Response</span></span>

<span data-ttu-id="d9978-214">回應是包含所有的篩選指定的查詢參數所提供的封裝識別碼的封裝版本的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="d9978-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d9978-215">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="d9978-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="d9978-216">名稱</span><span class="sxs-lookup"><span data-stu-id="d9978-216">Name</span></span>      | <span data-ttu-id="d9978-217">類型</span><span class="sxs-lookup"><span data-stu-id="d9978-217">Type</span></span>             | <span data-ttu-id="d9978-218">必要</span><span class="sxs-lookup"><span data-stu-id="d9978-218">Required</span></span> | <span data-ttu-id="d9978-219">注意</span><span class="sxs-lookup"><span data-stu-id="d9978-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d9978-220">資料</span><span class="sxs-lookup"><span data-stu-id="d9978-220">data</span></span>      | <span data-ttu-id="d9978-221">字串陣列</span><span class="sxs-lookup"><span data-stu-id="d9978-221">array of strings</span></span> | <span data-ttu-id="d9978-222">是</span><span class="sxs-lookup"><span data-stu-id="d9978-222">yes</span></span>      | <span data-ttu-id="d9978-223">封裝版本要求所比對</span><span class="sxs-lookup"><span data-stu-id="d9978-223">The package versions matched by the request</span></span>

<span data-ttu-id="d9978-224">中的封裝版本`data`陣列可能包含 SemVer 2.0.0 建置中繼資料 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查詢字串中提供。</span><span class="sxs-lookup"><span data-stu-id="d9978-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d9978-225">範例要求</span><span class="sxs-lookup"><span data-stu-id="d9978-225">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="d9978-226">範例回應</span><span class="sxs-lookup"><span data-stu-id="d9978-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
