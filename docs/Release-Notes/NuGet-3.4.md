---
title: "NuGet 3.4 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr 的版本資訊。"
keywords: "NuGet 3.4 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 515fb888aca2a8eb138c8fea1fb5b3f5a8f4e275
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 版本資訊

[NuGet 3.4 RC 版本資訊](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 版本資訊](../release-notes/nuget-3.4.1.md)

NuGet 3.4 2016 年 3 月 30 日發行 Visual Studio 2015 Update 2 與 Visual Studio 15 Preview 版本的一部分，並不在建置中對少數原則：

*  跨平台支援
*  效能改善
*  次要的 UI 增強功能

下列功能先前 RC 中新增和已更新或完成 3.4 版本：

## <a name="new-features"></a>新功能

* NuGet 用戶端現在支援 gzip 內容編碼方式從儲存機制
* 支援從 xproj 專案封裝的 Pdb
* 適用於 iOS 和 Android 的建置動作 contentFiles 元素中的支援
* 支援 netstandard 和 netstandardapp framework moniker

## <a name="new-user-interface-features"></a>新的使用者介面功能

* 特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善
* 彙總所有封裝來源 ' 來源是適用於適當的搜尋結果合併
* 安裝和更新索引標籤現在會依字母順序排序
* 新增 [重新整理] 按鈕，可讓重新整理的搜尋
* 頂端的 [版本] 清單的最新組建選項

## <a name="updates-and-improvements"></a>更新和增強功能

* 封裝中參考`project.json`具有浮點版本將不會在每次建置更新。 相反地，他們會更新只能在強制還原、 清除、 重建或修改時`project.json`。
* 當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不會強制到專案組態。
* NuGet 無法再還原共用的專案中的封裝，也寫入鎖定檔案。
* 我們已改進網路失敗，然後重試處理連上或緩慢-到-回應的伺服器。
* 鍵盤和滑鼠的行為會在 Visual Studio 封裝管理員 UI 改進。
* 我們現在支援最新`project.json`DNX 中的結構描述。

## <a name="breaking-changes"></a>重大變更

* 封裝的版本號碼現在會正規化為格式*主要*。*次要*。*修補程式*-*發行前版本*每個主要、 次要、 和修補程式會被視為整數和卸除任何前置零。  發行前資訊會被視為字串，並不套用任何變更。 NuGet 用戶端和 nuget.org 服務所提供的搜尋查詢中使用這些數字。  更多詳細資料，請參閱 NuGet 文件下[搶鮮版版本](../create-packages/prerelease-packages.md)。

## <a name="known-issues"></a>已知問題

* **問題：** Windows 10 v1511 使用者可能會遇到問題或甚至 Visual Studio 損毀在 Visual Studio 中使用 Powershell 在下列案例：
    * 安裝 / 解除安裝有 install.ps1 / uninstall.ps1 指令碼
    * 載入有 init.ps1 指令碼 （例如 EntityFramework) 的專案
    * 發行的 web 內容

* **因應措施：**請確認您的 Windows 10 安裝已套用最新的修補程式、 expecially 年 1 月 2016 (KB 3124263) 或更新版的更新。  更多詳細資料位於[GitHub 問題 # 1638年](http://github.com/nuget/home/issues/1638)

* **問題** ：NuGet v2 通訊協定重新導向中斷。
將要求重新導向至替代主機的自訂 NuGet 儲存機制不接受重新導向要求。
* **因應措施：**若要解決此問題，請同時設定封裝儲存機制的 URI 設定為指向重新導向的伺服器位置。
如需詳細資訊，請參閱[GitHub 提取要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。

我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)