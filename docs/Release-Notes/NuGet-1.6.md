---
title: "NuGet 1.6 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ed433790-99bf-4b71-92a8-17314bd49867
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.6 版的版本資訊。"
keywords: "NuGet 1.6 的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7824d62cb73c54205175ec742cfc26d1ca3aa741
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 版的版本資訊

[NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md) | [NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md)

NuGet 1.6 已於 2011 年 12 月 13 日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您正在執行 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您有安裝較舊的版本。

因應措施是只要解除安裝 NuGet，然後再從 VS 擴充功能庫進行安裝。  請參閱[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)如需詳細資訊。

注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕會停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。

## <a name="features"></a>功能

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>支援語意版本設定和套件發行前版本
NuGet 1.6 版引進了 (SemVer) 的語意版本設定的支援。 如需如何使用 SemVer 的詳細資訊，請參閱[版本控制文件](../create-packages/prerelease-packages.md)。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>使用 NuGet 而不要簽入的封裝 （封裝還原）
NuGet 1.6 現在具有第一級支援工作流程中的 NuGet 封裝不會加入至原始檔控制，但改為會還原在建置階段遺失。 如需詳細資訊，請參閱[不認可封裝至原始檔控制使用的 NuGet](../consume-packages/packages-and-source-control.md)主題。

### <a name="item-templates-that-install-nuget-packages"></a>安裝 NuGet 封裝的項目範本
支援預先安裝的 NuGet 封裝加入 Visual Studio 專案範本的工作為基礎，NuGet 1.6 也新增支援 Visual Studio 項目範本。 項目範本可以有相關的叫用中的範本時所安裝的 NuGet 套件。

如需有關如何變更要安裝 NuGet 封裝的專案/項目範本的詳細資訊，請參閱[封裝在 Visual Studio 範本](../visual-studio-extensibility/visual-studio-templates.md)主題。

### <a name="support-for-disabling-package-sources"></a>停用封裝來源的支援
當多個封裝來源的設定時，NuGet 安裝封裝及其相依性時看起來中每個封裝。 已關閉的原因可以嚴重會拖慢 NuGet 套件來源。

NuGet 1.6 前您無法移除封裝來源，但您必須記住的詳細資料，為您想要將它新增回。

NuGet 1.6 可讓您取消核取 要停用，但保留周圍的封裝來源。

![停用封裝](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.6 有工作項目固定 106 總數。 這些 95 已分類為 bug 和 10，這些功能。

如需完整的工作清單項目固定在 NuGet 1.6，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
