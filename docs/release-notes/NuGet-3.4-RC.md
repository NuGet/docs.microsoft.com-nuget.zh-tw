---
title: NuGet 3.4 RC 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.4 RC 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546750"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC 版本資訊

[NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md) | [NuGet 3.4 的版本資訊](../release-notes/nuget-3.4.md)

NuGet 3.4 RC 發行 2016 年 3 月 3 日與 Visual Studio 2015 Update 2 RC，並在心中的幾個要件建置：

* 跨平台支援
* 效能改善
* 次要 UI 增強功能

下列功能時才可在這個 RC 中，使用更有計劃 3.4 版的最終發行版本。

## <a name="new-features"></a>新功能

* NuGet 用戶端現在支援 gzip 內容編碼方式從存放庫
* 從 xproj 專案封裝的 Pdb 的支援
* 適用於 iOS 和 Android 的建置動作 contentFiles 項目中的支援
* 支援 netstandard 和 netstandardapp framework moniker

## <a name="new-user-interface-features"></a>新的使用者介面功能

* 特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善
* 安裝和更新索引標籤現在會依字母順序排序
* 新增 [重新整理] 按鈕，可搜尋，以重新整理

## <a name="updates-and-improvements"></a>更新和增強功能

* 中參考的套件`project.json`具有浮點版本將不會在每個組建上更新。 相反地，它們會在其中更新時，只強制還原、 清除、 重建或修改`project.json`。
* 當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不再強制到專案組態。
* NuGet 不會再還原共用專案中的套件，或寫入鎖定的檔案。
* 我們改進了網路連線失敗，並再試一次無法連線或緩慢回覆伺服器處理。
* 鍵盤和滑鼠行為有改進 Visual Studio 套件管理員 UI 中。
* 我們現在支援最新`project.json`DNX 中的結構描述。

## <a name="known-issues"></a>已知問題

我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)