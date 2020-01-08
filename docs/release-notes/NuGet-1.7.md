---
title: NuGet 1.7 版本資訊
description: NuGet 1.7 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383315"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 版本資訊

[Nuget 1.6 版本](../release-notes/nuget-1.6.md)資訊 | [nuget 1.8 版本](../release-notes/nuget-1.8.md)資訊

NuGet 1.7 已于2012年4月4日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行 VS 2010 SP1，如果您已安裝舊版，則嘗試升級 NuGet 時可能會發生安裝錯誤。

因應措施是直接卸載 NuGet，然後從 VS 延伸模組資源庫進行安裝。  如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>。

注意：如果 Visual Studio 不允許您卸載擴充功能（[卸載] 按鈕已停用），您可能需要使用 [以系統管理員身分執行] 重新開機 Visual Studio。

## <a name="features"></a>功能

### <a name="support-opening-readmetxt-file-after-installation"></a>支援在安裝後開啟 readme.txt 檔案
1\.7 的新功能，如果您的套件在套件的根目錄包含 `readme.txt` 檔案，NuGet 會在完成封裝的安裝後自動開啟此檔案。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>[管理 NuGet 封裝] 對話方塊中的 [顯示發行前版本套件]
[管理 NuGet 封裝] 對話方塊現在包含一個下拉式清單，其中提供可顯示發行前版本套件的選項。

![顯示發行前版本套件](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>遺失套件檔案時顯示封裝還原按鈕
當您開啟 [套件管理員主控台] 或 [管理員 NuGet 套件] 對話方塊時，NuGet 會檢查目前的解決方案是否已啟用封裝還原模式，以及是否有任何封裝檔案從 `packages` 資料夾中遺失。 如果符合這兩個條件，NuGet 將會通知您，而且會顯示方便的 [還原] 按鈕。 按一下此按鈕會觸發 NuGet，以還原所有遺失的封裝。

![對話方塊上的 [封裝還原] 按鈕](./media/packagerestore-dialog.png)

![主控台上的 [封裝還原] 按鈕](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>新增方案層級的封裝 .config 檔案
在舊版的 NuGet 中，每個專案都有一個 `packages.config` 檔案，可追蹤該專案中安裝的 NuGet 套件。 不過，解決方案層級沒有類似的檔案可以追蹤解決方案層級的封裝。 因此，沒有任何方法可以還原解決方案層級的封裝。
這項功能現在已在 NuGet 1.7 中執行。 解決方案層級的 `packages.config` 檔案會放在 [方案根目錄] 底下的 [`.nuget`] 資料夾底下，而且只會儲存解決方案層級的封裝。

### <a name="remove-new-package-command"></a>移除新的-封裝命令
由於使用量過低，已移除新的-Package 命令。 建議開發人員使用 nuget.exe 或方便的 NuGet 套件瀏覽器來建立封裝。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.7 已針對套件還原工作流程和網路/原始檔控制案例，修正許多 bug。

如需 NuGet 1.7 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
