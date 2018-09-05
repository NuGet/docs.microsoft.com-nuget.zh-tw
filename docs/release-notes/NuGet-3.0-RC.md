---
title: NuGet 3.0 RC 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.0 RC 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551715"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 版本資訊

[NuGet 3.0 Beta 版本資訊](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 版本資訊](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC 於 2015 年 4 月 29 日發行 Visual Studio 2015 RC 版本。 此版本還有幾個重要的 bug 修正、 效能增強功能和更新以支援新的架構。  它只適用於 Visual Studio 2015。

### <a name="continued-focus-on-performance"></a>在效能上持續的關注

持續是熱門話題，我們會專注於穩定性和 NuGet 查詢的效能。  此版本中，您應該開始查看非常快速的搜尋作業中的 NuGet UI 和網站。  我們正在監視的服務，並使用服務，以便我們可以繼續微調這些作業。

## <a name="significant-issues-resolved"></a>已解決的重要問題

穩定的 NuGet 用戶端，以便我們可以解決許多問題做為此版本的一部分。  以下是只有一些更重要的問題已解決的簡短清單：

* 隨著 ASP.NET 5 的 K framework 的重新命名的詳細資訊，framework moniker 已更新，以處理 dnx 和 dnxcore[連結](https://github.com/NuGet/Home/issues/215)
* 從 Visual Studio UI 中的連結新增說明文件[連結](https://github.com/NuGet/Home/issues/232)
* 更妥善地處理複雜的參考中的`.nuspec`逗號分隔的 framework 參考[連結](https://github.com/NuGet/Home/issues/276)
* 已修正日文的文化特性的支援[連結](https://github.com/NuGet/Home/issues/253)
* 更新的用戶端，讓 ASP.NET 5 專案使用新的 v3 端點[連結](https://github.com/NuGet/Home/issues/219)
* 已更新為較佳的控制代碼與原始檔控制的 packages 資料夾[連結](https://github.com/NuGet/Home/issues/56)
* 已修正的附屬套件支援[連結](https://github.com/NuGet/Home/issues/17)
* 已更正的架構特定的內容檔案支援[連結](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub 存在變革

我們已進行一些變更以我們[原始程式碼儲存機制在 GitHub 上的](http://github.com/nuget/home)。  如果您有任何問題，與 Visual Studio 的 NuGet 用戶端、 Powershell 命令，或在命令列可執行檔可以記錄這些問題，並上監視其進度我們[首頁 GitHub 存放庫問題清單](http://github.com/nuget/home/issues)。  我們在追蹤中的資源庫的問題我們[GitHub NuGetGallery 存放庫](http://github.com/nuget/NuGetGallery/issues)。


## <a name="stay-tuned"></a>敬請期待

請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和 NuGet 3.0 公告 ！