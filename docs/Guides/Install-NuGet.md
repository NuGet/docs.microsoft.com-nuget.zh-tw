---
title: "安裝 NuGet 用戶端工具 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "安裝用戶端工具、命令列介面 (CLI) 和 Package Manager for Visual Studio 的指南。"
keywords: "nuget.exe CLI, NuGet 用戶端工具, NuGet 套件管理員, NuGet 套件管理員主控台, NuGet for Visual Studio, NuGet 搶鮮版 (Beta)通道"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="9d5b7-104">安裝 NuGet 用戶端工具</span><span class="sxs-lookup"><span data-stu-id="9d5b7-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="9d5b7-105">**想要安裝套件？請參閱[快速入門 - 使用套件](../Quickstart/Use-a-Package.md)。**</span><span class="sxs-lookup"><span data-stu-id="9d5b7-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="9d5b7-106">有兩個主要的工具可幫助您建置、發行和取用 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="9d5b7-107">[**NuGet CLI** ](#nuget-cli) 是適用於 Windows 的命令列公用程式，它提供所有 NuGet 功能，也可以在 Mac OSX 與 Linux 上使用 Mono 執行，或透過 .NET Core CLI 執行 (`dotnet`)。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="9d5b7-108">[**Visual Studio 中的 NuGet 套件管理員**](#nuget-package-manager-in-visual-studio) (僅限 Windows) 是一種管理套件的 GUI 工具，並包含 PowerShell 主控台；透過它，您可以直接在 VisualStudio 內使用特定的 NuGet 命令。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="9d5b7-109">套件管理員 UI 和主控台都包含在 Visual Studio (在 Windows 上) 2012 及更新版本中，且可以針對先前的版本手動安裝。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="9d5b7-110">使用 Visual Studio for Mac，NuGet 功能已直接內建。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="9d5b7-111">如需逐步解說，請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-111">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="9d5b7-112">目前的 Visual Studio 程式碼沒有任何內建的 NuGet 支援。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="9d5b7-113">請使用 NuGet CLI 或 [dotnet CLI](../Tools/dotnet-Commands.md)。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="9d5b7-114">NuGet CLI 和套件管理員都支援下列作業：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="9d5b7-115">搜尋套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-115">Search packages</span></span>
- <span data-ttu-id="9d5b7-116">安裝套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-116">Install packages</span></span>
- <span data-ttu-id="9d5b7-117">更新套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-117">Update packages</span></span>
- <span data-ttu-id="9d5b7-118">解除安裝套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-118">Uninstall packages</span></span>
- <span data-ttu-id="9d5b7-119">還原套件 (在套件管理員中僅限 UI)</span><span class="sxs-lookup"><span data-stu-id="9d5b7-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="9d5b7-120">管理 NuGet 來源</span><span class="sxs-lookup"><span data-stu-id="9d5b7-120">Manage NuGet sources</span></span>

<span data-ttu-id="9d5b7-121">下列功能只在 NuGet CLI 中受支援：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="9d5b7-122">管理套件 (nuget.org 或私人摘要)</span><span class="sxs-lookup"><span data-stu-id="9d5b7-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="9d5b7-123">建立套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-123">Create packages</span></span> 
- <span data-ttu-id="9d5b7-124">發行套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-124">Publish packages</span></span>
- <span data-ttu-id="9d5b7-125">管理 NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="9d5b7-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="9d5b7-126">管理 NuGet 快取</span><span class="sxs-lookup"><span data-stu-id="9d5b7-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="9d5b7-127">複製套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="9d5b7-128">另一個很好的工具是 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)，這是一個開放原始碼的獨立工具，以視覺化方式瀏覽、建立和編輯 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="9d5b7-129">例如，它很適用對套件結構進行實驗性的變更，而不必每次重建套件。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="9d5b7-130">跨平台的 [.NET Core CLI](/dotnet/articles/core/tools/index#installation) 工具鏈，用來開發 .NET Core 應用程式，能支援數個 NuGet 命令，例如 delete、locals、push、pack 和 restore。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-130">The cross-platform [.NET Core CLI](/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="9d5b7-131">NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="9d5b7-131">NuGet CLI</span></span>

<span data-ttu-id="9d5b7-132">NuGet 命令列介面提供對所有 NuGet 功能的存取權，並可以在 Windows、Mac OSX 與 Linux 上執行，如下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="9d5b7-133">Windows</span><span class="sxs-lookup"><span data-stu-id="9d5b7-133">Windows</span></span>

<span data-ttu-id="9d5b7-134">**直接下載：**</span><span class="sxs-lookup"><span data-stu-id="9d5b7-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="9d5b7-135">在 NuGet 1.4+，您可以使用 `nuget update -self` 將現有的 nuget.exe 更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="9d5b7-136">**其他方法：**</span><span class="sxs-lookup"><span data-stu-id="9d5b7-136">**Other methods:**</span></span>

- <span data-ttu-id="9d5b7-137">**Chocolatey**：使用 [Chocalatey](http://chocolatey.org) 用戶端安裝 [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey 套件。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="9d5b7-138">**Visual Studio**：從 Visual Studio 的套件管理員主控台安裝 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 套件。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="9d5b7-139">**對於 NuGet 2.x 使用者**：因為 NuGet 3.2 中導入的重大變更，[https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) 指向最新且穩定的 NuGet 2.x 版本，以防止連續整合系統可能的中斷。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="9d5b7-140">Mac OSX 與 Linux</span><span class="sxs-lookup"><span data-stu-id="9d5b7-140">Mac OSX and Linux</span></span>

<span data-ttu-id="9d5b7-141">在 Mac OSX 與 Linux 上，有兩種方式可以執行 NuGet CLI：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="9d5b7-142">安裝 [.NET Core SDK](https://www.microsoft.com/net/download/core)，其中包括核心 NuGet 功能。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="9d5b7-143">下載項目也會列在 [github.com/dotnet/cli](https://github.com/dotnet/cli) 上。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="9d5b7-144">如果您需要更完整的功能，請使用下方的第二個選項，使用 `nuget.exe` 搭配 Mono。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="9d5b7-145">安裝 [Mono](http://www.mono-project.com/docs/getting-started/install/)，然後從 [nuget.org/downloads](https://nuget.org/downloads)，使用適用於 Windows 的 `nuget.exe` 命令列可執行檔 (3.2 版及更新版本)。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="9d5b7-146">在 Mono 上執行 NuGet 受限於下列限制：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="9d5b7-147">已測試可運作的命令：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-147">Commands tested to work:</span></span>
        - <span data-ttu-id="9d5b7-148">config</span><span class="sxs-lookup"><span data-stu-id="9d5b7-148">config</span></span>
        - <span data-ttu-id="9d5b7-149">刪除</span><span class="sxs-lookup"><span data-stu-id="9d5b7-149">delete</span></span>
        - <span data-ttu-id="9d5b7-150">help</span><span class="sxs-lookup"><span data-stu-id="9d5b7-150">help</span></span>
        - <span data-ttu-id="9d5b7-151">install</span><span class="sxs-lookup"><span data-stu-id="9d5b7-151">install</span></span>
        - <span data-ttu-id="9d5b7-152">清單</span><span class="sxs-lookup"><span data-stu-id="9d5b7-152">list</span></span>
        - <span data-ttu-id="9d5b7-153">push</span><span class="sxs-lookup"><span data-stu-id="9d5b7-153">push</span></span>
        - <span data-ttu-id="9d5b7-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="9d5b7-154">setApiKey</span></span>
        - <span data-ttu-id="9d5b7-155">sources</span><span class="sxs-lookup"><span data-stu-id="9d5b7-155">sources</span></span>
        - <span data-ttu-id="9d5b7-156">spec</span><span class="sxs-lookup"><span data-stu-id="9d5b7-156">spec</span></span>

    - <span data-ttu-id="9d5b7-157">部分可運作的命令：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-157">Partially-working commands:</span></span>
        - <span data-ttu-id="9d5b7-158">pack：搭配 `.nuspec` 檔案可運作，但無法搭配專案檔。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="9d5b7-159">restore：搭配 `packages.config` 和 `project.json` 檔案可運作，但無法搭配解決方案 (`.sln`) 檔案運作。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="9d5b7-160">無法運作的命令：</span><span class="sxs-lookup"><span data-stu-id="9d5b7-160">Commands that do not work:</span></span>
        - <span data-ttu-id="9d5b7-161">更新</span><span class="sxs-lookup"><span data-stu-id="9d5b7-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="9d5b7-162">相關主題</span><span class="sxs-lookup"><span data-stu-id="9d5b7-162">Related topics</span></span>

- [<span data-ttu-id="9d5b7-163">NuGet CLI 參考</span><span class="sxs-lookup"><span data-stu-id="9d5b7-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="9d5b7-164">建立套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="9d5b7-165">發行套件</span><span class="sxs-lookup"><span data-stu-id="9d5b7-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="9d5b7-166">Visual Studio 中的 NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9d5b7-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="9d5b7-167">NuGet 套件管理員包含於 Windows 上的 Visual Studio 2012 及更新版本的所有版本。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="9d5b7-168">它包含套件管理員 UI ([參考](../tools/package-manager-ui.md))，以及您可以用來存取特定套件所附之工具的套件管理員主控台 ([參考](../tools/package-manager-console.md))。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="9d5b7-169">Visual Studio 2017 安裝程式會在採用 .NET 的任何工作負載包含 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="9d5b7-170">若要個別安裝，或確認已安裝套管理員，請執行 Visual Studio 2017 安裝程式，並核取 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 下方選項。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="9d5b7-171">主控台需要 [PowerShell 2.0](http://support.microsoft.com/kb/968929)，這在 Windows 7 或更新版本以及 Windows Server 2008 R2 或更高版本上已經安裝。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="9d5b7-172">套件管理員主控台命令也只在 Windows 上的 Visual Studio 內運作。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="9d5b7-173">在該環境之外使用 NuGet CLI，包括使用 Visual Studio for Mac 和 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="9d5b7-174">Visual Studio 2010 和更早版本的套件管理員安裝</span><span class="sxs-lookup"><span data-stu-id="9d5b7-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="9d5b7-175">*Visual Studio 2012 及更新版本不需要這些步驟，它們已經包含套件管理員。*</span><span class="sxs-lookup"><span data-stu-id="9d5b7-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="9d5b7-176">在 Visual Studio 2010 和舊版中，按一下 [工具] > [延伸模組和更新]。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="9d5b7-177">巡覽至 [線上]，然後搜尋 [Visual Studio 的 NuGet 套件管理員]，然後按一下 [下載]。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="9d5b7-178">在 [安裝程式] 對話方塊中，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="9d5b7-179">安裝完成時，請重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="9d5b7-180">如果您無法在 Visual Studio 中使用 [延伸模組和更新] 對話方塊 (例如，被 Proxy 封鎖)，可以直接在 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下載 Visual Studio 2013 和 2015 的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="9d5b7-181">更新套件管理員</span><span class="sxs-lookup"><span data-stu-id="9d5b7-181">Updating the Package Manager</span></span>

<span data-ttu-id="9d5b7-182">對於 Visual Studio 2015 Update 2 和更新版本，套件管理員會自動更新至最新穩定版本。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="9d5b7-183">對於 Visual Studio 2015 Update 1 和更早版本，請選取 [工具] > [延伸模組和更新] 命令，然後按一下 [更新] 索引標籤，以查看是否有可用的套件管理員新版本。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="9d5b7-184">NuGet 預覽</span><span class="sxs-lookup"><span data-stu-id="9d5b7-184">NuGet previews</span></span>

<span data-ttu-id="9d5b7-185">如果您想要預覽即將推出的 NuGet 功能，請安裝 [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/)，它能與穩定版本的 Visual Studio 並存運作。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="9d5b7-186">請注意，先前的 Visual Studio 2015 NuGet 搶鮮版 (Beta)通道 (`https://dotnet.myget.org/F/nuget-beta/vsix/`) 已不再使用。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="9d5b7-187">若要報告任何 NuGet 版本的問題或是分享想法，請在 [NuGet GitHub 儲存機制](https://github.com/Nuget/Home)上開啟問題。</span><span class="sxs-lookup"><span data-stu-id="9d5b7-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="9d5b7-188">相關主題</span><span class="sxs-lookup"><span data-stu-id="9d5b7-188">Related topics</span></span>

- [<span data-ttu-id="9d5b7-189">套件管理員 UI 參考</span><span class="sxs-lookup"><span data-stu-id="9d5b7-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="9d5b7-190">套件管理員主控台參考</span><span class="sxs-lookup"><span data-stu-id="9d5b7-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="9d5b7-191">套件管理員主控台 PowerShell 參考</span><span class="sxs-lookup"><span data-stu-id="9d5b7-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)