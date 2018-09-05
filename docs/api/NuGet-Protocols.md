---
title: nuget.org 通訊協定
description: 要與 NuGet 用戶端互動的發展 nuget.org 通訊協定。
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547269"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="e0503-103">nuget.org 通訊協定</span><span class="sxs-lookup"><span data-stu-id="e0503-103">nuget.org protocols</span></span>

<span data-ttu-id="e0503-104">若要與 nuget.org 互動，用戶端必須遵循特定通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e0503-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="e0503-105">這些通訊協定將持續進化的因為用戶端必須找出呼叫特定 nuget.org 的 Api 時，他們使用的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="e0503-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="e0503-106">這可讓以非中斷的方式會造成變更，舊的用戶端的 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="e0503-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="e0503-107">在此頁面上記載的 Api 特有 nuget.org 還有不會預期其他介紹這些 Api 的 NuGet 伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="e0503-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="e0503-108">廣泛實作橫跨 NuGet 生態系統的 NuGet API 的相關資訊，請參閱[API 概觀](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e0503-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="e0503-109">本主題列出各種通訊協定，當它們再存在。</span><span class="sxs-lookup"><span data-stu-id="e0503-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="e0503-110">NuGet 4.1.0 的通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="e0503-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="e0503-111">4.1.0 通訊協定指定驗證範圍 nuget.org，若要驗證套件的 nuget.org 帳戶以外的服務進行互動的金鑰使用方式。</span><span class="sxs-lookup"><span data-stu-id="e0503-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="e0503-112">請注意，`4.1.0`是不透明的字串，但剛好符合官方 NuGet 用戶端支援此通訊協定的第一個版本的版本。</span><span class="sxs-lookup"><span data-stu-id="e0503-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="e0503-113">驗證可確保使用者建立 API 金鑰只會搭配 nuget.org，，和該其他驗證或從協力廠商服務的驗證透過使用一次驗證領域索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e0503-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="e0503-114">這些驗證範圍金鑰可用來驗證封裝所屬 nuget.org 上的特定使用者 （帳戶）。</span><span class="sxs-lookup"><span data-stu-id="e0503-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="e0503-115">用戶端需求</span><span class="sxs-lookup"><span data-stu-id="e0503-115">Client requirement</span></span>

<span data-ttu-id="e0503-116">用戶端都必須通過下列標頭，當它們進行 API 呼叫來**推播**至 nuget.org 的套件：</span><span class="sxs-lookup"><span data-stu-id="e0503-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="e0503-117">請注意，`X-NuGet-Client-Version`標頭的語意很類似，但會保留僅供官方 NuGet 用戶端。</span><span class="sxs-lookup"><span data-stu-id="e0503-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="e0503-118">協力廠商用戶端應該使用`X-NuGet-Protocol-Version`標頭和值。</span><span class="sxs-lookup"><span data-stu-id="e0503-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="e0503-119">**推播**通訊協定本身所述的文件[`PackagePublish`資源](package-publish-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="e0503-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="e0503-120">如果用戶端與外部服務，且必須驗證是否屬於特定使用者 （帳戶） 的封裝互動時，它應該使用下列通訊協定，並使用的驗證領域索引鍵和不從 nuget.org 的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e0503-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="e0503-121">若要確認範圍金鑰的 API</span><span class="sxs-lookup"><span data-stu-id="e0503-121">API to request a verify-scope key</span></span>

<span data-ttu-id="e0503-122">此 API 用來取得驗證領域金鑰來驗證封裝，其所擁有的 nuget.org 作者。</span><span class="sxs-lookup"><span data-stu-id="e0503-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="e0503-123">要求參數</span><span class="sxs-lookup"><span data-stu-id="e0503-123">Request parameters</span></span>

<span data-ttu-id="e0503-124">名稱</span><span class="sxs-lookup"><span data-stu-id="e0503-124">Name</span></span>           | <span data-ttu-id="e0503-125">In</span><span class="sxs-lookup"><span data-stu-id="e0503-125">In</span></span>     | <span data-ttu-id="e0503-126">類型</span><span class="sxs-lookup"><span data-stu-id="e0503-126">Type</span></span>   | <span data-ttu-id="e0503-127">必要</span><span class="sxs-lookup"><span data-stu-id="e0503-127">Required</span></span> | <span data-ttu-id="e0503-128">注意</span><span class="sxs-lookup"><span data-stu-id="e0503-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e0503-129">識別碼</span><span class="sxs-lookup"><span data-stu-id="e0503-129">ID</span></span>             | <span data-ttu-id="e0503-130">URL</span><span class="sxs-lookup"><span data-stu-id="e0503-130">URL</span></span>    | <span data-ttu-id="e0503-131">字串</span><span class="sxs-lookup"><span data-stu-id="e0503-131">string</span></span> | <span data-ttu-id="e0503-132">是</span><span class="sxs-lookup"><span data-stu-id="e0503-132">yes</span></span>      | <span data-ttu-id="e0503-133">要求的驗證領域索引鍵封裝 identidier</span><span class="sxs-lookup"><span data-stu-id="e0503-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="e0503-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="e0503-134">VERSION</span></span>        | <span data-ttu-id="e0503-135">URL</span><span class="sxs-lookup"><span data-stu-id="e0503-135">URL</span></span>    | <span data-ttu-id="e0503-136">字串</span><span class="sxs-lookup"><span data-stu-id="e0503-136">string</span></span> | <span data-ttu-id="e0503-137">否</span><span class="sxs-lookup"><span data-stu-id="e0503-137">no</span></span>       | <span data-ttu-id="e0503-138">套件版本</span><span class="sxs-lookup"><span data-stu-id="e0503-138">The package version</span></span>
<span data-ttu-id="e0503-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="e0503-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="e0503-140">頁首</span><span class="sxs-lookup"><span data-stu-id="e0503-140">Header</span></span> | <span data-ttu-id="e0503-141">字串</span><span class="sxs-lookup"><span data-stu-id="e0503-141">string</span></span> | <span data-ttu-id="e0503-142">是</span><span class="sxs-lookup"><span data-stu-id="e0503-142">yes</span></span>      | <span data-ttu-id="e0503-143">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="e0503-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="e0503-144">回應</span><span class="sxs-lookup"><span data-stu-id="e0503-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="e0503-145">若要驗證的驗證領域索引鍵的 API</span><span class="sxs-lookup"><span data-stu-id="e0503-145">API to verify the verify scope key</span></span>

<span data-ttu-id="e0503-146">此 API 用來驗證套件 nuget.org 作者所擁有的驗證領域索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e0503-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="e0503-147">要求參數</span><span class="sxs-lookup"><span data-stu-id="e0503-147">Request parameters</span></span>

<span data-ttu-id="e0503-148">名稱</span><span class="sxs-lookup"><span data-stu-id="e0503-148">Name</span></span>           | <span data-ttu-id="e0503-149">In</span><span class="sxs-lookup"><span data-stu-id="e0503-149">In</span></span>     | <span data-ttu-id="e0503-150">類型</span><span class="sxs-lookup"><span data-stu-id="e0503-150">Type</span></span>   | <span data-ttu-id="e0503-151">必要</span><span class="sxs-lookup"><span data-stu-id="e0503-151">Required</span></span> | <span data-ttu-id="e0503-152">注意</span><span class="sxs-lookup"><span data-stu-id="e0503-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="e0503-153">識別碼</span><span class="sxs-lookup"><span data-stu-id="e0503-153">ID</span></span>             | <span data-ttu-id="e0503-154">URL</span><span class="sxs-lookup"><span data-stu-id="e0503-154">URL</span></span>    | <span data-ttu-id="e0503-155">字串</span><span class="sxs-lookup"><span data-stu-id="e0503-155">string</span></span> | <span data-ttu-id="e0503-156">是</span><span class="sxs-lookup"><span data-stu-id="e0503-156">yes</span></span>      | <span data-ttu-id="e0503-157">要求的驗證領域索引鍵的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="e0503-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="e0503-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="e0503-158">VERSION</span></span>        | <span data-ttu-id="e0503-159">URL</span><span class="sxs-lookup"><span data-stu-id="e0503-159">URL</span></span>    | <span data-ttu-id="e0503-160">字串</span><span class="sxs-lookup"><span data-stu-id="e0503-160">string</span></span> | <span data-ttu-id="e0503-161">否</span><span class="sxs-lookup"><span data-stu-id="e0503-161">no</span></span>       | <span data-ttu-id="e0503-162">套件版本</span><span class="sxs-lookup"><span data-stu-id="e0503-162">The package version</span></span>
<span data-ttu-id="e0503-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="e0503-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="e0503-164">頁首</span><span class="sxs-lookup"><span data-stu-id="e0503-164">Header</span></span> | <span data-ttu-id="e0503-165">字串</span><span class="sxs-lookup"><span data-stu-id="e0503-165">string</span></span> | <span data-ttu-id="e0503-166">是</span><span class="sxs-lookup"><span data-stu-id="e0503-166">yes</span></span>      | <span data-ttu-id="e0503-167">例如：`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="e0503-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="e0503-168">此驗證範圍的 API 金鑰將於一天的時間到期，或在第一次使用時，何者先發生。</span><span class="sxs-lookup"><span data-stu-id="e0503-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="e0503-169">回應</span><span class="sxs-lookup"><span data-stu-id="e0503-169">Response</span></span>

<span data-ttu-id="e0503-170">狀態碼</span><span class="sxs-lookup"><span data-stu-id="e0503-170">Status Code</span></span> | <span data-ttu-id="e0503-171">意義</span><span class="sxs-lookup"><span data-stu-id="e0503-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="e0503-172">200</span><span class="sxs-lookup"><span data-stu-id="e0503-172">200</span></span>         | <span data-ttu-id="e0503-173">API 金鑰無效</span><span class="sxs-lookup"><span data-stu-id="e0503-173">The API key is valid</span></span>
<span data-ttu-id="e0503-174">403</span><span class="sxs-lookup"><span data-stu-id="e0503-174">403</span></span>         | <span data-ttu-id="e0503-175">API 金鑰不正確或未獲授權，以針對封裝推送</span><span class="sxs-lookup"><span data-stu-id="e0503-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="e0503-176">404</span><span class="sxs-lookup"><span data-stu-id="e0503-176">404</span></span>         | <span data-ttu-id="e0503-177">所參考封裝`ID`和`VERSION`（選擇性） 不存在</span><span class="sxs-lookup"><span data-stu-id="e0503-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
