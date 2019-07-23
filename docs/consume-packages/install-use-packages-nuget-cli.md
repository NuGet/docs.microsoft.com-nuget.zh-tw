---
title: 使用 nuget.exe CLI 管理 NuGet 套件
description: 使用 nuget.exe CLI 以處理 NuGet 套件的指示。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a7177b956930835693921163e634321548c22462
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842374"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="a0b9c-103">使用 nuget.exe CLI 管理套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="a0b9c-104">CLI 工具可讓您輕鬆地在專案和解決方案中更新及還原 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="a0b9c-105">此工具會在 Windows 上提供所有的 NuGet 功能，在 Mono 底下執行時也在 Mac 和 Linux 上提供大部分功能。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="a0b9c-106">Nuget.exe CLI 適用於 .NET Framework 專案和非 SDK 樣式專案 (例如，以 .NET Standard 程式庫為目標的非 SDK 樣式專案)。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-106">The nuget.exe CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="a0b9c-107">如果您使用已移轉到 `PackageReference` 的非 SDK 樣式專案，請改為使用 dotnet CLI。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the dotnet CLI instead.</span></span> <span data-ttu-id="a0b9c-108">NuGet CLI 需要 [packages.config](../reference/packages-config.md) 檔案來進行套件參考。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-108">The NuGet CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="a0b9c-109">在大部分情況下，我們建議將使用 `packages.config` 的[非 SDK 樣式專案移轉](../reference/migrate-packages-config-to-package-reference.md)至 PackageReference，然後您便可以使用 dotnet CLI 而不是 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the dotnet CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="a0b9c-110">移轉目前不適用於 C++ 和 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="a0b9c-111">本文顯示一些最常用 nuget.exe CLI 命令的基本使用方式。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-111">This article shows you basic usage for a few of the most common nuget.exe CLI commands.</span></span> <span data-ttu-id="a0b9c-112">針對這些命令的大部分，CLI 工具會在目前的目錄中尋找專案檔，除非在命令中指定專案檔。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="a0b9c-113">如需您可以使用的命令和引數完整清單，請參閱 [nuget.exe CLI 參考](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0b9c-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-114">Prerequisites</span></span>

- <span data-ttu-id="a0b9c-115">安裝 `nuget.exe` CLI，作法是從 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下載它、將該 `.exe` 檔案儲存至適當的資料夾，然後將該資料夾新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="a0b9c-116">安裝套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-116">Install a package</span></span>

<span data-ttu-id="a0b9c-117">[install](../tools/cli-ref-install.md) 命令會下載並安裝套件至專案，預設為目前的資料夾，且使用指定的套件來源。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-117">The [install](../tools/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="a0b9c-118">請將新套件安裝到專案根目錄中的 *packages* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0b9c-119">`install` 命令不會修改專案檔或 *packages.config*；如此，它類似於 `restore`，因為它只會將套件新增至磁碟，但不會變更專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="a0b9c-120">若要新增相依性，請在 Visual Studio 中透過套件管理員 UI 或主控台來新增套件，或是修改 *packages.config*，然後執行 `install` 或 `restore`。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="a0b9c-121">開啟命令列並切換至包含您專案檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="a0b9c-122">使用下列命令，將 NuGet 套件安裝到 *packages* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="a0b9c-123">若要將 `Newtonsoft.json` 套件安裝到 *packages* 資料夾，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a0b9c-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="a0b9c-124">或者，您可以使用下列命令，使用現有的 `packages.config` 檔案將 NuGet 套件安裝到 *packages* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="a0b9c-125">這不會將套件新增至您的專案相依性，但會將它安裝在本機。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="a0b9c-126">安裝特定版本的套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-126">Install a specific version of a package</span></span>

<span data-ttu-id="a0b9c-127">如果當您使用 [install](../tools/cli-ref-install.md) 命令時未指定版本，NuGet 會安裝最新版的套件。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-127">If the version is not specified when you use the [install](../tools/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="a0b9c-128">您也可以安裝特定版本的 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="a0b9c-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="a0b9c-129">例如，若要新增 12.0.1 版的 `Newtonsoft.json` 套件，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="a0b9c-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="a0b9c-130">如需 `install` 限制和行為的詳細資訊，請參閱[安裝套件](#install-a-package)。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="a0b9c-131">移除套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-131">Remove a package</span></span>

<span data-ttu-id="a0b9c-132">若要刪除一或多個套件，請從 *packages* 資料夾刪除您想要移除的套件。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="a0b9c-133">如果您想要重新安裝套件，請使用 `restore` 或 `install` 命令。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="a0b9c-134">列出套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-134">List packages</span></span>

<span data-ttu-id="a0b9c-135">您可以使用 [list](../tools/cli-ref-list.md) 命令顯示來自指定來源的套件清單。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-135">You can display a list of packages from a given source using the [list](../tools/cli-ref-list.md) command.</span></span> <span data-ttu-id="a0b9c-136">使用 `-Source` 選項以限制搜尋。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="a0b9c-137">例如，列出 *packages* 資料夾中的套件。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="a0b9c-138">如果您使用搜尋字詞，搜尋會包含套件名稱、標籤和套件描述。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="a0b9c-139">更新個別套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-139">Update an individual package</span></span>

<span data-ttu-id="a0b9c-140">除非您指定套件版本，否則當您使用 `install` 命令時 NuGet 會安裝最新版套件。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="a0b9c-141">更新所有套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-141">Update all packages</span></span>

<span data-ttu-id="a0b9c-142">使用 [update](../tools/cli-ref-update.md) 命令來更新所有套件。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-142">Use the [update](../tools/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="a0b9c-143">將專案中的所有套件 (使用 `packages.config`) 更新為最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="a0b9c-144">建議您先執行 `restore`，再執行 `update`。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="a0b9c-145">還原套件</span><span class="sxs-lookup"><span data-stu-id="a0b9c-145">Restore packages</span></span>

<span data-ttu-id="a0b9c-146">使用 [restore](../tools/cli-ref-restore.md) 命令，它會下載並安裝 *packages* 資料夾遺漏的任何套件。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-146">Use the [restore](../tools/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="a0b9c-147">`restore` 只會將套件新增至磁碟，但不會變更專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="a0b9c-148">若要還原專案相依性，請修改 `packages.config`，然後使用 `restore` 命令。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="a0b9c-149">如同其他 `dotnet` CLI 命令，請先開啟命令列並切換至包含您專案檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="a0b9c-149">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="a0b9c-150">使用 `restore` 還原套件：</span><span class="sxs-lookup"><span data-stu-id="a0b9c-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```