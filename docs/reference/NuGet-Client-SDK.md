---
title: NuGet 用戶端 SDK
description: API 不斷演進，尚未記載，但範例可在 Dave Glick 的 blog 中取得。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231236"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="1be3d-103">NuGet 用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="1be3d-103">NuGet Client SDK</span></span>

<span data-ttu-id="1be3d-104">*Nuget 用戶端 SDK*是指 nuget 套件的群組：</span><span class="sxs-lookup"><span data-stu-id="1be3d-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="1be3d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用來與 HTTP 和以檔案為基礎的 NuGet 摘要互動</span><span class="sxs-lookup"><span data-stu-id="1be3d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="1be3d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用來與 NuGet 套件互動。</span><span class="sxs-lookup"><span data-stu-id="1be3d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="1be3d-107">`NuGet.Protocol` 相依于此套件</span><span class="sxs-lookup"><span data-stu-id="1be3d-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="1be3d-108">您可以在[nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) GitHub 存放庫中找到這些套件的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="1be3d-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="1be3d-109">如需 NuGet 伺服器通訊協定的相關檔，請參閱[Nuget 伺服器 API](~/api/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1be3d-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="1be3d-110">開始使用</span><span class="sxs-lookup"><span data-stu-id="1be3d-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="1be3d-111">安裝套件</span><span class="sxs-lookup"><span data-stu-id="1be3d-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="1be3d-112">範例</span><span class="sxs-lookup"><span data-stu-id="1be3d-112">Examples</span></span>

<span data-ttu-id="1be3d-113">您可以在 GitHub 上的[範例](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples)專案中找到這些範例。</span><span class="sxs-lookup"><span data-stu-id="1be3d-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="1be3d-114">列出套件版本</span><span class="sxs-lookup"><span data-stu-id="1be3d-114">List package versions</span></span>

<span data-ttu-id="1be3d-115">使用[NuGet V3 套件內容 API](../api/package-base-address-resource.md#enumerate-package-versions)來尋找 Newtonsoft 的所有版本：</span><span class="sxs-lookup"><span data-stu-id="1be3d-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="1be3d-116">下載套件</span><span class="sxs-lookup"><span data-stu-id="1be3d-116">Download a package</span></span>

<span data-ttu-id="1be3d-117">使用[NuGet V3 套件內容 API](../api/package-base-address-resource.md)下載 Newtonsoft 12.0.1：</span><span class="sxs-lookup"><span data-stu-id="1be3d-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="1be3d-118">取得套件中繼資料</span><span class="sxs-lookup"><span data-stu-id="1be3d-118">Get package metadata</span></span>

<span data-ttu-id="1be3d-119">使用[NuGet V3 套件中繼資料 API](../api/registration-base-url-resource.md)取得 "Newtonsoft" 套件的中繼資料：</span><span class="sxs-lookup"><span data-stu-id="1be3d-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="1be3d-120">搜尋套件</span><span class="sxs-lookup"><span data-stu-id="1be3d-120">Search packages</span></span>

<span data-ttu-id="1be3d-121">使用[NuGet V3 搜尋 API](../api/search-query-service-resource.md)搜尋 "json" 套件：</span><span class="sxs-lookup"><span data-stu-id="1be3d-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="1be3d-122">協力廠商檔</span><span class="sxs-lookup"><span data-stu-id="1be3d-122">Third-party documentation</span></span>

<span data-ttu-id="1be3d-123">您可以在下列 blog 系列中找到一些 API 的範例和檔： Dave Glick，發佈的2016：</span><span class="sxs-lookup"><span data-stu-id="1be3d-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="1be3d-124">探索 NuGet v3 程式庫，第1部分：簡介和概念</span><span class="sxs-lookup"><span data-stu-id="1be3d-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="1be3d-125">探索 NuGet v3 程式庫，第2部分：搜尋封裝</span><span class="sxs-lookup"><span data-stu-id="1be3d-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="1be3d-126">探索 NuGet v3 程式庫，第3部分：安裝套件</span><span class="sxs-lookup"><span data-stu-id="1be3d-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="1be3d-127">這些 blog 文章是在 NuGet 用戶端 SDK 套件的**3.4.3**版本發行後不久撰寫。</span><span class="sxs-lookup"><span data-stu-id="1be3d-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="1be3d-128">較新版本的套件可能與 blog 文章中的資訊不相容。</span><span class="sxs-lookup"><span data-stu-id="1be3d-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="1be3d-129">聖馬丁 Björkström 在 Dave Glick 的 blog 系列文章中，介紹了使用 NuGet 用戶端 SDK 來安裝 NuGet 套件的不同方法：</span><span class="sxs-lookup"><span data-stu-id="1be3d-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="1be3d-130">重新訪 NuGet v3 程式庫</span><span class="sxs-lookup"><span data-stu-id="1be3d-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
