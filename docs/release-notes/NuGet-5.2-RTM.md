---
title: NuGet 5.2 RTM 版本資訊
description: NuGet 5.2 的版本資訊, 包括新功能、bug 修正和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471181"
---
# <a name="nuget-52-release-notes"></a>NuGet 5.2 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.2 版](https://visualstudio.microsoft.com/downloads/) | [2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝 

<sup>2</sup>以含 .NET Core 工作負載的 Visual Studio 2019 的選擇性安裝形式提供

## <a name="summary-whats-new-in-52"></a>摘要: 5.2 中的新功能

* 已修正因 Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)上的路徑問題而造成不定期進行 NuGet 作業失敗的嚴重錯誤 (bug)

* 改善使用中的 NuGet 套件管理員 UI 流覽套件時的 UI 回應性 Visual Studio 特別明顯用於緩慢的來源- [#8039](https://github.com/NuGet/Home/issues/8039)

* 鎖定檔案 ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) 和驗證外掛程式的大量可靠性修正 ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271](https://github.com/NuGet/Home/issues/8271)、[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)、[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 效能套件管理員主控台:UI 延遲更新 [預設專案] combobox 選取的值- [#8235](https://github.com/NuGet/Home/issues/8235)

* 效能PM UI 中的效能改進- [#8039](https://github.com/NuGet/Home/issues/8039)

* 效能在 PMC 中讀取預設專案時的 UI 延遲- [#6824](https://github.com/NuGet/Home/issues/6824)

* 效能: [vsfeedback] 本機套件來源的 [NuGet 更新] 索引標籤凍結- [#6470](https://github.com/NuGet/Home/issues/6470)

* 外掛程式如果外掛程式無法啟動或提早終止, NuGet 會等待完整的交握超時時間[#8300](https://github.com/NuGet/Home/issues/8300)

* 外掛程式: 改善外掛程式啟動失敗的診斷- [#8271](https://github.com/NuGet/Home/issues/8271)

* 外掛程式內建外掛程式的 nuget.exe 探索問題- [#8269](https://github.com/NuGet/Home/issues/8269)

* 外掛程式: 絕對不會讀取快取檔案[#8210](https://github.com/NuGet/Home/issues/8210)

* 外掛程式「工作已取消。」 還原期間驗證外掛程式的錯誤- [#8198](https://github.com/NuGet/Home/issues/8198)

* 在 linux 平臺上的外掛程式快取無法再發現- [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: 有了 ATF, 因為目標 framework 相等檢查不正確, 所以它有 false NU1004- [#8187](https://github.com/NuGet/Home/issues/8187)

* LockFile: 如果鎖定檔案是空的或格式不正確, 則不遵守「--鎖定模式」還原旗標- [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile:不使用封裝中的自訂群組件名稱進行小寫專案鎖定檔案- [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile:在鎖定檔案中讓專案參考小寫- [#7840](https://github.com/NuGet/Home/issues/7840)

* 還原: 安裝遭篡改的簽署套件會導致多次失敗的安裝嘗試 (具有重複的輸出)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: 在 NuGet 更新之後, 解決方案使用者選項無法還原序列化- [#8166](https://github.com/NuGet/Home/issues/8166)

* UnitTest 專案中的 dotnet-list 封裝會傳回錯誤- [#8154](https://github.com/NuGet/Home/issues/8154)

* 建立 VS 安裝程式的 NuGet 封裝群組-修正某些 VSIX 安裝問題- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild 不應設定 NoBuild。 - [#7801](https://github.com/NuGet/Home/issues/7801)

* 當 nuspec 檔案包含明確的元件參考元素時, 新選項 "-SymbolPackageFormat .snupkg" 會產生錯誤- [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. 目標 (498, 5): 錯誤:找不到路徑 '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)的一部分

**DCR：**

* 新增 msbuild 屬性, 指出支援 PackageDownload- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference 透過 FrameworkReference 隱藏相依性流程-PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* 在封裝外部提供執行時間 json 的機制- [#7351](https://github.com/NuGet/Home/issues/7351)

**[此版本-5.2 RTM 中已修正的所有問題清單](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


