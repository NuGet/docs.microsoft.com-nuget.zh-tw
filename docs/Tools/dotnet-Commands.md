---
title: "dotNet NuGet 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "簡短 NuGet 相關的命令使用 dotnet 命令列介面的參考。"
keywords: "dotnet NuGet 命令 dotnet、 組件、 dotnet 還原、 dotnet nuget 區域變數、 dotnet nuget 發送 dotnet nuget 刪除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="d3af9-104">dotNet 命令</span><span class="sxs-lookup"><span data-stu-id="d3af9-104">dotNet commands</span></span>

<span data-ttu-id="d3af9-105">`dotnet`命令列介面，在 Windows、 Mac OS X 和 Linux 執行，提供數個重要 nuget.exe 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d3af9-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="d3af9-106">如果 dotnet 滿足您的需求，則不需要使用`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="d3af9-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="d3af9-107">如需完整資訊`dotnet`，請參閱[.NET Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="d3af9-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="d3af9-108">封裝耗用量</span><span class="sxs-lookup"><span data-stu-id="d3af9-108">Package consumption</span></span>

- <span data-ttu-id="d3af9-109">[**將封裝加入 dotnet**](/dotnet/core/tools/dotnet-add-package): 封裝將參考加入至專案檔，然後執行`dotnet restore`安裝套件。</span><span class="sxs-lookup"><span data-stu-id="d3af9-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="d3af9-110">[**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package)： 從專案檔中移除封裝參考。</span><span class="sxs-lookup"><span data-stu-id="d3af9-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="d3af9-111">[**dotnet 還原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 還原的相依性和專案的工具。</span><span class="sxs-lookup"><span data-stu-id="d3af9-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d3af9-112">為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="d3af9-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d3af9-113">[**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals)： 清除或列出本機 NuGet 資源，例如 http 要求的快取、 暫時快取，以及 [全機器全域 packages] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d3af9-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="d3af9-114">建立封裝</span><span class="sxs-lookup"><span data-stu-id="d3af9-114">Package creation</span></span>

- <span data-ttu-id="d3af9-115">[**dotnet 套件**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 組件在 NuGet 封裝中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d3af9-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="d3af9-116">為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="d3af9-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="d3af9-117">[**dotnet nuget 發送**](/dotnet/core/tools/dotnet-nuget-push)： 將封裝推入到伺服器並將其發佈，適用於 nuget.org、 Visual Studio Team Services，與協力廠商的 NuGet 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d3af9-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="d3af9-118">[**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete)： 刪除或 unlists 從主應用程式，適用於 nuget.org、 Visual Studio Team Services，與協力廠商的 NuGet 伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="d3af9-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
