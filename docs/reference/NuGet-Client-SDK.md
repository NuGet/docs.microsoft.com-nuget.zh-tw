---
title: NuGet 用戶端 SDK
description: API 是不斷演變以及不尚未記載，但 Dave Glick 部落格上的範例可用。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911032"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="df602-103">NuGet 用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="df602-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="df602-104">不到與混淆[NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="df602-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="df602-105">*NuGet 用戶端 SDK*參考為主的.NET 程式庫的一組[NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands)， [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging)，和[NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="df602-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="df602-106">這些套件取代舊版[NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)程式庫。</span><span class="sxs-lookup"><span data-stu-id="df602-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="df602-107">我們正努力有穩定的介面區，我們很快就可以文件。</span><span class="sxs-lookup"><span data-stu-id="df602-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="df602-108">原始程式碼</span><span class="sxs-lookup"><span data-stu-id="df602-108">Source code</span></span>

<span data-ttu-id="df602-109">GitHub 上發行的原始碼專案中[NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client)。</span><span class="sxs-lookup"><span data-stu-id="df602-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="df602-110">協力廠商文件</span><span class="sxs-lookup"><span data-stu-id="df602-110">Third-party documentation</span></span>

<span data-ttu-id="df602-111">下列部落格系列由 Dave Glick，發行 2016年中，您可以找到範例和某些 API 的文件：</span><span class="sxs-lookup"><span data-stu-id="df602-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="df602-112">瀏覽 NuGet v3 程式庫，第 1 部分：簡介和概念</span><span class="sxs-lookup"><span data-stu-id="df602-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="df602-113">瀏覽 NuGet v3 程式庫，第 2 部分：搜尋套件</span><span class="sxs-lookup"><span data-stu-id="df602-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="df602-114">瀏覽 NuGet v3 程式庫，第 3 部分：安裝套件</span><span class="sxs-lookup"><span data-stu-id="df602-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="df602-115">這些部落格文章所撰寫後不久**3.4.3**發行用戶端 SDK 套件的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="df602-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="df602-116">較新版本的封裝可能與部落格文章中的資訊不相容。</span><span class="sxs-lookup"><span data-stu-id="df602-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="df602-117">Martin Björkström 未 Dave Glick 部落格系列的待處理的部落格文章，其中介紹他如何使用安裝 NuGet 套件的 NuGet 用戶端 SDK 不同的方法：</span><span class="sxs-lookup"><span data-stu-id="df602-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="df602-118">重新認識 NuGet v3 程式庫</span><span class="sxs-lookup"><span data-stu-id="df602-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
