---
title: NuGet 4.0 RC 版本資訊
description: NuGet 4.0 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547757"
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4.0 RTM 版本資訊

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附於 NuGet 4.0，後者新增 .NET Core 支援、有許多品質修正，以及改善了效能。 此版本也帶來幾項改善，像是支援 PackageReference，以及 MSBuild 目標、背景套件還原等多項 NuGet 命令。

## <a name="known-issues"></a>已知問題

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>當您有多個專案參考方案中的另一個專案時，NuGet 還原可能會失敗

#### <a name="issue"></a>問題

如果方案中的專案參考大小寫不同或相對路徑不同的專案，NuGet 還原可能無法運作。 [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>因應措施

將所有專案參考的大小寫或相對路徑修正為一致。

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>使用套件管理員主控台時，'Enter' 鍵可能無法運作

#### <a name="issue"></a>問題

有時候，Enter 鍵無法在套件管理員主控台中運作。 如果您遇到此問題，請查看本修正的進度，並針對您的重新產生步驟提供任何有用的資訊。 [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>因應措施

重新啟動 Visual Studio 並在開啟解決方案之前開啟 PMC。 或者，嘗試刪除 `project.lock.json` 並再次還原。

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>在 .NET Core 專案中，當您使用的套件包含具有無效簽章的組件時，可能會得到無限還原迴圈

#### <a name="issue"></a>問題

有時候，當您使用的套件包含具有無效簽章的組件時，或套件版本使用 'DateTime' 指示器設定時，會導致套件自動還原在無限迴圈中執行。 [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>因應措施

此問題目前沒有因應措施。

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>您無法使用 NuGet 套件管理員檢視、新增或更新 DotNetCLITools

#### <a name="issue"></a>問題

NuGet 套件管理員沒有顯示，而且不允許加入/更新 DotNetCLITools。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>因應措施

您必須在專案檔中手動編輯 DotNetCLIToolReferences。

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>當您設定專案的 PackageId 屬性時，NuGet 還原將會失敗

#### <a name="issue"></a>問題

針對 .NET Core 專案，Visual Studio 中的 NuGet 還原不遵守專案的 PackageId 屬性。 [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>因應措施

使用命令列執行還原。

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>當您的專案沒有 'obj' 資料夾時，套件還原可能會失敗

#### <a name="issue"></a>問題

當 'obj' 資料夾已刪除時，Visual Studio 無法還原 PackageReferences。 [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>因應措施

手動建立 'obj' 資料夾，應該就能執行還原。

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>在主控台中使用 Update-Package 手動更新套件可能會失敗

#### <a name="issue"></a>問題

對於剛轉換的 PackageReferences 專案，在主控台中手動使用 Update-Package 僅一次有效。 [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>因應措施

此問題目前沒有因應措施。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>重定目標 Framework 版本可能會導致不完整的 Intellisense

#### <a name="issue"></a>問題

在 Visual Studio 中重定目標 Framework 版本可能會導致不完整的 Intellisense。 當您使用 PackageReferences 作為套件管理員格式時，就會發生這種情況。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>因應措施

請執行手動還原。

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>當以 .NET461 為目標的專案參考另一個以 .NETStandard 為目標的專案時，msbuild /t:restore 就會失敗

#### <a name="issue"></a>問題

當以 .NET461 為目標的 PackageReferenece 型專案參考另一個以 .NETStandard 為目標的 PackageReference 型專案時，msbuild /t:restore 就會失敗。  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>因應措施

此問題目前沒有因應措施。

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4.0 RTM 時間範圍中已修正的問題

[NuGet 4.0 RC 版本資訊](../release-notes/nuget-4.0-RC.md) - 列出所有 NuGet 4.0 RC 修正的問題

### <a name="features"></a>功能

- NuGet.Core.sln 中的當地語系化字串 - [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget 強制以 LSL 模式載入 Web 應用程式專案 - [#4258](https://github.com/NuGet/Home/issues/4258)

- AutoReferenced PackageReference 支援封鎖「已安裝 SDK」套件 UI 中的版本變更 - [#4044](https://github.com/NuGet/Home/issues/4044)

- 正確進行任何專案相依性的 PackageSpec.Version 通訊 - [#3902](https://github.com/NuGet/Home/issues/3902)

- 支援從命令列將參考移入 `.csproj` - [#4101](https://github.com/NuGet/Home/issues/4101)

- 支援還原 PackageReference 專案 (一般和 xplat) 以及輕量型解決方案負載 - [#4003](https://github.com/NuGet/Home/issues/4003)

- 支援從命令列將參考新增至 `.csproj` - [#3751](https://github.com/NuGet/Home/issues/3751)

- 支援 `packages.config` 或 `project.json` 的輕量型解決方案負載 NuGet 還原 - [#3711](https://github.com/NuGet/Home/issues/3711)

- Nuget 產生之目標檔案中的 contentFiles 支援 - [#3683](https://github.com/NuGet/Home/issues/3683)

- 使用 MSBuild 在 Mac 上建立 nuget.exe 驗證的 Mono CI - [#3646](https://github.com/NuGet/Home/issues/3646)

- 移開 v2 NuGet.Core 相依性的 NuGet - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Bug

- Visual Studio 中的 NuGet 還原不遵守專案的 PackageId 屬性 - [#4586](https://github.com/NuGet/Home/issues/4586)

- 在 vsix 套件中新增套件時，發生 NuGet ProjectSystemCache 錯誤 - [#4545](https://github.com/NuGet/Home/issues/4545)

- 如果在有多個 TFM 的專案中使用 IncludeSource，套件會擲回例外狀況 - [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 在使用全解決方案套件管理更新時當機 - [#4474](https://github.com/NuGet/Home/issues/4474)

- 無法解除安裝新安裝的套件 - [#4435](https://github.com/NuGet/Home/issues/4435)

- 移轉至 PackageRef 時，混合式解決方案有奇怪的還原行為 - [#4433](https://github.com/NuGet/Home/issues/4433)

- 一開始 NuGet 作業 (安裝、更新、還原) 即建置，將會導致 VS 停止回應 - [#4420](https://github.com/NuGet/Home/issues/4420)

- UI 停止回應 - 鎖死初始化 NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- 新增套件命令應該會將版本新增為屬性，而不是項目 - [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo.sln - SLN 中的組態造成還原圖形出現重複 (不是 diff config) 的專案時會失敗 - [#4316](https://github.com/NuGet/Home/issues/4316)

- 僅套件內容 - [#3668](https://github.com/NuGet/Home/issues/3668)

- 根據預設，選擇不使用套件格式選取器選項 - [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%). 基準 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec. 基準 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- 在多重 TFM 專案中提名失敗 -[#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%). 基準 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - 以 netcoreapp1.1 為目標時發生套件警告 - [#4397](https://github.com/NuGet/Home/issues/4397)

- 嘗試在空的 ASP.NET Core Web 應用程式中新增 NuGet 套件時發生 PathTooLongException - [#4391](https://github.com/NuGet/Home/issues/4391)

- 套件執行太頻繁 -- dotnet
  - 與目標「套件」有關的目標相依性圖形中有循環相依性時，dotnetcore pack 會失敗 - [#4381](https://github.com/NuGet/Home/issues/4381)

- 套件執行太頻繁 -- 產生的 NuGet 套件不包含所有組態 - [#4380](https://github.com/NuGet/Home/issues/4380)

- 在 C++ 專案中，NullReferenceException 新增 Nuget 與 packageref - [#4378](https://github.com/NuGet/Home/issues/4378)

- 協助工具：朗讀程式不讀出核取方塊來選取要安裝套件的專案 - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 偶爾無法連線至 VSO/VSTS 摘要 - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)

- 如果 PackagePath 指定路徑為 "contentFiles"contentFiles，會取得錯誤位置的輸出 - [#4348](https://github.com/NuGet/Home/issues/4348)

- 套件目標附加有 VersionSuffix 的 PackageVersion 屬性 - [#4324](https://github.com/NuGet/Home/issues/4324)

- 指定套件路徑對 dotnet 套件無效 - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet 在還原期間輸出一堆重複匯入的警告 - [#4304](https://github.com/NuGet/Home/issues/4304)

- 在暗色調佈景主題下選擇不正確的 [NuGet 套件管理員格式] 對話方塊 - [#4300](https://github.com/NuGet/Home/issues/4300)

- 還原組建時發生 VS 損毀 - [#4298](https://github.com/NuGet/Home/issues/4298)

- 如果將 TFM 新增至 targetframeworks、儲存，然後建置，Visual Studio 就會鎖死。 10% 的時間 - [#4295](https://github.com/NuGet/Home/issues/4295)

- 成功封裝專案時，NuGet 套件不會輸出成功訊息 - [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask 失敗，因為找不到 System.IO.Compression 4.1 - [#4290](https://github.com/NuGet/Home/issues/4290)

- 套件執行太頻繁 - PackTask 經常因檔案存取衝突而失敗 - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet 在背景還原期間開啟輸出視窗 - [#4274](https://github.com/NuGet/Home/issues/4274)

- 將 ServiceProvider 視為危險的程式碼撰寫模式予以排除 (這可能會造成停止回應) - [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/UIHang - 改善 DownloadTimeoutStream 讀取 - [#4266](https://github.com/NuGet/Home/issues/4266)

- 如果在 NuGet 還原完成前企圖關閉專案，Visual Studio 會鎖死 - [#4257](https://github.com/NuGet/Home/issues/4257)

- PackTask 與封裝 `.nuspec` 的問題 - [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] 無法對新專案解析 NuGet 套件 (需要重新啟動 Visual Studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] 顯示可用套件版本的 [版本] 下拉式清單，不斷與所選的 NuGet 套件保持同步 - [#4198](https://github.com/NuGet/Home/issues/4198)

- 與 CPS 互動以防止發生鎖死時，Nuget.Client 應該使用 CPS JoinableTaskFactory - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 不從套件解除封裝 `.targets` - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore pack 不支援 `.csproj` 中的標題 - [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package 會導致 VS2017 RC 的錯誤對話方塊 - [#4127](https://github.com/NuGet/Home/issues/4127)

- 更新 .net core 專案的套件似乎無效，因為 UI 不會從提名取得 CPS 更新。 - [#4035](https://github.com/NuGet/Home/issues/4035)

- 改善未解決的參考警告 - [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore pack - ProjectReference 遺失版本資訊 - [#3953](https://github.com/NuGet/Home/issues/3953)

- 建立 UWP 應用程式會建立專案並重建已耗用時間總和迴歸 - [#3873](https://github.com/NuGet/Home/issues/3873)

- 還原期間即使發生錯誤仍會顯示成功還原訊息。 - [#3799](https://github.com/NuGet/Home/issues/3799)

- 將 Nuget.CommandLine 3.4.4 重新發佈至 Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- 在移轉時，專案從 `project.json` 變更至 `.csproj` --- 還原失敗 - [#4297](https://github.com/NuGet/Home/issues/4297)

- 新建立的 xunit 測試專案還原失敗 - [#4296](https://github.com/NuGet/Home/issues/4296)

- 核心專案可以在開啟時停止回應、鎖死 UI - [#4269](https://github.com/NuGet/Home/issues/4269)

- 修正組建工作的目標檔案 - [#4267](https://github.com/NuGet/Home/issues/4267)

- 組建卸載已參考專案的解決方案後，錯誤清單發生錯誤 - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057：專案中沒有目標 "_GenerateRestoreGraphProjectEntry"。 - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback：當您選取所有專案時，解決方案的 Nuget 管理員 UI 當機 - [#4191](https://github.com/NuGet/Home/issues/4191)

- 沒有尾端斜線時 nuget.exe msbuildpath 失敗 - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback：NuGet 還原提供數個 LinqToTwitter 專案的專案參考警告 - [#4156](https://github.com/NuGet/Home/issues/4156)

- `.csproj` 的套件不包含 minClientVersion 屬性 - [#4135](https://github.com/NuGet/Home/issues/4135)

- VS2017 中簽署的 NuGet.Build.Tasks.Pack.dll 運送延遲 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback：無法還原以 CMake 3.7.1 產生的 VS 2015 專案 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback：還原錯誤可能會混淆組建可能提供的更多完整錯誤訊息 - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] 還原網站專案的 NuGet 套件時發生錯誤：值不可為 Null。 - [#4092](https://github.com/NuGet/Home/issues/4092)

- 在 NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker 中移轉會擲回「物件參考例外狀況」 - [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore pack 應該以建置套件所用的版本來封裝工具 - [#4063](https://github.com/NuGet/Home/issues/4063)

- 新的背景還原在狀態列寫入毫秒，但還原時間以秒計 - [#4036](https://github.com/NuGet/Home/issues/4036)

- 因為錯字無法解析所有的專案參考 - [#4018](https://github.com/NuGet/Home/issues/4018)

- 在套件參考案例中啟用 PCM 工作流程 - [#4016](https://github.com/NuGet/Home/issues/4016)

- 套件管理員 UI 中找不到已安裝的套件 - [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - 當 PackagePath 為空時，dotnetcore pack 會失敗 - [#3993](https://github.com/NuGet/Home/issues/3993)

- 多使用者案例中的還原工作失敗 - [#3897](https://github.com/NuGet/Home/issues/3897)

- 使用 NuGet 套件工作進行封裝時，無法變更內容類型 - [#3895](https://github.com/NuGet/Home/issues/3895)

- MsBuild /t:pack 的預設複本 ContentFiles 不正確 - [#3894](https://github.com/NuGet/Home/issues/3894)

- 安裝套件還原記錄兩次還原套件訊息 - [#3785](https://github.com/NuGet/Home/issues/3785)

- 移除 [執行階段] 區段的 [Guardrails - Restore] \(防撞欄 - 還原) 僅適用於目前的專案 - [#3768](https://github.com/NuGet/Home/issues/3768)

- 套件工作會將內容檔放在 'content/' 和 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 會執行額外標記分割 - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore pack：以套件參考封裝專案會造成匯入警告重複出現 - [#3665](https://github.com/NuGet/Home/issues/3665)

- VS 中的還原記錄不一定顯示 - [#3633](https://github.com/NuGet/Home/issues/3633)

- Nuget 區域變數說明文字仍然提及套件快取 - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 結合 PackageReferences 與 TargetFrameworks。 - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget 在 VS "15" Preview 4 dev. 中挑選了非預期的 MSBuild 版本 命令提示字元 - [#3408](https://github.com/NuGet/Home/issues/3408)

- 在失敗的還原上寫出目標/props 檔案 - [#3399](https://github.com/NuGet/Home/issues/3399)

- 在 VS 15 命令提示字元中執行時，NuGet 在還原期間不遵守與 MSBuild 相同的相容性填充碼 - [#3387](https://github.com/NuGet/Home/issues/3387)

- 重新啟用 VS15 的 PackFromProjectWithDevelopmentDependencySet - [#3272](https://github.com/NuGet/Home/issues/3272)

- NuGet 的 Blend 問題 - [#4043](https://github.com/NuGet/Home/issues/4043)

- 將 4.0.0.2067 整合到 CLI 和 SDK 的存放庫以隨附 RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)

- 當您建立新的核心主控台應用程式、關閉解決方案、開啟解決方案和關閉解決方案時，VS 停止回應 - [#4008](https://github.com/NuGet/Home/issues/4008)

- 針對 d15prerel.25916.01 叫用停止回應開啟專案 - [#3982](https://github.com/NuGet/Home/issues/3982)

- 修正 dotnet/nuget.exe 區域變數 doc/help 訊息 - [#3919](https://github.com/NuGet/Home/issues/3919)

- 檢查 PackTask 的開頭或結尾空格問題 - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore pack 是從 obj 壓縮，不是 bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore pack 似乎一律將 ProjectReference 版本設定為 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - dotnetcore pack 因專案參考和 <TargetFramework> 而失敗 - [#3865](https://github.com/NuGet/Home/issues/3865)

- ProjectSystemCache.TryGetProjectNameByShortName 中的 LockRecursionException - [#3861](https://github.com/NuGet/Home/issues/3861)

- 修剪 MSBuild 屬性的空白字元 - [#3819](https://github.com/NuGet/Home/issues/3819)

- 合併專案載入時引發的兩個專案事件 - [#3759](https://github.com/NuGet/Home/issues/3759)

- `project.assets.json` 檔案中的 P2P 程式庫版本不正確 - [#3748](https://github.com/NuGet/Home/issues/3748)

- 還原損毀，因為沒有會回應的摘要，也無法使用套件 - [#3672](https://github.com/NuGet/Home/issues/3672)

- 發生大量 MSBuild 錯誤輸出時，nuget.exe 可能停止回應 - [#3572](https://github.com/NuGet/Home/issues/3572)

- Blend 的建置時還原第一次失敗，第二次成功 (VS 案例已修正) - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCR

- 將 vsix 從 v2 vsix 移轉至 v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet 應有取得 MSBuild 之鎖定檔案路徑的機制 - [#3351](https://github.com/NuGet/Home/issues/3351)

- 將組建資產新增至 TFM 相容性檢查和資產檔案 - [#3296](https://github.com/NuGet/Home/issues/3296)

- 定義套件目標中的新 ProjectCapability「套件」以啟用套件的相關功能 - [#4146](https://github.com/NuGet/Home/issues/4146)

- 根據 "GeneratePackageOnBuild" MSBuild 屬性的條件，將套件 執行為後組建目標 - [#4145](https://github.com/NuGet/Home/issues/4145)

- 使用 NuGet 屬性 RestoreProjectStyle 建立特定的 NuGet 專案 - [#4134](https://github.com/NuGet/Home/issues/4134)

- 可轉移的專案參考變更為調整還原 - [#4076](https://github.com/NuGet/Home/issues/4076)

- 在非 UWP 專案的目標檔案中新增 NuGet 屬性 - [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion 支援 - [#3923](https://github.com/NuGet/Home/issues/3923)

- 進行專案參考中繼資料和 NuGet 專案系統的通訊 - [#3922](https://github.com/NuGet/Home/issues/3922)

- 將 UI 新增至封裝模式 - [#3921](https://github.com/NuGet/Home/issues/3921)

- 舊版的 `.csproj` 需要在 proj/目標中設定 NugetTargetMoniker 和 RuntimeIdentifiers - [#3854](https://github.com/NuGet/Home/issues/3854)

- 安裝套件可能會與自動還原重疊 - [#3836](https://github.com/NuGet/Home/issues/3836)

- 未載入 VSPackage 時不會發生操作功能表 QueryStatus - [#3835](https://github.com/NuGet/Home/issues/3835)

- 解決方案還原和組建還原仍會顯示對話方塊 - [#3789](https://github.com/NuGet/Home/issues/3789)

- 隔離 NuGet.Clients 解決方案組建中的 VSSDK 版本 - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>RTM 中已修正的 GitHub 問題連結
[問題清單 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[問題清單 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[問題清單 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[問題清單 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[問題清單 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
