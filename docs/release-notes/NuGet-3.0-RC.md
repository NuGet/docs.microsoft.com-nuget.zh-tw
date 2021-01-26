---
title: NuGet 3.0 RC 版本資訊
description: NuGet 3.0 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776575"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 版本資訊

[NuGet 3.0 Beta 版注意事項](../release-notes/nuget-3.0-beta.md)  | [NuGet 3.0 RC2 版本](../release-notes/nuget-3.0-RC2.md)資訊

NuGet 3.0 RC 已于2015年4月29日發行，Visual Studio 2015 RC 版本。 此版本有許多重要的 bug 修正、效能改進和更新，以支援新的架構。  它僅適用于 Visual Studio 2015。

### <a name="continued-focus-on-performance"></a>繼續專注于效能

NuGet 查詢的穩定性和效能會持續成為我們所關注的熱門主題。  在此版本中，您應該會開始在 NuGet UI 和網站中看到非常快速的搜尋作業。  我們正在監視服務以及您使用服務的方式，讓我們可以繼續調整這些作業。

## <a name="significant-issues-resolved"></a>已解決重大問題

為了穩定 NuGet 用戶端，我們在此版本中解決了許多問題。  以下是已解決的一些更重要問題的簡短清單：

* 在 ASP.NET 5 的 K 架構重新命名過程中，架構的名字標記已更新為可處理 dnx 和 dnxcore [連結](https://github.com/NuGet/Home/issues/215)
* 在 Visual Studio UI[連結](https://github.com/NuGet/Home/issues/232)中新增連結的說明文件
* `.nuspec`使用以逗號分隔的架構參考[連結](https://github.com/NuGet/Home/issues/276)，更有效地處理中的複雜參考
* 已修正日文文化特性[連結](https://github.com/NuGet/Home/issues/253)的支援
* 已更新用戶端，以允許 ASP.NET 5 專案使用新的 v3 端點 [連結](https://github.com/NuGet/Home/issues/219)
* 已更新為使用原始檔控制[連結](https://github.com/NuGet/Home/issues/56)更妥善處理套件資料夾
* 已修正附屬套件[連結](https://github.com/NuGet/Home/issues/17)的支援
* 已更正架構特定內容檔案[連結](https://github.com/NuGet/Home/issues/18)的支援

## <a name="github-presence-overhaul"></a>GitHub 狀態檢驗

我們已對 [GitHub 上的原始程式碼存放庫](http://github.com/nuget/home)進行一些變更。  如果您有 NuGet Visual Studio 用戶端、Powershell 命令或命令列可執行檔的任何問題，您可以記錄這些問題，並在 [GitHub 首頁存放庫問題清單](http://github.com/nuget/home/issues)上監視其進度。  我們在 [GitHub NuGetGallery 存放庫](http://github.com/nuget/NuGetGallery/issues)中追蹤資源庫的問題。


## <a name="stay-tuned"></a>持續關注

請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多 NuGet 3.0 的進度和公告！