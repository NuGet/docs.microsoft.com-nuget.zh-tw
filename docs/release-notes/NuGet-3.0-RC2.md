---
title: NuGet 3.0 RC2 版本資訊
description: NuGet 3.0 RC2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780277"
---
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 版本資訊

[NuGet 3.0 RC 版本](../release-notes/nuget-3.0-RC.md)  |  資訊[NuGet 3.0 版本](../release-notes/nuget-3.0.0.md)資訊

NuGet 3.0 RC2 發行于2015年6月3日，作為 Visual Studio 2015 擴充功能庫和 [Codeplex](https://nuget.codeplex.com/releases/view/615507)提供的過渡版。 此版本有許多重要的 bug 修正和效能改進，我們認為在完成的 Visual Studio 2015 版之前必須先釋出。 此 NuGet 擴充功能版本僅適用于 Visual Studio 2015。

我們在此版本中已關閉158問題，您可以在 [GitHub 上查看問題的完整清單](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)。

## <a name="summary-of-top-issues-resolved"></a>已解決常見問題的摘要

* [當套件管理員視窗重新整理時頻繁的網路更新呼叫](https://github.com/NuGet/Home/issues/515)
* [在封裝管理員中變更為已安裝的視圖時，延遲捲軸](https://github.com/NuGet/Home/issues/519)
* [應在背景執行緒上執行網路呼叫](https://github.com/NuGet/Home/issues/516)
* [已新增 [不要顯示預覽視窗] 核取方塊](https://github.com/NuGet/Home/issues/566)
* [已新增進程節流來降低處理器使用量](https://github.com/NuGet/Home/issues/356)
* 改良的便攜類別程式庫參考處理
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [自動完成服務區分大小寫](https://github.com/NuGet/Home/issues/198)
* [更新以重新引入基本驗證認證](https://github.com/NuGet/Home/issues/456)
* [已改善錯誤記錄](https://github.com/NuGet/Home/issues/407)
* [已改善呼叫更新套件時的 powershell 錯誤訊息](https://github.com/NuGet/Home/issues/5)

從 Codeplex 將此 [更新下載到 nuget 擴充](https://nuget.codeplex.com/releases/view/615507) 功能，請留意我們的 [blog](http://blog.nuget.org) ，以取得更多 nuget 3.0 的進度和公告！