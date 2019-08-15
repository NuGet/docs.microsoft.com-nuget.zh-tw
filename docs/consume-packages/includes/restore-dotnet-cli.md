---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860612"
---
<span data-ttu-id="326ee-101">使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令來還原專案檔 (請參閱 [PackageReference](../../consume-packages/package-references-in-project-files.md)) 中所列的套件。</span><span class="sxs-lookup"><span data-stu-id="326ee-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="326ee-102">使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 自動完成還原。</span><span class="sxs-lookup"><span data-stu-id="326ee-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="326ee-103">截至 NuGet 4.0，這會執行與 `nuget restore` 相同的程式碼。</span><span class="sxs-lookup"><span data-stu-id="326ee-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="326ee-104">如同其他 `dotnet` CLI 命令，請先開啟命令列並切換至包含您專案檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="326ee-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="326ee-105">使用 `dotnet restore` 還原套件：</span><span class="sxs-lookup"><span data-stu-id="326ee-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```