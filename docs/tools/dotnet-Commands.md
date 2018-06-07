---
title: dotnet NuGet 命令
description: 簡短 NuGet 相關的命令使用 dotnet 命令列介面的參考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817010"
---
# <a name="dotnet-commands"></a>dotnet 命令

`dotnet`命令列介面，在 Windows、 Mac OS X 和 Linux 執行，提供數個重要 nuget.exe 命令，如下所示。 如果 dotnet 滿足您的需求，則不需要使用`nuget.exe`。

如需完整資訊`dotnet`，請參閱[.NET Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>封裝耗用量

- [**將封裝加入 dotnet**](/dotnet/core/tools/dotnet-add-package): 封裝將參考加入至專案檔，然後執行`dotnet restore`安裝套件。
- [**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package)： 從專案檔中移除封裝參考。
- [**dotnet 還原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 還原的相依性和專案的工具。 為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget restore`。
- [**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals)： 列出之位置*全域封裝*， *http 快取*，和*temp*資料夾，並清除的內容這些資料夾中。

## <a name="package-creation"></a>建立封裝

- [**dotnet 套件**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 組件在 NuGet 封裝中的程式碼。 為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget pack`。
- [**dotnet nuget 發送**](/dotnet/core/tools/dotnet-nuget-push)： 將封裝推入到伺服器並將其發佈，適用於 nuget.org、 Visual Studio Team Services，與協力廠商的 NuGet 伺服器。
- [**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete)： 刪除或 unlists 從主應用程式，適用於 nuget.org、 Visual Studio Team Services，與協力廠商的 NuGet 伺服器的封裝。
