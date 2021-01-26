---
title: 服務索引，NuGet API
description: 服務索引是 NuGet HTTP API 的進入點，而且會列舉伺服器的功能。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775356"
---
# <a name="service-index"></a><span data-ttu-id="e2ea5-103">服務索引</span><span class="sxs-lookup"><span data-stu-id="e2ea5-103">Service index</span></span>

<span data-ttu-id="e2ea5-104">服務索引是一個 JSON 檔，它是 NuGet 套件來源的進入點，可讓用戶端執行探索套件來源的功能。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="e2ea5-105">服務索引是具有兩個必要屬性的 JSON 物件： `version` (服務索引的架構版本) 和 `resources`  (套件來源) 的端點或功能。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="e2ea5-106">nuget.exe 的服務索引位於 `https://api.nuget.org/v3/index.json` 。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="e2ea5-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="e2ea5-107">Versioning</span></span>

<span data-ttu-id="e2ea5-108">`version`值是 SemVer 2.0.0 剖析或是版本字串，表示服務索引的架構版本。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="e2ea5-109">API 會要求版本字串具有的主要版本號碼 `3` 。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="e2ea5-110">對服務索引架構進行非中斷的變更時，將會增加版本字串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="e2ea5-111">服務索引中的每個資源都會與服務索引架構版本分開建立版本。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="e2ea5-112">目前的架構版本是 `3.0.0` 。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="e2ea5-113">`3.0.0`版本的功能等同于較舊的 `3.0.0-beta.1` 版本，但應優先于更明確地傳達穩定的已定義架構。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e2ea5-114">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="e2ea5-114">HTTP methods</span></span>

<span data-ttu-id="e2ea5-115">您可以使用 HTTP 方法和來存取服務索引 `GET` `HEAD` 。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="e2ea5-116">資源</span><span class="sxs-lookup"><span data-stu-id="e2ea5-116">Resources</span></span>

<span data-ttu-id="e2ea5-117">`resources`屬性包含此封裝來源所支援的資源陣列。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="e2ea5-118">資源</span><span class="sxs-lookup"><span data-stu-id="e2ea5-118">Resource</span></span>

<span data-ttu-id="e2ea5-119">資源是陣列中的物件 `resources` 。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="e2ea5-120">它代表套件來源的已建立版本功能。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="e2ea5-121">資源具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e2ea5-121">A resource has the following properties:</span></span>

<span data-ttu-id="e2ea5-122">名稱</span><span class="sxs-lookup"><span data-stu-id="e2ea5-122">Name</span></span>          | <span data-ttu-id="e2ea5-123">類型</span><span class="sxs-lookup"><span data-stu-id="e2ea5-123">Type</span></span>   | <span data-ttu-id="e2ea5-124">必要</span><span class="sxs-lookup"><span data-stu-id="e2ea5-124">Required</span></span> | <span data-ttu-id="e2ea5-125">備註</span><span class="sxs-lookup"><span data-stu-id="e2ea5-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="e2ea5-126">字串</span><span class="sxs-lookup"><span data-stu-id="e2ea5-126">string</span></span> | <span data-ttu-id="e2ea5-127">是</span><span class="sxs-lookup"><span data-stu-id="e2ea5-127">yes</span></span>      | <span data-ttu-id="e2ea5-128">資源的 URL</span><span class="sxs-lookup"><span data-stu-id="e2ea5-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="e2ea5-129">字串</span><span class="sxs-lookup"><span data-stu-id="e2ea5-129">string</span></span> | <span data-ttu-id="e2ea5-130">是</span><span class="sxs-lookup"><span data-stu-id="e2ea5-130">yes</span></span>      | <span data-ttu-id="e2ea5-131">代表資源類型的字串常數。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-131">A string constant representing the resource type</span></span>
<span data-ttu-id="e2ea5-132">comment</span><span class="sxs-lookup"><span data-stu-id="e2ea5-132">comment</span></span>       | <span data-ttu-id="e2ea5-133">字串</span><span class="sxs-lookup"><span data-stu-id="e2ea5-133">string</span></span> | <span data-ttu-id="e2ea5-134">不可以</span><span class="sxs-lookup"><span data-stu-id="e2ea5-134">no</span></span>       | <span data-ttu-id="e2ea5-135">人們看得懂的資源描述</span><span class="sxs-lookup"><span data-stu-id="e2ea5-135">A human readable description of the resource</span></span>

<span data-ttu-id="e2ea5-136">`@id`是必須是絕對的 URL，而且必須有 HTTP 或 HTTPS 架構。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="e2ea5-137">`@type`用來識別與資源互動時要使用的特定通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="e2ea5-138">資源的類型是不透明的字串，但其格式通常為：</span><span class="sxs-lookup"><span data-stu-id="e2ea5-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="e2ea5-139">用戶端預期會將其瞭解的值硬編碼， `@type` 並在套件來源的服務索引中查詢它們。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="e2ea5-140">`@type`目前使用的確切值會列舉在[API 總覽](overview.md#resources-and-schema)中列出的個別資源參考檔上。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="e2ea5-141">基於本檔的目的，有關不同資源的檔基本上會依在 `{RESOURCE_NAME}` 服務索引中找到的分組，類似于依案例分組。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="e2ea5-142">不需要每個資源都有唯一的 `@id` 或 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="e2ea5-143">用戶端會決定要使用哪一種資源。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="e2ea5-144">其中一個可能的執行，就是 `@type` 當連接失敗或伺服器錯誤時，可以使用迴圈配置資源的方式來使用相同或相容的資源。</span><span class="sxs-lookup"><span data-stu-id="e2ea5-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e2ea5-145">範例要求</span><span class="sxs-lookup"><span data-stu-id="e2ea5-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="e2ea5-146">範例回應</span><span class="sxs-lookup"><span data-stu-id="e2ea5-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
