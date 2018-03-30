---
title: 查詢發佈至 nuget.org 的所有套件 | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: 使用 NuGet API 可以查詢發佈到 nuget.org 的所有套件，並隨時保持最新狀態。
keywords: NuGet API 列舉所有套件, NuGet API 複寫套件, 發佈至 nuget.org 的最新套件
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5ea11e1b4edd87b6d30d3838986ca60aaa77870f
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="3806c-104">查詢發佈至 nuget.org 的所有套件</span><span class="sxs-lookup"><span data-stu-id="3806c-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="3806c-105">舊版 OData V2 API 有一個常見查詢模式，會列舉發佈至 nuget.org 的所有套件，並依套件發佈時間排序。</span><span class="sxs-lookup"><span data-stu-id="3806c-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="3806c-106">需要對 nuget.org 進行這種查詢的案例差異非常大：</span><span class="sxs-lookup"><span data-stu-id="3806c-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="3806c-107">完全複寫 nuget.org</span><span class="sxs-lookup"><span data-stu-id="3806c-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="3806c-108">當套件發行新版本時偵測</span><span class="sxs-lookup"><span data-stu-id="3806c-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="3806c-109">尋找依存於您套件的套件</span><span class="sxs-lookup"><span data-stu-id="3806c-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="3806c-110">執行此作業的傳統方式，通常取決於依時間戳記排序 OData 套件實體，以及使用 `skip` 和 `top` (頁面大小) 參數分頁龐大的結果集。</span><span class="sxs-lookup"><span data-stu-id="3806c-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="3806c-111">不幸的是，這個方法有一些缺點：</span><span class="sxs-lookup"><span data-stu-id="3806c-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="3806c-112">可能會遺失套件，因為正在查詢經常變更順序的資料</span><span class="sxs-lookup"><span data-stu-id="3806c-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="3806c-113">降低查詢回應時間，因為查詢未最佳化 (最佳化程度最高的查詢，是支援官方 NuGet 用戶端主線情節的查詢)</span><span class="sxs-lookup"><span data-stu-id="3806c-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="3806c-114">使用已取代且未記錄的 API，表示未來不保證對這類查詢的支援</span><span class="sxs-lookup"><span data-stu-id="3806c-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="3806c-115">無法以完全一致的公佈順序重新執行記錄</span><span class="sxs-lookup"><span data-stu-id="3806c-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="3806c-116">因此，您可遵循下列指南，以更可靠且未來有保證的方式處理上述案例。</span><span class="sxs-lookup"><span data-stu-id="3806c-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="3806c-117">總覽</span><span class="sxs-lookup"><span data-stu-id="3806c-117">Overview</span></span>

<span data-ttu-id="3806c-118">本指南的中心是 [NuGet API](../../api/overview.md) 的資源，稱之為**目錄**。</span><span class="sxs-lookup"><span data-stu-id="3806c-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="3806c-119">目錄是僅附加的 API，可讓呼叫端查看 nuget.org 新增、修改及刪除套件的完整記錄。如果您對發佈至 nuget.org 的所有套件或甚至套件子集有興趣，目錄會是隨時將目前可用套件集保持在最新狀態的絕佳方式。</span><span class="sxs-lookup"><span data-stu-id="3806c-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="3806c-120">本指南旨在成為總體的逐步解說，但如果您對目錄的細部詳細資料有興趣，請參閱其 [API 參考文件](../../api/catalog-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="3806c-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="3806c-121">您選擇的任何程式語言皆可實作下列步驟。</span><span class="sxs-lookup"><span data-stu-id="3806c-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="3806c-122">如果您想要完整的執行範例，請參閱下文的 [C# 範例](#c-sample-code)。</span><span class="sxs-lookup"><span data-stu-id="3806c-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="3806c-123">否則，請遵循下文的指南來建置可靠的目錄讀取器。</span><span class="sxs-lookup"><span data-stu-id="3806c-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="3806c-124">初始化資料指標</span><span class="sxs-lookup"><span data-stu-id="3806c-124">Initialize a cursor</span></span>

<span data-ttu-id="3806c-125">建置可靠之目錄讀取器的第一個步驟是實作資料指標。</span><span class="sxs-lookup"><span data-stu-id="3806c-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="3806c-126">如需目錄資料指標設計的完整詳細資料，請參閱[目錄參考文件](../../api/catalog-resource.md#cursor)。</span><span class="sxs-lookup"><span data-stu-id="3806c-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="3806c-127">簡而言之，資料指標是您在目錄中處理完事件的時間點。</span><span class="sxs-lookup"><span data-stu-id="3806c-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="3806c-128">目錄中的事件代表套件發行和其他套件變更。</span><span class="sxs-lookup"><span data-stu-id="3806c-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="3806c-129">如果您在意所有曾發佈至 NuGet 的套件 (自有記錄以來)，您可以將資料指標初始化為「最小值」的時間戳記 (例如 .NET 中的 `DateTime.MinValue`)。</span><span class="sxs-lookup"><span data-stu-id="3806c-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="3806c-130">如果您只在意從現在開始發行的套件，您可以使用目前的時間戳記作為初始資料指標值。</span><span class="sxs-lookup"><span data-stu-id="3806c-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="3806c-131">在本指南中，我們會將資料指標初始化為一小時前的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="3806c-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="3806c-132">目前只要將該時間戳記儲存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="3806c-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="3806c-133">決定目錄索引 URL</span><span class="sxs-lookup"><span data-stu-id="3806c-133">Determine catalog index URL</span></span>

<span data-ttu-id="3806c-134">使用[服務索引](../../api/service-index.md)應該會探索到 NuGet API 中的每個資源 (端點) 位置。</span><span class="sxs-lookup"><span data-stu-id="3806c-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="3806c-135">因為本指南著重於 nuget.org，所以我們會使用 nuget.org 的服務索引。</span><span class="sxs-lookup"><span data-stu-id="3806c-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="3806c-136">服務文件是包含所有 nuget.org 資源的 JSON 文件。尋找 `@type` 屬性值為 `Catalog/3.0.0` 的資源。</span><span class="sxs-lookup"><span data-stu-id="3806c-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="3806c-137">相關聯的 `@id` 屬性值是目錄索引本身的 URL。</span><span class="sxs-lookup"><span data-stu-id="3806c-137">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="3806c-138">尋找新的目錄分葉</span><span class="sxs-lookup"><span data-stu-id="3806c-138">Find new catalog leaves</span></span>

<span data-ttu-id="3806c-139">使用上一個步驟找到的 `@id` 屬性值，下載目錄索引：</span><span class="sxs-lookup"><span data-stu-id="3806c-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="3806c-140">還原序列化[目錄索引](../../api/catalog-resource.md#catalog-index)。</span><span class="sxs-lookup"><span data-stu-id="3806c-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="3806c-141">篩選掉 `commitTimeStamp` 小於或等於目前資料指標值的所有[目錄頁面物件](../../api/catalog-resource.md#catalog-page-object-in-the-index)。</span><span class="sxs-lookup"><span data-stu-id="3806c-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="3806c-142">使用 `@id` 屬性為每個剩餘的目錄頁面下載完整的文件。</span><span class="sxs-lookup"><span data-stu-id="3806c-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="3806c-143">還原序列化[目錄頁面](../../api/catalog-resource.md#catalog-page)。</span><span class="sxs-lookup"><span data-stu-id="3806c-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="3806c-144">篩選掉 `commitTimeStamp` 小於或等於目前資料指標值的所有[目錄分葉物件](../../api/catalog-resource.md#catalog-item-object-in-a-page)。</span><span class="sxs-lookup"><span data-stu-id="3806c-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="3806c-145">下載所有未篩選掉的目錄頁面後，您會有一組目錄分葉物件，代表從資料指標時間戳記到現在這段時間中，已發佈、未列出、已列出或已刪除的套件。</span><span class="sxs-lookup"><span data-stu-id="3806c-145">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="3806c-146">處理新的目錄分葉</span><span class="sxs-lookup"><span data-stu-id="3806c-146">Process catalog leaves</span></span>

<span data-ttu-id="3806c-147">此時，您可以對目錄項目執行任何您想要的自訂處理。</span><span class="sxs-lookup"><span data-stu-id="3806c-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="3806c-148">如果只需要套件的識別碼和版本，您可以檢查頁面中找到的目錄項目物件的 `nuget:id` 和 `nuget:version` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3806c-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="3806c-149">請務必查看 `@type` 屬性，了解目錄項目與現有的套件還是已刪除的套件有關。</span><span class="sxs-lookup"><span data-stu-id="3806c-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="3806c-150">如果對套件的中繼資料有興趣 (例如描述、相依性、.nupkg 大小等等)，您可以使用 `@id` 屬性擷取[目錄分葉文件](../../api/catalog-resource.md#catalog-leaf)。</span><span class="sxs-lookup"><span data-stu-id="3806c-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="3806c-151">本文件有[套件中繼資料資源](../../api/registration-base-url-resource.md)中包含的全部中繼資料及其他資訊！</span><span class="sxs-lookup"><span data-stu-id="3806c-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="3806c-152">這個步驟要實作您的自訂邏輯。</span><span class="sxs-lookup"><span data-stu-id="3806c-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="3806c-153">無論您要使用目錄分葉執行何種作業，本指南中其他步驟的實作方法都差不多。</span><span class="sxs-lookup"><span data-stu-id="3806c-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="3806c-154">下載 .nupkg</span><span class="sxs-lookup"><span data-stu-id="3806c-154">Downloading the .nupkg</span></span>

<span data-ttu-id="3806c-155">如果想要下載目錄中找到的套件 .nupkg，您可以使用[套件內容資源](../../api/package-base-address-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="3806c-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="3806c-156">但請注意，發現目錄中有套件的時間和套件內容資源提供該套件的時間之間有短暫的延遲。</span><span class="sxs-lookup"><span data-stu-id="3806c-156">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="3806c-157">因此，如果在嘗試下載於目錄中找到的套件 .nupkg 時，發生 `404 Not Found` 問題，只要稍後再試即可。</span><span class="sxs-lookup"><span data-stu-id="3806c-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="3806c-158">GitHub 問題 [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) 會追蹤修正此延遲。</span><span class="sxs-lookup"><span data-stu-id="3806c-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="3806c-159">將資料指標向前移</span><span class="sxs-lookup"><span data-stu-id="3806c-159">Move the cursor forward</span></span>

<span data-ttu-id="3806c-160">一旦成功處理目錄項目，即需要決定要儲存的新資料指標值。</span><span class="sxs-lookup"><span data-stu-id="3806c-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="3806c-161">若要這樣做，請找出已處理之所有目錄項目的 `commitTimeStamp` 最大值 (最新的時間先後順序)。</span><span class="sxs-lookup"><span data-stu-id="3806c-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="3806c-162">這就是您的新資料指標值。</span><span class="sxs-lookup"><span data-stu-id="3806c-162">This is your new cursor value.</span></span> <span data-ttu-id="3806c-163">請將它儲存在持續性存放區，例如資料庫、檔案系統或 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="3806c-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="3806c-164">當您想要取得更多目錄項目時，只要初始化這個持續性存放區的資料指標值，從[第一步](#initialize-a-cursor)開始即可。</span><span class="sxs-lookup"><span data-stu-id="3806c-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="3806c-165">如果您的應用程式擲回例外狀況或錯誤，請不要將資料指標向前移。</span><span class="sxs-lookup"><span data-stu-id="3806c-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="3806c-166">將資料指標向前移，表示您再也不需要處理資料指標前的目錄項目。</span><span class="sxs-lookup"><span data-stu-id="3806c-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="3806c-167">如果基於某些原因，在處理目錄分葉時發生 Bug，只要將資料指標的時間向後退，讓程式碼重新處理舊的目錄項目即可。</span><span class="sxs-lookup"><span data-stu-id="3806c-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="3806c-168">C# 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="3806c-168">C# sample code</span></span>

<span data-ttu-id="3806c-169">因為目錄是可透過 HTTP 使用的 JSON 文件集，所以它可與使用任何程式設計語言的 HTTP 用戶端和 JSON 還原序列化程式互動。</span><span class="sxs-lookup"><span data-stu-id="3806c-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="3806c-170">C# 範例位於 [NuGet/範例存放庫](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)。</span><span class="sxs-lookup"><span data-stu-id="3806c-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="3806c-171">目錄 SDK</span><span class="sxs-lookup"><span data-stu-id="3806c-171">Catalog SDK</span></span>

<span data-ttu-id="3806c-172">取用目錄最簡單的方法，是使用發行前版本的 .NET 目錄 SDK 套件：[NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog)。</span><span class="sxs-lookup"><span data-stu-id="3806c-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="3806c-173">此套件位於 `nuget-build` MyGet 摘要，針對它使用 NuGet 套件來源 URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="3806c-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="3806c-174">您可以將這個套件安裝到與 `netstandard1.3` 或更高版本相容的專案 (例如.NET Framework 4.6)。</span><span class="sxs-lookup"><span data-stu-id="3806c-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="3806c-175">使用此套件的範例位於 GitHub 的 [NuGet.Protocol.Catalog.Sample 專案](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)。</span><span class="sxs-lookup"><span data-stu-id="3806c-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="3806c-176">範例輸出</span><span class="sxs-lookup"><span data-stu-id="3806c-176">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="3806c-177">最小的範例</span><span class="sxs-lookup"><span data-stu-id="3806c-177">Minimal sample</span></span>

<span data-ttu-id="3806c-178">如需較少的相依性，示範與目錄更詳細互動的範例，請參閱 [CatalogReaderExample 範例專案](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)。</span><span class="sxs-lookup"><span data-stu-id="3806c-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="3806c-179">專案以 `netcoreapp2.0` 為目標，並依存於 [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (適用於解析服務索引) 和 [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (適用於 JSON 還原序列化)。</span><span class="sxs-lookup"><span data-stu-id="3806c-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="3806c-180">程式碼的主要邏輯會顯示在 [Program.cs 檔案](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs) 中。</span><span class="sxs-lookup"><span data-stu-id="3806c-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="3806c-181">範例輸出</span><span class="sxs-lookup"><span data-stu-id="3806c-181">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
