---
title: "dotNet NuGet 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "簡短 NuGet 相關的命令使用 dotnet 命令列介面的參考。"
keywords: "dotnet NuGet 命令 dotnet、 組件、 dotnet 還原、 dotnet nuget 區域變數、 dotnet nuget 發送 dotnet nuget 刪除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="02190-104">dotNet 命令</span><span class="sxs-lookup"><span data-stu-id="02190-104">dotNet commands</span></span>

<span data-ttu-id="02190-105">DotNet 命令列介面，在 Windows、 Mac OS X 和 Linux 執行，提供一些基本 nuget.exe 命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="02190-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="02190-106">其中 dotnet 提供所需的命令，則不需要下載 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="02190-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="02190-107">[**dotnet 套件**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 組件在 NuGet 封裝中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="02190-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="02190-108">為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="02190-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="02190-109">[**dotnet 還原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 還原的相依性和專案的工具。</span><span class="sxs-lookup"><span data-stu-id="02190-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="02190-110">為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="02190-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="02190-111">[**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals)： 清除或列出本機 NuGet 資源，例如 http-要求快取、 暫時快取或整個電腦的全域 packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="02190-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="02190-112">[**dotnet nuget 發送**](/dotnet/core/tools/dotnet-nuget-push)： 將封裝推入到伺服器並將其發佈，適用於 nuget.org、 Visual Studio Team Services 或任何協力廠商的 NuGet 伺服器。</span><span class="sxs-lookup"><span data-stu-id="02190-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="02190-113">[**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete)： 刪除或 unlists 來源伺服器，適用於 nuget.org、 Visual Studio Team Services 或任何協力廠商的 NuGet 伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="02190-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
