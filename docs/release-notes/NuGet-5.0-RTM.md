---
title: NuGet 5.0 RTM 版本資訊
description: 包括已知的問題、 bug 修正、 新功能和 Dcr NuGet 5.0 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921581"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>安裝的 Visual Studio 2019 是使用.NET Core 工作負載 

<sup>2</sup>與.NET Core 工作負載的 Visual Studio 2019 提供選擇性的安裝

## <a name="summary-whats-new-in-50"></a>摘要: 什麼是 5.0 的新功能

* 支援還原[篩選解決方案](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019)在 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` 資料夾可讓封裝以可轉移方式參與目標 /props 至主應用程式專案- [#6091](https://github.com/NuGet/Home/issues/6091)
* 更妥善支援適合在 NuGet Iv Api-PackageReference [#7005](https://github.com/NuGet/Home/issues/7005)， [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)
* 層代 1 的認證提供者外掛程式已被取代[Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin)且即將被取代- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* NoOp 還原時，避免 *。 在 obj 目錄-dgspec.json 寫入[#7854](https://github.com/NuGet/Home/issues/7854)

* ~/.Nuget 內建立檔案的權限會太開啟- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 不適用於需要驗證-來源[#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller-求助於未封裝的專案參考一律會使用 packages.config，即使預設設定為 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC:更新套件重新取消列入套件安裝失敗 （「 無法找到的套件 」）。 - [#7268](https://github.com/NuGet/Home/issues/7268)

* 在我們的存放庫和 VSIX 內-新增第三方注意事項[#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage 應該安裝最新版本時指定-任何版本[#7493](https://github.com/NuGet/Home/issues/7493)

* -dotnet nuget push 互動式支援- [#7519](https://github.com/NuGet/Home/issues/7519)

* 還原時鎖定檔案，就不應該引發 NU1603 警告。 - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet 不應該使用最低限度記錄-還原期間會列印專案路徑[#7647](https://github.com/NuGet/Home/issues/7647)

* -dotnet 提供互動式支援移除封裝- [#7727](https://github.com/NuGet/Home/issues/7727)

* 新增與 TypeForwardedTo attrs-回 NuGet.Packaging.Core [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache 需要短的路徑無法正常運作- [#7770](https://github.com/NuGet/Home/issues/7770)

* 偏好使用 msbuild 探索的路徑，如果使用者未要求特定的 msbuild 版本- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 應該會列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5)： 錯誤：找不到的部分路徑 ' / tmp/NuGetScratch--在 mono 上[#7793](https://github.com/NuGet/Home/issues/7793)

* 還原不必要地列舉的所有版本的電腦快取中參照的套件內容[#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild 的自動偵測一律選取 16.0 之後安裝 VS 2019 預覽- [#7621](https://github.com/NuGet/Home/issues/7621)

* 在方案上的 dotnet 列出封裝輸出的架構-重複的項目[#7607](https://github.com/NuGet/Home/issues/7607)

* 例外狀況 「 空的路徑名稱不合法 」 呼叫 IVsPackageInstaller.InstallPackage 舊專案，並封裝資料夾不存在。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t: restore 最少的詳細資訊應該很多小- [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 的 NuGet UI 有無法讀取的索引標籤色彩的問題-由於[#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt 釐清- [#7629](https://github.com/NuGet/Home/issues/7629)

* 還原不必要地列舉全域套件資料夾，在嘗試判定類型- [#7596](https://github.com/NuGet/Home/issues/7596)

* 鎖定檔案強制執行中的錯誤應該會顯示在錯誤清單 視窗- [#7429](https://github.com/NuGet/Home/issues/7429)

* 修正 NuGet.Configuration 問題- [#7326](https://github.com/NuGet/Home/issues/7326)

* 適應 MSBuild 更新其安裝位置- [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)

* 新增組件擴充點，包括偵錯符號- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` 應該保留在建立 nupkg 中的相依性版本範圍 （即使使用浮動版本）- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` 失敗時使用者層級組態也會有原始檔-已驗證的來源[#7209](https://github.com/NuGet/Home/issues/7209)

* 組件應該不會限制內容的檔案-BuildActions 集[#7155](https://github.com/NuGet/Home/issues/7155)

* 使用 ProjectReference 需要 AssetTargetFallback 才會成功，應該發出警告。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* 由於執行緒的問題，當呼叫 CPS (CommonProjectSystem)-死結[#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` 不使用認證，從全域設定本機設定-中指定的來源[#6935](https://github.com/NuGet/Home/issues/6935)

* MEF 上非同步呼叫的執行緒問題的程式碼路徑- [#6771](https://github.com/NuGet/Home/issues/6771)

* 簽章： 錯誤報告兩次，而不呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)

* 安裝已簽署的封裝使用未受信任的簽章憑證應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet 還原不正確 Noop 時 2 個專案共用 obj 目錄- [#6114](https://github.com/NuGet/Home/issues/6114)

* 無法使用與 PAT`dotnet restore`在 Linux 上使用來自已驗證的摘要-套件[#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet 還原失敗，因為已停用全機器摘要- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* 未來移除"dotnet pack project.json-"，即發出警告[#7928](https://github.com/NuGet/Home/issues/7928)
 
* 新增取代警告 Gen1 認證外掛程式- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* 簽署：已啟用的存放庫，以要求為存放庫的用戶端驗證的每個套件簽署-透過 RepositorySignatures/5.0.0 資源- [#7759](https://github.com/NuGet/Home/issues/7759)

* 每個來源 NuGet.Config-透過 http 要求數目限制[#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet 應為目標 （以協助清除 VSIX 16.0 組建） Net472- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC:移除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)

* 請 NetCoreApp 3.0 對應為 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)

* 將 netstandard2.0 支援新增至 NuGet.* 封裝- [#6516](https://github.com/NuGet/Home/issues/6516)

* 讓套件作者可以定義建置的資產轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)

* 支援 VS 2019 方案篩選功能。 也支援不在方案中，專案或卸載的專案。 需要先還原完整的解決方案 （透過 CLI 或 VS） [#5820](https://github.com/NuGet/Home/issues/5820)

* NuGet 5.0 組件 （透過 TFM 變化）-需要.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)

* 從 NuGet.Packaging NuGetLicenseData 應該是公用型別。 更新 spdx 從內嵌的授權中繼資料。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 移除過時的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 因應措施 1 的系統上的還原逾時 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet 偏好 NTLM 驗證，即使在 NuGet.config 中認證-config 選項加入篩選驗證類型，認證- [#5286](https://github.com/NuGet/Home/issues/5286)

* 啟用 EmbedInteropTypes packagereference （比對 Packages.Config 功能）- [# 2365年](https://github.com/NuGet/Home/issues/2365)

**[此版本為 5.0 RTM 修正的所有問題的清單](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a>已知問題

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。 - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>問題
使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。 這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。<br>
#### <a name="workaround"></a>因應措施
停用的後援的資料夾使用方式設定`RestoreAdditionalProjectSources`沒有任何字元：

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

這個謹慎使用，現在會從 NuGet.org 下載會從後援資料夾還原的套件。
