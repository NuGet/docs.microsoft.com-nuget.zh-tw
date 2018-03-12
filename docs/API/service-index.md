---
title: "服務索引，NuGet API |Microsoft 文件"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "服務索引是 NuGet HTTP 應用程式開發介面的進入點，並列舉伺服器的功能。"
keywords: "NuGet 的 API 進入點，NuGetA PI 端點探索"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="57c68-104">服務索引</span><span class="sxs-lookup"><span data-stu-id="57c68-104">Service index</span></span>

<span data-ttu-id="57c68-105">服務索引是 JSON 文件是 NuGet 套件來源的進入點，可讓用戶端實作探索套件來源的功能。</span><span class="sxs-lookup"><span data-stu-id="57c68-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="57c68-106">服務索引會使用兩個必要屬性的 JSON 物件： `version` （服務索引的結構描述版本） 和`resources`（端點或套件來源的功能）。</span><span class="sxs-lookup"><span data-stu-id="57c68-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="57c68-107">nuget.org 的服務索引位於`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="57c68-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="57c68-108">版本控制</span><span class="sxs-lookup"><span data-stu-id="57c68-108">Versioning</span></span>

<span data-ttu-id="57c68-109">`version`值是 SemVer 2.0.0 可以剖析版本的字串表示服務索引的結構描述版本。</span><span class="sxs-lookup"><span data-stu-id="57c68-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="57c68-110">API 要求的版本字串的主要版本號碼`3`。</span><span class="sxs-lookup"><span data-stu-id="57c68-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="57c68-111">服務索引結構描述會進行非中斷變更，就會增加的版本字串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="57c68-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="57c68-112">服務索引中的每個資源的版本也是獨立於服務索引結構描述版本。</span><span class="sxs-lookup"><span data-stu-id="57c68-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="57c68-113">目前的結構描述版本是`3.0.0`。</span><span class="sxs-lookup"><span data-stu-id="57c68-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="57c68-114">`3.0.0`版本功能上相當於舊版`3.0.0-beta.1`版本，但應該是慣用的穩定，已定義的結構描述更清楚地通訊。</span><span class="sxs-lookup"><span data-stu-id="57c68-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="57c68-115">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="57c68-115">HTTP methods</span></span>

<span data-ttu-id="57c68-116">服務索引是使用 HTTP 方法存取`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="57c68-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="57c68-117">資源</span><span class="sxs-lookup"><span data-stu-id="57c68-117">Resources</span></span>

<span data-ttu-id="57c68-118">`resources`屬性包含此封裝來源所支援的資源陣列。</span><span class="sxs-lookup"><span data-stu-id="57c68-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="57c68-119">資源</span><span class="sxs-lookup"><span data-stu-id="57c68-119">Resource</span></span>

<span data-ttu-id="57c68-120">資源是中的物件`resources`陣列。</span><span class="sxs-lookup"><span data-stu-id="57c68-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="57c68-121">它代表套件來源已建立版本功能。</span><span class="sxs-lookup"><span data-stu-id="57c68-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="57c68-122">資源具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="57c68-122">A resource has the following properties:</span></span>

<span data-ttu-id="57c68-123">名稱</span><span class="sxs-lookup"><span data-stu-id="57c68-123">Name</span></span>          | <span data-ttu-id="57c68-124">類型</span><span class="sxs-lookup"><span data-stu-id="57c68-124">Type</span></span>   | <span data-ttu-id="57c68-125">必要</span><span class="sxs-lookup"><span data-stu-id="57c68-125">Required</span></span> | <span data-ttu-id="57c68-126">注意</span><span class="sxs-lookup"><span data-stu-id="57c68-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="57c68-127">字串</span><span class="sxs-lookup"><span data-stu-id="57c68-127">string</span></span> | <span data-ttu-id="57c68-128">是</span><span class="sxs-lookup"><span data-stu-id="57c68-128">yes</span></span>      | <span data-ttu-id="57c68-129">資源 URL</span><span class="sxs-lookup"><span data-stu-id="57c68-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="57c68-130">字串</span><span class="sxs-lookup"><span data-stu-id="57c68-130">string</span></span> | <span data-ttu-id="57c68-131">是</span><span class="sxs-lookup"><span data-stu-id="57c68-131">yes</span></span>      | <span data-ttu-id="57c68-132">字串常數，其代表資源類型</span><span class="sxs-lookup"><span data-stu-id="57c68-132">A string constant representing the resource type</span></span>
<span data-ttu-id="57c68-133">註解</span><span class="sxs-lookup"><span data-stu-id="57c68-133">comment</span></span>       | <span data-ttu-id="57c68-134">字串</span><span class="sxs-lookup"><span data-stu-id="57c68-134">string</span></span> | <span data-ttu-id="57c68-135">否</span><span class="sxs-lookup"><span data-stu-id="57c68-135">no</span></span>       | <span data-ttu-id="57c68-136">可讀取描述的資源</span><span class="sxs-lookup"><span data-stu-id="57c68-136">A human readable description of the resource</span></span>

<span data-ttu-id="57c68-137">`@id`是 URL，必須是絕對路徑，也必須是具有 HTTP 或 HTTPS 的結構描述。</span><span class="sxs-lookup"><span data-stu-id="57c68-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="57c68-138">`@type`用來識別與資源進行互動時所要使用的特定通訊協定。</span><span class="sxs-lookup"><span data-stu-id="57c68-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="57c68-139">資源的類型是不透明的字串，但通常具有格式：</span><span class="sxs-lookup"><span data-stu-id="57c68-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="57c68-140">用戶端預期硬`@type`他們了解及套件來源的服務索引中查閱值。</span><span class="sxs-lookup"><span data-stu-id="57c68-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="57c68-141">確切`@type`現今使用的值會列舉中列出的個別資源的參考文件上[API 概觀](overview.md#resources-and-schema)。</span><span class="sxs-lookup"><span data-stu-id="57c68-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="57c68-142">本文件中，為了不同資源的相關文件將基本上是依據`{RESOURCE_NAME}`服務索引相當於群組案例中找到。</span><span class="sxs-lookup"><span data-stu-id="57c68-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="57c68-143">沒有每個資源都有唯一的需求`@id`或`@type`。</span><span class="sxs-lookup"><span data-stu-id="57c68-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="57c68-144">這是由用戶端實作，以判斷哪個資源，而不用另一個。</span><span class="sxs-lookup"><span data-stu-id="57c68-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="57c68-145">一個可能的實作是相同或相容的資源`@type`可用以循環配置資源方式發生連線失敗或伺服器發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="57c68-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="57c68-146">範例要求</span><span class="sxs-lookup"><span data-stu-id="57c68-146">Sample request</span></span>

<span data-ttu-id="57c68-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="57c68-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="57c68-148">範例回應</span><span class="sxs-lookup"><span data-stu-id="57c68-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
