---
title: "NuGet 2.8.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含 NuGet 2.8.1 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.8.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 版本資訊

[NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 版本資訊](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 已於 2014 年 4 月 2 日發行。

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 專案的支援
此版本現在支援下列新目標 framework moniker 用於目標 Windows Phone 8.1 專案：

* WindowsPhone81 / WP81 （適用於 silverlight 的 Windows Phone 專案）
* WindowsPhoneApp81 / WPA81 （適用於 WinRT 為基礎的 Windows Phone 應用程式專案）

### <a name="update-of-the-nuget-webmatrix-extension"></a>更新 NuGet WebMatrix 擴充
這個版本會更新 NuGet 用戶端到 WebMatrix 中找到[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，並使它 XDT 轉換等的功能。 更重要的是，2.6.1 核心更新可以讓 WebMatrix 用戶端安裝 NuGet 封裝，其中包含較新版本`.nuspec`結構描述，包括 ASP.NET NuGet 套件。

如需 WebMatrix 的擴充功能更新的詳細資訊，請參閱這些特定[版本資訊](../release-notes/nuget-2.6.1-for-WebMatrix.md)。

### <a name="bug-fixes"></a>Bug 修正
除了這些功能，這個版本的 NuGet 會包括其他 bug 修正。 有一些版本中解決的 16 總問題。 如需完整清單的工作項目固定在 NuGet 2.8.1，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping 與 Visual Studio"14"CTP
在 Visual Studio"14"CTP 3 2014 年 6 月發行中，NuGet 2.8.1 是箱子運送。 它支援那些功能仍會在長條上方與其他 2.8.1 VSIXes，例如 Visual Studio 2013。
