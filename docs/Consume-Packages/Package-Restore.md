---
title: "NuGet 套件還原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "描述 NuGet 如何還原專案所相依的套件，包含如何停用還原和限制版本。"
keywords: "NuGet 套件還原, NuGet 套件安裝, 安裝套件, 還原套件、相依性版本, 停用自動還原, 限制套件版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a><span data-ttu-id="7d6f2-104">套件還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-104">Package Restore</span></span>

<span data-ttu-id="7d6f2-105">若要升級更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原**會先安裝所有參考的套件，再建置專案。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="7d6f2-106">這項廣泛使用的功能可確保專案中具有所有相依性，而這些套件不需要儲存在原始檔控制中 (請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)，以了解如何設定存放庫排除套件二進位檔)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="7d6f2-107">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-107">In this topic:</span></span>
- [<span data-ttu-id="7d6f2-108">套件還原快速指南</span><span class="sxs-lookup"><span data-stu-id="7d6f2-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="7d6f2-109">套件還原概觀</span><span class="sxs-lookup"><span data-stu-id="7d6f2-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="7d6f2-110">啟用和停用套件還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="7d6f2-111">使用還原限制套件版本</span><span class="sxs-lookup"><span data-stu-id="7d6f2-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="7d6f2-112">[命令列還原](#command-line-restore)，適用於所有版本的 NuGet</span><span class="sxs-lookup"><span data-stu-id="7d6f2-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="7d6f2-113">[Visual Studio 中的自動還原](#automatic-restore-in-visual-studio)，適用於 NuGet 2.7 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="7d6f2-114">[Visual Studio 中的 MSBuild 整合還原](#msbuild-integrated-restore)，適用於 NuGet 2.6 和更早版本。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="7d6f2-115">使用 Team Foundation Build 的套件還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="7d6f2-116">還原行為會因版本而異；若要檢查 NuGet 版本，只需要在命令列上執行 `nuget.exe`，並查看輸出的第一行。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="7d6f2-117">如需組建伺服器上套件還原的詳細資料，請參閱[使用 TFBuild 的套件還原](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="7d6f2-118">設定進行套件還原的專案也會與 Mono 上的 xbuild 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="7d6f2-119">套件還原快速指南</span><span class="sxs-lookup"><span data-stu-id="7d6f2-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="7d6f2-120">如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請遵循[啟用和停用套件還原](#enabling-and-disabling-package-restore)下的指示來開啟自動還原。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="7d6f2-121">套件還原概觀</span><span class="sxs-lookup"><span data-stu-id="7d6f2-121">Package restore overview</span></span>

<span data-ttu-id="7d6f2-122">首先，會使用下列其中一種套件管理格式來維護套件參考 (視專案類型和 NuGet 版本而定) </span><span class="sxs-lookup"><span data-stu-id="7d6f2-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="7d6f2-123">(請注意，NuGet 4 和 MSBuild 15.1 是與 Visual Studio 2017 一起安裝)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="7d6f2-124">方法</span><span class="sxs-lookup"><span data-stu-id="7d6f2-124">Method</span></span> | <span data-ttu-id="7d6f2-125">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="7d6f2-125">NuGet Version</span></span> | <span data-ttu-id="7d6f2-126">說明</span><span class="sxs-lookup"><span data-stu-id="7d6f2-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="7d6f2-127">2.x+</span><span class="sxs-lookup"><span data-stu-id="7d6f2-127">2.x+</span></span> | <span data-ttu-id="7d6f2-128">列出一組完整深層相依性。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="7d6f2-129">新增至 `packages.config` 的套件也必須新增至專案檔，而且 [目標] 和 [屬性] 也必須新增至專案檔。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="7d6f2-130">這是 NuGet 所有版本的基準方法，但與其他選項相較之下效能較慢。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="7d6f2-131">(請參閱 [packages.config 結構描述](../schema/packages-config.md))。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="7d6f2-132">3.x+</span><span class="sxs-lookup"><span data-stu-id="7d6f2-132">3.x+</span></span> | <span data-ttu-id="7d6f2-133">預設只會與 UWP 專案搭配使用，但可以從 `packages.config` 轉換專案。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="7d6f2-134">`project.json` 只會列出最上層相依性。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="7d6f2-135">在建置期間會將參考、目標和屬性動態新增至專案，並與 `packages.config` 相較之下可產生更好的效能 </span><span class="sxs-lookup"><span data-stu-id="7d6f2-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="7d6f2-136">(請參閱 [project.json 結構描述](../schema/project-json.md))。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="7d6f2-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="7d6f2-137">PackageReference</span></span> | <span data-ttu-id="7d6f2-138">4.x+</span><span class="sxs-lookup"><span data-stu-id="7d6f2-138">4.x+</span></span> | <span data-ttu-id="7d6f2-139">直接在 `<PackageReference>` 節點以及 `<Reference>` 和 `<ProjectReference>` 的專案檔中列出相依性。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="7d6f2-140">運作方式與 `project.json` 類似；請參閱[專案檔中的套件參考](../Consume-Packages/Package-References-in-Project-Files.md)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="7d6f2-141">其次，您透過各種方式，使用參考清單來開始還原：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="7d6f2-142">從命令列或[套件管理員主控台](../tools/Package-Manager-Console.md)：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="7d6f2-143">命令</span><span class="sxs-lookup"><span data-stu-id="7d6f2-143">Command</span></span> | <span data-ttu-id="7d6f2-144">適用的案例</span><span class="sxs-lookup"><span data-stu-id="7d6f2-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="7d6f2-145">所有版本的 NuGet 和所有參考類型。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="7d6f2-146">請參閱下方的[命令列還原](#command-line-restore)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="7d6f2-147">與 .NET Core 專案的 `nuget restore` 相同。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="7d6f2-148">請參閱 [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-148">See [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="7d6f2-149">僅限具有[專案檔中的套件參考](../Consume-Packages/Package-References-in-Project-Files.md)的 Nuget 4.x+ 和 MSBuild 15.1+。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="7d6f2-150">`nuget restore` 和 `dotnet restore` 都會將這個命令用於適用的專案。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="7d6f2-151">請參閱 [NuGet 封裝和還原為 MSBuild 目標 - 還原目標](../schema/msbuild-targets.md#restore-target)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="7d6f2-152">Visual Studio 本身也會在不同的時間還原套件：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="7d6f2-153">類型</span><span class="sxs-lookup"><span data-stu-id="7d6f2-153">Type</span></span> | <span data-ttu-id="7d6f2-154">進行還原的時機</span><span class="sxs-lookup"><span data-stu-id="7d6f2-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="7d6f2-155">範本還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-155">Template restore</span></span> | <span data-ttu-id="7d6f2-156">在建立新專案期間，某些範本與外部套件相依。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="7d6f2-157">組建還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-157">Build restore</span></span> | <span data-ttu-id="7d6f2-158">為組建的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-158">As the first step of a build.</span></span> |
| <span data-ttu-id="7d6f2-159">方案還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-159">Solution restore</span></span> | <span data-ttu-id="7d6f2-160">使用者以滑鼠右鍵按一下方案並選取 [還原 NuGet 套件] 時。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="7d6f2-161">在專案變更時還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-161">Restore on project change</span></span> | <span data-ttu-id="7d6f2-162">*(僅限 NuGet 4.x)* 使用 .NET Core SDK 專案時，包含專案狀態變更時。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="7d6f2-163">啟用和停用套件還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="7d6f2-164">套件還原主要是透過 Visual Studio 中的 [工具] > [選項] > [NuGet 套件管理員] 所啟用：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![透過 NuGet 套件管理員選項控制套件還原行為](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="7d6f2-166">**允許 NuGet 下載遺漏的套件**：變更 `%AppData%\NuGet\NuGet.Config` 檔案中的 `packageRestore/enabled` 設定，以控制所有形式的套件還原，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="7d6f2-167">在啟動 Visual Studio 或啟動組建之前，可以設定稱為 **EnableNuGetPackageRestore** 且值為 TRUE 或 FALSE 的環境變數，以全域覆寫 `packageRestore/enabled` 設定。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="7d6f2-168">**在 Visual Studio 建置期間自動檢查遺漏的套件**：變更 `%AppData%\NuGet\NuGet.Config` 檔案中的 `packageRestore/automatic` 設定，以控制 NuGet 2.7 和更新版本的自動還原，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="7d6f2-169">如需參考，請參閱 [NuGet 組態檔 - packageRestore 區段](../Schema/nuget-config-file.md#packagerestore-section)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="7d6f2-170">在某些情況下，根據預設，開發人員或公司可能想要啟用或停用電腦上所有使用者的套件還原。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="7d6f2-171">做法是將上述相同設定新增至 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` 的全域 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="7d6f2-172">個別使用者接著可以視需要選擇性地啟用專案層級的還原。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="7d6f2-173">如需 NuGet 如何設定多個組態檔優先順序的確切詳細資料，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="7d6f2-174">使用還原限制套件版本</span><span class="sxs-lookup"><span data-stu-id="7d6f2-174">Constraining package versions with restore</span></span>

<span data-ttu-id="7d6f2-175">NuGet 透過任何方法還原套件時，會使用 `packages.config`、`project.json` 或專案檔中所指定的任何條件約束：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="7d6f2-176">`packages.config`：指定相依性之 `allowedVersion` 屬性中的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="7d6f2-177">請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="7d6f2-178">例如: </span><span class="sxs-lookup"><span data-stu-id="7d6f2-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="7d6f2-179">`project.json`：直接使用相依性的版本號碼來指定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="7d6f2-180">例如: </span><span class="sxs-lookup"><span data-stu-id="7d6f2-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="7d6f2-181">專案檔中的套件參考：直接使用相依性的版本號碼來指定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="7d6f2-182">例如: </span><span class="sxs-lookup"><span data-stu-id="7d6f2-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="7d6f2-183">在所有情況下，都請使用[套件版本控制](../reference/package-versioning.md)中所述的標記法。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="7d6f2-184">命令列還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-184">Command-line restore</span></span>

<span data-ttu-id="7d6f2-185">針對 NuGet 2.7 和更新版本，使用 [Restore](../tools/cli-ref-restore.md) 命令，以還原方案中的所有套件 (無論是使用 `packages.config`、`project.json` 或是專案檔中的套件參考)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="7d6f2-186">針對 `c:\proj\app` 這類指定專案資料夾，其下的一般變異會還原套件：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="7d6f2-187">針對 NuGet 4.0+ 和 MSBuild 15.1+，您也可以使用 `MSBuild /t:restore`，如 [NuGet 封裝和還原為 MSBuild 目標](../schema/msbuild-targets.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="7d6f2-188">Visual Studio 中的建置時間還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="7d6f2-189">Visual Studio 預設會在建置開始時自動還原遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="7d6f2-190">此行為的變更方式是清除 [工具] > [選項] > [NuGet 套件管理員] > [一般] > [在 Visual Studio 建置期間自動檢查遺漏的套件]。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="7d6f2-191">啟用時，自動還原會如下運作：</span><span class="sxs-lookup"><span data-stu-id="7d6f2-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="7d6f2-192">開始建置時，Visual Studio 會指示 NuGet 還原套件。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="7d6f2-193">NuGet 會遞迴尋找方案中的所有 `packages.config` 檔案、尋找 `project.json` 或查看專案檔。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="7d6f2-194">針對參考檔案中所列的每個套件，NuGet 會檢查它是否已存在於方案中 (`packages` 資料夾、`project.lock.json` 或 `project.assets.json`，根據專案使用 `packages.config`、`project.json` 還是專案檔中的套件參考而定)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="7d6f2-195">如果找不到套件，NuGet 會嘗試先從其快取擷取套件 (請參閱[管理 NuGet 快取](../consume-packages/managing-the-nuget-cache.md))。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="7d6f2-196">如果套件不在快取中，則 NuGet 會嘗試從 [工具] > [選項] > [NuGet 套件管理員] > [套件來源] 中所列的已啟用來源下載套件，而下載順序就是來源出現的順序。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="7d6f2-197">在此情況下，除非已檢查所有來源，否則 NuGet 不會指出尋找套件失敗，而它在此時只會報告清單中最後一個來源的失敗。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="7d6f2-198">這類錯誤也隱含表示套件未出現在任何其他來源上，即使未個別顯示這些來源的錯誤也是一樣。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="7d6f2-199">如果成功下載，則 NuGet 會快取套件，並將它安裝至方案 (同樣地安裝至 `packages` 資料夾、`project.lock.json` 或 `project.assets.json`)；否則 NuGet 會失敗，而且建置會失敗。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="7d6f2-200">在此程序期間，您會看到內含取消套件還原選項的進度對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="7d6f2-201">使用 Team Foundation Build 的套件還原</span><span class="sxs-lookup"><span data-stu-id="7d6f2-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="7d6f2-202">套件還原常用於在組建伺服器上建置專案時，與使用 Team Foundation Server (TFS) 和 Visual Studio Team Services 相同 (以及這裡未涵蓋的其他組建系統)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="7d6f2-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="7d6f2-203">Visual Studio Team Services</span></span>

<span data-ttu-id="7d6f2-204">在 Team Services 上建立組建定義時，只需要在定義中於任何建置工作之前包含「還原 NuGet 套件」工作。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="7d6f2-205">在許多組建範本中，預設會包含此工作。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-205">This task is included by default in a number of build templates.</span></span>

![Visual Studio Team Service 組建定義中的 NuGet 套件還原工作](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="7d6f2-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="7d6f2-207">Team Foundation Server</span></span>

<span data-ttu-id="7d6f2-208">使用 TFS 2013 和更新版本，在建置期間預設會自動還原套件，前提是您將 Team Build 範本用於 Team Foundation Server 2013 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="7d6f2-209">如果您使用舊版的組建範本 (例如，在已從舊版 TFS 移轉的專案中)，則也需要將這些組建範本移轉至 TFS 2013。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="7d6f2-210">這基本上表示使用原始檔控制 (TFVC 或 Git) 的適當範本來重建組建範本的自訂組件。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="7d6f2-211">針對較早的 TFS 版本，您可以只包含可叫用[命令列還原](#command-line-restore)的建置步驟，如上所述。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="7d6f2-212">如需詳細資料，請參閱[使用 Team Foundation Build 的套件還原逐步解說](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="7d6f2-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
