---
title: NuGet 3.0 Beta 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.0 Beta 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550909"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta 版本資訊

[NuGet 3.0 Preview 版本資訊](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 版本資訊](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 beta 版於 2015 年 2 月 23 日發行 Visual Studio 2015 CTP 6 版本。 此版本給我們的團隊，表示很多，因為我們有一些架構和效能增強功能，若要共用，而且我們很高興能夠開始微調我們 nuget.org 的服務上的效能設定。

我們強烈建議您先解除安裝任何舊版的 NuGet Visual Studio 2015 延伸模組，再安裝此新版本。  如果您有與此版本的延伸模組的任何問題，我們建議您還原[舊版](http://nuget.codeplex.com/downloads/get/909582)搭配 Visual Studio 2015 preview。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

若要安裝 Visual Studio 2015 CTP 6 延伸模組組件庫中使用此 NuGet 3.0 beta 版。 我們正努力取得預覽卸除 Visual Studio 2012 和 Visual Studio 2013 推出。 我們之前告訴大家我們試圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，但未將該相當困難的決定。

## <a name="new-clientserver-api"></a>新用戶端/伺服器 API

我們一直在處理某些 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。 我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。 新的 API 以 REST 為基礎，並已選取超媒體和我們[JSON-LD](http://json-ld.org)為我們資源的格式。

在 NuGet 3.0 Beta 位元為單位，您會看到新的封裝來源的封裝來源下拉式清單中稱為 「 api.nuget.org"。   如果您選取該套件來源，我們將使用我們的新 API，而是要連接到 nuget.org。在 NuGet 3.0 RC 中，這個新的 API v3 套件來源將會取代 v2 為基礎的"nuget.org"套件來源。  我們建議您停用的所有其他公用套件來源，並將僅 api.nuget.org 保留為僅針對公用套件存放庫。

我們已經放了很多時間建置我們的 v3 API，並將繼續維護舊的用戶端想要存取的公用存放庫的標準 v2 API。

## <a name="updated-ui"></a>更新的 UI

我們已增強這一版包含可讓您選擇要與封裝執行的動作，而轉換至螢幕的 [選項] 區域中的核取方塊的 [預覽] 按鈕的下拉式方塊中的使用者介面。  [選項] 區域不再可摺疊，而且現在會提供說明可用選項的 [說明] 連結。

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>作業記錄

我們已移除強制回應視窗會快速顯示及隱藏在安裝或解除安裝時的記錄資訊。  您真正想看到的資訊，或是能夠複製並貼上從它時，此視窗會新增任何值。  相反地，我們會立即重新導向所有輸出記錄到輸出 視窗的 套件管理員 窗格。  我們認為這是更自在，類似於標準的建置報表，您會想要檢查。


### <a name="focus-on-performance"></a>著重在效能

我們加入了許多變更，改善效能，NuGet 搜尋，以及提取的名稱。  這是從我們的客戶，我們首要考量，我們想要確定我們在此版本中已解決。  我們已調整我們的伺服器，建立新的 CDN 和更佳的查詢比對希望傳遞給您更多相關的邏輯，並更快的套件搜尋結果。

當我們繼續透過 NuGet 3.0 開發的這個階段，我們將會調整並監視 [nuget.org] 服務，以確保我們提供較佳的體驗。  我們執行未計劃參與任何停機時間，但會新增及變更在服務中的資源。  敬請期待我們[twitter 摘要](http://twitter.com/nuget)如當我們變更服務組態的詳細資訊。

## <a name="building-nuget-with-nuget"></a>使用 NuGet 建置 NuGet

我們現在有重新我們 NuGet 用戶端架構本身內建 NuGet 套件的數個元件。 此重複使用我們自己的程式庫會強制我們建立可重複使用，而且，可以正確地將它封裝的元件。  我們已能夠消除重複的程式碼，並已了解如何進一步設定我們的開發程序，以支援需要建置整個解決方案的封裝。  尋找推出的部落格文章，我們會討論程式碼專案的結構方式，以及我們的建置程序的運作方式。

## <a name="stay-tuned"></a>敬請期待

請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和 NuGet 3.0 公告 ！
