---
title: 3.5 RC 版本資訊
description: NuGet 3.5 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780195"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC 版本資訊

[NuGet 3.5-Beta2 版本](../release-notes/nuget-3.5-Beta2.md)  |  資訊[NuGet 3.5-RTM 版本](../release-notes/nuget-3.5-RTM.md)資訊

3.5 版著重于改善 NuGet 用戶端的品質和效能。 此外，我們也提供了一些功能，例如支援回溯 [資料夾](https://github.com/NuGet/Home/issues/2899)、 [PackageType](https://github.com/NuGet/Home/issues/2476) 支援 `.nuspec` 等等。

[問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Bug 修正

* 套件的安裝/還原失敗，並出現「封裝包含多個檔案」 `.nuspec` 。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 無論什麼 #3203，nuget 套件都會強制將檔案新增 `.tt` 至[](https://github.com/NuGet/Home/issues/3203)內容資料夾

* nuget 套件 .csproj (`project.json` 如果沒有 JSON 檔案中的 packOptions 和擁有者，) 會當機- [#3180](https://github.com/NuGet/Home/issues/3180)

* 的 nuget 套件會 `project.json` 忽略 packOptions 標記，例如摘要、作者、擁有者等 [#3161](https://github.com/NuGet/Home/issues/3161)

* nuget 套件會忽略 #3145 輸出 `.nuspec` 的 `project.json`  -  [](https://github.com/NuGet/Home/issues/3145)相依性

* 使用 rollback 更新多個封裝會讓專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)

* 未針對 netstandard 專案新增任何的 ContentFiles- [#3118](https://github.com/NuGet/Home/issues/3118)

* 無法正確封裝以 .Net Standard 為目標的程式庫- [#3108](https://github.com/NuGet/Home/issues/3108)

* 檔案-> 新專案 > 類別庫 (便攜) 專案在 VS2015 和 Dev15 中失敗- [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 錯誤-1.0.0-* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package 無法顯示，但 Install-Package 運作- [#3068](https://github.com/NuGet/Home/issues/3068)

* 在 dev15 上「安裝套件 jquery. 驗證」時發生錯誤- [#3061](https://github.com/NuGet/Home/issues/3061)

* 在使用 NuGet 版本3.5.0 的 VS 上安裝 VS 2015 update 3 時發生錯誤- [#3053](https://github.com/NuGet/Home/issues/3053)

* 套件管理員 UI：更新封裝之後不會顯示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -在3.5.0 中不會讀取/傳送 ApiKey on delete 命令列-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正確的字串：套件的穩定版本不應具有發行前版本的相依性。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* 建立 PCL (net46 和 windows 10) project get NullRef 例外狀況。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* 當較高的版本受限於 allowedVersions 條件約束時，Nuget 更新應提供資訊性訊息 [#3013](https://github.com/NuGet/Home/issues/3013)

* 認證外掛程式結束，發生錯誤-1/在使用具有多個來源的認證提供者時下載封裝時發生錯誤- [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget 套件-套件相依性缺少 Newtonsoft.Js- [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + Mono [#2860](https://github.com/NuGet/Home/issues/2860)上的 ExecuteSynchronizedCore 錯誤

* VS 不支援 repositoryPath ( # A0) [#2763](https://github.com/NuGet/Home/issues/2763)的環境變數

* 修正協助工具問題- [#2745](https://github.com/NuGet/Home/issues/2745)

* 具有斷字元設定檔的可移植架構會遭到拒絕。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 套件管理員應該確定套件詳細資料的選項清單不適用 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新失敗，並出現「額外的條件約束 .。。在 packages.config 中定義會防止這項作業。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 從不存在的本機來源安裝套件會擲回假訊息 [#1674](https://github.com/NuGet/Home/issues/1674)

* "Upgrade v) " 篩選器會顯示違反版本條件約束的升級- [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>效能改進

* 效能：改善 ContentModel 目標 framework 剖析- [#3162](https://github.com/NuGet/Home/issues/3162)

* 效能：避免讀取沒有 `runtime.json` rid [#3150](https://github.com/NuGet/Home/issues/3150)的還原檔案。 在 CI 機器上，將範例 ASP.NET Web 應用程式的還原從超過15秒減少為3秒。

* 效能：封裝管理員主控台 init.ps1 載入時間 [#2956](https://github.com/NuGet/Home/issues/2956)。 從132s 到10s 的某些案例中，開啟 PackageManagerConsole 的時間已獲得改善。

* 解決 NuGet 更新中的 ReSharper 效能問題- [#3044](https://github.com/NuGet/Home/issues/3044)：在範例專案中，安裝套件所需的時間從140s 減少到68s。

## <a name="dcrs"></a>DCR

* NuGet 必須讓使用者知道以 dotnet tfm 為基礎的 PCL 進行升級/安裝可能會造成問題- [#3138](https://github.com/NuGet/Home/issues/3138)

* 針對專案的不正確安裝/升級發出警告/tfm = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 新增 netcoreapp11 和 netstandard17 支援- [#2998](https://github.com/NuGet/Home/issues/2998)

* 在 nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)中將 NuGet-Warning 標頭內容列印到主控台

* 利用 AssemblyMetadata 屬性進行 `.nuspec` 權杖取代- [#2851](https://github.com/NuGet/Home/issues/2851)

* 從鎖定檔案中移除鎖定的屬性- [#2379](https://github.com/NuGet/Home/issues/2379)

* 在安裝或更新時，不應該使用符號套件 #2807

## <a name="features"></a>功能

* 支援 fallback 封裝資料夾- [#2899](https://github.com/NuGet/Home/issues/2899)

* 設計和執行封裝類型的概念以支援工具套件- [#2476](https://github.com/NuGet/Home/issues/2476)

* 取得全域套件資料夾路徑的 API- [#2403](https://github.com/NuGet/Home/issues/2403)

* 原生套件更新支援- [#1291](https://github.com/NuGet/Home/issues/1291)
