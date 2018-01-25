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
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="service-index"></a><span data-ttu-id="164cb-104">服務索引</span><span class="sxs-lookup"><span data-stu-id="164cb-104">Service index</span></span>

<span data-ttu-id="164cb-105">服務索引是 JSON 文件是 NuGet 套件來源的進入點，可讓用戶端實作探索套件來源的功能。</span><span class="sxs-lookup"><span data-stu-id="164cb-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="164cb-106">服務索引會使用兩個必要屬性的 JSON 物件： `version` （服務索引的結構描述版本） 和`resources`（端點或套件來源的功能）。</span><span class="sxs-lookup"><span data-stu-id="164cb-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="164cb-107">nuget.org 的服務索引位於`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="164cb-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="164cb-108">版本控制</span><span class="sxs-lookup"><span data-stu-id="164cb-108">Versioning</span></span>

<span data-ttu-id="164cb-109">`version`值是 SemVer 2.0.0 可以剖析版本的字串表示服務索引的結構描述版本。</span><span class="sxs-lookup"><span data-stu-id="164cb-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span>
<span data-ttu-id="164cb-110">API 要求的版本字串的主要版本號碼`3`。</span><span class="sxs-lookup"><span data-stu-id="164cb-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="164cb-111">服務索引結構描述會進行非中斷變更，就會增加的版本字串的次要版本。</span><span class="sxs-lookup"><span data-stu-id="164cb-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="164cb-112">服務索引中的每個資源的版本也是獨立於服務索引結構描述版本。</span><span class="sxs-lookup"><span data-stu-id="164cb-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="164cb-113">目前的結構描述版本是`3.0.0-beta.1`。</span><span class="sxs-lookup"><span data-stu-id="164cb-113">The current schema version is `3.0.0-beta.1`.</span></span>

## <a name="http-methods"></a><span data-ttu-id="164cb-114">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="164cb-114">HTTP methods</span></span>

<span data-ttu-id="164cb-115">服務索引是使用 HTTP 方法存取`GET`和`HEAD`。</span><span class="sxs-lookup"><span data-stu-id="164cb-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="164cb-116">資源</span><span class="sxs-lookup"><span data-stu-id="164cb-116">Resources</span></span>

<span data-ttu-id="164cb-117">`resources`屬性包含此封裝來源所支援的資源陣列。</span><span class="sxs-lookup"><span data-stu-id="164cb-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="164cb-118">資源</span><span class="sxs-lookup"><span data-stu-id="164cb-118">Resource</span></span>

<span data-ttu-id="164cb-119">資源是中的物件`resources`陣列。</span><span class="sxs-lookup"><span data-stu-id="164cb-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="164cb-120">它代表套件來源已建立版本功能。</span><span class="sxs-lookup"><span data-stu-id="164cb-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="164cb-121">資源具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="164cb-121">A resource has the following properties:</span></span>

<span data-ttu-id="164cb-122">名稱</span><span class="sxs-lookup"><span data-stu-id="164cb-122">Name</span></span>          | <span data-ttu-id="164cb-123">類型</span><span class="sxs-lookup"><span data-stu-id="164cb-123">Type</span></span>   | <span data-ttu-id="164cb-124">必要</span><span class="sxs-lookup"><span data-stu-id="164cb-124">Required</span></span> | <span data-ttu-id="164cb-125">注意</span><span class="sxs-lookup"><span data-stu-id="164cb-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="164cb-126">字串</span><span class="sxs-lookup"><span data-stu-id="164cb-126">string</span></span> | <span data-ttu-id="164cb-127">是</span><span class="sxs-lookup"><span data-stu-id="164cb-127">yes</span></span>      | <span data-ttu-id="164cb-128">資源 URL</span><span class="sxs-lookup"><span data-stu-id="164cb-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="164cb-129">字串</span><span class="sxs-lookup"><span data-stu-id="164cb-129">string</span></span> | <span data-ttu-id="164cb-130">是</span><span class="sxs-lookup"><span data-stu-id="164cb-130">yes</span></span>      | <span data-ttu-id="164cb-131">字串常數，其代表資源類型</span><span class="sxs-lookup"><span data-stu-id="164cb-131">A string constant representing the resource type</span></span>
<span data-ttu-id="164cb-132">註解</span><span class="sxs-lookup"><span data-stu-id="164cb-132">comment</span></span>       | <span data-ttu-id="164cb-133">字串</span><span class="sxs-lookup"><span data-stu-id="164cb-133">string</span></span> | <span data-ttu-id="164cb-134">否</span><span class="sxs-lookup"><span data-stu-id="164cb-134">no</span></span>       | <span data-ttu-id="164cb-135">可讀取描述的資源</span><span class="sxs-lookup"><span data-stu-id="164cb-135">A human readable description of the resource</span></span>

<span data-ttu-id="164cb-136">`@id`是 URL，必須是絕對路徑，也必須是具有 HTTP 或 HTTPS 的結構描述。</span><span class="sxs-lookup"><span data-stu-id="164cb-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="164cb-137">`@type`用來識別與資源進行互動時所要使用的特定通訊協定。</span><span class="sxs-lookup"><span data-stu-id="164cb-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="164cb-138">資源的類型是不透明的字串，但通常具有格式：</span><span class="sxs-lookup"><span data-stu-id="164cb-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="164cb-139">用戶端預期硬`@type`他們了解及套件來源的服務索引中查閱值。</span><span class="sxs-lookup"><span data-stu-id="164cb-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="164cb-140">確切`@type`現今使用的值會列舉中列出的個別資源的參考文件上[API 概觀](overview.md#resources-and-schema)。</span><span class="sxs-lookup"><span data-stu-id="164cb-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="164cb-141">本文件中，為了不同資源的相關文件將基本上是依據`{RESOURCE_NAME}`服務索引相當於群組案例中找到。</span><span class="sxs-lookup"><span data-stu-id="164cb-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="164cb-142">沒有每個資源都有唯一的需求`@id`或`@type`。</span><span class="sxs-lookup"><span data-stu-id="164cb-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="164cb-143">這是由用戶端實作，以判斷哪個資源，而不用另一個。</span><span class="sxs-lookup"><span data-stu-id="164cb-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="164cb-144">一個可能的實作是相同或相容的資源`@type`可用以循環配置資源方式發生連線失敗或伺服器發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="164cb-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="164cb-145">範例要求</span><span class="sxs-lookup"><span data-stu-id="164cb-145">Sample request</span></span>

<span data-ttu-id="164cb-146">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="164cb-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="164cb-147">範例回應</span><span class="sxs-lookup"><span data-stu-id="164cb-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
