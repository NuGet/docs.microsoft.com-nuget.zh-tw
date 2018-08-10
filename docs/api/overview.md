---
title: NuGet API 的概觀
description: NuGet API 是一組可以用來下載套件、 擷取中繼資料，發佈新的套件等的 HTTP 端點。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fe843a121e2f1aae376f3e30a7b911792057688f
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020527"
---
# <a name="nuget-api"></a>NuGet API

NuGet API 是一組可用來下載套件、 擷取中繼資料、 發行新的套件，以及執行大部分其他官方 NuGet 用戶端中可用的作業的 HTTP 端點。

此 API 可由 NuGet 用戶端，在 Visual Studio 中，nuget.exe 和.NET CLI 來執行 NuGet 作業，例如[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)，在 Visual Studio UI 中，搜尋並[ `nuget.exe push` ](../tools/cli-ref-push.md)。

請注意在某些情況下，nuget.org 不會強制執行由其他套件來源的其他需求。 這些差異都記錄所[nuget.org 通訊協定](nuget-protocols.md)。

## <a name="service-index"></a>服務索引

API 的進入點是 JSON 文件中的已知的位置。 這份文件會呼叫**服務索引**。 Nuget.org 的服務索引的位置是`https://api.nuget.org/v3/index.json`。

此 JSON 文件包含一份*資源*這提供不同的功能，而且滿足不同使用案例。

支援 API 的用戶端應接受一或多個這些服務的索引 URL 做為連接到個別的套件來源的方法。

如需有關服務索引的詳細資訊，請參閱[其 API 參考](service-index.md)。

## <a name="versioning"></a>版本控制

NuGet 的 HTTP 通訊協定第 3 版的 API。 此通訊協定有時稱為 「 V3 API。 」 這些參考文件會參考到此版本的通訊協定，簡稱為 「 API 」。

服務索引結構描述版本由`version`服務索引中的屬性。 API 要求的版本字串具有主要版本號碼`3`。 服務索引結構描述會進行非中斷變更，就會增加的版本字串的次要版本。

舊版的用戶端 (例如 nuget.exe 2.x) 不支援 V3 API 和只支援較舊的 V2 API，此處並未記載。

因為它是已藉由將 2.x 版的官方 NuGet 用戶端的 OData 型通訊協定 V2 API 的後續版本，是這樣命名 NuGet V3 API。 V3 API 第一次支援官方 NuGet 用戶端 3.0 版，仍的最新的主要通訊協定版本的 NuGet 用戶端，4.0 和支援上。 

非重大通訊協定已變更的 API 因為它是第一個版本。

## <a name="resources-and-schema"></a>資源和結構描述

**服務索引**說明各種不同的資源。 目前的一組支援資源如下所示：

資源名稱                                                          | 必要 | 描述
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | 是      | 推送和刪除 （或取消列出） 封裝。
[`SearchQueryService`](search-query-service-resource.md)               | 是      | 篩選和關鍵字搜尋的封裝。
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | 是      | 取得套件中繼資料。
[`PackageBaseAddress`](package-base-address-resource.md)               | 是      | 取得封裝的內容 (.nupkg)。
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | 否       | 探索的子字串的封裝識別碼和版本。
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | 否       | 建構存取 「 檢舉不當使用 」 網頁的 URL。
[`RepositorySignatures`](repository-signatures-resource.md)            | 否       | 取得用來存放庫簽章的憑證。
[`Catalog`](catalog-resource.md)                                       | 否       | 完整封裝的所有事件的記錄。

一般情況下，API 資源傳回的所有非二進位資料會使用 JSON 序列化的。 服務索引中每個資源所傳回的回應結構描述是個別針對該資源定義。 如需有關每個資源的詳細資訊，請參閱以上所列的主題。

> [!Note]
> 當來源未實作`SearchAutocompleteService`應該依正常程序停用任何自動完成行為。 當`ReportAbuseUriTemplate`未實作，官方的 NuGet 用戶端會回到 nuget.org 的報告不當使用 URL (藉由追蹤[NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924))。 其他用戶端也可以選擇只顯示檢舉不當使用 URL 給使用者。

## <a name="timestamps"></a>時間戳記

所有 API 所傳回的時間戳記 UTC 或另外指定使用[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表示法。 

## <a name="http-methods"></a>HTTP 方法

動詞命令   | 使用
------ | -----------
GET    | 執行唯讀作業，通常擷取資料。
HEAD   | 擷取對應的回應標頭`GET`要求。
PUT    | 建立不存在，或如果存在，則會更新它的資源。 某些資源可能不支援更新。
DELETE | 刪除或取消列出的資源。

## <a name="http-status-codes"></a>HTTP 狀態碼

程式碼 | 描述
---- | -----
200  | 如果成功，而且沒有回應主體。
201  | 已建立成功時和資源。
202  | 成功時，要求已被接受，但是一些工作，仍可能不完整和已完成以非同步的方式。
204  | 如果成功，但沒有回應主體。
301  | 永久重新導向。
302  | 暫時重新導向。
400  | 在 URL 或要求主體中的參數不是有效的。
401  | 提供的認證不正確。
403  | 指定提供的認證，不允許的動作。
404  | 要求的資源不存在。
409  | 與現有的資源要求衝突。
500  | 服務發生未預期的錯誤。
503  | 暫時無法使用此服務。

任何`GET`對 API 端點提出的要求可能會傳回 HTTP 重新導向 （301 或 302）。 用戶端應妥善處理這類的重新導向，觀察`Location`標頭和發出的後續`GET`。 關於特定端點的文件不會明確呼叫時可能會使用重新導向。

如果層級的 500 狀態碼和用戶端可以實作合理的重試機制。 官方 NuGet 用戶端時的重試三次發生的任何層級的 500 狀態碼或 TCP/DNS 錯誤。

## <a name="http-request-headers"></a>HTTP 要求標頭

名稱                     | 描述
------------------------ | -----------
X-NuGet-ApiKey           | 所需的推送和刪除，請參閱[`PackagePublish`資源](package-publish-resource.md)
X-NuGet-Client-Version   | **已被取代**而被取代 `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | 在某些情況下，只能在 nuget.org 上有需要，請參閱[nuget.org 通訊協定](NuGet-Protocols.md)
X-NuGet-Session-Id       | *選擇性*。 NuGet 用戶端 v4.7 + 識別屬於相同的 NuGet 用戶端工作階段的 HTTP 要求。 針對`PackageReference`有還原作業是單一工作階段識別碼，其他情況下自動完成，例如和`packages.config`可能有數個不同的工作階段識別碼的由於重整程式碼的方式還原。

## <a name="authentication"></a>驗證

驗證會保留最多定義的套件來源實作。 對於 nuget.org，只有`PackagePublish`資源需要驗證透過特殊的 API 金鑰標頭。 請參閱[`PackagePublish`資源](package-publish-resource.md)如需詳細資訊。
