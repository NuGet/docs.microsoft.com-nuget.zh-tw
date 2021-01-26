---
title: NuGet 3.4-RC 版本資訊
description: NuGet 3.4 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780244"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4-RC 版本資訊

[NuGet 3.3 版本](../release-notes/nuget-3.3.md)  |  資訊[NuGet 3.4 版本](../release-notes/nuget-3.4.md)資訊

NuGet 3.4-RC 已于2016年3月3日和 Visual Studio 2015 Update 2 RC 發行，並以一些思維原則建立：

* 跨平臺支援
* 效能改善
* 次要 UI 改進

此 RC 提供下列功能，並已針對3.4 最終版本提供更多規劃。

## <a name="new-features"></a>新功能

* NuGet 用戶端現在支援從存放庫進行 gzip 內容編碼
* 從 xproj 專案中的套件支援 Pdb
* ContentFiles 元素中的 iOS 和 Android 組建動作支援
* 支援 netstandard 和 netstandardapp 架構的名字標記

## <a name="new-user-interface-features"></a>新的消費者介面功能

* 明顯的效能改進，特別是針對已安裝、更新和合併索引標籤
* 已安裝和更新索引標籤現在會依字母順序排序
* 已新增可讓您重新整理搜尋的 [重新整理] 按鈕

## <a name="updates-and-improvements"></a>更新和改進

* 中參考的封裝在 `project.json` 每個組建上都不會更新。 相反地，只有在強制還原、清除、重建或修改時，才會更新 `project.json` 。
* 當您使用 NuGet 設定 UI 時，不會再將 nuget.org 存放庫來源強制進入專案設定。
* NuGet 不再還原共用專案中的套件，也不會寫入鎖定檔案。
* 我們改進了網路失敗，並會重試處理，以找出無法連線或回應緩慢的伺服器。
* Visual Studio 封裝管理員 UI 中的鍵盤和滑鼠行為已獲得改善。
* 我們現在支援 DNX 中的最新 `project.json` 架構。

## <a name="known-issues"></a>已知問題

我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)