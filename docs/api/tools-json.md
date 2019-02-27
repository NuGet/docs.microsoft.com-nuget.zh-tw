---
title: tools.json 探索 nuget.exe 版本
description: 端點
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852529"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="32a48-103">tools.json 探索 nuget.exe 版本</span><span class="sxs-lookup"><span data-stu-id="32a48-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="32a48-104">現在，有幾種可編寫指令碼的方式在電腦上取得最新版的 nuget.exe 的方式。</span><span class="sxs-lookup"><span data-stu-id="32a48-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="32a48-105">例如，您可以下載並解壓縮[ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/)從 nuget.org 的套件。這會有一些複雜性，因為它可能需要您已經有 nuget.exe (如`nuget.exe install`) 或您必須解壓縮.nupkg 使用基本的解壓縮工具，並尋找二進位的內部。</span><span class="sxs-lookup"><span data-stu-id="32a48-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="32a48-106">如果您已經有 nuget.exe，您也可以使用`nuget.exe update -self`，但也必須有現有的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="32a48-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="32a48-107">這個方法也會更新您的最新版本。</span><span class="sxs-lookup"><span data-stu-id="32a48-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="32a48-108">它不允許使用特定版本。</span><span class="sxs-lookup"><span data-stu-id="32a48-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="32a48-109">`tools.json`端點會提供給同時解決啟動問題並讓您下載 nuget.exe 的版本控制。</span><span class="sxs-lookup"><span data-stu-id="32a48-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="32a48-110">這可用在 CI/CD 環境中，或在自訂指令碼來探索並下載任何已發行的新版的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="32a48-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="32a48-111">`tools.json`可以使用未經驗證的 HTTP 要求擷取端點 (例如`Invoke-WebRequest`在 PowerShell 中或`wget`)。</span><span class="sxs-lookup"><span data-stu-id="32a48-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="32a48-112">可以剖析使用 JSON 還原序列化程式，而且後續的 nuget.exe 下載 Url 可以也會擷取使用未經驗證的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="32a48-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="32a48-113">端點可以使用擷取`GET`方法：</span><span class="sxs-lookup"><span data-stu-id="32a48-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="32a48-114">[JSON 結構描述](http://json-schema.org/)的端點，請參閱這裡：</span><span class="sxs-lookup"><span data-stu-id="32a48-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="32a48-115">回應</span><span class="sxs-lookup"><span data-stu-id="32a48-115">Response</span></span>

<span data-ttu-id="32a48-116">回應是 nuget.exe 的 JSON 文件包含所有可用版本。</span><span class="sxs-lookup"><span data-stu-id="32a48-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="32a48-117">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="32a48-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="32a48-118">名稱</span><span class="sxs-lookup"><span data-stu-id="32a48-118">Name</span></span>      | <span data-ttu-id="32a48-119">類型</span><span class="sxs-lookup"><span data-stu-id="32a48-119">Type</span></span>             | <span data-ttu-id="32a48-120">必要</span><span class="sxs-lookup"><span data-stu-id="32a48-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="32a48-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="32a48-121">nuget.exe</span></span> | <span data-ttu-id="32a48-122">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="32a48-122">array of objects</span></span> | <span data-ttu-id="32a48-123">是</span><span class="sxs-lookup"><span data-stu-id="32a48-123">yes</span></span>

<span data-ttu-id="32a48-124">在每個物件`nuget.exe`陣列具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="32a48-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="32a48-125">名稱</span><span class="sxs-lookup"><span data-stu-id="32a48-125">Name</span></span>     | <span data-ttu-id="32a48-126">類型</span><span class="sxs-lookup"><span data-stu-id="32a48-126">Type</span></span>   | <span data-ttu-id="32a48-127">必要</span><span class="sxs-lookup"><span data-stu-id="32a48-127">Required</span></span> | <span data-ttu-id="32a48-128">注意</span><span class="sxs-lookup"><span data-stu-id="32a48-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="32a48-129">版本</span><span class="sxs-lookup"><span data-stu-id="32a48-129">version</span></span>  | <span data-ttu-id="32a48-130">字串</span><span class="sxs-lookup"><span data-stu-id="32a48-130">string</span></span> | <span data-ttu-id="32a48-131">是</span><span class="sxs-lookup"><span data-stu-id="32a48-131">yes</span></span>      | <span data-ttu-id="32a48-132">SemVer 2.0.0 字串</span><span class="sxs-lookup"><span data-stu-id="32a48-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="32a48-133">URL</span><span class="sxs-lookup"><span data-stu-id="32a48-133">url</span></span>      | <span data-ttu-id="32a48-134">字串</span><span class="sxs-lookup"><span data-stu-id="32a48-134">string</span></span> | <span data-ttu-id="32a48-135">是</span><span class="sxs-lookup"><span data-stu-id="32a48-135">yes</span></span>      | <span data-ttu-id="32a48-136">絕對 URL 下載這個新版的 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="32a48-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="32a48-137">階段</span><span class="sxs-lookup"><span data-stu-id="32a48-137">stage</span></span>    | <span data-ttu-id="32a48-138">字串</span><span class="sxs-lookup"><span data-stu-id="32a48-138">string</span></span> | <span data-ttu-id="32a48-139">是</span><span class="sxs-lookup"><span data-stu-id="32a48-139">yes</span></span>      | <span data-ttu-id="32a48-140">列舉字串</span><span class="sxs-lookup"><span data-stu-id="32a48-140">An enum string</span></span>
<span data-ttu-id="32a48-141">上傳</span><span class="sxs-lookup"><span data-stu-id="32a48-141">uploaded</span></span> | <span data-ttu-id="32a48-142">字串</span><span class="sxs-lookup"><span data-stu-id="32a48-142">string</span></span> | <span data-ttu-id="32a48-143">是</span><span class="sxs-lookup"><span data-stu-id="32a48-143">yes</span></span>      | <span data-ttu-id="32a48-144">版本時所提供之近似 ISO 8601 時間戳記</span><span class="sxs-lookup"><span data-stu-id="32a48-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="32a48-145">陣列中的項目會以遞減，SemVer 2.0.0 順序來排序。</span><span class="sxs-lookup"><span data-stu-id="32a48-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="32a48-146">這項保證是要降低最高的版本號碼有興趣的用戶端的負擔。</span><span class="sxs-lookup"><span data-stu-id="32a48-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="32a48-147">不過這表示不依時間順序排序清單。</span><span class="sxs-lookup"><span data-stu-id="32a48-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="32a48-148">例如，如果較舊的主要版本服務在日期晚於更高版本的主要版本中，此服務的版本不會出現在清單頂端。</span><span class="sxs-lookup"><span data-stu-id="32a48-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="32a48-149">如果您想要發行的最新版本*時間戳記*，只是排序的陣列`uploaded`字串。</span><span class="sxs-lookup"><span data-stu-id="32a48-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="32a48-150">這是因為`uploaded`時間戳記是以[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式也可以使用詞彙編篡排序 （也就是簡單的字串排序） 來依時間先後順序排序。</span><span class="sxs-lookup"><span data-stu-id="32a48-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="32a48-151">`stage`屬性表示是如何經審核的此版本的工具。</span><span class="sxs-lookup"><span data-stu-id="32a48-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="32a48-152">階段</span><span class="sxs-lookup"><span data-stu-id="32a48-152">Stage</span></span>              | <span data-ttu-id="32a48-153">意義</span><span class="sxs-lookup"><span data-stu-id="32a48-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="32a48-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="32a48-154">EarlyAccessPreview</span></span> | <span data-ttu-id="32a48-155">尚未顯示在[下載網頁](https://www.nuget.org/downloads)和應該由協力廠商驗證</span><span class="sxs-lookup"><span data-stu-id="32a48-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="32a48-156">已發行</span><span class="sxs-lookup"><span data-stu-id="32a48-156">Released</span></span>           | <span data-ttu-id="32a48-157">下載站台上的可用但尚未建議用於普遍耗用量</span><span class="sxs-lookup"><span data-stu-id="32a48-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="32a48-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="32a48-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="32a48-159">下載站台上的可用建議在耗用量</span><span class="sxs-lookup"><span data-stu-id="32a48-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="32a48-160">有最新一個簡單的作法，建議的版本是要採取的第一個版本的清單中，具有`stage`的值`ReleasedAndBlessed`。</span><span class="sxs-lookup"><span data-stu-id="32a48-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="32a48-161">這是因為 SemVer 2.0.0 順序排序的版本。</span><span class="sxs-lookup"><span data-stu-id="32a48-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="32a48-162">`NuGet.CommandLine` Nuget.org 上的封裝通常只會更新與`ReleasedAndBlessed`版本。</span><span class="sxs-lookup"><span data-stu-id="32a48-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="32a48-163">範例要求</span><span class="sxs-lookup"><span data-stu-id="32a48-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="32a48-164">範例回應</span><span class="sxs-lookup"><span data-stu-id="32a48-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
