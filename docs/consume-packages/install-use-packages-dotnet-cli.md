---
title: 使用 dotnet CLI 安裝和管理 NuGet 套件
description: 使用 dotnet CLI 以便處理 NuGet 套件的指示。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 38455e61bd91f115df9f27df090ba47a029f6877
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622937"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="91312-103">使用 dotnet CLI 安裝和管理套件</span><span class="sxs-lookup"><span data-stu-id="91312-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="91312-104">CLI 工具可讓您輕鬆地在專案和解決方案中安裝、解除安裝及更新 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="91312-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="91312-105">可在 Windows、Mac OS X 及 Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="91312-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="91312-106">Dotnet CLI 適用於 .NET Core 和 .NET Standard 專案 (SDK 樣式專案類型)，以及其他任何 SDK 樣式專案 (例如以 .NET Framework 為目標的 SDK 樣式專案)。</span><span class="sxs-lookup"><span data-stu-id="91312-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="91312-107">如需詳細資訊，請參閱 [SDK 屬性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="91312-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="91312-108">本文顯示一些最常用 dotnet CLI 命令的基本使用方式。</span><span class="sxs-lookup"><span data-stu-id="91312-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="91312-109">針對這些命令的大部分，CLI 工具會在目前的目錄中尋找專案檔，除非在命令中指定專案檔 (專案檔為選用參數)。</span><span class="sxs-lookup"><span data-stu-id="91312-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="91312-110">如需您可以使用的命令和引數完整清單，請參閱 [.NET Core 命令列介面 (CLI) 工具](../reference/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="91312-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91312-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91312-111">Prerequisites</span></span>

- <span data-ttu-id="91312-112">[.NET Core SDK](https://www.microsoft.com/net/download/)，它會提供 `dotnet` 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="91312-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="91312-113">從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。</span><span class="sxs-lookup"><span data-stu-id="91312-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="91312-114">安裝套件</span><span class="sxs-lookup"><span data-stu-id="91312-114">Install a package</span></span>

<span data-ttu-id="91312-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 會將套件參考新增到專案檔中，然後執行 `dotnet restore` 安裝套件。</span><span class="sxs-lookup"><span data-stu-id="91312-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="91312-116">開啟命令列並切換至包含您專案檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="91312-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="91312-117">使用下列命令來安裝 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="91312-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="91312-118">例如，若要安裝 `Newtonsoft.Json` 套件，請使用下列命令</span><span class="sxs-lookup"><span data-stu-id="91312-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="91312-119">在命令完成之後，請查看專案檔以確定已安裝套件。</span><span class="sxs-lookup"><span data-stu-id="91312-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="91312-120">您可以開啟 `.csproj` 檔案來查看已新增的參考：</span><span class="sxs-lookup"><span data-stu-id="91312-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="91312-121">安裝特定版本的套件</span><span class="sxs-lookup"><span data-stu-id="91312-121">Install a specific version of a package</span></span>

<span data-ttu-id="91312-122">如果未指定版本，則 NuGet 會安裝最新版的套件。</span><span class="sxs-lookup"><span data-stu-id="91312-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="91312-123">您也可以使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 命令來安裝特定版本的 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="91312-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="91312-124">例如，若要新增 12.0.1 版的 `Newtonsoft.Json` 套件，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="91312-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="91312-125">列出套件參考</span><span class="sxs-lookup"><span data-stu-id="91312-125">List package references</span></span>

<span data-ttu-id="91312-126">您可以使用 [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 命令列出專案的套件參考。</span><span class="sxs-lookup"><span data-stu-id="91312-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="91312-127">移除套件</span><span class="sxs-lookup"><span data-stu-id="91312-127">Remove a package</span></span>

<span data-ttu-id="91312-128">使用 [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 命令來移除專案檔中的套件參考。</span><span class="sxs-lookup"><span data-stu-id="91312-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="91312-129">例如，若要移除 `Newtonsoft.Json` 套件，請使用下列命令</span><span class="sxs-lookup"><span data-stu-id="91312-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="91312-130">更新套件</span><span class="sxs-lookup"><span data-stu-id="91312-130">Update a package</span></span>

<span data-ttu-id="91312-131">除非您指定套件版本 (`-v` 參數)，否則當您使用 `dotnet add package` 命令時 NuGet 會安裝最新版的套件。</span><span class="sxs-lookup"><span data-stu-id="91312-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="91312-132">還原套件</span><span class="sxs-lookup"><span data-stu-id="91312-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
