---
title: NuGet 的 API 的概觀
description: NuGet API 是一組可用來下載套件、 擷取中繼資料，發佈新的封裝、 等等的 HTTP 端點。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a638dba005c14bff4b2e668e2d6ca527a67b94a9
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-api"></a>NuGet 的 API

NuGet API 是一組可用來下載的封裝、 擷取中繼資料、 發行新的封裝，並執行大部分官方 NuGet 用戶端中提供其他作業的 HTTP 端點。

這個 API 用於在 Visual Studio、 nuget.exe 和.NET CLI NuGet 用戶端執行 NuGet 作業，例如[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)，在 Visual Studio UI 中，搜尋和[ `nuget.exe push` ](../tools/cli-ref-push.md)。

請注意，在某些情況下中, nuget.org 有額外的需求不會強制執行由其他封裝來源。 這些差異皆記錄由[nuget.org 通訊協定](nuget-protocols.md)。

## <a name="service-index"></a>服務索引

應用程式開發介面的進入點是 JSON 文件中的已知位置。 這份文件稱為**服務索引**。 Nuget.org 的服務索引的位置是`https://api.nuget.org/v3/index.json`。

此 JSON 文件包含一份*資源*提供不同的功能以及滿足不同使用案例。

支援 API 的用戶端應接受一或多個這些服務索引 URL 做為連接到個別的套件來源的方法。

如需服務索引的詳細資訊，請參閱[其應用程式開發介面參考](service-index.md)。

## <a name="versioning"></a>版本控制

應用程式開發介面是 NuGet 的 HTTP 通訊協定第 3 版。 此通訊協定有時稱為 「 V3 API。 」 這個版本的通訊協定會參考這些參考文件簡稱為 「 應用程式開發介面。 」

服務索引結構描述版本會以`version`服務索引中的屬性。 API 要求的版本字串的主要版本號碼`3`。 服務索引結構描述會進行非中斷變更，就會增加的版本字串的次要版本。

舊版的用戶端 (例如 nuget.exe 2.x) 不支援 V3 API，僅支援 舊 V2 API，這裡不記錄。

NuGet V3 API 名為在這種情況，所以 V2 API 的後置項已正式 NuGet 用戶端的 2.x 版本所實作的 OData 型通訊協定。 3.0 版的官方 NuGet 用戶端第一次支援 V3 API，而且仍然的最新的主要通訊協定版本支援 NuGet 用戶端，4.0，在。 

第一次發行以來已經對 API 進行非重大通訊協定變更。

## <a name="resources-and-schema"></a>資源和結構描述

**服務索引**描述各種資源。 目前的支援的資源集，如下所示：

資源名稱                                                          | 必要 | 描述
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | 是      | 推入和刪除 （或 unlist） 封裝。
[`SearchQueryService`](search-query-service-resource.md)               | 是      | 篩選並依關鍵字搜尋的封裝。
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | 是      | 取得封裝的中繼資料。
[`PackageBaseAddress`](package-base-address-resource.md)               | 是      | 取得封裝的內容 (.nupkg)。
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | 否       | 探索的子字串的封裝識別碼和版本。
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | 否       | 建構存取 「 檢舉不當使用 「 web 網頁的 URL。
[`Catalog`](catalog-resource.md)                                       | 否       | 完整記錄的所有封裝事件。

一般情況下，應用程式開發介面資源所傳回的所有非二進位資料會使用 JSON 序列化的。 服務索引中每項資源所傳回的回應結構描述是個別定義該資源。 如需有關每個資源的詳細資訊，請參閱上面所列的主題。

> [!Note]
> 當來源未實作`SearchAutocompleteService`應該依正常程序停用任何自動完成行為。 當`ReportAbuseUriTemplate`未實作，正式的 NuGet 用戶端會回到 nuget.org 的報表濫用的 URL (所追蹤[NuGet/首頁 #4924](https://github.com/NuGet/Home/issues/4924))。 其他用戶端也可以選擇只要不向使用者顯示報表濫用的 URL。

## <a name="timestamps"></a>時間戳記

所有 API 所傳回的時間戳記是 UTC，或未指定使用[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表示法。 

## <a name="http-methods"></a>HTTP 方法

動詞命令   | 使用
------ | -----------
GET    | 執行唯讀作業，通常擷取資料。
HEAD   | 擷取對應的回應標頭`GET`要求。
PUT    | 建立不存在，或如果檔案存在，會更新它的資源。 有些資源可能不支援更新。
DELETE | 刪除或 unlists 資源。

## <a name="http-status-codes"></a>HTTP 狀態碼

程式碼 | 描述
---- | -----
200  | 如果成功，而且沒有回應主體。
201  | 已建立成功時，與資源。
202  | 成功時，要求已接受，但是某些工作可能仍然會在不完整而且已完成以非同步的方式。
204  | 如果成功，但不會有回應主體。
301  | 永久重新導向。
302  | 暫時重新導向。
400  | 在 URL 或要求主體中的參數不是有效的。
401  | 提供的認證不正確。
403  | 此動作不允許指定所提供的認證。
404  | 要求的資源不存在。
409  | 與現有資源的要求衝突。
500  | 服務發生未預期的錯誤。
503  | 此服務暫時無法使用。

任何`GET`對 API 端點的要求可能會傳回 HTTP 重新導向 （301 或 302）。 用戶端應妥善處理這類的重新導向觀察`Location`標頭和後續發出`GET`。 關於特定端點的文件不會明確呼叫時可能會使用重新導向。

在 500 層級狀態程式碼中，用戶端可以實作合理的重試機制。 官方 NuGet 用戶端重試三次時遇到任何 500 層級狀態程式碼或 TCP/DNS 錯誤。

## <a name="http-request-headers"></a>HTTP 要求標頭

名稱                     | 描述
------------------------ | -----------
X-NuGet-ApiKey           | 所需推入和刪除，請參閱[`PackagePublish`資源](package-publish-resource.md)
X-NuGet-Client-Version   | **已被取代**而被取代 `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | 在某些情況下，只在 nuget.org 的需要，請參閱[nuget.org 通訊協定](NuGet-Protocols.md)
X-NuGet-Session-Id       | *選擇性*。 NuGet 的用戶端 v4.7 + 識別相同 NuGet 用戶端工作階段的一部分的 HTTP 要求。 如`PackageReference`有還原作業是單一工作階段識別碼，如需其他案例，例如自動完成，並`packages.config`可能有數個不同的工作階段 id 的由於程式碼分解的方式還原。

## <a name="authentication"></a>驗證

驗證會保持最多要定義的封裝來源實作。 只有 nuget.org 的`PackagePublish`的資源需要驗證，透過特殊的 API 金鑰標頭。 請參閱[`PackagePublish`資源](package-publish-resource.md)如需詳細資訊。
