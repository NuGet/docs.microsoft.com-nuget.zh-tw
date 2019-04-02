---
title: 封裝詳細資料 URL 範本，NuGet API
description: 封裝詳細資料 URL 範本可讓用戶端在其 web 連結至多個套件詳細資料的 UI 中顯示
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638069"
---
# <a name="package-details-url-template"></a><span data-ttu-id="2f0b5-103">封裝詳細資料 URL 範本</span><span class="sxs-lookup"><span data-stu-id="2f0b5-103">Package details URL template</span></span>

<span data-ttu-id="2f0b5-104">就可以建置可供使用者查看網頁瀏覽器中的多個套件詳細資料的 URL 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="2f0b5-105">當想要顯示的 NuGet 用戶端應用程式的顯示範圍內的封裝可能不適合的其他資訊的套件來源，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="2f0b5-106">用來建立此 URL 的資源`PackageDetailsUriTemplate`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2f0b5-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="2f0b5-107">Versioning</span></span>

<span data-ttu-id="2f0b5-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="2f0b5-108">The following `@type` values are used:</span></span>

<span data-ttu-id="2f0b5-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="2f0b5-109">@type value</span></span>                     | <span data-ttu-id="2f0b5-110">注意</span><span class="sxs-lookup"><span data-stu-id="2f0b5-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="2f0b5-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="2f0b5-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="2f0b5-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="2f0b5-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="2f0b5-113">URL 範本</span><span class="sxs-lookup"><span data-stu-id="2f0b5-113">URL template</span></span>

<span data-ttu-id="2f0b5-114">下列 API 的 URL 是 windows 7`@id`其中一個先前提及的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2f0b5-115">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2f0b5-115">HTTP methods</span></span>

<span data-ttu-id="2f0b5-116">雖然用戶端不是代表使用者對套件詳細資料 URL 的要求，應支援網頁`GET`方法，以允許輕鬆地在網頁瀏覽器中開啟已按下的 URL。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="2f0b5-117">建構的 URL</span><span class="sxs-lookup"><span data-stu-id="2f0b5-117">Construct the URL</span></span>

<span data-ttu-id="2f0b5-118">指定已知的套件識別碼和版本，用戶端實作可以建構 URL，用來存取 web 介面。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="2f0b5-119">用戶端實作應該顯示使用者讓他們開啟網頁瀏覽器的 url，並深入了解封裝這個建構的 URL （或可點選連結）。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="2f0b5-120">套件詳細資料頁面的內容取決於伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="2f0b5-121">此 URL 必須是絕對 URL，並配置 （通訊協定） 必須是 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="2f0b5-122">值`@id`服務中的索引為 URL 字串，包含任何下列預留位置語彙基元：</span><span class="sxs-lookup"><span data-stu-id="2f0b5-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="2f0b5-123">URL 預留位置</span><span class="sxs-lookup"><span data-stu-id="2f0b5-123">URL placeholders</span></span>

<span data-ttu-id="2f0b5-124">名稱</span><span class="sxs-lookup"><span data-stu-id="2f0b5-124">Name</span></span>        | <span data-ttu-id="2f0b5-125">類型</span><span class="sxs-lookup"><span data-stu-id="2f0b5-125">Type</span></span>    | <span data-ttu-id="2f0b5-126">必要</span><span class="sxs-lookup"><span data-stu-id="2f0b5-126">Required</span></span> | <span data-ttu-id="2f0b5-127">注意</span><span class="sxs-lookup"><span data-stu-id="2f0b5-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="2f0b5-128">字串</span><span class="sxs-lookup"><span data-stu-id="2f0b5-128">string</span></span>  | <span data-ttu-id="2f0b5-129">否</span><span class="sxs-lookup"><span data-stu-id="2f0b5-129">no</span></span>       | <span data-ttu-id="2f0b5-130">套件識別碼，以取得詳細資料</span><span class="sxs-lookup"><span data-stu-id="2f0b5-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="2f0b5-131">字串</span><span class="sxs-lookup"><span data-stu-id="2f0b5-131">string</span></span>  | <span data-ttu-id="2f0b5-132">否</span><span class="sxs-lookup"><span data-stu-id="2f0b5-132">no</span></span>       | <span data-ttu-id="2f0b5-133">套件版本，以取得詳細資料</span><span class="sxs-lookup"><span data-stu-id="2f0b5-133">The package version to get details for</span></span>

<span data-ttu-id="2f0b5-134">伺服器應該接受`{id}`和`{version}`任何大小寫的值。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="2f0b5-135">此外，伺服器不能區分版本是否[正規化](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="2f0b5-136">換句話說，伺服器應接受也接受非標準化的版本。</span><span class="sxs-lookup"><span data-stu-id="2f0b5-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="2f0b5-137">比方說，nuget.org 的套件詳細資料範本看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="2f0b5-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="2f0b5-138">如果用戶端實作需要的 NuGet.Versioning 4.3.0 套件詳細資料，它會產生下列 URL，並提供給使用者：</span><span class="sxs-lookup"><span data-stu-id="2f0b5-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
