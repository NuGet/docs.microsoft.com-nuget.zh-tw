---
title: "NuGet 3.4.2 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b514da09-da1f-416b-9bfc-692f08fb6957
description: "版本資訊包含 NuGet 3.4.2 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 3.4.2 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6761c59b6dc85b9a8503041928c2707549006d9c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 版本資訊

[NuGet 3.4.1 版本資訊](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 版本資訊](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 已於 2016 年 4 月 8 日解決幾個問題中 3.4 和 3.4.1 已識別發行版本。

## <a name="nugetexe-342-rc-is-now-available"></a>現已提供 nuget.exe 3.4.2 RC

您可以下載的發行候選版本的 nuget.exe 3.4.2[這裡](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和增強功能

* 我們已經大幅改善效能的特定案例中，更新封裝名稱中有深入的相依性圖形上花費很長的時間而停止 Visual Studio 中的更新。
* 沒有網路流量的 nuget 還原是 2.5 x – 更快速的 Visual Studio 中的 3 倍。
* 除了這項變更，我們已修正問題，我們已達到網路 VS UI 中擷取更新計數時，兩次。 這是部分負責經驗的 3.4/3.4.1 某些逾時問題客戶。
* 已新增的支援 no_proxy 設定

##<a name="fixes"></a>修正程式

* 其中 nuget.org 的來源遺漏 NuGet 設定或組態中更新至 3.4.1 之後修正的問題。
* 其中 FindPackagesById 3.4.1 中的大小寫變更會中斷 Artifactory 修正的問題。
* 已更正 fips 與 nuget.exe NuGet 還原造成失敗的問題。
* 瀏覽具有無效的圖示 URL 來源時，請修正損毀。
* 已修正的問題合併版本和項目從 「 所有來源 」。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>已知問題 3.4.2 中 Windows x86 命令列 (RC)

早期的下一週我們叫用 RTM 之前會解決這些問題。

*  如果方案檔放在較低的資料夾階層，於專案檔，針對方案執行 nuget 還原將會失敗。
*  封裝使用 V2 摘要上執行 nuget delete 命令將會失敗。 請改用 V3 摘要。


如中這一版的修正和改善的完整清單，請參閱問題的清單[這裡](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。