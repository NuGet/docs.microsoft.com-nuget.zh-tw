---
title: NuGet 5.5 版本資訊
description: NuGet 5.5 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780108"
---
# <a name="nuget-55-release-notes"></a>NuGet 5.5 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.5 版](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝

## <a name="summary-whats-new-in-55"></a>摘要：5.5 中的新功能

* 改善 Visual Studio 中 NuGet 套件管理員 UI 的協助工具和螢幕讀取程式體驗
    * 螢幕閱讀程式體驗中的協助工具問題，已安裝的文字方塊缺少 altText 和可存取的名稱，以及- [#9059](https://github.com/NuGet/Home/issues/9059)
    * 套件清單中螢幕閱讀程式體驗的協助工具問題- [#9077](https://github.com/NuGet/Home/issues/9077)
    * 與 [流覽]、[安裝]、[更新] 索引標籤相關的螢幕閱讀程式體驗中的協助工具問題- [#9078](https://github.com/NuGet/Home/issues/9078)
    * 朗讀程式未宣告「空白」、「沒有 Dependencies"、key org」、「MIT」連結標籤 [#9157](https://github.com/NuGet/Home/issues/9157)

* 支援在 Visual Studio 套件管理員 UI 中，為裝載于本機摘要上的套件呈現獨立的圖示- [#8189](https://github.com/NuGet/Home/issues/8189)

* 藉 `RestoreUseStaticGraphEvaluation` 由呼叫 MSBuild 靜態圖形 api 來加速評估，以大幅改善無作業還原效能- [8791](https://github.com/NuGet/Home/issues/8791)

* 使用跨平臺驗證外掛程式改善 dotnet.exe 可靠性
    * dotnet restore 失敗並出現 TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * 外掛程式：「工作已取消」-ADO 驗證的問題，原因如下。 - [#8528](https://github.com/NuGet/Home/issues/8528)

* 新增 `dotnet nuget <add|remove|update|disable|enable|list> source` 命令- [#4126](https://github.com/NuGet/Home/issues/4126)

* `--skip-duplicate`使用 dotnet nuget push [#8778](https://github.com/NuGet/Home/issues/8778)的支援

* 支援 `packages.config` msbuild/restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 使用 V3 Api 修改 Self-Updater- [#4197](https://github.com/NuGet/Home/issues/4197)

* 套件相依性版本設定為 ' * ' 時，錯誤的套件相依性版本- [#6697](https://github.com/NuGet/Home/issues/6697)

* ErrorUnsafePackageEntry 錯誤訊息未指向問題來源- [#7505](https://github.com/NuGet/Home/issues/7505)

* 「*」案例中不接受鎖定檔案- [#8073](https://github.com/NuGet/Home/issues/8073)

* 在 PackageReference 中使用 * 時，NuGet.exe 無法解析為最新版本的套件 (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)

* 具有多目標 WPF 專案的 dotnet 清單套件- [#8463](https://github.com/NuGet/Home/issues/8463)

* 改善 ConcurrencyUtilities (降低 CPU 使用量) - [#8653](https://github.com/NuGet/Home/issues/8653)

* 已卸載專案案例的 DG 規格不應以預覽還原來撰寫- [#8793](https://github.com/NuGet/Home/issues/8793)

* Visual Studio NuGet 套件 (RestoreManagerPackage) 必須在解決方案組建事件上自動載入- [#8796](https://github.com/NuGet/Home/issues/8796)

* .Vssettings init 中的鎖死- [#8842](https://github.com/NuGet/Home/issues/8842)

* 如果專案放置於方案資料夾中，則不會從 NuGet 套件填入 VisualStudio 工具箱- [#8868](https://github.com/NuGet/Home/issues/8868)

* VS：解決方案還原永久因競爭條件而失敗- [#8881](https://github.com/NuGet/Home/issues/8881)

* [已安裝] 索引標籤上的 [正在載入 ...] 常數，以及搜尋 <term>[更新] 索引標籤上的 [更新] 索引標籤 [#8890](https://github.com/NuGet/Home/issues/8890)

* 快取到期之後，VS PM UI 中缺少內嵌的圖示- [#9069](https://github.com/NuGet/Home/issues/9069)

* FireAndForget PM UI 啟動- [#9112](https://github.com/NuGet/Home/issues/9112)

* Restore： IncludeExcludeFiles. Equals ( ... ) 執行不正確- [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore： PackageSpec. Clone ( # A1 建立不相等的複製- [#9211](https://github.com/NuGet/Home/issues/9211)

* 未核取 [如果組建完成但發生錯誤時一律顯示錯誤清單]，所顯示的錯誤清單- [#8190](https://github.com/NuGet/Home/issues/8190)

* 靜態圖形還原不應傳遞空的 SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)

* 還原：每個專案4次計算的關閉次數- [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore： DependencyGraphSpec Load ( ... ) 不需要 JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* 還原：在大型物件堆積上建立的大型字串 (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)

* 新 mono 的自訂 nuget.exe 可能會因 MSBuild SDK 解析程式而中斷- [8848](https://github.com/NuGet/Home/issues/8848)

* 當 nuget.dgspec.js為「由另一個進程使用中」時，restore 會失敗- [8692](https://github.com/NuGet/Home/issues/8692)

**DCR**

* _GetRestoreProjectStyle 中的邏輯應該在工作中 [#8804](https://github.com/NuGet/Home/issues/8804)

* 預設會在 [已安裝] 索引標籤上新增取代資訊- [#8541](https://github.com/NuGet/Home/issues/8541)

**[此版本修正的所有問題清單-5。5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
