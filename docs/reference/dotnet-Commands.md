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
# <a name="dotnet-cli-commands"></a><span data-ttu-id="e629c-103">dotnet CLI 命令</span><span class="sxs-lookup"><span data-stu-id="e629c-103">dotnet CLI commands</span></span>

<span data-ttu-id="e629c-104">`dotnet`命令列介面 (CLI) ，可在 Windows、Mac OS X 和 Linux 上執行，提供許多必要的命令，例如安裝、還原和發行套件。</span><span class="sxs-lookup"><span data-stu-id="e629c-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="e629c-105">如果 dotnet 滿足您的需求，就不需要使用 `nuget.exe` 。</span><span class="sxs-lookup"><span data-stu-id="e629c-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="e629c-106">如需使用這些命令來取用封裝的範例，請參閱 [使用 DOTNET CLI 安裝和管理套件](../consume-packages/install-use-packages-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="e629c-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="e629c-107">如需使用這些命令建立套件的範例，請參閱 [使用 DOTNET CLI 建立和發佈套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="e629c-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="e629c-108">如需 cli 的完整命令參考 `dotnet` ，請參閱 [.net Core 命令列介面 (cli) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="e629c-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="e629c-109">套件耗用量</span><span class="sxs-lookup"><span data-stu-id="e629c-109">Package consumption</span></span>

- <span data-ttu-id="e629c-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package)：將套件參考新增至專案檔，然後執行 `dotnet restore` 以安裝套件。</span><span class="sxs-lookup"><span data-stu-id="e629c-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="e629c-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package)：移除專案檔中的套件參考。</span><span class="sxs-lookup"><span data-stu-id="e629c-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="e629c-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)：還原專案的相依性和工具。</span><span class="sxs-lookup"><span data-stu-id="e629c-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="e629c-113">截至 NuGet 4.0，這會執行與 `nuget restore` 相同的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e629c-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="e629c-114">[**dotnet nuget 區域變數**](/dotnet/core/tools/dotnet-nuget-locals)：列出 *全域封裝*、 *HTTP* 快取和 *暫存* 資料夾的位置，以及清除這些資料夾的內容。</span><span class="sxs-lookup"><span data-stu-id="e629c-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="e629c-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new)：建立檔案 [`nuget.config`](../reference/nuget-config-file.md) 以設定 NuGet 的行為。</span><span class="sxs-lookup"><span data-stu-id="e629c-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="e629c-116">封裝建立</span><span class="sxs-lookup"><span data-stu-id="e629c-116">Package creation</span></span>

- <span data-ttu-id="e629c-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)：將程式碼封裝到 NuGet 套件中。</span><span class="sxs-lookup"><span data-stu-id="e629c-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="e629c-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)：將封裝發佈至 nuget 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e629c-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="e629c-119">適用于 nuget.org、Azure Artifacts 和 [協力廠商 nuget 伺服器](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e629c-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="e629c-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete)：從 nuget 伺服器刪除或取消列出套件。</span><span class="sxs-lookup"><span data-stu-id="e629c-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="e629c-121">適用于 nuget.org、Azure Artifacts 和 [協力廠商 nuget 伺服器](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e629c-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="e629c-122">[**dotnet nuget 驗證**](/dotnet/core/tools/dotnet-nuget-verify)：驗證已簽署的 nuget 套件。</span><span class="sxs-lookup"><span data-stu-id="e629c-122">[**dotnet nuget verify**](/dotnet/core/tools/dotnet-nuget-verify): Verifies a signed NuGet package.</span></span>
