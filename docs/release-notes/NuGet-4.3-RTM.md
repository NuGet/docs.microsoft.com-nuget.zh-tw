---
title: NuGet 4.3 RTM 版本資訊
description: NuGet 4.3 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496597"
---
# <a name="nuget-43-release-notes"></a>NuGet 4.3 版本資訊

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附有 NuGet 4.3 RTM，它新增新案例的支援，例如 .NET Standard 2.0/.NET Core 2.0、包含許多品質修正，並且改善效能。 此版本也帶來數項改善，像是支援語意化版本控制系統 2.0.0、NuGet 警告和錯誤的 MSBuild 整合等等。

## <a name="summary-whats-new-in-430"></a>摘要:4.3.0 中的新增功能

## <a name="summary-whats-new-in-431"></a>摘要:4.3.1 中的新增功能

* 安全修復:在 #/.nuget 中創建的檔案的許可權在[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673)太開放
* 安全修復:NUPKG 內部的檔可以在 NUPKG 目錄上方具有相對路徑[#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>已知問題

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>在某些情況下，NuGet restore 會將已停用的套件來源視為已啟用

#### <a name="issue"></a>問題

下列 restore 命令列技術會將已停用的套件視為已啟用。 [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (可能出現在 VS 或 NetCore SDK 2.0.0 所隨附的 dotnet.exe)

#### <a name="workaround"></a>因應措施

1. 使用 Visual Studio (2017 15.3 或更新版本) 或 NuGet.exe (v4.3.0 或更新版本)
1. 刪除已停用的來源，然後繼續使用 msbuild 或 dotnet.exe。
1. 對於您的解決方案，您可以在 NuGet.config 中使用 "Clear"，然後定義該解決方案的必要來源。

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>使用套件管理員主控台時，'Enter' 鍵可能無法運作

#### <a name="issue"></a>問題

有時候，Enter 鍵無法在套件管理員主控台中運作。 如果您遇到此問題，請查看本修正的進度，並針對您的重新產生步驟提供任何有用的資訊。 [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>因應措施

重新啟動 Visual Studio 並在開啟解決方案之前開啟 PMC。 或者，嘗試刪除 `project.lock.json` 並再次還原。

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>您無法使用 NuGet 套件管理員檢視、新增或更新 DotNetCLITools

#### <a name="issue"></a>問題

NuGet 套件管理員沒有顯示，而且不允許加入/更新 DotNetCLITools。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>因應措施

您必須在專案檔中手動編輯 DotNetCLIToolReferences。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>重定目標 Framework 版本可能會導致不完整的 Intellisense

#### <a name="issue"></a>問題

在 Visual Studio 中重定目標 Framework 版本可能會導致不完整的 Intellisense。 當您使用 PackageReferences 作為套件管理員格式時，就會發生這種情況。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>因應措施

請執行手動還原。

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>NuGet 4.3 RTM 時間範圍中已修正的問題

[NuGet 4.0 RTM 版本資訊](../release-notes/nuget-4.0-RTM.md) - 列出所有 NuGet 4.0 RTM 修正的問題

### <a name="features"></a>特性

- 改善 NuGet 還原效能 - 針對命令列還原作業和 VS 實作更聰明的 NoOp - [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0：VS/Dotnet CLI 應該開始使用現有的 NuGet 功能：回溯資料夾 - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0：讓使用者能略過特定的還原警告 (或提高至錯誤) - [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0：CLI 當地語系化組件 - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0：向資產檔案註冊所有警告/錯誤 (包括 PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- 啟用 TFM 支援：NetStandard2.0、Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- 減少 NuGet.Core 和 NuGet.Client 專案數 (以及 DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)

- 新增將 Nuget 警告標記為錯誤的功能 - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Bug

- msbuild /t:pack 失敗，因為 "PackTask" 工作不支援 "DevelopmentDependency" 參數 - [#5584](https://github.com/NuGet/Home/issues/5584)

- 如果不在 PackagePath 結尾處新增 Windows 目錄分隔符號，則為壓平合併的內容檔案目錄結構 - [#4795](https://github.com/NuGet/Home/issues/4795)

- netcore 專案不支援設定為 developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- 同步載入 RestoreManagerPackage，這會封鎖 UI 執行緒並使 VS 鎖死 - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnetcore Restore (以及 msbuild /t:restore) 會略過具有明確方案專案相依性的專案 [#4578](https://github.com/NuGet/Home/issues/4578)

- 如果解決方案中有參考到相同專案的 projectreferences、有不同的大小寫，還原可能無法運作。 這也會影響大小寫沒有差異的不同相對路徑 - [#4574](https://github.com/NuGet/Home/issues/4574)

- 從 NuGet 套件還原的可執行檔，無法再與 .NET Core 2.0 搭配執行 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe 在剖析解決方案檔時會抑制例外狀況的詳細資料 - [#4411](https://github.com/NuGet/Home/issues/4411)

- 在 Windows 上，如果 ContentTargetFolders 包含結尾使用 '/' 的路徑，組件會將內容檔案放在錯誤的位置 - [#4407](https://github.com/NuGet/Home/issues/4407)

- 無法為以 netcoreapp1.1 為目標的工具套件還原 DotNetCliToolReference - [#4396](https://github.com/NuGet/Home/issues/4396)

- Nuget 更新 CLI 在專案檔中留下舊的套件版本條件 (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- 從 CPS nomation 讀取 DotnetCliToolTargetFramework - [#5397](https://github.com/NuGet/Home/issues/5397)

- 專案樣式 UWP 的 TPMinV 檢查應該能運作 - [#4763](https://github.com/NuGet/Home/issues/4763)

- 改善自動參考套件的 UI 描述 - [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet 還原從執行階段欄位區段選取編譯資產。 - [#4207](https://github.com/NuGet/Home/issues/4207)

- 相依性診斷放在鎖定檔中 - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>4.3 RTM 中已修正之 GitHub 問題的連結

[問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
