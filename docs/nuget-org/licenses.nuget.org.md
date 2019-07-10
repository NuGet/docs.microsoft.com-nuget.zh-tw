---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427113"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="a8db4-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="a8db4-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="a8db4-103">基本原理</span><span class="sxs-lookup"><span data-stu-id="a8db4-103">Rationale</span></span>

<span data-ttu-id="a8db4-104">引進[授權運算式](../reference/nuspec.md#license)後，出現要有可靠服務的需求，該服務得提供個別授權識別碼的參考文字、例外狀況識別碼或授權運算式。</span><span class="sxs-lookup"><span data-stu-id="a8db4-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="a8db4-105">這項服務的另一項需求是要有穩定的 URL 結構描述，也就是連結不容易腐壞，以便我們可以安全地用它為較舊的用戶端提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="a8db4-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="a8db4-106">Licenses.nuget.org 可滿足該角色。</span><span class="sxs-lookup"><span data-stu-id="a8db4-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="a8db4-107">Nuget.org 使用它來為使用授權運算式指定授權的套件提供授權文字參考。</span><span class="sxs-lookup"><span data-stu-id="a8db4-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="a8db4-108">`nuget pack` 或使用其他[用戶端工具](../install-nuget-client-tools.md)來封裝會設定 [`licenseUrl`](../reference/nuspec.md#licenseurl) 元素以指向 licenses.nuget.org，為不支援 `license` 元素的舊版用戶端提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="a8db4-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="a8db4-109">通訊協定</span><span class="sxs-lookup"><span data-stu-id="a8db4-109">Protocol</span></span>

<span data-ttu-id="a8db4-110">Licenses.nuget.org 是為了讓人們在瀏覽器中檢視並不會提供任何電腦可讀取的回應。</span><span class="sxs-lookup"><span data-stu-id="a8db4-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="a8db4-111">必須使用 HTTPS 通訊協定，而要求應該要以特定方式建構。</span><span class="sxs-lookup"><span data-stu-id="a8db4-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="a8db4-112">它只支援 `GET` 要求。</span><span class="sxs-lookup"><span data-stu-id="a8db4-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="a8db4-113">它接受授權運算式或授權例外狀況識別碼，作為以下方式指定的輸入。</span><span class="sxs-lookup"><span data-stu-id="a8db4-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="a8db4-114">請注意，授權運算式的所有元素都會區分大小寫，因此對 licenses.nuget.org 的所有輸入也都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a8db4-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="a8db4-115">授權運算式</span><span class="sxs-lookup"><span data-stu-id="a8db4-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="a8db4-116">要求</span><span class="sxs-lookup"><span data-stu-id="a8db4-116">Request</span></span>

<span data-ttu-id="a8db4-117">授權運算式 (包括運算式由單一授權組成的簡單情況) 必須要 [URL 編碼](https://tools.ietf.org/html/rfc3986#section-2.1)，且用作 licenses.nuget.org 要求中的路徑。</span><span class="sxs-lookup"><span data-stu-id="a8db4-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="a8db4-118">授權運算式</span><span class="sxs-lookup"><span data-stu-id="a8db4-118">License expression</span></span> | <span data-ttu-id="a8db4-119">要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="a8db4-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="a8db4-120">MIT</span><span class="sxs-lookup"><span data-stu-id="a8db4-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="a8db4-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="a8db4-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="a8db4-122">(僅限 LGPL 2.0，FLTK 或 Apache-2.0+ 例外)</span><span class="sxs-lookup"><span data-stu-id="a8db4-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="a8db4-123">服務僅支援 nuget.org 接受的授權識別碼和授權例外狀況識別碼。包含不受支援授權識別碼或授權例外狀況識別碼的所有授權運算式，或是不符合授權運算式語法的所有授權運算式，都視為無效。</span><span class="sxs-lookup"><span data-stu-id="a8db4-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="a8db4-124">回應</span><span class="sxs-lookup"><span data-stu-id="a8db4-124">Response</span></span>

<span data-ttu-id="a8db4-125">Licenses.nuget.org 會回應包含有效授權運算式且具有 HTTP 200 狀態碼的要求，以及包含授權運算式描述的網頁：</span><span class="sxs-lookup"><span data-stu-id="a8db4-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="a8db4-126">如果提供的授權運算式包含單一授權識別碼，則會傳回包含該授權參考文字的網頁；</span><span class="sxs-lookup"><span data-stu-id="a8db4-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="a8db4-127">如果提供的授權運算式是複合授權運算式，則會傳回包含授權運算式以及個別授權或授權例外狀況參考連結的網頁。</span><span class="sxs-lookup"><span data-stu-id="a8db4-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="a8db4-128">包含無效授權運算式的任何要求會導致 HTTP 404 回應。</span><span class="sxs-lookup"><span data-stu-id="a8db4-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="a8db4-129">授權例外狀況</span><span class="sxs-lookup"><span data-stu-id="a8db4-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="a8db4-130">要求</span><span class="sxs-lookup"><span data-stu-id="a8db4-130">Request</span></span>

<span data-ttu-id="a8db4-131">授權例外狀況識別碼必須是 URL 編碼，並用作 licenses.nuget.org 要求中的路徑。只有單一授權例外狀況識別碼可以在單一要求中提供。</span><span class="sxs-lookup"><span data-stu-id="a8db4-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="a8db4-132">除了授權例外狀況識別碼以外沒有額外字元可以存在於 URL 的路徑部分中。</span><span class="sxs-lookup"><span data-stu-id="a8db4-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="a8db4-133">授權例外狀況識別碼</span><span class="sxs-lookup"><span data-stu-id="a8db4-133">License exception identifier</span></span> | <span data-ttu-id="a8db4-134">要使用的 URL</span><span class="sxs-lookup"><span data-stu-id="a8db4-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="a8db4-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="a8db4-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="a8db4-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="a8db4-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="a8db4-137">回應</span><span class="sxs-lookup"><span data-stu-id="a8db4-137">Response</span></span>

<span data-ttu-id="a8db4-138">Licenses.nuget.org 會回應具有已知授權例外狀況識別碼和 HTTP 200 回應的要求，以及指定授權例外狀況參考文字的網頁。</span><span class="sxs-lookup"><span data-stu-id="a8db4-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="a8db4-139">任何包含不支援授權例外狀況識別碼的要求會導致 HTTP 404 回應。</span><span class="sxs-lookup"><span data-stu-id="a8db4-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>