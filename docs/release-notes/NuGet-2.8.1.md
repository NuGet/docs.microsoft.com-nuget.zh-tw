---
title: NuGet 2.8.1 版本資訊
description: NuGet 2.8.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776762"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 版本資訊

[NuGet 2.8 版本](../release-notes/nuget-2.8.md)  |  資訊[NuGet 2.8.2 版本](../release-notes/nuget-2.8.2.md)資訊

NuGet 2.8.1 發行于2014年4月2日。

## <a name="notable-features-in-the-release"></a>版本中的值得注意功能

### <a name="support-for-windows-phone-81-projects"></a>支援 Windows Phone 8.1 專案
此版本現在支援下列新的目標 framework 名字標記，可用來將 Windows Phone 8.1 專案設為目標：

* 以 Silverlight 為基礎的 Windows Phone 專案的 WindowsPhone81/WP81 () 
* 以 WinRT 為基礎 Windows Phone 應用程式專案的 WindowsPhoneApp81/WPA81 () 

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix 擴充功能的更新
此版本會將 WebMatrix 中找到的 NuGet 用戶端更新為 [nuget.exe](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，並引進 XDT 轉換等 it 功能。 更重要的是，2.6.1 core 更新可讓 WebMatrix 用戶端安裝 NuGet 套件，其中包含最新版本的 `.nuspec` 架構，包括 ASP.NET NuGet 套件。

如需有關 WebMatrix 擴充功能更新的詳細資訊，請參閱這些特定的 [版本](../release-notes/nuget-2.6.1-for-WebMatrix.md)資訊。

### <a name="bug-fixes"></a>Bug 修正
除了這些功能之外，此版本的 NuGet 還包含其他 bug 修正。 發行中已解決16個問題。 如需 NuGet 2.8.1 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。

### <a name="reshipping-with-visual-studio-14-ctp"></a>Visual Studio "14" CTP 的 Reshipping
在2014年6月3日發行的 Visual Studio "14" CTP 中，NuGet 2.8.1 隨附于 box。 It 支援的功能與其他 2.8.1 VSIXes （例如 Visual Studio 2013）保持不變。
