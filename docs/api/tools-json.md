---
title: tools.json 探索 nuget.exe 版本
description: 端點
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546931"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="4109e-103">tools.json 探索 nuget.exe 版本</span><span class="sxs-lookup"><span data-stu-id="4109e-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="4109e-104">現在，有幾種可編寫指令碼的方式在電腦上取得最新版的 nuget.exe 的方式。</span><span class="sxs-lookup"><span data-stu-id="4109e-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="4109e-105">例如，您可以下載並解壓縮[ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/)從 nuget.org 的套件。這會有一些複雜性，因為它可能需要您已經有 nuget.exe (如`nuget.exe install`) 或您必須解壓縮.nupkg 使用基本的解壓縮工具，並尋找二進位的內部。</span><span class="sxs-lookup"><span data-stu-id="4109e-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="4109e-106">如果您已經有 nuget.exe，您也可以使用`nuget.exe update -self`，但也必須有現有的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="4109e-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="4109e-107">這個方法也會更新您的最新版本。</span><span class="sxs-lookup"><span data-stu-id="4109e-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="4109e-108">它不允許使用特定版本。</span><span class="sxs-lookup"><span data-stu-id="4109e-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="4109e-109">`tools.json`端點會提供給同時解決啟動問題並讓您下載 nuget.exe 的版本控制。</span><span class="sxs-lookup"><span data-stu-id="4109e-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="4109e-110">這可用在 CI/CD 環境中，或在自訂指令碼來探索並下載任何已發行的新版的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="4109e-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="4109e-111">`tools.json`可以使用未經驗證的 HTTP 要求擷取端點 (例如`Invoke-WebRequest`在 PowerShell 中或`wget`)。</span><span class="sxs-lookup"><span data-stu-id="4109e-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="4109e-112">可以剖析使用 JSON 還原序列化程式，而且後續的 nuget.exe 下載 Url 可以也會擷取使用未經驗證的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="4109e-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="4109e-113">端點可以使用擷取`GET`方法：</span><span class="sxs-lookup"><span data-stu-id="4109e-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="4109e-114">[JSON 結構描述](http://json-schema.org/)的端點，請參閱這裡：</span><span class="sxs-lookup"><span data-stu-id="4109e-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="4109e-115">回應</span><span class="sxs-lookup"><span data-stu-id="4109e-115">Response</span></span>

<span data-ttu-id="4109e-116">回應是 nuget.exe 的 JSON 文件包含所有可用版本。</span><span class="sxs-lookup"><span data-stu-id="4109e-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="4109e-117">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4109e-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="4109e-118">名稱</span><span class="sxs-lookup"><span data-stu-id="4109e-118">Name</span></span>      | <span data-ttu-id="4109e-119">類型</span><span class="sxs-lookup"><span data-stu-id="4109e-119">Type</span></span>             | <span data-ttu-id="4109e-120">必要</span><span class="sxs-lookup"><span data-stu-id="4109e-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="4109e-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4109e-121">nuget.exe</span></span> | <span data-ttu-id="4109e-122">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="4109e-122">array of objects</span></span> | <span data-ttu-id="4109e-123">是</span><span class="sxs-lookup"><span data-stu-id="4109e-123">yes</span></span>

<span data-ttu-id="4109e-124">在每個物件`nuget.exe`陣列具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4109e-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="4109e-125">名稱</span><span class="sxs-lookup"><span data-stu-id="4109e-125">Name</span></span>     | <span data-ttu-id="4109e-126">類型</span><span class="sxs-lookup"><span data-stu-id="4109e-126">Type</span></span>   | <span data-ttu-id="4109e-127">必要</span><span class="sxs-lookup"><span data-stu-id="4109e-127">Required</span></span> | <span data-ttu-id="4109e-128">注意</span><span class="sxs-lookup"><span data-stu-id="4109e-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="4109e-129">版本</span><span class="sxs-lookup"><span data-stu-id="4109e-129">version</span></span>  | <span data-ttu-id="4109e-130">字串</span><span class="sxs-lookup"><span data-stu-id="4109e-130">string</span></span> | <span data-ttu-id="4109e-131">是</span><span class="sxs-lookup"><span data-stu-id="4109e-131">yes</span></span>      | <span data-ttu-id="4109e-132">SemVer 2.0.0 字串</span><span class="sxs-lookup"><span data-stu-id="4109e-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="4109e-133">URL</span><span class="sxs-lookup"><span data-stu-id="4109e-133">url</span></span>      | <span data-ttu-id="4109e-134">字串</span><span class="sxs-lookup"><span data-stu-id="4109e-134">string</span></span> | <span data-ttu-id="4109e-135">是</span><span class="sxs-lookup"><span data-stu-id="4109e-135">yes</span></span>      | <span data-ttu-id="4109e-136">絕對 URL 下載這個新版的 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4109e-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="4109e-137">階段</span><span class="sxs-lookup"><span data-stu-id="4109e-137">stage</span></span>    | <span data-ttu-id="4109e-138">字串</span><span class="sxs-lookup"><span data-stu-id="4109e-138">string</span></span> | <span data-ttu-id="4109e-139">是</span><span class="sxs-lookup"><span data-stu-id="4109e-139">yes</span></span>      | <span data-ttu-id="4109e-140">列舉字串</span><span class="sxs-lookup"><span data-stu-id="4109e-140">An enum string</span></span>
<span data-ttu-id="4109e-141">上傳</span><span class="sxs-lookup"><span data-stu-id="4109e-141">uploaded</span></span> | <span data-ttu-id="4109e-142">字串</span><span class="sxs-lookup"><span data-stu-id="4109e-142">string</span></span> | <span data-ttu-id="4109e-143">是</span><span class="sxs-lookup"><span data-stu-id="4109e-143">yes</span></span>      | <span data-ttu-id="4109e-144">當版本所提供的大約時間戳記</span><span class="sxs-lookup"><span data-stu-id="4109e-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="4109e-145">陣列中的項目會以遞減，SemVer 2.0.0 順序來排序。</span><span class="sxs-lookup"><span data-stu-id="4109e-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="4109e-146">這項保證是要尋找最新版本的用戶端上減輕負擔。</span><span class="sxs-lookup"><span data-stu-id="4109e-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="4109e-147">`stage`屬性會指出 vettect 這個版本的工具的方式。</span><span class="sxs-lookup"><span data-stu-id="4109e-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="4109e-148">階段</span><span class="sxs-lookup"><span data-stu-id="4109e-148">Stage</span></span>              | <span data-ttu-id="4109e-149">意義</span><span class="sxs-lookup"><span data-stu-id="4109e-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="4109e-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="4109e-150">EarlyAccessPreview</span></span> | <span data-ttu-id="4109e-151">尚未顯示在[下載網頁](https://www.nuget.org/downloads)和應該由協力廠商驗證</span><span class="sxs-lookup"><span data-stu-id="4109e-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="4109e-152">已發行</span><span class="sxs-lookup"><span data-stu-id="4109e-152">Released</span></span>           | <span data-ttu-id="4109e-153">下載站台上的可用但尚未建議用於普遍耗用量</span><span class="sxs-lookup"><span data-stu-id="4109e-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="4109e-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="4109e-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="4109e-155">下載站台上的可用建議在耗用量</span><span class="sxs-lookup"><span data-stu-id="4109e-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="4109e-156">有最新一個簡單的作法，建議的版本是要採取的第一個版本的清單中，具有`stage`的值`ReleasedAndBlessed`。</span><span class="sxs-lookup"><span data-stu-id="4109e-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="4109e-157">`NuGet.CommandLine` Nuget.org 上的封裝通常只會更新與`ReleasedAndBlessed`版本。</span><span class="sxs-lookup"><span data-stu-id="4109e-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4109e-158">範例要求</span><span class="sxs-lookup"><span data-stu-id="4109e-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="4109e-159">範例回應</span><span class="sxs-lookup"><span data-stu-id="4109e-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
