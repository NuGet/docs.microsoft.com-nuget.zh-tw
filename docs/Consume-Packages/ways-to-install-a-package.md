---
title: "安裝 NuGet 套件的方式 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/30/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "描述將 NuGet 套件安裝到專案的程序，包括在磁碟上及適用的專案檔會發生什麼情況。"
keywords: "安裝 NuGet, NuGet 套件耗用量, 安裝 NuGet 套件, NuGet 套件參考"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e48bbe813168e773bc46b7fe25af29785ff75df
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a><span data-ttu-id="e98d6-104">安裝 NuGet 套件的不同方式</span><span class="sxs-lookup"><span data-stu-id="e98d6-104">Different ways to install a NuGet Package</span></span>

<span data-ttu-id="e98d6-105">NuGet 套件會使用下列任一種方法來下載並安裝 (如果您尚未安裝這些項目，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md))：</span><span class="sxs-lookup"><span data-stu-id="e98d6-105">NuGet packages are downloaded and installed using any of the following methods (see [Install NuGet client tools](../install-nuget-client-tools.md) if you don't have these installed already):</span></span>

| <span data-ttu-id="e98d6-106">方法</span><span class="sxs-lookup"><span data-stu-id="e98d6-106">Method</span></span> | <span data-ttu-id="e98d6-107">描述</span><span class="sxs-lookup"><span data-stu-id="e98d6-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e98d6-108">dotnet.exe CLI</span><span class="sxs-lookup"><span data-stu-id="e98d6-108">dotnet.exe CLI</span></span><br/>`dotnet install <package_name>` | <span data-ttu-id="e98d6-109">(所有平台) 下載 \<package_name\> 所識別的套件、在目前目錄的資料夾中展開其內容，並將參考新增到專案檔。</span><span class="sxs-lookup"><span data-stu-id="e98d6-109">(All platforms) Downloads the package identified by \<package_name\>, expands its contents into a folder in the current directory, and adds a reference to the project file.</span></span> <span data-ttu-id="e98d6-110">此外，也請下載並安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="e98d6-110">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="e98d6-111">安裝並使用套件 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="e98d6-111">Install and use a package (dotnet CLI)</span></span>](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[<span data-ttu-id="e98d6-112">dotnet 命令</span><span class="sxs-lookup"><span data-stu-id="e98d6-112">dotnet commands</span></span>](../tools/dotnet-commands.md)</li></ul> |
| <span data-ttu-id="e98d6-113">套件管理員 UI (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e98d6-113">Package Manager UI (Visual Studio)</span></span> | <span data-ttu-id="e98d6-114">(Windows 和 Mac) 提供 UI，透過該 UI 可瀏覽、選取套件及其相依性並安裝至專案。</span><span class="sxs-lookup"><span data-stu-id="e98d6-114">(Windows and Mac) Provides a UI through which you can browse, select, and install packages and their dependencies into a project.</span></span> <span data-ttu-id="e98d6-115">將對於已安裝套件的參考新增至專案檔。</span><span class="sxs-lookup"><span data-stu-id="e98d6-115">Adds references to installed packages to the project file.</span></span><ul><li>[<span data-ttu-id="e98d6-116">安裝並使用套件 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e98d6-116">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="e98d6-117">套件管理員 UI 參考 (Windows)</span><span class="sxs-lookup"><span data-stu-id="e98d6-117">Package Manager UI reference (Windows)</span></span>](../tools/package-manager-ui.md)</li><li>[<span data-ttu-id="e98d6-118">在專案中包含 NuGet 套件 (Mac)</span><span class="sxs-lookup"><span data-stu-id="e98d6-118">Including a NuGet package in your project (Mac)</span></span>](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| <span data-ttu-id="e98d6-119">套件管理員主控台 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e98d6-119">Package Manager Console (Visual Studio)</span></span><br/>`Install-Package <package_name>` | <span data-ttu-id="e98d6-120">(僅限 Windows) 下載 \<package_name\> 所識別的套件並安裝到方案中的指定專案，然後將參考新增到專案檔。</span><span class="sxs-lookup"><span data-stu-id="e98d6-120">(Windows only) Downloads and installs the package identified by \<package_name\> into a specified project in the solution, then adds a reference to the project file.</span></span> <span data-ttu-id="e98d6-121">此外，也請下載並安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="e98d6-121">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="e98d6-122">安裝並使用套件 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e98d6-122">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="e98d6-123">套件管理員主控台指南</span><span class="sxs-lookup"><span data-stu-id="e98d6-123">Package Manager Console guide</span></span>](../tools/package-manager-console.md)</li></ul> |
| <span data-ttu-id="e98d6-124">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="e98d6-124">nuget.exe CLI</span></span><br/>`nuget install <package_name>` | <span data-ttu-id="e98d6-125">(所有平台) 下載 \<package_name\> 所識別的套件，並在目前目錄的資料夾中展開其內容；也可以下載 `packages.config` 檔案中列出的所有套件。</span><span class="sxs-lookup"><span data-stu-id="e98d6-125">(All platforms) Downloads the package identified by \<package_name\> and expands its contents into a folder in the current directory; can also download all packages listed in a `packages.config` file.</span></span> <span data-ttu-id="e98d6-126">此外，也請下載並安裝相依性，但不要對專案檔進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="e98d6-126">Also downloads and installs dependencies, but makes no changes to project files.</span></span><ul><li>[<span data-ttu-id="e98d6-127">安裝命令</span><span class="sxs-lookup"><span data-stu-id="e98d6-127">install command</span></span>](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a><span data-ttu-id="e98d6-128">一般安裝程序</span><span class="sxs-lookup"><span data-stu-id="e98d6-128">General install process</span></span>

<span data-ttu-id="e98d6-129">NuGet 通常會執行下列動作，然後要求安裝套件：</span><span class="sxs-lookup"><span data-stu-id="e98d6-129">In general, NuGet does the following then asked to install a package:</span></span>

1. <span data-ttu-id="e98d6-130">取得套件：</span><span class="sxs-lookup"><span data-stu-id="e98d6-130">Acquire the package:</span></span>
    - <span data-ttu-id="e98d6-131">檢查要求的套件是否已經存在快取中 (請參閱[管理 NuGet 快取](managing-the-nuget-cache.md))。</span><span class="sxs-lookup"><span data-stu-id="e98d6-131">Check if the requested package already exists in a cache (see [Managing the NuGet cache](managing-the-nuget-cache.md)).</span></span>
    - <span data-ttu-id="e98d6-132">如果套件不在快取中，請嘗試從組態檔中所列的來源下載套件，從清單的第一個項目開始。</span><span class="sxs-lookup"><span data-stu-id="e98d6-132">If the package is not in the cache, attempt to download the package from the sources listed in the configuration files, starting with the first in the list.</span></span> <span data-ttu-id="e98d6-133">此行為可讓您在於 nuget.org 上尋找套件之前，先使用私人套件摘要 (請參閱[設定 NuGet 行為](configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="e98d6-133">This behavior allows you to use private package feeds before looking for a package on nuget.org (see [Configuring NuGet behavior](configuring-nuget-behavior.md)).</span></span>
    - <span data-ttu-id="e98d6-134">如果已成功從其中一個來源取得套件，NuGet 就會將它新增至快取。</span><span class="sxs-lookup"><span data-stu-id="e98d6-134">If the package is successfully acquired from one of the sources, NuGet adds it to the cache.</span></span> <span data-ttu-id="e98d6-135">否則，安裝會失敗。</span><span class="sxs-lookup"><span data-stu-id="e98d6-135">Otherwise, installation fails.</span></span>

1. <span data-ttu-id="e98d6-136">在專案中展開套件。</span><span class="sxs-lookup"><span data-stu-id="e98d6-136">Expand the package into the project.</span></span>
    - <span data-ttu-id="e98d6-137">展開的意思是將套件的內容解壓縮到適當的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="e98d6-137">Expanding means unzipping the package's contents into an appropriate subfolder.</span></span> <span data-ttu-id="e98d6-138">系統也會在子資料夾中放置 `.nupkg` 本身的複本。</span><span class="sxs-lookup"><span data-stu-id="e98d6-138">A copy of the `.nupkg` itself is also placed in the subfolder.</span></span>
    - <span data-ttu-id="e98d6-139">如果將套件安裝到 Visual Studio 或 .NET Core 專案，就只會展開與專案目標 Framework 相關的檔案。</span><span class="sxs-lookup"><span data-stu-id="e98d6-139">If the package is being installed into a Visual Studio or .NET Core project, only the files relevant to the project's target framework are expanded.</span></span> <span data-ttu-id="e98d6-140">使用 nuget.exe 命令列安裝時，會展開所有組件。</span><span class="sxs-lookup"><span data-stu-id="e98d6-140">When installed using the nuget.exe command line, all assemblies are expanded.</span></span>

1. <span data-ttu-id="e98d6-141">如果將套件安裝於 Visual Studio 或 dotnet CLI 內，就會將參考新增至適當的專案檔 (或 `packages.config`，適用於 Visual Studio 中的某些專案類型)。</span><span class="sxs-lookup"><span data-stu-id="e98d6-141">If the package is installed within Visual Studio or the dotnet CLI, a reference is added to the appropriate project file (or `packages.config` for some project types in Visual Studio).</span></span>

## <a name="related-topics"></a><span data-ttu-id="e98d6-142">相關主題</span><span class="sxs-lookup"><span data-stu-id="e98d6-142">Related topics</span></span>

- [<span data-ttu-id="e98d6-143">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="e98d6-143">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="e98d6-144">尋找及選擇套件</span><span class="sxs-lookup"><span data-stu-id="e98d6-144">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="e98d6-145">設定 NuGet 行為</span><span class="sxs-lookup"><span data-stu-id="e98d6-145">Configuring NuGet behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
- [<span data-ttu-id="e98d6-146">管理 NuGet 快取</span><span class="sxs-lookup"><span data-stu-id="e98d6-146">Managing the NuGet cache</span></span>](managing-the-nuget-cache.md)
