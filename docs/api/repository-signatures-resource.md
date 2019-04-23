---
title: 存放庫簽章，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存放庫簽章資源可讓用戶端地宣布其簽署功能的存放庫的套件來源。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931848"
---
# <a name="repository-signatures"></a><span data-ttu-id="3a9ab-103">存放庫簽章</span><span class="sxs-lookup"><span data-stu-id="3a9ab-103">Repository signatures</span></span>

<span data-ttu-id="3a9ab-104">如果套件來源支援新增存放庫簽章，以發佈的封裝，就可以判斷所使用的套件來源的簽章憑證的用戶端。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="3a9ab-105">這項資源可讓用戶端偵測封裝存放庫簽章是否遭到竄改，或有非預期的簽章憑證。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="3a9ab-106">用於擷取此存放庫簽章資訊的資源`RepositorySignatures`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="3a9ab-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="3a9ab-107">Versioning</span></span>

<span data-ttu-id="3a9ab-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="3a9ab-108">The following `@type` value is used:</span></span>

<span data-ttu-id="3a9ab-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="3a9ab-109">@type value</span></span>                | <span data-ttu-id="3a9ab-110">注意</span><span class="sxs-lookup"><span data-stu-id="3a9ab-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="3a9ab-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="3a9ab-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="3a9ab-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="3a9ab-112">The initial release</span></span>
<span data-ttu-id="3a9ab-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="3a9ab-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="3a9ab-114">NuGet 4.9 + 用戶端支援</span><span class="sxs-lookup"><span data-stu-id="3a9ab-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="3a9ab-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="3a9ab-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="3a9ab-116">可讓啟用`allRepositorySigned`。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="3a9ab-117">NuGet v5.0 + 用戶端支援</span><span class="sxs-lookup"><span data-stu-id="3a9ab-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="3a9ab-118">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="3a9ab-118">Base URL</span></span>

<span data-ttu-id="3a9ab-119">下列 Api 的進入點 URL 是 windows 7`@id`上述的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="3a9ab-120">本主題使用的預留位置 URL `{@id}`。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="3a9ab-121">請注意，不同於其他資源， `{@id}` URL，才能透過 HTTPS 提供服務。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3a9ab-122">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="3a9ab-122">HTTP methods</span></span>

<span data-ttu-id="3a9ab-123">在存放庫簽章資源支援的 HTTP 方法中找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="3a9ab-124">存放庫簽章索引</span><span class="sxs-lookup"><span data-stu-id="3a9ab-124">Repository signatures index</span></span>

<span data-ttu-id="3a9ab-125">存放庫簽章索引包含兩項資訊：</span><span class="sxs-lookup"><span data-stu-id="3a9ab-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="3a9ab-126">在來源上找到所有的套件是經過此套件來源的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="3a9ab-127">用來簽署套件的套件來源的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="3a9ab-128">在大部分情況下，憑證清單只會將附加到。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="3a9ab-129">先前的簽署憑證已過期，而且若要開始使用新的簽署憑證需要的套件來源時，新的憑證將會新增至清單。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="3a9ab-130">如果憑證從清單中移除，這表示，使用已移除的簽署憑證建立的所有套件簽章應不會再都視為有效用戶端。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="3a9ab-131">在此情況下，封裝簽章 （但不是一定是封裝） 無效。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="3a9ab-132">用戶端原則可能會允許安裝為不帶正負號的套件。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="3a9ab-133">在憑證撤銷 （例如金鑰洩露） 的情況下的套件來源應該重新簽署所有受影響的憑證所簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="3a9ab-134">此外，套件來源應該移除受影響的憑證簽署的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="3a9ab-135">下列要求擷取存放庫簽章索引。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-135">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="3a9ab-136">存放庫簽章索引是 JSON 文件，其中包含具有下列屬性的物件：</span><span class="sxs-lookup"><span data-stu-id="3a9ab-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="3a9ab-137">名稱</span><span class="sxs-lookup"><span data-stu-id="3a9ab-137">Name</span></span>                | <span data-ttu-id="3a9ab-138">類型</span><span class="sxs-lookup"><span data-stu-id="3a9ab-138">Type</span></span>             | <span data-ttu-id="3a9ab-139">必要</span><span class="sxs-lookup"><span data-stu-id="3a9ab-139">Required</span></span> | <span data-ttu-id="3a9ab-140">注意</span><span class="sxs-lookup"><span data-stu-id="3a9ab-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="3a9ab-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="3a9ab-141">allRepositorySigned</span></span> | <span data-ttu-id="3a9ab-142">boolean</span><span class="sxs-lookup"><span data-stu-id="3a9ab-142">boolean</span></span>          | <span data-ttu-id="3a9ab-143">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-143">yes</span></span>      | <span data-ttu-id="3a9ab-144">必須是`false`4.7.0 和 4.9.0 資源</span><span class="sxs-lookup"><span data-stu-id="3a9ab-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="3a9ab-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="3a9ab-145">signingCertificates</span></span> | <span data-ttu-id="3a9ab-146">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="3a9ab-146">array of objects</span></span> | <span data-ttu-id="3a9ab-147">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-147">yes</span></span>      | 

<span data-ttu-id="3a9ab-148">`allRepositorySigned`布林值為 false，如果套件來源具有一些套件有沒有存放庫簽章。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="3a9ab-149">如果布林值會設為 true，在所有的封裝來源必須具有存放庫簽章所述的簽章憑證的其中一個產生`signingCertificates`。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="3a9ab-150">`allRepositorySigned`布林值必須為偽 4.7.0 和 4.9.0 資源上。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="3a9ab-151">NuGet v4.7、 v4.8 和 4.9 用戶端無法從來源安裝套件`allRepositorySigned`設為 true。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="3a9ab-152">應該有一或多個中的簽署憑證`signingCertificates`陣列，如果`allRepositorySigned`布林值會設為 true。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="3a9ab-153">如果是空的陣列和`allRepositorySigned`設為 true，所有的封裝來源的資料應視為無效，雖然用戶端原則仍然允許套件耗用量。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="3a9ab-154">此陣列中的每個項目是具有下列屬性的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="3a9ab-155">名稱</span><span class="sxs-lookup"><span data-stu-id="3a9ab-155">Name</span></span>         | <span data-ttu-id="3a9ab-156">類型</span><span class="sxs-lookup"><span data-stu-id="3a9ab-156">Type</span></span>   | <span data-ttu-id="3a9ab-157">必要</span><span class="sxs-lookup"><span data-stu-id="3a9ab-157">Required</span></span> | <span data-ttu-id="3a9ab-158">注意</span><span class="sxs-lookup"><span data-stu-id="3a9ab-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="3a9ab-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="3a9ab-159">contentUrl</span></span>   | <span data-ttu-id="3a9ab-160">字串</span><span class="sxs-lookup"><span data-stu-id="3a9ab-160">string</span></span> | <span data-ttu-id="3a9ab-161">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-161">yes</span></span>      | <span data-ttu-id="3a9ab-162">DER 編碼的公開憑證的絕對 URL</span><span class="sxs-lookup"><span data-stu-id="3a9ab-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="3a9ab-163">指紋</span><span class="sxs-lookup"><span data-stu-id="3a9ab-163">fingerprints</span></span> | <span data-ttu-id="3a9ab-164">object</span><span class="sxs-lookup"><span data-stu-id="3a9ab-164">object</span></span> | <span data-ttu-id="3a9ab-165">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-165">yes</span></span>      |
<span data-ttu-id="3a9ab-166">主旨</span><span class="sxs-lookup"><span data-stu-id="3a9ab-166">subject</span></span>      | <span data-ttu-id="3a9ab-167">字串</span><span class="sxs-lookup"><span data-stu-id="3a9ab-167">string</span></span> | <span data-ttu-id="3a9ab-168">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-168">yes</span></span>      | <span data-ttu-id="3a9ab-169">從憑證主體辨別的名稱</span><span class="sxs-lookup"><span data-stu-id="3a9ab-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="3a9ab-170">issuer</span><span class="sxs-lookup"><span data-stu-id="3a9ab-170">issuer</span></span>       | <span data-ttu-id="3a9ab-171">字串</span><span class="sxs-lookup"><span data-stu-id="3a9ab-171">string</span></span> | <span data-ttu-id="3a9ab-172">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-172">yes</span></span>      | <span data-ttu-id="3a9ab-173">憑證的簽發者的辨別的名稱</span><span class="sxs-lookup"><span data-stu-id="3a9ab-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="3a9ab-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="3a9ab-174">notBefore</span></span>    | <span data-ttu-id="3a9ab-175">字串</span><span class="sxs-lookup"><span data-stu-id="3a9ab-175">string</span></span> | <span data-ttu-id="3a9ab-176">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-176">yes</span></span>      | <span data-ttu-id="3a9ab-177">憑證的有效期間的開始時間戳記</span><span class="sxs-lookup"><span data-stu-id="3a9ab-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="3a9ab-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="3a9ab-178">notAfter</span></span>     | <span data-ttu-id="3a9ab-179">字串</span><span class="sxs-lookup"><span data-stu-id="3a9ab-179">string</span></span> | <span data-ttu-id="3a9ab-180">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-180">yes</span></span>      | <span data-ttu-id="3a9ab-181">憑證的有效期間結束的時間戳記</span><span class="sxs-lookup"><span data-stu-id="3a9ab-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="3a9ab-182">請注意，`contentUrl`才能透過 HTTPS 提供服務。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="3a9ab-183">此 URL 有沒有特定的 URL 模式，而且必須動態探索使用此存放庫簽章索引文件。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="3a9ab-184">這個物件中的所有屬性 (除了來自`contentUrl`) 必須是可從憑證，請參閱衍生`contentUrl`。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="3a9ab-185">為了方便起見，將往返降至最低，會提供這些可衍生的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="3a9ab-186">`fingerprints`物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="3a9ab-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="3a9ab-187">名稱</span><span class="sxs-lookup"><span data-stu-id="3a9ab-187">Name</span></span>                   | <span data-ttu-id="3a9ab-188">類型</span><span class="sxs-lookup"><span data-stu-id="3a9ab-188">Type</span></span>   | <span data-ttu-id="3a9ab-189">必要</span><span class="sxs-lookup"><span data-stu-id="3a9ab-189">Required</span></span> | <span data-ttu-id="3a9ab-190">注意</span><span class="sxs-lookup"><span data-stu-id="3a9ab-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="3a9ab-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="3a9ab-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="3a9ab-192">字串</span><span class="sxs-lookup"><span data-stu-id="3a9ab-192">string</span></span> | <span data-ttu-id="3a9ab-193">是</span><span class="sxs-lookup"><span data-stu-id="3a9ab-193">yes</span></span>      | <span data-ttu-id="3a9ab-194">SHA-256 指紋</span><span class="sxs-lookup"><span data-stu-id="3a9ab-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="3a9ab-195">索引鍵名稱`2.16.840.1.101.3.4.2.1`是 SHA-256 雜湊演算法的 OID。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="3a9ab-196">所有的雜湊值必須是摘要的小寫字母、 十六進位編碼的字串表示的雜湊。</span><span class="sxs-lookup"><span data-stu-id="3a9ab-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3a9ab-197">範例要求</span><span class="sxs-lookup"><span data-stu-id="3a9ab-197">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="3a9ab-198">範例回應</span><span class="sxs-lookup"><span data-stu-id="3a9ab-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
