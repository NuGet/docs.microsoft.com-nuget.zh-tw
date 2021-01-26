---
title: NuGet 2.8.2 版本資訊
description: NuGet 2.8.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780375"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 版本資訊

[NuGet 2.8.1 版本](../release-notes/nuget-2.8.1.md)  |  資訊[NuGet 2.8.3 版本](../release-notes/nuget-2.8.3.md)資訊

已于2014年5月22日發行 NuGet 2.8.2。  此版本只包含 nuget.exe 命令列、NuGet. 伺服器套件和其他 NuGet 套件的變更。  版本不包含更新的 Visual Studio 延伸模組或 WebMatrix 延伸模組。

## <a name="notable-updates"></a>值得注意的更新

最值得注意的更新是在 nuget.exe 命令列中，而 (適用于自我裝載 NuGet 摘要) 的 NuGet. 伺服器套件。

### <a name="important-nugetexe-bug-fixes"></a>重要 nuget.exe 錯誤修正

1. [nuget.exe 推送失敗並繼續重試](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe 推送不會正確傳送基本驗證認證](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 推送不會遵循暫時重新導向](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>重要的 NuGet。伺服器錯誤修正

1. [Nuget.exe 傳回的 IsAbsoluteLatestVersion 值錯誤。伺服器](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>更新的套件

nuget.exe 命令列和 NuGet. 伺服器修正會隨附于 NuGet 套件更新。  另外還有其他套件也會以2.8.2 更新。

以下是已更新的套件清單：

1. [Nuget.exe](https://www.nuget.org/packages/NuGet.Core/)
1. [Nuget.exe](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [Nuget.exe](https://www.nuget.org/packages/NuGet.Build/)
1. [VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (套件，而不是延伸模組) 

## <a name="all-changes"></a>所有變更
發行中已解決10個問題。 如需 NuGet 2.8.2 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。
