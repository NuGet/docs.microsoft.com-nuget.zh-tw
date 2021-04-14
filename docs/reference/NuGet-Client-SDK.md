---
title: NuGet 用戶端 SDK
description: API 不斷演進且尚未記載，但範例可在 Dave Glick 的 blog 上取得。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387383"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="accfd-103">NuGet 用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="accfd-103">NuGet Client SDK</span></span>

<span data-ttu-id="accfd-104">*Nuget 用戶端 SDK* 指的是一組 nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="accfd-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="accfd-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用來與 HTTP 和以檔案為基礎的 NuGet 摘要互動</span><span class="sxs-lookup"><span data-stu-id="accfd-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="accfd-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用來與 NuGet 套件互動。</span><span class="sxs-lookup"><span data-stu-id="accfd-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="accfd-107">`NuGet.Protocol` 相依于此套件</span><span class="sxs-lookup"><span data-stu-id="accfd-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="accfd-108">您可以在 [NuGet/nuget. 用戶端](https://github.com/NuGet/NuGet.Client) GitHub 存放庫中找到這些套件的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="accfd-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="accfd-109">您可以在 GitHub 上的 [nuget.exe](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) 範例專案中找到這些範例的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="accfd-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="accfd-110">如需 NuGet 伺服器通訊協定的相關檔，請參閱 [Nuget 伺服器 API](~/api/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="accfd-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="accfd-111">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="accfd-111">NuGet.Protocol</span></span>

<span data-ttu-id="accfd-112">安裝 `NuGet.Protocol` 套件以與 HTTP 和以資料夾為基礎的 NuGet 套件摘要進行互動：</span><span class="sxs-lookup"><span data-stu-id="accfd-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="accfd-113">`Repository.Factory` 是在 `NuGet.Protocol.Core.Types` 命名空間中定義，而 `GetCoreV3` 方法是在命名空間中定義的擴充方法 `NuGet.Protocol` 。</span><span class="sxs-lookup"><span data-stu-id="accfd-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="accfd-114">因此，您將需要為 `using` 這兩個命名空間加入語句。</span><span class="sxs-lookup"><span data-stu-id="accfd-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="accfd-115">列出套件版本</span><span class="sxs-lookup"><span data-stu-id="accfd-115">List package versions</span></span>

<span data-ttu-id="accfd-116">使用 [NuGet V3 套件內容 API](../api/package-base-address-resource.md#enumerate-package-versions)尋找 Newtonsoft.Js的所有版本：</span><span class="sxs-lookup"><span data-stu-id="accfd-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="accfd-117">下載套件</span><span class="sxs-lookup"><span data-stu-id="accfd-117">Download a package</span></span>

<span data-ttu-id="accfd-118">使用 [NuGet V3 套件內容 API](../api/package-base-address-resource.md)下載 Newtonsoft.Json v 12.0.1：</span><span class="sxs-lookup"><span data-stu-id="accfd-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="accfd-119">取得套件中繼資料</span><span class="sxs-lookup"><span data-stu-id="accfd-119">Get package metadata</span></span>

<span data-ttu-id="accfd-120">使用 [NuGet V3 套件中繼資料 API](../api/registration-base-url-resource.md)來取得 "Newtonsoft.Json" 套件的中繼資料：</span><span class="sxs-lookup"><span data-stu-id="accfd-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="accfd-121">搜尋套件</span><span class="sxs-lookup"><span data-stu-id="accfd-121">Search packages</span></span>

<span data-ttu-id="accfd-122">使用 [NuGet V3 搜尋 API](../api/search-query-service-resource.md)來搜尋 "json" 套件：</span><span class="sxs-lookup"><span data-stu-id="accfd-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="accfd-123">推送套件</span><span class="sxs-lookup"><span data-stu-id="accfd-123">Push a package</span></span>

<span data-ttu-id="accfd-124">使用 [NuGet V3 推送和刪除 API](../api/package-publish-resource.md)來推送套件：</span><span class="sxs-lookup"><span data-stu-id="accfd-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="accfd-125">刪除套件</span><span class="sxs-lookup"><span data-stu-id="accfd-125">Delete a package</span></span>

<span data-ttu-id="accfd-126">使用 [NuGet V3 推送和刪除 API](../api/package-publish-resource.md)來刪除套件：</span><span class="sxs-lookup"><span data-stu-id="accfd-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="accfd-127">NuGet 伺服器可任意將套件刪除要求解讀為「實刪除」、「虛刪除」或「取消列出」。</span><span class="sxs-lookup"><span data-stu-id="accfd-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="accfd-128">例如，nuget.org 會將套件刪除要求解讀為 "取消列出"。</span><span class="sxs-lookup"><span data-stu-id="accfd-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="accfd-129">如需這種作法的詳細資訊，請參閱 [刪除封裝](../nuget-org/policies/deleting-packages.md) 原則。</span><span class="sxs-lookup"><span data-stu-id="accfd-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="accfd-130">使用已驗證的摘要</span><span class="sxs-lookup"><span data-stu-id="accfd-130">Work with authenticated feeds</span></span>

<span data-ttu-id="accfd-131">使用 [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) 來處理已驗證的摘要。</span><span class="sxs-lookup"><span data-stu-id="accfd-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="accfd-132">NuGet. 封裝</span><span class="sxs-lookup"><span data-stu-id="accfd-132">NuGet.Packaging</span></span>

<span data-ttu-id="accfd-133">安裝 `NuGet.Packaging` 套件以與資料流程互動 `.nupkg` 和檔案 `.nuspec` ：</span><span class="sxs-lookup"><span data-stu-id="accfd-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="accfd-134">建立套件</span><span class="sxs-lookup"><span data-stu-id="accfd-134">Create a package</span></span>

<span data-ttu-id="accfd-135">使用建立封裝、設定中繼資料，以及新增相依性 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。</span><span class="sxs-lookup"><span data-stu-id="accfd-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="accfd-136">強烈建議您使用官方 NuGet 工具來建立 NuGet 套件，而 **不要** 使用此低層級 API。</span><span class="sxs-lookup"><span data-stu-id="accfd-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="accfd-137">格式正確的封裝有許多重要的特性，而最新版本的工具可協助您併入這些最佳做法。</span><span class="sxs-lookup"><span data-stu-id="accfd-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="accfd-138">如需有關建立 NuGet 套件的詳細資訊，請參閱 [套件建立工作流程](../create-packages/overview-and-workflow.md) 的總覽，以及官方套件工具的檔 (例如， [使用 dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)) 。</span><span class="sxs-lookup"><span data-stu-id="accfd-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="accfd-139">讀取套件</span><span class="sxs-lookup"><span data-stu-id="accfd-139">Read a package</span></span>

<span data-ttu-id="accfd-140">使用從檔案資料流程讀取封裝 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。</span><span class="sxs-lookup"><span data-stu-id="accfd-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="accfd-141">協力廠商檔</span><span class="sxs-lookup"><span data-stu-id="accfd-141">Third-party documentation</span></span>

<span data-ttu-id="accfd-142">您可以在下列 Dave Glick 的 blog 系列中找到某些 API 的範例和檔，發佈2016：</span><span class="sxs-lookup"><span data-stu-id="accfd-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="accfd-143">探索 NuGet v3 程式庫，第1部分：簡介和概念</span><span class="sxs-lookup"><span data-stu-id="accfd-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="accfd-144">探索 NuGet v3 程式庫，第2部分：搜尋套件</span><span class="sxs-lookup"><span data-stu-id="accfd-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="accfd-145">探索 NuGet v3 程式庫，第3部分：安裝套件</span><span class="sxs-lookup"><span data-stu-id="accfd-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="accfd-146">這些 blog 文章是在 **3.4.3** 版本的 NuGet 用戶端 SDK 套件發行之後不久撰寫的。</span><span class="sxs-lookup"><span data-stu-id="accfd-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="accfd-147">較新版本的套件可能與 blog 文章中的資訊不相容。</span><span class="sxs-lookup"><span data-stu-id="accfd-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="accfd-148">Björkström 在 Dave Glick 的 blog 文章中，有一篇的 blog 文章，其中引進了使用 NuGet 用戶端 SDK 安裝 NuGet 套件的不同方法：</span><span class="sxs-lookup"><span data-stu-id="accfd-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="accfd-149">重新訪 NuGet v3 程式庫</span><span class="sxs-lookup"><span data-stu-id="accfd-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
