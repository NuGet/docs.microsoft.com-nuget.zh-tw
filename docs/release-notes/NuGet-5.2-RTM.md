---
title: NuGet 5.2 RTM 版本資訊
description: NuGet 5.2 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776209"
---
# <a name="nuget-52-release-notes"></a>NuGet 5.2 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.2 版](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝 

<sup>2</sup>可透過 .NET Core 工作負載，以選用的方式安裝 Visual Studio 2019

## <a name="summary-whats-new-in-52"></a>摘要：5.2 中的新功能

* 修正因 Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)上的路徑問題而造成不定期 NuGet 作業失敗的嚴重錯誤

* 在 Visual Studio 中使用 NuGet 套件管理員 UI 流覽套件時，改善了 UI 回應性，特別是針對緩慢的來源- [#8039](https://github.com/NuGet/Home/issues/8039)

* 許多鎖定檔案的可靠性修正 ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) 和驗證外掛程式 ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271](https://github.com/NuGet/Home/issues/8271)、[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)#7845) [ ](https://github.com/NuGet/Home/issues/7845)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 效能：封裝管理員主控台： UI 延遲更新「預設專案」 combobox 選取的值- [#8235](https://github.com/NuGet/Home/issues/8235)

* 效能： PM UI 中的效能改進- [#8039](https://github.com/NuGet/Home/issues/8039)

* 效能：在 PMC 中讀取預設專案時的 UI 延遲- [#6824](https://github.com/NuGet/Home/issues/6824)

* 效能： [vsfeedback] 本機套件來源的 [NuGet 更新] 索引標籤凍結- [#6470](https://github.com/NuGet/Home/issues/6470)

* 外掛程式：如果外掛程式無法啟動或終止早期[#8300](https://github.com/NuGet/Home/issues/8300) ，NuGet 會等待完整的交握超時

* 外掛程式：改善外掛程式啟動失敗的診斷- [#8271](https://github.com/NuGet/Home/issues/8271)

* 外掛程式： nuget.exe 探索內建外掛程式的問題- [#8269](https://github.com/NuGet/Home/issues/8269)

* 外掛程式：快取檔案永遠不會讀取 [#8210](https://github.com/NuGet/Home/issues/8210)

* 外掛程式：「工作已取消」。 還原期間的驗證外掛程式發生錯誤- [#8198](https://github.com/NuGet/Home/issues/8198)

* 無法在 linux 平臺上間歇性探索外掛程式快取- [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile：使用 ATF 時，由於目標 framework 的相等[#8187](https://github.com/NuGet/Home/issues/8187)檢查不正確，所以會有 false NU1004

* LockFile：如果鎖定檔案是空的或格式不正確，則不遵守「--鎖定模式」還原旗標- [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile：在封裝中使用自訂群組件名稱的小寫專案會鎖定 file- [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile：讓專案參考在鎖定檔案中的小寫- [#7840](https://github.com/NuGet/Home/issues/7840)

* 還原：安裝已遭篡改的已簽署套件會導致多個失敗的安裝嘗試 (有重複的輸出) - [#8175](https://github.com/NuGet/Home/issues/8175)

* VS：方案使用者選項無法在 NuGet 更新後還原序列化- [#8166](https://github.com/NuGet/Home/issues/8166)

* UnitTest 專案中的 dotnet 清單套件會傳回錯誤 [#8154](https://github.com/NuGet/Home/issues/8154)

* 建立 VS 安裝程式的 NuGet 套件群組-修正某些 VSIX 安裝問題- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild 不應設定 NoBuild。 - [#7801](https://github.com/NuGet/Home/issues/7801)

* 當 nuspec 檔案包含明確元件參考元素時，新的選項 "-SymbolPackageFormat .snupkg" 會產生錯誤- [#7638](https://github.com/NuGet/Home/issues/7638)

* Nuget.exe (就是498，5) ：錯誤：找不到路徑 '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)的一部分

**DCR：**

* 新增表示支援 PackageDownload 的 msbuild 屬性- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference 透過 FrameworkReference 隱藏相依性流程。 PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* 在封裝之外提供 runtime.js的機制- [#7351](https://github.com/NuGet/Home/issues/7351)

**[此版本中所有已修正問題的清單-5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


