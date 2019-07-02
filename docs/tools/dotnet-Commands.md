---
title: dotnet CLI NuGet 命令
description: 使用 dotnet 命令列介面的 NuGet 相關命令的簡短的參考。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496472"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI 命令

`dotnet`命令列介面 (CLI)，在 Windows、 Mac OS X 和 Linux 執行，提供數個重要的命令，例如安裝、 還原和發行套件。 如果 dotnet 滿足您的需求，不需要使用`nuget.exe`。

如需使用這些命令，來取用套件的範例，請參閱[安裝和管理套件利用 dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md)。 如需使用這些命令建立套件的範例，請參閱[建立及發佈套件，使用 dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。

如需完整的命令參考`dotnet`CLI，請參閱 < [.NET Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>套件耗用量

- [**dotnet 新增套件**](/dotnet/core/tools/dotnet-add-package):新增套件參考專案檔，然後執行`dotnet restore`安裝套件。
- [**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package):從專案檔中移除套件參考。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):還原相依性和專案的工具。 截至 NuGet 4.0，如此就會執行相同的程式碼`nuget restore`。
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals):列出位置*全域套件*， *http 快取*，並*temp*資料夾並清除這些資料夾的內容。
- [**dotnet 新 nugetconfig**](/dotnet/core/tools/dotnet-new):會建立[ `nuget.config` ](../reference/nuget-config-file.md)檔案來設定 NuGet 行為。

## <a name="package-creation"></a>封裝建立

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):套件的程式碼封裝到 NuGet 套件。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):將封裝發佈至 NuGet 伺服器中。 適用於 nuget.org，Azure 的成品，並[協力廠商 NuGet 伺服器](../hosting-packages/overview.md)。
- [**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete):刪除或取消列出套件的 NuGet 伺服器。 適用於 nuget.org，Azure 的成品，並[協力廠商 NuGet 伺服器](../hosting-packages/overview.md)。
