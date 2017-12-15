---
title: "nuget.org 通訊協定 |Microsoft 文件"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "要與 NuGet 用戶端互動的發展 nuget.org 通訊協定。"
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="232bc-103">nuget.org 通訊協定</span><span class="sxs-lookup"><span data-stu-id="232bc-103">nuget.org Protocols</span></span>

<span data-ttu-id="232bc-104">若要與 nuget.org 互動，用戶端必須遵循特定的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="232bc-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="232bc-105">由於這些通訊協定保持進化，用戶端必須識別呼叫特定 nuget.org 應用程式開發介面時，他們使用的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="232bc-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="232bc-106">這可讓以非中斷的方式引入的變更，舊的用戶端的 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="232bc-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="232bc-107">此頁面上記載的 Api 僅供 nuget.org，而且沒有任何其他導入的這些 Api 的 NuGet 伺服器實作預期的情況。</span><span class="sxs-lookup"><span data-stu-id="232bc-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="232bc-108">如需 NuGet 的 API 實作廣泛 NuGet 生態系統資訊，請參閱[API 概觀](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="232bc-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="232bc-109">本主題列出各種的通訊協定和當他們回到至存在。</span><span class="sxs-lookup"><span data-stu-id="232bc-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="232bc-110">4.1.0 的 NuGet 通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="232bc-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="232bc-111">4.1.0 通訊協定指定 nuget.org，若要驗證封裝，以針對 nuget.org 帳戶以外的服務互動的驗證領域索引鍵使用方式。</span><span class="sxs-lookup"><span data-stu-id="232bc-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="232bc-112">請注意，`4.1.0`版本是不透明的字串，但發生的第一個版本支援此通訊協定的官方 NuGet 用戶端通常會一致。</span><span class="sxs-lookup"><span data-stu-id="232bc-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="232bc-113">驗證可確保使用者建立 API 金鑰只會搭配 nuget.org，，和該其他驗證或來自協力廠商服務的驗證透過使用一次驗證領域索引鍵。</span><span class="sxs-lookup"><span data-stu-id="232bc-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="232bc-114">這些範圍驗證金鑰可以用來驗證封裝所屬上 nuget.org 的特定使用者 （帳戶）。</span><span class="sxs-lookup"><span data-stu-id="232bc-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="232bc-115">用戶端需求</span><span class="sxs-lookup"><span data-stu-id="232bc-115">Client requirement</span></span>

<span data-ttu-id="232bc-116">用戶端都必須通過下列標頭，當他們完成應用程式開發介面呼叫**發送**nuget.org 的封裝：</span><span class="sxs-lookup"><span data-stu-id="232bc-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="232bc-117">請注意，預先`X-NuGet-Client-Version`標頭具有相同目的，但是目前已被取代，而且無法再使用。</span><span class="sxs-lookup"><span data-stu-id="232bc-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="232bc-118">**發送**本身的通訊協定所述的文件[`PackagePublish`資源](package-publish-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="232bc-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="232bc-119">如果用戶端與外部服務，必須驗證是否屬於特定的使用者 （帳戶） 的封裝互動時，它應該使用下列通訊協定，並使用驗證範圍和不從 nuget.org 的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="232bc-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="232bc-120">API 要求的驗證領域索引鍵</span><span class="sxs-lookup"><span data-stu-id="232bc-120">API to request a verify-scope key</span></span>

<span data-ttu-id="232bc-121">這個 API 用來取得 nuget.org 作者來驗證所經擁有封裝的驗證領域索引鍵。</span><span class="sxs-lookup"><span data-stu-id="232bc-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="232bc-122">要求參數</span><span class="sxs-lookup"><span data-stu-id="232bc-122">Request parameters</span></span>

<span data-ttu-id="232bc-123">名稱</span><span class="sxs-lookup"><span data-stu-id="232bc-123">Name</span></span>           | <span data-ttu-id="232bc-124">In</span><span class="sxs-lookup"><span data-stu-id="232bc-124">In</span></span>     | <span data-ttu-id="232bc-125">類型</span><span class="sxs-lookup"><span data-stu-id="232bc-125">Type</span></span>   | <span data-ttu-id="232bc-126">必要</span><span class="sxs-lookup"><span data-stu-id="232bc-126">Required</span></span> | <span data-ttu-id="232bc-127">注意</span><span class="sxs-lookup"><span data-stu-id="232bc-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="232bc-128">ID</span><span class="sxs-lookup"><span data-stu-id="232bc-128">ID</span></span>             | <span data-ttu-id="232bc-129">URL</span><span class="sxs-lookup"><span data-stu-id="232bc-129">URL</span></span>    | <span data-ttu-id="232bc-130">字串</span><span class="sxs-lookup"><span data-stu-id="232bc-130">string</span></span> | <span data-ttu-id="232bc-131">是</span><span class="sxs-lookup"><span data-stu-id="232bc-131">yes</span></span>      | <span data-ttu-id="232bc-132">要求的驗證領域索引鍵封裝 identidier</span><span class="sxs-lookup"><span data-stu-id="232bc-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="232bc-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="232bc-133">VERSION</span></span>        | <span data-ttu-id="232bc-134">URL</span><span class="sxs-lookup"><span data-stu-id="232bc-134">URL</span></span>    | <span data-ttu-id="232bc-135">字串</span><span class="sxs-lookup"><span data-stu-id="232bc-135">string</span></span> | <span data-ttu-id="232bc-136">no</span><span class="sxs-lookup"><span data-stu-id="232bc-136">no</span></span>       | <span data-ttu-id="232bc-137">封裝版本</span><span class="sxs-lookup"><span data-stu-id="232bc-137">The package version</span></span>
<span data-ttu-id="232bc-138">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="232bc-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="232bc-139">頁首</span><span class="sxs-lookup"><span data-stu-id="232bc-139">Header</span></span> | <span data-ttu-id="232bc-140">字串</span><span class="sxs-lookup"><span data-stu-id="232bc-140">string</span></span> | <span data-ttu-id="232bc-141">是</span><span class="sxs-lookup"><span data-stu-id="232bc-141">yes</span></span>      | <span data-ttu-id="232bc-142">例如：`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="232bc-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="232bc-143">回應</span><span class="sxs-lookup"><span data-stu-id="232bc-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="232bc-144">若要驗證的驗證領域索引鍵的 API</span><span class="sxs-lookup"><span data-stu-id="232bc-144">API to verify the verify scope key</span></span>

<span data-ttu-id="232bc-145">這個 API 用來驗證封裝 nuget.org 作者所擁有的驗證領域索引鍵。</span><span class="sxs-lookup"><span data-stu-id="232bc-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="232bc-146">要求參數</span><span class="sxs-lookup"><span data-stu-id="232bc-146">Request parameters</span></span>

<span data-ttu-id="232bc-147">名稱</span><span class="sxs-lookup"><span data-stu-id="232bc-147">Name</span></span>           | <span data-ttu-id="232bc-148">In</span><span class="sxs-lookup"><span data-stu-id="232bc-148">In</span></span>     | <span data-ttu-id="232bc-149">類型</span><span class="sxs-lookup"><span data-stu-id="232bc-149">Type</span></span>   | <span data-ttu-id="232bc-150">必要</span><span class="sxs-lookup"><span data-stu-id="232bc-150">Required</span></span> | <span data-ttu-id="232bc-151">注意</span><span class="sxs-lookup"><span data-stu-id="232bc-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="232bc-152">ID</span><span class="sxs-lookup"><span data-stu-id="232bc-152">ID</span></span>             | <span data-ttu-id="232bc-153">URL</span><span class="sxs-lookup"><span data-stu-id="232bc-153">URL</span></span>    | <span data-ttu-id="232bc-154">字串</span><span class="sxs-lookup"><span data-stu-id="232bc-154">string</span></span> | <span data-ttu-id="232bc-155">是</span><span class="sxs-lookup"><span data-stu-id="232bc-155">yes</span></span>      | <span data-ttu-id="232bc-156">要求的驗證領域索引鍵的封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="232bc-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="232bc-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="232bc-157">VERSION</span></span>        | <span data-ttu-id="232bc-158">URL</span><span class="sxs-lookup"><span data-stu-id="232bc-158">URL</span></span>    | <span data-ttu-id="232bc-159">字串</span><span class="sxs-lookup"><span data-stu-id="232bc-159">string</span></span> | <span data-ttu-id="232bc-160">no</span><span class="sxs-lookup"><span data-stu-id="232bc-160">no</span></span>       | <span data-ttu-id="232bc-161">封裝版本</span><span class="sxs-lookup"><span data-stu-id="232bc-161">The package version</span></span>
<span data-ttu-id="232bc-162">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="232bc-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="232bc-163">頁首</span><span class="sxs-lookup"><span data-stu-id="232bc-163">Header</span></span> | <span data-ttu-id="232bc-164">字串</span><span class="sxs-lookup"><span data-stu-id="232bc-164">string</span></span> | <span data-ttu-id="232bc-165">是</span><span class="sxs-lookup"><span data-stu-id="232bc-165">yes</span></span>      | <span data-ttu-id="232bc-166">例如：`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="232bc-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="232bc-167">此確認範圍 API 金鑰到期日的時間，或在第一次使用時，何者先發生。</span><span class="sxs-lookup"><span data-stu-id="232bc-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="232bc-168">回應</span><span class="sxs-lookup"><span data-stu-id="232bc-168">Response</span></span>

<span data-ttu-id="232bc-169">狀態碼</span><span class="sxs-lookup"><span data-stu-id="232bc-169">Status Code</span></span> | <span data-ttu-id="232bc-170">意義</span><span class="sxs-lookup"><span data-stu-id="232bc-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="232bc-171">200</span><span class="sxs-lookup"><span data-stu-id="232bc-171">200</span></span>         | <span data-ttu-id="232bc-172">API 金鑰無效</span><span class="sxs-lookup"><span data-stu-id="232bc-172">The API key is valid</span></span>
<span data-ttu-id="232bc-173">403</span><span class="sxs-lookup"><span data-stu-id="232bc-173">403</span></span>         | <span data-ttu-id="232bc-174">API 金鑰是無效或未獲授權來針對封裝推入</span><span class="sxs-lookup"><span data-stu-id="232bc-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="232bc-175">404</span><span class="sxs-lookup"><span data-stu-id="232bc-175">404</span></span>         | <span data-ttu-id="232bc-176">封裝所參考`ID`和`VERSION`（選擇性） 不存在</span><span class="sxs-lookup"><span data-stu-id="232bc-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
