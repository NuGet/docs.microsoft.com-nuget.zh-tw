---
title: 套件詳細資料 URL 範本，NuGet API
description: 套件詳細資料 URL 範本可讓用戶端在其 UI 中顯示更多套件詳細資料的 web 連結
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773948"
---
# <a name="package-details-url-template"></a><span data-ttu-id="512c7-103">套件詳細資料 URL 範本</span><span class="sxs-lookup"><span data-stu-id="512c7-103">Package details URL template</span></span>

<span data-ttu-id="512c7-104">用戶端可以建立一個 URL，讓使用者在網頁瀏覽器中查看更多套件詳細資料。</span><span class="sxs-lookup"><span data-stu-id="512c7-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="512c7-105">當套件來源想要顯示可能無法容納 NuGet 用戶端應用程式所顯示之內容約制內之套件的其他資訊時，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="512c7-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="512c7-106">用來建立此 URL 的資源是在 `PackageDetailsUriTemplate` [服務索引](service-index.md)中找到的資源。</span><span class="sxs-lookup"><span data-stu-id="512c7-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="512c7-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="512c7-107">Versioning</span></span>

<span data-ttu-id="512c7-108">使用的 `@type` 值如下：</span><span class="sxs-lookup"><span data-stu-id="512c7-108">The following `@type` values are used:</span></span>

<span data-ttu-id="512c7-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="512c7-109">@type value</span></span>                     | <span data-ttu-id="512c7-110">備註</span><span class="sxs-lookup"><span data-stu-id="512c7-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="512c7-111">PackageDetailsUriTemplate/5.1。0</span><span class="sxs-lookup"><span data-stu-id="512c7-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="512c7-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="512c7-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="512c7-113">URL template</span><span class="sxs-lookup"><span data-stu-id="512c7-113">URL template</span></span>

<span data-ttu-id="512c7-114">下列 API 的 URL 是 `@id` 與上述其中一個資源值相關聯之屬性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="512c7-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="512c7-115">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="512c7-115">HTTP methods</span></span>

<span data-ttu-id="512c7-116">雖然用戶端不會代表使用者對套件詳細資料 URL 提出要求，但網頁應該支援 `GET` 方法，以允許在網頁瀏覽器中輕鬆地開啟所選的 url。</span><span class="sxs-lookup"><span data-stu-id="512c7-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="512c7-117">建立 URL</span><span class="sxs-lookup"><span data-stu-id="512c7-117">Construct the URL</span></span>

<span data-ttu-id="512c7-118">假設有已知的封裝識別碼和版本，則用戶端執行可以建立用來存取 web 介面的 URL。</span><span class="sxs-lookup"><span data-stu-id="512c7-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="512c7-119">用戶端的執行應該會顯示這個已建立的 URL (或可點選連結) 給使用者，讓他們可以開啟網頁瀏覽器並前往 URL，以及深入瞭解套件。</span><span class="sxs-lookup"><span data-stu-id="512c7-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="512c7-120">封裝詳細資料頁面的內容是由伺服器執行所決定。</span><span class="sxs-lookup"><span data-stu-id="512c7-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="512c7-121">URL 必須是絕對 URL，且 (通訊協定) 的配置必須是 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="512c7-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="512c7-122">`@id`服務索引中的值為 URL 字串，其中包含下列任何預留位置標記：</span><span class="sxs-lookup"><span data-stu-id="512c7-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="512c7-123">URL 預留位置</span><span class="sxs-lookup"><span data-stu-id="512c7-123">URL placeholders</span></span>

<span data-ttu-id="512c7-124">名稱</span><span class="sxs-lookup"><span data-stu-id="512c7-124">Name</span></span>        | <span data-ttu-id="512c7-125">類型</span><span class="sxs-lookup"><span data-stu-id="512c7-125">Type</span></span>    | <span data-ttu-id="512c7-126">必要</span><span class="sxs-lookup"><span data-stu-id="512c7-126">Required</span></span> | <span data-ttu-id="512c7-127">備註</span><span class="sxs-lookup"><span data-stu-id="512c7-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="512c7-128">字串</span><span class="sxs-lookup"><span data-stu-id="512c7-128">string</span></span>  | <span data-ttu-id="512c7-129">不可以</span><span class="sxs-lookup"><span data-stu-id="512c7-129">no</span></span>       | <span data-ttu-id="512c7-130">要取得其詳細資料的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="512c7-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="512c7-131">字串</span><span class="sxs-lookup"><span data-stu-id="512c7-131">string</span></span>  | <span data-ttu-id="512c7-132">不可以</span><span class="sxs-lookup"><span data-stu-id="512c7-132">no</span></span>       | <span data-ttu-id="512c7-133">要取得其詳細資料的套件版本</span><span class="sxs-lookup"><span data-stu-id="512c7-133">The package version to get details for</span></span>

<span data-ttu-id="512c7-134">伺服器應該接受 `{id}` `{version}` 任何大小寫的值。</span><span class="sxs-lookup"><span data-stu-id="512c7-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="512c7-135">此外，伺服器應該不區分版本是否 [正規化](../concepts/package-versioning.md#normalized-version-numbers)。</span><span class="sxs-lookup"><span data-stu-id="512c7-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="512c7-136">換句話說，伺服器也應接受非正規化的版本。</span><span class="sxs-lookup"><span data-stu-id="512c7-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="512c7-137">例如，nuget 的套件詳細資料範本看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="512c7-137">For example, nuget.org's package details template looks like this:</span></span>

```http
https://www.nuget.org/packages/{id}/{version}
```

<span data-ttu-id="512c7-138">如果用戶端執行需要顯示 NuGet 的封裝詳細資料的連結，則會產生下列 URL 並將其提供給使用者：</span><span class="sxs-lookup"><span data-stu-id="512c7-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
