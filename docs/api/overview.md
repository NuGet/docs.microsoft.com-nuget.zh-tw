---
title: NuGet 伺服器 API 總覽
description: NuGet 伺服器 API 是一組 HTTP 端點，可用來下載套件、提取中繼資料、發佈新的封裝等等。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237805"
---
# <a name="nuget-server-api"></a>NuGet 伺服器 API

NuGet 伺服器 API 是一組 HTTP 端點，可用來下載套件、提取中繼資料、發佈新的封裝，以及執行官方 NuGet 用戶端中其他可用的其他作業。

Visual Studio、nuget.exe 和 .NET CLI 中的 NuGet 用戶端會使用此 API 來執行 NuGet 作業 [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) ，例如，在 VISUAL STUDIO UI 中搜尋，以及 [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md) 。

請注意，在某些情況下，nuget.org 具有其他套件來源未強制執行的其他需求。 這些差異記載于 [Nuget.org 通訊協定](nuget-protocols.md)。

如需簡單列舉和下載可用 nuget.exe 版本，請參閱端點 [ 上的tools.js](tools-json.md) 。

## <a name="service-index"></a>服務索引

API 的進入點是已知位置中的 JSON 檔。 這份檔稱為「 **服務索引** 」。 Nuget.org 服務索引的位置是 `https://api.nuget.org/v3/index.json` 。

此 JSON 檔包含的 *資源清單* 可提供不同的功能，並滿足不同的使用案例。

支援 API 的用戶端應接受其中一或多個服務索引 URL，以作為連接到個別套件來源的方法。

如需有關服務索引的詳細資訊，請參閱 [其 API 參考](service-index.md)。

## <a name="versioning"></a>版本控制

API 是 NuGet HTTP 通訊協定第3版。 此通訊協定有時稱為「V3 API」。 這些參考檔將會以「API」的形式來參考此版本的通訊協定。

服務索引架構版本是由 `version` 服務索引中的屬性所表示。 API 會要求版本字串具有的主要版本號碼 `3` 。 對服務索引架構進行非中斷的變更時，將會增加版本字串的次要版本。

較舊的用戶端 (例如 nuget.exe 2.x) 不支援 V3 API，而且僅支援舊版 V2 API，此處並未記載。

NuGet V3 API 的命名方式為，因為它是 V2 API 的後續版本，也就是由2.x 版的官方 NuGet 用戶端所執行的 OData 型通訊協定。 第3版的正式 NuGet 用戶端3.0 支援 V3 API，但它仍然是 NuGet 用戶端、4.0 和 on 所支援的最新主要通訊協定版本。 

自第一次發行之後，已對 API 進行了非中斷的通訊協定變更。

## <a name="resources-and-schema"></a>資源和架構

**服務索引** 會描述各種不同的資源。 目前支援的資源集如下所示：

資源名稱                                                        | 必要 | 描述
-------------------------------------------------------------------- | -------- | -----------
[目錄](catalog-resource.md)                                       | 否       | 所有封裝事件的完整記錄。
[PackageBaseAddress](package-base-address-resource.md)               | yes      | 取得套件內容 ( nupkg) 。
[PackageDetailsUriTemplate](package-details-template-resource.md)    | 否       | 建立 URL 以存取套件詳細資料網頁。
[PackagePublish](package-publish-resource.md)                        | yes      | 推送和刪除 (或取消列出) 套件。
[RegistrationsBaseUrl](registration-base-url-resource.md)            | yes      | 取得套件中繼資料。
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | 否       | 建立 URL 以存取報告不當使用的網頁。
[RepositorySignatures](repository-signatures-resource.md)            | 否       | 取得用於儲存機制簽署的憑證。
[SearchAutocompleteService](search-autocomplete-service-resource.md) | 否       | 依子字串探索套件識別碼和版本。
[SearchQueryService](search-query-service-resource.md)               | yes      | 依關鍵字篩選和搜尋封裝。
[SymbolPackagePublish](symbol-package-publish-resource.md)           | 否       | 推送符號套件。

一般而言，API 資源所傳回的所有非二進位資料都會使用 JSON 進行序列化。 服務索引中每個資源所傳回的回應架構會針對該資源個別定義。 如需有關每個資源的詳細資訊，請參閱以上所列的主題。

未來當通訊協定演進時，可能會將新的屬性新增至 JSON 回應。 為了讓用戶端能夠進行更好的驗證，此實行不應假設回應架構是最終的，且不能包含額外的資料。 應忽略此執行不了解的所有屬性。

> [!Note]
> 當來源未執行 `SearchAutocompleteService` 任何自動完成的行為時，應正常停用。 當未 `ReportAbuseUriTemplate` 執行時，官方 nuget 用戶端會切換回 nuget。組織的報告濫用 URL (由 [NuGet/Home # 4924](https://github.com/NuGet/Home/issues/4924)) 追蹤。 其他用戶端可能會選擇單純地不要向使用者顯示報告濫用 URL。

### <a name="undocumented-resources-on-nugetorg"></a>Nuget.org 上未記載的資源

Nuget.org 上的 V3 服務索引有一些先前未記載的資源。 沒有記錄資源的原因有很多。

首先，我們不會記錄用來作為 nuget.org 之執行詳細資料的資源。 `SearchGalleryQueryService` 屬於此類別。 [NuGetGallery](https://github.com/NuGet/NuGetGallery) 會使用此資源將某些 V2 (OData) 查詢委派給搜尋索引，而不是使用資料庫。 這項資源是為了因應擴充性而引進的，並非供外部使用。

其次，我們不會記錄未隨附于 RTM 版官方用戶端的資源。
`PackageDisplayMetadataUriTemplate` 並 `PackageVersionDisplayMetadataUriTemplate` 屬於這個類別。

Etag，我們不會記錄與 V2 通訊協定緊密結合的資源，而這些資源本身是刻意未記載的。 `LegacyGallery`資源會落在此類別中。 此資源可讓 V3 服務索引指向對應的 V2 來源 URL。 此資源支援 `nuget.exe list` 。

如果此處未記載資源， *強烈* 建議您不要相依于這些資源。 我們可能會移除或變更這些未記載資源的行為，這些資源可能會以非預期的方式中斷您的執行。

## <a name="timestamps"></a>時間戳記

API 所傳回的所有時間戳記都是 UTC，或使用 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 標記法來指定。 

## <a name="http-methods"></a>HTTP 方法

動詞命令   | 使用
------ | -----------
GET    | 執行唯讀操作，通常會抓取資料。
HEAD   | 提取對應要求的回應標頭 `GET` 。
PUT    | 建立不存在的資源，如果存在，則會加以更新。 有些資源可能不支援更新。
刪除 | 刪除或取消列出資源。

## <a name="http-status-codes"></a>HTTP 狀態碼

程式碼 | 描述
---- | -----
200  | 成功，而且有回應主體。
201  | 成功，而且已建立資源。
202  | 成功，已接受要求，但部分工作可能仍未完成，並以非同步方式完成。
204  | 成功，但沒有回應主體。
301  | 永久重新導向。
302  | 暫時重新導向。
400  | URL 或要求主體中的參數無效。
401  | 提供的認證無效。
403  | 提供的認證不允許此動作。
404  | 所要求的資源不存在。
409  | 要求與現有的資源發生衝突。
500  | 服務發生未預期的錯誤。
503  | 服務暫時無法使用。

對 `GET` API 端點提出的任何要求，都可能會傳回 HTTP 重新導向 (301 或 302) 。 用戶端應該藉由觀察 `Location` 標頭併發出後續的來適當地處理這類重新導向 `GET` 。 關於特定端點的檔將不會明確地呼叫可使用重新導向的位置。

在500層級狀態碼的情況下，用戶端可以執行合理的重試機制。 官方 NuGet 用戶端在遇到任何500層級的狀態碼或 TCP/DNS 錯誤時，會重試三次。

## <a name="http-request-headers"></a>HTTP 要求標頭

Name                     | 描述
------------------------ | -----------
X-NuGet-ApiKey           | 推送和刪除的必要參數，請參閱[ `PackagePublish` 資源](package-publish-resource.md)
X-NuGet-用戶端版本   | 已 **淘汰** 並取代為`X-NuGet-Protocol-Version`
X-NuGet-通訊協定版本 | 只有 nuget.org 上的某些情況下才需要，請參閱 [nuget.org 通訊協定](NuGet-Protocols.md)
X-NuGet-會話識別碼       | *選擇項* 。 NuGet 用戶端 4.7 + 識別屬於相同 NuGet 用戶端會話的 HTTP 要求。

`X-NuGet-Session-Id`對於與單一還原相關的所有作業，都有單一值 `PackageReference` 。 針對其他案例（例如自動完成和還原）， `packages.config` 可能會有數個不同的會話識別碼，原因是程式碼的因素。

## <a name="authentication"></a>驗證

驗證會保留給套件來源執行，以進行定義。 針對 nuget.org，只有 `PackagePublish` 資源需要透過特殊的 API 金鑰標頭進行驗證。 請參閱[ `PackagePublish` 資源](package-publish-resource.md)以取得詳細資料。
