---
title: NuGet 4.8 RTM 版本資訊
description: NuGet 4.8.1 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813763"
---
# <a name="nuget-48-release-notes"></a>NuGet 4.8 版本資訊

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 NuGet 4.8 功能。


相同的功能也有命令列版本可供使用：
* NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>摘要:4.8.0 中的新增功能
* NuGet.exe 現在可在 Windows 10 上支援 longfilenames - [#6937](https://github.com/NuGet/Home/issues/6937)
* 驗證外掛程式現在可以在 MsBuild、DotNet.exe、NuGet.exe 和 Visual Studio 間運作，包括跨平台運作。 第一代的驗證外掛程式在 MsBuild DotNet.exe 中不受支援。 注意：VS 2017 15.9 預覽組建包含 VSTS 驗證外掛程式。 [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild 的 SDK 解析程式現在建置為 NuGet 的一部分，並使用 VS 的 NuGet 工具進行安裝。 這可避免版本不同步的情形。[#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference 現在支援 DevelopmentDependency 中繼資料 - [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>摘要:4.8.2 中的新增功能

* 安全修復:在 #/.nuget 中創建的檔案的許可權在[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673)太開放

## <a name="known-issues"></a>已知問題
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>在 CI 電腦上或在離線環境中安裝已簽署的套件需要較多時間

#### <a name="issue"></a>問題
如果電腦的網際網路存取受到限制 (例如，CI/CD 案例中的組建電腦)，在安裝/還原已簽署的 Nuget 套件時將會因為撤銷伺服器無法連線而出現警告 ([NU3028](../reference/errors-and-warnings/nu3028.md))。 這是預期行為。 但在某些情況下，這可能會有非預期的後果，例如套件安裝/還原耗時較長。

#### <a name="workaround"></a>因應措施
在 Visual Studio 15.8.4 和 NuGet.exe 4.8.1 的更新中，我們引進了可切換撤銷檢查模式的環境變數。
將 `NUGET_CERT_REVOCATION_MODE` 環境變數設定為 `offline`，會強制 NuGet 僅對快取的憑證撤銷清單檢查憑證的撤銷狀態，且 NuGet 將不會嘗試連線到撤銷伺服器。 當撤銷檢查模式設定為 `offline` 時，警告將會降級為資訊。

> [!Warning]
> 在一般情況下，不建議您將撤銷檢查模式切換為離線狀態。 這樣會導致 NuGet 略過線上撤銷檢查，而僅對可能已過期的快取憑證撤銷清單執行離線撤銷檢查。 這表示簽署憑證可能已遭撤銷的套件將會繼續安裝/還原，但原本其撤銷檢查將會失敗，且不會安裝。

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項

#### <a name="issue"></a>問題

當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。 這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。

#### <a name="workaround"></a>因應措施

執行以下任何一個 NuGet 動作：
* 開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...`
* 開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console`
* 執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages`
* 建置專案也會觸發 NuGet 還原

您現在應該可以看到移轉選項。 請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。
注意：此問題已在 VS 2017 15.9 Preview 3 中修正

## <a name="issues-fixed-in-this-release"></a>本版已修正的問題

### <a name="bugs"></a>Bug
#### <a name="signing"></a>簽署
* 簽署：在離線環境中安裝已簽署的套件 [#7008](https://github.com/NuGet/Home/issues/7008) - 已在 4.8.1 中修正
* 簽署：不正確的 URL 檢查 - [#7174](https://github.com/NuGet/Home/issues/7174)
* 簽署：存放庫已副署時，在 RepositorySignatureVerifier 中檢查套件完整性 - [#6926](https://github.com/NuGet/Home/issues/6926)
* 「套件完整性檢查失敗。」 在訊息中應有套件識別碼 (和錯誤碼) - [#6944](https://github.com/NuGet/Home/issues/6944)
* 存放庫已簽署的套件驗證允許以不同的憑證簽署的套件 - [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - 簽署 - 時間戳記 URL 不可為 https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* 請勿在 NuSpec 封裝案例中使用 NullRef，並請改善選項 - [#6866](https://github.com/NuGet/Home/issues/6866)
* 在更新簽署者資訊期間，將時間戳記新增至副署時發生記憶體無效的狀況 - [#6840](https://github.com/NuGet/Home/issues/6840)
* 簽署：移除 CTL 例外狀況 - [#6794](https://github.com/NuGet/Home/issues/6794)
* 簽署：contentUrl 必須是 HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* 簽署：未使用 SignedPackageVerifierSettings.VSClientDefaultPolicy - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Pack
* 使用 dotnet.exe 來封裝 nuspec 時應該不需要還原和建置 - [#6866](https://github.com/NuGet/Home/issues/6866)
* 在 NuspecProperties 中允許空的取代權杖 - [#6722](https://github.com/NuGet/Home/issues/6722)
* 已指定 NuspecProperties 時，PackTask 會擲回 NullReferenceException - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Accessibility
* [協助工具] 在 PM UI 中，套件按鈕下的字串「發行前版本」被其套件描述遮住 - [#4504](https://github.com/NuGet/Home/issues/4504)
* [協助工具] 在 PM UI 中選取 [Microsoft Visual Studio 離線套件] 時，套件來源下拉式清單和設定按鈕會截斷 - [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Powershell 管理主控台 (PMC)
* `Update-Package` 會忽略 PackageReference 版本範圍 - [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` 解決方案整體問題 - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` 會重新安裝所有套件，而非指定的單一套件 - [#737](https://github.com/NuGet/Home/issues/737)
* 可從套件管理員主控台更新為未列出的 NuGet 套件 - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>其他
* 若要修正 `NuGet update self` NuGet.Commandline，nupkg 不應為 semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* 改善 NU1107 安裝失敗的體驗 - [#7107](https://github.com/NuGet/Home/issues/7107)
* GetAuthenticationCredentialRequest 的序列化不正確 - [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage 在 UI 執行緒外初始化時無法載入 - [#6976](https://github.com/NuGet/Home/issues/6976)
* 還原作業會回報誤導的錯誤，指出需要 project.json - [#6959](https://github.com/NuGet/Home/issues/6959)
* 套件管理員 UI：預覽變更的 [確定] 按鈕不會自動供鍵盤使用 - [#6893](https://github.com/NuGet/Home/issues/6893)
* 對於具有 p2p 參考的專案會忽略 RestoreSources - [#6776](https://github.com/NuGet/Home/issues/6776)
* 使用 .NET Framework 範本建立單元測試專案，將會開啟具有 packages.config 的舊有專案模型 - [#6736](https://github.com/NuGet/Home/issues/6736)
* 允許專案參考覆寫套件相依性 - [#6536](https://github.com/NuGet/Home/issues/6536)
* 在 MSBuild 工作中公開 NoDefaultExcludes - [#6450](https://github.com/NuGet/Home/issues/6450)
* 「清除所有 NuGet 快取」的狀態訊息可能會在調整視窗大小後隱藏 - [#5938](https://github.com/NuGet/Home/issues/5938)


[本版修正的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
