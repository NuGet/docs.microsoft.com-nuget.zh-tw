---
title: NuGet 3.4 版本資訊
description: NuGet 3.4 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776418"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 版本資訊

[NuGet 3.4-RC 版本](../release-notes/nuget-3.4-RC.md)  |  資訊[NuGet 3.4.1 版本](../release-notes/nuget-3.4.1.md)資訊

NuGet 3.4 已于2016年3月30日發行，作為 Visual Studio 2015 Update 2 和 Visual Studio 15 Preview 版本的一部分，並以一些思維原則建立：

* 跨平臺支援
* 效能改善
* 次要 UI 改進

先前已在 RC 中新增下列功能，並已針對3.4 版本更新或完成：

## <a name="new-features"></a>新功能

* NuGet 用戶端現在支援從存放庫進行 gzip 內容編碼
* 從 xproj 專案中的套件支援 Pdb
* ContentFiles 元素中的 iOS 和 Android 組建動作支援
* 支援 netstandard 和 netstandardapp 架構的名字標記

## <a name="new-user-interface-features"></a>新的消費者介面功能

* 明顯的效能改進，特別是針對已安裝、更新和合併索引標籤
* 匯總的「所有套件來源」來源可透過適當的搜尋結果合併來使用
* 已安裝和更新索引標籤現在會依字母順序排序
* 已新增可讓您重新整理搜尋的 [重新整理] 按鈕
* 版本清單頂端的最新組建選項

## <a name="updates-and-improvements"></a>更新和改進

* 中參考的封裝在 `project.json` 每個組建上都不會更新。 相反地，只有在強制還原、清除、重建或修改時，才會更新 `project.json` 。
* 當您使用 NuGet 設定 UI 時，不會再將 nuget.org 存放庫來源強制進入專案設定。
* NuGet 不再還原共用專案中的套件，也不會寫入鎖定檔案。
* 我們改進了網路失敗，並會重試處理，以找出無法連線或回應緩慢的伺服器。
* Visual Studio 封裝管理員 UI 中的鍵盤和滑鼠行為已獲得改善。
* 我們現在支援 DNX 中的最新 `project.json` 架構。

## <a name="breaking-changes"></a>重大變更

* 套件版本號碼現在會正規化為 *主要* 格式。*次要*。*修補程式* -*發行* 前版本  每個主要、次要和修補程式都會被視為整數，並捨棄任何前置零。  發行前版本資訊會視為字串，且不會套用任何變更。 NuGet 用戶端和 nuget.org 服務提供的搜尋會在查詢中使用這些數位。  您可以在 NuGet 檔的 [發行前版本](../create-packages/prerelease-packages.md)中找到更多詳細資料。

## <a name="known-issues"></a>已知問題

* **問題：** 在下列情況下，Windows 10 v1511 使用者可能會在 Visual Studio 中遇到問題，或甚至是使用 Powershell Visual Studio 損毀：
    * 安裝/卸載具有 install.ps1/uninstall.ps1 腳本的封裝
    * 載入具有 init.ps1 腳本的專案 (例如 EntityFramework) 
    * 發佈 web 內容

* 因應措施 **：** 確定您的 Windows 10 安裝已套用最新的修補程式，請別2016年1月 (KB 3124263) 或更新版本。  [GitHub 問題](http://github.com/nuget/home/issues/1638)有更多詳細資料 #1638

* **問題** ：NuGet v2 通訊協定重新導向中斷。
將要求重新導向至替代主機的自訂 NuGet 儲存機制不接受重新導向要求。
* 因應措施 **：** 若要解決此問題，請將設定中的套件存放庫 URI 設定為指向重新導向的伺服器位置。
如需詳細資訊，請參閱 [GitHub 提取要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。

我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)