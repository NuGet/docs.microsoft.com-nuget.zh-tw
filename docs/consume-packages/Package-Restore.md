---
title: NuGet 套件還原
description: 概述 NuGet 如何還原專案相依的套件，包括如何停用還原和限制版本。
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9acb87a5f5731fb33c91a1ae9b106c6df492ddcd
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453529"
---
# <a name="package-restore"></a><span data-ttu-id="926f0-103">套件還原</span><span class="sxs-lookup"><span data-stu-id="926f0-103">Package Restore</span></span>

<span data-ttu-id="926f0-104">為了升級更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原**會依專案檔或 `packages.config`中所列，安裝所有專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="926f0-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all a project's dependencies as listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="926f0-105">Visual Studio 可在建置專案時自動還原套件。</span><span class="sxs-lookup"><span data-stu-id="926f0-105">Visual Studio can restore packages automatically when a project is built.</span></span> <span data-ttu-id="926f0-106">`dotnet build` 和 `dotnet run` 命令 (.NET Core 2.0 +) 也會執行自動還原。</span><span class="sxs-lookup"><span data-stu-id="926f0-106">The `dotnet build` and `dotnet run` commands (.NET Core 2.0+) also perform an automatic restore.</span></span> <span data-ttu-id="926f0-107">您也可以透過 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 上的 xbuild，隨時還原套件。</span><span class="sxs-lookup"><span data-stu-id="926f0-107">You can also restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="926f0-108">套件還原會確認所有專案的相依性是可用的，而不用將那些套件儲存在原始檔控制中。</span><span class="sxs-lookup"><span data-stu-id="926f0-108">Package restore makes sure that all a project's dependencies are available without storing those packages in source control.</span></span> <span data-ttu-id="926f0-109">有關如何設定存放庫以排除套件二進位檔，請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="926f0-109">See [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries.</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="926f0-110">套件還原概觀</span><span class="sxs-lookup"><span data-stu-id="926f0-110">Package restore overview</span></span>

<span data-ttu-id="926f0-111">還原套件會先視需要安裝專案的直接相依性，然後在整個相依性關係圖中安裝那些套件的任何相依性。</span><span class="sxs-lookup"><span data-stu-id="926f0-111">Restoring packages first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="926f0-112">如果尚未安裝套件，NuGet 會先嘗試從[快取](../consume-packages/managing-the-global-packages-and-cache-folders.md)中擷取它。</span><span class="sxs-lookup"><span data-stu-id="926f0-112">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="926f0-113">如果套件不在快取中，則 NuGet 會嘗試從所有已啟用的來源下載套件 (請參閱[設定 NuGet 行為](Configuring-NuGet-Behavior.md)；來源也會出現在 Visual Studio 中的 [工具] > [選項] > [NuGet 套件管理員] > [套件來源] 中)。</span><span class="sxs-lookup"><span data-stu-id="926f0-113">If the package is not in the cache, NuGet then attempts to download the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="926f0-114">在還原過程中，NuGet 會忽略套件來源的順序，而使用任一個最先回應要求的來源。</span><span class="sxs-lookup"><span data-stu-id="926f0-114">During restore, NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="926f0-115">在所有來源檢查完畢前，NuGet 不會指出還原套件的失敗。</span><span class="sxs-lookup"><span data-stu-id="926f0-115">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="926f0-116">到那時候，NuGet 只會針對清單中的最後一個來源回報失敗。</span><span class="sxs-lookup"><span data-stu-id="926f0-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="926f0-117">這項錯誤表示套件未出現在其他*任何*來源上，即使那些來源都未個別出現錯誤亦然。</span><span class="sxs-lookup"><span data-stu-id="926f0-117">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="926f0-118">套件還原會以下列方式觸發：</span><span class="sxs-lookup"><span data-stu-id="926f0-118">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="926f0-119">**dotnet CLI**：使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令來還原專案檔 (請參閱 [PackageReference](../consume-packages/package-references-in-project-files.md)) 中所列的套件。</span><span class="sxs-lookup"><span data-stu-id="926f0-119">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="926f0-120">使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 自動完成還原。</span><span class="sxs-lookup"><span data-stu-id="926f0-120">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="926f0-121">**套件管理員 UI (Windows 上的 Visual Studio)**：從範本建立專案時，以及建置專案時，會自動還原套件 (受限於[啟用和停用套件還原](#enabling-and-disabling-package-restore)中所述的選項)。</span><span class="sxs-lookup"><span data-stu-id="926f0-121">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="926f0-122">在 NuGet 4.0+ 中，還原也會在對 .NET Core SDK 型專案進行變更時自動進行。</span><span class="sxs-lookup"><span data-stu-id="926f0-122">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="926f0-123">若要手動還原，請以滑鼠右鍵按一下方案總管中的解決方案，然後選取 [還原 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="926f0-123">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="926f0-124">如有一或多個個別套件仍未正確安裝 (表示方案總管顯示錯誤圖示)，則使用套件管理員 UI 來解除安裝並重新安裝受影響的套件。</span><span class="sxs-lookup"><span data-stu-id="926f0-124">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="926f0-125">請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="926f0-125">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="926f0-126">如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請遵循[啟用和停用套件還原](#enabling-and-disabling-package-restore)下的指示來開啟自動還原。</span><span class="sxs-lookup"><span data-stu-id="926f0-126">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span> <span data-ttu-id="926f0-127">另請參閱[套件還原疑難排解](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="926f0-127">Also see [Package restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="926f0-128">**NuGet CLI**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令來還原專案檔或 `packages.config`中所列的套件。</span><span class="sxs-lookup"><span data-stu-id="926f0-128">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file or in `packages.config`.</span></span> <span data-ttu-id="926f0-129">您也可以指定方案檔。</span><span class="sxs-lookup"><span data-stu-id="926f0-129">You can also specify a solution file.</span></span>

- <span data-ttu-id="926f0-130">**MSBuild**：使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令來還原專案檔中所列的套件 (僅限 PackageReference)。</span><span class="sxs-lookup"><span data-stu-id="926f0-130">**MSBuild**: use the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (PackageReference only).</span></span> <span data-ttu-id="926f0-131">只適用於 NuGet 4.x+ 和 MSBuild 15.1+ (兩者均隨附於 Visual Studio 2017)。</span><span class="sxs-lookup"><span data-stu-id="926f0-131">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="926f0-132">`nuget restore` 和 `dotnet restore` 都會將這個命令用於適用的專案。</span><span class="sxs-lookup"><span data-stu-id="926f0-132">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="926f0-133">**Visual Studio Team Services**：在 Team Services 上建立組建定義時，在定義中於任何建置工作之前包含 [NuGet 還原](/vsts/build-release/tasks/package/nuget#restore-nuget-packages)或 [.NET Core 還原](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages)工作。</span><span class="sxs-lookup"><span data-stu-id="926f0-133">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="926f0-134">在許多組建範本中，預設會包含此工作。</span><span class="sxs-lookup"><span data-stu-id="926f0-134">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="926f0-135">**Team Foundation Server**：TFS 2013 和更新版本會在建置期間自動還原套件，前提是您使用的是適用於 TFS 2013 或更新版本的 Team Build 範本。</span><span class="sxs-lookup"><span data-stu-id="926f0-135">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="926f0-136">針對較早的 TFS 版本，您可以包含一個建置步驟來叫用上述其中一個命令列還原選項。</span><span class="sxs-lookup"><span data-stu-id="926f0-136">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="926f0-137">您可以選擇性地將建置範本移轉至 TFS 2013。</span><span class="sxs-lookup"><span data-stu-id="926f0-137">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="926f0-138">如需詳細資訊，請參閱[使用 Team Foundation Build 的套件還原逐步解說](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="926f0-138">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="926f0-139">啟用和停用套件還原</span><span class="sxs-lookup"><span data-stu-id="926f0-139">Enabling and disabling package restore</span></span>

<span data-ttu-id="926f0-140">套件還原主要是透過 Visual Studio 中的 [工具] > [選項] > [NuGet 套件管理員] 所啟用：</span><span class="sxs-lookup"><span data-stu-id="926f0-140">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![透過 NuGet 套件管理員選項控制套件還原行為](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="926f0-142">**允許 NuGet 下載遺漏的套件**：變更 `NuGet.Config` 檔案中的 `packageRestore/enabled` 設定，以控制所有形式的套件還原，如下所示 (在 Windows 上為 `%AppData%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.nuget/NuGet/NuGet.Config`)。</span><span class="sxs-lookup"><span data-stu-id="926f0-142">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="926f0-143">在 Visual Studio 中，此設定可讓解決方案操作功能表上的 [還原 NuGet 套件] 命令運作。</span><span class="sxs-lookup"><span data-stu-id="926f0-143">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  <span data-ttu-id="926f0-144">在啟動 Visual Studio 或啟動組建之前，可以設定稱為 **EnableNuGetPackageRestore** 且值為 TRUE 或 FALSE 的環境變數，以全域覆寫 `packageRestore/enabled` 設定。</span><span class="sxs-lookup"><span data-stu-id="926f0-144">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="926f0-145">**在 Visual Studio 建置期間自動檢查遺漏的套件**：變更 `NuGet.Config` 檔案中的 `packageRestore/automatic` 設定，以控制自動還原，如下所示 (在 Windows 上為 `%AppData%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.nuget/NuGet/NuGet.Config`)。</span><span class="sxs-lookup"><span data-stu-id="926f0-145">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="926f0-146">設定此選項時，從 Visual Studio 中執行組建，會自動還原任何遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="926f0-146">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="926f0-147">此選項不會影響使用 MSBuild 從命令列執行的組建。</span><span class="sxs-lookup"><span data-stu-id="926f0-147">The option does not affect builds run from the command line using MSBuild.</span></span>

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

<span data-ttu-id="926f0-148">如需參考，請參閱 [NuGet 組態檔 - packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)。</span><span class="sxs-lookup"><span data-stu-id="926f0-148">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="926f0-149">在某些情況下，開發人員或公司可能想要針對電腦上的所有使用者啟用或停用套件還原。</span><span class="sxs-lookup"><span data-stu-id="926f0-149">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="926f0-150">若要這麼做，請將上述相同設定新增到全域 NuGet 組態檔中，此檔案位於 `%ProgramData%\NuGet\Config` (Windows，可能位於 Visual Studio 的特定 `\{IDE}\{Version}\{SKU}\` 資料夾下) 或 `~/.local/share` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="926f0-150">To do this, add the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config` (Windows, potentially under a specific `\{IDE}\{Version}\{SKU}\` folder for Visual Studio) or `~/.local/share` (Mac/Linux).</span></span> <span data-ttu-id="926f0-151">個別使用者接著可以視需要選擇性地啟用專案層級的還原。</span><span class="sxs-lookup"><span data-stu-id="926f0-151">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="926f0-152">如需 NuGet 如何設定多個組態檔優先順序的確切詳細資料，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="926f0-152">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

> [!Important]
> <span data-ttu-id="926f0-153">如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓選項對話方塊顯示目前的值。</span><span class="sxs-lookup"><span data-stu-id="926f0-153">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="926f0-154">使用還原限制套件版本</span><span class="sxs-lookup"><span data-stu-id="926f0-154">Constraining package versions with restore</span></span>

<span data-ttu-id="926f0-155">透過任何方法還原套件時，NuGet 會遵循 `packages.config` 或專案檔中所指定的任何條件約束：</span><span class="sxs-lookup"><span data-stu-id="926f0-155">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="926f0-156">`packages.config`：指定相依性之 `allowedVersion` 屬性中的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="926f0-156">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="926f0-157">請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="926f0-157">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="926f0-158">例如：</span><span class="sxs-lookup"><span data-stu-id="926f0-158">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="926f0-159">專案檔 (PackageReference)：直接使用相依性的版本號碼來指定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="926f0-159">Project file (PackageReference): Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="926f0-160">例如：</span><span class="sxs-lookup"><span data-stu-id="926f0-160">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="926f0-161">在所有情況下，都請使用[套件版本控制](../reference/package-versioning.md)中所述的標記法。</span><span class="sxs-lookup"><span data-stu-id="926f0-161">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="forcing-restore-from-package-sources"></a><span data-ttu-id="926f0-162">強制從套件來源還原</span><span class="sxs-lookup"><span data-stu-id="926f0-162">Forcing restore from package sources</span></span>

<span data-ttu-id="926f0-163">根據預設，NuGet 還原作業會使用來自 *global-packages* 和 *http-cache* 資料夾的套件，這在[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中有說明。</span><span class="sxs-lookup"><span data-stu-id="926f0-163">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="926f0-164">若要避免使用 *global-packages* 資料夾，請執行下列任一步驟：</span><span class="sxs-lookup"><span data-stu-id="926f0-164">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="926f0-165">使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除資料夾</span><span class="sxs-lookup"><span data-stu-id="926f0-165">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`</span></span>
- <span data-ttu-id="926f0-166">使用下列方法其中之一，在還原作業之前暫時變更 *global-packages* 資料夾的位置：</span><span class="sxs-lookup"><span data-stu-id="926f0-166">Temporarily change the location of the *global-packages* folder before the restore operation using one of the following methods:</span></span>
  - <span data-ttu-id="926f0-167">將 NUGET_PACKAGES 環境變數設定為不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="926f0-167">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="926f0-168">建立將 `globalPackagesFolder` (如果使用 PackageReference) 或 `repositoryPath` (如果使用 `packages.config`) 設定為不同資料夾的 `NuGet.Config` 檔案 (請參閱[組態設定](../reference/nuget-config-file.md#config-section)</span><span class="sxs-lookup"><span data-stu-id="926f0-168">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder (see [configuration settings](../reference/nuget-config-file.md#config-section)</span></span>
  - <span data-ttu-id="926f0-169">僅限 MSBuild：使用 `RestorePackagesPath` 屬性來指定不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="926f0-169">MSBuild only: specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="926f0-170">若要避免使用 HTTP 來源的快取，請執行下列任一步驟：</span><span class="sxs-lookup"><span data-stu-id="926f0-170">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="926f0-171">使用 `-NoCache` 選項搭配 `nuget restore`，或 `--no-cache` 選項搭配 `dotnet restore`。</span><span class="sxs-lookup"><span data-stu-id="926f0-171">Use the `-NoCache` option with `nuget restore` or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="926f0-172">這些選項不會影響透過 Visual Studio 套件管理員 UI 或主控台進行的還原作業。</span><span class="sxs-lookup"><span data-stu-id="926f0-172">These options do not affect restore operations through the Visual Studio Package Manager UI or Console.</span></span>
- <span data-ttu-id="926f0-173">使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear`清除快取。</span><span class="sxs-lookup"><span data-stu-id="926f0-173">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="926f0-174">暫時將 NUGET_HTTP_CACHE_PATH 環境變數設定為不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="926f0-174">Temporarily set of the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="926f0-175">疑難排解</span><span class="sxs-lookup"><span data-stu-id="926f0-175">Troubleshooting</span></span>

<span data-ttu-id="926f0-176">請參閱[針對套件還原進行疑難排解](package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="926f0-176">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>
