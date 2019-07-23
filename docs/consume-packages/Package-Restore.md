---
title: NuGet 套件還原
description: NuGet 如何還原專案相依套件的概觀，包括如何停用還原和限制版本。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: e85d8cc3fd9492118bd8f34cfd05f20a9724c281
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842346"
---
# <a name="package-restore-options"></a><span data-ttu-id="97938-103">套件還原選項</span><span class="sxs-lookup"><span data-stu-id="97938-103">Package Restore options</span></span>

<span data-ttu-id="97938-104">為了提倡更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原**會依專案檔或 `packages.config` 中所列，安裝專案的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="97938-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="97938-105">.NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令會執行自動套件還原。</span><span class="sxs-lookup"><span data-stu-id="97938-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="97938-106">Visual Studio 可以在建置專案時自動還原套件，您可以隨時透過 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 上的 xbuild 來還原套件。</span><span class="sxs-lookup"><span data-stu-id="97938-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="97938-107">套件還原會確認專案的所有相依性都可用，而不必將它們儲存在原始檔控制中。</span><span class="sxs-lookup"><span data-stu-id="97938-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="97938-108">若要設定原始程式碼控制存放庫以排除套件二進位檔，請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="97938-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="97938-109">套件還原概觀</span><span class="sxs-lookup"><span data-stu-id="97938-109">Package Restore overview</span></span>

<span data-ttu-id="97938-110">套件還原會先視需要安裝專案的直接相依性，然後在整個相依性關係圖中安裝那些套件的任何相依性。</span><span class="sxs-lookup"><span data-stu-id="97938-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="97938-111">如果尚未安裝套件，NuGet 會先嘗試從[快取](../consume-packages/managing-the-global-packages-and-cache-folders.md)中擷取它。</span><span class="sxs-lookup"><span data-stu-id="97938-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="97938-112">如果套件不在快取中，NuGet 會嘗試從清單中的所有已啟用來源下載套件，位置是 Visual Studio 中的 [工具]   > [選項]   > [NuGet 套件管理員]   > [套件來源]  。</span><span class="sxs-lookup"><span data-stu-id="97938-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="97938-113">在還原程序中，NuGet 會忽略套件來源的順序，且使用任一個最先回應要求的來源。</span><span class="sxs-lookup"><span data-stu-id="97938-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="97938-114">如需 NuGet 運作方式的詳細資訊，請參閱[常用的 NuGet 組態](Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="97938-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="97938-115">在所有來源檢查完畢前，NuGet 不會指出還原套件失敗。</span><span class="sxs-lookup"><span data-stu-id="97938-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="97938-116">到那時候，NuGet 只會針對清單中的最後一個來源回報失敗。</span><span class="sxs-lookup"><span data-stu-id="97938-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="97938-117">這項錯誤表示套件未出現在其他「任何」  來源上，即使那些來源都未個別出現錯誤亦然。</span><span class="sxs-lookup"><span data-stu-id="97938-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="97938-118">還原套件</span><span class="sxs-lookup"><span data-stu-id="97938-118">Restore packages</span></span>

<span data-ttu-id="97938-119">您可以用下列任一方式來觸發套件還原：</span><span class="sxs-lookup"><span data-stu-id="97938-119">You can trigger Package Restore in any of the following ways:</span></span>

- <span data-ttu-id="97938-120">**Visual Studio**：在 Windows 的 Visual Studio 中，可以使用下列方法之一。</span><span class="sxs-lookup"><span data-stu-id="97938-120">**Visual Studio**: In Visual Studio on Windows, use one of the following methods.</span></span>

    - <span data-ttu-id="97938-121">自動還原套件。</span><span class="sxs-lookup"><span data-stu-id="97938-121">Restore packages automatically.</span></span> <span data-ttu-id="97938-122">套件還原會在您從範本建立專案或建置專案時自動進行，且受限於[啟用和停用套件還原](#enable-and-disable-package-restore-visual-studio)中的選項。</span><span class="sxs-lookup"><span data-stu-id="97938-122">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="97938-123">在 NuGet 4.0+ 中，還原也會在您變更 SDK 樣式專案 (通常是 .NET Core 或 .NET Standard 專案) 時自動進行。</span><span class="sxs-lookup"><span data-stu-id="97938-123">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

    - <span data-ttu-id="97938-124">手動還原套件。</span><span class="sxs-lookup"><span data-stu-id="97938-124">Restore packages manually.</span></span> <span data-ttu-id="97938-125">若要手動還原，請以滑鼠右鍵按一下 [方案總管]  中的解決方案，然後選取 [還原 NuGet 套件]  。</span><span class="sxs-lookup"><span data-stu-id="97938-125">To restore manually, right-click the solution in **Solution Explorer** and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="97938-126">如果一或多個個別套件仍未正確安裝，則 [方案總管]  會顯示錯誤圖示。</span><span class="sxs-lookup"><span data-stu-id="97938-126">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="97938-127">以滑鼠右鍵按一下並選取 [管理 NuGet 套件]  ，且使用 [套件管理員]  先解除安裝再重新安裝受影響的套件。</span><span class="sxs-lookup"><span data-stu-id="97938-127">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="97938-128">如需詳細資訊，請參閱[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="97938-128">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="97938-129">如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請[啟用自動還原](#enable-and-disable-package-restore-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="97938-129">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="97938-130">此外，請參閱[遷移至自動套件還原](#migrate-to-automatic-package-restore-visual-studio)和[套件還原疑難排解](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="97938-130">Also, see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio) and [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="97938-131">**dotnet CLI**：在命令列中，切換至包含專案的資料夾，然後使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令來還原專案檔中以 [PackageReference](../consume-packages/package-references-in-project-files.md) 列出的套件。</span><span class="sxs-lookup"><span data-stu-id="97938-131">**dotnet CLI**: In the command line, switch to the folder that contains your project, and then use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command to restore packages listed in the project file with [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span> <span data-ttu-id="97938-132">使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 命令自動完成還原。</span><span class="sxs-lookup"><span data-stu-id="97938-132">With .NET Core 2.0 and later, restore happens automatically with the `dotnet build` and `dotnet run` commands.</span></span>  

- <span data-ttu-id="97938-133">**nuget.exe CLI**：在命令列中，切換至包含專案的資料夾，然後使用 [nuget restore](../tools/cli-ref-restore.md) 命令來還原專案檔或解決方案檔中 (或 `packages.config` 中) 列出的套件。</span><span class="sxs-lookup"><span data-stu-id="97938-133">**nuget.exe CLI**: In the command line, switch to the folder that contains your project, and then use the [nuget restore](../tools/cli-ref-restore.md) command to restore packages listed in a project or solution file, or in `packages.config`.</span></span> 

- <span data-ttu-id="97938-134">**MSBuild**：使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令，利用 PackageReference 來還原專案檔中所列套件。</span><span class="sxs-lookup"><span data-stu-id="97938-134">**MSBuild**: Use the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command to restore packages listed in the project file with PackageReference.</span></span> <span data-ttu-id="97938-135">這個命令只適用於 NuGet 4.x+ 和 MSBuild 15.1+ (兩者均隨附於 Visual Studio 2017 和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="97938-135">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="97938-136">`nuget restore` 和 `dotnet restore` 都會將這個命令用於適用的專案。</span><span class="sxs-lookup"><span data-stu-id="97938-136">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

- <span data-ttu-id="97938-137">**Azure Pipelines**：在 Azure Pipelines 中建立組建定義時，在定義中於任何建置工作之前包含 NuGet [還原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)或 .NET Core [還原](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops)工作。</span><span class="sxs-lookup"><span data-stu-id="97938-137">**Azure Pipelines**: When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="97938-138">根據預設，一些建置範本已包含還原工作。</span><span class="sxs-lookup"><span data-stu-id="97938-138">Some build templates include the restore task by default.</span></span>

- <span data-ttu-id="97938-139">**Azure DevOps Server**：Azure DevOps Server 和 TFS 2013 及更新版本會在建置期間自動還原套件，前提是您使用 TFS 2013 或更新版本的 Team Build 範本。</span><span class="sxs-lookup"><span data-stu-id="97938-139">**Azure DevOps Server**: Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="97938-140">針對較舊的 TFS 版本，您可以包含一個建置步驟來執行命令列還原選項，或選擇性地將建置範本移轉至較新版本。</span><span class="sxs-lookup"><span data-stu-id="97938-140">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="97938-141">如需詳細資訊，請參閱[使用 Team Foundation Build 的套件還原設定](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="97938-141">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enable-and-disable-package-restore-visual-studio"></a><span data-ttu-id="97938-142">啟用和停用套件還原 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="97938-142">Enable and disable package restore (Visual Studio)</span></span>

<span data-ttu-id="97938-143">在 Visual Studio 中，您主要是透過 [工具]   > [選項]   > [NuGet 套件管理員]  來控制套件還原：</span><span class="sxs-lookup"><span data-stu-id="97938-143">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![透過 NuGet 套件管理員選項控制套件還原](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="97938-145">**允許 NuGet 下載遺漏的套件**會藉由變更 `NuGet.Config` 檔案 (在 Windows 上為 `%AppData%\NuGet\`，在 Mac/Linux 上則為 `~/.nuget/NuGet/`) [packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)的 `packageRestore/enabled` 設定，控制所有形式的套件還原。</span><span class="sxs-lookup"><span data-stu-id="97938-145">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="97938-146">此設定也會啟用 Visual Studio 中解決方案操作功能表上的 [還原 NuGet 套件]  命令。</span><span class="sxs-lookup"><span data-stu-id="97938-146">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > <span data-ttu-id="97938-147">在啟動 Visual Studio 或啟動組建之前，若要全域覆寫 `packageRestore/enabled` 設定，可以用值 True 或 False 來設定 **EnableNuGetPackageRestore** 環境變數。</span><span class="sxs-lookup"><span data-stu-id="97938-147">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="97938-148">**在 Visual Studio 建置期間自動檢查遺漏的套件**會藉由變更 `NuGet.Config` 檔案 [packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)中的 `packageRestore/automatic` 設定來控制自動還原。</span><span class="sxs-lookup"><span data-stu-id="97938-148">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="97938-149">將此選項設為 True 時，從 Visual Studio 中執行組建會自動還原任何遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="97938-149">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="97938-150">此設定不會影響從 MSBuild 命令列執行的組建。</span><span class="sxs-lookup"><span data-stu-id="97938-150">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="97938-151">若要針對電腦上的所有使用者啟用或停用套件還原，開發人員或公司可以將組態設定新增到全域 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="97938-151">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="97938-152">全域 `nuget.config` 是在 Windows 中的 `%ProgramData%\NuGet\Config`，有時在特定 `\{IDE}\{Version}\{SKU}\` Visual Studio 資料夾中，或在 Mac/Linux 的 `~/.local/share`。</span><span class="sxs-lookup"><span data-stu-id="97938-152">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="97938-153">個別使用者接著可以視需要選擇性地啟用專案層級的還原。</span><span class="sxs-lookup"><span data-stu-id="97938-153">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="97938-154">如需 NuGet 如何排定多個組態檔優先順序的詳細資料，請參閱[常見的 NuGet 行為](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="97938-154">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="97938-155">如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓 [選項]  對話方塊顯示目前的值。</span><span class="sxs-lookup"><span data-stu-id="97938-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="97938-156">使用還原來限制套件版本</span><span class="sxs-lookup"><span data-stu-id="97938-156">Constrain package versions with restore</span></span>

<span data-ttu-id="97938-157">NuGet 透過任何方法還原套件時，會使用 `packages.config` 或專案檔中所指定的任何條件約束：</span><span class="sxs-lookup"><span data-stu-id="97938-157">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="97938-158">在 `packages.config` 中，您可以在相依性的 `allowedVersion` 屬性中指定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="97938-158">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="97938-159">如需詳細資訊，請參閱[限制升級版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="97938-159">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="97938-160">例如：</span><span class="sxs-lookup"><span data-stu-id="97938-160">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="97938-161">在專案檔中，您可以使用 PackageReference 來直接指定相依性的範圍。</span><span class="sxs-lookup"><span data-stu-id="97938-161">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="97938-162">例如：</span><span class="sxs-lookup"><span data-stu-id="97938-162">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="97938-163">在所有情況下，都請使用[套件版本控制](../reference/package-versioning.md)中所述的標記法。</span><span class="sxs-lookup"><span data-stu-id="97938-163">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="97938-164">強制從套件來源還原</span><span class="sxs-lookup"><span data-stu-id="97938-164">Force restore from package sources</span></span>

<span data-ttu-id="97938-165">根據預設，NuGet 還原作業會使用來自 *global-packages* 和 *http-cache* 資料夾的套件，這在[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中有描述。</span><span class="sxs-lookup"><span data-stu-id="97938-165">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="97938-166">若要避免使用 *global-packages* 資料夾，請執行下列任一步驟：</span><span class="sxs-lookup"><span data-stu-id="97938-166">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="97938-167">使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除資料夾。</span><span class="sxs-lookup"><span data-stu-id="97938-167">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="97938-168">使用下列其中一種方法，在還原作業之前暫時變更 *global-packages* 資料夾的位置：</span><span class="sxs-lookup"><span data-stu-id="97938-168">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="97938-169">將 NUGET_PACKAGES 環境變數設定為不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="97938-169">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="97938-170">建立將 `globalPackagesFolder` (如果使用 PackageReference) 或 `repositoryPath` (如果使用 `packages.config`) 設定為不同資料夾的 `NuGet.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="97938-170">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="97938-171">如需詳細資訊，請參閱[組態設定](../reference/nuget-config-file.md#config-section)。</span><span class="sxs-lookup"><span data-stu-id="97938-171">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="97938-172">僅限 MSBuild：使用 `RestorePackagesPath` 屬性來指定不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="97938-172">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="97938-173">若要避免使用 HTTP 來源的快取，請執行下列任一步驟：</span><span class="sxs-lookup"><span data-stu-id="97938-173">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="97938-174">使用 `-NoCache` 選項搭配 `nuget restore`，或 `--no-cache` 選項搭配 `dotnet restore`。</span><span class="sxs-lookup"><span data-stu-id="97938-174">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="97938-175">這些選項不會影響透過 Visual Studio 套件管理員或主控台進行的還原作業。</span><span class="sxs-lookup"><span data-stu-id="97938-175">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="97938-176">使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear`清除快取。</span><span class="sxs-lookup"><span data-stu-id="97938-176">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="97938-177">暫時將 NUGET_HTTP_CACHE_PATH 環境變數設定為不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="97938-177">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="97938-178">遷移至自動套件還原 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="97938-178">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="97938-179">針對 NuGet 2.6 和更早版本，先前支援的 MSBuild 整合套件還原已不再適用。</span><span class="sxs-lookup"><span data-stu-id="97938-179">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="97938-180">(通常是在 Visual Studio 中以滑鼠右鍵按一下解決方案，然後選取 [啟用 NuGet 套件還原]  來啟用)。</span><span class="sxs-lookup"><span data-stu-id="97938-180">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="97938-181">如果您的專案是使用整合 MSBuild 套件還原，請遷移至自動套件還原。</span><span class="sxs-lookup"><span data-stu-id="97938-181">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="97938-182">使用整合 MSBuild 套件還原的專案通常會包含 [.nuget]  資料夾和三個檔案：*NuGet.config*、*nuget.exe* 和 *NuGet.targets*。</span><span class="sxs-lookup"><span data-stu-id="97938-182">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="97938-183">*NuGet.targets* 檔案的存在會決定 NuGet 是否繼續使用整合 MSBuild 方法，所以進行遷移時必須移除該檔案。</span><span class="sxs-lookup"><span data-stu-id="97938-183">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="97938-184">若要遷移至自動套件還原：</span><span class="sxs-lookup"><span data-stu-id="97938-184">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="97938-185">關閉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="97938-185">Close Visual Studio.</span></span>
2. <span data-ttu-id="97938-186">刪除 *.nuget/nuget.exe* 和 *.nuget/NuGet.targets*。</span><span class="sxs-lookup"><span data-stu-id="97938-186">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="97938-187">針對每個專案檔，移除 `<RestorePackages>` 元素，並移除任何對 *NuGet.targets* 的參考。</span><span class="sxs-lookup"><span data-stu-id="97938-187">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="97938-188">若要測試自動套件還原：</span><span class="sxs-lookup"><span data-stu-id="97938-188">To test the automatic package restore:</span></span>

1. <span data-ttu-id="97938-189">將 [packages]  資料夾從解決方案中移除。</span><span class="sxs-lookup"><span data-stu-id="97938-189">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="97938-190">在 Visual Studio 中開啟方案，並啟動建置。</span><span class="sxs-lookup"><span data-stu-id="97938-190">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="97938-191">自動套件還原應該會下載並安裝每個相依性套件，而不會將他們新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="97938-191">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="97938-192">疑難排解</span><span class="sxs-lookup"><span data-stu-id="97938-192">Troubleshooting</span></span>

<span data-ttu-id="97938-193">請參閱[針對套件還原進行疑難排解](package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="97938-193">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
