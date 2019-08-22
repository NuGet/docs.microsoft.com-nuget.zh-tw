---
title: NuGet 4.7 RTM 版本資訊
description: NuGet 4.7.0 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: fe769f95e3eda4bc07db4369544472c00b35363d
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488646"
---
# <a name="nuget-47-release-notes"></a>NuGet 4.7 版本資訊

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)。

## <a name="summary-whats-new-in-470"></a>摘要: 4.7.0 中的新功能

* 我們已增強套件簽署，以啟用[存放庫簽署套件](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* Visual Studio Version 15.7 引進了一個功能，[讓使用 packages.config 格式的現有專案移轉成改為使用 PackageReference](https://docs.microsoft.com/en-us/nuget/consume-packages/migrate-packages-config-to-package-reference)。

## <a name="summary-whats-new-in-472"></a>摘要: 4.7.2 中的新功能

* 安全性修正：在 ~/.nuget 內建立的檔案權限過於開放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>摘要: 4.7.3 中的新功能

* 安全性修正：NUPKG 內的檔案可以有 NUPKG 目錄上層的相對路徑 [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>已知問題

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

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題

.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。 [這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。

## <a name="top-issues-fixed-in-this-release"></a>本版修正的主要問題

### <a name="bugs"></a>Bug

* NuGet 在 .Net Core 專案系統 (新迴歸) 中會進入死結。 - [#6733](https://github.com/NuGet/Home/issues/6733) \(英文\)
* 套件：如果搭配使用 TfmSpecificPackageFile 和萬用字元路徑，PackagePath 的建構會不正確 - [#6726](https://github.com/NuGet/Home/issues/6726)
* 套件：除非明確地設定 ispackable，否則 Web API 無法建立套件。 - [#6156](https://github.com/NuGet/Home/issues/6156) \(英文\)
* VS UI 和 PMC 花費 30 分鐘查看新的套件 (nuget.exe 可立刻查看) - [#6657](https://github.com/NuGet/Home/issues/6657) \(英文\)
* 簽署：SignatureUtility.GetCertificateChain(...) 不會檢查所有鏈結狀態 - [#6565](https://github.com/NuGet/Home/issues/6565)
* 簽署：改善 DER GeneralizedTime 處理 - [#6564](https://github.com/NuGet/Home/issues/6564) \(英文\)
* 簽署：安裝遭竄改的套件時，VS 不會顯示 NU3002 錯誤 - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary 會區分大小寫 - [#6500](https://github.com/NuGet/Home/issues/6500) \(英文\)
* 安裝/更新還原程式碼和還原程式碼路徑不一致 - [#3471](https://github.com/NuGet/Home/issues/3471) \(英文\)
* 方案 PackageManager 版本 ComboBox 可以透過鍵盤選取分隔符號 - [#2606](https://github.com/NuGet/Home/issues/2606) \(英文\)
* 無法載入來源 `https://www.myget.org/F/<id>` 的服務索引 ---> System.Net.Http.HttpRequestException：回應狀態碼未指出成功：403 (禁止) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* 跨要求發出 X-NuGet-Session-Id 標頭以進行相互關聯 [功能建議] - [#5330](https://github.com/NuGet/Home/issues/5330) \(英文\)
* 針對在 Visual Studio 中透過 IVs API 執行還原作業時，公開等候執行的方式。 - [#6029](https://github.com/NuGet/Home/issues/6029) \(英文\)
* NuGet.exe -NoServiceEndpoint 會避免附加服務 URL 尾碼 - [#6586](https://github.com/NuGet/Home/issues/6586) \(英文\)
* 新增認可雜湊至資訊版本 - [#6492](https://github.com/NuGet/Home/issues/6492) \(英文\)
* 簽署：啟用移除存放庫簽章/副署 - [#6646](https://github.com/NuGet/Home/issues/6646) \(英文\)
* 簽署：刪除存放庫簽章/副署的 API - [#6589](https://github.com/NuGet/Home/issues/6589)
* VS 中的記錄來源 - [#6527](https://github.com/NuGet/Home/issues/6527) \(英文\)
* 只在 TFM 和 RID 上篩選 /tools，所以設定 XML 可以放在 /tools 資料夾中 - [#6197](https://github.com/NuGet/Home/issues/6197) \(英文\)
* 當 Pack 命令排除開頭為 . 的檔案時發出警告  - [#3308](https://github.com/NuGet/Home/issues/3308) \(英文\)

[本版修正的所有問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
