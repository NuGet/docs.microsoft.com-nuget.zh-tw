---
title: "報告濫用的 URL 範本，NuGet API |Microsoft 文件"
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
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "報表濫用的 URL 範本可讓用戶端在其 UI 中顯示報表濫用連結。"
keywords: "NuGet 的 API 回報不當使用 NuGet API 檔案相容、 NuGet.org 報表 URL 範本"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="fd7e3-104">報表濫用的 URL 範本</span><span class="sxs-lookup"><span data-stu-id="fd7e3-104">Report Abuse URL Template</span></span>

<span data-ttu-id="fd7e3-105">您可讓用戶端建立可供使用者有關的特定套件回報濫用的 URL。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="fd7e3-106">封裝來源想要啟用所有用戶端經驗 （即使第 3 個合作對象） 委派濫用套件來源的報表時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="fd7e3-107">用於擷取套件內容的資源是`ReportAbuseUriTemplate`資源中找到[服務索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="fd7e3-108">版本控制</span><span class="sxs-lookup"><span data-stu-id="fd7e3-108">Versioning</span></span>

<span data-ttu-id="fd7e3-109">下列`@type`會使用值：</span><span class="sxs-lookup"><span data-stu-id="fd7e3-109">The following `@type` values are used:</span></span>

<span data-ttu-id="fd7e3-110">@type 值</span><span class="sxs-lookup"><span data-stu-id="fd7e3-110">@type value</span></span>                       | <span data-ttu-id="fd7e3-111">注意</span><span class="sxs-lookup"><span data-stu-id="fd7e3-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="fd7e3-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="fd7e3-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="fd7e3-113">初版</span><span class="sxs-lookup"><span data-stu-id="fd7e3-113">The initial release</span></span>
<span data-ttu-id="fd7e3-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="fd7e3-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="fd7e3-115">別名`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="fd7e3-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="fd7e3-116">URL 範本</span><span class="sxs-lookup"><span data-stu-id="fd7e3-116">URL template</span></span>

<span data-ttu-id="fd7e3-117">下列 api 的 URL 是值`@id`與其中一個先前提及的資源相關聯的屬性`@type`值。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fd7e3-118">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="fd7e3-118">HTTP methods</span></span>

<span data-ttu-id="fd7e3-119">雖然用戶端不代表使用者對報表濫用的 URL 的要求，應支援網頁`GET`方法，以允許使用按的 URL，輕鬆地在網頁瀏覽器中開啟。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="fd7e3-120">建構 URL</span><span class="sxs-lookup"><span data-stu-id="fd7e3-120">Construct the URL</span></span>

<span data-ttu-id="fd7e3-121">根據給定的已知的封裝識別碼和版本，用戶端實作可以建構用來存取 web 介面的 URL。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="fd7e3-122">用戶端實作應該給使用者讓他們，以便開啟網頁瀏覽器的 url，並進行任何必要的不當使用報表會顯示這個建構的 URL （或可點按的連結）。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="fd7e3-123">濫用報表表單的實作取決於伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="fd7e3-124">值`@id`為 URL 字串，包含任何下列預留位置語彙基元：</span><span class="sxs-lookup"><span data-stu-id="fd7e3-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="fd7e3-125">URL 預留位置</span><span class="sxs-lookup"><span data-stu-id="fd7e3-125">URL placeholders</span></span>

<span data-ttu-id="fd7e3-126">名稱</span><span class="sxs-lookup"><span data-stu-id="fd7e3-126">Name</span></span>        | <span data-ttu-id="fd7e3-127">類型</span><span class="sxs-lookup"><span data-stu-id="fd7e3-127">Type</span></span>    | <span data-ttu-id="fd7e3-128">必要</span><span class="sxs-lookup"><span data-stu-id="fd7e3-128">Required</span></span> | <span data-ttu-id="fd7e3-129">注意</span><span class="sxs-lookup"><span data-stu-id="fd7e3-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="fd7e3-130">字串</span><span class="sxs-lookup"><span data-stu-id="fd7e3-130">string</span></span>  | <span data-ttu-id="fd7e3-131">no</span><span class="sxs-lookup"><span data-stu-id="fd7e3-131">no</span></span>       | <span data-ttu-id="fd7e3-132">要為回報不當使用的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="fd7e3-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="fd7e3-133">字串</span><span class="sxs-lookup"><span data-stu-id="fd7e3-133">string</span></span>  | <span data-ttu-id="fd7e3-134">no</span><span class="sxs-lookup"><span data-stu-id="fd7e3-134">no</span></span>       | <span data-ttu-id="fd7e3-135">回報不當使用的封裝版本</span><span class="sxs-lookup"><span data-stu-id="fd7e3-135">The package version to report abuse for</span></span>

<span data-ttu-id="fd7e3-136">`{id}`和`{version}`伺服器實作的解譯的值必須是大小寫 usernames 並不容易版本是否會正規化。</span><span class="sxs-lookup"><span data-stu-id="fd7e3-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="fd7e3-137">例如，nuget.org 的報表濫用範本看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="fd7e3-137">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="fd7e3-138">如果用戶端實作需要的 NuGet.Versioning 4.3.0 蒩盓繨報表濫用表單時，它會產生下列 URL，並提供給使用者：</span><span class="sxs-lookup"><span data-stu-id="fd7e3-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```