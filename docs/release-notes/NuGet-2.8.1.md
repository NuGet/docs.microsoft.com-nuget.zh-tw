---
title: NuGet 2.8.1 版本資訊
description: NuGet 2.8.1 所包括的版本資訊的已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545235"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 版本資訊

[NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 版本資訊](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 已於 2014 年 4 月 2 日發行。

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 專案的支援
此版本現在支援下列新目標 framework moniker 可以用於以 Windows Phone 8.1 為目標的專案：

* WindowsPhone81 / WP81 （適用於 Silverlight 為基礎的 Windows Phone 專案）
* WindowsPhoneApp81 / WPA81 （針對 WinRT 型的 Windows Phone 應用程式專案）

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix 延伸模組的更新
這個版本會更新到 WebMatrix 中找到 NuGet 用戶端[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，並使它等 XDT 轉換與功能。 更重要的是，2.6.1 核心更新可讓 WebMatrix 用戶端安裝包含較新版本的 NuGet 套件`.nuspec`結構描述，其中包含 ASP.NET NuGet 封裝。

如需詳細的 WebMatrix 的擴充功能更新的詳細資訊，請參閱這些特定[版本資訊](../release-notes/nuget-2.6.1-for-WebMatrix.md)。

### <a name="bug-fixes"></a>Bug 修正
除了這些功能，這個版本的 NuGet 會包括其他 bug 修正。 發生在版本中解決的 16 總問題。 如需完整的工作清單項目中已修正 NuGet 2.8.1，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping 使用 Visual Studio"14"CTP
在 Visual Studio"14"CTP 3 2014 年 6 月發行，NuGet 2.8.1 隨附在方塊中。 它支援的功能仍在 par 與其他 2.8.1 VSIXes 像是 Visual Studio 2013。
