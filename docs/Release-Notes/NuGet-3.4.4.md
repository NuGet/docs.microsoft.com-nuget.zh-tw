---
title: "NuGet 3.4.4 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含 NuGet 3.4.4 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 3.4.4 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 版本資訊

[NuGet 3.4.3 版本資訊](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta 版本資訊](../release-notes/nuget-3.5-Beta.md)

此版本的主要焦點在於已 3.4.3 品質的改良版本與 Visual Studio 擴充功能的幾個修正 nuget.exe。

您可以下載 VSIX 和 nuget.exe[這裡](https://dist.nuget.org/index.html)。

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[完整的變更記錄](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[問題的清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>變更

- 組件的改進： 改進符號，封裝的功能與封裝`project.json`多[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- 尋找專案中更新命令失敗時所顯示的例外狀況 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- 從輸入讀取封裝類型`.nuspec`和`project.json`時封裝[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- 請 NuGet.Shared 非專案。 [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- 推入逾時做為 HTTP 回應逾時[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- 未來的時間與封裝檔案並不會使用其時間[ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- 更新`NuGet.Core.dll`版本來修正 XML 問題 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- 支援./NuGet.CommandLine.XPlat v\<詳細等級\>\<模式\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- 顯示而不還原錯誤`project.json`或`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- 當所需的版本不同時修復相依性版本[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)