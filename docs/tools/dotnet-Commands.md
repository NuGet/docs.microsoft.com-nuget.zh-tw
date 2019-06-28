---
title: dotnet CLI NuGet 命令
description: 使用 dotnet 命令列介面的 NuGet 相關命令的簡短的參考。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426010"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="76db9-103">dotnet CLI 命令</span><span class="sxs-lookup"><span data-stu-id="76db9-103">dotnet CLI commands</span></span>

<span data-ttu-id="76db9-104">`dotnet`命令列介面 (CLI)，在 Windows、 Mac OS X 和 Linux 執行，提供數個重要的命令，例如安裝、 還原和發行套件。</span><span class="sxs-lookup"><span data-stu-id="76db9-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="76db9-105">如果 dotnet 滿足您的需求，不需要使用`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="76db9-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="76db9-106">如需使用這些命令，來取用套件的範例，請參閱[安裝和管理套件利用 dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="76db9-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="76db9-107">如需使用這些命令建立套件的範例，請參閱 [建立及發佈套件，使用 dotnet CLI].../ quickstart/create-and-publish-a-package-using-the-dotnet-cli.md）。</span><span class="sxs-lookup"><span data-stu-id="76db9-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="76db9-108">如需完整的命令參考`dotnet`CLI，請參閱 < [.NET Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="76db9-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="76db9-109">套件耗用量</span><span class="sxs-lookup"><span data-stu-id="76db9-109">Package consumption</span></span>

- <span data-ttu-id="76db9-110">[**dotnet 新增套件**](/dotnet/core/tools/dotnet-add-package):新增套件參考專案檔，然後執行`dotnet restore`安裝套件。</span><span class="sxs-lookup"><span data-stu-id="76db9-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="76db9-111">[**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package):從專案檔中移除套件參考。</span><span class="sxs-lookup"><span data-stu-id="76db9-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="76db9-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):還原相依性和專案的工具。</span><span class="sxs-lookup"><span data-stu-id="76db9-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="76db9-113">截至 NuGet 4.0，如此就會執行相同的程式碼`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="76db9-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="76db9-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals):列出位置*全域套件*， *http 快取*，並*temp*資料夾並清除這些資料夾的內容。</span><span class="sxs-lookup"><span data-stu-id="76db9-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="76db9-115">封裝建立</span><span class="sxs-lookup"><span data-stu-id="76db9-115">Package creation</span></span>

- <span data-ttu-id="76db9-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):套件的程式碼封裝到 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="76db9-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="76db9-117">截至 NuGet 4.0，如此就會執行相同的程式碼`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="76db9-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="76db9-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):將套件推送至伺服器並發行，適用於 nuget.org，Visual Studio Team Services 和第三方 NuGet 伺服器。</span><span class="sxs-lookup"><span data-stu-id="76db9-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="76db9-119">[**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete):刪除或取消列出套件從主應用程式，適用於 nuget.org，Visual Studio Team Services 和第三方 NuGet 伺服器。</span><span class="sxs-lookup"><span data-stu-id="76db9-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
