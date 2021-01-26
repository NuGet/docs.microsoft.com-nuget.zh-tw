---
title: NuGet 2.2.1 版本資訊
description: NuGet 2.2.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776808"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 版本資訊

[NuGet 2.2 版本](../release-notes/nuget-2.2.md)  |  資訊[NuGet 2.5 版本](../release-notes/nuget-2.5.md)資訊

NuGet 2.2.1 發行于2013年2月15日。  VS 延伸模組的版本號碼為2.2.40116.9051。

## <a name="localization-refresh"></a>當地語系化更新
當 NuGet 隨附于 Visual Studio 2012 的一部分時，會完整地當地語系化為英文 + 13 種其他語言。  從那時起，NuGet 2.1 和2.2 已出貨，但當地語系化尚未重新整理。  NuGet 2.2.1 版本會更新我們的當地語系化。

NuGet 的 UI 和 PowerShell 主控台會當地語系化成下列語言：

1. 簡體中文
1. 繁體中文
1. 捷克文
1. 英文
1. 法文
1. 德文
1. 義大利文
1. 日文
1. 韓文
1. 波蘭文
1. 葡萄牙文 (巴西)
1. 俄文
1. 西班牙文
1. 土耳其文

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio 範本支援多個預先安裝的套件存放庫
如果您產生 Visual Studio 範本，您可以使用 NuGet 將 [套件預先安裝](../visual-studio-extensibility/visual-studio-templates.md) 為範本的一部分。  到目前為止，這項功能會限制所有需要來自相同來源的套件。  不過，使用 NuGet 2.2.1，您可以從範本、VSIX 或登錄) 中定義之磁片上的資料夾中，安裝多個存放庫 (的套件。

這項功能的主要案例是自訂的 ASP.NET 專案範本。  內建的 ASP.NET 範本使用預先安裝的套件，從本機磁片提取套件。  您現在可以建立自訂 ASP.NET 專案範本，以使用 ASP.NET 所安裝的現有套件，但是將額外的 NuGet 套件新增至您的範本。

## <a name="bug-fixes"></a>Bug 修正
NuGet 2.2.1 包含一些目標錯誤修正。 如需 NuGet 2.2.1 中已修正的工作專案清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。


## <a name="known-issues"></a>已知問題

如果您要擴充 ASP.NET 專案範本，所有預先安裝的套件存放庫都必須使用相同的 `isPreunzipped` 屬性值。
