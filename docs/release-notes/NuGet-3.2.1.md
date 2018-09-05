---
title: NuGet 3.2.1 版本資訊
description: 中包含 NuGet 3.2.1 版本資訊的已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548186"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 版本資訊

[NuGet 3.2 版本資訊](../release-notes/nuget-3.2.md) | [NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md)

2015 年 10 月 12 日發行具有少數幾個功能最佳化與修正 3.2 版且可從命令列的 NuGet 3.2.1 [dist.nuget.org](http://dist.nuget.org/index.html)。

## <a name="improvements"></a>增強功能

* NuGet 現在會使用組態檔的原始大小寫`NuGet.Config`。  這一點在區分大小寫的作業系統上[1427年](https://github.com/NuGet/Home/issues/1427)
* NuGet 還原現在將會忽略 dnx 專案 (`*.xproj`)，應該處理`dnu` [1227年](https://github.com/NuGet/Home/issues/1227)
* 使用時，最佳化網路使用量`index.json`和封裝的登錄資料[1426年](https://github.com/NuGet/Home/issues/1426)
* 改善的資源下載更加健全與 v2 服務處理[1448年](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>修正

* NuGet 更新已正確更新`.csproj` / `.vcxproj`參考[1483年](https://github.com/NuGet/Home/issues/1483)
* 現在防止本機.nuget 資料夾建立時找不到 SpecialFolders.UserProfile [1531年](https://github.com/NuGet/Home/issues/1531)
* 改進處理的封裝，在本機快取下載期間已損毀[1405年](https://github.com/NuGet/Home/issues/1405) [1157年](https://github.com/NuGet/Home/issues/1157)

命令列和 Visual Studio 擴充功能可以找到 NuGet GitHub 中的已解決問題的完整清單[3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>已知問題

我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)