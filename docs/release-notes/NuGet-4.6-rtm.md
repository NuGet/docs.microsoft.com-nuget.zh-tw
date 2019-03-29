---
title: NuGet 4.6 RTM 版本資訊
description: NuGet 4.6.0 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432552"
---
# <a name="nuget-46-release-notes"></a>NuGet 4.6 版本資訊

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe)。

## <a name="summary-whats-new-in-460"></a>摘要: 4.6.0 中的新功能

* 新增了[簽署套件](../create-packages/sign-a-package.md)的支援。
* Visual Studio 2017 和 nuget.exe 現在會在安裝之前驗證套件的完整性，為[簽署的套件](../reference/signed-packages-reference.md)還原套件。
* 改善了後續還原的效能。

## <a name="summary-whats-new-in-463"></a>摘要: 4.6.3 中的新功能

* 安全性修正：在 ~/.nuget 內建立的檔案權限過於開放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-464"></a>摘要: 4.6.4 中的新功能

* 安全性修正：NUPKG 內的檔案可以有 NUPKG 目錄上層的相對路徑 [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>已知問題

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題 

.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。 [這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。

## <a name="top-issues-fixed-in-this-release"></a>本版修正的主要問題

**效能修正**

* 請勿在沒有任何變更時寫入資產檔案 - [#6491](https://github.com/NuGet/Home/issues/6491)
* 當子專案的 TFM 與父專案的不符時，還原會造成額外的 MSBuild 評估 - [#6311](https://github.com/NuGet/Home/issues/6311)
* 將相依性關係圖的規格建立最佳化，以改善 NoOp 還原效能 - [#6252](https://github.com/NuGet/Home/issues/6252)

**Bug**

* 推送到本機資料夾會鎖定 nupkg - [#6325](https://github.com/NuGet/Home/issues/6325)
* NuGet 外掛程式實作：多項問題 - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - 從 VSSolutionManager 的 MEF 初始化移除查詢服務呼叫 - [#6110](https://github.com/NuGet/Home/issues/6110)
* 回報取消的套件下載工作有例外狀況時發生錯誤 - [#6096](https://github.com/NuGet/Home/issues/6096)
* 在組件名稱中，NuGet.exe 會將 '+' 取代為 '%2B' - [#5956](https://github.com/NuGet/Home/issues/5956)
* 在 PM UI 和主控台，Fn + F1 不會導向正確的說明頁面 - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet 在特定情況下會將絕對路徑寫入專案檔 - [#5888](https://github.com/NuGet/Home/issues/5888)
* 修正 4.3 迴歸 - 預留位置 $product$ 和 $AssemblyGuid$ 未透過轉換在 contentfile 中取代 - [#5880](https://github.com/NuGet/Home/issues/5880)
* dotnet restore 有多次原始檔損毀 - [#5817](https://github.com/NuGet/Home/issues/5817)
* 套件應重新評估專案版本，以允許 git 版本控制 - [#4790](https://github.com/NuGet/Home/issues/4790)
* 改善了安裝不相容的套件時，難以理解的錯誤 - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard 需要選項來將套件安裝為 PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* 當 MSBuild.exe 從開發人員命令提示字元之外執行時，會略過套件傳遞的 props 檔案 - [#4530](https://github.com/NuGet/Home/issues/4530)
* 修正在參考不適用於專案的 .NET Standard 程式庫時，不良的錯誤訊息 - [#4423](https://github.com/NuGet/Home/issues/4423)
* dotnet add package 在以可攜式設定檔為目標的套件會失敗，而且顯示很少指導 - [#4349](https://github.com/NuGet/Home/issues/4349)
* ProjectReference 中缺少 dotnet pack - 版本尾碼 - [#4337](https://github.com/NuGet/Home/issues/4337)
* .NET Core 範本出現建置錯誤，而且 VS 會損毀 - [#3973](https://github.com/NuGet/Home/issues/3973)
* 無法為來源 https:* 載入服務索引 - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list -allversions 無法運作 - [#3441](https://github.com/NuGet/Home/issues/3441)
* 誤導的相依性解析錯誤訊息 - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe restore 不會為 .msbuildproj (v3.3.0-3.4.4 升級中的迴歸) 產生 .props 和 .targets 檔案 - [#2921](https://github.com/NuGet/Home/issues/2921)
* 在 XAML 檔案開啟的情況下，UI 會在更新 NuGet 套件時延遲 - [#2878](https://github.com/NuGet/Home/issues/2878)
* 來自 IIS 的 Web 專案因路徑中有不合法的字元而失敗 - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget add 在 CentOS 會停止回應 - [#2708](https://github.com/NuGet/Home/issues/2708)
* 在 json.net 使用 packagesavemode -nupkg 進行還原會失敗 - [#2706](https://github.com/NuGet/Home/issues/2706)
* 在還原命令的 VS 輸出視窗中，套件管理員篩選無法使用 - [#2704](https://github.com/NuGet/Home/issues/2704)

[本版修正的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
