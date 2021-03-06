---
title: NuGet 5.3 版本資訊
description: NuGet 5.3 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 009a219139a767ee6453305be68ccce478b0ec75
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780120"
---
# <a name="nuget-53-release-notes"></a>NuGet 5.3 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.3 版](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 版本16.3.6 版](https://visualstudio.microsoft.com/downloads/) | [未來版本：3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝

## <a name="summary-whats-new-in-53"></a>摘要：5.3 中的新功能

* [封裝圖示可以內嵌于封裝中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而不需要外部 URL。 - [#352](https://github.com/NuGet/Home/issues/352)

* 增強了 SHA 追蹤和強制執行 Packages.Config [#7281](https://github.com/NuGet/Home/issues/7281)的安全性

* 啟用淘汰/舊版 NuGet 套件的淘汰[#2867](https://github.com/NuGet/Home/issues/2867)  |  [Blog 文章](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)  |  [](../nuget-org/deprecate-packages.md)檔

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 2.2 SDK 使用者無法使用 3.0.100-preview9 SDK 所產生的 NuGet 套件 .。。視您的時區而定 [#8603](https://github.com/NuGet/Home/issues/8603)

* 「路徑」中的字元會導致「路徑中有不合法的字元」失敗 `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* VS：元件完全是 ngen-ed，並非部分 ngen-ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* 減少記憶體使用量 (取消訂閱事件) - [#8471](https://github.com/NuGet/Home/issues/8471)

* "Error_UnableToFindProjectInfo" 訊息的語法不正確- [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 改進-驗證所有封裝，包括預期/實際的 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)

* #8401 中的多個列舉 `NuGetPackageManager.PreviewUpdatePackagesAsync`  -  [](https://github.com/NuGet/Home/issues/8401)

* 還原 PluginProcess 中的「公用-> 內部」變更- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. GetSources ( ... ) 定義錯誤的例外狀況行為- [#8383](https://github.com/NuGet/Home/issues/8383)

* 再次將 PluginManager 的函式設為公用- [#8379](https://github.com/NuGet/Home/issues/8379)

* 追蹤 PM UI 更新率的計量- [#8369](https://github.com/NuGet/Home/issues/8369)

* 當透過封裝管理員 UI 安裝時，減少 UI 重新整理的次數- [#8358](https://github.com/NuGet/Home/issues/8358)

* 遙測：日期時間值使用特定文化特性格式- [#8351](https://github.com/NuGet/Home/issues/8351)

* 在封裝管理員 UI 的 [流覽] 索引標籤中減少 UI 重新整理 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [測試失敗][無法剖析設定檔] 會出現兩次的提示 [#8320](https://github.com/NuGet/Home/issues/8320)

* 使用良好的 doc 頁面引發 NU5037 錯誤，此頁面會解釋客戶修正 (套件缺少必要的 nuspec 檔) - [#8291](https://github.com/NuGet/Home/issues/8291)

* 變更專案的 RuntimeIdentifier 時，鎖定模式還原失敗- [#8260](https://github.com/NuGet/Home/issues/8260)

* 將設定讀入 VS lazy [#8156](https://github.com/NuGet/Home/issues/8156)

* 中的回歸 `Nuget sources add` 會導致 "'： ' 字元（十六進位值0x3A）不能包含在名稱" errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* NuGet 外掛程式認證提供者-隱藏進程視窗- [#7511](https://github.com/NuGet/Home/issues/7511)

* 強制 PackagePathResolver 是絕對路徑- [#7349](https://github.com/NuGet/Home/issues/7349)

* 減少封裝管理員 UI 的 [安裝和更新] 索引標籤中的 UI 更新- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR：**

* 將 Xamarin framework 更新為對應至 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)

* 針對安裝/更新- [#8324](https://github.com/NuGet/Home/issues/8324)啟用複製套件管理員 "preview window" 的內容

* 在 proj 檔案上啟用還原- [#8212](https://github.com/NuGet/Home/issues/8212)

* 引進 `NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` 支援同時設定兩者 [#8151](https://github.com/NuGet/Home/issues/8151)

* 啟用 PackageDownload via Version 屬性的多個版本- [#8074](https://github.com/NuGet/Home/issues/8074)

* 將-SolutionDirectory 和-PackageDirectory 選項新增至 nuget.exe 套件- [#7163](https://github.com/NuGet/Home/issues/7163)

**[此版本修正的所有問題清單-5。3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>摘要：5.3.1 的新功能

* 外掛程式：工作已取消-不要讓取消影響外掛程式具現化- [#8648](https://github.com/NuGet/Home/issues/8648)

* 當使用認證提供者時，無法在一個進程 (中安全地執行還原工作) - [#8688](https://github.com/NuGet/Home/issues/8688)
