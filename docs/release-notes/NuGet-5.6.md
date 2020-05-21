---
title: NuGet 5.6 版本資訊
description: NuGet 5.6 的版本資訊，包括新功能、bug 修正和 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727818"
---
# <a name="nuget-56-release-notes"></a>NuGet 5.6 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.6 版](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝

## <a name="summary-whats-new-in-56"></a>摘要：5.6 中的新功能

* 支援具有浮動版本的發行前版本套件。 `Version="*-*"`、 `Version="1.*-*"` 和類似的浮動到最新版本，包括發行前版本（在指定的範圍內） [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>此版本所修正的問題

**存在**

* `nuget push *.nupkg`當 .snupkg 不存在時失敗- [#8148](https://github.com/NuGet/Home/issues/8148)

* Pack 和其他幾個程式碼路徑會因地區設定而失敗。 使用 System.text.regularexpressions.RegExoptions. Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* 效能：卸載專案案例的 DG 規格不應以預覽還原撰寫- [#8793](https://github.com/NuGet/Home/issues/8793)

* 還原：藉由快取解決方案相依性圖形規格來改善效能[#9201](https://github.com/NuGet/Home/issues/9201)

* PM UI 在使用 PM 主控台安裝套件之後，不適用於 SDK 樣式專案- [#9203](https://github.com/NuGet/Home/issues/9203)

* 在 PM UI 中，無法以本機套件摘要顯示內嵌圖示-取決於/vs-- [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict （）如果無法剖析，則應該傳回 false [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`的說明 `-source` 應建議使用來源名稱，而不是來源 URL- [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`建立錯誤的預設封裝來源名稱- [#9277](https://github.com/NuGet/Home/issues/9277)

* 螢幕閱讀程式未公告「搜尋 ...」切換索引標籤時的訊息- [#9307](https://github.com/NuGet/Home/issues/9307)

* 協助工具：焦點矩形色彩無法以深色主題的 UI 索引標籤存取- [#9336](https://github.com/NuGet/Home/issues/9336)

* nuget.exe 5.5 無法使用 MSBuild 14 或以下的還原- [#9458](https://github.com/NuGet/Home/issues/9458)

* 不要在還原訊息中記錄毫秒時間- [#8977](https://github.com/NuGet/Home/issues/8977)

* 使 IOutputConsole 非同步[#9268](https://github.com/NuGet/Home/issues/9268)

* MSBuild 版本挑選在某些非英文文化特性上運作不佳- [#9322](https://github.com/NuGet/Home/issues/9322)

* #9337 上的預設遺漏格式 `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* 效能： RestoreOperationLogger 具有不必要的執行緒親和性- [#9288](https://github.com/NuGet/Home/issues/9288)

* 自動建立命令的檔 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)

* 預設詳細資訊不應報告每個專案的 noop 還原- [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`的支援參數 `NuGet.exe update` ，類似于 install command- [#7694](https://github.com/NuGet/Home/issues/7694)


**Dcr**

* 新增 net 5.0 目標架構的初始支援- [#9584](https://github.com/NuGet/Home/issues/9584)

* 在 PM UI 的 [更新] 索引標籤中依識別碼排序套件- [#9278](https://github.com/NuGet/Home/issues/9278)


**[此版本中已修正的所有問題清單-5。6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
