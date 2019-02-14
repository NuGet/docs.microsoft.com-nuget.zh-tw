---
title: NuGet 5.0 preview 版本資訊
description: 包括已知的問題、 bug 修正、 新功能和 Dcr NuGet 5.0 preview 版本資訊。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247655"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 Preview 版本資訊

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 Preview 版本

* 2019 年 2 月 13 日- [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)
* 2019 年 1 月 23 日- [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-3"></a>摘要: 什麼是 NuGet 5.0 Preview 3 的新功能

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題 

**錯誤：**

* nuget.exe /? 應該會列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5)： 錯誤：找不到的部分路徑 ' / tmp/NuGetScratch--在 mono 上[#7793](https://github.com/NuGet/Home/issues/7793)

* 還原不必要地列舉的所有版本的電腦快取中參照的套件內容[#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild 的自動偵測一律選取 16.0 之後安裝 VS 2019 預覽- [#7621](https://github.com/NuGet/Home/issues/7621)

* 在方案上的 dotnet 列出封裝輸出的架構-重複的項目[#7607](https://github.com/NuGet/Home/issues/7607)

* 例外狀況 「 空的路徑名稱不合法 」 呼叫 IVsPackageInstaller.InstallPackage 舊專案，並封裝資料夾不存在。 - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t: restore 最少的詳細資訊應該很多小- [#4695](https://github.com/NuGet/Home/issues/4695)

**DCRs**

* 讓套件作者可以定義建置的資產轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)

* 在成功的專案不是方案的一部分或未載入，但先前已還原-VS 中啟用還原[#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>摘要: 什麼是 5.0 Preview 2 的新功能

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**錯誤：**

* VS 16.0 的 NuGet UI 有無法讀取的索引標籤色彩的問題-由於[#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt 釐清- [#7629](https://github.com/NuGet/Home/issues/7629)

* 還原不必要地列舉全域套件資料夾，在嘗試判定類型- [#7596](https://github.com/NuGet/Home/issues/7596)

* 鎖定檔案強制執行中的錯誤應該會顯示在錯誤清單 視窗- [#7429](https://github.com/NuGet/Home/issues/7429)

* 修正 NuGet.Configuration 問題- [#7326](https://github.com/NuGet/Home/issues/7326)

* 適應 MSBuild 更新它的安裝位置。  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)

* 新增組件擴充點，包括偵錯符號- [#7234](https://github.com/NuGet/Home/issues/7234)

* dotnet 套件應該保留在建立 nupkg 中的相依性版本範圍。 （即使使用浮動版本）- [#7232](https://github.com/NuGet/Home/issues/7232)

* dotnet 還原會失敗已驗證的來源上，當使用者層級組態也會有原始檔- [#7209](https://github.com/NuGet/Home/issues/7209)

* 組件應該不會限制內容的檔案-BuildActions 集[#7155](https://github.com/NuGet/Home/issues/7155)

* 使用 projectreference 需要 AssetTargetFallback 才會成功，應該發出警告。 - [#7137](https://github.com/NuGet/Home/issues/7137)

* 由於執行緒的問題，當呼叫 CPS (CommonProjectSystem)-死結[#7103](https://github.com/NuGet/Home/issues/7103)

* dotnet 新增套件不會使用本機組態檔-中指定的來源的認證，從全域設定[#6935](https://github.com/NuGet/Home/issues/6935)

* 執行緒處理問題與 MEF 所呼叫的非同步程式碼路徑- [#6771](https://github.com/NuGet/Home/issues/6771)

* 簽章： 錯誤報告兩次，而不呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)

* 安裝已簽署的封裝使用未受信任的簽章憑證應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet 還原不正確 Noop 時 2 個專案共用 obj 目錄- [#6114](https://github.com/NuGet/Home/issues/6114)

* 無法使用 Linux 上的 dotnet restore，有來自已驗證的摘要-套件 PAT [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet 還原失敗，因為已停用全機器摘要- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* NuGet 5.0 組件 （透過 TFM 變化）-需要.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)

* 從 NuGet.Packaging NuGetLicenseData 應該是公用型別。 更新 spdx 從內嵌的授權中繼資料。 - [#7471](https://github.com/NuGet/Home/issues/7471)

* 移除過時的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)

* 因應措施 1 的系統上的還原逾時 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet 偏好 NTLM 驗證，即使在 NuGet.config 中認證-config 選項加入篩選驗證類型，認證- [#5286](https://github.com/NuGet/Home/issues/5286)

* 啟用 EmbedInteropTypes packagereference （比對 Packages.Config 功能）- [# 2365年](https://github.com/NuGet/Home/issues/2365)

[在此版本 5.0.0-preview2 中修正的所有問題的清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>已知問題

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive 在 Mac 上發生錯誤。 - [#7519](https://github.com/NuGet/Home/issues/7519)
**問題**`--interactive`引數不轉送 dotnet cli 和錯誤會導致`error: Missing value for option 'interactive'` 
**因應措施**以互動式的選項，例如執行任何其他的dotnet命令`dotnet restore --interactive`並進行驗證。 驗證接著可能會由認證提供者快取。 接著，執行 `dotnet nuget push`。

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。 - [#7414](https://github.com/NuGet/Home/issues/7414)
**問題**使用 dotnet.exe 時還原專案的多重目標 netcoreapp 2.x 1.x 和 netcoreapp 2.x，後援的資料夾會被視為檔案摘要。 這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。
**因應措施**停用的後援的資料夾使用方式設定`RestoreAdditionalProjectSources`為 nothing。 `<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。
