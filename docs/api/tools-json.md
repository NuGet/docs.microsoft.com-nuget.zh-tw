---
title: 探索 nuget.exe 版本的 tools.js
description: 的端點
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773814"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="48274-103">探索 nuget.exe 版本的 tools.js</span><span class="sxs-lookup"><span data-stu-id="48274-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="48274-104">現在，有幾種方式可在電腦上以可編寫腳本的方式取得最新版本的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="48274-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="48274-105">例如，您可以從 nuget.org 下載並解壓縮 [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) 套件。這會有一些複雜性，因為它需要您已經有) 的 nuget.exe (， `nuget.exe install` 或是您必須使用基本的解壓縮工具解壓縮 nupkg，然後在內部尋找二進位檔。</span><span class="sxs-lookup"><span data-stu-id="48274-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="48274-106">如果您已經有 nuget.exe，也可以使用 `nuget.exe update -self` ，不過這也需要現有的 nuget.exe 複本。</span><span class="sxs-lookup"><span data-stu-id="48274-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="48274-107">這種方法也會將您更新至最新版本。</span><span class="sxs-lookup"><span data-stu-id="48274-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="48274-108">不允許使用特定版本。</span><span class="sxs-lookup"><span data-stu-id="48274-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="48274-109">`tools.json`端點可用於解決啟動載入問題，並提供您所下載之 nuget.exe 版本的控制權。</span><span class="sxs-lookup"><span data-stu-id="48274-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="48274-110">這可用於 CI/CD 環境或自訂腳本，以探索並下載任何已發行的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="48274-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="48274-111">您 `tools.json` 可以使用未經驗證的 HTTP (要求來提取端點，例如 `Invoke-WebRequest` 在 PowerShell 或 `wget`) 中。</span><span class="sxs-lookup"><span data-stu-id="48274-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="48274-112">您可以使用 JSON 還原序列化來剖析它，後續 nuget.exe 下載 Url 也可以使用未驗證的 HTTP 要求來提取。</span><span class="sxs-lookup"><span data-stu-id="48274-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="48274-113">您可以使用方法來提取端點 `GET` ：</span><span class="sxs-lookup"><span data-stu-id="48274-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="48274-114">您可以在這裡找到端點的 [JSON 架構](https://json-schema.org/) ：</span><span class="sxs-lookup"><span data-stu-id="48274-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="48274-115">回應</span><span class="sxs-lookup"><span data-stu-id="48274-115">Response</span></span>

<span data-ttu-id="48274-116">回應是 JSON 檔，其中包含所有可用的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="48274-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="48274-117">根 JSON 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="48274-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="48274-118">名稱</span><span class="sxs-lookup"><span data-stu-id="48274-118">Name</span></span>      | <span data-ttu-id="48274-119">類型</span><span class="sxs-lookup"><span data-stu-id="48274-119">Type</span></span>             | <span data-ttu-id="48274-120">必要</span><span class="sxs-lookup"><span data-stu-id="48274-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="48274-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="48274-121">nuget.exe</span></span> | <span data-ttu-id="48274-122">物件的陣列</span><span class="sxs-lookup"><span data-stu-id="48274-122">array of objects</span></span> | <span data-ttu-id="48274-123">是</span><span class="sxs-lookup"><span data-stu-id="48274-123">yes</span></span>

<span data-ttu-id="48274-124">陣列中的每個物件 `nuget.exe` 都有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="48274-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="48274-125">名稱</span><span class="sxs-lookup"><span data-stu-id="48274-125">Name</span></span>     | <span data-ttu-id="48274-126">類型</span><span class="sxs-lookup"><span data-stu-id="48274-126">Type</span></span>   | <span data-ttu-id="48274-127">必要</span><span class="sxs-lookup"><span data-stu-id="48274-127">Required</span></span> | <span data-ttu-id="48274-128">備註</span><span class="sxs-lookup"><span data-stu-id="48274-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="48274-129">version</span><span class="sxs-lookup"><span data-stu-id="48274-129">version</span></span>  | <span data-ttu-id="48274-130">字串</span><span class="sxs-lookup"><span data-stu-id="48274-130">string</span></span> | <span data-ttu-id="48274-131">是</span><span class="sxs-lookup"><span data-stu-id="48274-131">yes</span></span>      | <span data-ttu-id="48274-132">SemVer 2.0.0 字串</span><span class="sxs-lookup"><span data-stu-id="48274-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="48274-133">url</span><span class="sxs-lookup"><span data-stu-id="48274-133">url</span></span>      | <span data-ttu-id="48274-134">字串</span><span class="sxs-lookup"><span data-stu-id="48274-134">string</span></span> | <span data-ttu-id="48274-135">是</span><span class="sxs-lookup"><span data-stu-id="48274-135">yes</span></span>      | <span data-ttu-id="48274-136">下載此版本 nuget.exe 的絕對 URL</span><span class="sxs-lookup"><span data-stu-id="48274-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="48274-137">stage (階段)</span><span class="sxs-lookup"><span data-stu-id="48274-137">stage</span></span>    | <span data-ttu-id="48274-138">字串</span><span class="sxs-lookup"><span data-stu-id="48274-138">string</span></span> | <span data-ttu-id="48274-139">是</span><span class="sxs-lookup"><span data-stu-id="48274-139">yes</span></span>      | <span data-ttu-id="48274-140">列舉字串</span><span class="sxs-lookup"><span data-stu-id="48274-140">An enum string</span></span>
<span data-ttu-id="48274-141">上傳</span><span class="sxs-lookup"><span data-stu-id="48274-141">uploaded</span></span> | <span data-ttu-id="48274-142">字串</span><span class="sxs-lookup"><span data-stu-id="48274-142">string</span></span> | <span data-ttu-id="48274-143">是</span><span class="sxs-lookup"><span data-stu-id="48274-143">yes</span></span>      | <span data-ttu-id="48274-144">當版本可供使用時的大約 ISO 8601 時間戳記</span><span class="sxs-lookup"><span data-stu-id="48274-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="48274-145">陣列中的專案將會以遞減的 SemVer 2.0.0 順序排序。</span><span class="sxs-lookup"><span data-stu-id="48274-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="48274-146">這項保證的目的是要降低對最高版本號碼有興趣之用戶端的負擔。</span><span class="sxs-lookup"><span data-stu-id="48274-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="48274-147">不過這表示清單不是依時間順序排序。</span><span class="sxs-lookup"><span data-stu-id="48274-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="48274-148">例如，如果較低的主要版本在晚于較高主要版本的日期提供服務，此服務版本將不會出現在清單的頂端。</span><span class="sxs-lookup"><span data-stu-id="48274-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="48274-149">如果您想要以 *時間戳記* 發行的最新版本，只要依字串排序陣列即可 `uploaded` 。</span><span class="sxs-lookup"><span data-stu-id="48274-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="48274-150">這是有效的，因為 `uploaded` 時間戳記的格式為 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) ，可以使用字典排序來依時間順序排序 (例如，簡單的字串排序) 。</span><span class="sxs-lookup"><span data-stu-id="48274-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="48274-151">`stage`屬性工作表示此工具版本的通過。</span><span class="sxs-lookup"><span data-stu-id="48274-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="48274-152">階段</span><span class="sxs-lookup"><span data-stu-id="48274-152">Stage</span></span>              | <span data-ttu-id="48274-153">意義</span><span class="sxs-lookup"><span data-stu-id="48274-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="48274-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="48274-154">EarlyAccessPreview</span></span> | <span data-ttu-id="48274-155">尚未在 [下載網頁](https://www.nuget.org/downloads) 上顯示，應該由夥伴進行驗證</span><span class="sxs-lookup"><span data-stu-id="48274-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="48274-156">已發行</span><span class="sxs-lookup"><span data-stu-id="48274-156">Released</span></span>           | <span data-ttu-id="48274-157">在下載網站上提供，但不建議用於寬範圍耗用量</span><span class="sxs-lookup"><span data-stu-id="48274-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="48274-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="48274-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="48274-159">可在下載網站上取得，並建議用於耗用量</span><span class="sxs-lookup"><span data-stu-id="48274-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="48274-160">具有最新的建議版本的一個簡單方法是，採用清單中具有值的第一個版本 `stage` `ReleasedAndBlessed` 。</span><span class="sxs-lookup"><span data-stu-id="48274-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="48274-161">這是有效的，因為版本會以 SemVer 2.0.0 順序排序。</span><span class="sxs-lookup"><span data-stu-id="48274-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="48274-162">`NuGet.CommandLine`Nuget.org 上的封裝通常只會以 `ReleasedAndBlessed` 版本更新。</span><span class="sxs-lookup"><span data-stu-id="48274-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="48274-163">範例要求</span><span class="sxs-lookup"><span data-stu-id="48274-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="48274-164">範例回應</span><span class="sxs-lookup"><span data-stu-id="48274-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
