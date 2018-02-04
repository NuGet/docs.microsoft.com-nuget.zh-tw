---
title: "NuGet 3.4 RC 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.4 RC 版本資訊。"
keywords: "NuGet 3.4 RC 版本資訊、 錯誤修正，已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC 版本資訊

[NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md) | [NuGet 3.4 版本資訊](../release-notes/nuget-3.4.md)

NuGet 3.4 RC 2016 年 3 月 3 日與 Visual Studio 2015 Update 2 RC 一起發行，並不在建置中對少數原則：

* 跨平台支援
* 效能改善
* 次要的 UI 增強功能

下列功能可用在 RC 中，具有多個計劃 3.4 最後發行版本。

## <a name="new-features"></a>新功能

* NuGet 用戶端現在支援 gzip 內容編碼方式從儲存機制
* 支援從 xproj 專案封裝的 Pdb
* 適用於 iOS 和 Android 的建置動作 contentFiles 元素中的支援
* 支援 netstandard 和 netstandardapp framework moniker

## <a name="new-user-interface-features"></a>新的使用者介面功能

* 特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善
* 安裝和更新索引標籤現在會依字母順序排序
* 新增 [重新整理] 按鈕，可讓重新整理的搜尋

## <a name="updates-and-improvements"></a>更新和增強功能

* 封裝中參考`project.json`具有浮點版本將不會在每次建置更新。 相反地，他們會更新只能在強制還原、 清除、 重建或修改時`project.json`。
* 當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不會強制到專案組態。
* NuGet 無法再還原共用的專案中的封裝，也寫入鎖定檔案。
* 我們已改進網路失敗，然後重試處理連上或緩慢-到-回應的伺服器。
* 鍵盤和滑鼠的行為會在 Visual Studio 封裝管理員 UI 改進。
* 我們現在支援最新`project.json`DNX 中的結構描述。

## <a name="known-issues"></a>已知問題

我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)