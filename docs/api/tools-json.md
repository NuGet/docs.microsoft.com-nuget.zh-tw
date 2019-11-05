---
title: 用來探索 nuget.exe 版本的工具. json
description: 的端點
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611024"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="10479-103">用來探索 nuget.exe 版本的工具. json</span><span class="sxs-lookup"><span data-stu-id="10479-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="10479-104">今天，有幾種方式可讓您以腳本的方式，在您的電腦上取得最新版本的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="10479-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="10479-105">例如，您可以從 nuget.org 下載並解壓縮[`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/)套件。這有一些複雜性，因為它需要您已經有 nuget.exe （適用于 `nuget.exe install`），或者您必須使用基本的解壓縮工具來解壓縮 nupkg，並在裡面尋找二進位檔。</span><span class="sxs-lookup"><span data-stu-id="10479-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="10479-106">如果您已經有 nuget.exe，也可以使用 `nuget.exe update -self`，不過這也需要有一個現有的 nuget.exe 複本。</span><span class="sxs-lookup"><span data-stu-id="10479-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="10479-107">此方法也會將您更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="10479-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="10479-108">它不允許使用特定版本。</span><span class="sxs-lookup"><span data-stu-id="10479-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="10479-109">`tools.json` 端點可用來解決啟動載入問題，並提供您下載的 nuget.exe 版本的控制權。</span><span class="sxs-lookup"><span data-stu-id="10479-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="10479-110">這可用於 CI/CD 環境或自訂腳本，以探索並下載任何已發行的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="10479-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="10479-111">`tools.json` 端點可以使用未經驗證的 HTTP 要求來提取（例如，在 PowerShell 或 `wget`中 `Invoke-WebRequest`）。</span><span class="sxs-lookup"><span data-stu-id="10479-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="10479-112">它可以使用 JSON 還原序列化進行剖析，而後續的 nuget.exe 下載 Url 也可以使用未經驗證的 HTTP 要求來提取。</span><span class="sxs-lookup"><span data-stu-id="10479-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="10479-113">您可以使用 `GET` 方法來提取端點：</span><span class="sxs-lookup"><span data-stu-id="10479-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="10479-114">端點的[JSON 架構](https://json-schema.org/)可在這裡取得：</span><span class="sxs-lookup"><span data-stu-id="10479-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="10479-115">回應</span><span class="sxs-lookup"><span data-stu-id="10479-115">Response</span></span>

<span data-ttu-id="10479-116">回應是 JSON 檔，其中包含所有可用的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="10479-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="10479-117">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="10479-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="10479-118">[屬性]</span><span class="sxs-lookup"><span data-stu-id="10479-118">Name</span></span>      | <span data-ttu-id="10479-119">輸入</span><span class="sxs-lookup"><span data-stu-id="10479-119">Type</span></span>             | <span data-ttu-id="10479-120">必要項</span><span class="sxs-lookup"><span data-stu-id="10479-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="10479-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="10479-121">nuget.exe</span></span> | <span data-ttu-id="10479-122">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="10479-122">array of objects</span></span> | <span data-ttu-id="10479-123">是</span><span class="sxs-lookup"><span data-stu-id="10479-123">yes</span></span>

<span data-ttu-id="10479-124">`nuget.exe` 陣列中的每個物件都具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="10479-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="10479-125">[屬性]</span><span class="sxs-lookup"><span data-stu-id="10479-125">Name</span></span>     | <span data-ttu-id="10479-126">輸入</span><span class="sxs-lookup"><span data-stu-id="10479-126">Type</span></span>   | <span data-ttu-id="10479-127">必要項</span><span class="sxs-lookup"><span data-stu-id="10479-127">Required</span></span> | <span data-ttu-id="10479-128">備註</span><span class="sxs-lookup"><span data-stu-id="10479-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="10479-129">version</span><span class="sxs-lookup"><span data-stu-id="10479-129">version</span></span>  | <span data-ttu-id="10479-130">字串</span><span class="sxs-lookup"><span data-stu-id="10479-130">string</span></span> | <span data-ttu-id="10479-131">是</span><span class="sxs-lookup"><span data-stu-id="10479-131">yes</span></span>      | <span data-ttu-id="10479-132">SemVer 2.0.0 字串</span><span class="sxs-lookup"><span data-stu-id="10479-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="10479-133">URL</span><span class="sxs-lookup"><span data-stu-id="10479-133">url</span></span>      | <span data-ttu-id="10479-134">字串</span><span class="sxs-lookup"><span data-stu-id="10479-134">string</span></span> | <span data-ttu-id="10479-135">是</span><span class="sxs-lookup"><span data-stu-id="10479-135">yes</span></span>      | <span data-ttu-id="10479-136">下載此版本 nuget.exe 的絕對 URL</span><span class="sxs-lookup"><span data-stu-id="10479-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="10479-137">階段</span><span class="sxs-lookup"><span data-stu-id="10479-137">stage</span></span>    | <span data-ttu-id="10479-138">字串</span><span class="sxs-lookup"><span data-stu-id="10479-138">string</span></span> | <span data-ttu-id="10479-139">是</span><span class="sxs-lookup"><span data-stu-id="10479-139">yes</span></span>      | <span data-ttu-id="10479-140">列舉字串</span><span class="sxs-lookup"><span data-stu-id="10479-140">An enum string</span></span>
<span data-ttu-id="10479-141">#b0</span><span class="sxs-lookup"><span data-stu-id="10479-141">uploaded</span></span> | <span data-ttu-id="10479-142">字串</span><span class="sxs-lookup"><span data-stu-id="10479-142">string</span></span> | <span data-ttu-id="10479-143">是</span><span class="sxs-lookup"><span data-stu-id="10479-143">yes</span></span>      | <span data-ttu-id="10479-144">提供版本時的大約 ISO 8601 時間戳記</span><span class="sxs-lookup"><span data-stu-id="10479-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="10479-145">陣列中的專案將會以遞減的 SemVer 2.0.0 順序排序。</span><span class="sxs-lookup"><span data-stu-id="10479-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="10479-146">這項保證的目的是要降低用戶端對最高版本號碼感興趣的負擔。</span><span class="sxs-lookup"><span data-stu-id="10479-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="10479-147">不過，這表示清單不會依時間順序排序。</span><span class="sxs-lookup"><span data-stu-id="10479-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="10479-148">例如，如果在較高主要版本的日期之後提供較低的主要版本，則此服務版本將不會出現在清單的頂端。</span><span class="sxs-lookup"><span data-stu-id="10479-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="10479-149">如果您想要由*時間戳記*發行的最新版本，只要依 `uploaded` 字串排序陣列即可。</span><span class="sxs-lookup"><span data-stu-id="10479-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="10479-150">這是因為 `uploaded` 時間戳記是[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式，可以使用字典排序（也就是簡單字串排序）依時間順序排序。</span><span class="sxs-lookup"><span data-stu-id="10479-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="10479-151">`stage` 屬性指出此工具版本的通過方式。</span><span class="sxs-lookup"><span data-stu-id="10479-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="10479-152">階段</span><span class="sxs-lookup"><span data-stu-id="10479-152">Stage</span></span>              | <span data-ttu-id="10479-153">意義</span><span class="sxs-lookup"><span data-stu-id="10479-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="10479-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="10479-154">EarlyAccessPreview</span></span> | <span data-ttu-id="10479-155">尚未在[下載網頁](https://www.nuget.org/downloads)上顯示，應由合作夥伴驗證</span><span class="sxs-lookup"><span data-stu-id="10479-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="10479-156">已發行</span><span class="sxs-lookup"><span data-stu-id="10479-156">Released</span></span>           | <span data-ttu-id="10479-157">可在下載網站上取得，但不建議用於廣泛散佈的耗用量</span><span class="sxs-lookup"><span data-stu-id="10479-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="10479-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="10479-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="10479-159">可在下載網站上取得，建議用於耗用量</span><span class="sxs-lookup"><span data-stu-id="10479-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="10479-160">有最新的建議版本的一個簡單方法，就是採用清單中具有 `ReleasedAndBlessed``stage` 值的第一個版本。</span><span class="sxs-lookup"><span data-stu-id="10479-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="10479-161">這是可行的，因為版本會以 SemVer 2.0.0 順序排序。</span><span class="sxs-lookup"><span data-stu-id="10479-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="10479-162">Nuget.org 上的 `NuGet.CommandLine` 套件通常只會以 `ReleasedAndBlessed` 版本進行更新。</span><span class="sxs-lookup"><span data-stu-id="10479-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="10479-163">範例要求</span><span class="sxs-lookup"><span data-stu-id="10479-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="10479-164">範例回應</span><span class="sxs-lookup"><span data-stu-id="10479-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
