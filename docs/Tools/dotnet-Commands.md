---
title: dotNet NuGet 命令 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 簡短 NuGet 相關的命令使用 dotnet 命令列介面的參考。
keywords: dotnet NuGet 命令 dotnet、 組件、 dotnet 還原、 dotnet nuget 區域變數、 dotnet nuget 發送 dotnet nuget 刪除
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 352145701fba509e21e774a429d227e7427a1f0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="dotnet-commands"></a>dotNet 命令

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
