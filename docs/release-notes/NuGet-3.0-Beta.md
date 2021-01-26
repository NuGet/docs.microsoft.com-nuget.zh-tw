---
title: NuGet 3.0 Beta 版注意事項
description: NuGet 3.0 搶鮮版（Beta）的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776623"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta 版注意事項

[NuGet 3.0 Preview 版本](../release-notes/nuget-3.0-preview.md)  |  資訊[NuGet 3.0 RC 版本](../release-notes/nuget-3.0-rc.md)資訊

NuGet 3.0 Beta 發行于2015年2月23日，適用于 Visual Studio 2015 CTP 6 版。 這一版對我們的團隊來說很多，因為我們有許多可共用的架構和效能改進，而我們很高興能開始調整 nuget.org 服務的效能設定。

強烈建議您先卸載任何舊版的 NuGet Visual Studio 2015 延伸模組，再安裝這個新版本。  如果您在此版本的延伸模組中遇到任何問題，建議您還原為 [先前的版本](http://nuget.codeplex.com/downloads/get/909582) ，以搭配 Visual Studio 2015 preview 使用。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

此 NuGet 3.0 Beta 版可在 Visual Studio 2015 CTP 6 擴充功能資源庫中進行安裝。 我們即將致力於取得 Visual Studio 2012 的預覽，並 Visual Studio 2013。 我們先前已分享我們的意圖，以 [停止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，而我們的確進行了這種困難的決策。

## <a name="new-clientserver-api"></a>新用戶端/伺服器 API

我們已處理 NuGet 用戶端/伺服器通訊協定的一些執行詳細資料。 我們所做的工作是建立 NuGet 的「API v3」，這是針對重大案例（例如套件還原和安裝封裝）的高可用性而設計的。 新的 API 是以 REST 和超媒體為基礎，而且我們選取了 [JSON-LD](http://json-ld.org) 作為資源格式。

在 NuGet 3.0 搶鮮版（Beta）中，您會在 [套件來源] 下拉式清單中看到名為 "api.nuget.org" 的新套件來源。   如果您選取該套件來源，我們將使用新的 API，而不是連接到 nuget.org。在 NuGet 3.0 RC 中，這個新的 API v3 套件來源會取代 v2 型的 "nuget.org" 套件來源。  建議您停用所有其他公用套件來源，並只將 api.nuget.org 保留為您唯一的公用套件存放庫。

我們花了很多時間來建立 v3 API，並會繼續為舊版用戶端維護標準 v2 API，以存取公用存放庫。

## <a name="updated-ui"></a>更新的 UI

我們已增強此版本中的使用者介面，以包含一個下拉式方塊，可讓您選擇要對封裝執行的動作，並將 [預覽] 按鈕轉換成螢幕上 [選項] 區域中的核取方塊。  [選項] 區域不再是可折迭的，現在會提供說明連結來描述可用的選項。

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>作業記錄

我們已移除具有記錄資訊的強制回應視窗，這些資訊會在安裝或卸載時快速顯示及隱藏。  當您真正想要查看資訊或從中複製和貼上時，此視窗不會加入任何值。  相反地，我們現在會將所有輸出記錄重新導向至 [輸出] 視窗的封裝管理員窗格。  我們認為這比較熟悉，而且類似于您想要檢查的一般組建報告。


### <a name="focus-on-performance"></a>專注于效能

我們對改善 NuGet 搜尋和提取的效能進行了許多變更。  這是我們的客戶所關注的，我們想要確定我們已在此版本中解決這種問題。  我們已調整伺服器、建立新的 CDN，並改進了查詢符合邏輯，以提供更相關且更快速的封裝搜尋結果。

隨著我們在開發 NuGet 3.0 的這個階段進行，我們將會調整並監視 nuget.org 服務，以確保我們能提供更佳的體驗。  我們不打算參與任何停機時間，但會在服務中新增和變更資源。  請留意我們的 [twitter](http://twitter.com/nuget) 摘要，以取得何時變更服務設定的詳細資料。

## <a name="building-nuget-with-nuget"></a>使用 NuGet 建立 NuGet

我們現在已將 NuGet 用戶端重新架構至多個元件，而這些元件本身內建于 NuGet 套件中。 這種重複使用的程式庫會強制我們建立可重複使用且可正確封裝的元件。  我們可以消除重複的程式碼，並瞭解如何以更好的方式設定開發流程，以支援在整個解決方案中建立套件的需求。  請在稍後探討程式碼專案的結構化方式，以及我們的組建程式如何運作的詳細資訊。

## <a name="stay-tuned"></a>持續關注

請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多 NuGet 3.0 的進度和公告！
