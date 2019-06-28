---
title: 封裝內容，NuGet API
description: 封裝的基底位址是一個簡單的介面，以擷取封裝本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426758"
---
# <a name="package-content"></a><span data-ttu-id="3ab27-103">封裝內容</span><span class="sxs-lookup"><span data-stu-id="3ab27-103">Package Content</span></span>

<span data-ttu-id="3ab27-104">可以產生 URL，以擷取使用 V3 API 的任意套件的內容 （.nupkg 檔案）。</span><span class="sxs-lookup"><span data-stu-id="3ab27-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="3ab27-105">用於擷取套件內容資源`PackageBaseAddress`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab27-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="3ab27-106">此資源也可讓封裝時，所列出的所有版本的探索或未列出。</span><span class="sxs-lookup"><span data-stu-id="3ab27-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="3ab27-107">此資源統稱為 「 封裝基底位址 」 或 「 一般容器 」。</span><span class="sxs-lookup"><span data-stu-id="3ab27-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="3ab27-108">版本控制</span><span class="sxs-lookup"><span data-stu-id="3ab27-108">Versioning</span></span>

<span data-ttu-id="3ab27-109">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="3ab27-109">The following `@type` value is used:</span></span>

<span data-ttu-id="3ab27-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="3ab27-110">@type value</span></span>              | <span data-ttu-id="3ab27-111">注意</span><span class="sxs-lookup"><span data-stu-id="3ab27-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="3ab27-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="3ab27-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="3ab27-113">初始版本</span><span class="sxs-lookup"><span data-stu-id="3ab27-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="3ab27-114">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="3ab27-114">Base URL</span></span>

<span data-ttu-id="3ab27-115">下列 Api 的基底 URL 是值`@id`上述的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="3ab27-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="3ab27-116">在下列的文件中的預留位置基底 URL`{@id}`將使用。</span><span class="sxs-lookup"><span data-stu-id="3ab27-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3ab27-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="3ab27-117">HTTP methods</span></span>

<span data-ttu-id="3ab27-118">所有 Url 的 HTTP 方法位於註冊資源的支援`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="3ab27-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="3ab27-119">列舉套件版本</span><span class="sxs-lookup"><span data-stu-id="3ab27-119">Enumerate package versions</span></span>

<span data-ttu-id="3ab27-120">如果用戶端知道的封裝識別碼，並想要探索的封裝版本的封裝來源可用，用戶端可以建構可預測的 URL 來列舉所有的套件版本。</span><span class="sxs-lookup"><span data-stu-id="3ab27-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="3ab27-121">這份清單會是用來 「 目錄清單 」，如下所述的套件內容 api。</span><span class="sxs-lookup"><span data-stu-id="3ab27-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="3ab27-122">此清單包含兩個列出與未列出的套件版本。</span><span class="sxs-lookup"><span data-stu-id="3ab27-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="3ab27-123">要求參數</span><span class="sxs-lookup"><span data-stu-id="3ab27-123">Request parameters</span></span>

<span data-ttu-id="3ab27-124">名稱</span><span class="sxs-lookup"><span data-stu-id="3ab27-124">Name</span></span>     | <span data-ttu-id="3ab27-125">In</span><span class="sxs-lookup"><span data-stu-id="3ab27-125">In</span></span>     | <span data-ttu-id="3ab27-126">類型</span><span class="sxs-lookup"><span data-stu-id="3ab27-126">Type</span></span>    | <span data-ttu-id="3ab27-127">必要</span><span class="sxs-lookup"><span data-stu-id="3ab27-127">Required</span></span> | <span data-ttu-id="3ab27-128">注意</span><span class="sxs-lookup"><span data-stu-id="3ab27-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="3ab27-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="3ab27-129">LOWER_ID</span></span> | <span data-ttu-id="3ab27-130">URL</span><span class="sxs-lookup"><span data-stu-id="3ab27-130">URL</span></span>    | <span data-ttu-id="3ab27-131">字串</span><span class="sxs-lookup"><span data-stu-id="3ab27-131">string</span></span>  | <span data-ttu-id="3ab27-132">是</span><span class="sxs-lookup"><span data-stu-id="3ab27-132">yes</span></span>      | <span data-ttu-id="3ab27-133">封裝識別碼、 小寫字母</span><span class="sxs-lookup"><span data-stu-id="3ab27-133">The package ID, lowercase</span></span>

<span data-ttu-id="3ab27-134">`LOWER_ID`值是小寫使用規則實作所需的套件識別碼。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="3ab27-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="3ab27-135">回應</span><span class="sxs-lookup"><span data-stu-id="3ab27-135">Response</span></span>

<span data-ttu-id="3ab27-136">如果套件來源不具有提供的套件識別碼的任何版本，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3ab27-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="3ab27-137">如果套件來源具有一個或多個版本，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3ab27-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="3ab27-138">回應主體是具有下列屬性的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="3ab27-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="3ab27-139">名稱</span><span class="sxs-lookup"><span data-stu-id="3ab27-139">Name</span></span>     | <span data-ttu-id="3ab27-140">類型</span><span class="sxs-lookup"><span data-stu-id="3ab27-140">Type</span></span>             | <span data-ttu-id="3ab27-141">必要</span><span class="sxs-lookup"><span data-stu-id="3ab27-141">Required</span></span> | <span data-ttu-id="3ab27-142">注意</span><span class="sxs-lookup"><span data-stu-id="3ab27-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="3ab27-143">版本</span><span class="sxs-lookup"><span data-stu-id="3ab27-143">versions</span></span> | <span data-ttu-id="3ab27-144">字串陣列</span><span class="sxs-lookup"><span data-stu-id="3ab27-144">array of strings</span></span> | <span data-ttu-id="3ab27-145">是</span><span class="sxs-lookup"><span data-stu-id="3ab27-145">yes</span></span>      | <span data-ttu-id="3ab27-146">封裝識別碼可用</span><span class="sxs-lookup"><span data-stu-id="3ab27-146">The package IDs available</span></span>

<span data-ttu-id="3ab27-147">中的字串`versions`全部小寫陣列，[正規化 NuGet 版本字串](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="3ab27-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="3ab27-148">版本字串不包含任何的 SemVer 2.0.0 組建中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3ab27-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="3ab27-149">其目的是，此陣列中找到的版本字串可以用於逐字`LOWER_VERSION`下列端點中找到的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="3ab27-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3ab27-150">範例要求</span><span class="sxs-lookup"><span data-stu-id="3ab27-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="3ab27-151">範例回應</span><span class="sxs-lookup"><span data-stu-id="3ab27-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="3ab27-152">下載套件內容 (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="3ab27-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="3ab27-153">如果用戶端知道的套件識別碼和版本，而且想要下載套件內容，他們只需要建構下列 URL:</span><span class="sxs-lookup"><span data-stu-id="3ab27-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="3ab27-154">要求參數</span><span class="sxs-lookup"><span data-stu-id="3ab27-154">Request parameters</span></span>

<span data-ttu-id="3ab27-155">名稱</span><span class="sxs-lookup"><span data-stu-id="3ab27-155">Name</span></span>          | <span data-ttu-id="3ab27-156">In</span><span class="sxs-lookup"><span data-stu-id="3ab27-156">In</span></span>     | <span data-ttu-id="3ab27-157">類型</span><span class="sxs-lookup"><span data-stu-id="3ab27-157">Type</span></span>   | <span data-ttu-id="3ab27-158">必要</span><span class="sxs-lookup"><span data-stu-id="3ab27-158">Required</span></span> | <span data-ttu-id="3ab27-159">注意</span><span class="sxs-lookup"><span data-stu-id="3ab27-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3ab27-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="3ab27-160">LOWER_ID</span></span>      | <span data-ttu-id="3ab27-161">URL</span><span class="sxs-lookup"><span data-stu-id="3ab27-161">URL</span></span>    | <span data-ttu-id="3ab27-162">字串</span><span class="sxs-lookup"><span data-stu-id="3ab27-162">string</span></span> | <span data-ttu-id="3ab27-163">是</span><span class="sxs-lookup"><span data-stu-id="3ab27-163">yes</span></span>      | <span data-ttu-id="3ab27-164">封裝識別碼、 小寫字母</span><span class="sxs-lookup"><span data-stu-id="3ab27-164">The package ID, lowercase</span></span>
<span data-ttu-id="3ab27-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="3ab27-165">LOWER_VERSION</span></span> | <span data-ttu-id="3ab27-166">URL</span><span class="sxs-lookup"><span data-stu-id="3ab27-166">URL</span></span>    | <span data-ttu-id="3ab27-167">字串</span><span class="sxs-lookup"><span data-stu-id="3ab27-167">string</span></span> | <span data-ttu-id="3ab27-168">是</span><span class="sxs-lookup"><span data-stu-id="3ab27-168">yes</span></span>      | <span data-ttu-id="3ab27-169">套件版本，並以標準化小寫</span><span class="sxs-lookup"><span data-stu-id="3ab27-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="3ab27-170">兩者`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="3ab27-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="3ab27-171">方法。</span><span class="sxs-lookup"><span data-stu-id="3ab27-171">method.</span></span>

<span data-ttu-id="3ab27-172">`LOWER_VERSION`所需的套件版本使用標準化 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="3ab27-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="3ab27-173">這表示必須在此情況下排除組建中繼資料所允許的 SemVer 2.0.0 規格。</span><span class="sxs-lookup"><span data-stu-id="3ab27-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="3ab27-174">回應本文</span><span class="sxs-lookup"><span data-stu-id="3ab27-174">Response body</span></span>

<span data-ttu-id="3ab27-175">如果封裝存在於封裝來源，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3ab27-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="3ab27-176">回應主體會封裝內容本身。</span><span class="sxs-lookup"><span data-stu-id="3ab27-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="3ab27-177">如果封裝不存在套件來源，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3ab27-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3ab27-178">範例要求</span><span class="sxs-lookup"><span data-stu-id="3ab27-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="3ab27-179">範例回應</span><span class="sxs-lookup"><span data-stu-id="3ab27-179">Sample response</span></span>

<span data-ttu-id="3ab27-180">二進位資料流是.nupkg Newtonsoft.Json 9.0.1 （英文)。</span><span class="sxs-lookup"><span data-stu-id="3ab27-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="3ab27-181">下載封裝資訊清單 (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="3ab27-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="3ab27-182">如果用戶端知道的套件識別碼和版本，而且想要下載的封裝資訊清單，他們只需要建構下列 URL:</span><span class="sxs-lookup"><span data-stu-id="3ab27-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="3ab27-183">要求參數</span><span class="sxs-lookup"><span data-stu-id="3ab27-183">Request parameters</span></span>

<span data-ttu-id="3ab27-184">名稱</span><span class="sxs-lookup"><span data-stu-id="3ab27-184">Name</span></span>          | <span data-ttu-id="3ab27-185">In</span><span class="sxs-lookup"><span data-stu-id="3ab27-185">In</span></span>     | <span data-ttu-id="3ab27-186">類型</span><span class="sxs-lookup"><span data-stu-id="3ab27-186">Type</span></span>   | <span data-ttu-id="3ab27-187">必要</span><span class="sxs-lookup"><span data-stu-id="3ab27-187">Required</span></span> | <span data-ttu-id="3ab27-188">注意</span><span class="sxs-lookup"><span data-stu-id="3ab27-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3ab27-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="3ab27-189">LOWER_ID</span></span>      | <span data-ttu-id="3ab27-190">URL</span><span class="sxs-lookup"><span data-stu-id="3ab27-190">URL</span></span>    | <span data-ttu-id="3ab27-191">字串</span><span class="sxs-lookup"><span data-stu-id="3ab27-191">string</span></span> | <span data-ttu-id="3ab27-192">是</span><span class="sxs-lookup"><span data-stu-id="3ab27-192">yes</span></span>      | <span data-ttu-id="3ab27-193">封裝識別碼、 小寫字母</span><span class="sxs-lookup"><span data-stu-id="3ab27-193">The package ID, lowercase</span></span>
<span data-ttu-id="3ab27-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="3ab27-194">LOWER_VERSION</span></span> | <span data-ttu-id="3ab27-195">URL</span><span class="sxs-lookup"><span data-stu-id="3ab27-195">URL</span></span>    | <span data-ttu-id="3ab27-196">字串</span><span class="sxs-lookup"><span data-stu-id="3ab27-196">string</span></span> | <span data-ttu-id="3ab27-197">是</span><span class="sxs-lookup"><span data-stu-id="3ab27-197">yes</span></span>      | <span data-ttu-id="3ab27-198">套件版本，並以標準化小寫</span><span class="sxs-lookup"><span data-stu-id="3ab27-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="3ab27-199">兩者`LOWER_ID`和`LOWER_VERSION`會變成使用所實作的規則。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。</span><span class="sxs-lookup"><span data-stu-id="3ab27-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="3ab27-200">`LOWER_VERSION`所需的套件版本使用標準化 NuGet 的版本[正規化規則](../reference/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="3ab27-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="3ab27-201">這表示必須在此情況下排除組建中繼資料所允許的 SemVer 2.0.0 規格。</span><span class="sxs-lookup"><span data-stu-id="3ab27-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="3ab27-202">回應本文</span><span class="sxs-lookup"><span data-stu-id="3ab27-202">Response body</span></span>

<span data-ttu-id="3ab27-203">如果封裝存在於封裝來源，則會傳回 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3ab27-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="3ab27-204">回應主體會是包含在對應的.nupkg.nuspec 套件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="3ab27-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="3ab27-205">.nuspec 是 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="3ab27-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="3ab27-206">如果封裝不存在套件來源，則會傳回 404 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3ab27-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3ab27-207">範例要求</span><span class="sxs-lookup"><span data-stu-id="3ab27-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="3ab27-208">範例回應</span><span class="sxs-lookup"><span data-stu-id="3ab27-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
