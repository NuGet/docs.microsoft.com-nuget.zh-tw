---
title: NuGet 5.0 RTM 版本資訊
description: NuGet 5.0 的版本資訊，包括已知問題、bug 修正、新功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 52c71c6fe1a1854d5aed229abf2ce7ddc2685ae9
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611332"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.0 版](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2 版**](https://nuget.org/downloads) | [Visual Studio 2019 版本16.0.4 版](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝 

<sup>2</sup>以含 .NET Core 工作負載的 Visual Studio 2019 的選擇性安裝形式提供

## <a name="summary-whats-new-in-50"></a>摘要：5.0 中的新功能

* 支援在 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)中還原已[篩選的解決方案](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019)
* `BuildTransitive` 資料夾可讓封裝以可轉移的目標/.props 傳遞至主項目目- [#6091](https://github.com/NuGet/Home/issues/6091)
* 針對 NuGet Iv Api 中的 PackageReference 案例提供更佳的支援- [#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` 已被取代- [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 認證提供者外掛程式已由[gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin)取代，即將淘汰- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 執行 NoOp 還原時，請避免在 obj 目錄中使用 *. dgspec. json write- [#7854](https://github.com/NuGet/Home/issues/7854)

* 在 ~/.nuget 內建立之檔案的許可權太過開啟- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 無法與需要驗證[#7605](https://github.com/NuGet/Home/issues/7605)的來源搭配使用

* VisualStudio. IVsPackageInstaller-在沒有封裝參考的專案上呼叫時，一律會使用 package，即使預設值是設定為 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC：在 delisted 套件上，更新-套件重新安裝失敗（「找不到套件」）。 - [#7268](https://github.com/NuGet/Home/issues/7268)

* 在我們的存放庫和 VSIX 中新增協力廠商注意事項- [#7409](https://github.com/NuGet/Home/issues/7409)

* 若未指定任何版本，則 InstallPackage 應該安裝最新版本[#7493](https://github.com/NuGet/Home/issues/7493)

* --dotnet nuget push [#7519](https://github.com/NuGet/Home/issues/7519)的互動式支援

* 使用鎖定檔案還原時，不應該引發 NU1603 警告。 - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet 在還原期間不應使用最少的記錄來列印專案路徑- [#7647](https://github.com/NuGet/Home/issues/7647)

* --dotnet 移除封裝的互動式支援- [#7727](https://github.com/NuGet/Home/issues/7727)

* 使用 TypeForwardedTo attrs 新增後置 NuGet. 封裝- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache 需要較短的路徑才能順利運作- [#7770](https://github.com/NuGet/Home/issues/7770)

* 如果使用者未要求特定 msbuild 版本，則偏好使用 msbuild 探索的路徑- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 應該列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet .targets （498，5）：錯誤：在 mono 上找不到路徑 '/tmp/NuGetScratch 的一部分- [#7793](https://github.com/NuGet/Home/issues/7793)

* 還原會不必要地列舉電腦快取中所有版本參考套件的內容- [#7639](https://github.com/NuGet/Home/issues/7639)

* 在安裝 VS 2019 Preview 之後，MSBuild 自動偵測一律會選取 16.0- [#7621](https://github.com/NuGet/Home/issues/7621)

* 解決方案的 dotnet 清單套件會輸出架構的重複專案- [#7607](https://github.com/NuGet/Home/issues/7607)

* 在舊專案上呼叫 IVsPackageInstaller 時，例外狀況「空的路徑名稱不合法」，而且封裝資料夾不存在。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild/t：還原最少詳細資訊應該更少- [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 的 NuGet UI 因為色彩問題而無法讀取索引標籤- [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet & NuGet。用戶端授權 .txt- [#7629](https://github.com/NuGet/Home/issues/7629)

* 還原不必要地列舉全域封裝資料夾，以嘗試判斷類型[#7596](https://github.com/NuGet/Home/issues/7596)

* [鎖定檔案強制] 中的錯誤應該會顯示在錯誤清單] 視窗中- [#7429](https://github.com/NuGet/Home/issues/7429)

* 修正 NuGet。設定問題- [#7326](https://github.com/NuGet/Home/issues/7326)

* 適應 MSBuild 更新其安裝位置- [#7325](https://github.com/NuGet/Home/issues/7325)

* Nuget.exe 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)

* 新增包含偵錯工具符號的套件擴充點- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` 應該在所建立的 nupkg 中保留相依性版本範圍（即使使用浮動版本）- [#7232](https://github.com/NuGet/Home/issues/7232)

* 當使用者層級設定也具有來源[#7209](https://github.com/NuGet/Home/issues/7209)時，`dotnet restore` 在已驗證的來源上失敗

* 套件不應限制內容檔案的 BuildActions 集- [#7155](https://github.com/NuGet/Home/issues/7155)

* 使用需要 AssetTargetFallback 成功的 ProjectReference，應該會發出警告。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* 因呼叫 CPS （CommonProjectSystem）時的執行緒問題而造成鎖死- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` 不會針對本機設定中指定的來源使用全域設定中的認證- [#6935](https://github.com/NuGet/Home/issues/6935)

* 在非同步程式碼路徑上呼叫 MEF 的執行緒問題- [#6771](https://github.com/NuGet/Home/issues/6771)

* 簽署：錯誤報表兩次，但沒有呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)

* 安裝具有不受信任簽署憑證的已簽署套件時，應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)

* 當2個專案共用 obj 目錄時，NuGet 還原不當 NoOps- [#6114](https://github.com/NuGet/Home/issues/6114)

* 無法在 Linux 上使用具有來自已驗證摘要之套件的 PAT 與 `dotnet restore` [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore 因為已停用的整部電腦的饋送而失敗- [#5410](https://github.com/NuGet/Home/issues/5410)

**Dcr**

* 未來移除「dotnet pack 專案. json」的警告- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* 新增 Gen1 認證外掛程式的取代警告- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* 簽署：啟用存放庫，以要求每個套件的用戶端驗證做為已簽署的存放庫--透過 RepositorySignatures/5.0.0 資源- [#7759](https://github.com/NuGet/Home/issues/7759)

* 透過 Nuget.exe 限制每個來源的 HTTP 要求數目- [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet 應以 Net472 為目標（以協助清除 VSIX 的16.0 組建）- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC： Remove OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)

* 將 NetCoreApp 3.0 對應到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)

* 將 netstandard 2.0 支援新增至 NuGet. * 套件- [#6516](https://github.com/NuGet/Home/issues/6516)

* 允許套件作者定義組建資產可轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)

* 支援 VS 2019 解決方案篩選功能。 也支援不在方案中的專案或卸載的專案。 需要還原完整的解決方案（透過 CLI 或 VS） first- [#5820](https://github.com/NuGet/Home/issues/5820)

* 需要 .NET 4.7.2 的 NuGet 5.0 元件（經由 TFM 變更）- [#7510](https://github.com/NuGet/Home/issues/7510)

* 從 NuGet NuGetLicenseData。封裝應該是公用類型。 從 spdx 更新授權中繼資料內嵌。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 移除過時的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 解決具有1個 cpu [#6742](https://github.com/NuGet/Home/issues/6742)之系統上的還原超時的因應措施

* 即使 Nuget.exe 中有認證，NuGet 也偏好 NTLM 驗證-新增設定選項以篩選認證的驗證類型- [#5286](https://github.com/NuGet/Home/issues/5286)

* 啟用 PackageReference 的 EmbedInteropTypes （符合的封裝 .Config 功能）- [#2365](https://github.com/NuGet/Home/issues/2365)

**[此版本-5.0 RTM 中已修正的所有問題清單](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>摘要：5.0.2 版的新功能

* 安全性（當透過 dotnet 或 mono 執行時）-應該使用正確的許可權建立 obj 資料夾[#7908](https://github.com/NuGet/Home/issues/7908)

* mono/MacOS 上的 nuget.exe 還原因自訂的 nuget.exe 和 `PackageSignatureValidity: False` 而失敗[#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>已知問題

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。 - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>問題
使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。 這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。<br>
#### <a name="workaround"></a>因應措施
將 [`RestoreAdditionalProjectSources`] 設定為 [無]，以停用 fallback 資料夾的使用方式：

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

請謹慎使用，因為從回溯資料夾還原的套件現在會從 NuGet.org 下載。
