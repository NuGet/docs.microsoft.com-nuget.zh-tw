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
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248438"
---
# <a name="repository-signatures"></a><span data-ttu-id="88f2b-103">存放庫簽章</span><span class="sxs-lookup"><span data-stu-id="88f2b-103">Repository signatures</span></span>

<span data-ttu-id="88f2b-104">如果套件來源支援新增存放庫簽章，以發佈的封裝，就可以判斷所使用的套件來源的簽章憑證的用戶端。</span><span class="sxs-lookup"><span data-stu-id="88f2b-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="88f2b-105">這項資源可讓用戶端偵測封裝存放庫簽章是否遭到竄改，或有非預期的簽章憑證。</span><span class="sxs-lookup"><span data-stu-id="88f2b-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="88f2b-106">用於擷取此存放庫簽章資訊的資源`RepositorySignatures`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="88f2b-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="88f2b-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="88f2b-107">Versioning</span></span>

<span data-ttu-id="88f2b-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="88f2b-108">The following `@type` value is used:</span></span>

<span data-ttu-id="88f2b-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="88f2b-109">@type value</span></span>                | <span data-ttu-id="88f2b-110">注意</span><span class="sxs-lookup"><span data-stu-id="88f2b-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="88f2b-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="88f2b-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="88f2b-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="88f2b-112">The initial release</span></span>
<span data-ttu-id="88f2b-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="88f2b-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="88f2b-114">可讓啟用 `allRepositorySigned`</span><span class="sxs-lookup"><span data-stu-id="88f2b-114">Allows enabling `allRepositorySigned`</span></span>

## <a name="base-url"></a><span data-ttu-id="88f2b-115">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="88f2b-115">Base URL</span></span>

<span data-ttu-id="88f2b-116">下列 Api 的進入點 URL 是 windows 7`@id`上述的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="88f2b-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="88f2b-117">本主題使用的預留位置 URL `{@id}`。</span><span class="sxs-lookup"><span data-stu-id="88f2b-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="88f2b-118">請注意，不同於其他資源， `{@id}` URL，才能透過 HTTPS 提供服務。</span><span class="sxs-lookup"><span data-stu-id="88f2b-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="88f2b-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="88f2b-119">HTTP methods</span></span>

<span data-ttu-id="88f2b-120">在存放庫簽章資源支援的 HTTP 方法中找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="88f2b-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="88f2b-121">存放庫簽章索引</span><span class="sxs-lookup"><span data-stu-id="88f2b-121">Repository signatures index</span></span>

<span data-ttu-id="88f2b-122">存放庫簽章索引包含兩項資訊：</span><span class="sxs-lookup"><span data-stu-id="88f2b-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="88f2b-123">在來源上找到所有的套件是經過此套件來源的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="88f2b-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="88f2b-124">用來簽署套件的套件來源的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="88f2b-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="88f2b-125">在大部分情況下，憑證清單只會將附加到。</span><span class="sxs-lookup"><span data-stu-id="88f2b-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="88f2b-126">先前的簽署憑證已過期，而且若要開始使用新的簽署憑證需要的套件來源時，新的憑證將會新增至清單。</span><span class="sxs-lookup"><span data-stu-id="88f2b-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="88f2b-127">如果憑證從清單中移除，這表示，使用已移除的簽署憑證建立的所有套件簽章應不會再都視為有效用戶端。</span><span class="sxs-lookup"><span data-stu-id="88f2b-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="88f2b-128">在此情況下，封裝簽章 （但不是一定是封裝） 無效。</span><span class="sxs-lookup"><span data-stu-id="88f2b-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="88f2b-129">用戶端原則可能會允許安裝為不帶正負號的套件。</span><span class="sxs-lookup"><span data-stu-id="88f2b-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="88f2b-130">在憑證撤銷 （例如金鑰洩露） 的情況下的套件來源應該重新簽署所有受影響的憑證所簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="88f2b-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="88f2b-131">此外，套件來源應該移除受影響的憑證簽署的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="88f2b-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="88f2b-132">下列要求擷取存放庫簽章索引。</span><span class="sxs-lookup"><span data-stu-id="88f2b-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="88f2b-133">存放庫簽章索引是 JSON 文件，其中包含具有下列屬性的物件：</span><span class="sxs-lookup"><span data-stu-id="88f2b-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="88f2b-134">名稱</span><span class="sxs-lookup"><span data-stu-id="88f2b-134">Name</span></span>                | <span data-ttu-id="88f2b-135">類型</span><span class="sxs-lookup"><span data-stu-id="88f2b-135">Type</span></span>             | <span data-ttu-id="88f2b-136">必要</span><span class="sxs-lookup"><span data-stu-id="88f2b-136">Required</span></span> | <span data-ttu-id="88f2b-137">注意</span><span class="sxs-lookup"><span data-stu-id="88f2b-137">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="88f2b-138">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="88f2b-138">allRepositorySigned</span></span> | <span data-ttu-id="88f2b-139">boolean</span><span class="sxs-lookup"><span data-stu-id="88f2b-139">boolean</span></span>          | <span data-ttu-id="88f2b-140">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-140">yes</span></span>      | <span data-ttu-id="88f2b-141">必須是`false`上 4.7.0 資源</span><span class="sxs-lookup"><span data-stu-id="88f2b-141">Must be `false` on 4.7.0 resource</span></span>
<span data-ttu-id="88f2b-142">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="88f2b-142">signingCertificates</span></span> | <span data-ttu-id="88f2b-143">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="88f2b-143">array of objects</span></span> | <span data-ttu-id="88f2b-144">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-144">yes</span></span>      | 

<span data-ttu-id="88f2b-145">`allRepositorySigned`布林值為 false，如果套件來源具有一些套件有沒有存放庫簽章。</span><span class="sxs-lookup"><span data-stu-id="88f2b-145">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="88f2b-146">如果布林值會設為 true，在所有的封裝來源必須具有存放庫簽章所述的簽章憑證的其中一個產生`signingCertificates`。</span><span class="sxs-lookup"><span data-stu-id="88f2b-146">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="88f2b-147">`allRepositorySigned`布林值必須為偽上 4.7.0 資源。</span><span class="sxs-lookup"><span data-stu-id="88f2b-147">The `allRepositorySigned` boolean must be false on the 4.7.0 resource.</span></span> <span data-ttu-id="88f2b-148">NuGet v4.7 和 v4.8 用戶端無法從來源安裝套件`allRepositorySigned`設為 true。</span><span class="sxs-lookup"><span data-stu-id="88f2b-148">NuGet v4.7 and v4.8 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="88f2b-149">應該有一或多個中的簽署憑證`signingCertificates`陣列，如果`allRepositorySigned`布林值會設為 true。</span><span class="sxs-lookup"><span data-stu-id="88f2b-149">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="88f2b-150">如果是空的陣列和`allRepositorySigned`設為 true，所有的封裝來源的資料應視為無效，雖然用戶端原則仍然允許套件耗用量。</span><span class="sxs-lookup"><span data-stu-id="88f2b-150">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="88f2b-151">此陣列中的每個項目是具有下列屬性的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="88f2b-151">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="88f2b-152">名稱</span><span class="sxs-lookup"><span data-stu-id="88f2b-152">Name</span></span>         | <span data-ttu-id="88f2b-153">類型</span><span class="sxs-lookup"><span data-stu-id="88f2b-153">Type</span></span>   | <span data-ttu-id="88f2b-154">必要</span><span class="sxs-lookup"><span data-stu-id="88f2b-154">Required</span></span> | <span data-ttu-id="88f2b-155">注意</span><span class="sxs-lookup"><span data-stu-id="88f2b-155">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="88f2b-156">contentUrl</span><span class="sxs-lookup"><span data-stu-id="88f2b-156">contentUrl</span></span>   | <span data-ttu-id="88f2b-157">字串</span><span class="sxs-lookup"><span data-stu-id="88f2b-157">string</span></span> | <span data-ttu-id="88f2b-158">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-158">yes</span></span>      | <span data-ttu-id="88f2b-159">DER 編碼的公開憑證的絕對 URL</span><span class="sxs-lookup"><span data-stu-id="88f2b-159">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="88f2b-160">指紋</span><span class="sxs-lookup"><span data-stu-id="88f2b-160">fingerprints</span></span> | <span data-ttu-id="88f2b-161">object</span><span class="sxs-lookup"><span data-stu-id="88f2b-161">object</span></span> | <span data-ttu-id="88f2b-162">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-162">yes</span></span>      |
<span data-ttu-id="88f2b-163">主旨</span><span class="sxs-lookup"><span data-stu-id="88f2b-163">subject</span></span>      | <span data-ttu-id="88f2b-164">字串</span><span class="sxs-lookup"><span data-stu-id="88f2b-164">string</span></span> | <span data-ttu-id="88f2b-165">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-165">yes</span></span>      | <span data-ttu-id="88f2b-166">從憑證主體辨別的名稱</span><span class="sxs-lookup"><span data-stu-id="88f2b-166">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="88f2b-167">issuer</span><span class="sxs-lookup"><span data-stu-id="88f2b-167">issuer</span></span>       | <span data-ttu-id="88f2b-168">字串</span><span class="sxs-lookup"><span data-stu-id="88f2b-168">string</span></span> | <span data-ttu-id="88f2b-169">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-169">yes</span></span>      | <span data-ttu-id="88f2b-170">憑證的簽發者的辨別的名稱</span><span class="sxs-lookup"><span data-stu-id="88f2b-170">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="88f2b-171">notBefore</span><span class="sxs-lookup"><span data-stu-id="88f2b-171">notBefore</span></span>    | <span data-ttu-id="88f2b-172">字串</span><span class="sxs-lookup"><span data-stu-id="88f2b-172">string</span></span> | <span data-ttu-id="88f2b-173">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-173">yes</span></span>      | <span data-ttu-id="88f2b-174">憑證的有效期間的開始時間戳記</span><span class="sxs-lookup"><span data-stu-id="88f2b-174">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="88f2b-175">notAfter</span><span class="sxs-lookup"><span data-stu-id="88f2b-175">notAfter</span></span>     | <span data-ttu-id="88f2b-176">字串</span><span class="sxs-lookup"><span data-stu-id="88f2b-176">string</span></span> | <span data-ttu-id="88f2b-177">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-177">yes</span></span>      | <span data-ttu-id="88f2b-178">憑證的有效期間結束的時間戳記</span><span class="sxs-lookup"><span data-stu-id="88f2b-178">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="88f2b-179">請注意，`contentUrl`才能透過 HTTPS 提供服務。</span><span class="sxs-lookup"><span data-stu-id="88f2b-179">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="88f2b-180">此 URL 有沒有特定的 URL 模式，而且必須動態探索使用此存放庫簽章索引文件。</span><span class="sxs-lookup"><span data-stu-id="88f2b-180">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="88f2b-181">這個物件中的所有屬性 (除了來自`contentUrl`) 必須是可從憑證，請參閱衍生`contentUrl`。</span><span class="sxs-lookup"><span data-stu-id="88f2b-181">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="88f2b-182">為了方便起見，將往返降至最低，會提供這些可衍生的屬性。</span><span class="sxs-lookup"><span data-stu-id="88f2b-182">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="88f2b-183">`fingerprints`物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="88f2b-183">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="88f2b-184">名稱</span><span class="sxs-lookup"><span data-stu-id="88f2b-184">Name</span></span>                   | <span data-ttu-id="88f2b-185">類型</span><span class="sxs-lookup"><span data-stu-id="88f2b-185">Type</span></span>   | <span data-ttu-id="88f2b-186">必要</span><span class="sxs-lookup"><span data-stu-id="88f2b-186">Required</span></span> | <span data-ttu-id="88f2b-187">注意</span><span class="sxs-lookup"><span data-stu-id="88f2b-187">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="88f2b-188">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="88f2b-188">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="88f2b-189">字串</span><span class="sxs-lookup"><span data-stu-id="88f2b-189">string</span></span> | <span data-ttu-id="88f2b-190">是</span><span class="sxs-lookup"><span data-stu-id="88f2b-190">yes</span></span>      | <span data-ttu-id="88f2b-191">SHA-256 指紋</span><span class="sxs-lookup"><span data-stu-id="88f2b-191">The SHA-256 fingerprint</span></span>

<span data-ttu-id="88f2b-192">索引鍵名稱`2.16.840.1.101.3.4.2.1`是 SHA-256 雜湊演算法的 OID。</span><span class="sxs-lookup"><span data-stu-id="88f2b-192">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="88f2b-193">所有的雜湊值必須是摘要的小寫字母、 十六進位編碼的字串表示的雜湊。</span><span class="sxs-lookup"><span data-stu-id="88f2b-193">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="88f2b-194">範例要求</span><span class="sxs-lookup"><span data-stu-id="88f2b-194">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="88f2b-195">範例回應</span><span class="sxs-lookup"><span data-stu-id="88f2b-195">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
