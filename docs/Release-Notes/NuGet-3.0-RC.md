---
title: "NuGet 3.0 RC 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.0 RC 版本資訊。"
keywords: "NuGet 3.0 RC 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 版本資訊

[NuGet 3.0 Beta 版本資訊](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 版本資訊](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC 於 2015 年 4 月 29 日發行 Visual Studio 2015 RC 版本。 此版本有一些重要的 bug 修正、 效能增強功能和更新以支援新的架構。  它只適用於 Visual Studio 2015。

### <a name="continued-focus-on-performance"></a>繼續對效能的焦點

穩定性和效能的 NuGet 查詢繼續我們會將焦點放在一個熱門主題。  在此版本中，您應該開始查看非常快速搜尋作業中的 NuGet UI 和網站。  我們正在監視的服務，並使用服務，以便我們可以繼續微調這些作業。

## <a name="significant-issues-resolved"></a>已解決的重要問題

穩定 NuGet 用戶端，以便我們可以解決的許多問題做為此版本的一部分。  以下是只有一些更重要的是已解決的問題的簡短清單：

* ASP.NET 5 命名 K framework 的一部分，framework moniker 已更新來處理 dnx 和 dnxcore[連結](https://github.com/NuGet/Home/issues/215)
* 加入說明 」 文件從 Visual Studio UI 中的連結[連結](https://github.com/NuGet/Home/issues/232)
* 中的複雜參照的進一步處理`.nuspec`逗點分隔的 framework 參考與[連結](https://github.com/NuGet/Home/issues/276)
* 修正日文的文化特性的支援[連結](https://github.com/NuGet/Home/issues/253)
* 更新的用戶端，以允許 ASP.NET 5 專案以使用新的 v3 端點[連結](https://github.com/NuGet/Home/issues/219)
* 已更新為更好的控制代碼封裝與原始檔控制 資料夾[連結](https://github.com/NuGet/Home/issues/56)
* 固定的附屬項目封裝的支援[連結](https://github.com/NuGet/Home/issues/17)
* 已更正的架構特定的內容檔案支援[連結](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub 存在重

我們所做一些變更，以便我們[來源 GitHub 上的程式碼儲存機制](http://github.com/nuget/home)。  如果 Visual Studio 用戶端、 Powershell 命令，或命令列中有任何問題可執行檔可以記錄這些問題，並監視其進度上我們[首頁 GitHub 儲存機制的問題清單](http://github.com/nuget/home/issues)。  我們在圖庫中的問題追蹤我們[GitHub NuGetGallery 儲存機制](http://github.com/nuget/NuGetGallery/issues)。


## <a name="stay-tuned"></a>敬請期待

請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及針對 NuGet 3.0 公告 ！