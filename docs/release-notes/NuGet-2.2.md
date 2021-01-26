---
title: NuGet 2.2 版本資訊
description: NuGet 2.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780428"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 版本資訊

[NuGet 2.1 版本](../release-notes/nuget-2.1.md)  |  資訊[NuGet 2.2.1 版本](../release-notes/nuget-2.2.1.md)資訊

NuGet 2.2 已于2012年12月12日發行。

## <a name="visual-studio-quick-launch"></a>Visual Studio 快速啟動
在 Visual Studio 2012 中新增的其中一個新功能是 [ [快速啟動] 對話方塊](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。 NuGet 2.2 會擴充此對話方塊，讓它能夠使用快速啟動中輸入的搜尋字詞來初始化 [套件管理員] 對話方塊。 例如，在 [快速啟動] 中輸入 ' jquery ' 現在會在結果中包含一個選項，以搜尋與 ' jquery ' 相符的 NuGet 套件。

![Visual Studio 快速啟動中的 NuGet](./media/quick-launch.png)

選取此選項將會啟動「jquery」一詞的標準 NuGet 套件管理員搜尋體驗。

![預先填入的 NuGet 封裝管理員對話方塊](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>針對套件內容指定整個資料夾
NuGet 2.2 現在可讓您在檔案的元素中指定整個資料夾， `<file>` `.nuspec` 以包含該資料夾的所有內容。 例如，下列程式碼會在套件安裝至專案時，將封裝腳本資料夾中的所有腳本新增至 contents\scripts 資料夾。

```xml
<file src="scripts\" target="content\scripts"/>
```

**更新6/24/16：安裝套件時，會忽略 [內容] 資料夾中的空資料夾。**

## <a name="known-issues"></a>已知問題

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>使用套件管理員主控台時，F # 專案的套件安裝失敗
使用套件管理員主控台嘗試將 NuGet 套件安裝到 F # 專案時，會擲回 InvalidOperationException。 我們正積極使用 F # 小組來解決問題，但在此情況下，因應措施是透過 NuGet 的 [套件管理員] 對話方塊（而不是主控台）將 NuGet 套件安裝到 F # 專案中。 您[可以在 CodePlex 上取得詳細資訊](http://nuget.codeplex.com/workitem/2873)。


## <a name="bug-fixes"></a>Bug 修正
NuGet 2.2 包含許多 bug 修正。 如需 NuGet 2.2 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
