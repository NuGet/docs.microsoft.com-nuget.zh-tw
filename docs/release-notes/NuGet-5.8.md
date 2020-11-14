---
title: NuGet 5.8 版本資訊
description: NuGet 5.8 的版本資訊，包括新功能、bug 修正及 Dcr。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 09fb98eec79ee4ed08d85a1c557a420d6b265f11
ms.sourcegitcommit: f4b74b500e3db9e468f11142df48d87880382267
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2020
ms.locfileid: "94572827"
---
# <a name="nuget-58-release-notes"></a>NuGet 5.8 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本 | 隨附於 .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 16.8 版](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝
  
> [!NOTE]
> Visual Studio 16.8、MSBuild 16.8 和 .NET 5.0 需要 NuGet.exe 5.8 或更新版本。


## <a name="summary-whats-new-in-58"></a>摘要：5.8 中的新功能
🎉 **這是為以 .net 5.0 為目標的 NuGet 套件提供完整撰寫和還原支援的第一個版本** 🎉

* 使用 mmap/CreateFileMapping 加速 nupkg 的解壓縮- [#9807](https://github.com/NuGet/Home/issues/9807)

* 在封裝管理員 UI 套件詳細資料窗格中顯示套件弱點詳細資料- [#9850](https://github.com/NuGet/Home/issues/9850)

* 使用新的命令來確認已簽署的 NuGet 套件 [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) - [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) 支援 `--prerelease` 新增套件最新版本的選項，包括發行前版本- [#4699](https://github.com/NuGet/Home/issues/4699)

* 使用 [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) 命令[#9704](https://github.com/NuGet/Home/issues/9704)在 CLI 中搜尋套件

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) 命令支援 `--verbosity` 選項 [#9600](https://github.com/NuGet/Home/issues/9600)

* 在 Visual Studio [#9565](https://github.com/NuGet/Home/issues/9565)中，為 .csproj 樣式的 PackageReference 專案啟用快速 No-Op 還原優化

* 解決方案層級封裝管理員 UI 作業，例如封裝安裝和更新的速度高達10倍- [#6010](https://github.com/NuGet/Home/issues/6010)

* Visual Studio [#9982](https://github.com/NuGet/Home/issues/9982)、 [#9984](https://github.com/NuGet/Home/issues/9984)、 [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)中的數個其他 NuGet 效能改進


### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Dcr**

* .NET 5.0 TFM： Framework 優先順序規則- [#9436](https://github.com/NuGet/Home/issues/9436)

* 剖析 TargetFramework 時，NuGet 不應推中斷點平臺版本- [#9842](https://github.com/NuGet/Home/issues/9842)

* 使用 TargetFrameworkMoniker & TargetPlatformMoniker 來推斷架構，而不是使用個別 TFI、TFV、TPI、TPV 屬性- [#9895](https://github.com/NuGet/Home/issues/9895)

* 更新 `GetReferenceNearestTargetFrameworkTask()` 以支援具有平臺 (的目標 framework，例如 net 5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)

* .NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)

* 封裝管理員 UI：合併或更新套件作業不應封鎖，因為 (封裝降級等錯誤 ) ） [#9224](https://github.com/NuGet/Home/issues/9224)

* 具有此功能的專案應該亮亮 NuGet 功能;"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* 在 Visual Studio [#6384](https://github.com/NuGet/Home/issues/6384)中隱藏 No-Op 還原訊息

**錯誤：**

* 在背景執行緒上不應呼叫 OutputWindowTextWriter 的函式- [#9764](https://github.com/NuGet/Home/issues/9764)

* 在 Big Endian Cpu 上還原已簽署的套件- [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger 不應在 MEF 函式中呼叫相似化為方法- [#9591](https://github.com/NuGet/Home/issues/9591)

* Nuget.exe 中的 Bug-命令列 `PrintJustified()` 方法- [#9737](https://github.com/NuGet/Home/issues/9737)

* 當套件中繼資料因為系結錯誤而被垃圾收集時，封裝管理員 UI 記憶體流失 [#9757](https://github.com/NuGet/Home/issues/9757)

* 簽名使用封裝管理員 UI 中的 packages.config 格式安裝簽署套件時，不會在錯誤清單中顯示任何警告- [#9798](https://github.com/NuGet/Home/issues/9798)

* XPlat 不應該有公用 Api- [#9821](https://github.com/NuGet/Home/issues/9821)

* 藉由封鎖具有 #9822 的執行緒集區執行緒，來減少解決方案載入時間所造成的資源爭用 `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* 在命令列還原中，使用多目標專案時，NuGet 應從內部組建讀取目標 framework 相關資訊- [#9869](https://github.com/NuGet/Home/issues/9869)

* 透過 TargetFrameworkInformation 專案讀取執行時間識別碼圖形- [#9874](https://github.com/NuGet/Home/issues/9874)

* 相較于 Visual Studio 和一般 MSBuild 評估還原，靜態圖形還原與 CrossTargeting 屬性不一致- [#9881](https://github.com/NuGet/Home/issues/9881)

* 在靜態圖形還原中，有多個目標專案時，NuGet 應該從內部組建讀取目標 framework 相關的資訊。 - [#9870](https://github.com/NuGet/Home/issues/9870)

* 允許 `net5.0-platform` 在 Visual Studio 中載入和還原專案 [#9863](https://github.com/NuGet/Home/issues/9863)

* 在封裝管理員 UI 中顯示已解決的版本- [#9826](https://github.com/NuGet/Home/issues/9826)

* 封裝管理員 UI：方案總管不會顯示所有 NuGet 套件相依性- [#9898](https://github.com/NuGet/Home/issues/9898)

* 更新 SPDX 授權清單- [#9946](https://github.com/NuGet/Home/issues/9946)

* 開啟管理 NuGet 套件之後的 VS 2019 損毀：圖示會導致映射 conversio 中未處理的例外狀況- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet。解壓縮需要 ilmerge，以排除 Newtonsoft.Js內部 [#9966](https://github.com/NuGet/Home/issues/9966)

* 沒有錯誤時，ContinuePackingAfterGeneratingNuspec = false 的封裝不應失敗- [#9786](https://github.com/NuGet/Home/issues/9786)

* 封裝管理員 UI：圖示未正確地反轉色彩- [#10017](https://github.com/NuGet/Home/issues/10017)

* 在還原時，最新和 No-Op 專案的專案計數不正確- [#10026](https://github.com/NuGet/Home/issues/10026)

* 使用 `/p:RestoreUseStaticGraphEvaluation=true` 值的結果不可以是 Null- [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` 錯誤地使用 WPF 程式庫專案的別名- [#10020](https://github.com/NuGet/Home/issues/10020)

* 封裝管理員 UI：簽章驗證失敗時的 NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces：不使用 `object` 類型的專案中繼資料值- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces：在 [工具選項] 中儲存套件來源將會覆寫認證- [#9711](https://github.com/NuGet/Home/issues/9711)


**[此版本修正的所有問題清單-5。8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[在此版本中修正的問題/認可清單-5。8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>社群投稿

感謝所有協助讓此 NuGet 版本絕佳的參與者！

|人員|Pr|問題|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | 錯誤訊息中的錯誤訊息。 "系統管理員身分" 而不是 "administrator"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | 具有無效 AssemblyInformationalVersion 報告的 NuGet 套件「需要描述」- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` 不會考慮分支和認可屬性- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | 若要在 Visual Studio 錯誤清單視窗中按一下 [NU 程式碼]，請移至 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | 透過 Visual Studio 選項新增套件來源時，請使用 ' HTTPs://'- [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` Mono 的效能問題- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | 新增 SemanticVersion 類別的 TypeConverter- [#9125](https://github.com/NuGet/Home/issues/9125)


## <a name="feedback-welcome"></a>歡迎意見反應

您的意見反應對我們非常寶貴。  如果此版本有任何問題，請查看我們的 [GitHub 問題](https://github.com/NuGet/Home/issues) ，並 [Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/) 現有的問題。  針對 NuGet 內的新問題，請報告 [GitHub 問題](hhttps://github.com/NuGet/Home/issues/new)。
如需一般的 NuGet 體驗問題，請透過 [說明] 下您最愛的 IDE 中的 [回報 [問題](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ] 選項，讓我們知道 **> 報告問題** 。
