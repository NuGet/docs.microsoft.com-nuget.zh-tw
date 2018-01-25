---
title: "NuGet 2.8.2 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含 NuGet 2.8.2 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.8.2 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f50bd1f0c981ef293a4d2ff425e0dffbdf58036c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 版本資訊

[NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 已於 2014 年 22 日發行。  此版本僅包含變更 nuget.exe 命令列、 NuGet.Server 套件以及其他 NuGet 封裝。  更新 Visual Studio 擴充功能或 WebMatrix 的擴充功能未包含版本。

## <a name="notable-updates"></a>值得注意的更新

最值得注意的更新已在命令列 nuget.exe 和 NuGet.Server （適用於封裝自我裝載的 NuGet 摘要）。

### <a name="important-nugetexe-bug-fixes"></a>重要 nuget.exe Bug 修正

1. [nuget.exe 推送失敗，且會持續重試一次](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe 推送不會正確傳送基本驗證認證](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 推送將不會遵循暫時重新導向](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>重要 NuGet.Server Bug 修正

1. [IsAbsoluteLatestVersion NuGet.Server 所傳回的值錯誤](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>更新套件

Nuget.exe 命令列和 NuGet.Server 修正隨附做為 NuGet 套件的更新。  沒有更新 2.8.2 以及其他封裝。

以下是已更新封裝的清單：

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) （封裝、 非副檔名）

## <a name="all-changes"></a>所有的變更
有一些 10 發行版本中解決的問題。 如需完整清單的工作項目固定在 NuGet 2.8.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。
