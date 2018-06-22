---
title: NuGet 3.2.1 版本資訊
description: 版本資訊包含 NuGet 3.2.1 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820140"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 版本資訊

[NuGet 3.2 版本資訊](../release-notes/nuget-3.2.md) | [NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md)

NuGet 3.2.1 的命令列發行 2015 年 10 月 12 日少數幾個最佳化和 3.2 版的修正程式，且可從[dist.nuget.org](http://dist.nuget.org/index.html)。

## <a name="improvements"></a>增強功能

* NuGet 現在會使用組態檔的原始大小寫`NuGet.Config`。  這是很重要，在區分大小寫的作業系統上[1427年](https://github.com/NuGet/Home/issues/1427)
* NuGet 還原現在將會忽略 dnx 專案 (`*.xproj`)，應具有處理`dnu` [1227年](https://github.com/NuGet/Home/issues/1227)
* 使用時，最佳化網路使用量`index.json`和封裝註冊資料[1426年](https://github.com/NuGet/Home/issues/1426)
* 改善的資源下載較強大 v2 服務與處理[1448年](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>修正程式

* NuGet 更新已正確更新`.csproj` / `.vcxproj`參考[1483年](https://github.com/NuGet/Home/issues/1483)
* 現在防止本機.nuget 資料夾建立時找不到 SpecialFolders.UserProfile [1531年](https://github.com/NuGet/Home/issues/1531)
* 改善的本機快取中的封裝下載期間損毀的處理[1405年](https://github.com/NuGet/Home/issues/1405) [1157年](https://github.com/NuGet/Home/issues/1157)

命令列與 Visual Studio 擴充功能可以找到 NuGet GitHub 中解決問題的完整清單[3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>已知問題

我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)