---
title: dotnet NuGet 命令
description: 簡短 NuGet 相關的命令使用 dotnet 命令列介面的參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="a2584-103">dotnet 命令</span><span class="sxs-lookup"><span data-stu-id="a2584-103">dotnet commands</span></span>

<span data-ttu-id="a2584-104">`dotnet`命令列介面，在 Windows、 Mac OS X 和 Linux 執行，提供數個重要 nuget.exe 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a2584-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="a2584-105">如果 dotnet 滿足您的需求，則不需要使用`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="a2584-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="a2584-106">如需完整資訊`dotnet`，請參閱[.NET Core 命令列介面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="a2584-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="a2584-107">封裝耗用量</span><span class="sxs-lookup"><span data-stu-id="a2584-107">Package consumption</span></span>

- <span data-ttu-id="a2584-108">[**將封裝加入 dotnet**](/dotnet/core/tools/dotnet-add-package): 封裝將參考加入至專案檔，然後執行`dotnet restore`安裝套件。</span><span class="sxs-lookup"><span data-stu-id="a2584-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="a2584-109">[**dotnet 移除封裝**](/dotnet/core/tools/dotnet-remove-package)： 從專案檔中移除封裝參考。</span><span class="sxs-lookup"><span data-stu-id="a2584-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="a2584-110">[**dotnet 還原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 還原的相依性和專案的工具。</span><span class="sxs-lookup"><span data-stu-id="a2584-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="a2584-111">為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="a2584-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="a2584-112">[**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals)： 列出之位置*全域封裝*， *http 快取*，和*temp*資料夾，並清除的內容這些資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a2584-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="a2584-113">建立封裝</span><span class="sxs-lookup"><span data-stu-id="a2584-113">Package creation</span></span>

- <span data-ttu-id="a2584-114">[**dotnet 套件**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 組件在 NuGet 封裝中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a2584-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="a2584-115">為準，NuGet 4.0，如此就會執行相同的程式碼做為`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="a2584-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="a2584-116">[**dotnet nuget 發送**](/dotnet/core/tools/dotnet-nuget-push)： 將封裝推入到伺服器並將其發佈，適用於 nuget.org、 Visual Studio Team Services，與協力廠商的 NuGet 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a2584-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="a2584-117">[**dotnet nuget 刪除**](/dotnet/core/tools/dotnet-nuget-delete)： 刪除或 unlists 從主應用程式，適用於 nuget.org、 Visual Studio Team Services，與協力廠商的 NuGet 伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="a2584-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>