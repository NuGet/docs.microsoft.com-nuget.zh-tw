---
title: NuGet 4.0 RC 版本資訊
description: NuGet 4.0 RC 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821882"
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC 版本資訊

[NuGet 3.5 RTM 版本資訊](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) 著重於新增 .NET Core 案例支援、處理重要客戶意見，以及改善各種案例中的效能。 此版本帶來幾項改善，像是支援 PackageReference，以及 MSBuild 目標、背景套件還原等多項 NuGet 命令。

## <a name="bug-fixes"></a>Bug 修正

- `dotnet pack --version-suffix foo` 中的行為變更  - [#3838](https://github.com/NuGet/Home/issues/3838)

- 僅有 vs "15" 電腦上的 nuget.exe restore 失敗 - [#3834](https://github.com/NuGet/Home/issues/3834)

- .NETCore 檔案新專案應該在還原期間封鎖組建 - [#3780](https://github.com/NuGet/Home/issues/3780)

- 無法還原從 VS2015 移轉至 VS "15" 的 ASP.NET Core Web 應用程式。 - [#3773](https://github.com/NuGet/Home/issues/3773)

- [測試失敗] PM UI 無法解除安裝套件「jQuery 驗證」- [#3755](https://github.com/NuGet/Home/issues/3755)

- 將套件安裝至 UWP `project.json` 時，也應該還原父專案 - [#3731](https://github.com/NuGet/Home/issues/3731)

- 修改 NuGet 目標以將套件來源記錄為高詳細資訊，而非標準 - [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore pack3 預設應該會包含 XML 文件 - [#3698](https://github.com/NuGet/Home/issues/3698)

- 從沒有套件的來源並選取所有來源時，從 UI 的批次更新會失敗 - [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget pack 命令不會包含所有檔案 - [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM 問題 - [#3661](https://github.com/NuGet/Home/issues/3661)

- 資產檔案的 ProjectFileDependencyGroups 區段應該使用專案的程式庫名稱 - [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" 和遞迴目錄 - [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 失敗會記錄為警告，而非錯誤 - [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS 問題：「在您的工作區中找不到 [file]，或您沒有其存取權限」- [#2805](https://github.com/NuGet/Home/issues/2805)

- 在 vs 快速啟動搜尋方塊中鍵入 "nuget <packagename>" 會保留 "nuget " 前置詞 - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: 在 Core Properties 部分發現無法識別的根項目。 行 2，位置 2。 - [#2718](https://github.com/NuGet/Home/issues/2718)

- 不再建置文字欄位中含逸出 &lt; 或 &gt; 的`.nuspec` - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe delete 不會提示您輸入認證 (它是非互動模式) - [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete 會警告本機來源的 API 金鑰，即使沒有任何意義也是一樣 - [#2625](https://github.com/NuGet/Home/issues/2625)

- 安裝 EF 時錯誤體驗不佳 -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)

- 在套件管理員中變更選取範圍之後，Visual Studio 讓嘗試損毀 - [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - 使用浮動版本時，dotnetcore restore 會對一般清單本機存放庫執行區分大小寫識別碼查閱 - [#2516](https://github.com/NuGet/Home/issues/2516)

- 中斷 V2 摘要的 nuget.exe delete - [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe push timeout 需要較佳的錯誤訊息 - [#2503](https://github.com/NuGet/Home/issues/2503)

- 沒有適當匯入的工具還原會以無訊息模式失敗。 - [#2462](https://github.com/NuGet/Home/issues/2462)

- 有私人摘要時，NuGet 會提示輸入認證，即使從 nuget.org 安裝時也是一樣 - [#2346](https://github.com/NuGet/Home/issues/2346)

- ApplicationInsights 2.0 套件已列出，但尚未存在 - [#2317](https://github.com/NuGet/Home/issues/2317)

- VS "15" Preview 5 分支中的 UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)

- 在 UWP 建置期間遺漏還原的第一個 OnBuild 事件 - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 中斷 EntityFramework 安裝？ - [#3312](https://github.com/NuGet/Home/issues/3312)

- 將來源新增至詳細記錄 (請考慮用於 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- nuget 用戶端版本 3.4+ 不支援 NoCache 參數 - [#3074](https://github.com/NuGet/Home/issues/3074)

- VS 中無法載入認證提供者時，不會中斷 NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>功能

- 設定 CI 執行 x86 - [#3868](https://github.com/NuGet/Home/issues/3868)

- 自動還原 3/3：非封鎖 UI - [#3658](https://github.com/NuGet/Home/issues/3658)

- 自動還原 2/3：提名時的背景還原 - [#3657](https://github.com/NuGet/Home/issues/3657)

- 還原專案參考以符合建置行為 (遞迴) - [#3615](https://github.com/NuGet/Home/issues/3615)

- VS "15" 中的 DPL 支援 - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- 將設定檔移至 Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)

- 產生的還原屬性和目標需要跨目標參與支援 - [#3496](https://github.com/NuGet/Home/issues/3496)

- PackageTargetFallback 的 NuGet Restore 支援 (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)

- ToolsRef 實作 - [#3472](https://github.com/NuGet/Home/issues/3472)

- RID 的 Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)

- 支援新增/移除/更新 PackageRefs 的 NuGet UI - [#3457](https://github.com/NuGet/Home/issues/3457)

- 自動還原 1/3：透過快取專案還原資訊的提名 API 實作 - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet Restore 工作和目標 - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] 在 MSBuild 中啟用方案層級還原 - [#2993](https://github.com/NuGet/Home/issues/2993)

- Visual Studio 中支援認證提供者公用擴充性 - [#2909](https://github.com/NuGet/Home/issues/2909)

- 遞迴 nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)

- 無法在 dev15 上載入 Microsoft.TeamFoundation.Client，需要將 VS "15" Preview 的 Microsoft.TeamFoundation.Client 版本更新為 15.0 - [#2392](https://github.com/NuGet/Home/issues/2392)

- 在 VS "15" Preview 中，無法將 C++ 套件安裝至 C++ UWP 專案 - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg 需要支援 \buildCrossTargeting\ 資料夾 - 以及匯入 `.targets` / `.props` 來「跨目標設為」MSBuild 範圍。 - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference 設計 - [#3462](https://github.com/NuGet/Home/issues/3462)

- 修正 NuGet UI 以支援 `.csproj` 中含 PackageReferences 的 restore - [#3455](https://github.com/NuGet/Home/issues/3455)

- 將清除快取按鈕新增至 VS 套件管理員設定 - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- 進行自動還原時，應該會封鎖方案還原。 - [#3797](https://github.com/NuGet/Home/issues/3797)

- NuGet 套件管理員 UI 中的 NetCore install 會安裝到每個 TFM，而不是套件所支援的 TFM - [#3721](https://github.com/NuGet/Home/issues/3721)

- 還原提名者 API 也需要支援 DotNetCliToolsReferences。 - [#3702](https://github.com/NuGet/Home/issues/3702)

- 將 VS "15" vsix 標示為 systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- 從參考 MS.VS.Services.Client 移轉至 MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- restore 應該在專案層級使用 $(RestoreLegacyPackagesDirectory) - [#3618](https://github.com/NuGet/Home/issues/3618)

- 還原至含單一 TargetFramework 的專案不得設定屬性條件 - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj 應該遵循 projectref 相依性，同時還原這些相依性。 例如組建。 - [#3577](https://github.com/NuGet/Home/issues/3577)

- 在鎖定檔案中，"type": "platform" 相依性呈現為 "type":"package" - [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe 詳細資訊模式應該顯示下載 URL - [#2629](https://github.com/NuGet/Home/issues/2629)

- 將 NuGet xplat 移至 Microsoft.NetCore.App 和 netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- 推送 - 從命令列推送時，應該可以覆寫符號伺服器 - [#2348](https://github.com/NuGet/Home/issues/2348)

- 合併用於尋找全域套件路徑的程式碼 - [#2296](https://github.com/NuGet/Home/issues/2296)

- 需要比 suppressParent 更適合的名稱 - [#2196](https://github.com/NuGet/Home/issues/2196)

- 判斷要用於 MSBuild 專案的 `project.json` 相依性名稱 - [#1914](https://github.com/NuGet/Home/issues/1914)

- 將 SemVer 2.0.0 支援新增至 NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- 允許可在 MSBuild 中使用 `.targets` 的可轉移相依性 NuPkg - [#3342](https://github.com/NuGet/Home/issues/3342)

- 命令列中的 NuGet restore 明顯比 VS 還要慢 - [#3330](https://github.com/NuGet/Home/issues/3330)

- 將套件識別碼和版本比較設為不區分大小寫 - [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache 選項不適用於 `packages.config` 型 restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdResource 資源需要預設快取內容和記錄器 - [#1357](https://github.com/NuGet/Home/issues/1357)
