---
title: NuGet 3.5 RTM 版本資訊
description: NuGet 3.5 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776354"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 版本資訊

[NuGet 3.5-RC 版本](../release-notes/nuget-3.5-RC.md)  |  資訊[NuGet 4.0 RC 版本](../release-notes/nuget-4.0-RC.md)資訊

## <a name="bug-fixes"></a>Bug 修正

* 套件未在 mono 上使用 MSBuild 14.1- [#3550](https://github.com/NuGet/Home/issues/3550)

* [更新] 索引標籤未選取要更新的最新可用版本，改為選取 [目前安裝的版本- [#3498](https://github.com/NuGet/Home/issues/3498)

* 修正驗證私用 v2 MyGet 摘要之後的損毀，並按一下 [顯示更多結果]- [#3469](https://github.com/NuGet/Home/issues/3469)

* [#3446](https://github.com/NuGet/Home/issues/3446) UI 的記錄訊息看似反向順序

* v 3.4.4-Nuget 還原會擲回「不支援指定路徑的格式」- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 搶鮮版（Beta）不接受-a-a Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* IKVM 大型專案的 Nuget 慢安裝- [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe 更新-自行持續更新- [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 從 UNC 共用安裝/還原具有從 3.4.4 [#3355](https://github.com/NuGet/Home/issues/3355)的效能回歸

* 從 net451 專案的封裝管理 UI 安裝 Moq 時發生錯誤- [#3349](https://github.com/NuGet/Home/issues/3349)

* 解決方案層級的 [安裝] 索引標籤不會顯示套件的版本 [#3339](https://github.com/NuGet/Home/issues/3339)

* 從 [已安裝] 索引標籤的 [xproj `project.json` 更新] 失去狀態- [#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet 套件 on 會 `.csproj` 忽略檔案 `.nuspec` - [#3257](https://github.com/NuGet/Home/issues/3257)中的空檔案元素

* 裝載在 IIS 中的網站專案不應導致還原失敗 [#3235](https://github.com/NuGet/Home/issues/3235)

* V3 端點重新導向至 v2- [#3179](https://github.com/NuGet/Home/issues/3179)時，不會從 Nuget.Config 取出認證

* NuGet 套件在抓取可移植元件中繼資料時無法解析元件- [#3128](https://github.com/NuGet/Home/issues/3128)

* 在 Mono 上找不到 Nuget `msbuild.exe` - [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe 套件不允許以數位開頭的發行前標記- [#1743](https://github.com/NuGet/Home/issues/1743)

* 在 VS2015E 上安裝 nuget 套件失敗- [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions 篩選無法在解決方案層級運作- [#333](https://github.com/NuGet/Home/issues/333)

* 因為已新增具有相同索引鍵的專案，所以隨機還原失敗。 - [#2646](https://github.com/NuGet/Home/issues/2646)

* 無法安裝 Nuget。 `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)中常見

* 使用 UI 來搜尋 V2 來源時，會針對每個識別碼呼叫 FindPackagesById 兩次- [#2517](https://github.com/NuGet/Home/issues/2517)

* 套件無法相依于專案- [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe 套件-排除已記載但不受支援- [#2284](https://github.com/NuGet/Home/issues/2284)

* 當的 ' contentFiles ' 區段無效時，出現錯誤訊息的問題 `.nuspec` - [#1686](https://github.com/NuGet/Home/issues/1686)

* 推送一律會使用已驗證的套件來源傳送整個套件兩次- [#1501](https://github.com/NuGet/Home/issues/1501)

* 當專案沒有 #1496 時，在呼叫 nuget.exe update * .csproj 時未提供任何資訊。 `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)

* `packages.config` restore 不會重試來自 V2 來源的5xx 狀態碼- [#1217](https://github.com/NuGet/Home/issues/1217)

* File src 中的雙點 `.nuspec` 無法運作- [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR restore 需要使用加密來忽略摘要- [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe 推送403處理-錯誤地提示輸入認證- [#2910](https://github.com/NuGet/Home/issues/2910)

* 透過套件管理員的 NuGet 更新會移除 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)的屬性

* VisualStudio 嘗試載入 "Nuget.exe. TeamFoundationServer14"，但該 DLL 名稱變更為 "TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)

* 套件管理員 UI 未顯示新更新的版本- [#2828](https://github.com/NuGet/Home/issues/2828)

* 更新套件嘗試使用 packageid、版本而非套件。版本- [#2771](https://github.com/NuGet/Home/issues/2771)

* 如果專案未使用 nuget (`packages.config` 或 `project.json`) [#2766](https://github.com/NuGet/Home/issues/2766) ，nuget restore .csproj 應該會發生錯誤

* 在您的工作區中找不到 TFS 錯誤 "[file]，或您沒有許可權可在方案/專案系結至 TFS 原始檔控制時，于升級或卸載期間進行存取- [#2739](https://github.com/NuGet/Home/issues/2739)

* 更新套件不會取得非目標套件的相依性- [#2724](https://github.com/NuGet/Home/issues/2724)

* 沒有任何方法可以設定 Nuget 套件管理員 UI 動作的記錄詳細資訊層級- [#2705](https://github.com/NuGet/Home/issues/2705)

* nuget 設定無效-VS 2015 VSIX (v 3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* `NuGetDefaults.Config` () 中 `ProgramData\NuGet` 的 DefaultPushSource 無法運作- [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 在套件組建上的版本取得值不可以是 null- [#2648](https://github.com/NuGet/Home/issues/2648)

* 還原未使用來自 Nuget.Config 的 VSTS 摘要預存認證- [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--get-help 相對於專案目錄，而非 cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)

* 版本比較程式碼中的過度配置- [#2632](https://github.com/NuGet/Home/issues/2632)

* nuget.exe 嘗試以平行方式安裝相同封裝的多個實例會導致雙重寫入 [#2628](https://github.com/NuGet/Home/issues/2628)

* 不會快取多專案作業的相依性資訊- [#2619](https://github.com/NuGet/Home/issues/2619)

* 安裝並更新下載套件，而不需先檢查套件資料夾 [#2618](https://github.com/NuGet/Home/issues/2618)

* 如果 [套件來源] 清單是空的，則無法透過 UI 新增套件來源 (NuGet 3.4. x) - [#2617](https://github.com/NuGet/Home/issues/2617)

* 嘗試安裝相依于設計階段 facade 的封裝時發生誤導錯誤- [#2594](https://github.com/NuGet/Home/issues/2594)

* 從 >packagemanager 主控台安裝具有「全部」設定的封裝，只會嘗試第一個來源 [#2557](https://github.com/NuGet/Home/issues/2557)

* 最新 Beta 未解壓縮 ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* 在啟動時使用自行建立的 NuGet 3.4.1 VS2015 損毀- [#2419](https://github.com/NuGet/Home/issues/2419)

* 如果我要求，Update 命令可能有點詳細資訊 ...- [#2418](https://github.com/NuGet/Home/issues/2418)

* 在本機建立的 VSIX 應該與 CI 組建具有相同的 Dll 和檔案。 - [#2401](https://github.com/NuGet/Home/issues/2401)

* 修正組建- [#2396](https://github.com/NuGet/Home/issues/2396)中的 NuGet 降級警告

* 無法驗證套件來源 (3 次) 將永遠封鎖 [#2362](https://github.com/NuGet/Home/issues/2362)

* 當套件包含檔案時，從 nuget v1.0 + 摘要安裝套件時，無法正確還原套件內容 `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354) -NoCache

* 使用所有套件來源安裝 Nuget，但從1來源遺失套件，失敗- [#2322](https://github.com/NuGet/Home/issues/2322)

* PerfWatsonUIDelay： nuget.packagemanagement.visualstudio.dll！Nuget.exe. VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt;c__DisplayClass_0 + &lt; &lt; AddReference &gt; b__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* 如果單一來源失敗授權，請安裝區塊- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本範圍應覆寫-IncludeReferencedProjects 版本- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package 超級緩慢-「嘗試收集相依性資訊」- [#1909](https://github.com/NuGet/Home/issues/1909)

* 當批次更新其相依性時，NuGet 隱形降級套件- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe 更新會卸載元件強式名稱和私用屬性。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource" 的相對檔案路徑- [#1746](https://github.com/NuGet/Home/issues/1746)

* 改善解析程式失敗訊息- [#1373](https://github.com/NuGet/Home/issues/1373)

* v3 中的更新套件失敗，套件不在指定的來源中- [#1013](https://github.com/NuGet/Home/issues/1013)

* 使用套件來源的相對路徑對使用有問題- [#865](https://github.com/NuGet/Home/issues/865)

* 缺少 NUPKG 中的相依性-如果間接相依性已存在，且版本需求較低，則會從專案產生： [#759](https://github.com/NuGet/Home/issues/759)

* 刪除專案會關閉對應的 UI 視窗，但是重新命名專案並不會重新命名 UI 視窗。 請注意，PMC 會接聽專案重新命名和專案移除事件- [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web 工作負載]建立 Razor v3 WSP 停止回應- [#3241](https://github.com/NuGet/Home/issues/3241)

* 特定套件的安裝/還原失敗，並出現「封裝包含多個 nuspec 檔案」。 - [#3231](https://github.com/NuGet/Home/issues/3231)

* 小寫識別碼 & `packages.config` 案例- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-Beta2]封裝還原無法還原「舊版」套件- [#3208](https://github.com/NuGet/Home/issues/3208)

* 無論什麼[#3203](https://github.com/NuGet/Home/issues/3203) ，nuget 套件都會強制將 tt 檔新增至內容資料夾

* ASP.NET web 應用程式的更新套件會產生與檔案相關的警告：來源- [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget 套件 .csproj (`project.json` 如果沒有 JSON 檔案中的 packOptions 和擁有者，) 會當機- [#3180](https://github.com/NuGet/Home/issues/3180)

* 的 nuget 套件會 `project.json` 忽略 packOptions 標記，例如摘要、作者、擁有者等 [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet 套件會忽略 #3145 輸出 `.nuspec` 的 `project.json`  -  [](https://github.com/NuGet/Home/issues/3145)相依性

* 使用 rollback 更新多個封裝會讓專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)

* 未針對 netstandard 專案新增任何的 ContentFiles- [#3118](https://github.com/NuGet/Home/issues/3118)

* 無法正確封裝以 .Net Standard 為目標的程式庫- [#3108](https://github.com/NuGet/Home/issues/3108)

* 檔案-> 新專案 > 類別庫 (便攜) 專案在 VS2015 和 Dev15 中失敗- [#3094](https://github.com/NuGet/Home/issues/3094)

* nuGet 錯誤-1.0.0-* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package 無法顯示，但 Install-Package 運作- [#3068](https://github.com/NuGet/Home/issues/3068)

* 在 dev15 上「安裝套件 jquery. 驗證」時發生錯誤- [#3061](https://github.com/NuGet/Home/issues/3061)

* xproj 的 nuget 套件預設為不正確目標路徑- [#3060](https://github.com/NuGet/Home/issues/3060)

* 在使用 NuGet 版本3.5.0 的 VS 上安裝 VS 2015 update 3 時發生錯誤- [#3053](https://github.com/NuGet/Home/issues/3053)

*  (UWP 中的「封鎖者」 packages.config」，也就 `project.json` 是整合) 專案的組建- [#3046](https://github.com/NuGet/Home/issues/3046)

* 將組建腳本所安裝的 dotnet cli 更新為 preview2-003121，也就是官方 preview2 組建。 - [#3045](https://github.com/NuGet/Home/issues/3045)

* 套件管理員 UI：更新封裝之後不會顯示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -在3.5.0 中不會讀取/傳送 ApiKey on delete 命令列-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正確的字串：套件的穩定版本不應具有發行前版本的相依性。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage 快取會保留空的資料夾- [#3029](https://github.com/NuGet/Home/issues/3029)

* 建立 PCL (net46 和 windows 10) project get NullRef 例外狀況。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* 當較高的版本受限於 allowedVersions 條件約束時，Nuget 更新應提供資訊性訊息 [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 還原問題- [#2891](https://github.com/NuGet/Home/issues/2891)

* 認證外掛程式結束，發生錯誤-1/在使用具有多個來源的認證提供者時下載封裝時發生錯誤- [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` 當沒有任何變更時，nuget 還原會導致重新編譯- [#2817](https://github.com/NuGet/Home/issues/2817)

* 符號套件絕不能用在安裝或更新- [#2807](https://github.com/NuGet/Home/issues/2807)

* VS 不支援 repositoryPath ( # A0) [#2763](https://github.com/NuGet/Home/issues/2763)的環境變數

* 針對協助工具將未標記的 UIElements 標示為封裝管理員 UI- [#2745](https://github.com/NuGet/Home/issues/2745)

* 具有斷字元設定檔的可移植架構會遭到拒絕。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 套件管理員應該確定套件詳細資料的選項清單不適用 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe 推送/刪除不會使用 API 金鑰- [#2627](https://github.com/NuGet/Home/issues/2627)

* 從鎖定檔案中移除鎖定的屬性- [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 更新失敗，並出現「額外的條件約束 .。。在 packages.config 中定義會防止這項作業。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 從不存在的本機來源安裝套件會擲回假訊息 [#1674](https://github.com/NuGet/Home/issues/1674)

* 「可用升級」篩選器會顯示違反版本條件約束的升級- [#1094](https://github.com/NuGet/Home/issues/1094)

* 無法更新原生封裝- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>功能

* 支援在 NuGet 新增的參考上將 CopyLocal 設定為 false- [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15 [#1937](https://github.com/NuGet/Home/issues/1937)的 nuget.exe 支援

* 的套件支援。`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 當正在執行使用者動作時停用使用者動作- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet 應該新增 `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)的支援

* 新增 NuGet 2.x 中遺失的 framework 相容性（已在2.x 中 (）) - [#2720](https://github.com/NuGet/Home/issues/2720)

* 支援 fallback 封裝資料夾- [#2899](https://github.com/NuGet/Home/issues/2899)

* 設計和執行封裝類型的概念以支援工具套件- [#2476](https://github.com/NuGet/Home/issues/2476)

* 新增 API 以取得全域套件資料夾的路徑- [#2403](https://github.com/NuGet/Home/issues/2403)

* 在 pack- [#3356](https://github.com/NuGet/Home/issues/3356)中啟用 SemVer 2.0。0

## <a name="dcrs"></a>DCR

* nuget.exe push-timeout 參數無法運作- [#2785](https://github.com/NuGet/Home/issues/2785)

* 封裝描述文字應為可選取- [#1769](https://github.com/NuGet/Home/issues/1769)

* 啟用 nuget.exe 以產生 `.props` `.targets` `.nuproj` 專案 [#2711](https://github.com/NuGet/Home/issues/2711)

* 新增擴充性 API 以使用 imports 進行比較- [#2633](https://github.com/NuGet/Home/issues/2633)

* 使用 #2486 時隱藏相依性選項 `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)

* 在詳細的輸出中列印出 nuget.exe 版本標頭- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet 必須讓使用者知道以 dotnet tfm 為基礎的 PCL 進行升級/安裝可能會造成問題- [#3138](https://github.com/NuGet/Home/issues/3138)

* 針對專案的不正確安裝/升級發出警告/tfm = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 修正 ReShaper 和 NuGet for Update 的效能問題- [#3044](https://github.com/NuGet/Home/issues/3044)

* 新增 netcoreapp11 和 netstandard17 支援- [#2998](https://github.com/NuGet/Home/issues/2998)

* 利用 AssemblyMetadata 屬性進行 `.nuspec` 權杖取代- [#2851](https://github.com/NuGet/Home/issues/2851)
