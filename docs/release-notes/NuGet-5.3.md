---
title: NuGet 5.3 版本資訊
description: NuGet 5.3 的版本資訊，包括新功能、bug 修正和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774098"
---
# <a name="nuget-53-release-notes"></a>NuGet 5.3 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.3.0-preview3**](https://nuget.org/downloads) | [Visual Studio 2019 16.3 版 Preview 3](https://visualstudio.microsoft.com/vs/preview/) | [3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |

<sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝

## <a name="summary-whats-new-in-53-preview-3"></a>摘要: 5.3 preview 3 的新功能

* [封裝圖示可以內嵌在封裝中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而不需要外部 URL。 - [#352](https://github.com/NuGet/Home/issues/352)

* 針對封裝進行 SHA 追蹤和強制執行的增強安全性- [#7281](https://github.com/NuGet/Home/issues/7281)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* VS：元件完全是 ngen-ed，不是部分 ngen [#8513](https://github.com/NuGet/Home/issues/8513)

* 減少記憶體使用量（取消訂閱事件）- [#8471](https://github.com/NuGet/Home/issues/8471)

* "Error_UnableToFindProjectInfo" 訊息的語法不正確- [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 改進-驗證所有套件，包括預期/實際的 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)

* NuGetPackageManager 中的多個列舉： PreviewUpdatePackagesAsync- [#8401](https://github.com/NuGet/Home/issues/8401)

* 還原 PluginProcess 中的「公用 > 內部」變更- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. GetSources （...）定義錯誤的例外狀況行為- [#8383](https://github.com/NuGet/Home/issues/8383)

* 再次將 PluginManager 的函式設為公用- [#8379](https://github.com/NuGet/Home/issues/8379)

* 追蹤 PM UI 的重新整理頻率的計量- [#8369](https://github.com/NuGet/Home/issues/8369)

* 透過套件管理員 UI 安裝時，減少 UI 重新整理的次數- [#8358](https://github.com/NuGet/Home/issues/8358)

* 遙測： datetime 值使用特定文化特性格式- [#8351](https://github.com/NuGet/Home/issues/8351)

* 在套件管理員 UI 的 [流覽] 索引標籤中減少 UI 重新整理 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [測試失敗]「無法剖析設定檔」會提示兩次[#8320](https://github.com/NuGet/Home/issues/8320)

* 以良好的檔頁面引發 NU5037 錯誤，其中會說明客戶修正（套件缺少必要的 nuspec 檔案）- [#8291](https://github.com/NuGet/Home/issues/8291)

* 當專案的 RuntimeIdentifier 變更時，鎖定模式的還原會失敗- [#8260](https://github.com/NuGet/Home/issues/8260)

* 在 VS lazy [#8156](https://github.com/NuGet/Home/issues/8156)中進行讀取設定

* 「Nuget 來源新增」中的回歸會導致「'： ' 字元，十六進位值0x3A 無法包含在名稱中」錯誤- [#7948](https://github.com/NuGet/Home/issues/7948)

* NuGet 外掛程式認證提供者-隱藏進程視窗- [#7511](https://github.com/NuGet/Home/issues/7511)

* 強制 PackagePathResolver 是絕對路徑- [#7349](https://github.com/NuGet/Home/issues/7349)

* 在套件管理員 UI 的 [安裝及更新] 索引標籤中減少 UI 重新整理- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR：**

* 更新 Xamarin 架構以對應至 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)

* 針對安裝/更新[#8324](https://github.com/NuGet/Home/issues/8324) ，啟用複製套件管理員「預覽視窗」的內容

* 在 proj 檔案上啟用還原- [#8212](https://github.com/NuGet/Home/issues/8212)

* 引進`NUGET_NETFX_PLUGIN_PATHS` 和`NUGET_NETCORE_PLUGIN_PATHS`同時支援兩者的設定- [#8151](https://github.com/NuGet/Home/issues/8151)

* 透過版本屬性啟用 PackageDownload 的多個版本- [#8074](https://github.com/NuGet/Home/issues/8074)

* 將-SolutionDirectory 和-PackageDirectory 選項新增至 nuget.exe pack- [#7163](https://github.com/NuGet/Home/issues/7163)

* 啟用 NuGet 套件以具決定性的[#6229](https://github.com/NuGet/Home/issues/6229)

**[此版本中已修正的所有問題清單-5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**