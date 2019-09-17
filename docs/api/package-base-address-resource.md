---
title: 套件內容，NuGet API
description: 封裝基底位址是一個簡單的介面，可供提取封裝本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488225"
---
# <a name="package-content"></a><span data-ttu-id="86d07-103">封裝內容</span><span class="sxs-lookup"><span data-stu-id="86d07-103">Package Content</span></span>

<span data-ttu-id="86d07-104">您可以使用 V3 API 來產生 URL，以提取任意套件的內容（nupkg 檔案）。</span><span class="sxs-lookup"><span data-stu-id="86d07-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="86d07-105">用來提取封裝內容的資源是`PackageBaseAddress`在[服務索引](service-index.md)中找到的資源。</span><span class="sxs-lookup"><span data-stu-id="86d07-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="86d07-106">此資源也可讓您探索已列出或未列出的所有套件版本。</span><span class="sxs-lookup"><span data-stu-id="86d07-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="86d07-107">這項資源通常稱為「套件基底位址」或「平面容器」。</span><span class="sxs-lookup"><span data-stu-id="86d07-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="86d07-108">版本控制</span><span class="sxs-lookup"><span data-stu-id="86d07-108">Versioning</span></span>

<span data-ttu-id="86d07-109">會使用`@type`下列值：</span><span class="sxs-lookup"><span data-stu-id="86d07-109">The following `@type` value is used:</span></span>

<span data-ttu-id="86d07-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="86d07-110">@type value</span></span>              | <span data-ttu-id="86d07-111">注意</span><span class="sxs-lookup"><span data-stu-id="86d07-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="86d07-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="86d07-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="86d07-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="86d07-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="86d07-114">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="86d07-114">Base URL</span></span>

<span data-ttu-id="86d07-115">下列 api 的基底 URL 是與上述資源`@id` `@type`值相關聯的屬性值。</span><span class="sxs-lookup"><span data-stu-id="86d07-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="86d07-116">在下列檔中，將會使用預留位置`{@id}`基底 URL。</span><span class="sxs-lookup"><span data-stu-id="86d07-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="86d07-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="86d07-117">HTTP methods</span></span>

<span data-ttu-id="86d07-118">在註冊資源中找到的所有 url 都支援 HTTP `GET`方法`HEAD`和。</span><span class="sxs-lookup"><span data-stu-id="86d07-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="86d07-119">列舉封裝版本</span><span class="sxs-lookup"><span data-stu-id="86d07-119">Enumerate package versions</span></span>

<span data-ttu-id="86d07-120">如果用戶端知道套件識別碼，而且想要探索封裝來源可用的封裝版本，用戶端可以建立可預測的 URL 來列舉所有套件版本。</span><span class="sxs-lookup"><span data-stu-id="86d07-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="86d07-121">這份清單應該是下面所述套件內容 API 的「目錄清單」。</span><span class="sxs-lookup"><span data-stu-id="86d07-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="86d07-122">這份清單同時包含列出和未列出的套件版本。</span><span class="sxs-lookup"><span data-stu-id="86d07-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="86d07-123">要求參數</span><span class="sxs-lookup"><span data-stu-id="86d07-123">Request parameters</span></span>

<span data-ttu-id="86d07-124">名稱</span><span class="sxs-lookup"><span data-stu-id="86d07-124">Name</span></span>     | <span data-ttu-id="86d07-125">In</span><span class="sxs-lookup"><span data-stu-id="86d07-125">In</span></span>     | <span data-ttu-id="86d07-126">類型</span><span class="sxs-lookup"><span data-stu-id="86d07-126">Type</span></span>    | <span data-ttu-id="86d07-127">必要</span><span class="sxs-lookup"><span data-stu-id="86d07-127">Required</span></span> | <span data-ttu-id="86d07-128">注意</span><span class="sxs-lookup"><span data-stu-id="86d07-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="86d07-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="86d07-129">LOWER_ID</span></span> | <span data-ttu-id="86d07-130">URL</span><span class="sxs-lookup"><span data-stu-id="86d07-130">URL</span></span>    | <span data-ttu-id="86d07-131">字串</span><span class="sxs-lookup"><span data-stu-id="86d07-131">string</span></span>  | <span data-ttu-id="86d07-132">是</span><span class="sxs-lookup"><span data-stu-id="86d07-132">yes</span></span>      | <span data-ttu-id="86d07-133">封裝識別碼，小寫</span><span class="sxs-lookup"><span data-stu-id="86d07-133">The package ID, lowercase</span></span>

<span data-ttu-id="86d07-134">`LOWER_ID`值是所需的套件識別碼小寫，使用由所執行的規則。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="86d07-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="86d07-135">回應</span><span class="sxs-lookup"><span data-stu-id="86d07-135">Response</span></span>

<span data-ttu-id="86d07-136">如果封裝來源沒有提供的套件識別碼版本，則會傳回404狀態碼。</span><span class="sxs-lookup"><span data-stu-id="86d07-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="86d07-137">如果封裝來源有一或多個版本，則會傳回200狀態碼。</span><span class="sxs-lookup"><span data-stu-id="86d07-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="86d07-138">回應主體是具有下列屬性的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="86d07-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="86d07-139">名稱</span><span class="sxs-lookup"><span data-stu-id="86d07-139">Name</span></span>     | <span data-ttu-id="86d07-140">類型</span><span class="sxs-lookup"><span data-stu-id="86d07-140">Type</span></span>             | <span data-ttu-id="86d07-141">必要</span><span class="sxs-lookup"><span data-stu-id="86d07-141">Required</span></span> | <span data-ttu-id="86d07-142">注意</span><span class="sxs-lookup"><span data-stu-id="86d07-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="86d07-143">版本</span><span class="sxs-lookup"><span data-stu-id="86d07-143">versions</span></span> | <span data-ttu-id="86d07-144">字串陣列</span><span class="sxs-lookup"><span data-stu-id="86d07-144">array of strings</span></span> | <span data-ttu-id="86d07-145">是</span><span class="sxs-lookup"><span data-stu-id="86d07-145">yes</span></span>      | <span data-ttu-id="86d07-146">可用的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="86d07-146">The package IDs available</span></span>

<span data-ttu-id="86d07-147">`versions`陣列中的字串都是小寫、[正規化的 NuGet 版本字串](../concepts/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="86d07-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="86d07-148">版本字串不包含任何 SemVer 的2.0.0 組建中繼資料。</span><span class="sxs-lookup"><span data-stu-id="86d07-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="86d07-149">其目的是在此陣列中找到的版本字串可以逐字用於下列端點中`LOWER_VERSION`找到的權杖。</span><span class="sxs-lookup"><span data-stu-id="86d07-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="86d07-150">範例要求</span><span class="sxs-lookup"><span data-stu-id="86d07-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="86d07-151">範例回應</span><span class="sxs-lookup"><span data-stu-id="86d07-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="86d07-152">下載套件內容（. nupkg）</span><span class="sxs-lookup"><span data-stu-id="86d07-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="86d07-153">如果用戶端知道套件識別碼和版本，而且想要下載封裝內容，則只需要建立下列 URL：</span><span class="sxs-lookup"><span data-stu-id="86d07-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="86d07-154">要求參數</span><span class="sxs-lookup"><span data-stu-id="86d07-154">Request parameters</span></span>

<span data-ttu-id="86d07-155">名稱</span><span class="sxs-lookup"><span data-stu-id="86d07-155">Name</span></span>          | <span data-ttu-id="86d07-156">In</span><span class="sxs-lookup"><span data-stu-id="86d07-156">In</span></span>     | <span data-ttu-id="86d07-157">類型</span><span class="sxs-lookup"><span data-stu-id="86d07-157">Type</span></span>   | <span data-ttu-id="86d07-158">必要</span><span class="sxs-lookup"><span data-stu-id="86d07-158">Required</span></span> | <span data-ttu-id="86d07-159">注意</span><span class="sxs-lookup"><span data-stu-id="86d07-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="86d07-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="86d07-160">LOWER_ID</span></span>      | <span data-ttu-id="86d07-161">URL</span><span class="sxs-lookup"><span data-stu-id="86d07-161">URL</span></span>    | <span data-ttu-id="86d07-162">字串</span><span class="sxs-lookup"><span data-stu-id="86d07-162">string</span></span> | <span data-ttu-id="86d07-163">是</span><span class="sxs-lookup"><span data-stu-id="86d07-163">yes</span></span>      | <span data-ttu-id="86d07-164">封裝識別碼，小寫</span><span class="sxs-lookup"><span data-stu-id="86d07-164">The package ID, lowercase</span></span>
<span data-ttu-id="86d07-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="86d07-165">LOWER_VERSION</span></span> | <span data-ttu-id="86d07-166">URL</span><span class="sxs-lookup"><span data-stu-id="86d07-166">URL</span></span>    | <span data-ttu-id="86d07-167">字串</span><span class="sxs-lookup"><span data-stu-id="86d07-167">string</span></span> | <span data-ttu-id="86d07-168">是</span><span class="sxs-lookup"><span data-stu-id="86d07-168">yes</span></span>      | <span data-ttu-id="86d07-169">封裝版本，正規化和小寫</span><span class="sxs-lookup"><span data-stu-id="86d07-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="86d07-170">`LOWER_ID` 和`LOWER_VERSION`都是使用所執行的規則小寫。NET[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="86d07-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="86d07-171">方法。</span><span class="sxs-lookup"><span data-stu-id="86d07-171">method.</span></span>

<span data-ttu-id="86d07-172">`LOWER_VERSION` 是使用 NuGet 版本[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)標準化的所需套件版本。</span><span class="sxs-lookup"><span data-stu-id="86d07-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="86d07-173">這表示在此情況下，必須排除 SemVer 2.0.0 規格所允許的組建中繼資料。</span><span class="sxs-lookup"><span data-stu-id="86d07-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="86d07-174">回應本文</span><span class="sxs-lookup"><span data-stu-id="86d07-174">Response body</span></span>

<span data-ttu-id="86d07-175">如果封裝存在於套件來源上，則會傳回200狀態碼。</span><span class="sxs-lookup"><span data-stu-id="86d07-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="86d07-176">回應主體將會是封裝內容本身。</span><span class="sxs-lookup"><span data-stu-id="86d07-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="86d07-177">如果封裝不存在於套件來源上，則會傳回404狀態碼。</span><span class="sxs-lookup"><span data-stu-id="86d07-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="86d07-178">範例要求</span><span class="sxs-lookup"><span data-stu-id="86d07-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="86d07-179">範例回應</span><span class="sxs-lookup"><span data-stu-id="86d07-179">Sample response</span></span>

<span data-ttu-id="86d07-180">二進位資料流程，也就是 Newtonsoft 的 nupkg。</span><span class="sxs-lookup"><span data-stu-id="86d07-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="86d07-181">下載套件資訊清單（. nuspec）</span><span class="sxs-lookup"><span data-stu-id="86d07-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="86d07-182">如果用戶端知道套件識別碼和版本，而且想要下載套件資訊清單，他們只需要建立下列 URL：</span><span class="sxs-lookup"><span data-stu-id="86d07-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="86d07-183">要求參數</span><span class="sxs-lookup"><span data-stu-id="86d07-183">Request parameters</span></span>

<span data-ttu-id="86d07-184">名稱</span><span class="sxs-lookup"><span data-stu-id="86d07-184">Name</span></span>          | <span data-ttu-id="86d07-185">In</span><span class="sxs-lookup"><span data-stu-id="86d07-185">In</span></span>     | <span data-ttu-id="86d07-186">類型</span><span class="sxs-lookup"><span data-stu-id="86d07-186">Type</span></span>   | <span data-ttu-id="86d07-187">必要</span><span class="sxs-lookup"><span data-stu-id="86d07-187">Required</span></span> | <span data-ttu-id="86d07-188">注意</span><span class="sxs-lookup"><span data-stu-id="86d07-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="86d07-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="86d07-189">LOWER_ID</span></span>      | <span data-ttu-id="86d07-190">URL</span><span class="sxs-lookup"><span data-stu-id="86d07-190">URL</span></span>    | <span data-ttu-id="86d07-191">字串</span><span class="sxs-lookup"><span data-stu-id="86d07-191">string</span></span> | <span data-ttu-id="86d07-192">是</span><span class="sxs-lookup"><span data-stu-id="86d07-192">yes</span></span>      | <span data-ttu-id="86d07-193">封裝識別碼，小寫</span><span class="sxs-lookup"><span data-stu-id="86d07-193">The package ID, lowercase</span></span>
<span data-ttu-id="86d07-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="86d07-194">LOWER_VERSION</span></span> | <span data-ttu-id="86d07-195">URL</span><span class="sxs-lookup"><span data-stu-id="86d07-195">URL</span></span>    | <span data-ttu-id="86d07-196">字串</span><span class="sxs-lookup"><span data-stu-id="86d07-196">string</span></span> | <span data-ttu-id="86d07-197">是</span><span class="sxs-lookup"><span data-stu-id="86d07-197">yes</span></span>      | <span data-ttu-id="86d07-198">封裝版本，正規化和小寫</span><span class="sxs-lookup"><span data-stu-id="86d07-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="86d07-199">`LOWER_ID` 和`LOWER_VERSION`都是使用所執行的規則小寫。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="86d07-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="86d07-200">`LOWER_VERSION` 是使用 NuGet 版本[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)標準化的所需套件版本。</span><span class="sxs-lookup"><span data-stu-id="86d07-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="86d07-201">這表示在此情況下，必須排除 SemVer 2.0.0 規格所允許的組建中繼資料。</span><span class="sxs-lookup"><span data-stu-id="86d07-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="86d07-202">回應本文</span><span class="sxs-lookup"><span data-stu-id="86d07-202">Response body</span></span>

<span data-ttu-id="86d07-203">如果封裝存在於套件來源上，則會傳回200狀態碼。</span><span class="sxs-lookup"><span data-stu-id="86d07-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="86d07-204">回應主體將會是封裝資訊清單，也就是包含在對應 nupkg 中的 nuspec。</span><span class="sxs-lookup"><span data-stu-id="86d07-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="86d07-205">Nuspec 是一份 XML 檔。</span><span class="sxs-lookup"><span data-stu-id="86d07-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="86d07-206">如果封裝不存在於套件來源上，則會傳回404狀態碼。</span><span class="sxs-lookup"><span data-stu-id="86d07-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="86d07-207">範例要求</span><span class="sxs-lookup"><span data-stu-id="86d07-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="86d07-208">範例回應</span><span class="sxs-lookup"><span data-stu-id="86d07-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
