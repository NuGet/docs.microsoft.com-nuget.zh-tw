---
title: "NuGet v3 用戶端和 NuGetGallery Api |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d1a393b7-51b1-4840-b1a8-fdd76455077d
description: "NuGet 和 NuGetGallery Api 發展且不尚未記載，但是 Dave Glick 部落格上的可用範例。"
keywords: "NuGet 的 API，NuGetGallery API NuGet v3 程式庫"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 43a2e569b64f5e9d6e93cc6c279faf91a6dda9ee
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="51c99-104">NuGet 用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="51c99-104">NuGet Client SDK</span></span>

<span data-ttu-id="51c99-105">不斷演變的 NuGet v3 用戶端和 NuGetGallery Api 和我們努力需要穩定的介面區，我們很快就可以文件。</span><span class="sxs-lookup"><span data-stu-id="51c99-105">The NuGet v3 Client and NuGetGallery APIs are constantly evolving and we are working on having a stable surface area that we can document soon.</span></span>

<span data-ttu-id="51c99-106">在此同時，您可以在下列部落格系列由 Dave Glick 找到範例和 API 的某些文件：</span><span class="sxs-lookup"><span data-stu-id="51c99-106">In the meantime, you can find examples and documentation for some of the API in the following blog series by Dave Glick:</span></span>

- [<span data-ttu-id="51c99-107">瀏覽 NuGet v3 程式庫，第 1 部分： 簡介和概念</span><span class="sxs-lookup"><span data-stu-id="51c99-107">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="51c99-108">瀏覽 NuGet v3 程式庫，第 2 部分： 搜尋的封裝</span><span class="sxs-lookup"><span data-stu-id="51c99-108">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="51c99-109">瀏覽 NuGet v3 程式庫，第 3 篇： 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="51c99-109">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="51c99-110">下列部落格文章所撰寫後，馬上**3.4.3** NuGet 用戶端 SDK 封裝已發行的版本。</span><span class="sxs-lookup"><span data-stu-id="51c99-110">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="51c99-111">較新版本的封裝可能不相容的部落格文章中的資訊。</span><span class="sxs-lookup"><span data-stu-id="51c99-111">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>
