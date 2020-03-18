---
title: NuGet 伺服器 API 總覽
description: NuGet 伺服器 API 是一組 HTTP 端點，可用來下載封裝、提取中繼資料、發佈新套件等等。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428706"
---
# <a name="nuget-server-api"></a>NuGet 伺服器 API

NuGet 伺服器 API 是一組 HTTP 端點，可用來下載封裝、提取中繼資料、發佈新封裝，以及執行官方 NuGet 用戶端中的大部分其他作業。

Visual Studio、nuget.exe 和 .NET CLI 中的 NuGet 用戶端會使用此 API 來執行 NuGet 作業，例如[`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)、在 Visual Studio UI 中搜尋，以及[`nuget.exe push`](../reference/cli-reference/cli-ref-push.md)。

請注意，在某些情況下，nuget.org 有其他套件來源不會強制執行的其他需求。 這些差異都是由[Nuget.org 通訊協定](nuget-protocols.md)所記載。

如需簡單列舉和可下載可用的 nuget.exe 版本，請參閱[tools. json](tools-json.md)端點。

## <a name="service-index"></a>服務索引

API 的進入點是已知位置中的 JSON 檔。 這份檔稱為**服務索引**。 Nuget.org 服務索引的位置是 `https://api.nuget.org/v3/index.json`。

此 JSON 檔包含提供不同功能和滿足不同使用案例的*資源清單*。

支援 API 的用戶端應該接受其中一或多個服務索引 URL，做為連接到個別套件來源的方法。

如需服務索引的詳細資訊，請參閱[其 API 參考](service-index.md)。

## <a name="versioning"></a>版本控制

API 是 NuGet 的 HTTP 通訊協定第3版。 此通訊協定有時稱為「V3 API」。 這些參考檔將會參考此版本的通訊協定，就像「API」一樣。

服務索引架構版本是由服務索引中的 `version` 屬性所表示。 API 會要求版本字串具有 `3`的主要版本號碼。 當對服務索引架構進行非重大變更時，將會增加版本字串的次要版本。

較舊的用戶端（例如 nuget.exe 2.x）不支援 V3 API，而且只支援舊版 V2 API，此處未記載。

NuGet V3 API 的命名方式如下，因為它是 V2 API 的後續版本，這是由2.x 版的官方 NuGet 用戶端所實作為的 OData 通訊協定。 V3 API 第一次受到3.0 版官方 NuGet 用戶端支援，而且仍然是 NuGet 用戶端、4.0 和上所支援的最新主要通訊協定版本。 

自第一次發行後，已對 API 進行非中斷的通訊協定變更。

## <a name="resources-and-schema"></a>資源和架構

**服務索引**會描述各種不同的資源。 目前支援的資源集如下所示：

資源名稱                                                        | 必要項 | 描述
-------------------------------------------------------------------- | -------- | -----------
[目錄](catalog-resource.md)                                       | no       | 所有封裝事件的完整記錄。
[PackageBaseAddress](package-base-address-resource.md)               | 是      | 取得套件內容（. nupkg）。
[PackageDetailsUriTemplate](package-details-template-resource.md)    | no       | 建立 URL 以存取封裝詳細資料網頁。
[PackagePublish](package-publish-resource.md)                        | 是      | 推送和刪除（或取消列出）套件。
[RegistrationsBaseUrl](registration-base-url-resource.md)            | 是      | 取得套件中繼資料。
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | no       | 建立 URL 以存取報告不當使用的網頁。
[RepositorySignatures](repository-signatures-resource.md)            | no       | 取得用於存放庫簽署的憑證。
[SearchAutocompleteService](search-autocomplete-service-resource.md) | no       | 依子字串探索套件識別碼和版本。
[SearchQueryService](search-query-service-resource.md)               | 是      | 依關鍵字篩選及搜尋封裝。
[SymbolPackagePublish](symbol-package-publish-resource.md)           | no       | 推送符號套件。

一般而言，API 資源傳回的所有非二進位資料都會使用 JSON 進行序列化。 服務索引中每個資源所傳回的回應架構，會針對該資源個別定義。 如需有關每個資源的詳細資訊，請參閱上面所列的主題。

未來，當通訊協定進化時，可能會將新的屬性新增至 JSON 回應。 若要讓用戶端成為未來的證明，此執行應該不會假設回應架構是最終的，而且不能包含額外的資料。 應該忽略此實作為不了解的所有屬性。

> [!Note]
> 當來源未執行時 `SearchAutocompleteService` 應正常地停用任何自動完成行為。 未執行 `ReportAbuseUriTemplate` 時，官方 NuGet 用戶端會切換回 nuget. 組織的報告不當使用 URL （由[NuGet/Home # 4924](https://github.com/NuGet/Home/issues/4924)追蹤）。 其他用戶端可能只選擇不要向使用者顯示報告不當的 URL。

### <a name="undocumented-resources-on-nugetorg"></a>Nuget.org 上未記載的資源

Nuget.org 上的 V3 服務索引有一些未記載的資源。 不記載資源有幾個原因。

首先，我們不會記載用來作為 nuget.org 之執行詳細資料的資源。`SearchGalleryQueryService` 落在此類別中。 [NuGetGallery](https://github.com/NuGet/NuGetGallery)會使用此資源將一些 V2 （OData）查詢委派給我們的搜尋索引，而不是使用資料庫。 這是基於擴充性的原因而引進的資源，並非供外部使用。

第二，我們不記載官方用戶端 RTM 版本中從未發行的資源。
`PackageDisplayMetadataUriTemplate` 和 `PackageVersionDisplayMetadataUriTemplate` 都屬於此類別。

Etag，我們不會記錄與 V2 通訊協定緊密結合的資源，這本身是刻意記載的。 `LegacyGallery` 資源屬於此類別。 此資源可讓 V3 服務索引指向對應的 V2 來源 URL。 此資源支援 `nuget.exe list`。

如果資源未記載在此處，我們*強烈*建議您不要依賴它們。 我們可能會移除或變更這些未記載資源的行為，這可能會以非預期的方式中斷您的執行。

## <a name="timestamps"></a>時間戳記

API 傳回的所有時間戳記都是 UTC，否則會使用[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)標記法來指定。 

## <a name="http-methods"></a>HTTP 方法

動詞   | 用法
------ | -----------
GET    | 執行唯讀作業，通常會抓取資料。
HEAD   | 提取對應 `GET` 要求的回應標頭。
PUT    | 建立不存在的資源，或如果存在，則會加以更新。 某些資源可能不支援更新。
DELETE | 刪除或取消列出資源。

## <a name="http-status-codes"></a>HTTP 狀態碼

程式碼 | 描述
---- | -----
200  | 成功，而且有回應主體。
201  | 成功，並建立資源。
202  | 成功，已接受要求，但部分工作可能仍未完成，且以非同步方式完成。
204  | 成功，但沒有回應主體。
301  | 永久重新導向。
302  | 暫時重新導向。
400  | URL 或要求主體中的參數無效。
401  | 提供的認證無效。
403  | 提供的認證不允許此動作。
404  | 要求的資源不存在。
409  | 要求與現有的資源衝突。
500  | 服務發生未預期的錯誤。
503  | 服務暫時無法使用。

對 API 端點提出的任何 `GET` 要求可能會傳回 HTTP 重新導向（301或302）。 用戶端應該藉由觀察 `Location` 標頭併發出後續的 `GET`，正常地處理這類重新導向。 關於特定端點的檔不會明確地呼叫可使用重新導向的位置。

在500層級狀態碼的情況下，用戶端可以執行合理的重試機制。 當遇到任何500層級狀態碼或 TCP/IP 錯誤時，官方 NuGet 用戶端會重試三次。

## <a name="http-request-headers"></a>HTTP 要求標頭

名稱                     | 描述
------------------------ | -----------
X-NuGet-ApiKey           | 需要進行推送和刪除，請參閱[`PackagePublish` 資源](package-publish-resource.md)
X-NuGet-用戶端版本   | 已**淘汰**，並由 `X-NuGet-Protocol-Version` 取代
X-NuGet-通訊協定-版本 | 只有在 nuget.org 上的某些情況下才需要，請參閱[nuget.org 通訊協定](NuGet-Protocols.md)
X-NuGet-會話識別碼       | *選擇性*。 NuGet 用戶端 4.7 + 會識別屬於相同 NuGet 用戶端會話的 HTTP 要求。

`X-NuGet-Session-Id` 具有單一值，適用于 `PackageReference`中單一還原相關的所有作業。 針對其他案例（例如自動完成和 `packages.config` 還原），可能會有數個不同的會話識別碼，原因是程式碼的要素。

## <a name="authentication"></a>驗證

驗證會保留給要定義的套件來源執行。 針對 nuget.org，只有 `PackagePublish` 資源需要透過特殊 API 金鑰標頭進行驗證。 如需詳細資訊，請參閱[`PackagePublish` 資源](package-publish-resource.md)。
