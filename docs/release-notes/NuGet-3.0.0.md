---
title: NuGet 3.0 版本資訊
description: NuGet 3.0.0 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776549"
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 版本資訊

[NuGet 3.0 RC2 版本](../release-notes/nuget-3.0-RC2.md)  |  資訊[NuGet 3.1 版本](../release-notes/nuget-3.1.md)資訊

NuGet 3.0 已于2015年7月20日發行為 Visual Studio 2015 的組合延伸模組。 我們推送了 Visual Studio 的版本，讓新的 Visual Studio 使用者可以使用完整的更新 NuGet 3.0 體驗。 此 NuGet 擴充功能版本僅適用于 Visual Studio 2015。

我們建議可存取 Visual Studio 資源庫的開發人員更新為可用的最新版本，因為我們會在發行包含 Windows 10 開發支援的 Visual Studio 2015 之後，立即發佈更新。

總共我們在3.0 版中已關閉240問題，您可以在 [GitHub 上查看問題的完整清單](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。

## <a name="known-issues"></a>已知問題

此版本提供了許多已知問題，所有這些專案都已在我們的排程3.1 版本中修正，以符合7月29日的 Windows 10 版本。  您可以從資源庫中或在該日期之後更新 Visual Studio 延伸模組，以修正這些已知問題。

*  [預覽] 視窗上的 [不要再顯示] 標籤和 [封裝描述] 視窗中的 [作者] 標籤不提供轉譯。
*  當您使用 TFS 原始檔控制來處理專案時，如果 Nuget.Config 檔案標示為唯讀，則 NuGet 無法顯示套件管理員使用者介面。
   * 因應措施從 TFS 簽出檔案。
*  當您使用 Visual Studio 深色主題時，不會顯示 [NuGet Powershell] 視窗中黃色「重新開機列」的文字。
   * 因應措施使用 Visual Studio 淺色主題。


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
* [已修正 [瞭解選項] 連結，以防止當 Windows 10 時發生損毀](https://github.com/NuGet/Home/issues/822)
* [[記住發行前版本] 核取方塊設定](https://github.com/NuGet/Home/issues/732)
* [藉由快取解決方案中各專案的結果來改善收集效能](https://github.com/NuGet/Home/issues/721)
* [可以平行收集多個封裝](https://github.com/NuGet/Home/issues/713)
* [已移除安裝封裝-force 命令](https://github.com/NuGet/Home/issues/697)

當我們準備好提供 Windows 10 開發的支援時，請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多的進度和公告。