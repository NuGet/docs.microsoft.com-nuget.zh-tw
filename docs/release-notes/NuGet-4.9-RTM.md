---
title: NuGet 4.9 RTM 版本資訊
description: NuGet 4.9 版本資訊，包含已知問題、錯誤 (Bug) 修正、新功能與 DCR。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432487"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 15.9.0 版](https://visualstudio.microsoft.com/downloads/) | [2.1.500、2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | N/A | N/A |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 15.9.4 版](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 15.9.6 版](https://visualstudio.microsoft.com/downloads/) | [2.1.504、2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>摘要: 4.9.0 中的新功能

* 簽署：讓 ClientPolicies 要求使用 NuGet.Config 中所列的一組受信任作者與存放庫 - [#6961](https://github.com/NuGet/Home/issues/6961)、[部落格文章](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* 建立 ".snupkg" 檔案以在套件中包含符號 -- 加強推送以了解 nuget 通訊協定以接受符號伺服器的 snupkg 檔案 - [#6878](https://github.com/NuGet/Home/issues/6878)、[部落格文章](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet 認證外掛程式 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* 自封式 NuGet 套件 - 授權 - [#4628](https://github.com/NuGet/Home/issues/4628)、[公告](https://github.com/NuGet/Announcements/issues/32)

* 啟用 PackageReference 上的選擇性加入 "GeneratePathProperty" 中繼資料以產生每個套件的 MSBuild 屬性到 "Foo.Bar\1.0\" 目錄 - [#6949](https://github.com/NuGet/Home/issues/6949)

* 使用 NuGet 作業改進客戶成功 - [#7108](https://github.com/NuGet/Home/issues/7108)

* 使用鎖定檔案啟用可重複的套件還原 - [#5602](https://github.com/NuGet/Home/issues/5602)、[公告](https://github.com/NuGet/Announcements/issues/28)、[部落格文章](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

* 由 PackageExtraction 引發的警告提升為錯誤 (透過 WarnAsErrors) 不應該留下擷取的套件 - [#7445](https://github.com/NuGet/Home/issues/7445)

* 錯誤簽署的套件最後不應該存在於全域套件資料夾中 - [#7423](https://github.com/NuGet/Home/issues/7423)

* 繫結重新導向產生不應該跳過 facade 組件 - [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals 無法比較浮點數範圍 - [#7324](https://github.com/NuGet/Home/issues/7324)

* 還原：使用新的 .NET Core 2.1 HTTP 堆疊的效能迴歸 - [#7314](https://github.com/NuGet/Home/issues/7314)

* 套件的更新不應該修改 PackageReference 的 PrivateAssets - [#7285](https://github.com/NuGet/Home/issues/7285)

* 簽署：若套件有太多套件項目 (>65534)，簽署應該失敗 - [#7248](https://github.com/NuGet/Home/issues/7248)

* "dotnet nuget push" 程式碼路徑應該支援新的認證提供者 - [#7233](https://github.com/NuGet/Home/issues/7233)

* 支援執行具有不因文化特性而異的外掛程式 (如 Docker 中所發生) - [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget sources add 不應該從 NuGet.config 刪除認證 - [#7200](https://github.com/NuGet/Home/issues/7200)

* 安裝 devDependency PackageReference 不應該預設為 excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)

* 修正移轉程式選項以針對所有專案顯示並在專案不相容時顯示錯誤 - [#6958](https://github.com/NuGet/Home/issues/6958)

* "dotnet add package" 應該認可它對資產檔案所執行的還原 - [#6928](https://github.com/NuGet/Home/issues/6928)

* 簽署：改進簽署相關錯誤訊息 - [#6906](https://github.com/NuGet/Home/issues/6906)

* [測試失敗][zh-TW]套件管理器主控台上的 "Package Manager Console" 字串未當地語系化 - [#6381](https://github.com/NuGet/Home/issues/6381)

* 有關「找不到專案資訊」的錯誤訊息在 VS 內應該更確切一點 - [#5350](https://github.com/NuGet/Home/issues/5350)

* 不正確地使用 nuget 套件的 nuspec 版本標記時沒有幫助的錯誤訊息 - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - 簽署：支援 NuGet 通訊協定：RepositorySignatures/4.9.0 資源- [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - 現在將會在套件擷取期間建立 .nupkg.metadata 檔案 - 包含 "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - 在 Mono 上執行時跳過外掛程式的 Authenticode 驗證 - [#7222](https://github.com/NuGet/Home/issues/7222)

[此 4.9.0 版中修更的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>摘要: 4.9.1 中的新功能

* 新增透過新的命令受信任簽署者將寫入項目讀取到 nuget.config 的支援 - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

* 修正授權連結產生 - [#7515](https://github.com/NuGet/Home/issues/7515)

* 用於驗證簽章的錯誤碼迴歸 - [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack 套件沒有授權資訊 - [#7379](https://github.com/NuGet/Home/issues/7379)

[此 4.9.1 版本修正的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>摘要: 4.9.2 中的新功能

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

* 當來源名稱包含空格時，VS/dotnet.exe/nuget.exe/msbuild.exe 資源未使用認證 - [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow 與 LicenseFileWindow 協助工具問題 - [#7452](https://github.com/NuGet/Home/issues/7452)

* 修正 DateTime.Parse 中來自 DateTimeConverter 的 FormatException - [#7539](https://github.com/NuGet/Home/issues/7539)

[此 4.9.2 版本修正的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>摘要: 4.9.3 中的新功能

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>「使用鎖定檔案的可重複的套件還原」問題

* 針對先前的已快取套件，未以雜湊方式運作的鎖定模式計算錯誤 - [#7682](https://github.com/NuGet/Home/issues/7682)

* 還原會解析為與 `packages.lock.json` 檔案中所定義之版本不同的版本 - [#7667](https://github.com/NuGet/Home/issues/7667)

* '--locked-mode / RestoreLockedMode' 導致可疑的還原失敗 (當涉及 ProjectReferences 時) - [#7646](https://github.com/NuGet/Home/issues/7646)

* MSBuild SDK 解析程式嘗試驗證 SDK 套件的 SHA (在使用 packages.lock.json 時，此套件還原失敗) - [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>「使用可設定的信任原則鎖定您的相依性」問題
* 簽署不支援的套件時，dotnet.exe 不應該評估信任的簽署者 - [#7574](https://github.com/NuGet/Home/issues/7574)

* 設定檔中 trustedSigners 的順序會影響信任評估 - [#7572](https://github.com/NuGet/Home/issues/7572)

* 無法實作 ISettings [由重構 API 設定以支援信任原則功能引起] - [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>「改良的偵錯體驗」問題

* 無法為 .NET Core 全域工具發行符號套件 - [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>「自封式 NuGet 套件 - 授權」問題

* 使用內嵌授權檔案時，建置符號 .snupkg 套件發生錯誤 - [#7591](https://github.com/NuGet/Home/issues/7591)

[此 4.9.3 版本修正的所有問題清單](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>摘要: 4.9.4 中的新功能

* 安全性修正：在 ~/.nuget 內建立的檔案權限過於開放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>已知問題

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive 在 Mac 上發生錯誤。 - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>問題
`--interactive` 引數未由 dotnet cli 轉送並導致錯誤 `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>因應措施
使用互動式選項 (例如 `dotnet restore --interactive`) 執行任何其他 dotnet 命令並驗證。 驗證接著可能會由認證提供者快取。 接著，執行 `dotnet nuget push`。

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。 - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>問題
使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。 這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。

#### <a name="workaround"></a>因應措施
透過將 `RestoreAdditionalProjectSources` 設定為空無一物以停用後援資料夾的使用。 `<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。
