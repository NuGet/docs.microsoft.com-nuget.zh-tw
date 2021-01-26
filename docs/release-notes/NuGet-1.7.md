---
title: NuGet 1.7 版本資訊
description: NuGet 1.7 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777072"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 版本資訊

[NuGet 1.6 版本](../release-notes/nuget-1.6.md)  |  資訊[NuGet 1.8 版本](../release-notes/nuget-1.8.md)資訊

NuGet 1.7 發行于2012年4月4日。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行的是 VS 2010 SP1，如果您已安裝較舊的版本，可能會在嘗試升級 NuGet 時發生安裝錯誤。

解決方法是直接卸載 NuGet，然後從 VS 延伸模組資源庫安裝它。  如需相關資訊，請參閱 <https://support.microsoft.com/kb/2581019> 。

注意：如果 Visual Studio 不允許您卸載擴充功能 () 停用 [卸載] 按鈕，那麼您可能需要使用 [以系統管理員身分執行] 來重新開機 Visual Studio。

## <a name="features"></a>功能

### <a name="support-opening-readmetxt-file-after-installation"></a>支援在安裝後開啟 readme.txt 檔案
1.7 的新功能，如果您的套件在 `readme.txt` 套件的根目錄包含檔案，NuGet 會在完成安裝套件之後自動開啟此檔案。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>在 [管理 NuGet 封裝] 對話方塊中顯示發行前版本套件
[管理 NuGet 封裝] 對話方塊現在包含一個下拉式清單，其中提供了顯示發行前版本套件的選項。

![顯示發行前版本套件](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>遺失套件檔案時顯示套件還原按鈕
當您開啟封裝管理員主控台或 [管理員 NuGet 套件] 對話方塊時，NuGet 會檢查目前的解決方案是否已啟用套件還原模式，以及資料夾中是否遺失任何封裝檔案 `packages` 。 如果符合這兩個條件，NuGet 將會通知您，而且會顯示方便的 [還原] 按鈕。 按一下這個按鈕將會觸發 NuGet 來還原所有遺失的封裝。

![對話方塊上的 [封裝還原] 按鈕](./media/packagerestore-dialog.png)

![主控台上的 [封裝還原] 按鈕](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>新增解決方案層級的 packages.config 檔案
在舊版的 NuGet 中，每個專案都有一個檔案， `packages.config` 可追蹤該專案中安裝的 NuGet 套件。 不過，方案層級沒有類似的檔案可追蹤解決方案層級的封裝。 因此，沒有辦法可以還原解決方案層級的封裝。
這項功能現在已在 NuGet 1.7 中執行。 解決方案層級檔案 `packages.config` 會放置在 [ `.nuget` 方案根目錄] 下的資料夾底下，而且只會儲存方案層級的封裝。

### <a name="remove-new-package-command"></a>移除 New-Package 命令
由於使用量很低，因此已移除 New-Package 命令。 建議開發人員使用 nuget.exe 或方便的 NuGet 套件瀏覽器來建立封裝。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.7 已修正套件還原工作流程和網路/原始檔控制案例的許多錯誤。

如需 NuGet 1.7 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
