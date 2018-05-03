---
title: 內容套件，NuGet API
description: 封裝的基底位址是一個簡單的介面，以擷取封裝本身。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a><span data-ttu-id="a1775-103">封裝內容</span><span class="sxs-lookup"><span data-stu-id="a1775-103">Package Content</span></span>

<span data-ttu-id="a1775-104">很可能產生的 URL 來擷取使用 V3 應用程式開發介面的任意套件的內容 （.nupkg 檔案）。</span><span class="sxs-lookup"><span data-stu-id="a1775-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="a1775-105">用於擷取套件內容的資源是`PackageBaseAddress`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="a1775-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="a1775-106">此資源也可讓封裝時，所列出的所有版本的探索或未列出。</span><span class="sxs-lookup"><span data-stu-id="a1775-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="a1775-107">此資源通常稱為為任一個 「 封裝基底位址 」 或 「 一般容器 >。</span><span class="sxs-lookup"><span data-stu-id="a1775-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="a1775-108">版本控制</span><span class="sxs-lookup"><span data-stu-id="a1775-108">Versioning</span></span>

<span data-ttu-id="a1775-109">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="a1775-109">The following `@type` value is used:</span></span>

<span data-ttu-id="a1775-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="a1775-110">@type value</span></span>              | <span data-ttu-id="a1775-111">注意</span><span class="sxs-lookup"><span data-stu-id="a1775-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="a1775-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="a1775-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="a1775-113">初版</span><span class="sxs-lookup"><span data-stu-id="a1775-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="a1775-114">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="a1775-114">Base URL</span></span>

<span data-ttu-id="a1775-115">下列應用程式開發介面的基底 URL 是值`@id`上述資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="a1775-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="a1775-116">下列文件預留位置基底 URL`{@id}`將使用。</span><span class="sxs-lookup"><span data-stu-id="a1775-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a1775-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="a1775-117">HTTP methods</span></span>

<span data-ttu-id="a1775-118">位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="a1775-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="a1775-119">列舉封裝版本</span><span class="sxs-lookup"><span data-stu-id="a1775-119">Enumerate package versions</span></span>

<span data-ttu-id="a1775-120">如果用戶端知道封裝識別碼，而且想要探索的封裝版本的封裝來源可供使用，用戶端可以建構列舉所有的封裝版本的可預測的 URL。</span><span class="sxs-lookup"><span data-stu-id="a1775-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="a1775-121">這份清單會是用來 「 目錄清單 」，如下所述的套件內容 api。</span><span class="sxs-lookup"><span data-stu-id="a1775-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="a1775-122">此清單包含兩個列出與未列出的套件版本。</span><span class="sxs-lookup"><span data-stu-id="a1775-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="a1775-123">要求參數</span><span class="sxs-lookup"><span data-stu-id="a1775-123">Request parameters</span></span>

<span data-ttu-id="a1775-124">名稱</span><span class="sxs-lookup"><span data-stu-id="a1775-124">Name</span></span>     | <span data-ttu-id="a1775-125">In</span><span class="sxs-lookup"><span data-stu-id="a1775-125">In</span></span>     | <span data-ttu-id="a1775-126">類型</span><span class="sxs-lookup"><span data-stu-id="a1775-126">Type</span></span>    | <span data-ttu-id="a1775-127">必要</span><span class="sxs-lookup"><span data-stu-id="a1775-127">Required</span></span> | <span data-ttu-id="a1775-128">注意</span><span class="sxs-lookup"><span data-stu-id="a1775-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="a1775-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a1775-129">LOWER_ID</span></span> | <span data-ttu-id="a1775-130">URL</span><span class="sxs-lookup"><span data-stu-id="a1775-130">URL</span></span>    | <span data-ttu-id="a1775-131">字串</span><span class="sxs-lookup"><span data-stu-id="a1775-131">string</span></span>  | <span data-ttu-id="a1775-132">是</span><span class="sxs-lookup"><span data-stu-id="a1775-132">yes</span></span>      | <span data-ttu-id="a1775-133">封裝識別碼、 小寫</span><span class="sxs-lookup"><span data-stu-id="a1775-133">The package ID, lowercase</span></span>

<span data-ttu-id="a1775-134">`LOWER_ID`值是小寫使用所實作的規則所需的封裝識別碼。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="a1775-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="a1775-135">回應</span><span class="sxs-lookup"><span data-stu-id="a1775-135">Response</span></span>

<span data-ttu-id="a1775-136">如果套件來源已不提供的封裝識別碼的版本，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="a1775-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="a1775-137">如果套件來源具有一個或多個版本，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="a1775-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="a1775-138">回應主體是使用下列屬性的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="a1775-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="a1775-139">名稱</span><span class="sxs-lookup"><span data-stu-id="a1775-139">Name</span></span>     | <span data-ttu-id="a1775-140">類型</span><span class="sxs-lookup"><span data-stu-id="a1775-140">Type</span></span>             | <span data-ttu-id="a1775-141">必要</span><span class="sxs-lookup"><span data-stu-id="a1775-141">Required</span></span> | <span data-ttu-id="a1775-142">注意</span><span class="sxs-lookup"><span data-stu-id="a1775-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="a1775-143">版本</span><span class="sxs-lookup"><span data-stu-id="a1775-143">versions</span></span> | <span data-ttu-id="a1775-144">字串陣列</span><span class="sxs-lookup"><span data-stu-id="a1775-144">array of strings</span></span> | <span data-ttu-id="a1775-145">是</span><span class="sxs-lookup"><span data-stu-id="a1775-145">yes</span></span>      | <span data-ttu-id="a1775-146">封裝識別碼可用</span><span class="sxs-lookup"><span data-stu-id="a1775-146">The package IDs available</span></span>

<span data-ttu-id="a1775-147">中的字串`versions`所有小寫陣列，[正規化 NuGet 版本字串](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="a1775-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a1775-148">版本字串不包含任何 SemVer 2.0.0 建置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a1775-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="a1775-149">其目的是，這個陣列中找到的版本字串可以用於逐字`LOWER_VERSION`下列端點中找到的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="a1775-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a1775-150">範例要求</span><span class="sxs-lookup"><span data-stu-id="a1775-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="a1775-151">範例回應</span><span class="sxs-lookup"><span data-stu-id="a1775-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="a1775-152">下載封裝內容 (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="a1775-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="a1775-153">如果用戶端知道套件識別碼和版本，而且想要下載封裝內容，他們只需要建構下列 URL:</span><span class="sxs-lookup"><span data-stu-id="a1775-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="a1775-154">要求參數</span><span class="sxs-lookup"><span data-stu-id="a1775-154">Request parameters</span></span>

<span data-ttu-id="a1775-155">名稱</span><span class="sxs-lookup"><span data-stu-id="a1775-155">Name</span></span>          | <span data-ttu-id="a1775-156">In</span><span class="sxs-lookup"><span data-stu-id="a1775-156">In</span></span>     | <span data-ttu-id="a1775-157">類型</span><span class="sxs-lookup"><span data-stu-id="a1775-157">Type</span></span>   | <span data-ttu-id="a1775-158">必要</span><span class="sxs-lookup"><span data-stu-id="a1775-158">Required</span></span> | <span data-ttu-id="a1775-159">注意</span><span class="sxs-lookup"><span data-stu-id="a1775-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="a1775-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a1775-160">LOWER_ID</span></span>      | <span data-ttu-id="a1775-161">URL</span><span class="sxs-lookup"><span data-stu-id="a1775-161">URL</span></span>    | <span data-ttu-id="a1775-162">字串</span><span class="sxs-lookup"><span data-stu-id="a1775-162">string</span></span> | <span data-ttu-id="a1775-163">是</span><span class="sxs-lookup"><span data-stu-id="a1775-163">yes</span></span>      | <span data-ttu-id="a1775-164">封裝識別碼、 小寫</span><span class="sxs-lookup"><span data-stu-id="a1775-164">The package ID, lowercase</span></span>
<span data-ttu-id="a1775-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="a1775-165">LOWER_VERSION</span></span> | <span data-ttu-id="a1775-166">URL</span><span class="sxs-lookup"><span data-stu-id="a1775-166">URL</span></span>    | <span data-ttu-id="a1775-167">字串</span><span class="sxs-lookup"><span data-stu-id="a1775-167">string</span></span> | <span data-ttu-id="a1775-168">是</span><span class="sxs-lookup"><span data-stu-id="a1775-168">yes</span></span>      | <span data-ttu-id="a1775-169">封裝版本，正規化和小寫</span><span class="sxs-lookup"><span data-stu-id="a1775-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="a1775-170">同時`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="a1775-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="a1775-171">`LOWER_VERSION`所需的封裝版本都是使用 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="a1775-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a1775-172">這表示，允許使用 SemVer 2.0.0 規格的建置中繼資料，必須排除在此情況下。</span><span class="sxs-lookup"><span data-stu-id="a1775-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="a1775-173">回應本文</span><span class="sxs-lookup"><span data-stu-id="a1775-173">Response body</span></span>

<span data-ttu-id="a1775-174">如果封裝存在於封裝來源，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="a1775-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="a1775-175">回應主體會將封裝內容本身。</span><span class="sxs-lookup"><span data-stu-id="a1775-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="a1775-176">如果封裝不存在套件來源上，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="a1775-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a1775-177">範例要求</span><span class="sxs-lookup"><span data-stu-id="a1775-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="a1775-178">範例回應</span><span class="sxs-lookup"><span data-stu-id="a1775-178">Sample response</span></span>

<span data-ttu-id="a1775-179">表示如 Newtonsoft.Json 9.0.1.nupkg 二進位資料流。</span><span class="sxs-lookup"><span data-stu-id="a1775-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="a1775-180">下載封裝資訊清單 (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="a1775-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="a1775-181">如果用戶端知道套件識別碼和版本，而且想要下載的封裝資訊清單，只需要建構下列 URL:</span><span class="sxs-lookup"><span data-stu-id="a1775-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="a1775-182">要求參數</span><span class="sxs-lookup"><span data-stu-id="a1775-182">Request parameters</span></span>

<span data-ttu-id="a1775-183">名稱</span><span class="sxs-lookup"><span data-stu-id="a1775-183">Name</span></span>          | <span data-ttu-id="a1775-184">In</span><span class="sxs-lookup"><span data-stu-id="a1775-184">In</span></span>     | <span data-ttu-id="a1775-185">類型</span><span class="sxs-lookup"><span data-stu-id="a1775-185">Type</span></span>    | <span data-ttu-id="a1775-186">必要</span><span class="sxs-lookup"><span data-stu-id="a1775-186">Required</span></span> | <span data-ttu-id="a1775-187">注意</span><span class="sxs-lookup"><span data-stu-id="a1775-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="a1775-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a1775-188">LOWER_ID</span></span>      | <span data-ttu-id="a1775-189">URL</span><span class="sxs-lookup"><span data-stu-id="a1775-189">URL</span></span>    | <span data-ttu-id="a1775-190">字串</span><span class="sxs-lookup"><span data-stu-id="a1775-190">string</span></span>  | <span data-ttu-id="a1775-191">是</span><span class="sxs-lookup"><span data-stu-id="a1775-191">yes</span></span>      | <span data-ttu-id="a1775-192">封裝識別碼、 小寫</span><span class="sxs-lookup"><span data-stu-id="a1775-192">The package ID, lowercase</span></span>
<span data-ttu-id="a1775-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="a1775-193">LOWER_VERSION</span></span> | <span data-ttu-id="a1775-194">URL</span><span class="sxs-lookup"><span data-stu-id="a1775-194">URL</span></span>    | <span data-ttu-id="a1775-195">整數</span><span class="sxs-lookup"><span data-stu-id="a1775-195">integer</span></span> | <span data-ttu-id="a1775-196">是</span><span class="sxs-lookup"><span data-stu-id="a1775-196">yes</span></span>      | <span data-ttu-id="a1775-197">封裝版本，正規化和小寫</span><span class="sxs-lookup"><span data-stu-id="a1775-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="a1775-198">同時`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="a1775-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="a1775-199">`LOWER_VERSION`所需的封裝版本都是使用 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="a1775-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a1775-200">這表示，允許使用 SemVer 2.0.0 規格的建置中繼資料，必須排除在此情況下。</span><span class="sxs-lookup"><span data-stu-id="a1775-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="a1775-201">回應本文</span><span class="sxs-lookup"><span data-stu-id="a1775-201">Response body</span></span>

<span data-ttu-id="a1775-202">如果封裝存在於封裝來源，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="a1775-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="a1775-203">回應主體會是包含在對應的.nupkg.nuspec 封裝資訊清單。</span><span class="sxs-lookup"><span data-stu-id="a1775-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="a1775-204">.nuspec 是 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="a1775-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="a1775-205">如果封裝不存在套件來源上，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="a1775-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a1775-206">範例要求</span><span class="sxs-lookup"><span data-stu-id="a1775-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="a1775-207">範例回應</span><span class="sxs-lookup"><span data-stu-id="a1775-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
