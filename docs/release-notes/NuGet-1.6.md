---
title: NuGet 1.6 版本資訊
description: NuGet 1.6 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777018"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 版本資訊

[NuGet 1.5 版本](../release-notes/nuget-1.5.md)  |  資訊[NuGet 1.7 版本](../release-notes/nuget-1.7.md)資訊

NuGet 1.6 已于2011年12月13日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行的是 VS 2010 SP1，如果您已安裝較舊的版本，可能會在嘗試升級 NuGet 時發生安裝錯誤。

解決方法是直接卸載 NuGet，然後從 VS 延伸模組資源庫安裝它。  如需相關資訊，請參閱 <https://support.microsoft.com/kb/2581019> 。

注意：如果 Visual Studio 不允許您卸載擴充功能 () 停用 [卸載] 按鈕，那麼您可能需要使用 [以系統管理員身分執行] 來重新開機 Visual Studio。

## <a name="features"></a>功能

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>支援語義版本控制和發行前版本套件
NuGet 1.6 引進 (SemVer) 的語義版本設定支援。 如需有關如何使用 SemVer 的詳細資訊，請參閱 [版本設定檔](../create-packages/prerelease-packages.md)。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>在不簽入套件的情況下使用 NuGet (套件還原) 
NuGet 1.6 現在具有工作流程的第一個類別支援，NuGet 封裝不會新增至原始檔控制，而是在組建時還原（如果遺失的話）。 如需詳細資訊，請閱讀 [使用 NuGet，而不將套件認可至原始檔控制](../consume-packages/packages-and-source-control.md) 主題。

### <a name="item-templates-that-install-nuget-packages"></a>安裝 NuGet 套件的專案範本
為了支援預先安裝的 NuGet 套件來 Visual Studio 專案範本，NuGet 1.6 也加入了 Visual Studio 專案範本的支援。 專案範本可以具有在叫用範本時所安裝的相關聯 NuGet 套件。

如需如何變更專案/專案範本以安裝 NuGet 套件的詳細資訊，請參閱 [Visual Studio 範本主題中的套件](../visual-studio-extensibility/visual-studio-templates.md) 。

### <a name="support-for-disabling-package-sources"></a>支援停用套件來源
當您設定多個套件來源時，NuGet 會在套件安裝期間和其相依性的套件中尋找套件。 基於某個原因而關閉的套件來源可能會嚴重降低 NuGet 的速度。

在 NuGet 1.6 之前，您可以移除套件來源，但是當您想要將它重新加入時，必須記住的詳細資料。

NuGet 1.6 允許取消核取套件來源以將它停用，但請將其保留。

![停用封裝](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.6 總共修正了106個工作專案。 其中的95分類為 bug，而其中有10個是功能。

如需 NuGet 1.6 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
