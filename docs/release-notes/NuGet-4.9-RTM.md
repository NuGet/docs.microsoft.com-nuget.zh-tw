---
title: NuGet 4.9 RTM 版本資訊
description: NuGet 4.9 版本資訊，包含已知問題、錯誤 (Bug) 修正、新功能與 DCR。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453768"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 版本資訊

[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 NuGet 4.9.0 功能。


相同的功能也有命令列版本可供使用：
* NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)
* dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-490"></a>摘要：4.9.0 的新功能

* 簽署：讓 ClientPolicies 要求使用 NuGet.Config 中所列的一組受信任作者與存放庫 - [#6961](https://github.com/NuGet/Home/issues/6961)

* 建立 ".snupkg" 檔案以在套件中包含符號 -- 加強推送以了解 nuget 通訊協定以接受符號伺服器的 snupkg 檔案 - [#6878](https://github.com/NuGet/Home/issues/6878)

* NuGet 認證外掛程式 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* 自封式 NuGet 套件 - 授權 - [#4628](https://github.com/NuGet/Home/issues/4628)

* 啟用 PackageReference 上的選擇性加入 "GeneratePathProperty" 中繼資料以產生每個套件的 MSBuild 屬性到 "Foo.Bar\1.0\" 目錄 - [#6949](https://github.com/NuGet/Home/issues/6949)

* 使用 NuGet 作業改進客戶成功 - [#7108](https://github.com/NuGet/Home/issues/7108)

### <a name="issues-fixed-in-this-release"></a>此版本已修正的問題

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

* DCR - 簽署：支援 NuGet 通訊協定：RepositorySignatures/4.9.0 資源 - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - 現在將會在套件擷取期間建立 .nupkg.metadata 檔案 - 包含 "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - 在 Mono 上執行時跳過外掛程式的 Authenticode 驗證 - [#7222](https://github.com/NuGet/Home/issues/7222)

[此 4.9.0 版中修更的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>摘要：4.9.1 的新功能

* 新增透過新的命令受信任簽署者將寫入項目讀取到 nuget.config 的支援 - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>此版本已修正的問題

* 修正授權連結產生 - [#7515](https://github.com/NuGet/Home/issues/7515)

* 用於驗證簽章的錯誤碼迴歸 - [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack 套件沒有授權資訊 - [#7379](https://github.com/NuGet/Home/issues/7379)

[此 4.9.1 版本修正的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a>已知問題

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a>當來源名稱包含空格時，dotnet.exe/nuget.exe 未使用認證 - [#7517](https://github.com/NuGet/Home/issues/7517)

#### <a name="issue"></a>問題
當來源名稱中包含空格時，nuget.exe 擲回如 `The ' ' character, hexadecimal value 0x20, cannot be included in a name.` 的錯誤

#### <a name="workaround"></a>因應措施
變更來源名稱，使其不包含空格。

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive 在 Mac 上發生錯誤。 - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>問題
`--interactive` 引數未由 dotnet cli 轉送並導致錯誤 `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>因應措施
使用互動式選項 (例如 `dotnet restore --interactive`) 執行任何其他 dotnet 命令並驗證。 驗證接著可能會由認證提供者快取。 接著，執行 `dotnet nuget push`。

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a>LicenseAcceptanceWindow 與 LicenseFileWindow 協助工具問題 - [#7452](https://github.com/NuGet/Home/issues/7452)

#### <a name="issue"></a>問題
授權接受視窗與授權檔案視窗有鍵盤瀏覽與使用螢幕助讀程式和 JAWS 朗讀方面的協助工具問題。

#### <a name="workaround"></a>因應措施
沒有因應措施。

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。 - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>問題
使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。 這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。

#### <a name="workaround"></a>因應措施
透過將 `RestoreAdditionalProjectSources` 設定為空無一物以停用後援資料夾的使用。 `<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。
