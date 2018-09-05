---
title: NuGet 3.4.2 版本資訊
description: NuGet 3.4.2 中包含的版本資訊的已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549147"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 版本資訊

[NuGet 3.4.1 版本資訊](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 版本資訊](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 已於 2016 年 4 月 8 日解決在 3.4 和 3.4.1 中識別的幾個問題發行版本。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC 已正式發行

您可以下載的發行候選版本的 nuget.exe 3.4.2[此處](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和增強功能

* 我們大幅改善效能的特定案例中，更新封裝名稱中有深入的相依性圖形，花了很長的時間和停止 Visual Studio 中的更新。
* nuget 還原，而不需要網路流量是 2.5 倍快 Visual Studio 中的 3 倍。
* 除了這項變更，我們已修正的問題，我們已達到網路 VS UI 中擷取更新計數時，兩次。 這是部分負責一些逾時問題的客戶經驗 3.4/3.4.1。
* 已新增的支援 no_proxy 設定

## <a name="fixes"></a>修正

* Nuget.org 來源的 NuGet 設定或組態中遺漏更新至 3.4.1 之後修正的問題。
* 其中 FindPackagesById 3.4.1 中的大小寫變更會中斷 Artifactory 修正的問題。
* 已更正 fips，nuget.exe 與 NuGet 還原導致失敗的問題。
* 瀏覽具有無效的圖示 URL 來源時，請修正損毀。
* 已修正合併版本和項目從 「 所有來源 」 的問題。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>已知問題 3.4.2 中 Windows x86 命令列 (RC)

早期的下一週我們按下 RTM 之前，將會修正這些問題。

*  如果方案檔放在較低的資料夾階層，於專案檔，在方案上的執行 nuget 還原將會失敗。
*  使用 V2 摘要的套件上執行 nuget delete 命令將會失敗。 請改用 V3 摘要。


如中此版本的修正和改善的完整清單，請參閱的問題清單[此處](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。