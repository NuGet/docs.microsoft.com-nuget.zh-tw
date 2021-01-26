---
title: dotnet CLI NuGet 命令
description: 使用 dotnet 命令列介面之 NuGet 相關命令的簡短參考。
author: JonDouglas
ms.author: jodou
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 5438354729ccc851bbbae6c0e7b9394d4226da52
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779997"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI 命令

`dotnet`命令列介面 (CLI) ，可在 Windows、Mac OS X 和 Linux 上執行，提供許多必要的命令，例如安裝、還原和發行套件。 如果 dotnet 滿足您的需求，就不需要使用 `nuget.exe` 。

如需使用這些命令來取用封裝的範例，請參閱 [使用 DOTNET CLI 安裝和管理套件](../consume-packages/install-use-packages-dotnet-cli.md)。 如需使用這些命令建立套件的範例，請參閱 [使用 DOTNET CLI 建立和發佈套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。

如需 cli 的完整命令參考 `dotnet` ，請參閱 [.net Core 命令列介面 (cli) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>套件耗用量

- [**dotnet add package**](/dotnet/core/tools/dotnet-add-package)：將套件參考新增至專案檔，然後執行 `dotnet restore` 以安裝套件。
- [**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package)：移除專案檔中的套件參考。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)：還原專案的相依性和工具。 截至 NuGet 4.0，這會執行與 `nuget restore` 相同的程式碼。
- [**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals)：列出 *全域封裝*、 *HTTP* 快取和 *暫存* 資料夾的位置，以及清除這些資料夾的內容。
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new)：建立檔案 [`nuget.config`](../reference/nuget-config-file.md) 以設定 NuGet 的行為。

## <a name="package-creation"></a>封裝建立

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)：將程式碼封裝到 NuGet 套件中。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)：將封裝發佈至 nuget 伺服器。 適用于 nuget.org、Azure Artifacts 和 [協力廠商 nuget 伺服器](../hosting-packages/overview.md)。
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete)：從 nuget 伺服器刪除或取消列出套件。 適用于 nuget.org、Azure Artifacts 和 [協力廠商 nuget 伺服器](../hosting-packages/overview.md)。
- [**dotnet nuget 驗證**](/dotnet/core/tools/dotnet-nuget-verify)：驗證已簽署的 nuget 套件。
