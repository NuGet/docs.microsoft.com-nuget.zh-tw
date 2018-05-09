---
title: 3.5 RC 版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.5 RC 版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d620a8b8d97f9a52cb2bc93a91eb393130a42898
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC 版本資訊

[NuGet 3.5 Beta2 前版本資訊](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM 版本資訊](../release-notes/nuget-3.5-RTM.md)

3.5 版本著重於改善品質及效能的 NuGet 用戶端。 此外，我們已寄出一些功能，例如支援[後援資料夾](https://github.com/NuGet/Home/issues/2899)， [PackageType](https://github.com/NuGet/Home/issues/2476)支援`.nuspec`等等。

[問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Bug 修正

* 封裝安裝/還原失敗的 「 封裝包含多個`.nuspec`檔案。 」 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 強制將 nuget 套件加入`.tt`檔案解壓縮至內容的資料夾，不論什麼- [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget 套件 csproj (與`project.json`) 損毀，如果有任何 packOptions 和擁有者，在 JSON 檔案- [#3180](https://github.com/NuGet/Home/issues/3180)

* nuget 套件`project.json`會忽略摘要、 作者、 等位的擁有者等 packOptions 標記[#3161](https://github.com/NuGet/Home/issues/3161)

* nuget 套件會忽略輸出中的相依性`.nuspec`如`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 使用回復更新多個封裝保持專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard 專案-不會新增任何 ContentFiles [#3118](https://github.com/NuGet/Home/issues/3118)

* 無法封裝以.Net 為目標的程式庫標準正確[#3108](https://github.com/NuGet/Home/issues/3108)

* 檔案]-> [新增專案]-> [類別庫 （可攜式） 專案失敗 VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 錯誤-1.0.0-* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)

* 尋找套件無法顯示，但是 Install-package works- [#3068](https://github.com/NuGet/Home/issues/3068)

* 錯誤時 dev15 層上的 「 安裝套件 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* 當已安裝的 VS 2015 更新 3 上使用的 NuGet 版本 3.5.0 錯誤，就會發生-VS [#3053](https://github.com/NuGet/Home/issues/3053)

* 封裝管理員 UI： 更新封裝之後，不會顯示新的版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey delete 命令列上不會讀取/傳送中 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正確的字串： 一個穩定的套件版本不應該在發行前版本相依性。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* 建立 （net46 和 windows 10） 的 PCL 專案 get NullRef 例外狀況。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget 更新應該提供具有資訊價值訊息時更高的版本受到 allowedVersions 條件約束- [#3013](https://github.com/NuGet/Home/issues/3013)

* 認證外掛程式已結束，錯誤碼為-1 / 錯誤下載封裝使用多個來源的認證提供者時[# 2885年](https://github.com/NuGet/Home/issues/2885)

* nuget 套件遺漏 Newtonsoft.Json 封裝相依性- [# 2876年](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + Mono-ExecuteSynchronizedCore 中的 bug [# 2860年](https://github.com/NuGet/Home/issues/2860)

* VS 不支援環境變數中 repositoryPath （nuget.exe 運作）- [# 2763年](https://github.com/NuGet/Home/issues/2763)

* 修正存取問題- [# 2745年](https://github.com/NuGet/Home/issues/2745)

* 可攜式架構來使用連字號連接的設定檔會遭到拒絕。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 封裝管理員可以讓您清楚該詳細不適用於封裝中的選項清單`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新無法使用 '...額外的條件約束中定義 packages.config 阻止了此作業。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 假的訊息-不存在則會擲回的本機來源從安裝封裝[# 1674年](https://github.com/NuGet/Home/issues/1674)

* 「 可用的升級 」 篩選條件會顯示升級違反版本條件約束- [# 1094年](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>效能改善

* 效能： 改善 ContentModel 目標 framework 剖析- [#3162](https://github.com/NuGet/Home/issues/3162)

* 效能： 避免讀取`runtime.json`檔案的還原作業沒有 Rid [#3150](https://github.com/NuGet/Home/issues/3150)。 CI 在電腦上，還原的範例，透過 15 秒至 3 秒降低的 ASP.NET Web 應用程式。

* 效能： Package Manager Console init.ps1 載入時間[# 2956年](https://github.com/NuGet/Home/issues/2956)。 若要開啟 PackageManagerConsole 時間改善 10s 132s年從某些情況。

* 解決 NuGet 更新-ReSharper 效能問題[#3044](https://github.com/NuGet/Home/issues/3044)： 範例專案，安裝套件時所花費的時間用來減少從 140s年 68s。

## <a name="dcrs"></a>DCR

* 若要讓使用者知道，在基礎 dotnet tfm 升級/安裝 PCL 可能會導致問題-需要 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* 警告錯誤安裝/升級專案以 tfm ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 新增 netcoreapp11 和 netstandard17 支援- [# 2998年](https://github.com/NuGet/Home/issues/2998)

* 列印到主控台中 nuget.exe-NuGet 警告標頭內容[# 2934年](https://github.com/NuGet/Home/issues/2934)

* 運用 AssemblyMetadata 屬性`.nuspec`語彙基元取代- [# 2851年](https://github.com/NuGet/Home/issues/2851)

* 鎖定的屬性移除鎖定檔案- [# 2379年](https://github.com/NuGet/Home/issues/2379)

* 符號套件不應曾經用於安裝或更新 #2807

## <a name="features"></a>功能

* 支援後援封裝資料夾- [# 2899年](https://github.com/NuGet/Home/issues/2899)

* 設計和實作封裝類型的概念，以支援工具套件- [# 2476年](https://github.com/NuGet/Home/issues/2476)

* API 來取得全域套件資料夾的路徑[# 2403年](https://github.com/NuGet/Home/issues/2403)

* 原生封裝更新支援- [# 1291年](https://github.com/NuGet/Home/issues/1291)
