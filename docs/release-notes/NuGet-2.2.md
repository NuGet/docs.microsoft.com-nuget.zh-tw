---
title: NuGet 2.2 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.2 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545988"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 版本資訊

[NuGet 2.1 版本資訊](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 版本資訊](../release-notes/nuget-2.2.1.md)

NuGet 2.2 已於 2012 年 12 月 12 日發行。

## <a name="visual-studio-quick-launch"></a>Visual Studio 快速啟動
Visual Studio 2012 中已加入的新功能的其中一個已[快速啟動對話方塊](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。 NuGet 2.2 擴充這個對話方塊中，讓它可以在 快速啟動中輸入搜尋字詞以初始化 套件管理員 對話方塊。 在結果中搜尋相符的 'jquery' 的 NuGet 套件，現在快速啟動中輸入 'jquery' 包含例如的選項。

![Visual Studio 快速啟動中的 NuGet](./media/quick-launch.png)

選取此選項會啟動標準 NuGet 封裝管理員搜尋體驗的詞彙 'jquery'。

![預先填入的 NuGet 套件管理員 對話方塊](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>指定封裝內容的整個資料夾
NuGet 2.2 現在可讓您指定在整個資料夾`<file>`項目`.nuspec`檔案來包含所有該資料夾的內容。 例如，下列會導致所有指令碼套件的套件安裝至專案時，要加入至 contents\scripts 資料夾的指令碼資料夾。

```xml
<file src="scripts\" target="content\scripts"/>
```

**更新 6/24/16： 安裝套件時，會忽略 [內容] 資料夾中的空資料夾。**

## <a name="known-issues"></a>已知問題

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>使用套件管理員主控台時，套件安裝失敗的 F # 專案
嘗試將安裝到使用套件管理員主控台的 F # 專案的 NuGet 套件時，會擲回 InvalidOperationException。 我們正積極與 F # 小組若要解決此問題，但在此同時，因應措施是 NuGet 套件安裝到 F # 專案透過 NuGet 的套件管理員 對話方塊中，而不是  主控台。 [CodePlex 上提供的詳細資訊，是](http://nuget.codeplex.com/workitem/2873)。


## <a name="bug-fixes"></a>Bug 修正
NuGet ack 2.2 包含括許多錯誤修正。 如需完整的工作清單項目中已修正 NuGet 2.2，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
