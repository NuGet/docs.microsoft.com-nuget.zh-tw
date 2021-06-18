---
title: NuGet 5.10 版本資訊
description: NuGet 5.10 的版本資訊，包括新功能、bug 修正及 Dcr。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356534"
---
# <a name="nuget-510-release-notes"></a>NuGet 5.10 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本 | 隨附於 .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.10 版](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝
  
> [!NOTE]
> Visual Studio 16.10、MSBuild 16.10 和 .NET 5.0.300 + 需要 NuGet.exe 5.10 或更新版本。

## <a name="summary-whats-new-in-510"></a>摘要：5.10 中的新功能

* 簽署：實行 dotnet 受信任-簽署者命令- [#8053](https://github.com/NuGet/Home/issues/8053)

* 在 Linux 上將預設驗證設為停用，但在 Windows 上預設為啟用- [#10713](https://github.com/NuGet/Home/issues/10713)

* 在 .NET 5 + Linux/MAC 上新增適用于套件簽署驗證的 ENV 變數- [#10742](https://github.com/NuGet/Home/issues/10742)

* 改善大型解決方案的安裝新套件效能- [#10166](https://github.com/NuGet/Home/issues/10166)

* 將專案類型新增 `nfproj` 至 NUGET CLI 的 supportedProjectExtensions 清單。 - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

* <requireLicenseAcceptance>封裝專案時隱藏元素- [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] 預覽警告應顯示在 dotnet cli 上- [#10226](https://github.com/NuGet/Home/issues/10226)

* 將 PMUI 的背景和前景色彩標記更新為 CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash]在 PM UI 中快速切換索引標籤時，[使用者已取消的作業] 錯誤顯示在 [錯誤清單] 視窗中： [#10671](https://github.com/NuGet/Home/issues/10671)

* PM UI：改善解決方案層級的套件安裝效能- [#10210](https://github.com/NuGet/Home/issues/10210)

* 將 GetService 取代為 NuGet 中的所有位置 GetServiceAsync。用戶端- [#3784](https://github.com/NuGet/Home/issues/3784)

* `..`相對路徑[#5016](https://github.com/NuGet/Home/issues/5016) NuGet.exe 套件效能問題

* 「Nuget 套件」的效能隨著來源路徑中增加的層級而減少- [#5706](https://github.com/NuGet/Home/issues/5706)

* 使用重複的檔案封裝 nuspec 時，NuGet 不會發生錯誤。 - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet 套件「指定的 DateTimeOffset 無法轉換成 Zip 檔案時間戳記」- [#7001](https://github.com/NuGet/Home/issues/7001)

* 封裝封裝的檔案時間戳記會依時區 [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 應包含更具可採取動作的資訊- [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash][測試失敗]當執行 ' dotnet restore-------------------lock-mode ' 時，不應更新空白/格式錯誤的鎖定檔案- [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange 可剖析邏輯上不正確的範圍- [#9145](https://github.com/NuGet/Home/issues/9145)

* PM UI 無法在選取和暫留套件來源之間顯示有辨別的背景色彩- [#9538](https://github.com/NuGet/Home/issues/9538)

* 螢幕讀取器無法讀取選取要安裝之專案的核取方塊- [#9578](https://github.com/NuGet/Home/issues/9578)

* 詳細資料窗格版本下拉式清單預設選項應安裝/LatestStable 在 [已安裝/更新] 索引標籤上- [#9887](https://github.com/NuGet/Home/issues/9887)

* 移除 #9913 的一些 .net 5 sdk 報表 TargetPlatformMoniker 的因應措施帳戶 ` ,Version= `  -  [](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget 驗證太安靜- [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange 無法剖析單一位數的範圍- [#10342](https://github.com/NuGet/Home/issues/10342)

* VS Solution manager 在調試期間擲回 null 例外狀況- [#10352](https://github.com/NuGet/Home/issues/10352)

* 將 CLI 例外狀況訊息移至字串資源檔- [#10392](https://github.com/NuGet/Home/issues/10392)

* 移除不正確程式碼 (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)

* 更新內容功能表應該會滾動至第一個選取的專案- [#10498](https://github.com/NuGet/Home/issues/10498)

* 方案 PMUI 詳細資料具有重迭的水準橫條 [#10533](https://github.com/NuGet/Home/issues/10533)

* 簽署：當憑證過期且時間戳記不受信任時，不會顯示主要簽章詳細資料- [#10535](https://github.com/NuGet/Home/issues/10535)

* 沒有已啟用的來源會防止 PM UI 顯示 [#10541](https://github.com/NuGet/Home/issues/10541)

* 封裝中繼資料 (詳細資料、取代) 有時不會從 CodeSpaces 中的 nuget.org 提取- [#10549](https://github.com/NuGet/Home/issues/10549)

* PMUI 初始化失敗，但在 debug 會話期間發生例外狀況- [#10559](https://github.com/NuGet/Home/issues/10559)

* nuget 還原會導致大型 endian 系統的套件完整性檢查失敗- [#10567](https://github.com/NuGet/Home/issues/10567)

* 擲回 >formatexception，而不是 PackagingException- [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM-圖形中的並行問題逐步解說演算法- [#10598](https://github.com/NuGet/Home/issues/10598)

* 新增 PMC powershell 版本遙測- [#10609](https://github.com/NuGet/Home/issues/10609)

* 改善 NuGetVersion 排序效能- [#10611](https://github.com/NuGet/Home/issues/10611)

* 受信任-簽署者新增具有不一致的引數- [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0：將 NuGet 封裝管理員中的索引標籤從 [更新] 切換至 [已安裝] 時，不會更新框架。 - [#10654](https://github.com/NuGet/Home/issues/10654)

* 從 PMUI 中的版本號碼移除 "v"- [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService 會在接收 CPS 專案系統提名之前擲回 GetInstalledPackagesAsync- [#10681](https://github.com/NuGet/Home/issues/10681)

* 內嵌圖示會導致在流覽索引標籤上從來源「Microsoft Visual Studio 離線套件」拒絕存取- [#10687](https://github.com/NuGet/Home/issues/10687)

* 如果未設定 MSBuildProjectExtensionsPath，則會擲回 INuGetProjectService GetInstalledPackagesAsync- [#10739](https://github.com/NuGet/Home/issues/10739)

* 「dotnet nuget 移除來源 nuget.org」無法在第一次使用 [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget 會封鎖非同步方法中的 threadpool 執行緒，以對 UI 執行緒進行同步呼叫 [#10775](https://github.com/NuGet/Home/issues/10775)

* 工具-> 選項-> NuGet 封裝管理員字串會被截斷- [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 是不正確程式碼，並會影響效能- [#10790](https://github.com/NuGet/Home/issues/10790)

* 使用 NuGet SDK 套件中的內嵌圖示- [#10795](https://github.com/NuGet/Home/issues/10795)

* 更新 SPDX 授權清單- [#10806](https://github.com/NuGet/Home/issues/10806)

**[此版本修正的所有問題清單-5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[此版本中的認可清單-5.10。0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>社群投稿

感謝所有協助讓此 NuGet 版本絕佳的參與者！

|人員|Pr|問題|
|----|----|----|
[港-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange 無法剖析單一位數的範圍- [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. 用戶端 build.sh 中斷- [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. 用戶端 build.sh 中斷- [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | 「Nuget 套件」的效能隨著來源路徑中增加的層級而減少- [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe pack 效能問題。 相對路徑- [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM-圖形中的並行問題逐步解說演算法- [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | 將專案類型 nfproj 新增至 Nuget CLI 的 supportedProjectExtensions 清單。 - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>歡迎意見反應

您的意見反應對我們非常寶貴。  如果此版本有任何問題，請查看我們的 [GitHub 問題](https://github.com/NuGet/Home/issues) ，並 [Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/) 現有的問題。  針對 NuGet 內的新問題，請報告 [GitHub 問題](https://github.com/NuGet/Home/issues/new)。
如需一般的 NuGet 體驗問題，請透過 [說明] 下您最愛的 IDE 中的 [回報 [問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ] 選項，讓我們知道 **> 報告問題**。
