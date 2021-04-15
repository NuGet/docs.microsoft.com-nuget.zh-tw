---
title: NuGet 5.7 版本資訊
description: NuGet 5.7 的版本資訊，包括新功能、bug 修正及 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508783"
---
# <a name="nuget-57-release-notes"></a>NuGet 5.7 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本 | 隨附於 .NET SDK |
|:---|:---|:---|
| [**5.7.0 版**](https://nuget.org/downloads) | [Visual Studio 2019 16.7 版](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |
| [**5.7.1**](https://nuget.org/downloads) | [Visual Studio 2019 16.7 版](https://visualstudio.microsoft.com/downloads/) | [3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝

## <a name="summary-whats-new-in-57"></a>摘要：5.7 中的新功能

### <a name="features-added-in-this-release"></a>此版本中新增的功能

* 已新增 NuGet 套件參考的外部別名支援- [#4989](https://github.com/NuGet/Home/issues/4989)

* 藉由允許它們共用資料來源並減少 resfreshing [#8294](https://github.com/NuGet/Home/issues/8294) ，使已安裝和更新索引標籤之間的切換變得更快

* 藉由呼叫 MSBuild 靜態圖形 api (dotnet.exe) [#9644](https://github.com/NuGet/Home/issues/9644) ，讓還原速度更快。

* 已為 PackageReference 專案新增 Visual Studio 部分還原 (無作業 + +) - [#9513](https://github.com/NuGet/Home/issues/9513)

* 在搜尋行為不正常的套件來源時，Visual Studio 封裝管理員 UI 的損毀，會傳回超過每個 HTTP 要求所要求的結果數目。 - [#8478](https://github.com/NuGet/Home/issues/8478)

* 在 VS restore- [#9236](https://github.com/NuGet/Home/issues/9236)中加入非 SDK 樣式專案的 PackageVersion 資訊整合

* 已新增 nuget.exe 更新的支援 `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* 在%APPDATA%\NuGet 目錄中新增了多個設定檔的支援- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths 現在會將 NuGet 來源套件納入帳戶 [#9431](https://github.com/NuGet/Home/issues/9431)

* 已新增 INuGetProjectService，GetInstalledPackagesAsync 擴充性 API- [#9702](https://github.com/NuGet/Home/issues/9702)

* 已新增 interop API 來列舉回溯資料夾，而不需要方案/專案 [#9395](https://github.com/NuGet/Home/issues/9395)

* 已新增 `latest` `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的選項

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**錯誤：**

* 在 dotnet CLI 還原中，啟動認證外掛程式時，如果 `DOTNET_HOST_PATH`  未定義環境變數，請嘗試在系統路徑上使用 DOTNET CLI。 - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe 規格會產生具有硬式編碼文字的著作權標記，而不是 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe 在元件名稱變更時，會在 .csproj 的封裝期間擲回例外狀況 ' 作者必要項 ' （如果變更元件名稱，則忽略預留位置和 assemblyinfo 屬性[#4234](https://github.com/NuGet/Home/issues/4234) ）

* HttpRequestMessage 會多次重複使用，SocketHttpHandler [#8661](https://github.com/NuGet/Home/issues/8661)不支援

* NuGet。 5.6.0 preview 3 和更新版本的索引使用不同的公開金鑰權杖- [#9481](https://github.com/NuGet/Home/issues/9481)

* 在建立 NuGet 套件期間接受 TreatWarningsAsErrors- [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM]多個 p2p 專案的假套件降級- [#9549](https://github.com/NuGet/Home/issues/9549)

* [流覽] 索引標籤不會靠左對齊搜尋方塊- [#9559](https://github.com/NuGet/Home/issues/9559)

* 安裝的版本與解決方案等級 PM UI 中的內嵌圖示不一致，其中一個套件識別碼已安裝多個版本- [#9321](https://github.com/NuGet/Home/issues/9321)

* 遺漏： PartCreationPolicy (CreationPolicy。非共用的) SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* 避免在無作業還原中讀取資產檔案- [#9693](https://github.com/NuGet/Home/issues/9693)

* Nuget.exe 不支援從搜尋[#9086](https://github.com/NuGet/Home/issues/9086)取得版本的下載計數

* 藉由減少 JObject 相依性來改善 PackageMetadataResourceV3 的記憶體效能- [#9719](https://github.com/NuGet/Home/issues/9719)

**設計變更要求：**

* `<owners>`當元素是多餘的時隱藏元素[#5134](https://github.com/NuGet/Home/issues/5134)

* 記錄 IntervalTrackers 為 ETW 事件- [#9593](https://github.com/NuGet/Home/issues/9593)

* 在還原時新增了參考用訊息，以通知 CPVM 使用者此功能目前為預覽狀態 [#9340](https://github.com/NuGet/Home/issues/9340)

* 從資產檔案填入方案總管套件/專案可轉移相依性- [#9580](https://github.com/NuGet/Home/issues/9580)

* [已安裝的套件] 索引標籤不應將套件清單分頁 [#6995](https://github.com/NuGet/Home/issues/6995)

**[此版本修正的所有問題清單-5。7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>社群投稿

感謝所有協助讓此 NuGet 版本絕佳的參與者！

|人員|Pr|問題|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433)、 [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|Nuget.exe 不支援從搜尋[#9086](https://github.com/NuGet/Home/issues/9086)取得版本的下載計數 </br>HttpRequestMessage 會多次重複使用，SocketHttpHandler [#8661](https://github.com/NuGet/Home/issues/8661)不支援|
|[Joseph Musser (jnm2) ](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|`<owners>`當元素是多餘的時隱藏元素[#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad) ](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet 無法從需要用戶端憑證的 HTTPS 來源還原- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok) ](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim 未來的校對- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek) ](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe 規格會產生具有硬式編碼文字的著作權標記，而不是 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (Olivier-Spinelli) ](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|在 dotnet CLI 還原中，啟動認證外掛程式時，如果 `DOTNET_HOST_PATH`  未定義環境變數，請嘗試在系統路徑上使用 DOTNET CLI。 - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|已新增 `latest` `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的選項|

## <a name="summary-whats-new-in-571"></a>摘要：5.7.1 的新功能

* 擴充 nupkg 中繼檔以包含安裝來源- [#10354](https://github.com/NuGet/Home/issues/10354)

* 記錄檔封裝 contenthash 在) 解壓縮期間的還原記錄 (- [#10384](https://github.com/NuGet/Home/issues/10384)

* 在正常的詳細資訊還原時，記錄要從中還原封裝的來源 [#10461](https://github.com/NuGet/Home/issues/10461)

**[此版本中已修正的所有問題清單-5.7。1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**

**[此版本中的認可清單-5.7。1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**
