---
title: 檢舉不當使用 URL 範本，NuGet API
description: 「報告濫用 URL」範本可讓用戶端在其 UI 中顯示「報告不當使用」連結。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775222"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="94415-103">報告濫用 URL 範本</span><span class="sxs-lookup"><span data-stu-id="94415-103">Report abuse URL template</span></span>

<span data-ttu-id="94415-104">用戶端可以建立一個 URL，讓使用者用來回報有關特定套件的濫用。</span><span class="sxs-lookup"><span data-stu-id="94415-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="94415-105">當套件來源想要啟用所有用戶端體驗 (甚至是協力廠商) 將濫用報表委派給套件來源時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="94415-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="94415-106">用來建立此 URL 的資源是在 `ReportAbuseUriTemplate` [服務索引](service-index.md)中找到的資源。</span><span class="sxs-lookup"><span data-stu-id="94415-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="94415-107">版本控制</span><span class="sxs-lookup"><span data-stu-id="94415-107">Versioning</span></span>

<span data-ttu-id="94415-108">使用的 `@type` 值如下：</span><span class="sxs-lookup"><span data-stu-id="94415-108">The following `@type` values are used:</span></span>

<span data-ttu-id="94415-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="94415-109">@type value</span></span>                       | <span data-ttu-id="94415-110">備註</span><span class="sxs-lookup"><span data-stu-id="94415-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="94415-111">ReportAbuseUriTemplate/3.0.0-Beta</span><span class="sxs-lookup"><span data-stu-id="94415-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="94415-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="94415-112">The initial release</span></span>
<span data-ttu-id="94415-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="94415-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="94415-114">別名 `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="94415-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="94415-115">URL template</span><span class="sxs-lookup"><span data-stu-id="94415-115">URL template</span></span>

<span data-ttu-id="94415-116">下列 API 的 URL 是 `@id` 與上述其中一個資源值相關聯之屬性的值 `@type` 。</span><span class="sxs-lookup"><span data-stu-id="94415-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="94415-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="94415-117">HTTP methods</span></span>

<span data-ttu-id="94415-118">雖然用戶端不會代表使用者對報告濫用 URL 提出要求，但網頁應該支援 `GET` 方法，以允許在網頁瀏覽器中輕鬆地開啟已按一下的 url。</span><span class="sxs-lookup"><span data-stu-id="94415-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="94415-119">建立 URL</span><span class="sxs-lookup"><span data-stu-id="94415-119">Construct the URL</span></span>

<span data-ttu-id="94415-120">假設有已知的封裝識別碼和版本，則用戶端執行可以建立用來存取 web 介面的 URL。</span><span class="sxs-lookup"><span data-stu-id="94415-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="94415-121">用戶端的執行應該會顯示此已建立的 URL (或可按的連結) 給使用者，讓他們能夠將網頁瀏覽器開啟至 URL，並進行任何必要的濫用報告。</span><span class="sxs-lookup"><span data-stu-id="94415-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="94415-122">「濫用報表」表單的執行是由伺服器執行所決定。</span><span class="sxs-lookup"><span data-stu-id="94415-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="94415-123">的值 `@id` 是包含下列任何預留位置標記的 URL 字串：</span><span class="sxs-lookup"><span data-stu-id="94415-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="94415-124">URL 預留位置</span><span class="sxs-lookup"><span data-stu-id="94415-124">URL placeholders</span></span>

<span data-ttu-id="94415-125">名稱</span><span class="sxs-lookup"><span data-stu-id="94415-125">Name</span></span>        | <span data-ttu-id="94415-126">類型</span><span class="sxs-lookup"><span data-stu-id="94415-126">Type</span></span>    | <span data-ttu-id="94415-127">必要</span><span class="sxs-lookup"><span data-stu-id="94415-127">Required</span></span> | <span data-ttu-id="94415-128">備註</span><span class="sxs-lookup"><span data-stu-id="94415-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="94415-129">字串</span><span class="sxs-lookup"><span data-stu-id="94415-129">string</span></span>  | <span data-ttu-id="94415-130">不可以</span><span class="sxs-lookup"><span data-stu-id="94415-130">no</span></span>       | <span data-ttu-id="94415-131">要報告濫用的套件識別碼</span><span class="sxs-lookup"><span data-stu-id="94415-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="94415-132">字串</span><span class="sxs-lookup"><span data-stu-id="94415-132">string</span></span>  | <span data-ttu-id="94415-133">不可以</span><span class="sxs-lookup"><span data-stu-id="94415-133">no</span></span>       | <span data-ttu-id="94415-134">要報告濫用的套件版本</span><span class="sxs-lookup"><span data-stu-id="94415-134">The package version to report abuse for</span></span>

<span data-ttu-id="94415-135">`{id}` `{version}` 伺服器執行所解讀的和值必須區分大小寫，且不區分版本是否正規化。</span><span class="sxs-lookup"><span data-stu-id="94415-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="94415-136">例如，nuget 的報告濫用範本看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="94415-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="94415-137">如果用戶端執行需要顯示 NuGet 的報告濫用表單連結，則會產生下列 URL 並將其提供給使用者：</span><span class="sxs-lookup"><span data-stu-id="94415-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
