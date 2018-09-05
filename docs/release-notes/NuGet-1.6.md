---
title: NuGet 1.6 版的版本資訊
description: 版本資訊適用於 NuGet 1.6 包括已知的問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549008"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 版的版本資訊

[NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md) | [NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md)

於 2011 年 12 月 13 日發行 NuGet 1.6。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行的 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您已安裝較舊版本。

因應措施是只解除安裝 NuGet，然後再從 VS 延伸模組資源庫進行安裝。  請參閱 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) 以取得詳細資訊。

注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕已停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。

## <a name="features"></a>功能

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>支援語意版本設定和發行前版本套件
NuGet 1.6 版引進了支援語意版本控制 (SemVer)。 如需如何使用 SemVer 的詳細資訊，請參閱[版本控制說明文件](../create-packages/prerelease-packages.md)。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>使用 NuGet 不簽入套件 （套件還原）
NuGet 1.6 現在提供工作流程中的 NuGet 套件不會新增至原始檔控制，但改為會還原在建置階段如果遺失的第一級支援。 如需詳細資訊，請參閱[使用的 NuGet，而不需要認可至原始檔控制的套件](../consume-packages/packages-and-source-control.md)主題。

### <a name="item-templates-that-install-nuget-packages"></a>安裝 NuGet 套件的項目範本
為建置基礎的工作，以支援 Visual Studio 專案範本以預先安裝的 NuGet 套件，NuGet 1.6 也新增支援 Visual Studio 項目範本。 叫用中的範本時所安裝的 NuGet 套件時，項目範本可以有相關聯。

如需如何變更專案/項目範本，以安裝 NuGet 套件的詳細資訊，請參閱[Visual Studio 範本中的套件](../visual-studio-extensibility/visual-studio-templates.md)主題。

### <a name="support-for-disabling-package-sources"></a>停用套件來源的支援
多個套件來源設定時，NuGet 會安裝封裝及其相依性期間尋找套件的每個。 已關閉，因為某些原因可以嚴重會拖慢 NuGet 的套件來源。

NuGet 1.6 中，您無法移除封裝來源，但接著您必須記得的詳細資料，為您想要將其新增回去。

NuGet 1.6 版可讓您取消核取 停用它，但保留該套件來源。

![停用封裝](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.6 必須共 106 工作固定的項目。 95 這些已分類為 bug，10，這些是功能。

如需完整的工作清單項目固定在 NuGet 1.6 中，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
