---
title: NuGet 3.2.1 版本資訊
description: NuGet 3.2.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776521"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 版本資訊

[NuGet 3.2 版本](../release-notes/nuget-3.2.md)  |  資訊[NuGet 3.3 版本](../release-notes/nuget-3.3.md)資訊

命令列的 NuGet 3.2.1 已于2015年10月12日發行，其中包含一些3.2 版本的優化和修正程式，可從 [dist.nuget.org](http://dist.nuget.org/index.html)取得。

## <a name="improvements"></a>改善

* NuGet 現在會使用原始大小寫的設定檔 `NuGet.Config` 。  這在區分大小寫的作業系統上很重要 [1427](https://github.com/NuGet/Home/issues/1427)
* NuGet 還原現在會忽略 dnx 專案 (`*.xproj`) 應使用1227進行處理 `dnu` [](https://github.com/NuGet/Home/issues/1227)
* 使用 `index.json` 和封裝註冊資料時優化網路使用量 [1426](https://github.com/NuGet/Home/issues/1426)
* 使用 v2 服務[1448](https://github.com/NuGet/Home/issues/1448)改進資源下載處理功能更強大

## <a name="fixes"></a>修正

* NuGet 更新正確更新 `.csproj` / `.vcxproj` 參考[1483](https://github.com/NuGet/Home/issues/1483)
* 現在防止在 SpecialFolders 時建立本機的 nuget 資料夾 [1531](https://github.com/NuGet/Home/issues/1531)
* 改進在本機快取中的封裝處理在下載[1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)期間損毀的程式

您可以在 NuGet GitHub [3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)中找到針對命令列和 Visual Studio 擴充功能所解決之問題的完整清單。

## <a name="known-issues"></a>已知問題

我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)