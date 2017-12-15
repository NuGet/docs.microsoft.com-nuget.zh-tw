---
title: "NuGet 3.5 Beta 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 082a96b9-607b-4225-864d-e1cea537f591
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.5 版本資訊。"
keywords: "NuGet 3.5 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0a0f039d2529e1d41bbc0c7f9ac3f76f51f96ce5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
#<a name="nuget-35-release-notes"></a>NuGet 3.5 版本資訊

[NuGet 3.5 RC 版本資訊](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 版本資訊](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Bug 修正

* 組件不會使用 MSBuild 14.1 上 mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* 更新索引標籤不會選取最新可用版本，來更新改為選取目前安裝的版本- [#3498](https://github.com/NuGet/Home/issues/3498)

* 驗證摘要的 MyGet 私用 v2 後按一下 [顯示更多結果 x] 中修正損毀- [#3469](https://github.com/NuGet/Home/issues/3469)

* 記錄檔訊息看起來是反向順序 ui- [#3446](https://github.com/NuGet/Home/issues/3446)

* v3.4.4-Nuget 還原就會擲回 「 不支援指定的路徑格式 」- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta 就不會接受-p o p Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* 在大型專案-安裝 Nuget IKVM 緩慢[#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe 本身會保留在更新本身的更新[#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 安裝/還原從 UNC 共用具有 3.4.4-迴歸效能[#3355](https://github.com/NuGet/Home/issues/3355)

* 從封裝管理 UI net451 專案-安裝 Moq 時的錯誤[#3349](https://github.com/NuGet/Home/issues/3349)

* 安裝在解決方案層級的索引標籤不會顯示封裝的版本- [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj`project.json`更新從已安裝 索引標籤將會遺失狀態- [#3303](https://github.com/NuGet/Home/issues/3303)

* 在 NuGet 套件`.csproj`會忽略空的檔案中的項目`.nuspec`檔案- [#3257](https://github.com/NuGet/Home/issues/3257)

* 在 IIS 中裝載的網站專案不會導致還原失敗- [#3235](https://github.com/NuGet/Home/issues/3235)

* 認證不時，從擷取 Nuget.Config v3 端點重新導向至 v2- [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet 套件無法解析組件時擷取可攜式的組件中繼資料- [#3128](https://github.com/NuGet/Home/issues/3128)

* 找不到 Nuget`msbuild.exe`上 Mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe 組件不允許開頭數字集的發行前版本標記[# 1743年](https://github.com/NuGet/Home/issues/1743)

* nuget 套件安裝失敗上 VS2015E- [# 1298年](https://github.com/NuGet/Home/issues/1298)

* allowedVersions 篩選不在方案層級的工作[#333](https://github.com/NuGet/Home/issues/333)

* 還原隨機失敗與具有相同的項目已加入索引鍵。 - [#2646](https://github.com/NuGet/Home/issues/2646)

* 無法安裝在 Nuget.Common `.csproj`  -  [# 2635年](https://github.com/NuGet/Home/issues/2635)

* FindPackagesById 時您可以使用 UI 來搜尋 V2 來源，會呼叫兩次的每個識別碼- [# 2517年](https://github.com/NuGet/Home/issues/2517)

* 封裝不能相依於專案- [# 2490年](https://github.com/NuGet/Home/issues/2490)

* nuget.exe 套件-排除適記載，但不是支援- [# 2284年](https://github.com/NuGet/Home/issues/2284)

* 問題的錯誤訊息 'contentFiles' 區段`.nuspec`無效- [# 1686年](https://github.com/NuGet/Home/issues/1686)

* 推入一律會傳送整個封裝兩次與已驗證的封裝來源- [# 1501年](https://github.com/NuGet/Home/issues/1501)

* 沒有資訊時呼叫 nuget.exe 更新 *.csproj 專案時沒有指定`packages.config`  -  [# 1496年](https://github.com/NuGet/Home/issues/1496)

* `packages.config`還原不會重試在來源 V2-5xx 狀態碼[# 1217年](https://github.com/NuGet/Home/issues/1217)

* 在檔案中的 src 雙點`.nuspec`無法運作- [# 2947年](https://github.com/NuGet/Home/issues/2947)

* CoreCLR 還原需要略過使用加密-摘要[# 2942年](https://github.com/NuGet/Home/issues/2942)

* nuget.exe 推送 403 處理-錯誤提示輸入認證- [# 2910年](https://github.com/NuGet/Home/issues/2910)

* NuGet 更新程式，透過封裝管理員會從內容`project.json`  -  [# 2888年](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio 嘗試載入"NuGet.TeamFoundationServer14"，但是的 DLL 名稱變更為"NuGet.TeamFoundationServer"- [# 2857年](https://github.com/NuGet/Home/issues/2857)

* 封裝管理員 UI 不會顯示新的更新版本- [# 2828年](https://github.com/NuGet/Home/issues/2828)

* 更新封裝嘗試使用 packageid，而不是 package.version-版本[# 2771年](https://github.com/NuGet/Home/issues/2771)

* 如果專案不使用 nuget，nuget 還原 csproj 應該錯誤 (`packages.config`或`project.json`)- [# 2766年](https://github.com/NuGet/Home/issues/2766)

* TFS 錯誤 「 [檔案] 會在您的工作區中找不到，或您沒有存取權限 」 期間升級或解除安裝方案/專案繫結至 TFS 原始檔控制-時[# 2739年](https://github.com/NuGet/Home/issues/2739)

* 更新套件不會取得非目標的封裝的相依性[# 2724年](https://github.com/NuGet/Home/issues/2724)

* 沒有任何方法來設定記錄檔詳細等級 Nuget 封裝管理員 UI 動作- [# 2705年](https://github.com/NuGet/Home/issues/2705)

* nuget 組態無效-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)

* 在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 無法運作- [# 2653年](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 版本取得值不可為 null 上封裝組建- [# 2648年](https://github.com/NuGet/Home/issues/2648)

* 還原並未使用來自 Nuget.Config 預存的認證的 VSTS 摘要- [# 2647年](https://github.com/NuGet/Home/issues/2647)

* [dotnet 還原]-configfile 是相對於專案目錄，而不是 cmd dir- [# 2639年](https://github.com/NuGet/Home/issues/2639)

* 版本 comparsion 碼-過度配置[# 2632年](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe 嘗試安裝相同的多個執行個體的封裝將平行會導致重複的寫入- [# 2628年](https://github.com/NuGet/Home/issues/2628)

* 相依性資訊不會快取的多重專案作業- [# 2619年](https://github.com/NuGet/Home/issues/2619)

* 安裝及更新下載的封裝，而不先檢查 [packages] 資料夾[# 2618年](https://github.com/NuGet/Home/issues/2618)

* 如果套件來源清單是空的無法新增套件來源透過 UI (NuGet 3.4.x)- [# 2617年](https://github.com/NuGet/Home/issues/2617)

* 誤導錯誤時嘗試安裝封裝相依於設計階段外貌- [# 2594年](https://github.com/NuGet/Home/issues/2594)

* 設定"All"PackageManager 主控台從安裝封裝會嘗試第一個來源- [# 2557年](https://github.com/NuGet/Home/issues/2557)

* 無法解壓縮的最新 beta ModernHttpClient- [# 2518年](https://github.com/NuGet/Home/issues/2518)

* 在具有內建自我 NuGet 3.4.1-啟動 VS2015 損毀[# 2419年](https://github.com/NuGet/Home/issues/2419)

* 更新命令可能是一個位元更多詳細資料如果 i 要求它能所以...- [# 2418年](https://github.com/NuGet/Home/issues/2418)

* 在本機上建立 VSIX 應該 CI 組建與具有相同的 Dll 和檔案。 - [#2401](https://github.com/NuGet/Home/issues/2401)

* 組建-中修正 NuGet 降級警告[# 2396年](https://github.com/NuGet/Home/issues/2396)

* 無法驗證封裝來源 （3 次） 會永久-封鎖[# 2362年](https://github.com/NuGet/Home/issues/2362)

* 從 nuget v3.3 + 安裝的套件摘要與引數時未正確地還原套件內容-NoCache 當封裝包含`.nupkg`檔案- [# 2354年](https://github.com/NuGet/Home/issues/2354)

* 所有的封裝來源，但遺漏了 1 個來源，封裝 Nuget 安裝失敗- [# 2322年](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson]UIDelay: nuget.packagemanagement.visualstudio.dll ！NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt;&gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext- [# 2285年](https://github.com/NuGet/Home/issues/2285)

* 如果單一來源授權-就會失敗，請安裝區塊[# 2034年](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`版本範圍應該覆寫-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)

* 更新套件 super 緩慢-「 嘗試收集相依性資訊 」- [# 1909年](https://github.com/NuGet/Home/issues/1909)

* NuGet 的鏃形降級封裝時批次更新其相依性- [# 1903年](https://github.com/NuGet/Home/issues/1903)

* 此組件強式名稱和私用屬性，會卸除 nuget.exe 更新。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 相對檔案路徑的"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)

* 改善解析程式失敗的訊息- [# 1373年](https://github.com/NuGet/Home/issues/1373)

* v3 封裝失敗並不在指定的來源封裝[# 1013年](https://github.com/NuGet/Home/issues/1013)

* 封裝來源中使用相對路徑會有問題，才能使用[#865](https://github.com/NuGet/Home/issues/865)

* 遺漏 NUPKG 檔如果間接相依性已經存在具有較低的版本需求-產生從專案中的相依性[#759](https://github.com/NuGet/Home/issues/759)

* 刪除專案關閉對應的 UI 視窗中，但重新命名專案並不會重新命名 UI 視窗。 請注意 PMC 接聽重新命名專案和專案移除事件- [#670](https://github.com/NuGet/Home/issues/670)

* [柳樹 Web 工作負載]建立 Razor v3 WSP 懸置- [#3241](https://github.com/NuGet/Home/issues/3241)

* 特定封裝安裝/還原失敗的 「 封裝包含多個 nuspec 檔案。 」 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 小寫識別碼 （& s)`packages.config`案例- [#3209](https://github.com/NuGet/Home/issues/3209)

* [beta2 前 3.5]封裝還原失敗時還原 「 舊版 」 封裝- [#3208](https://github.com/NuGet/Home/issues/3208)

* nuget 套件強制將.tt 檔案加入至內容的資料夾，不論什麼- [#3203](https://github.com/NuGet/Home/issues/3203)

* 更新套件的 ASP.NET web 應用程式會產生與檔案相關的警告： 來源- [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget 套件 csproj (與`project.json`) 損毀，如果有任何 packOptions 和擁有者，在 JSON 檔案- [#3180](https://github.com/NuGet/Home/issues/3180)

* nuget 套件`project.json`會忽略摘要、 作者、 等位的擁有者等 packOptions 標記[#3161](https://github.com/NuGet/Home/issues/3161)

* 透過 NuGet.Packaging.PhysicalPackageFile.GetStream-NullReferenceException [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet 套件會忽略輸出中的相依性`.nuspec`如`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 使用回復更新多個封裝保持專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard 專案-不會新增任何 ContentFiles [#3118](https://github.com/NuGet/Home/issues/3118)

* 無法封裝以.Net 為目標的程式庫標準正確[#3108](https://github.com/NuGet/Home/issues/3108)

* 檔案]-> [新增專案]-> [類別庫 （可攜式） 專案失敗 VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 錯誤-1.0.0-* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)

* 尋找套件無法顯示，但是 Install-package works- [#3068](https://github.com/NuGet/Home/issues/3068)

* 錯誤時 dev15 層上的 「 安裝套件 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* nuget 套件的 xproj 會預設為無效的目標路徑- [#3060](https://github.com/NuGet/Home/issues/3060)

* 當已安裝的 VS 2015 更新 3 上使用的 NuGet 版本 3.5.0 錯誤，就會發生-VS [#3053](https://github.com/NuGet/Home/issues/3053)

* 「 被封鎖的 packages.config 」 `project.json` (UWP，又稱為組建整合) 專案- [#3046](https://github.com/NuGet/Home/issues/3046)

* 更新 dotnet cli 安裝 preview2-003121，這是官方 preview2 組建的組建指令碼。 - [#3045](https://github.com/NuGet/Home/issues/3045)

* 封裝管理員 UI： 更新封裝之後，不會顯示新的版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey delete 命令列上不會讀取/傳送中 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正確的字串： 一個穩定的套件版本不應該在發行前版本相依性。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage 快取中留下空資料夾- [#3029](https://github.com/NuGet/Home/issues/3029)

* 建立 （net46 和 windows 10） 的 PCL 專案 get NullRef 例外狀況。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget 更新應該提供具有資訊價值訊息時更高的版本受到 allowedVersions 條件約束- [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 還原問題- [# 2891年](https://github.com/NuGet/Home/issues/2891)

* 認證外掛程式已結束，錯誤碼為-1 / 錯誤下載封裝使用多個來源的認證提供者時[# 2885年](https://github.com/NuGet/Home/issues/2885)

* `project.json`nuget 還原會造成重新編譯時不變更- [# 2817年](https://github.com/NuGet/Home/issues/2817)

* 符號套件永遠不能用於安裝或更新- [# 2807年](https://github.com/NuGet/Home/issues/2807)

* VS 不支援環境變數中 repositoryPath （nuget.exe 運作）- [# 2763年](https://github.com/NuGet/Home/issues/2763)

* 標示未加上標籤的 Uielement 封裝管理員 UI 中的協助工具： [# 2745年](https://github.com/NuGet/Home/issues/2745)

* 可攜式架構來使用連字號連接的設定檔會遭到拒絕。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 封裝管理員可以讓您清楚該詳細不適用於封裝中的選項清單`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)

* nuget.exe 推送/刪除不會使用 API 金鑰- [# 2627年](https://github.com/NuGet/Home/issues/2627)

* 鎖定的屬性移除鎖定檔案- [# 2379年](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 更新無法使用 '...額外的條件約束中定義 packages.config 阻止了此作業。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 假的訊息-不存在則會擲回的本機來源從安裝封裝[# 1674年](https://github.com/NuGet/Home/issues/1674)

* [可升級] 篩選條件會顯示升級違反版本條件約束- [# 1094年](https://github.com/NuGet/Home/issues/1094)

* 無法更新原生封裝- [# 1291年](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>功能

* 支援為 false 的設定 CopyLocal 參考加入 nuget- [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15-nuget.exe 支援[# 1937年](https://github.com/NuGet/Home/issues/1937)

* 組件支援。`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 正在執行的使用者動作時，停用使用者動作- [# 1440年](https://github.com/NuGet/Home/issues/1440)

* NuGet 應該加入支援`runtimes/{rid}/nativeassets/{txm}/`  -  [# 2782年](https://github.com/NuGet/Home/issues/2782)

* 加入遺漏的 NuGet 中的架構相容性 （也就是已在 3.x） 2.x- [# 2720年](https://github.com/NuGet/Home/issues/2720)

* 支援後援封裝資料夾- [# 2899年](https://github.com/NuGet/Home/issues/2899)

* 設計和實作封裝類型的概念，以支援工具套件- [# 2476年](https://github.com/NuGet/Home/issues/2476)

* 新增 API 來取得全域套件資料夾的路徑[# 2403年](https://github.com/NuGet/Home/issues/2403)

* 啟用在組件-SemVer 2.0.0 [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Dcr

* nuget.exe 推送的逾時參數無法運作- [# 2785年](https://github.com/NuGet/Home/issues/2785)

* 封裝描述文字應該是可選取- [# 1769年](https://github.com/NuGet/Home/issues/1769)

* 啟用產生 nuget.exe`.props`和`.targets`檔案`.nuproj`專案[# 2711年](https://github.com/NuGet/Home/issues/2711)

* 加入擴充性 API 來比較架構來使用匯入- [# 2633年](https://github.com/NuGet/Home/issues/2633)

* 隱藏相依性的選項，當使用`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)

* 列印出 nuget.exe 版本標頭中詳細的輸出- [# 1887年](https://github.com/NuGet/Home/issues/1887)

* 若要讓使用者知道，在基礎 dotnet tfm 升級/安裝 PCL 可能會導致問題-需要 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* 警告錯誤安裝/升級專案以 tfm ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* NuGet ReShaper 與修正效能問題的更新- [#3044](https://github.com/NuGet/Home/issues/3044)

* 新增 netcoreapp11 和 netstandard17 支援- [# 2998年](https://github.com/NuGet/Home/issues/2998)

* 運用 AssemblyMetadata 屬性`.nuspec`語彙基元取代- [# 2851年](https://github.com/NuGet/Home/issues/2851)
