---
title: NuGet 4.4 RTM 版本資訊
description: NuGet 4.3 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432565"
---
# <a name="nuget-44-release-notes"></a>NuGet 4.4 版本資訊

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 NuGet 4.4 RTM。

## <a name="summary-whats-new-in-440"></a>摘要: 4.4.0 中的新功能

## <a name="summary-whats-new-in-442"></a>摘要: 4.4.2 中的新功能

* 安全性修正：在 ~/.nuget 內建立的檔案權限過於開放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>摘要: 4.4.3 中的新功能

* 安全性修正：NUPKG 內的檔案可以有 NUPKG 目錄上層的相對路徑 [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>已知問題

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題 

.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。 [這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core 專案中的套件如包含具有無效簽章的組件，可能會觸發無限的還原迴圈。

#### <a name="issue"></a>問題

有時候，當您使用的套件包含具有無效簽章的組件時，或套件版本使用 'DateTime' 指示器設定時，會導致套件自動還原為在無限迴圈中執行 (dotnet/project-system#1457)。

#### <a name="workaround"></a>因應措施

此問題目前沒有因應措施。

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>NuGet 4.4 RTM 時間範圍中已修正的問題

[NuGet 4.3 RTM 版本資訊](../release-notes/nuget-4.3-RTM.md) - 列出所有 NuGet 4.3 RTM 修正的問題

### <a name="features"></a>功能

- PMC 和 NuGet PM UI 案例中的輕量型解決方案載入支援 - [#5180](https://github.com/NuGet/Home/issues/5180)

- msbuild 封裝目標在其前面應該有執行使用者目標的公用勾點 - [#5143](https://github.com/NuGet/Home/issues/5143)

- 功能：將 dependencyVersion 參數新增至 nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 應該對應至 .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- 使用 msbuild /t:restore 支援 Visual Studio Build Tools SKU - [#5562](https://github.com/NuGet/Home/issues/5562)

- 在還原期間，如果需要但未安裝 .NET Standard 2.0 的 .NET 4.6.1 支援，則會產生錯誤 - [#5325](https://github.com/NuGet/Home/issues/5325)

- 套件識別碼前置詞保留用戶端 UI - [#5572](https://github.com/NuGet/Home/issues/5572)

- 提供當地語系化 Nuget 元件以支援 dotnet.exe 當地語系化 - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Bug

- 不同的專案路徑轉換可能會導致還原遺失 PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)

- 將含警告號碼的錯誤碼移至錯誤範圍 - [#5824](https://github.com/NuGet/Home/issues/5824)

- 當 .NET Standard 版本不知道是否與目標架構相容時發生誤導錯誤 - [#5818](https://github.com/NuGet/Home/issues/5818)

- 含混淆授權的測試檔案 - [#5776](https://github.com/NuGet/Home/issues/5776)

- EndToEnd 測試範本中遺漏授權標頭 - [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config restore 將錯誤顯示為 NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe install 在 mono 上應該有 DisableParallelProcessing - [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe install 不正確地停用快取 - [#5737](https://github.com/NuGet/Home/issues/5737)

- VS 停用還原時針對 packages.config 執行 restore 命令會顯示不正確的訊息 - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS；停用還原時執行 restore 命令會顯示混淆的訊息 - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask 在遺失版本中繼資料時失敗 - [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore add package 可以清除 csproj 中的空行  - [#5697](https://github.com/NuGet/Home/issues/5697)

- NuGet.Config 中認證設定的來源名稱區分大小寫 - [#5695](https://github.com/NuGet/Home/issues/5695)

- 啟用 GeneratePackageOnBuild 已刪除我的整個套件歷程記錄 - [#5676](https://github.com/NuGet/Home/issues/5676)

- 還原無法還原 mono.cecil 或 semver 套件，但會還原所有其他套件。 - [#5649](https://github.com/NuGet/Home/issues/5649)

- 錯誤和警告 - 來源無法使用時發生嚴重錯誤。  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] NuGet 安裝狀態文字目前在暗色調佈景主題上看起來不正確。 - [#5642](https://github.com/NuGet/Home/issues/5642)

- 在所有專案的方案更新/安裝時更新套件 - [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - dotnetcore pack 的行為會根據 TargetFramework 與 TargetFrameworks 而不同 - [#5281](https://github.com/NuGet/Home/issues/5281)

- 工具資料夾內所含的 DLL 擲回警告 - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel 使用太多記憶體來執行字串作業 - [#4714](https://github.com/NuGet/Home/issues/4714)

- OSX 的 RuntimeEnvironmentHelper.IsLinux 傳回 true - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet pack' 會將 nuspec 放在 obj 下方，而不是 obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget 的套件升級極為緩慢 - [#4534](https://github.com/NuGet/Home/issues/4534)

- CPS 與具有尚未開啟 LSL (輕量型解決方案還原) 的大型方案的還原不同步 - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - 含所提供版本的 Nuget 封裝會忽略中繼資料 (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- 含版本號碼和 ExcludeVersion 旗標的 Nuget.exe (3.+) 安裝套件不會將套件更新為較新版本 - [#2405](https://github.com/NuGet/Home/issues/2405)

- Project.json restore 應該會在最上層套件違反條件約束時發出警告 - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile 未在 install 命令上設定自訂組態 - [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe install 不接受 '-DisableParallelProcessing' 參數 - [#1556](https://github.com/NuGet/Home/issues/1556)

- DotNet.exe 或 msbuild.exe 仍然會使用已停用來源 - [#5704](https://github.com/NuGet/Home/issues/5704)

- 修正 LSL 案例中的當機 - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCR

- nuget.exe install TargetFramework 支援 - [#5736](https://github.com/NuGet/Home/issues/5736)

- 新增不同 msbuild 工作 UserAgent 字串 (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName 應該是虛擬的 - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] 新增 NuGet 套件時發生混淆的訊息 - [#5641](https://github.com/NuGet/Home/issues/5641)

- [警告和錯誤] NoWarn 不會以可轉移方式流過 P2P 參考 - [#5501](https://github.com/NuGet/Home/issues/5501)

- 輕量型解決方案負載：PM UI、PMC 及 IV 的通用核心 - [#5057](https://github.com/NuGet/Home/issues/5057)

- 輕量型解決方案負載：支援 - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- 新增 Visual Studio 所觸發的預先還原 MSBuild 目標支援 - [#4781](https://github.com/NuGet/Home/issues/4781)

- 將公用目標新增至可使用 BeforeTargets 參考的 NuGet.targets - [#4634](https://github.com/NuGet/Home/issues/4634)

- 套件目標無法使用建置動作正確地建立 contentFiles - [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do 封鎖執行緒集區執行緒 - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- install 命令 DependencyVersion 和 Framework 旗標的文件 - [#5858](https://github.com/NuGet/Home/issues/5858)

- NuGet 警告和錯誤文件更新 - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>4.4 RTM 中已修正之 GitHub 問題的連結

[問題清單 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[問題清單 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[問題清單 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
