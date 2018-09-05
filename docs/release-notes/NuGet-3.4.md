---
title: NuGet 3.4 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.4 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551187"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 的版本資訊

[NuGet 3.4 RC 版本資訊](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 版本資訊](../release-notes/nuget-3.4.1.md)

NuGet 3.4 2016 年 3 月 30 日發行 Visual Studio 2015 Update 2 和 Visual Studio 15 Preview 版本的過程，並在心中的幾個要件建置：

* 跨平台支援
* 效能改善
* 次要 UI 增強功能

下列功能先前新增的功能和已更新或完成 3.4 的版本：

## <a name="new-features"></a>新功能

* NuGet 用戶端現在支援 gzip 內容編碼方式從存放庫
* 從 xproj 專案封裝的 Pdb 的支援
* 適用於 iOS 和 Android 的建置動作 contentFiles 項目中的支援
* 支援 netstandard 和 netstandardapp framework moniker

## <a name="new-user-interface-features"></a>新的使用者介面功能

* 特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善
* 彙總的 「 所有套件來源 」 來源會提供適當的搜尋結果合併
* 安裝和更新索引標籤現在會依字母順序排序
* 新增 [重新整理] 按鈕，可搜尋，以重新整理
* 頂端的 [版本] 清單的最新組建選項

## <a name="updates-and-improvements"></a>更新和增強功能

* 中參考的套件`project.json`具有浮點版本將不會在每個組建上更新。 相反地，它們會在其中更新時，只強制還原、 清除、 重建或修改`project.json`。
* 當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不再強制到專案組態。
* NuGet 不會再還原共用專案中的套件，或寫入鎖定的檔案。
* 我們改進了網路連線失敗，並再試一次無法連線或緩慢回覆伺服器處理。
* 鍵盤和滑鼠行為有改進 Visual Studio 套件管理員 UI 中。
* 我們現在支援最新`project.json`DNX 中的結構描述。

## <a name="breaking-changes"></a>重大變更

* 套件版本號碼現在會正規化格式*主要*。*次要*。*修補*-*發行前版本*每個主要、 次要和修補程式會被視為整數和卸除任何前置的零。  發行前版本的資訊會被視為字串，並不套用任何變更。 這些數字會使用 NuGet 用戶端和 nuget.org 服務所提供的搜尋查詢中。  更多詳細資料，請參閱 NuGet 文件下,[發行前版本版本](../create-packages/prerelease-packages.md)。

## <a name="known-issues"></a>已知問題

* **問題：** Windows 10 v1511 使用者可能會遇到問題或甚至是 Visual Studio 損毀在 Visual Studio 中使用 Powershell 在下列情況：
    * 安裝 / 解除安裝套件有 install.ps1 / uninstall.ps1 指令碼
    * 正在載入 （例如 EntityFramework) init.ps1 指令碼的專案
    * 發行的 web 內容

* **因應措施：** 請確定您的 Windows 10 安裝具有最新套用的修補程式、 expecially 年 1 月 2016 (KB 3124263) 或更新版的更新。  更多詳細資料位於[GitHub 問題 # 1638年](http://github.com/nuget/home/issues/1638)

* **問題** ：NuGet v2 通訊協定重新導向中斷。
將要求重新導向至替代主機的自訂 NuGet 儲存機制不接受重新導向要求。
* **因應措施：** 若要解決此問題，請同時設定套件儲存機制 URI 設定為指向重新導向的伺服器位置。
如需詳細資訊，請參閱 < [GitHub 提取要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。

我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)