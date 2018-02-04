---
title: "封裝的內容，NuGet API |Microsoft 文件"
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
description: "封裝的基底位址是一個簡單的介面，以擷取封裝本身。"
keywords: "NuGet 的一般容器、 NuGet 封裝基底地址、 NuGet nupkg API，API NuGet 套件的版本中，NuGet API 未列出的套件，NuGet API 下載 nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="10775-104">封裝內容</span><span class="sxs-lookup"><span data-stu-id="10775-104">Package Content</span></span>

<span data-ttu-id="10775-105">很可能產生的 URL 來擷取使用 V3 應用程式開發介面的任意套件的內容 （.nupkg 檔案）。</span><span class="sxs-lookup"><span data-stu-id="10775-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="10775-106">用於擷取套件內容的資源是`PackageBaseAddress`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="10775-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="10775-107">此資源也可讓封裝時，所列出的所有版本的探索或未列出。</span><span class="sxs-lookup"><span data-stu-id="10775-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="10775-108">此資源通常稱為為任一個 「 封裝基底位址 」 或 「 一般容器 >。</span><span class="sxs-lookup"><span data-stu-id="10775-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="10775-109">版本控制</span><span class="sxs-lookup"><span data-stu-id="10775-109">Versioning</span></span>

<span data-ttu-id="10775-110">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="10775-110">The following `@type` value is used:</span></span>

<span data-ttu-id="10775-111">@type 值</span><span class="sxs-lookup"><span data-stu-id="10775-111">@type value</span></span>              | <span data-ttu-id="10775-112">注意</span><span class="sxs-lookup"><span data-stu-id="10775-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="10775-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="10775-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="10775-114">初版</span><span class="sxs-lookup"><span data-stu-id="10775-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="10775-115">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="10775-115">Base URL</span></span>

<span data-ttu-id="10775-116">下列應用程式開發介面的基底 URL 是值`@id`上述資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="10775-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="10775-117">下列文件預留位置基底 URL`{@id}`將使用。</span><span class="sxs-lookup"><span data-stu-id="10775-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="10775-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="10775-118">HTTP methods</span></span>

<span data-ttu-id="10775-119">位於登錄資源支援的 HTTP 方法的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="10775-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="10775-120">列舉封裝版本</span><span class="sxs-lookup"><span data-stu-id="10775-120">Enumerate package versions</span></span>

<span data-ttu-id="10775-121">如果用戶端知道封裝識別碼，而且想要探索的封裝版本的封裝來源可供使用，用戶端可以建構列舉所有的封裝版本的可預測的 URL。</span><span class="sxs-lookup"><span data-stu-id="10775-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="10775-122">這份清單會是用來 「 目錄清單 」，如下所述的套件內容 api。</span><span class="sxs-lookup"><span data-stu-id="10775-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="10775-123">此清單包含兩個列出與未列出的套件版本。</span><span class="sxs-lookup"><span data-stu-id="10775-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="10775-124">要求參數</span><span class="sxs-lookup"><span data-stu-id="10775-124">Request parameters</span></span>

<span data-ttu-id="10775-125">名稱</span><span class="sxs-lookup"><span data-stu-id="10775-125">Name</span></span>     | <span data-ttu-id="10775-126">In</span><span class="sxs-lookup"><span data-stu-id="10775-126">In</span></span>     | <span data-ttu-id="10775-127">類型</span><span class="sxs-lookup"><span data-stu-id="10775-127">Type</span></span>    | <span data-ttu-id="10775-128">必要</span><span class="sxs-lookup"><span data-stu-id="10775-128">Required</span></span> | <span data-ttu-id="10775-129">注意</span><span class="sxs-lookup"><span data-stu-id="10775-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="10775-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="10775-130">LOWER_ID</span></span> | <span data-ttu-id="10775-131">URL</span><span class="sxs-lookup"><span data-stu-id="10775-131">URL</span></span>    | <span data-ttu-id="10775-132">字串</span><span class="sxs-lookup"><span data-stu-id="10775-132">string</span></span>  | <span data-ttu-id="10775-133">是</span><span class="sxs-lookup"><span data-stu-id="10775-133">yes</span></span>      | <span data-ttu-id="10775-134">封裝識別碼、 小寫</span><span class="sxs-lookup"><span data-stu-id="10775-134">The package ID, lowercase</span></span>

<span data-ttu-id="10775-135">`LOWER_ID`值是小寫使用所實作的規則所需的封裝識別碼。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="10775-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="10775-136">回應</span><span class="sxs-lookup"><span data-stu-id="10775-136">Response</span></span>

<span data-ttu-id="10775-137">如果套件來源已不提供的封裝識別碼的版本，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="10775-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="10775-138">如果套件來源具有一個或多個版本，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="10775-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="10775-139">回應主體是使用下列屬性的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="10775-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="10775-140">名稱</span><span class="sxs-lookup"><span data-stu-id="10775-140">Name</span></span>     | <span data-ttu-id="10775-141">類型</span><span class="sxs-lookup"><span data-stu-id="10775-141">Type</span></span>             | <span data-ttu-id="10775-142">必要</span><span class="sxs-lookup"><span data-stu-id="10775-142">Required</span></span> | <span data-ttu-id="10775-143">注意</span><span class="sxs-lookup"><span data-stu-id="10775-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="10775-144">版本</span><span class="sxs-lookup"><span data-stu-id="10775-144">versions</span></span> | <span data-ttu-id="10775-145">字串陣列</span><span class="sxs-lookup"><span data-stu-id="10775-145">array of strings</span></span> | <span data-ttu-id="10775-146">是</span><span class="sxs-lookup"><span data-stu-id="10775-146">yes</span></span>      | <span data-ttu-id="10775-147">封裝識別碼可用</span><span class="sxs-lookup"><span data-stu-id="10775-147">The package IDs available</span></span>

<span data-ttu-id="10775-148">中的字串`versions`所有小寫陣列，[正規化 NuGet 版本字串](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="10775-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="10775-149">版本字串不包含任何 SemVer 2.0.0 建置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="10775-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="10775-150">其目的是，這個陣列中找到的版本字串可以用於逐字`LOWER_VERSION`下列端點中找到的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="10775-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="10775-151">範例要求</span><span class="sxs-lookup"><span data-stu-id="10775-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="10775-152">範例回應</span><span class="sxs-lookup"><span data-stu-id="10775-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="10775-153">下載封裝內容 (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="10775-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="10775-154">如果用戶端知道套件識別碼和版本，而且想要下載封裝內容，他們只需要建構下列 URL:</span><span class="sxs-lookup"><span data-stu-id="10775-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="10775-155">要求參數</span><span class="sxs-lookup"><span data-stu-id="10775-155">Request parameters</span></span>

<span data-ttu-id="10775-156">名稱</span><span class="sxs-lookup"><span data-stu-id="10775-156">Name</span></span>          | <span data-ttu-id="10775-157">In</span><span class="sxs-lookup"><span data-stu-id="10775-157">In</span></span>     | <span data-ttu-id="10775-158">類型</span><span class="sxs-lookup"><span data-stu-id="10775-158">Type</span></span>   | <span data-ttu-id="10775-159">必要</span><span class="sxs-lookup"><span data-stu-id="10775-159">Required</span></span> | <span data-ttu-id="10775-160">注意</span><span class="sxs-lookup"><span data-stu-id="10775-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="10775-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="10775-161">LOWER_ID</span></span>      | <span data-ttu-id="10775-162">URL</span><span class="sxs-lookup"><span data-stu-id="10775-162">URL</span></span>    | <span data-ttu-id="10775-163">字串</span><span class="sxs-lookup"><span data-stu-id="10775-163">string</span></span> | <span data-ttu-id="10775-164">是</span><span class="sxs-lookup"><span data-stu-id="10775-164">yes</span></span>      | <span data-ttu-id="10775-165">封裝識別碼、 小寫</span><span class="sxs-lookup"><span data-stu-id="10775-165">The package ID, lowercase</span></span>
<span data-ttu-id="10775-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="10775-166">LOWER_VERSION</span></span> | <span data-ttu-id="10775-167">URL</span><span class="sxs-lookup"><span data-stu-id="10775-167">URL</span></span>    | <span data-ttu-id="10775-168">字串</span><span class="sxs-lookup"><span data-stu-id="10775-168">string</span></span> | <span data-ttu-id="10775-169">是</span><span class="sxs-lookup"><span data-stu-id="10775-169">yes</span></span>      | <span data-ttu-id="10775-170">封裝版本，正規化和小寫</span><span class="sxs-lookup"><span data-stu-id="10775-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="10775-171">同時`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="10775-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="10775-172">`LOWER_VERSION`所需的封裝版本都是使用 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="10775-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="10775-173">這表示，允許使用 SemVer 2.0.0 規格的建置中繼資料，必須排除在此情況下。</span><span class="sxs-lookup"><span data-stu-id="10775-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="10775-174">回應本文</span><span class="sxs-lookup"><span data-stu-id="10775-174">Response body</span></span>

<span data-ttu-id="10775-175">如果封裝存在於封裝來源，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="10775-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="10775-176">回應主體會將封裝內容本身。</span><span class="sxs-lookup"><span data-stu-id="10775-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="10775-177">如果封裝不存在套件來源上，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="10775-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="10775-178">範例要求</span><span class="sxs-lookup"><span data-stu-id="10775-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="10775-179">範例回應</span><span class="sxs-lookup"><span data-stu-id="10775-179">Sample response</span></span>

<span data-ttu-id="10775-180">表示如 Newtonsoft.Json 9.0.1.nupkg 二進位資料流。</span><span class="sxs-lookup"><span data-stu-id="10775-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="10775-181">下載封裝資訊清單 (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="10775-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="10775-182">如果用戶端知道套件識別碼和版本，而且想要下載的封裝資訊清單，只需要建構下列 URL:</span><span class="sxs-lookup"><span data-stu-id="10775-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="10775-183">要求參數</span><span class="sxs-lookup"><span data-stu-id="10775-183">Request parameters</span></span>

<span data-ttu-id="10775-184">名稱</span><span class="sxs-lookup"><span data-stu-id="10775-184">Name</span></span>          | <span data-ttu-id="10775-185">In</span><span class="sxs-lookup"><span data-stu-id="10775-185">In</span></span>     | <span data-ttu-id="10775-186">類型</span><span class="sxs-lookup"><span data-stu-id="10775-186">Type</span></span>    | <span data-ttu-id="10775-187">必要</span><span class="sxs-lookup"><span data-stu-id="10775-187">Required</span></span> | <span data-ttu-id="10775-188">注意</span><span class="sxs-lookup"><span data-stu-id="10775-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="10775-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="10775-189">LOWER_ID</span></span>      | <span data-ttu-id="10775-190">URL</span><span class="sxs-lookup"><span data-stu-id="10775-190">URL</span></span>    | <span data-ttu-id="10775-191">字串</span><span class="sxs-lookup"><span data-stu-id="10775-191">string</span></span>  | <span data-ttu-id="10775-192">是</span><span class="sxs-lookup"><span data-stu-id="10775-192">yes</span></span>      | <span data-ttu-id="10775-193">封裝識別碼、 小寫</span><span class="sxs-lookup"><span data-stu-id="10775-193">The package ID, lowercase</span></span>
<span data-ttu-id="10775-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="10775-194">LOWER_VERSION</span></span> | <span data-ttu-id="10775-195">URL</span><span class="sxs-lookup"><span data-stu-id="10775-195">URL</span></span>    | <span data-ttu-id="10775-196">整數</span><span class="sxs-lookup"><span data-stu-id="10775-196">integer</span></span> | <span data-ttu-id="10775-197">是</span><span class="sxs-lookup"><span data-stu-id="10775-197">yes</span></span>      | <span data-ttu-id="10775-198">封裝版本，正規化和小寫</span><span class="sxs-lookup"><span data-stu-id="10775-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="10775-199">同時`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。網路的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="10775-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="10775-200">`LOWER_VERSION`所需的封裝版本都是使用 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="10775-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="10775-201">這表示，允許使用 SemVer 2.0.0 規格的建置中繼資料，必須排除在此情況下。</span><span class="sxs-lookup"><span data-stu-id="10775-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="10775-202">回應本文</span><span class="sxs-lookup"><span data-stu-id="10775-202">Response body</span></span>

<span data-ttu-id="10775-203">如果封裝存在於封裝來源，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="10775-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="10775-204">回應主體會是包含在對應的.nupkg.nuspec 封裝資訊清單。</span><span class="sxs-lookup"><span data-stu-id="10775-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="10775-205">.nuspec 是 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="10775-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="10775-206">如果封裝不存在套件來源上，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="10775-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="10775-207">範例要求</span><span class="sxs-lookup"><span data-stu-id="10775-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="10775-208">範例回應</span><span class="sxs-lookup"><span data-stu-id="10775-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
