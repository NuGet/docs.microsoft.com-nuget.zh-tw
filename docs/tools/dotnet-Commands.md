---
title: dotnet NuGet 命令
description: 使用 dotnet 命令列介面的 NuGet 相關命令的簡短的參考。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546312"
---
# <a name="dotnet-commands"></a>dotnet 命令

`dotnet`命令列介面，在 Windows、 Mac OS X 和 Linux 執行，提供一些基本的 nuget.exe 命令，如下所示。 如果 dotnet 滿足您的需求，不需要使用`nuget.exe`。

如需完整資訊`dotnet`，請參閱 < [.NET Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>套件耗用量

- [**dotnet 新增套件**](/dotnet/core/tools/dotnet-add-package)： 新增套件參考專案檔，然後執行`dotnet restore`安裝套件。
- [**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package)： 從專案檔中移除套件參考。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 還原相依性和專案的工具。 截至 NuGet 4.0，如此就會執行相同的程式碼`nuget restore`。
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals)： 列出之位置*全域套件*， *http 快取*，以及*temp*資料夾，並清除的內容這些資料夾中。

## <a name="package-creation"></a>封裝建立

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 套件的程式碼封裝到 NuGet 套件。 截至 NuGet 4.0，如此就會執行相同的程式碼`nuget pack`。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)： 將套件推送至伺服器並將其發佈，適用於 nuget.org，Visual Studio Team Services 和第三方 NuGet 伺服器。
- [**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete)： 刪除或取消列出套件，以從主應用程式，適用於 nuget.org，Visual Studio Team Services 和第三方 NuGet 伺服器。
