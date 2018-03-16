---
title: "查詢發佈至 nuget.org 的所有套件 | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "使用 NuGet API 可以查詢發佈到 nuget.org 的所有套件，並隨時保持最新狀態。"
keywords: "NuGet API 列舉所有套件, NuGet API 複寫套件, 發佈至 nuget.org 的最新套件"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ce25680f3b591e9c6b0234b6ac30b82205d10ad3
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>查詢發佈至 nuget.org 的所有套件

舊版 OData V2 API 有一個常見查詢模式，會列舉發佈至 nuget.org 的所有套件，並依套件發佈時間排序。 需要對 nuget.org 進行這種查詢的案例差異非常大：

- 完全複寫 nuget.org
- 當套件發行新版本時偵測
- 尋找依存於您套件的套件

執行此作業的傳統方式，通常取決於依時間戳記排序 OData 套件實體，以及使用 `skip` 和 `top` (頁面大小) 參數分頁龐大的結果集。 不幸的是，這個方法有一些缺點：

- 可能會遺失套件，因為正在查詢經常變更順序的資料
- 降低查詢回應時間，因為查詢未最佳化 (最佳化程度最高的查詢，是支援官方 NuGet 用戶端主線情節的查詢)
- 使用已取代且未記錄的 API，表示未來不保證對這類查詢的支援
- 無法以完全一致的公佈順序重新執行記錄

因此，您可遵循下列指南，以更可靠且未來有保證的方式處理上述案例。

## <a name="overview"></a>總覽

本指南的中心是 [NuGet API](../../api/overview.md) 的資源，稱之為**目錄**。 目錄是僅附加的 API，可讓呼叫端查看 nuget.org 新增、修改及刪除套件的完整記錄。如果您對發佈至 nuget.org 的所有套件或甚至套件子集有興趣，目錄會是隨時將目前可用套件集保持在最新狀態的絕佳方式。

本指南旨在成為總體的逐步解說，但如果您對目錄的細部詳細資料有興趣，請參閱其 [API 參考文件](../../api/catalog-resource.md)。

您選擇的任何程式語言皆可實作下列步驟。 如果您想要完整的執行範例，請參閱下文的 [C# 範例](#c-sample-code)。

否則，請遵循下文的指南來建置可靠的目錄讀取器。

## <a name="initialize-a-cursor"></a>初始化資料指標

建置可靠之目錄讀取器的第一個步驟是實作資料指標。 如需目錄資料指標設計的完整詳細資料，請參閱[目錄參考文件](../../api/catalog-resource.md#cursor)。 簡而言之，資料指標是您在目錄中處理完事件的時間點。 目錄中的事件代表套件發行和其他套件變更。 如果您在意所有曾發佈至 NuGet 的套件 (自有記錄以來)，您可以將資料指標初始化為「最小值」的時間戳記 (例如 .NET 中的 `DateTime.MinValue`)。 如果您只在意從現在開始發行的套件，您可以使用目前的時間戳記作為初始資料指標值。

在本指南中，我們會將資料指標初始化為一小時前的時間戳記。 目前只要將該時間戳記儲存在記憶體中。

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>決定目錄索引 URL

使用[服務索引](../../api/service-index.md)應該會探索到 NuGet API 中的每個資源 (端點) 位置。 因為本指南著重於 nuget.org，所以我們會使用 nuget.org 的服務索引。

    GET https://api.nuget.org/v3/index.json

服務文件是包含所有 nuget.org 資源的 JSON 文件。尋找 `@type` 屬性值為 `Catalog/3.0.0` 的資源。 相關聯的 `@id` 屬性值是目錄索引本身的 URL。 

## <a name="find-new-catalog-leaves"></a>尋找新的目錄分葉

使用上一個步驟找到的 `@id` 屬性值，下載目錄索引：

    GET https://api.nuget.org/v3/catalog0/index.json

還原序列化[目錄索引](../../api/catalog-resource.md#catalog-index)。 篩選掉 `commitTimeStamp` 小於或等於目前資料指標值的所有[目錄頁面物件](../../api/catalog-resource.md#catalog-page-object-in-the-index)。

使用 `@id` 屬性為每個剩餘的目錄頁面下載完整的文件。

    GET https://api.nuget.org/v3/catalog0/page2926.json

還原序列化[目錄頁面](../../api/catalog-resource.md#catalog-page)。 篩選掉 `commitTimeStamp` 小於或等於目前資料指標值的所有[目錄分葉物件](../../api/catalog-resource.md#catalog-item-object-in-a-page)。

下載所有未篩選掉的目錄頁面後，您會有一組目錄分葉物件，代表從資料指標時間戳記到現在這段時間中，已發佈、未列出、已列出或已刪除的套件。

## <a name="process-catalog-leaves"></a>處理新的目錄分葉

此時，您可以對目錄項目執行任何您想要的自訂處理。 如果只需要套件的識別碼和版本，您可以檢查頁面中找到的目錄項目物件的 `nuget:id` 和 `nuget:version` 屬性。 請務必查看 `@type` 屬性，了解目錄項目與現有的套件還是已刪除的套件有關。

如果對套件的中繼資料有興趣 (例如描述、相依性、.nupkg 大小等等)，您可以使用 `@id` 屬性擷取[目錄分葉文件](../../api/catalog-resource.md#catalog-leaf)。

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

本文件有[套件中繼資料資源](../../api/registration-base-url-resource.md)中包含的全部中繼資料及其他資訊！

這個步驟要實作您的自訂邏輯。 無論您要使用目錄分葉執行何種作業，本指南中其他步驟的實作方法都差不多。

### <a name="downloading-the-nupkg"></a>下載 .nupkg

如果想要下載目錄中找到的套件 .nupkg，您可以使用[套件內容資源](../../api/package-base-address-resource.md)。 但請注意，發現目錄中有套件的時間和套件內容資源提供該套件的時間之間有短暫的延遲。 因此，如果在嘗試下載於目錄中找到的套件 .nupkg 時，發生 `404 Not Found` 問題，只要稍後再試即可。 GitHub 問題 [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) 會追蹤修正此延遲。

## <a name="move-the-cursor-forward"></a>將資料指標向前移

一旦成功處理目錄項目，即需要決定要儲存的新資料指標值。 若要這樣做，請找出已處理之所有目錄項目的 `commitTimeStamp` 最大值 (最新的時間先後順序)。 這就是您的新資料指標值。 請將它儲存在持續性存放區，例如資料庫、檔案系統或 Blob 儲存體。 當您想要取得更多目錄項目時，只要初始化這個持續性存放區的資料指標值，從[第一步](#initialize-a-cursor)開始即可。

如果您的應用程式擲回例外狀況或錯誤，請不要將資料指標向前移。 將資料指標向前移，表示您再也不需要處理資料指標前的目錄項目。

如果基於某些原因，在處理目錄分葉時發生 Bug，只要將資料指標的時間向後退，讓程式碼重新處理舊的目錄項目即可。

## <a name="c-sample-code"></a>C# 範例程式碼

因為目錄是可透過 HTTP 使用的 JSON 文件集，所以它可與使用任何程式設計語言的 HTTP 用戶端和 JSON 還原序列化程式互動。

C# 範例位於 [NuGet/範例存放庫](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)。

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>目錄 SDK

取用目錄最簡單的方法，是使用發行前版本的 .NET 目錄 SDK 套件：[NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog)。 此套件位於 `nuget-build` MyGet 摘要，針對它使用 NuGet 套件來源 URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`。

您可以將這個套件安裝到與 `netstandard1.3` 或更高版本相容的專案 (例如.NET Framework 4.6)。

使用此套件的範例位於 GitHub 的 [NuGet.Protocol.Catalog.Sample 專案](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)。

#### <a name="sample-output"></a>範例輸出

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

### <a name="minimal-sample"></a>最小的範例

如需較少的相依性，示範與目錄更詳細互動的範例，請參閱 [CatalogReaderExample 範例專案](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)。 專案以 `netcoreapp2.0` 為目標，並依存於 [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (適用於解析服務索引) 和 [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (適用於 JSON 還原序列化)。

程式碼的主要邏輯會顯示在 [Program.cs 檔案](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs) 中。

#### <a name="sample-output"></a>範例輸出

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
