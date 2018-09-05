---
title: NuGet 2.8.2 版本資訊
description: 版本資訊 NuGet 2.8.2 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551144"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 版本資訊

[NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 已於 2014 5 月 22 日發行。  此版本只包含變更 nuget.exe 命令列、 NuGet.Server 套件以及其他 NuGet 套件。  更新 Visual Studio 擴充功能或 WebMatrix 延伸模組未包含版本。

## <a name="notable-updates"></a>值得注意的更新

Nuget.exe 命令列和 NuGet.Server 套件 （適用於自我裝載的 NuGet 摘要） 中，是最值得注意的更新。

### <a name="important-nugetexe-bug-fixes"></a>重要的 nuget.exe Bug 修正

1. [nuget.exe 推送失敗，且會保留重試](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe 推送不會正確地傳送基本驗證認證](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 推送不會遵循暫時重新導向](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>NuGet.Server 重要 Bug 修正

1. [錯誤的 IsAbsoluteLatestVersion NuGet.Server 所傳回的值](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>已更新封裝

為 NuGet 套件更新運送的 nuget.exe 命令列和 NuGet.Server 修正。  沒有其他使用 2.8.2 也已更新的封裝。

以下是更新的套件清單：

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) （封裝，不是延伸模組）

## <a name="all-changes"></a>所有的變更
沒有 10 發行版本中已解決的問題。 如需完整的工作清單項目中已修正 NuGet 2.8.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。
