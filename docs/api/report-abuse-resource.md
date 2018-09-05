---
title: 報告不當使用 URL 範本，NuGet API
description: 報告不當使用 URL 範本可讓用戶端在其 UI 中顯示的報表內容粗俗的文章連結。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549335"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="d00eb-103">報告不當使用 URL 範本</span><span class="sxs-lookup"><span data-stu-id="d00eb-103">Report abuse URL template</span></span>

<span data-ttu-id="d00eb-104">就可以建置可供使用者特定封裝的相關檢舉不當使用 URL 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d00eb-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="d00eb-105">當想要啟用委派到套件來源的濫用報告所有的用戶端體驗 （甚至是第 3 個合作對象） 的套件來源，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="d00eb-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="d00eb-106">用來建立此 URL 的資源`ReportAbuseUriTemplate`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="d00eb-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d00eb-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="d00eb-107">Versioning</span></span>

<span data-ttu-id="d00eb-108">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="d00eb-108">The following `@type` values are used:</span></span>

<span data-ttu-id="d00eb-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="d00eb-109">@type value</span></span>                       | <span data-ttu-id="d00eb-110">注意</span><span class="sxs-lookup"><span data-stu-id="d00eb-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="d00eb-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d00eb-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="d00eb-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="d00eb-112">The initial release</span></span>
<span data-ttu-id="d00eb-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d00eb-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="d00eb-114">別名 `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="d00eb-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="d00eb-115">URL 範本</span><span class="sxs-lookup"><span data-stu-id="d00eb-115">URL template</span></span>

<span data-ttu-id="d00eb-116">下列 API 的 URL 是 windows 7`@id`其中一個先前提及的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="d00eb-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d00eb-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="d00eb-117">HTTP methods</span></span>

<span data-ttu-id="d00eb-118">雖然用戶端不是代表使用者對檢舉不當使用 URL 的要求，應支援網頁`GET`方法，以允許輕鬆地在網頁瀏覽器中開啟已按下的 URL。</span><span class="sxs-lookup"><span data-stu-id="d00eb-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="d00eb-119">建構的 URL</span><span class="sxs-lookup"><span data-stu-id="d00eb-119">Construct the URL</span></span>

<span data-ttu-id="d00eb-120">指定已知的套件識別碼和版本，用戶端實作可以建構 URL，用來存取 web 介面。</span><span class="sxs-lookup"><span data-stu-id="d00eb-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="d00eb-121">用戶端實作應該顯示此建構的 URL （或可點選連結） 給使用者，讓他們開啟網頁瀏覽器的 url，並進行任何必要的濫用報告。</span><span class="sxs-lookup"><span data-stu-id="d00eb-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="d00eb-122">不當使用的報表格式的實作取決於伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="d00eb-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="d00eb-123">值`@id`是 URL 的字串，包含任何下列預留位置語彙基元：</span><span class="sxs-lookup"><span data-stu-id="d00eb-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="d00eb-124">URL 預留位置</span><span class="sxs-lookup"><span data-stu-id="d00eb-124">URL placeholders</span></span>

<span data-ttu-id="d00eb-125">名稱</span><span class="sxs-lookup"><span data-stu-id="d00eb-125">Name</span></span>        | <span data-ttu-id="d00eb-126">類型</span><span class="sxs-lookup"><span data-stu-id="d00eb-126">Type</span></span>    | <span data-ttu-id="d00eb-127">必要</span><span class="sxs-lookup"><span data-stu-id="d00eb-127">Required</span></span> | <span data-ttu-id="d00eb-128">注意</span><span class="sxs-lookup"><span data-stu-id="d00eb-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="d00eb-129">字串</span><span class="sxs-lookup"><span data-stu-id="d00eb-129">string</span></span>  | <span data-ttu-id="d00eb-130">否</span><span class="sxs-lookup"><span data-stu-id="d00eb-130">no</span></span>       | <span data-ttu-id="d00eb-131">檢舉不當使用的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="d00eb-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="d00eb-132">字串</span><span class="sxs-lookup"><span data-stu-id="d00eb-132">string</span></span>  | <span data-ttu-id="d00eb-133">否</span><span class="sxs-lookup"><span data-stu-id="d00eb-133">no</span></span>       | <span data-ttu-id="d00eb-134">若要檢舉不當使用的套件版本</span><span class="sxs-lookup"><span data-stu-id="d00eb-134">The package version to report abuse for</span></span>

<span data-ttu-id="d00eb-135">`{id}`和`{version}`解譯伺服器實作的值必須是不區分大小寫，並不容易受到版本是否已標準化。</span><span class="sxs-lookup"><span data-stu-id="d00eb-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="d00eb-136">比方說，nuget.org 的報表內容粗俗的文章範本看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d00eb-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="d00eb-137">如果客戶端實現需要顯示NuGet.Versioning 4.3.0的報告濫用形式的鏈接，則會生成以下URL並將其提供給用戶：</span><span class="sxs-lookup"><span data-stu-id="d00eb-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
