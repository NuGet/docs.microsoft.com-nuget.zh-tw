---
title: 套件詳細資料 URL 範本，NuGet API
description: '[套件詳細資料 URL] 範本可讓用戶端在其 UI 中顯示更多套件詳細資料的 web 連結'
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610949"
---
# <a name="package-details-url-template"></a><span data-ttu-id="f3bdd-103">套件詳細資料 URL 範本</span><span class="sxs-lookup"><span data-stu-id="f3bdd-103">Package details URL template</span></span>

<span data-ttu-id="f3bdd-104">用戶端可以建立 URL，讓使用者用來在網頁瀏覽器中查看更多套件詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="f3bdd-105">當套件來源想要顯示可能無法符合 NuGet 用戶端應用程式顯示之範圍內的套件的其他資訊時，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="f3bdd-106">用來建立此 URL 的資源是在[服務索引](service-index.md)中找到的 `PackageDetailsUriTemplate` 資源。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="f3bdd-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="f3bdd-107">Versioning</span></span>

<span data-ttu-id="f3bdd-108">會使用下列 `@type` 值：</span><span class="sxs-lookup"><span data-stu-id="f3bdd-108">The following `@type` values are used:</span></span>

<span data-ttu-id="f3bdd-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="f3bdd-109">@type value</span></span>                     | <span data-ttu-id="f3bdd-110">備註</span><span class="sxs-lookup"><span data-stu-id="f3bdd-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="f3bdd-111">PackageDetailsUriTemplate/5.1。0</span><span class="sxs-lookup"><span data-stu-id="f3bdd-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="f3bdd-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="f3bdd-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="f3bdd-113">URL 範本</span><span class="sxs-lookup"><span data-stu-id="f3bdd-113">URL template</span></span>

<span data-ttu-id="f3bdd-114">下列 API 的 URL 是與上述其中一個資源 `@type` 值相關聯 `@id` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f3bdd-115">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="f3bdd-115">HTTP methods</span></span>

<span data-ttu-id="f3bdd-116">雖然用戶端不會代表使用者對封裝詳細資料 URL 提出要求，但網頁應支援 `GET` 方法，以便在網頁瀏覽器中輕鬆地開啟已按一下的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="f3bdd-117">結構 URL</span><span class="sxs-lookup"><span data-stu-id="f3bdd-117">Construct the URL</span></span>

<span data-ttu-id="f3bdd-118">假設有已知的封裝識別碼和版本，則用戶端執行可以建立用來存取 web 介面的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="f3bdd-119">用戶端的執行應該會將此結構化的 URL （或可點按的連結）顯示給使用者，讓他們可以將網頁瀏覽器開啟至 URL，並深入瞭解封裝。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="f3bdd-120">封裝詳細資料頁面的內容是由伺服器的執行所決定。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="f3bdd-121">URL 必須是絕對 URL，而配置（通訊協定）必須是 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="f3bdd-122">服務索引中的 `@id` 值是 URL 字串，其中包含下列任何預留位置權杖：</span><span class="sxs-lookup"><span data-stu-id="f3bdd-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="f3bdd-123">URL 預留位置</span><span class="sxs-lookup"><span data-stu-id="f3bdd-123">URL placeholders</span></span>

<span data-ttu-id="f3bdd-124">[屬性]</span><span class="sxs-lookup"><span data-stu-id="f3bdd-124">Name</span></span>        | <span data-ttu-id="f3bdd-125">輸入</span><span class="sxs-lookup"><span data-stu-id="f3bdd-125">Type</span></span>    | <span data-ttu-id="f3bdd-126">必要項</span><span class="sxs-lookup"><span data-stu-id="f3bdd-126">Required</span></span> | <span data-ttu-id="f3bdd-127">備註</span><span class="sxs-lookup"><span data-stu-id="f3bdd-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="f3bdd-128">字串</span><span class="sxs-lookup"><span data-stu-id="f3bdd-128">string</span></span>  | <span data-ttu-id="f3bdd-129">否</span><span class="sxs-lookup"><span data-stu-id="f3bdd-129">no</span></span>       | <span data-ttu-id="f3bdd-130">要取得詳細資料的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="f3bdd-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="f3bdd-131">字串</span><span class="sxs-lookup"><span data-stu-id="f3bdd-131">string</span></span>  | <span data-ttu-id="f3bdd-132">否</span><span class="sxs-lookup"><span data-stu-id="f3bdd-132">no</span></span>       | <span data-ttu-id="f3bdd-133">要取得詳細資料的套件版本</span><span class="sxs-lookup"><span data-stu-id="f3bdd-133">The package version to get details for</span></span>

<span data-ttu-id="f3bdd-134">伺服器應該接受 `{id}`，並 `{version}` 任何大小寫的值。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="f3bdd-135">此外，伺服器應該不會區分版本是否[正規化](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="f3bdd-136">換句話說，伺服器也應該接受非正規化版本。</span><span class="sxs-lookup"><span data-stu-id="f3bdd-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="f3bdd-137">例如，nuget 的 [套件詳細資料] 範本如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3bdd-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="f3bdd-138">如果用戶端執行需要顯示 NuGet 的封裝詳細資料連結，則會產生下列 URL，並將其提供給使用者：</span><span class="sxs-lookup"><span data-stu-id="f3bdd-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
