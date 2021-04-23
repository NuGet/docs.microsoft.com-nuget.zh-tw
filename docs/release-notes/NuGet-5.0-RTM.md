---
title: NuGet 5.0 RTM 版本資訊
description: NuGet 5.0 的版本資訊，包含已知問題、bug 修正、新功能及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901742"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.0 版](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2 版**](https://nuget.org/downloads) | [Visual Studio 2019 版本16.0.4 版](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝 

<sup>2</sup>可透過 .NET Core 工作負載，以選用的方式安裝 Visual Studio 2019

## <a name="summary-whats-new-in-50"></a>摘要：5.0 中的新功能

* 支援在 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)中還原已[篩選的解決方案](/visualstudio/ide/filtered-solutions)
* `BuildTransitive` 資料夾可讓套件以可傳遞的目標/.props 給主項目目- [#6091](https://github.com/NuGet/Home/issues/6091)
* 針對 NuGet Iv Api 中的 PackageReference 案例提供更佳的支援- [#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` 已淘汰- [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 認證提供者外掛程式已由 [gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) 取代，即將淘汰- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 進行 NoOp 還原時，請避免在 obj 目錄中寫入 * .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854)

* 在 ~/.nuget 內建立之檔案的許可權太開啟- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated`不適用於需要驗證[#7605](https://github.com/NuGet/Home/issues/7605)的來源

* VisualStudio：在沒有套件參考的專案上呼叫一律會使用 packages.config，即使預設值設定為 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC： Update-Package 重新安裝失敗 ( delisted 套件上的「找不到套件」 ) 。 - [#7268](https://github.com/NuGet/Home/issues/7268)

* 在我們的存放庫和 VSIX 中新增協力廠商通知- [#7409](https://github.com/NuGet/Home/issues/7409)

* 如果未指定任何版本，則 VisualStudio 應該安裝最新版本- [#7493](https://github.com/NuGet/Home/issues/7493)

* --dotnet nuget push [#7519](https://github.com/NuGet/Home/issues/7519)的互動式支援

* 使用鎖定檔案還原時，不應該引發 NU1603 警告。 - [#7529](https://github.com/NuGet/Home/issues/7529)

* 在還原期間，NuGet 不應使用基本記錄來列印專案路徑- [#7647](https://github.com/NuGet/Home/issues/7647)

* --dotnet 的互動式支援移除套件- [#7727](https://github.com/NuGet/Home/issues/7727)

* 使用 TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)來新增後置 NuGet

* plugins_cache 需要較短的路徑，才能順利運作- [#7770](https://github.com/NuGet/Home/issues/7770)

* 如果使用者未要求特定的 msbuild 版本，則偏好使用 msbuild 探索路徑- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 應列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)

* Nuget.exe (就是498，5) ：錯誤：找不到路徑 '/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)的部分

* 還原不必要地列舉電腦快取中參考封裝的所有版本內容- [#7639](https://github.com/NuGet/Home/issues/7639)

* 在安裝 VS 2019 Preview 之後，MSBuild 自動偵測一律會選取 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)

* 解決方案的 dotnet 清單套件會輸出架構[#7607](https://github.com/NuGet/Home/issues/7607)的重複專案

* 在舊專案上呼叫 IVsPackageInstaller 時，例外狀況「空的路徑名稱不合法」，且套件資料夾不存在。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild/t：還原的詳細程度應更低 [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 的 NuGet UI 由於色彩問題而無法讀取索引標籤- [#7735](https://github.com/NuGet/Home/issues/7735)

* Nuget.exe & NuGet. 用戶端 License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)

* 還原非必要的列舉全域封裝資料夾，以嘗試判斷類型 [#7596](https://github.com/NuGet/Home/issues/7596)

* [錯誤清單] 視窗中會顯示鎖定檔案強制執行的錯誤- [#7429](https://github.com/NuGet/Home/issues/7429)

* 修正 NuGet.Configuration 問題- [#7326](https://github.com/NuGet/Home/issues/7326)

* 適應 MSBuild 更新其安裝位置- [#7325](https://github.com/NuGet/Home/issues/7325)

* Nuget.exe 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)

* 新增套件擴充點以包含 debug 符號- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` 應該保留所建立之 nupkg (中的相依性版本範圍，即使是使用浮動版本) [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore`當使用者層級設定也有來源[#7209](https://github.com/NuGet/Home/issues/7209)時，已驗證的來源上會失敗

* 套件不應限制內容檔案的 BuildActions 集- [#7155](https://github.com/NuGet/Home/issues/7155)

* 使用需要 AssetTargetFallback 成功的 ProjectReference 時，應該發出警告。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* 呼叫 CPS (CommonProjectSystem) [#7103](https://github.com/NuGet/Home/issues/7103)時，因執行緒問題而造成鎖死

* `dotnet add package` 針對本機設定中指定的來源，不使用全域設定的認證- [#6935](https://github.com/NuGet/Home/issues/6935)

* 在非同步程式碼路徑上呼叫 MEF 的執行緒問題- [#6771](https://github.com/NuGet/Home/issues/6771)

* 簽署：錯誤報表兩次且沒有呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)

* 安裝具有未受信任簽署憑證的已簽署套件應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)

* 當2個專案共用[#6114](https://github.com/NuGet/Home/issues/6114)的 obj 目錄時，NuGet 還原不當 NoOps

* 無法在 Linux 上搭配使用 PAT 與 `dotnet restore` 已驗證摘要的套件- [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore 因為已停用電腦寬摘要而失敗- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* 未來移除「dotnet pack project.js」的警告- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* 新增 Gen1 認證外掛程式的取代警告- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* 簽署：已啟用存放庫，以要求每個套件的用戶端驗證（以存放庫簽署）--via RepositorySignatures/5.0.0 資源- [#7759](https://github.com/NuGet/Home/issues/7759)

* 透過 NuGet.Config [#4538](https://github.com/NuGet/Home/issues/4538)限制每個來源的 HTTP 要求號碼

* NuGet 應以 Net472 (為目標，以協助清理 VSIX) 的16.0 組建 [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC： Remove OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)

* 將 NetCoreApp 3.0 對應到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)

* 將 netstandard 2.0 支援新增至 NuGet. * 套件- [#6516](https://github.com/NuGet/Home/issues/6516)

* 允許封裝作者定義組建資產的可轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)

* 支援 VS 2019 解決方案篩選功能。 也支援不在方案中的專案，或已卸載的專案。 需要透過 CLI 或 VS) first [#5820](https://github.com/NuGet/Home/issues/5820)還原完整的解決方案 (

* 需要 .NET 4.7.2 的 NuGet 5.0 元件 (via TFM 變更) - [#7510](https://github.com/NuGet/Home/issues/7510)

* 從 NuGet NuGetLicenseData。封裝應該是公用類型。 更新來自 spdx 的授權中繼資料內嵌。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 移除淘汰的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 因應措施：在具有1個 cpu [#6742](https://github.com/NuGet/Home/issues/6742)的系統上還原超時

* 即使有 NuGet.config-新增設定選項中的認證可篩選認證的驗證類型，NuGet 仍優先于 NTLM 驗證- [#5286](https://github.com/NuGet/Home/issues/5286)

* 啟用 EmbedInteropTypes for PackageReference (符合 Packages.Config 功能) - [#2365](https://github.com/NuGet/Home/issues/2365)

**[此版本中所有已修正問題的清單-5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>摘要：5.0.2 版的新功能

* 透過 dotnet.exe 或 mono.exe) 執行時的安全性 (-應使用正確的許可權建立 obj 資料夾 [#7908](https://github.com/NuGet/Home/issues/7908)

* nuget.exe mono/MacOS 上的還原失敗，自訂 nuget.config 和 `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>已知問題

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。 - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>問題
使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。 這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。<br>
#### <a name="workaround"></a>因應措施
將設定為 [無]，以停用 [回溯] 資料夾的使用方式 `RestoreAdditionalProjectSources` ：

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

請小心使用此方法，因為將會從 NuGet.org 下載將從回溯資料夾還原的封裝。