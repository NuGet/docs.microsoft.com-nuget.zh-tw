---
title: 3.5 RC 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.5 RC 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548534"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC 版本資訊

[NuGet 3.5-Beta2 版本資訊](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 的 RTM 版本資訊](../release-notes/nuget-3.5-RTM.md)

3.5 版本著重於提升品質與效能的 NuGet 用戶端。 此外，我們所提供的一些功能，像是支援[後援的資料夾](https://github.com/NuGet/Home/issues/2899)， [PackageType](https://github.com/NuGet/Home/issues/2476)支援`.nuspec`和更多功能。

[問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Bug 修正

* 安裝/還原套件的失敗 」 封裝包含多個`.nuspec`檔案。 」 - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget 組件會強制加入`.tt`檔案複製到內容的資料夾，無論如何- [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget 套件 csproj (與`project.json`) 如果沒有任何 packOptions 及 JSON 檔案中的擁有者會當機[#3180](https://github.com/NuGet/Home/issues/3180)

* 適用於 nuget 套件`project.json`會忽略 packOptions 標記，例如摘要、 作者、 擁有者等- [#3161](https://github.com/NuGet/Home/issues/3161)

* nuget 套件會忽略輸出中的相依性`.nuspec`for `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 使用回復更新多個封裝離開專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)

* 任何的 ContentFiles 不會新增為 netstandard 專案- [#3118](https://github.com/NuGet/Home/issues/3118)

* 無法封裝以.Net 為目標的程式庫標準正確- [#3108](https://github.com/NuGet/Home/issues/3108)

* 檔案]-> [新增專案]-> [類別庫 （可攜式） 專案會失敗，VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 錯誤-1.0.0-* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)

* 尋找套件無法顯示，但安裝套件的運作方式- [#3068](https://github.com/NuGet/Home/issues/3068)

* 錯誤時 「 Install-package jquery.validation 」 在 dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* 當已安裝的 VS 2015 更新 3 上使用的 NuGet 3.5.0 的版本時發生錯誤，就會發生-VS [#3053](https://github.com/NuGet/Home/issues/3053)

* 套件管理員 UI： 不會顯示在更新封裝之後，新的版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* 刪除命令列上的-ApiKey 中不會讀取/傳送 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正確的字串： 上的發行前版本的相依性不應該有套件的穩定版本。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* 正在建立 PCL （net46 和 windows 10） 專案取得 NullRef 例外狀況。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget 更新應該提供的告知性訊息，當較高的版本會受到 allowedVersions 條件約束- [#3013](https://github.com/NuGet/Home/issues/3013)

* 認證外掛程式已結束，錯誤為-1 / 錯誤下載套件時使用多個來源的認證提供者[# 2885年](https://github.com/NuGet/Home/issues/2885)

* nuget 套件遺漏 Newtonsoft.Json 套件相依性- [# 2876年](https://github.com/NuGet/Home/issues/2876)

* 在 Linux/MacOS + Mono-ExecuteSynchronizedCore bug [# 2860年](https://github.com/NuGet/Home/issues/2860)

* 與不支援環境變數中 repositoryPath （nuget.exe 執行）- [# 2763年](https://github.com/NuGet/Home/issues/2763)

* 修正問題的協助工具問題- [# 2745年](https://github.com/NuGet/Home/issues/2745)

* 可移植的架構，與連字號連接的設定檔會遭到拒絕。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 套件管理員可以讓您清楚該詳細資料不適用於封裝中的 [選項] 清單`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新因 '...額外的條件約束中定義 packages.config 可避免這項作業。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 假的訊息-從本機來源不存在則會擲回安裝封裝[# 1674年](https://github.com/NuGet/Home/issues/1674)

* 「 可用的升級 」 篩選條件會顯示升級違反版本條件約束- [# 1094年](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>效能改善

* 效能： 改善 ContentModel 目標 framework 剖析- [#3162](https://github.com/NuGet/Home/issues/3162)

* 效能： 避免讀取`runtime.json`檔案的還原作業沒有 Rid [#3150](https://github.com/NuGet/Home/issues/3150)。 CI 電腦上的 ASP.NET Web 應用程式減少 15 秒到 3 的秒數可從範例中還原。

* 效能： Package Manager Console init.ps1 載入時間[# 2956年](https://github.com/NuGet/Home/issues/2956)。 在 10 秒從 132s年某些情況下，改善開啟 PackageManagerConsole 的時間。

* 解決 NuGet 更新-ReSharper 效能問題[#3044](https://github.com/NuGet/Home/issues/3044)： 範例專案，安裝套件所花費的時間用來減少從 140s年 68s。

## <a name="dcrs"></a>DCR

* NuGet 需要讓使用者知道，升級/安裝中基礎 dotnet tfm PCL 可能會造成問題- [#3138](https://github.com/NuGet/Home/issues/3138)

* 不正確安裝/升級具有 tfm 的專案，即發出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 新增 netcoreapp11 和 netstandard17 支援- [# 2998年](https://github.com/NuGet/Home/issues/2998)

* 列印到主控台中 nuget.exe-NuGet 警告標頭內容[# 2934年](https://github.com/NuGet/Home/issues/2934)

* 運用 AssemblyMetadata 屬性`.nuspec`語彙基元取代- [# 2851年](https://github.com/NuGet/Home/issues/2851)

* 已鎖定的屬性移除鎖定檔中- [# 2379年](https://github.com/NuGet/Home/issues/2379)

* 符號套件應該不曾經用於安裝或更新 #2807

## <a name="features"></a>功能

* 支援後援的套件資料夾- [# 2899年](https://github.com/NuGet/Home/issues/2899)

* 設計和實作封裝類型的概念，以支援工具套件- [# 2476年](https://github.com/NuGet/Home/issues/2476)

* API 來取得全域套件資料夾的路徑[# 2403年](https://github.com/NuGet/Home/issues/2403)

* 原生套件更新的支援- [# 1291年](https://github.com/NuGet/Home/issues/1291)
