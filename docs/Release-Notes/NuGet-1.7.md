---
title: "NuGet 1.7 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df7becc6-993d-4d06-8495-a0c26748bdfa
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.7 的版本資訊。"
keywords: "NuGet 1.7 的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 420b40576cb3862f0e4406966f9ccca9fd1f39a1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 版版本資訊

[NuGet 1.6 版本資訊](../release-notes/nuget-1.6.md) | [NuGet 1.8 版本資訊](../release-notes/nuget-1.8.md)

NuGet 1.7 已於 2012 年 4 月 4 日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您正在執行 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您有安裝較舊的版本。

因應措施是只要解除安裝 NuGet，然後再從 VS 擴充功能庫進行安裝。  請參閱[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)如需詳細資訊。

注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕會停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。

## <a name="features"></a>功能

### <a name="support-opening-readmetxt-file-after-installation"></a>開啟安裝後的 readme.txt 檔案，以支援
如果您的封裝包含新 1.7，`readme.txt`它完成安裝程式套件後，檔案位於根目錄的套件，NuGet 會自動開啟此檔案。

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>在 [管理 NuGet 封裝] 對話方塊中顯示套件發行前版本
[管理 NuGet 封裝] 對話方塊現在包含下拉式清單會提供選項，以顯示套件發行前版本。

![顯示套件發行前版本](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>遺漏封裝檔案時顯示封裝還原按鈕
當您開啟 [封裝管理員主控台或管理員 NuGet 封裝] 對話方塊，NuGet 會檢查目前的方案是否已啟用的封裝還原模式，如果任何封裝檔案中遺漏`packages`資料夾。 如果這兩項條件都符合，NuGet 會通知您，並會顯示方便的 [還原] 按鈕。 按一下此按鈕將會觸發 NuGet 還原所有遺漏的套件。

![在對話方塊上的封裝還原按鈕](./media/packagerestore-dialog.png)

![在主控台上的封裝還原按鈕](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>新增解決方案層級 packages.config 檔案
在舊版的 NuGet，每個專案有`packages.config`會追蹤哪些 NuGet 封裝會安裝在該專案中的檔案。 不過，在方案層級追蹤的方案層級封裝沒有類似檔。 如此一來，已沒有還原方案層級的封裝。
NuGet 1.7 現在實作這項功能。 方案層級`packages.config`檔案位於`.nuget`下的方案資料夾的根和只有方案層級封裝會儲存。

### <a name="remove-new-package-command"></a>移除新增套件 命令
低使用量，因為已經移除 [新增套件] 命令。 開發人員建議使用 nuget.exe 或很方便的 NuGet 封裝總管 來建立封裝。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.7 已修正許多 bug 周圍的封裝還原，工作流程和網路/原始檔控制案例。

如需完整的工作清單項目固定在 NuGet 1.7，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
