---
title: NuGet 1.6 版本資訊
description: NuGet 1.6 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384133"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 版本資訊

[Nuget 1.5 版本](../release-notes/nuget-1.5.md)資訊 | [nuget 1.7 版本](../release-notes/nuget-1.7.md)資訊

NuGet 1.6 已于2011年12月13日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行 VS 2010 SP1，如果您已安裝舊版，則嘗試升級 NuGet 時可能會發生安裝錯誤。

因應措施是直接卸載 NuGet，然後從 VS 延伸模組資源庫進行安裝。  如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>。

注意：如果 Visual Studio 不允許您卸載擴充功能（[卸載] 按鈕已停用），您可能需要使用 [以系統管理員身分執行] 重新開機 Visual Studio。

## <a name="features"></a>功能

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>支援語義版本控制和發行前版本套件
NuGet 1.6 引進了對語義版本設定（SemVer）的支援。 如需有關如何使用 SemVer 的詳細資訊，請閱讀[版本設定檔](../create-packages/prerelease-packages.md)。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>使用 NuGet 而不簽入套件（封裝還原）
NuGet 1.6 現在對工作流程具有第一類支援，NuGet 套件不會新增至原始檔控制，而是在組建時還原（如果遺漏的話）。 如需詳細資訊，請閱讀[使用 NuGet 但不將封裝認可至原始檔控制](../consume-packages/packages-and-source-control.md)主題。

### <a name="item-templates-that-install-nuget-packages"></a>安裝 NuGet 套件的專案範本
NuGet 1.6 也會在支援預先安裝 NuGet 套件的工作上建立 Visual Studio 專案範本，也新增了 Visual Studio 專案範本的支援。 專案範本可以有相關聯的 NuGet 套件，並在叫用範本時加以安裝。

如需如何變更專案/專案範本以安裝 NuGet 套件的詳細資訊，請閱讀[Visual Studio 範本中的套件](../visual-studio-extensibility/visual-studio-templates.md)主題。

### <a name="support-for-disabling-package-sources"></a>支援停用封裝來源
設定多個套件來源時，NuGet 會在套件和其相依性的安裝期間，查看套件中的每一個。 基於某些原因而關閉的套件來源可能會嚴重地使 NuGet 變慢。

在 NuGet 1.6 之前，您可以移除套件來源，但當您想要將它重新加入時，必須記住的詳細資料。

NuGet 1.6 允許取消核取套件來源來停用它，但請將它保持在最上面。

![停用封裝](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.6 總共已修正106個工作專案。 95的分類為 bug，而其中10個是功能。

如需 NuGet 1.6 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
