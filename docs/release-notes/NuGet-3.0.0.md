---
title: NuGet 3.0 版本資訊
description: 版本資訊包含 NuGet 3.0.0 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 版本資訊

[NuGet 3.0 RC2 版本資訊](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 版本資訊](../release-notes/nuget-3.1.md)

NuGet 3.0 為配套延伸至 Visual Studio 2015 發行於 2015 年 7 月 20 日。 我們推入傳遞此版本與 Visual Studio，讓完整的更新的 NuGet 3.0 經驗會是適用於新的 Visual Studio 使用者。 此 NuGet 延伸模組版本只適用於 Visual Studio 2015。

我們建議您有存取權，可供使用，因為我們會包含支援 Windows 10 開發的 Visual Studio 2015 發行後，馬上發佈更新的最新版本更新 Visual Studio 組件庫的開發人員。

總共我們關閉 240 在 3.0 版中，問題，而且您可以檢閱[GitHub 上的問題的完整清單](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。

## <a name="known-issues"></a>已知問題

沒有提供幾個使用此版本中，傳遞的已知問題，而且所有這些項目會在與 Windows 10 版本一致。 上年 7 月 29 我們排定 3.1 版本中修正。  也可以更新您的 Visual Studio 擴充功能，從組件庫上該日期或之後修正這些已知的問題。

*  未提供轉譯為 「 不要顯示此訊息 」 索引標籤上 [預覽] 視窗和 「 著作人 」 標籤封裝描述視窗中。
*  當您使用 TFS 處理專案原始檔控制時，NuGet 無法顯示封裝管理員的使用者介面 Nuget.Config 檔案標示為唯讀。
   * **因應措施**簽出檔案，從 TFS。
*  黃色 NuGet Powershell 視窗中的 「 重新啟動列 」 中的文字不是可見的當您使用 Visual Studio 暗色調佈景主題。
   * **因應措施**使用 Visual Studio 淺色佈景主題。


## <a name="summary-of-top-issues-resolved"></a>最常發生的問題已解決的摘要

* [封裝管理員 視窗中重新整理時，呼叫經常網路更新](https://github.com/NuGet/Home/issues/515)
* [變更為安裝在封裝管理員的檢視時，延遲捲軸](https://github.com/NuGet/Home/issues/519)
* [應在背景執行緒上執行的網路呼叫](https://github.com/NuGet/Home/issues/516)
* [加入 [不顯示預覽視窗] 核取方塊](https://github.com/NuGet/Home/issues/566)
* [加入的處理序節流來減少處理器使用量](https://github.com/NuGet/Home/issues/356)
* 改良的可攜式類別庫參考處理
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [「 自動完成 」 服務是區分大小寫](https://github.com/NuGet/Home/issues/198)
* [若要重新引入基本驗證認證的更新](https://github.com/NuGet/Home/issues/456)
* [改良的錯誤記錄](https://github.com/NuGet/Home/issues/407)
* [呼叫更新封裝時改善的 powershell 錯誤訊息](https://github.com/NuGet/Home/issues/5)
* [固定 '深入了解選項' 連結，以防止在 Windows 10 上損毀](https://github.com/NuGet/Home/issues/822)
* [請記住發行前版本核取方塊設定](https://github.com/NuGet/Home/issues/732)
* [藉由跨專案的方案中快取結果改善蒐集效能](https://github.com/NuGet/Home/issues/721)
* [您可以收集多個封裝，以平行方式](https://github.com/NuGet/Home/issues/713)
* [安裝套件中移除-強制執行命令](https://github.com/NuGet/Home/issues/697)

請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及公告隨著準備好將提供對 Windows 10 開發的支援。