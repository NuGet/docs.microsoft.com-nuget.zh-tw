---
title: "dotNet NuGet 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "簡短 NuGet 相關的命令使用 dotnet 命令列介面的參考。"
keywords: "dotnet NuGet 命令 dotnet、 組件、 dotnet 還原、 dotnet nuget 區域變數、 dotnet nuget 發送 dotnet nuget 刪除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d020e62b8bd04c8f4a75756fb30ebcf13ffdb1b3
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="dotnet-commands"></a>dotNet 命令

DotNet 命令列介面，在 Windows、 Mac OS X 和 Linux 執行，提供一些基本 nuget.exe 命令如下所示。 其中 dotnet 提供所需的命令，則不需要下載 nuget.exe。

- [**dotnet 套件**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 組件在 NuGet 封裝中的程式碼。 為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget pack`。
- [**dotnet 還原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 還原的相依性和專案的工具。 為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget restore`。
- [**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals)： 清除或列出本機 NuGet 資源，例如 http-要求快取、 暫時快取或整個電腦的全域 packages 資料夾。
- [**dotnet nuget 發送**](/dotnet/core/tools/dotnet-nuget-push)： 將封裝推入到伺服器並將其發佈，適用於 nuget.org、 Visual Studio Team Services 或任何協力廠商的 NuGet 伺服器。
- [**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete)： 刪除或 unlists 來源伺服器，適用於 nuget.org、 Visual Studio Team Services 或任何協力廠商的 NuGet 伺服器的封裝。
