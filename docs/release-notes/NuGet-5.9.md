---
title: NuGet 5.9 版本資訊
description: NuGet 5.9 的版本資訊，包括新功能、bug 修正及 Dcr。
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323878"
---
# <a name="nuget-59-release-notes"></a>NuGet 5.9 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本 | 隨附於 .NET SDK |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.9 版](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 16.9 版](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝
  
> [!NOTE]
> Visual Studio 16.9、MSBuild 16.9 和 .NET 5.0.200 + 需要 NuGet.exe 5.9 或更新版本。

## <a name="summary-whats-new-in-59"></a>摘要：5.9 中的新功能

* 針對使用預先選取的套件啟動封裝管理員 UI 的套件相依性，新增 [更新] 內容功能表項目以更新- [#10378](https://github.com/NuGet/Home/issues/10378)

    ![以滑鼠右鍵按一下 [封裝] 的 [更新] 體驗](media/releasenotes-59-update.png)

* 在方案層級中，于方案層級的 [版本] 資料行中顯示要求的版本 (包括浮動版本或版本範圍要求) 封裝管理員 UI- [#9827](https://github.com/NuGet/Home/issues/9827)

    ![解決方案層級封裝管理員 UI 中要求的版本](media/releasenotes-59-requested-version.png)

* 在封裝管理員 UI 流覽索引標籤中 IntelliCode 封裝的建議（以 A/B 測試 [#10053](https://github.com/NuGet/Home/issues/10053)

* 擴充檔案 `.nupkg.metadata` 以包含安裝來源- [#10354](https://github.com/NuGet/Home/issues/10354)

* 引進新的 msbuild 屬性，在 pack 工作期間排除特定 Tfm 的組建輸出- [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Dcr (設計變更要求) ：**

* 安裝最新的套件版本時，關閉圖示圖示並不直覺。 舊的綠色刻度是完美的 [#9789](https://github.com/NuGet/Home/issues/9789)

* Nuget Debug 詳細資訊應該指出封裝的來源- [#3055](https://github.com/NuGet/Home/issues/3055)

* NuGet 套件應該在版本號碼中攔截不正確的點省略- [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM]停用集中式可轉移相依性的釘選- [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM：缺少 TPV 時產生錯誤- [#9441](https://github.com/NuGet/Home/issues/9441)

* 記錄檔封裝 contenthash 在) 解壓縮期間的還原記錄 (- [#10384](https://github.com/NuGet/Home/issues/10384)

* 針對在開啟解決方案時呼叫還原的舊版 PR 專案，執行預先註冊機制 [#9986](https://github.com/NuGet/Home/issues/9986)

* 當套件管理員中選取了一個以上的來源時，NuGet 套件推薦應該會運作- [#10433](https://github.com/NuGet/Home/issues/10433)

* 在正常的詳細資訊還原時，記錄要從中還原封裝的來源 [#10461](https://github.com/NuGet/Home/issues/10461)

**錯誤：**

* INuGetPackageFileService-針對 Codespaces 連線和獨立[#10151](https://github.com/NuGet/Home/issues/10151)提取映射和內嵌授權

* VS OE： IProjectMetadataCoNtextInfo 缺少格式器- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-效能]減少寫入至 centralTransitiveDependencyGroups 的資訊- [#10002](https://github.com/NuGet/Home/issues/10002)

* 因為未載入的專案所擲回的還原作業會回報為 `NoOp` 遙測 [#9985](https://github.com/NuGet/Home/issues/9985)

* 具有特定顏色託盤的圖示會導致 PM UI 損毀與 [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-效能]新增 CPVM 資訊時減少 PackageSpec 複製- [#10003](https://github.com/NuGet/Home/issues/10003)

* PM UI-asyncify 圖示載入- [#10009](https://github.com/NuGet/Home/issues/10009)

* 在 PM UI 中載入圖示 Url 時的 UI 延遲- [#8505](https://github.com/NuGet/Home/issues/8505)

* BitmapSource 和 WPF UI 執行緒中的執行緒親和性- [#9161](https://github.com/NuGet/Home/issues/9161)

* 使用 targetframework 別名來 packastool 時警告 NU5128 的警告- [#10097](https://github.com/NuGet/Home/issues/10097)

* 自訂群組建中套件目標的 OutputPath 邏輯無法正常運作- [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE：用戶端上的快取 IServiceBroker 實例- [#10141](https://github.com/NuGet/Home/issues/10141)

* 建立 NuGetProjectActions 以從 PM UI 卸載平行作業- [#9956](https://github.com/NuGet/Home/issues/9956)

* 效能：減少舊版專案和非 PR 專案的 GetPackageSpecsAsync UIDelays- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` 未推送一個以上的檔案- [#4393](https://github.com/NuGet/Home/issues/4393)

* 當重新導向時，輸出會在 macOS 上以80個字元包裝： [#10198](https://github.com/NuGet/Home/issues/10198)

* 還原失敗，發生來源 <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp 5.0-windows 不會來回行程，也不會剖析平臺資訊- [#10177](https://github.com/NuGet/Home/issues/10177)

* 自訂的 CPS 專案需要 AssemblyReferences 專案功能才能進行還原。 - [#8071](https://github.com/NuGet/Home/issues/8071)

* 授權和圖示檔案存在檢查應該一律使用區分大小寫的比較- [#9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference 還原會讓您難以找出無 op 專案計數/uptodateprojectscount 的原因 [#10038](https://github.com/NuGet/Home/issues/10038)

* 當您在深色主題中透過 [選擇 NuGet 封裝管理員格式] 對話方塊流覽時，很難看到套件格式的虛線方塊- [#9729](https://github.com/NuGet/Home/issues/9729)

* 從 #10314 排除可轉移的架構參考 `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)

* 比較子的靜態屬性應為等冪- [#10339](https://github.com/NuGet/Home/issues/10339)

* 解決內部合約元件載入 (修正 RPS 或取得例外狀況) - [#9919](https://github.com/NuGet/Home/issues/9919)

* 將 GetService 取代為 NuGet 中的 GetServiceAsync。用戶端，第1部分- [#10362](https://github.com/NuGet/Home/issues/10362)

* CLI 安裝不應安裝未列出的套件- [#7466](https://github.com/NuGet/Home/issues/7466)

* 靜態 msbuild graph 還原-unnnecessary 有關 MSBuildStartupDirectory 的記錄- [#10335](https://github.com/NuGet/Home/issues/10335)

* 標記為 PrivateAssets 之 ProjectReferences 的專案相依性不應該包含在鎖定檔案中的最新檢查 [#8565](https://github.com/NuGet/Home/issues/8565)

* 具有錯誤資料的 SDK 專案未顯示 VS- [#10406](https://github.com/NuGet/Home/issues/10406)中的還原錯誤

* 從具有 LockedMode [#9623](https://github.com/NuGet/Home/issues/9623)的 cmd 行還原具有混合舊版和 netstandard2 專案的方案時，NU1004

* 套件包含透過相依性套件帶入目前專案套件中的內容， (SDK 型專案只) [#8867](https://github.com/NuGet/Home/issues/8867)

* 新增 NuGet 與擴充性 API 錯誤的遙測- [#10062](https://github.com/NuGet/Home/issues/10062)

* 在靜態圖形還原中新增 GenerateRestoreGraphFile，以改善 debugability。  - [#10365](https://github.com/NuGet/Home/issues/10365)

* 無法開啟 NuGet 套件管理員- [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/朗讀程式未讀取 "Apache-2.0" 連結的「授權」標籤- [#10425](https://github.com/NuGet/Home/issues/10425)

* 在 VS- [#9402](https://github.com/NuGet/Home/issues/9402)中，最新的狀態列訊息不太理想

* packages.config package.lock.js使用不正確的目標架構- [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces：修正 https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)的遙測

* 在啟用「RestoreLockedMode」之後建立解決方案時，錯誤 NU1004 消失- [#8973](https://github.com/NuGet/Home/issues/8973)

* 反向的 PMUI 中的 tab 鍵應向前鏡像 [#10234](https://github.com/NuGet/Home/issues/10234)

* 在實驗性實例中的 PMUI 錯，有時會從 SolutionView 擲回 InvalidCastException 至 ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)

* 在 [流覽] 索引標籤中按一下已淘汰的封裝之後，預設版本是 null- [#10380](https://github.com/NuGet/Home/issues/10380)

* Visual Studio 中的 NuGet 管理員在重新獲得焦點時重載- [#4176](https://github.com/NuGet/Home/issues/4176)

* 移除 IPackageSourceProvider2 和相關類型- [#10098](https://github.com/NuGet/Home/issues/10098)

* 套件 ' NameOfPackage ' 與專案[#5127](https://github.com/NuGet/Home/issues/5127)中的「所有」架構不相容

* CreateVersionsAsync 不需要 NuGetVersion 比較- [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet。用戶端應該使用 ManagedImageMonikers 取代 KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)

* 已淘汰的圖示與 [流覽] 索引標籤中已淘汰的套件版本重迭 [#10452](https://github.com/NuGet/Home/issues/10452)

* PackageReference NU1604 錯誤處理在 VS 和命令列之間不同 (Restore & 封裝管理員 UI) - [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces：未註冊必要的格式器- [#10467](https://github.com/NuGet/Home/issues/10467)

* 從 NuGet 以目標 framework 形式移除 net45。架構- [#10470](https://github.com/NuGet/Home/issues/10470)

* 執行-新增遙測以追蹤與 PMC 和 Powershell 使用方式相關的事件。 - [#10142](https://github.com/NuGet/Home/issues/10142)

* 當封裝管理員 UI 中有多個套件可供更新時，[預覽變更] 視窗中只會顯示一個套件： [#10483](https://github.com/NuGet/Home/issues/10483)

* 封裝 multitargeted 專案時，應該產生空白的 frameworkReferences 群組- [#10218](https://github.com/NuGet/Home/issues/10218)

* 很難在 [更新] 索引標籤[#8963](https://github.com/NuGet/Home/issues/8963))  (中，流覽 [更新] 索引標籤中的 [套件] 核取方塊。

* [更新] 索引標籤核取方塊無法與螢幕讀取器搭配使用- [#10449](https://github.com/NuGet/Home/issues/10449)

* 在 PMUI 中更新會導致物件參考未設定為物件的實例- [#9882](https://github.com/NuGet/Home/issues/9882)

* 執行-新增遙測以追蹤與 PMC 相關的事件，以及後續的 Powershell 使用方式。 - [#10478](https://github.com/NuGet/Home/issues/10478)

* V2FeedPackageInfo 中的複製貼上錯誤- [#10480](https://github.com/NuGet/Home/issues/10480)

* NuGetPackageFileService 修正-使用以取得可處置的 memorystream- [#10503](https://github.com/NuGet/Home/issues/10503)

**[此版本修正的所有問題清單-5.9。0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[此版本中的認可清單-5.9。0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>社群投稿

感謝所有協助讓此 NuGet 版本絕佳的參與者！

|人員|Pr|問題|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | V2FeedPackageInfo 中的複製貼上錯誤- [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | 遺漏以 PrivateAssets = "All" 屬性參考套件的案例的測試 [#10397](https://github.com/NuGet/Home/issues/10397)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | 新增推送多個套件的支援- [#4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | 停用元件簽署時，NuGet 程式庫的組建會中斷- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | 清除參與的檔- [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | 授權和圖示檔案存在檢查應該一律使用區分大小寫的比較- [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | 使用 DecodePixelWidth [#10037](https://github.com/NuGet/Home/issues/10037)時，請使用 BitmapCreateOptions IGNORECOLORPROFILE 解決 WPF 問題
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | NuGet 中的 Windows SDK 10 連結已中斷。用戶端投稿指南- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | NuGet 中的相對連結已中斷。用戶端偵測指南- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | 改善測試元件和相關的程式碼- [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | 當重新導向時，輸出會在 macOS 上以80個字元包裝： [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | 讓 Nuget.exe 以 .NET Standard 套件的形式提供- [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | 引進新的 msbuild 屬性，在 pack 工作期間排除特定 tfm 的組建輸出- [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>摘要：5.9.1 的新功能

* 「dotnet nuget 移除來源 nuget.org」無法在第一次使用 [#10745](https://github.com/NuGet/Home/issues/10745)
* 在 Linux 上將預設驗證設為停用，但在 Windows 上預設為啟用- [#10713](https://github.com/NuGet/Home/issues/10713)

**[此版本修正的所有問題清單-5.9。1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[此版本中的認可清單-5.9。1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>已知問題

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>nuget 5.9 套件引發 `Null Reference` 例外狀況。 - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>問題
當您使用檔案 tring 時 `pack` `.nuspec` ， `NuGet 5.9` `null reference` 如果指定 [明確的元件參考](../reference/nuspec.md#explicit-assembly-references) ，而沒有為目標的專案新增任何，則版本會引發例外狀況 `reference groups` `multiple frameworks` 。

#### <a name="workaround"></a>因應措施
使用 `nuget.exe` [5.8.1](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)  或最新版本 `5.9.1` 。

## <a name="feedback-welcome"></a>歡迎意見反應

您的意見反應對我們非常寶貴。  如果此版本有任何問題，請查看我們的 [GitHub 問題](https://github.com/NuGet/Home/issues) ，並 [Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/) 現有的問題。  針對 NuGet 內的新問題，請報告 [GitHub 問題](https://github.com/NuGet/Home/issues/new)。
如需一般的 NuGet 體驗問題，請透過 [說明] 下您最愛的 IDE 中的 [回報 [問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ] 選項，讓我們知道 **> 報告問題**。
