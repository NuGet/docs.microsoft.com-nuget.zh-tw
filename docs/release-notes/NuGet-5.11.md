---
title: NuGet 5.11 版本資訊
description: NuGet 5.11 的版本資訊，包括新功能、bug 修正及 dcr。
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728432"
---
# <a name="nuget-511-release-notes"></a>NuGet 5.11 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本 | 隨附於 .NET SDK |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.11 版](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup>與 .net Core 工作負載搭配 Visual Studio 2019 安裝
  
> [!NOTE]
> Visual Studio 16.11、MSBuild 16.11 和 .net 5.0.400 + 需要 NuGet.exe 5.11 或更新版本。

## <a name="summary-whats-new-in-511"></a>摘要：5.11 中的新功能

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**錯誤：**

* 工具-> 選項-> NuGet 封裝管理員字串會被截斷- [#10779](https://github.com/NuGet/Home/issues/10779)

* 引發 PackagesMissingStatusChanged 事件時停止回應- [#10854](https://github.com/NuGet/Home/issues/10854)

* NuGet 用戶端會忽略 NO_PROXY 設定， [#10902](https://github.com/NuGet/Home/issues/10902)

**[此版本修正的所有問題清單-5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[此版本中的認可清單-5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>歡迎意見反應

您的意見反應對我們非常寶貴。  如果此版本有任何問題，請查看我們的[GitHub 問題](https://github.com/NuGet/Home/issues)，並[Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/)現有的問題。  針對 NuGet 內的新問題，請報告[GitHub 問題](https://github.com/NuGet/Home/issues/new)。
針對一般 NuGet 體驗問題，請透過 [說明] > [回報 **問題**] 下的 [回報問題] 選項，讓我們知道您最愛的 IDE 中所找到的 [問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)。
