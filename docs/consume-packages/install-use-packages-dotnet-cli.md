---
title: 使用 dotnet CLI 安裝和管理 NuGet 套件
description: 使用 dotnet CLI 以便處理 NuGet 套件的指示。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842352"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="0557e-103">使用 dotnet CLI 安裝和管理套件</span><span class="sxs-lookup"><span data-stu-id="0557e-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="0557e-104">CLI 工具可讓您輕鬆地在專案和解決方案中安裝、解除安裝及更新 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="0557e-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="0557e-105">可在 Windows、Mac OS X 及 Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="0557e-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="0557e-106">Dotnet CLI 適用於 .NET Core 和 .NET Standard 專案 (SDK 樣式專案類型)，以及其他任何 SDK 樣式專案 (例如以 .NET Framework 為目標的 SDK 樣式專案)。</span><span class="sxs-lookup"><span data-stu-id="0557e-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="0557e-107">如需詳細資訊，請參閱 [SDK 屬性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="0557e-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="0557e-108">本文顯示一些最常用 dotnet CLI 命令的基本使用方式。</span><span class="sxs-lookup"><span data-stu-id="0557e-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="0557e-109">針對這些命令的大部分，CLI 工具會在目前的目錄中尋找專案檔，除非在命令中指定專案檔 (專案檔為選用參數)。</span><span class="sxs-lookup"><span data-stu-id="0557e-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="0557e-110">如需您可以使用的命令和引數完整清單，請參閱 [.NET Core 命令列介面 (CLI) 工具](../tools/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="0557e-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../tools/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0557e-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="0557e-111">Prerequisites</span></span>

- <span data-ttu-id="0557e-112">[.NET Core SDK](https://www.microsoft.com/net/download/)，它會提供 `dotnet` 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="0557e-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="0557e-113">從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。</span><span class="sxs-lookup"><span data-stu-id="0557e-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="0557e-114">安裝套件</span><span class="sxs-lookup"><span data-stu-id="0557e-114">Install a package</span></span>

<span data-ttu-id="0557e-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 會將套件參考新增到專案檔中，然後執行 `dotnet restore` 安裝套件。</span><span class="sxs-lookup"><span data-stu-id="0557e-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="0557e-116">開啟命令列並切換至包含您專案檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="0557e-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="0557e-117">使用下列命令來安裝 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="0557e-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="0557e-118">例如，若要安裝 `Newtonsoft.Json` 套件，請使用下列命令</span><span class="sxs-lookup"><span data-stu-id="0557e-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="0557e-119">在命令完成之後，請查看專案檔以確定已安裝套件。</span><span class="sxs-lookup"><span data-stu-id="0557e-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="0557e-120">您可以開啟 `.csproj` 檔案來查看已新增的參考：</span><span class="sxs-lookup"><span data-stu-id="0557e-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="0557e-121">安裝特定版本的套件</span><span class="sxs-lookup"><span data-stu-id="0557e-121">Install a specific version of a package</span></span>

<span data-ttu-id="0557e-122">如果未指定版本，則 NuGet 會安裝最新版的套件。</span><span class="sxs-lookup"><span data-stu-id="0557e-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="0557e-123">您也可以使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 命令來安裝特定版本的 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="0557e-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="0557e-124">例如，若要新增 12.0.1 版的 `Newtonsoft.Json` 套件，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="0557e-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="0557e-125">列出套件參考</span><span class="sxs-lookup"><span data-stu-id="0557e-125">List package references</span></span>

<span data-ttu-id="0557e-126">您可以使用 [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 命令列出專案的套件參考。</span><span class="sxs-lookup"><span data-stu-id="0557e-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="0557e-127">移除套件</span><span class="sxs-lookup"><span data-stu-id="0557e-127">Remove a package</span></span>

<span data-ttu-id="0557e-128">使用 [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 命令來移除專案檔中的套件參考。</span><span class="sxs-lookup"><span data-stu-id="0557e-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="0557e-129">例如，若要移除 `Newtonsoft.Json` 套件，請使用下列命令</span><span class="sxs-lookup"><span data-stu-id="0557e-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="0557e-130">更新套件</span><span class="sxs-lookup"><span data-stu-id="0557e-130">Update a package</span></span>

<span data-ttu-id="0557e-131">除非您指定套件版本 (`-v` 參數)，否則當您使用 `dotnet add package` 命令時 NuGet 會安裝最新版的套件。</span><span class="sxs-lookup"><span data-stu-id="0557e-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="0557e-132">還原套件</span><span class="sxs-lookup"><span data-stu-id="0557e-132">Restore packages</span></span>

<span data-ttu-id="0557e-133">使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令來還原專案檔 (請參閱 [PackageReference](../consume-packages/package-references-in-project-files.md)) 中所列的套件。</span><span class="sxs-lookup"><span data-stu-id="0557e-133">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="0557e-134">使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 自動完成還原。</span><span class="sxs-lookup"><span data-stu-id="0557e-134">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="0557e-135">截至 NuGet 4.0，這會執行與 `nuget restore` 相同的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0557e-135">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="0557e-136">如同其他 `dotnet` CLI 命令，請先開啟命令列並切換至包含您專案檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="0557e-136">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="0557e-137">使用 `dotnet restore` 還原套件：</span><span class="sxs-lookup"><span data-stu-id="0557e-137">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```
