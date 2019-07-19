---
title: dotnet CLI NuGet 命令
description: 使用 dotnet 命令列介面的 NuGet 相關命令簡短參考。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327485"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI 命令

`dotnet`命令列介面 (CLI) 在 Windows、Mac OS X 和 Linux 上執行, 提供一些必要的命令, 例如安裝、還原和發行套件。 如果 dotnet 滿足您的需求, 就不需要使用`nuget.exe`。

如需使用這些命令來取用套件的範例, 請參閱[使用 DOTNET CLI 安裝和管理套件](../consume-packages/install-use-packages-dotnet-cli.md)。 如需使用這些命令建立套件的範例, 請參閱[使用 DOTNET CLI 建立和發佈套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。

如需`dotnet` CLI 的完整命令參考, 請參閱[.net Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>套件耗用量

- [**dotnet 新增套件**](/dotnet/core/tools/dotnet-add-package):將套件參考新增至專案檔, 然後執行`dotnet restore`以安裝封裝。
- [**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package):從專案檔中移除封裝參考。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):還原專案的相依性和工具。 截至 NuGet 4.0，這會執行與 `nuget restore` 相同的程式碼。
- [**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals):列出*全域封裝*、 *HTTP*快取和*暫存*資料夾的位置, 並清除這些資料夾的內容。
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new):[`nuget.config`](../reference/nuget-config-file.md)建立檔案以設定 NuGet 的行為。

## <a name="package-creation"></a>封裝建立

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):將程式碼封裝至 NuGet 套件。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):將套件發佈至 NuGet 伺服器。 適用于 nuget.org、Azure Artifacts 和[協力廠商 nuget 伺服器](../hosting-packages/overview.md)。
- [**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete):從 NuGet 伺服器刪除或取消列出封裝。 適用于 nuget.org、Azure Artifacts 和[協力廠商 nuget 伺服器](../hosting-packages/overview.md)。
