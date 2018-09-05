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
# <a name="dotnet-commands"></a><span data-ttu-id="7fed8-103">dotnet 命令</span><span class="sxs-lookup"><span data-stu-id="7fed8-103">dotnet commands</span></span>

<span data-ttu-id="7fed8-104">`dotnet`命令列介面，在 Windows、 Mac OS X 和 Linux 執行，提供一些基本的 nuget.exe 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7fed8-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="7fed8-105">如果 dotnet 滿足您的需求，不需要使用`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="7fed8-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="7fed8-106">如需完整資訊`dotnet`，請參閱 < [.NET Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="7fed8-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="7fed8-107">套件耗用量</span><span class="sxs-lookup"><span data-stu-id="7fed8-107">Package consumption</span></span>

- <span data-ttu-id="7fed8-108">[**dotnet 新增套件**](/dotnet/core/tools/dotnet-add-package)： 新增套件參考專案檔，然後執行`dotnet restore`安裝套件。</span><span class="sxs-lookup"><span data-stu-id="7fed8-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="7fed8-109">[**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package)： 從專案檔中移除套件參考。</span><span class="sxs-lookup"><span data-stu-id="7fed8-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="7fed8-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 還原相依性和專案的工具。</span><span class="sxs-lookup"><span data-stu-id="7fed8-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="7fed8-111">截至 NuGet 4.0，如此就會執行相同的程式碼`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="7fed8-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="7fed8-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals)： 列出之位置*全域套件*， *http 快取*，以及*temp*資料夾，並清除的內容這些資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7fed8-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="7fed8-113">封裝建立</span><span class="sxs-lookup"><span data-stu-id="7fed8-113">Package creation</span></span>

- <span data-ttu-id="7fed8-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 套件的程式碼封裝到 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="7fed8-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="7fed8-115">截至 NuGet 4.0，如此就會執行相同的程式碼`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="7fed8-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="7fed8-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)： 將套件推送至伺服器並將其發佈，適用於 nuget.org，Visual Studio Team Services 和第三方 NuGet 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7fed8-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="7fed8-117">[**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete)： 刪除或取消列出套件，以從主應用程式，適用於 nuget.org，Visual Studio Team Services 和第三方 NuGet 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7fed8-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
