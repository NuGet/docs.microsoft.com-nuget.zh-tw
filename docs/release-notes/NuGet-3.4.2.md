---
title: NuGet 3.4.2 版本資訊
description: NuGet 3.4.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780255"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 版本資訊

[NuGet 3.4.1 版本](../release-notes/nuget-3.4.1.md)  |  資訊[NuGet 3.4.3 版本](../release-notes/nuget-3.4.3.md)資訊

NuGet 3.4.2 已于2016年4月8日發行，以解決3.4 和3.4.1 版本中所識別的數個問題。

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC 現已推出

您可以在 [這裡](https://dist.nuget.org/index.html)下載 nuget.exe 3.4.2 的候選版。

## <a name="updates-and-improvements"></a>更新和改進

* 我們大幅改善了特定案例中更新的效能，其中具有深度相依性圖形的套件更新會花很長的時間，並使 Visual Studio 無反應。
* 在 Visual Studio 的情況下，不需要網路流量的 nuget 還原為 2.5 x –3倍。
* 除了這項變更之外，我們也修正了在 VS UI 中提取更新計數時，達到網路兩次的問題。 這部分負責一些客戶在 3.4/3.4.1 中遇到的超時問題。
* 已新增 no_proxy 設定的支援

## <a name="fixes"></a>修正

* 修正了在更新至3.4.1 之後，NuGet 設定或設定中遺失 nuget.org 來源的問題。
* 修正3.4.1 中 FindPackagesById 的大小寫變更為中斷 Artifactory 的問題。
* 修正了使用 nuget.exe 的 NuGet 還原造成失敗的 FIPS 問題。
* 修正了使用無效圖示 URL 流覽來源時的損毀。
* 修正了從 [所有來源] 合併版本和專案的問題。

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>3.4.2 Windows x86 命令列 (RC) 的已知問題

這些問題將會在我們按下一周的初期修正。

*  如果解決方案檔放置於比專案檔還低的資料夾階層中，在方案上執行 nuget 還原將會失敗。
*  使用 V2 摘要在封裝上執行 nuget 刪除命令將會失敗。 請改用 V3 摘要。


如需此版本中的修正和增強功能的完整清單，請參閱 [此處](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)的問題清單。