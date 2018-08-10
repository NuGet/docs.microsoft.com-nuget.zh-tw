---
title: 存放庫簽章，NuGet API |Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 存放庫簽章資源可讓用戶端地宣布其簽署功能的存放庫的套件來源。
keywords: NuGet API 存放庫簽章、 簽章憑證，nuget.org nuget.org 套件簽署
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020553"
---
# <a name="repository-signatures"></a><span data-ttu-id="fd7fb-104">存放庫簽章</span><span class="sxs-lookup"><span data-stu-id="fd7fb-104">Repository signatures</span></span>

<span data-ttu-id="fd7fb-105">如果套件來源支援新增存放庫簽章，以發佈的封裝，就可以判斷所使用的套件來源的簽章憑證的用戶端。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="fd7fb-106">這項資源可讓用戶端偵測封裝存放庫簽章是否遭到竄改，或有非預期的簽章憑證。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="fd7fb-107">用於擷取此存放庫簽章資訊的資源`RepositorySignatures`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="fd7fb-108">NuGet.org 會宣布啟動`RepositorySignatures`在不久的將來的資源。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="fd7fb-109">版本控制</span><span class="sxs-lookup"><span data-stu-id="fd7fb-109">Versioning</span></span>

<span data-ttu-id="fd7fb-110">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="fd7fb-110">The following `@type` value is used:</span></span>

<span data-ttu-id="fd7fb-111">@type 值</span><span class="sxs-lookup"><span data-stu-id="fd7fb-111">@type value</span></span>                | <span data-ttu-id="fd7fb-112">注意</span><span class="sxs-lookup"><span data-stu-id="fd7fb-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="fd7fb-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="fd7fb-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="fd7fb-114">初始版本</span><span class="sxs-lookup"><span data-stu-id="fd7fb-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="fd7fb-115">基礎 URL</span><span class="sxs-lookup"><span data-stu-id="fd7fb-115">Base URL</span></span>

<span data-ttu-id="fd7fb-116">下列 Api 的進入點 URL 是 windows 7`@id`上述的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="fd7fb-117">本主題使用的預留位置 URL `{@id}`。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="fd7fb-118">請注意，不同於其他資源， `{@id}` URL，才能透過 HTTPS 提供服務。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fd7fb-119">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="fd7fb-119">HTTP methods</span></span>

<span data-ttu-id="fd7fb-120">在存放庫簽章資源支援的 HTTP 方法中找到的所有 Url`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="fd7fb-121">存放庫簽章索引</span><span class="sxs-lookup"><span data-stu-id="fd7fb-121">Repository signatures index</span></span>

<span data-ttu-id="fd7fb-122">存放庫簽章索引包含兩項資訊：</span><span class="sxs-lookup"><span data-stu-id="fd7fb-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="fd7fb-123">在來源上找到所有的套件是經過此套件來源的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="fd7fb-124">用來簽署套件的套件來源的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="fd7fb-125">在大部分情況下，憑證清單只會將附加到。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="fd7fb-126">先前的簽署憑證已過期，而且若要開始使用新的簽署憑證需要的套件來源時，新的憑證將會新增至清單。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="fd7fb-127">如果憑證從清單中移除，這表示，使用已移除的簽署憑證建立的所有套件簽章應不會再都視為有效用戶端。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="fd7fb-128">在此情況下，封裝簽章 （但不是一定是封裝） 無效。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="fd7fb-129">用戶端原則可能會允許安裝為不帶正負號的套件。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="fd7fb-130">如果憑證撤銷 （例如金鑰洩露），是封裝來源預期放棄所有受影響的憑證所簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to resign all packages signed by the affected certificate.</span></span> <span data-ttu-id="fd7fb-131">此外，套件來源應該移除受影響的憑證簽署的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="fd7fb-132">下列要求擷取存放庫簽章索引。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="fd7fb-133">存放庫簽章索引是 JSON 文件，其中包含具有下列屬性的物件：</span><span class="sxs-lookup"><span data-stu-id="fd7fb-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="fd7fb-134">名稱</span><span class="sxs-lookup"><span data-stu-id="fd7fb-134">Name</span></span>                | <span data-ttu-id="fd7fb-135">類型</span><span class="sxs-lookup"><span data-stu-id="fd7fb-135">Type</span></span>             | <span data-ttu-id="fd7fb-136">必要</span><span class="sxs-lookup"><span data-stu-id="fd7fb-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="fd7fb-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="fd7fb-137">allRepositorySigned</span></span> | <span data-ttu-id="fd7fb-138">boolean</span><span class="sxs-lookup"><span data-stu-id="fd7fb-138">boolean</span></span>          | <span data-ttu-id="fd7fb-139">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-139">yes</span></span>
<span data-ttu-id="fd7fb-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="fd7fb-140">signingCertificates</span></span> | <span data-ttu-id="fd7fb-141">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="fd7fb-141">array of objects</span></span> | <span data-ttu-id="fd7fb-142">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-142">yes</span></span>

<span data-ttu-id="fd7fb-143">`allRepositorySigned`布林值為 false，如果套件來源具有一些套件有沒有存放庫簽章。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="fd7fb-144">如果布林值會設為 true，在所有的封裝來源必須具有存放庫簽章所述的簽章憑證的其中一個產生`signingCertificates`。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="fd7fb-145">應該有一或多個中的簽署憑證`signingCertificates`陣列，如果`allRepositorySigned`布林值會設為 true。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="fd7fb-146">如果是空的陣列和`allRepositorySigned`設為 true，所有的封裝來源的資料應視為無效，雖然用戶端原則仍然允許套件耗用量。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="fd7fb-147">此陣列中的每個項目是具有下列屬性的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="fd7fb-148">名稱</span><span class="sxs-lookup"><span data-stu-id="fd7fb-148">Name</span></span>         | <span data-ttu-id="fd7fb-149">類型</span><span class="sxs-lookup"><span data-stu-id="fd7fb-149">Type</span></span>   | <span data-ttu-id="fd7fb-150">必要</span><span class="sxs-lookup"><span data-stu-id="fd7fb-150">Required</span></span> | <span data-ttu-id="fd7fb-151">注意</span><span class="sxs-lookup"><span data-stu-id="fd7fb-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="fd7fb-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="fd7fb-152">contentUrl</span></span>   | <span data-ttu-id="fd7fb-153">字串</span><span class="sxs-lookup"><span data-stu-id="fd7fb-153">string</span></span> | <span data-ttu-id="fd7fb-154">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-154">yes</span></span>      | <span data-ttu-id="fd7fb-155">DER 編碼的公開憑證的絕對 URL</span><span class="sxs-lookup"><span data-stu-id="fd7fb-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="fd7fb-156">指紋</span><span class="sxs-lookup"><span data-stu-id="fd7fb-156">fingerprints</span></span> | <span data-ttu-id="fd7fb-157">object</span><span class="sxs-lookup"><span data-stu-id="fd7fb-157">object</span></span> | <span data-ttu-id="fd7fb-158">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-158">yes</span></span>      |
<span data-ttu-id="fd7fb-159">主旨</span><span class="sxs-lookup"><span data-stu-id="fd7fb-159">subject</span></span>      | <span data-ttu-id="fd7fb-160">字串</span><span class="sxs-lookup"><span data-stu-id="fd7fb-160">string</span></span> | <span data-ttu-id="fd7fb-161">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-161">yes</span></span>      | <span data-ttu-id="fd7fb-162">從憑證主體辨別的名稱</span><span class="sxs-lookup"><span data-stu-id="fd7fb-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="fd7fb-163">issuer</span><span class="sxs-lookup"><span data-stu-id="fd7fb-163">issuer</span></span>       | <span data-ttu-id="fd7fb-164">字串</span><span class="sxs-lookup"><span data-stu-id="fd7fb-164">string</span></span> | <span data-ttu-id="fd7fb-165">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-165">yes</span></span>      | <span data-ttu-id="fd7fb-166">憑證的簽發者的辨別的名稱</span><span class="sxs-lookup"><span data-stu-id="fd7fb-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="fd7fb-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="fd7fb-167">notBefore</span></span>    | <span data-ttu-id="fd7fb-168">字串</span><span class="sxs-lookup"><span data-stu-id="fd7fb-168">string</span></span> | <span data-ttu-id="fd7fb-169">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-169">yes</span></span>      | <span data-ttu-id="fd7fb-170">憑證的有效期間的開始時間戳記</span><span class="sxs-lookup"><span data-stu-id="fd7fb-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="fd7fb-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="fd7fb-171">notAfter</span></span>     | <span data-ttu-id="fd7fb-172">字串</span><span class="sxs-lookup"><span data-stu-id="fd7fb-172">string</span></span> | <span data-ttu-id="fd7fb-173">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-173">yes</span></span>      | <span data-ttu-id="fd7fb-174">憑證的有效期間結束的時間戳記</span><span class="sxs-lookup"><span data-stu-id="fd7fb-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="fd7fb-175">請注意，`contentUrl`才能透過 HTTPS 提供服務。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="fd7fb-176">此 URL 有沒有特定的 URL 模式，而且必須動態探索使用此存放庫簽章索引文件。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="fd7fb-177">這個物件中的所有屬性 (除了來自`contentUrl`) 必須是可從憑證，請參閱衍生`contentUrl`。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="fd7fb-178">為了方便起見，將往返降至最低，會提供這些可衍生的屬性。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="fd7fb-179">`fingerprints`物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="fd7fb-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="fd7fb-180">名稱</span><span class="sxs-lookup"><span data-stu-id="fd7fb-180">Name</span></span>                   | <span data-ttu-id="fd7fb-181">類型</span><span class="sxs-lookup"><span data-stu-id="fd7fb-181">Type</span></span>   | <span data-ttu-id="fd7fb-182">必要</span><span class="sxs-lookup"><span data-stu-id="fd7fb-182">Required</span></span> | <span data-ttu-id="fd7fb-183">注意</span><span class="sxs-lookup"><span data-stu-id="fd7fb-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="fd7fb-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="fd7fb-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="fd7fb-185">字串</span><span class="sxs-lookup"><span data-stu-id="fd7fb-185">string</span></span> | <span data-ttu-id="fd7fb-186">是</span><span class="sxs-lookup"><span data-stu-id="fd7fb-186">yes</span></span>      | <span data-ttu-id="fd7fb-187">SHA-256 指紋</span><span class="sxs-lookup"><span data-stu-id="fd7fb-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="fd7fb-188">索引鍵名稱`2.16.840.1.101.3.4.2.1`是 SHA-256 雜湊演算法的 OID。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="fd7fb-189">所有的雜湊值必須是摘要的小寫字母、 十六進位編碼的字串表示的雜湊。</span><span class="sxs-lookup"><span data-stu-id="fd7fb-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fd7fb-190">範例要求</span><span class="sxs-lookup"><span data-stu-id="fd7fb-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="fd7fb-191">範例回應</span><span class="sxs-lookup"><span data-stu-id="fd7fb-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
