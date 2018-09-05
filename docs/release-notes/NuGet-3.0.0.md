---
title: NuGet 3.0 版本資訊
description: 版本資訊 NuGet 3.0.0 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551859"
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 版本資訊

[NuGet 3.0 RC2 版本資訊](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 版本資訊](../release-notes/nuget-3.1.md)

NuGet 3.0 已於 2015 年 7 月 20 日發行，為 Visual Studio 2015 的套件組合擴充功能。 我們推入來傳遞此版本中的使用 Visual Studio，以便完成更新的 NuGet 3.0 體驗可供新的 Visual Studio 使用者。 這個 NuGet 擴充功能版本僅適用於 Visual Studio 2015。

我們建議開發人員可存取 Visual Studio 組件庫更新，可供使用，因為我們會包含支援 Windows 10 開發的 Visual Studio 2015 發行後，馬上來發佈更新為最新版本。

總計中，我們關閉 240 問題在 3.0 版的版本中，且您可以檢閱[GitHub 上的問題的完整清單](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。

## <a name="known-issues"></a>已知問題

有幾個與此版本中，傳遞的已知問題，所有這些項目固定的排程與 Windows 10 版本一致。 在 7 月 29 3.1 版本中。  您就能夠更新您的 Visual Studio 延伸模組，從資源庫來修正這些已知的問題該日期當天或之後。

*  未提供轉譯為 「 不要再顯示此訊息 」 標籤上預覽 視窗，並封裝的 說明 視窗中的 「 著作人 」 標籤。
*  當您使用 TFS 使用的專案原始檔控制時，NuGet 無法呈現的套件管理員的使用者介面如果 Nuget.Config 檔案標示為唯讀。
   * **因應措施**查看 TFS 中的檔案。
*  以黃色 NuGet Powershell 視窗中的 「 重新啟動列 」 的文字不是可見的當您使用 Visual Studio 暗色調佈景主題。
   * **因應措施**使用 Visual Studio 的淺色佈景主題。


## <a name="summary-of-top-issues-resolved"></a>最常發生的問題已解決的摘要

* [常見網路更新呼叫時重新整理套件管理員視窗](https://github.com/NuGet/Home/issues/515)
* [變更為安裝套件管理員中的檢視時，延遲捲軸](https://github.com/NuGet/Home/issues/519)
* [網路呼叫應該在背景執行緒上執行](https://github.com/NuGet/Home/issues/516)
* [已新增 [不顯示預覽視窗] 的核取方塊](https://github.com/NuGet/Home/issues/566)
* [已新增的處理程序節流來降低處理器使用量](https://github.com/NuGet/Home/issues/356)
* 改良的可攜式類別庫參考處理
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [自動完成 service 已區分大小寫](https://github.com/NuGet/Home/issues/198)
* [引進基本驗證認證的更新](https://github.com/NuGet/Home/issues/456)
* [已改善的錯誤記錄](https://github.com/NuGet/Home/issues/407)
* [呼叫更新套件時，改善的 powershell 錯誤訊息](https://github.com/NuGet/Home/issues/5)
* [已修正 深入了解選項' 連結，以防止在 Windows 10 上損毀](https://github.com/NuGet/Home/issues/822)
* [請記住發行前版本 核取方塊設定](https://github.com/NuGet/Home/issues/732)
* [依方案中專案的快取結果的改良蒐集效能](https://github.com/NuGet/Home/issues/721)
* [您可以以平行方式收集多個封裝](https://github.com/NuGet/Home/issues/713)
* [安裝套件中移除-強制執行命令](https://github.com/NuGet/Home/issues/697)

請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和宣布，我們準備好提供適用於 Windows 10 開發的支援。