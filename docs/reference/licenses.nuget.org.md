---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921555"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="234dd-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="234dd-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="234dd-103">基本原理</span><span class="sxs-lookup"><span data-stu-id="234dd-103">Rationale</span></span>

<span data-ttu-id="234dd-104">引進[授權運算式](nuspec.md#license)，需求出現有的可靠服務，會提供個別的授權識別碼、 例外狀況識別項或授權運算式的參考文字。</span><span class="sxs-lookup"><span data-stu-id="234dd-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="234dd-105">這項服務的額外需求是具有穩定的 URL 結構描述，也是不容易連結腐壞，以便我們可以提供較舊的用戶端的回溯相容性，安全地使用它。</span><span class="sxs-lookup"><span data-stu-id="234dd-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="234dd-106">Licenses.nuget.org 可滿足該角色。</span><span class="sxs-lookup"><span data-stu-id="234dd-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="234dd-107">Nuget.org 會使用它來提供授權文字參考的封裝，指定使用授權的運算式其授權。</span><span class="sxs-lookup"><span data-stu-id="234dd-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> `nuget pack` <span data-ttu-id="234dd-108">或與其他封裝[用戶端工具](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools)設定[ `licenseUrl` ](nuspec.md#licenseurl)項目指向提供回溯相容性不支援的舊版用戶端 licenses.nuget.org `license`項目。</span><span class="sxs-lookup"><span data-stu-id="234dd-108">or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="234dd-109">通訊協定</span><span class="sxs-lookup"><span data-stu-id="234dd-109">Protocol</span></span>

<span data-ttu-id="234dd-110">Licenses.nuget.org 要檢視其瀏覽器中的人員，提供電腦可讀取的回應。</span><span class="sxs-lookup"><span data-stu-id="234dd-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="234dd-111">必須使用 HTTPS 通訊協定，而要求應要以特定方式建構。</span><span class="sxs-lookup"><span data-stu-id="234dd-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="234dd-112">它只支援`GET`要求。</span><span class="sxs-lookup"><span data-stu-id="234dd-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="234dd-113">它接受授權運算式或授權的例外狀況識別碼做為輸入下面指定的方式。</span><span class="sxs-lookup"><span data-stu-id="234dd-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="234dd-114">請注意，，授權運算式的所有項目會區分大小寫，因此所有輸入 licenses.nuget.org 都是區分大小寫以及。</span><span class="sxs-lookup"><span data-stu-id="234dd-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="234dd-115">授權運算式</span><span class="sxs-lookup"><span data-stu-id="234dd-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="234dd-116">要求</span><span class="sxs-lookup"><span data-stu-id="234dd-116">Request</span></span>

<span data-ttu-id="234dd-117">（當運算式組成的單一授權，包括簡單的情況下） 的授權運算式一定要[URL 編碼](https://tools.ietf.org/html/rfc3986#section-2.1)，當成 licenses.nuget.org 的要求中的路徑。</span><span class="sxs-lookup"><span data-stu-id="234dd-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="234dd-118">授權運算式</span><span class="sxs-lookup"><span data-stu-id="234dd-118">License expression</span></span> | <span data-ttu-id="234dd-119">若要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="234dd-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="234dd-120">MIT</span><span class="sxs-lookup"><span data-stu-id="234dd-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="234dd-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="234dd-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="234dd-122">(LGPL 2.0-僅限使用 FLTK 例外狀況或 Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="234dd-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="234dd-123">服務僅支援授權識別碼和接受的 nuget.org 的授權例外狀況識別項。授權的所有運算式包含不支援的授權識別碼或授權的例外狀況識別碼或，不符合授權運算式語法都視為無效。</span><span class="sxs-lookup"><span data-stu-id="234dd-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="234dd-124">回應</span><span class="sxs-lookup"><span data-stu-id="234dd-124">Response</span></span>

<span data-ttu-id="234dd-125">Licenses.nuget.org 回應包含 HTTP 200 狀態碼和網頁上包含描述的授權運算式的有效授權運算式的要求：</span><span class="sxs-lookup"><span data-stu-id="234dd-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="234dd-126">如果提供授權運算式，包含 web 網頁會傳回包含該授權參考文字的單一授權識別碼</span><span class="sxs-lookup"><span data-stu-id="234dd-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="234dd-127">如果提供授權運算式是複合授權運算式，網頁會傳回包含授權運算式與個別的授權或授權的例外狀況參考的連結。</span><span class="sxs-lookup"><span data-stu-id="234dd-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="234dd-128">包含無效的授權運算式的任何要求會導致 HTTP 404 回應。</span><span class="sxs-lookup"><span data-stu-id="234dd-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="234dd-129">授權例外狀況</span><span class="sxs-lookup"><span data-stu-id="234dd-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="234dd-130">要求</span><span class="sxs-lookup"><span data-stu-id="234dd-130">Request</span></span>

<span data-ttu-id="234dd-131">授權例外狀況識別項必須是 URL 編碼，並當做 licenses.nuget.org 的要求中的路徑。只是單一授權的例外狀況識別項可以在單一要求中提供。</span><span class="sxs-lookup"><span data-stu-id="234dd-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="234dd-132">沒有額外的字元，除了授權例外狀況識別項可能存在於 URL 的路徑部分。</span><span class="sxs-lookup"><span data-stu-id="234dd-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="234dd-133">授權例外狀況識別項</span><span class="sxs-lookup"><span data-stu-id="234dd-133">License exception identifier</span></span> | <span data-ttu-id="234dd-134">若要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="234dd-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="234dd-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="234dd-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="234dd-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="234dd-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="234dd-137">回應</span><span class="sxs-lookup"><span data-stu-id="234dd-137">Response</span></span>

<span data-ttu-id="234dd-138">Licenses.nuget.org 會回應 HTTP 200 回應，包含指定的授權例外狀況的參考文字的網頁與已知的授權例外狀況識別項的要求。</span><span class="sxs-lookup"><span data-stu-id="234dd-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="234dd-139">任何包含不支援的授權例外狀況識別項的要求會導致 HTTP 404 回應。</span><span class="sxs-lookup"><span data-stu-id="234dd-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>