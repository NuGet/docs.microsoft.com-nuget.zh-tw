---
title: NuGet 用戶端 SDK
description: API 不斷演進，尚未記載，但範例可在 Dave Glick 的 blog 中取得。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924610"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="cb285-103">NuGet 用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="cb285-103">NuGet Client SDK</span></span>

<span data-ttu-id="cb285-104">*Nuget 用戶端 SDK*是指以[nuget. 命令](https://www.nuget.org/packages/NuGet.Commands)、 [nuget、封裝](https://www.nuget.org/packages/NuGet.Packaging)和[NuGet. 通訊協定](https://www.nuget.org/packages/NuGet.Protocol)為中心的 nuget 套件群組。</span><span class="sxs-lookup"><span data-stu-id="cb285-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="cb285-105">這些套件會取代先前的[NuGet. 核心](https://www.nuget.org/packages/NuGet.Core/)程式庫。</span><span class="sxs-lookup"><span data-stu-id="cb285-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="cb285-106">如需 NuGet 伺服器通訊協定的相關檔，請參閱[Nuget 伺服器 API](~/api/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cb285-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="cb285-107">原始程式碼</span><span class="sxs-lookup"><span data-stu-id="cb285-107">Source code</span></span>

<span data-ttu-id="cb285-108">原始程式碼發佈于 GitHub 上的專案[NuGet/nuget. 用戶端](https://github.com/NuGet/NuGet.Client)。</span><span class="sxs-lookup"><span data-stu-id="cb285-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="cb285-109">協力廠商檔</span><span class="sxs-lookup"><span data-stu-id="cb285-109">Third-party documentation</span></span>

<span data-ttu-id="cb285-110">您可以在下列 blog 系列中找到一些 API 的範例和檔： Dave Glick，發佈的2016：</span><span class="sxs-lookup"><span data-stu-id="cb285-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="cb285-111">探索 NuGet v3 程式庫，第1部分：簡介和概念</span><span class="sxs-lookup"><span data-stu-id="cb285-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="cb285-112">探索 NuGet v3 程式庫，第2部分：搜尋封裝</span><span class="sxs-lookup"><span data-stu-id="cb285-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="cb285-113">探索 NuGet v3 程式庫，第3部分：安裝套件</span><span class="sxs-lookup"><span data-stu-id="cb285-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="cb285-114">這些 blog 文章是在 NuGet 用戶端 SDK 套件的**3.4.3**版本發行後不久撰寫。</span><span class="sxs-lookup"><span data-stu-id="cb285-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="cb285-115">較新版本的套件可能與 blog 文章中的資訊不相容。</span><span class="sxs-lookup"><span data-stu-id="cb285-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="cb285-116">聖馬丁 Björkström 在 Dave Glick 的 blog 系列文章中，介紹了使用 NuGet 用戶端 SDK 來安裝 NuGet 套件的不同方法：</span><span class="sxs-lookup"><span data-stu-id="cb285-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="cb285-117">重新訪 NuGet v3 程式庫</span><span class="sxs-lookup"><span data-stu-id="cb285-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
