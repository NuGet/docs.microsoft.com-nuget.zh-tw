---
title: NuGet 2.2.1 版本資訊
description: 版本資訊包含 NuGet 2.2.1 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819289"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 版本資訊

[NuGet 2.2 版本資訊](../release-notes/nuget-2.2.md) | [NuGet 2.5 版本資訊](../release-notes/nuget-2.5.md)

NuGet 2.2.1 已於 2013 年 2 月 15 日發行。  VS 擴充功能版本號碼是 2.2.40116.9051。

## <a name="localization-refresh"></a>當地語系化的重新整理
NuGet 隨附的 Visual Studio 2012，當它已完全當地語系化成英文 + 13 其他語言。  從那時起，NuGet 2.1 和 2.2 已出貨，但當地語系化有尚未重新整理。  NuGet 2.2.1 版本重新整理我們當地語系化。

NuGet 的 UI 及 PowerShell 主控台會當地語系化成下列語言：

1. 中文 (簡體)
1. 和 SharePoint 2010 顯示的
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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio 範本可支援多個預先安裝的封裝儲存機制
如果您產生 Visual Studio 範本，您可以使用 NuGet[預先安裝套件](../visual-studio-extensibility/visual-studio-templates.md)做為範本的一部分。  到目前為止，這項功能有一項限制的所有封裝需要來自相同的來源。  隨 NuGet 2.2.1，您可以從多個 （範本、 在 VSIX 中或在登錄中定義的磁碟上的資料夾） 內的儲存機制安裝套件。

這項功能的主要案例是自訂的 ASP.NET 專案範本。  內建 ASP.NET 範本使用預先安裝的套件，提取從本機磁碟的封裝。  您現在可以建立自訂 ASP.NET 專案範本使用 asp.net 安裝現有的封裝，但將額外的 NuGet 封裝加入至您的範本。

## <a name="bug-fixes"></a>Bug 修正
NuGet 2.2.1 包含幾個目標的 bug 修正。 如需工作的清單項目固定在 NuGet 2.2.1，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。


## <a name="known-issues"></a>已知問題

如果您要擴充 ASP.NET 專案範本，所有預先安裝的封裝儲存機制必須使用相同的值`isPreunzipped`屬性。
