---
title: nuget.org 通訊協定
description: 與 NuGet 用戶端互動的不斷演進 nuget.org 通訊協定。
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773973"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="29427-103">nuget.org 通訊協定</span><span class="sxs-lookup"><span data-stu-id="29427-103">nuget.org protocols</span></span>

<span data-ttu-id="29427-104">若要與 nuget.org 互動，用戶端必須遵循特定的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="29427-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="29427-105">因為這些通訊協定會持續演進，所以用戶端必須識別在呼叫特定 nuget.org Api 時所使用的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="29427-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="29427-106">這可讓 nuget.org 針對舊版用戶端以不間斷的方式引進變更。</span><span class="sxs-lookup"><span data-stu-id="29427-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="29427-107">此頁面上記載的 Api 是 nuget.org 專屬的，而且不會預期其他 NuGet 伺服器的開發人員會引入這些 Api。</span><span class="sxs-lookup"><span data-stu-id="29427-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="29427-108">如需有關跨 NuGet 生態系統廣泛執行之 NuGet API 的詳細資訊，請參閱 [API 總覽](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="29427-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="29427-109">本主題將列出各種不同的通訊協定，以及它們是否存在。</span><span class="sxs-lookup"><span data-stu-id="29427-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="29427-110">NuGet 通訊協定版本4.1。0</span><span class="sxs-lookup"><span data-stu-id="29427-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="29427-111">4.1.0 通訊協定會指定驗證範圍金鑰的使用方式，以與 nuget.org 以外的服務進行互動，以針對 nuget.org 帳戶驗證套件。</span><span class="sxs-lookup"><span data-stu-id="29427-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="29427-112">請注意， `4.1.0` 版本號碼是不透明的字串，但會與支援此通訊協定的正式 NuGet 用戶端的第一個版本相符。</span><span class="sxs-lookup"><span data-stu-id="29427-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="29427-113">驗證可確保使用者建立的 API 金鑰只會與 nuget.org 搭配使用，而協力廠商服務的其他驗證或驗證則是透過一次性使用驗證範圍金鑰來處理。</span><span class="sxs-lookup"><span data-stu-id="29427-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="29427-114">這些驗證範圍金鑰可以用來驗證封裝是否屬於 nuget.org 上的特定使用者 (帳戶) 。</span><span class="sxs-lookup"><span data-stu-id="29427-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="29427-115">用戶端需求</span><span class="sxs-lookup"><span data-stu-id="29427-115">Client requirement</span></span>

<span data-ttu-id="29427-116">用戶端進行 API 呼叫以將套件 **推送** 至 nuget.org 時，必須傳遞下列標頭：</span><span class="sxs-lookup"><span data-stu-id="29427-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="29427-117">請注意， `X-NuGet-Client-Version` 標頭具有類似的語法，但只保留給官方 NuGet 用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="29427-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="29427-118">協力廠商用戶端應該使用 `X-NuGet-Protocol-Version` 標頭和值。</span><span class="sxs-lookup"><span data-stu-id="29427-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="29427-119">[ `PackagePublish` 資源](package-publish-resource.md)的檔中說明了 **推** 播通訊協定本身。</span><span class="sxs-lookup"><span data-stu-id="29427-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="29427-120">如果用戶端與外部服務互動，而且需要驗證封裝是否屬於特定使用者 (帳戶) ，則應該使用下列通訊協定，並使用驗證範圍金鑰，而不是 nuget.org 的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="29427-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="29427-121">要求驗證範圍金鑰的 API</span><span class="sxs-lookup"><span data-stu-id="29427-121">API to request a verify-scope key</span></span>

<span data-ttu-id="29427-122">此 API 可用來取得 nuget.org 作者的驗證範圍金鑰，以驗證其擁有的套件。</span><span class="sxs-lookup"><span data-stu-id="29427-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="29427-123">要求參數</span><span class="sxs-lookup"><span data-stu-id="29427-123">Request parameters</span></span>

<span data-ttu-id="29427-124">名稱</span><span class="sxs-lookup"><span data-stu-id="29427-124">Name</span></span>           | <span data-ttu-id="29427-125">位於</span><span class="sxs-lookup"><span data-stu-id="29427-125">In</span></span>     | <span data-ttu-id="29427-126">類型</span><span class="sxs-lookup"><span data-stu-id="29427-126">Type</span></span>   | <span data-ttu-id="29427-127">必要</span><span class="sxs-lookup"><span data-stu-id="29427-127">Required</span></span> | <span data-ttu-id="29427-128">備註</span><span class="sxs-lookup"><span data-stu-id="29427-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="29427-129">識別碼</span><span class="sxs-lookup"><span data-stu-id="29427-129">ID</span></span>             | <span data-ttu-id="29427-130">URL</span><span class="sxs-lookup"><span data-stu-id="29427-130">URL</span></span>    | <span data-ttu-id="29427-131">字串</span><span class="sxs-lookup"><span data-stu-id="29427-131">string</span></span> | <span data-ttu-id="29427-132">是</span><span class="sxs-lookup"><span data-stu-id="29427-132">yes</span></span>      | <span data-ttu-id="29427-133">要求驗證範圍金鑰的封裝 identidier</span><span class="sxs-lookup"><span data-stu-id="29427-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="29427-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="29427-134">VERSION</span></span>        | <span data-ttu-id="29427-135">URL</span><span class="sxs-lookup"><span data-stu-id="29427-135">URL</span></span>    | <span data-ttu-id="29427-136">字串</span><span class="sxs-lookup"><span data-stu-id="29427-136">string</span></span> | <span data-ttu-id="29427-137">不可以</span><span class="sxs-lookup"><span data-stu-id="29427-137">no</span></span>       | <span data-ttu-id="29427-138">套件版本</span><span class="sxs-lookup"><span data-stu-id="29427-138">The package version</span></span>
<span data-ttu-id="29427-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="29427-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="29427-140">標頭</span><span class="sxs-lookup"><span data-stu-id="29427-140">Header</span></span> | <span data-ttu-id="29427-141">字串</span><span class="sxs-lookup"><span data-stu-id="29427-141">string</span></span> | <span data-ttu-id="29427-142">是</span><span class="sxs-lookup"><span data-stu-id="29427-142">yes</span></span>      | <span data-ttu-id="29427-143">例如， `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="29427-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="29427-144">回應</span><span class="sxs-lookup"><span data-stu-id="29427-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="29427-145">驗證驗證範圍金鑰的 API</span><span class="sxs-lookup"><span data-stu-id="29427-145">API to verify the verify scope key</span></span>

<span data-ttu-id="29427-146">此 API 可用來驗證 nuget.org 作者所擁有之套件的驗證範圍金鑰。</span><span class="sxs-lookup"><span data-stu-id="29427-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="29427-147">要求參數</span><span class="sxs-lookup"><span data-stu-id="29427-147">Request parameters</span></span>

<span data-ttu-id="29427-148">名稱</span><span class="sxs-lookup"><span data-stu-id="29427-148">Name</span></span>           | <span data-ttu-id="29427-149">位於</span><span class="sxs-lookup"><span data-stu-id="29427-149">In</span></span>     | <span data-ttu-id="29427-150">類型</span><span class="sxs-lookup"><span data-stu-id="29427-150">Type</span></span>   | <span data-ttu-id="29427-151">必要</span><span class="sxs-lookup"><span data-stu-id="29427-151">Required</span></span> | <span data-ttu-id="29427-152">備註</span><span class="sxs-lookup"><span data-stu-id="29427-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="29427-153">識別碼</span><span class="sxs-lookup"><span data-stu-id="29427-153">ID</span></span>             | <span data-ttu-id="29427-154">URL</span><span class="sxs-lookup"><span data-stu-id="29427-154">URL</span></span>    | <span data-ttu-id="29427-155">字串</span><span class="sxs-lookup"><span data-stu-id="29427-155">string</span></span> | <span data-ttu-id="29427-156">是</span><span class="sxs-lookup"><span data-stu-id="29427-156">yes</span></span>      | <span data-ttu-id="29427-157">要求驗證範圍金鑰的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="29427-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="29427-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="29427-158">VERSION</span></span>        | <span data-ttu-id="29427-159">URL</span><span class="sxs-lookup"><span data-stu-id="29427-159">URL</span></span>    | <span data-ttu-id="29427-160">字串</span><span class="sxs-lookup"><span data-stu-id="29427-160">string</span></span> | <span data-ttu-id="29427-161">不可以</span><span class="sxs-lookup"><span data-stu-id="29427-161">no</span></span>       | <span data-ttu-id="29427-162">套件版本</span><span class="sxs-lookup"><span data-stu-id="29427-162">The package version</span></span>
<span data-ttu-id="29427-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="29427-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="29427-164">標頭</span><span class="sxs-lookup"><span data-stu-id="29427-164">Header</span></span> | <span data-ttu-id="29427-165">字串</span><span class="sxs-lookup"><span data-stu-id="29427-165">string</span></span> | <span data-ttu-id="29427-166">是</span><span class="sxs-lookup"><span data-stu-id="29427-166">yes</span></span>      | <span data-ttu-id="29427-167">例如， `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="29427-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="29427-168">此驗證範圍 API 金鑰會在一天內到期，或在第一次使用時到期（以先發生者為准）。</span><span class="sxs-lookup"><span data-stu-id="29427-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="29427-169">回應</span><span class="sxs-lookup"><span data-stu-id="29427-169">Response</span></span>

<span data-ttu-id="29427-170">狀態碼</span><span class="sxs-lookup"><span data-stu-id="29427-170">Status Code</span></span> | <span data-ttu-id="29427-171">意義</span><span class="sxs-lookup"><span data-stu-id="29427-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="29427-172">200</span><span class="sxs-lookup"><span data-stu-id="29427-172">200</span></span>         | <span data-ttu-id="29427-173">API 金鑰有效</span><span class="sxs-lookup"><span data-stu-id="29427-173">The API key is valid</span></span>
<span data-ttu-id="29427-174">403</span><span class="sxs-lookup"><span data-stu-id="29427-174">403</span></span>         | <span data-ttu-id="29427-175">API 金鑰無效或未獲授權可針對套件進行推送</span><span class="sxs-lookup"><span data-stu-id="29427-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="29427-176">404</span><span class="sxs-lookup"><span data-stu-id="29427-176">404</span></span>         | <span data-ttu-id="29427-177">所參考的封裝 `ID` 和 `VERSION` (選擇性) 不存在</span><span class="sxs-lookup"><span data-stu-id="29427-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
