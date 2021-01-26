---
title: NuGet 5.1 RTM 版本資訊
description: NuGet 5.1 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780131"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.1 版](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝 

<sup>2</sup>可透過 .NET Core 工作負載，以選用的方式安裝 Visual Studio 2019

## <a name="summary-whats-new-in-51"></a>摘要：5.1 中的新功能

* 支援略過封裝推送（如果已存在），以提供更好的 CI/CD 工作流程整合- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio 現在提供了一個方便的連結，可連至套件的 [nuget.org 資源庫] 頁面- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* 支援新的 .NET Core 3.0 資產，例如 [目標套件](https://github.com/dotnet/cli/issues/10006) 和 [執行時間套件](https://github.com/dotnet/cli/issues/10007)
  * FrameworkReferences 的 NuGet 套件和還原支援，以啟用目標和執行時間封裝參考- [#7342](https://github.com/NuGet/Home/issues/7342)
  * 支援「僅下載」套件案例與 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * 使用 PackageType 從搜尋結果中排除執行時間和目標套件 & restore graph- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 外掛程式：在外掛程式建立期間遺失例外狀況詳細資料- [#8057](https://github.com/NuGet/Home/issues/8057)

* 如果其中一個來源上有下限，則具有獨佔下限的 PackageReference 範圍將無法運作。 - [#8054](https://github.com/NuGet/Home/issues/8054)

* 改善 IsPackableFalseError 訊息- [#8021](https://github.com/NuGet/Home/issues/8021)

* 封裝鎖定檔案-在專案圖形變更時重新產生鎖定檔案- [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem bug：取得自動移除的 Nuget 套件- [#8017](https://github.com/NuGet/Home/issues/8017)

* 新增傳回 FrameworkReference 的目標，類似于 CollectPackageDownloads 和 CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP 快取： RepositoryResources 資源不會以已設定版本的方式快取- [#7997](https://github.com/NuGet/Home/issues/7997)

* 記錄：未以詳細的詳細資訊[#7955](https://github.com/NuGet/Home/issues/7955)報告例外狀況呼叫堆疊

* 將所有 NuGet 檔 Url 變更為使用 HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)

* 改善 NU3024 警告訊息- [#7933](https://github.com/NuGet/Home/issues/7933)

* packagereference 移除時鎖定檔案未更新- [#7930](https://github.com/NuGet/Home/issues/7930)

* 改善在 nuspec 中驗證 licenseurl 和授權元素時的錯誤案例處理- [#7915](https://github.com/NuGet/Home/issues/7915)

* PM UI-以滑鼠右鍵按一下 tab 標頭，然後按一下 [開啟檔案位置] 會導致錯誤 [#7913](https://github.com/NuGet/Home/issues/7913)

* 外掛程式：當外掛程式進程結束時記錄- [#7907](https://github.com/NuGet/Home/issues/7907)

* 外掛程式：記錄日期時間值中的高衝突率- [#7899](https://github.com/NuGet/Home/issues/7899)

* 資訊清單。具有 LicenseExpression [#7894](https://github.com/NuGet/Home/issues/7894)的任何 nuspec 上的 system.xml.linq.xnode.readfrom 失敗

* RestoreLockedMode：當 ProjectReference 參考具有自訂 AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)的專案時，未預期的 NU1004

* 當外掛程式啟動失敗且發生例外狀況[#7857](https://github.com/NuGet/Home/issues/7857)時，會有更好的錯誤訊息

* 進行 NoOp 還原時，請避免在 obj 目錄中寫入 * .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true 無法在案例不符時產生屬性- [#7843](https://github.com/NuGet/Home/issues/7843)

* 設定：套件來源路徑中不合法的字元可能會損毀 VS- [#7820](https://github.com/NuGet/Home/issues/7820)

* 如果刪除鎖定檔案，restore 不會在 NoOp 上產生鎖定檔案- [#7807](https://github.com/NuGet/Home/issues/7807)

* 授權 URL 和授權會導致中繼資料的讀取錯誤- [#7547](https://github.com/NuGet/Home/issues/7547)

* V2FeedParser 中未處理的例外狀況- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe 傳回無效引數的結束代碼零- [#7178](https://github.com/NuGet/Home/issues/7178)

* 更新錯誤和警告檔以反映簽署相關案例- [#6498](https://github.com/NuGet/Home/issues/6498)

* 資產檔案應該使用相對路徑來更輕鬆地啟用移動專案- [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* 外掛程式：啟用診斷記錄- [#7859](https://github.com/NuGet/Home/issues/7859)

* 將 Tizen 6 對應到 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[此版本中所有已修正問題的清單-5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
