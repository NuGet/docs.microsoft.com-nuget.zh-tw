---
title: NuGet 3.0 Beta 版本資訊
description: 版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.0 Beta。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819623"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta 版本資訊

[NuGet 3.0 Preview 版本資訊](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 版本資訊](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta 已於 2015 年 2 月 23 日發行 Visual Studio 2015 CTP 6 版本。 此版本代表許多我們的團隊，我們有多個架構和效能改進的共用，以及我們很高興能夠開始微調我們 nuget.org 的服務上的效能設定。

我們強烈建議您先解除安裝任何舊版的 NuGet Visual Studio 2015 延伸模組，再安裝此新的版本。  如果您有與此版本的擴充功能的任何問題，我們建議您還原為[舊版](http://nuget.codeplex.com/downloads/get/909582)搭配 Visual Studio 2015 預覽。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

若要安裝 Visual Studio 2015 CTP 6 延伸模組組件庫中使用此 NuGet 3.0 Beta。 我們正努力預覽卸除的 Visual Studio 2012 和 Visual Studio 2013 很快。 我們先前共用我們意圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，我們沒有做出的決策，困難。

## <a name="new-clientserver-api"></a>新用戶端/伺服器應用程式開發介面

我們已尚未處理部分 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。 我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。 新的應用程式開發介面以 REST 為基礎和超，我們已選取[JSON LD](http://json-ld.org)為我們的資源格式。

在 NuGet 3.0 Beta 位元為單位，您會看到稱為"api.nuget.org"的套件來源下拉式清單中的新封裝來源。   如果您選取的套件來源，我們將使用新 API，而是要連接到 nuget.org。在 NuGet 3.0 RC 中，這個新的 API v3 為基礎的套件來源將會取代 v2 為基礎的 」 nuget.org"的套件來源。  我們建議您停用所有的其他公用封裝來源，將只 api.nuget.org 保留為您的封裝只公用儲存機制。

我們已放入建置 v3 API 的許多時間，而且將會繼續維護舊的用戶端來存取公用儲存機制尋找標準 v2 API。

## <a name="updated-ui"></a>更新的 UI

我們已增強使用者介面在本版中要包含下拉式方塊，可讓您選擇要與封裝所採取的動作，並轉換至螢幕的 [選項] 區域中的核取方塊的 [預覽] 按鈕。  [選項] 區域不再可摺疊，而且現在會提供說明可用選項的說明連結。

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>作業記錄

我們會移除強制回應視窗會快速顯示和隱藏安裝或解除安裝時的記錄資訊。  您真的想要看到的資訊，或是能夠複製並貼上它，此視窗會加入任何值。  相反地，我們現在將重新導向所有輸出記錄到輸出 視窗的 封裝管理員 窗格。  我們認為這是更舒適且類似於標準的建置報表，您會想要檢查。


### <a name="focus-on-performance"></a>專注於效能

我們進行許多變更，改善效能的 NuGet 搜尋及擷取的名稱。  這是從我們的客戶，我們數字一項考量，我們想確定我們在此版本中解決它。  我們已微調我們的伺服器，建立新的 CDN，並改善比對邏輯希望傳遞給您更有相關性的查詢，更快速的封裝搜尋結果。

當我們繼續透過這個階段中的 NuGet 3.0 開發時，我們將會調整和監視 nuget.org 服務，以確保我們提供較佳的體驗。  我們執行未進行任何停機時間，以計劃，但會新增及變更服務中的資源。  請注意我們[twitter 摘要](http://twitter.com/nuget)如當我們變更服務組態的詳細資訊。

## <a name="building-nuget-with-nuget"></a>建置隨 NuGet 的 NuGet

我們現在有重新我們 NuGet 用戶端架構本身正在建置為 NuGet 封裝的數個元件。 這個重複使用我們自己的程式庫會強制我們建立可重複使用，而且可以適當地封裝的元件。  我們已能夠消除重複的程式碼，並已經學會如何進一步設定我們的開發程序，以支援需要建置整個解決方案的封裝。  尋找推出的部落格文章，我們將討論如何結構化程式碼專案及我們的建置程序的運作方式。

## <a name="stay-tuned"></a>敬請期待

請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及針對 NuGet 3.0 公告 ！
