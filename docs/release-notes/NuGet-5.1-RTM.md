---
title: NuGet 5.1 RTM 版本資訊
description: 其中包括新功能、 bug 修正和 Dcr NuGet 5.1 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842573"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.1 版](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>安裝的 Visual Studio 2019 是使用.NET Core 工作負載 

<sup>2</sup>與.NET Core 工作負載的 Visual Studio 2019 提供選擇性的安裝

## <a name="summary-whats-new-in-51"></a>摘要: 在 5.1 中最新消息

* 如果已經存在以允許與 CI/CD 工作流程-更緊密整合，請略過封裝推送支援[# 1630年](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio 現在提供方便的連結，以套件的 nuget.org 資源庫頁面- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* 這類支援.NET Core 3.0 的新資產[為目標的組件](https://github.com/dotnet/cli/issues/10006)和[執行階段組件](https://github.com/dotnet/cli/issues/10007)
  * 若要啟用目標和執行階段封裝參考-FrameworkReferences 支援 NuGet 封裝和還原[#7342](https://github.com/NuGet/Home/issues/7342)
  * 支援 「 只下載 」 套件案例 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * 排除的執行階段和目標從搜尋結果與還原的套件圖形使用 PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 外掛程式： 例外狀況詳細資料遺失期間外掛程式- [#8057](https://github.com/NuGet/Home/issues/8057)

* PackageReference 獨佔的下限範圍無法運作如果下限是存在的其中一個來源。 - [#8054](https://github.com/NuGet/Home/issues/8054)

* Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)

* 封裝鎖定檔案-重新產生的鎖定檔案的專案圖形變更時- [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem bug:Nuget 套件取得自動移除- [#8017](https://github.com/NuGet/Home/issues/8017)

* 新增的目標傳回 FrameworkReference 類似 CollectPackageDownloads 和 CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP 快取：RepositoryResources 資源不會快取版本控制的方式- [#7997](https://github.com/NuGet/Home/issues/7997)

* 記錄： 例外狀況呼叫堆疊不會報告與詳細等級- [#7955](https://github.com/NuGet/Home/issues/7955)

* 變更所有 NuGet Docs Url 使用 HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)

* 改善 NU3024 警告訊息- [#7933](https://github.com/NuGet/Home/issues/7933)

* 無法更新時鎖定檔案移除-packagereference [#7930](https://github.com/NuGet/Home/issues/7930)

* 驗證在 nuspec-licenseurl 和授權的項目時，改善錯誤案例處理[#7915](https://github.com/NuGet/Home/issues/7915)

* PM UI-以滑鼠右鍵按一下索引標籤行標頭，然後按一下 [開啟檔案位置] 會導致錯誤- [#7913](https://github.com/NuGet/Home/issues/7913)

* 外掛程式： 記錄外掛程式處理序結束-時[#7907](https://github.com/NuGet/Home/issues/7907)

* 外掛程式： 記錄的日期時間值中高衝突率[#7899](https://github.com/NuGet/Home/issues/7899)

* 任何 nuspec LicenseExpression-與失敗 Manifest.ReadFrom [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode:未預期的 NU1004 當參考的專案的自訂組件名稱-ProjectReference [#7889](https://github.com/NuGet/Home/issues/7889)

* 更好的錯誤訊息時外掛程式啟動失敗並發生例外狀況- [#7857](https://github.com/NuGet/Home/issues/7857)

* NoOp 還原時，避免 *。 在 obj 目錄-dgspec.json 寫入[#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true 無法產生屬性上大小寫不符- [#7843](https://github.com/NuGet/Home/issues/7843)

* 設定： 在 套件來源路徑不合法的字元可能會損毀 VS- [#7820](https://github.com/NuGet/Home/issues/7820)

* 如果刪除鎖定檔案時，還原不會產生鎖定檔案上 NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)

* 授權 URL 和授權讀取中繼資料-錯誤的原因[#7547](https://github.com/NuGet/Home/issues/7547)

* 未處理例外狀況中 V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe 會傳回無效的引數-的結束代碼為零[#7178](https://github.com/NuGet/Home/issues/7178)

* 更新 錯誤和警告文件以反映簽章的相關的案例- [#6498](https://github.com/NuGet/Home/issues/6498)

* 資產檔案應該使用相對路徑，來更輕鬆地-啟用移動專案[#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* 外掛程式： 啟用診斷記錄- [#7859](https://github.com/NuGet/Home/issues/7859)

* 請 Tizen 6 對應為 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[此版本為 5.1 RTM 修正的所有問題的清單](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
