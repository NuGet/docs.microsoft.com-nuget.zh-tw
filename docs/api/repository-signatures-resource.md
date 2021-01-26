---
title: 存放庫簽章，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存放庫簽章資源可讓用戶端套件來源宣佈其存放庫簽署功能。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775337"
---
# <a name="repository-signatures"></a><span data-ttu-id="aa00f-103">存放庫簽章</span><span class="sxs-lookup"><span data-stu-id="aa00f-103">Repository signatures</span></span>

<span data-ttu-id="aa00f-104">如果封裝來源支援將存放庫簽章新增至已發佈的封裝，則用戶端可能會判斷套件來源所使用的簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="aa00f-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="aa00f-105">此資源可讓用戶端偵測存放庫簽署的套件是否已遭篡改，或是否有未預期的簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="aa00f-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="aa00f-106">用來提取此存放庫簽章資訊的資源是在 `RepositorySignatures` [服務索引](service-index.md)中找到的資源。</span><span class="sxs-lookup"><span data-stu-id="aa00f-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="aa00f-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="aa00f-107">Versioning</span></span>

<span data-ttu-id="aa00f-108">使用的 `@type` 值如下：</span><span class="sxs-lookup"><span data-stu-id="aa00f-108">The following `@type` value is used:</span></span>

<span data-ttu-id="aa00f-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="aa00f-109">@type value</span></span>                | <span data-ttu-id="aa00f-110">備註</span><span class="sxs-lookup"><span data-stu-id="aa00f-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="aa00f-111">RepositorySignatures/4.7。0</span><span class="sxs-lookup"><span data-stu-id="aa00f-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="aa00f-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="aa00f-112">The initial release</span></span>
<span data-ttu-id="aa00f-113">RepositorySignatures/4.9。0</span><span class="sxs-lookup"><span data-stu-id="aa00f-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="aa00f-114">NuGet v 4.9 + 用戶端支援</span><span class="sxs-lookup"><span data-stu-id="aa00f-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="aa00f-115">RepositorySignatures/5.0。0</span><span class="sxs-lookup"><span data-stu-id="aa00f-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="aa00f-116">允許啟用 `allRepositorySigned` 。</span><span class="sxs-lookup"><span data-stu-id="aa00f-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="aa00f-117">NuGet v 5.0 + 用戶端支援</span><span class="sxs-lookup"><span data-stu-id="aa00f-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="aa00f-118">基底 URL</span><span class="sxs-lookup"><span data-stu-id="aa00f-118">Base URL</span></span>

<span data-ttu-id="aa00f-119">下列 Api 的進入點 URL 是 `@id` 與上述資源值相關聯之屬性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="aa00f-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="aa00f-120">本主題使用預留位置 URL `{@id}` 。</span><span class="sxs-lookup"><span data-stu-id="aa00f-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="aa00f-121">請注意，與其他資源不同的是， `{@id}` 必須透過 HTTPS 提供 URL。</span><span class="sxs-lookup"><span data-stu-id="aa00f-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="aa00f-122">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="aa00f-122">HTTP methods</span></span>

<span data-ttu-id="aa00f-123">存放庫簽章資源中找到的所有 Url 都只支援 HTTP 方法 `GET` 和 `HEAD` 。</span><span class="sxs-lookup"><span data-stu-id="aa00f-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="aa00f-124">存放庫簽章索引</span><span class="sxs-lookup"><span data-stu-id="aa00f-124">Repository signatures index</span></span>

<span data-ttu-id="aa00f-125">存放庫簽章索引包含兩項資訊：</span><span class="sxs-lookup"><span data-stu-id="aa00f-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="aa00f-126">來源上找到的所有套件是否都是由這個套件來源簽署的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="aa00f-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="aa00f-127">封裝來源用來簽署套件的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="aa00f-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="aa00f-128">在大部分情況下，憑證清單只會附加至。</span><span class="sxs-lookup"><span data-stu-id="aa00f-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="aa00f-129">當先前的簽署憑證已過期，且套件來源需要開始使用新的簽署憑證時，就會將新的憑證新增至清單中。</span><span class="sxs-lookup"><span data-stu-id="aa00f-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="aa00f-130">如果從清單中移除憑證，這表示用戶端不應再將使用移除的簽署憑證所建立的所有封裝簽章視為有效。</span><span class="sxs-lookup"><span data-stu-id="aa00f-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="aa00f-131">在此情況下，封裝簽章 (但不一定是封裝) 無效。</span><span class="sxs-lookup"><span data-stu-id="aa00f-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="aa00f-132">用戶端原則可能會允許將套件安裝為未簽署。</span><span class="sxs-lookup"><span data-stu-id="aa00f-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="aa00f-133">在憑證撤銷的情況下 (例如金鑰洩漏) ，套件來源應該要重新簽署受影響之憑證簽署的所有套件。</span><span class="sxs-lookup"><span data-stu-id="aa00f-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="aa00f-134">此外，套件來源應該從簽署憑證清單中移除受影響的憑證。</span><span class="sxs-lookup"><span data-stu-id="aa00f-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="aa00f-135">下列要求會提取存放庫簽章索引。</span><span class="sxs-lookup"><span data-stu-id="aa00f-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="aa00f-136">存放庫簽章索引是 JSON 檔，其中包含具有下列屬性的物件：</span><span class="sxs-lookup"><span data-stu-id="aa00f-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="aa00f-137">名稱</span><span class="sxs-lookup"><span data-stu-id="aa00f-137">Name</span></span>                | <span data-ttu-id="aa00f-138">類型</span><span class="sxs-lookup"><span data-stu-id="aa00f-138">Type</span></span>             | <span data-ttu-id="aa00f-139">必要</span><span class="sxs-lookup"><span data-stu-id="aa00f-139">Required</span></span> | <span data-ttu-id="aa00f-140">備註</span><span class="sxs-lookup"><span data-stu-id="aa00f-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="aa00f-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="aa00f-141">allRepositorySigned</span></span> | <span data-ttu-id="aa00f-142">boolean</span><span class="sxs-lookup"><span data-stu-id="aa00f-142">boolean</span></span>          | <span data-ttu-id="aa00f-143">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-143">yes</span></span>      | <span data-ttu-id="aa00f-144">必須 `false` 在4.7.0 和4.9.0 資源上</span><span class="sxs-lookup"><span data-stu-id="aa00f-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="aa00f-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="aa00f-145">signingCertificates</span></span> | <span data-ttu-id="aa00f-146">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="aa00f-146">array of objects</span></span> | <span data-ttu-id="aa00f-147">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-147">yes</span></span>      | 

<span data-ttu-id="aa00f-148">`allRepositorySigned`如果封裝來源有一些沒有存放庫簽章的封裝，則布林值設定為 false。</span><span class="sxs-lookup"><span data-stu-id="aa00f-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="aa00f-149">如果布林值設定為 true，則來源上的所有可用封裝都必須有中所述的其中一個簽署憑證所產生的存放庫簽章 `signingCertificates` 。</span><span class="sxs-lookup"><span data-stu-id="aa00f-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="aa00f-150">`allRepositorySigned`4.7.0 和4.9.0 資源上的布林值必須為 false。</span><span class="sxs-lookup"><span data-stu-id="aa00f-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="aa00f-151">NuGet 4.7、4.8 和 v 4.9 用戶端無法從已設定為 true 的來源安裝套件 `allRepositorySigned` 。</span><span class="sxs-lookup"><span data-stu-id="aa00f-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="aa00f-152">`signingCertificates`如果 `allRepositorySigned` 布林值設定為 true，陣列中應該有一或多個簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="aa00f-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="aa00f-153">如果陣列是空的，而且 `allRepositorySigned` 設定為 true，則來源的所有套件都應視為無效，雖然用戶端原則仍允許使用套件。</span><span class="sxs-lookup"><span data-stu-id="aa00f-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="aa00f-154">此陣列中的每個元素都是具有下列屬性的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="aa00f-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="aa00f-155">名稱</span><span class="sxs-lookup"><span data-stu-id="aa00f-155">Name</span></span>         | <span data-ttu-id="aa00f-156">類型</span><span class="sxs-lookup"><span data-stu-id="aa00f-156">Type</span></span>   | <span data-ttu-id="aa00f-157">必要</span><span class="sxs-lookup"><span data-stu-id="aa00f-157">Required</span></span> | <span data-ttu-id="aa00f-158">備註</span><span class="sxs-lookup"><span data-stu-id="aa00f-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="aa00f-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="aa00f-159">contentUrl</span></span>   | <span data-ttu-id="aa00f-160">字串</span><span class="sxs-lookup"><span data-stu-id="aa00f-160">string</span></span> | <span data-ttu-id="aa00f-161">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-161">yes</span></span>      | <span data-ttu-id="aa00f-162">DER 編碼公開憑證的絕對 URL</span><span class="sxs-lookup"><span data-stu-id="aa00f-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="aa00f-163">指紋</span><span class="sxs-lookup"><span data-stu-id="aa00f-163">fingerprints</span></span> | <span data-ttu-id="aa00f-164">物件 (object)</span><span class="sxs-lookup"><span data-stu-id="aa00f-164">object</span></span> | <span data-ttu-id="aa00f-165">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-165">yes</span></span>      |
<span data-ttu-id="aa00f-166">subject</span><span class="sxs-lookup"><span data-stu-id="aa00f-166">subject</span></span>      | <span data-ttu-id="aa00f-167">字串</span><span class="sxs-lookup"><span data-stu-id="aa00f-167">string</span></span> | <span data-ttu-id="aa00f-168">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-168">yes</span></span>      | <span data-ttu-id="aa00f-169">憑證中的主體辨別名稱</span><span class="sxs-lookup"><span data-stu-id="aa00f-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="aa00f-170">簽發者</span><span class="sxs-lookup"><span data-stu-id="aa00f-170">issuer</span></span>       | <span data-ttu-id="aa00f-171">字串</span><span class="sxs-lookup"><span data-stu-id="aa00f-171">string</span></span> | <span data-ttu-id="aa00f-172">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-172">yes</span></span>      | <span data-ttu-id="aa00f-173">憑證簽發者的辨別名稱</span><span class="sxs-lookup"><span data-stu-id="aa00f-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="aa00f-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="aa00f-174">notBefore</span></span>    | <span data-ttu-id="aa00f-175">字串</span><span class="sxs-lookup"><span data-stu-id="aa00f-175">string</span></span> | <span data-ttu-id="aa00f-176">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-176">yes</span></span>      | <span data-ttu-id="aa00f-177">憑證有效期間的開始時間戳</span><span class="sxs-lookup"><span data-stu-id="aa00f-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="aa00f-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="aa00f-178">notAfter</span></span>     | <span data-ttu-id="aa00f-179">字串</span><span class="sxs-lookup"><span data-stu-id="aa00f-179">string</span></span> | <span data-ttu-id="aa00f-180">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-180">yes</span></span>      | <span data-ttu-id="aa00f-181">憑證有效期間的結束時間戳記</span><span class="sxs-lookup"><span data-stu-id="aa00f-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="aa00f-182">請注意， `contentUrl` 必須透過 HTTPS 來提供。</span><span class="sxs-lookup"><span data-stu-id="aa00f-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="aa00f-183">此 URL 沒有特定的 URL 模式，必須使用此存放庫簽章索引檔來動態探索。</span><span class="sxs-lookup"><span data-stu-id="aa00f-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="aa00f-184">此物件中)  (的所有屬性都 `contentUrl` 必須從找到的憑證可 `contentUrl` 。</span><span class="sxs-lookup"><span data-stu-id="aa00f-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="aa00f-185">提供這些可屬性是為了方便將往返次數降至最低。</span><span class="sxs-lookup"><span data-stu-id="aa00f-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="aa00f-186">`fingerprints` 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="aa00f-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="aa00f-187">名稱</span><span class="sxs-lookup"><span data-stu-id="aa00f-187">Name</span></span>                   | <span data-ttu-id="aa00f-188">類型</span><span class="sxs-lookup"><span data-stu-id="aa00f-188">Type</span></span>   | <span data-ttu-id="aa00f-189">必要</span><span class="sxs-lookup"><span data-stu-id="aa00f-189">Required</span></span> | <span data-ttu-id="aa00f-190">備註</span><span class="sxs-lookup"><span data-stu-id="aa00f-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="aa00f-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="aa00f-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="aa00f-192">字串</span><span class="sxs-lookup"><span data-stu-id="aa00f-192">string</span></span> | <span data-ttu-id="aa00f-193">是</span><span class="sxs-lookup"><span data-stu-id="aa00f-193">yes</span></span>      | <span data-ttu-id="aa00f-194">SHA-256 指紋</span><span class="sxs-lookup"><span data-stu-id="aa00f-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="aa00f-195">索引鍵名稱 `2.16.840.1.101.3.4.2.1` 是 SHA-256 雜湊演算法的 OID。</span><span class="sxs-lookup"><span data-stu-id="aa00f-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="aa00f-196">所有雜湊值都必須是雜湊摘要的小寫、十六進位編碼的字串表示。</span><span class="sxs-lookup"><span data-stu-id="aa00f-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="aa00f-197">範例要求</span><span class="sxs-lookup"><span data-stu-id="aa00f-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="aa00f-198">範例回應</span><span class="sxs-lookup"><span data-stu-id="aa00f-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
