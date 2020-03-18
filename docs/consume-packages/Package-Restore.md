---
title: NuGet 套件還原
description: NuGet 如何還原專案相依套件的概觀，包括如何停用還原和限制版本。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428741"
---
# <a name="restore-packages-using-package-restore"></a><span data-ttu-id="163d5-103">使用套件還原還原套件</span><span class="sxs-lookup"><span data-stu-id="163d5-103">Restore packages using Package Restore</span></span>

<span data-ttu-id="163d5-104">為了提倡更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原**會依專案檔或 `packages.config` 中所列，安裝專案的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="163d5-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="163d5-105">.NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令會執行自動套件還原。</span><span class="sxs-lookup"><span data-stu-id="163d5-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="163d5-106">Visual Studio 可以在建置專案時自動還原套件，您可以隨時透過 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 上的 xbuild 來還原套件。</span><span class="sxs-lookup"><span data-stu-id="163d5-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="163d5-107">套件還原會確認專案的所有相依性都可用，而不必將它們儲存在原始檔控制中。</span><span class="sxs-lookup"><span data-stu-id="163d5-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="163d5-108">若要設定原始程式碼控制存放庫以排除套件二進位檔，請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="163d5-109">套件還原概觀</span><span class="sxs-lookup"><span data-stu-id="163d5-109">Package Restore overview</span></span>

<span data-ttu-id="163d5-110">套件還原會先視需要安裝專案的直接相依性，然後在整個相依性關係圖中安裝那些套件的任何相依性。</span><span class="sxs-lookup"><span data-stu-id="163d5-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="163d5-111">如果尚未安裝套件，NuGet 會先嘗試從[快取](../consume-packages/managing-the-global-packages-and-cache-folders.md)中擷取它。</span><span class="sxs-lookup"><span data-stu-id="163d5-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="163d5-112">如果套件不在快取中，NuGet 會嘗試從清單中的所有已啟用來源下載套件，位置是 Visual Studio 中的 [工具] > [選項] > [NuGet 套件管理員] > [套件來源]。</span><span class="sxs-lookup"><span data-stu-id="163d5-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="163d5-113">在還原程序中，NuGet 會忽略套件來源的順序，且使用任一個最先回應要求的來源。</span><span class="sxs-lookup"><span data-stu-id="163d5-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="163d5-114">如需 NuGet 運作方式的詳細資訊，請參閱[常用的 NuGet 組態](Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="163d5-115">在所有來源檢查完畢前，NuGet 不會指出還原套件失敗。</span><span class="sxs-lookup"><span data-stu-id="163d5-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="163d5-116">到那時候，NuGet 只會針對清單中的最後一個來源回報失敗。</span><span class="sxs-lookup"><span data-stu-id="163d5-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="163d5-117">這項錯誤表示套件未出現在其他「任何」來源上，即使那些來源都未個別出現錯誤亦然。</span><span class="sxs-lookup"><span data-stu-id="163d5-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="163d5-118">還原套件</span><span class="sxs-lookup"><span data-stu-id="163d5-118">Restore packages</span></span>

<span data-ttu-id="163d5-119">套件還原會嘗試將所有套件相依性安裝到符合專案檔 ( *.csproj*) 或您的 *packages.config* 檔案中套件參考的正確狀態。</span><span class="sxs-lookup"><span data-stu-id="163d5-119">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="163d5-120">(在 Visual Studio 中，參考會出現在 [方案總管] 的 [相依性 \ NuGet] 或 [參考] 節點下。)</span><span class="sxs-lookup"><span data-stu-id="163d5-120">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.)</span></span>

1. <span data-ttu-id="163d5-121">如果專案檔中的套件參考是正確的，請使用您慣用的工具來還原套件。</span><span class="sxs-lookup"><span data-stu-id="163d5-121">If the package references in your project file are correct, use your preferred tool to restore packages.</span></span>

   - <span data-ttu-id="163d5-122">[Visual Studio](#restore-using-visual-studio) ([自動還原](#restore-packages-automatically-using-visual-studio)或[手動還原](#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="163d5-122">[Visual Studio](#restore-using-visual-studio) ([automatic restore](#restore-packages-automatically-using-visual-studio) or [manual restore](#restore-packages-manually-using-visual-studio))</span></span>
   - [<span data-ttu-id="163d5-123">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="163d5-123">dotnet CLI</span></span>](#restore-using-the-dotnet-cli)
   - [<span data-ttu-id="163d5-124">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="163d5-124">nuget.exe CLI</span></span>](#restore-using-the-nugetexe-cli)
   - [<span data-ttu-id="163d5-125">MSBuild</span><span class="sxs-lookup"><span data-stu-id="163d5-125">MSBuild</span></span>](#restore-using-msbuild)
   - [<span data-ttu-id="163d5-126">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="163d5-126">Azure Pipelines</span></span>](#restore-using-azure-pipelines)
   - [<span data-ttu-id="163d5-127">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="163d5-127">Azure DevOps Server</span></span>](#restore-using-azure-devops-server)

   <span data-ttu-id="163d5-128">如果專案檔 ( *.csproj*) 或您的 *packages.config* 檔案中的套件參考不正確 (不符合您在套件還原之後所需的狀態)，則您需要改為安裝套件或更新套件。</span><span class="sxs-lookup"><span data-stu-id="163d5-128">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead.</span></span>

   <span data-ttu-id="163d5-129">針對使用 PackageReference 的專案，在成功還原之後，套件應該會出現在 [global-packages] 資料夾中，而且 `obj/project.assets.json` 檔案會重新建立。</span><span class="sxs-lookup"><span data-stu-id="163d5-129">For projects using PackageReference, after a successful restore, the package should be present in the *global-packages* folder and the `obj/project.assets.json` file is recreated.</span></span> <span data-ttu-id="163d5-130">針對使用 `packages.config` 的專案，套件應該會出現在專案的 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="163d5-130">For projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="163d5-131">專案現在應可順利建置。</span><span class="sxs-lookup"><span data-stu-id="163d5-131">The project should now build successfully.</span></span> 

2. <span data-ttu-id="163d5-132">如果您在執行套件還原之後，仍然遇到缺少套件或套件相關的問題 (例如 Visual Studio 方案總管中的錯誤圖示)，建議您遵循[對套件還原錯誤進行疑難排解](package-restore-troubleshooting.md)中的指示，或者[重新安裝並更新套件](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-132">After running Package Restore, if you still experience missing packages or package-related errors (such as error icons in Solution Explorer in Visual Studio), you may need to follow instructions described in [Troubleshooting Package Restore errors](package-restore-troubleshooting.md) or, alternatively, [reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

   <span data-ttu-id="163d5-133">在 Visual Studio 中，套件管理員主控台提供幾個彈性的選項來重新安裝套件。</span><span class="sxs-lookup"><span data-stu-id="163d5-133">In Visual Studio, the Package Manager Console provides several flexible options for reinstalling packages.</span></span> <span data-ttu-id="163d5-134">請參閱[使用 Package-Update](reinstalling-and-updating-packages.md#using-update-package)。</span><span class="sxs-lookup"><span data-stu-id="163d5-134">See [Using Package-Update](reinstalling-and-updating-packages.md#using-update-package).</span></span>

## <a name="restore-using-visual-studio"></a><span data-ttu-id="163d5-135">使用 Visual Studio 進行還原</span><span class="sxs-lookup"><span data-stu-id="163d5-135">Restore using Visual Studio</span></span>

<span data-ttu-id="163d5-136">在 Windows 的 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="163d5-136">In Visual Studio on Windows, either:</span></span>

- <span data-ttu-id="163d5-137">自動還原套件，或</span><span class="sxs-lookup"><span data-stu-id="163d5-137">Restore packages automatically, or</span></span>

- <span data-ttu-id="163d5-138">手動還原套件</span><span class="sxs-lookup"><span data-stu-id="163d5-138">Restore packages manually</span></span>

### <a name="restore-packages-automatically-using-visual-studio"></a><span data-ttu-id="163d5-139">使用 Visual Studio 自動還原套件</span><span class="sxs-lookup"><span data-stu-id="163d5-139">Restore packages automatically using Visual Studio</span></span>

<span data-ttu-id="163d5-140">套件還原會在您從範本建立專案或建置專案時自動進行，且受限於[啟用和停用套件還原](#enable-and-disable-package-restore-in-visual-studio)中的選項。</span><span class="sxs-lookup"><span data-stu-id="163d5-140">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="163d5-141">在 NuGet 4.0+ 中，還原也會在您變更 SDK 樣式專案 (通常是 .NET Core 或 .NET Standard 專案) 時自動進行。</span><span class="sxs-lookup"><span data-stu-id="163d5-141">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

1. <span data-ttu-id="163d5-142">選擇 [工具] > [選項] > [NuGet 套件管理員]，然後選取 [套件還原] 下的 [在 Visual Studio 建置期間自動檢查遺漏的套件 ]。</span><span class="sxs-lookup"><span data-stu-id="163d5-142">Enable automatic package restore by choosing **Tools** > **Options** > **NuGet Package Manager**, and then selecting **Automatically check for missing packages during build in Visual Studio** under **Package Restore**.</span></span>

   <span data-ttu-id="163d5-143">針對非 SDK 樣式的專案，您必須先選取 [允許 NuGet 下載遺漏的套件 ] 以啟用自動還原選項。</span><span class="sxs-lookup"><span data-stu-id="163d5-143">For non-SDK-style projects, you first need to select **Allow NuGet to download missing packages** to enable the automatic restore option.</span></span>

1. <span data-ttu-id="163d5-144">建置專案。</span><span class="sxs-lookup"><span data-stu-id="163d5-144">Build the project.</span></span>

   <span data-ttu-id="163d5-145">如果一或多個個別套件仍未正確安裝，則 [方案總管] 會顯示錯誤圖示。</span><span class="sxs-lookup"><span data-stu-id="163d5-145">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="163d5-146">以滑鼠右鍵按一下並選取 [管理 NuGet 套件]，且使用 [套件管理員] 先解除安裝再重新安裝受影響的套件。</span><span class="sxs-lookup"><span data-stu-id="163d5-146">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="163d5-147">如需詳細資訊，請參閱[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="163d5-147">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="163d5-148">如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請[啟用自動還原](#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="163d5-148">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="163d5-149">針對較舊的專案，另請參閱[移轉至自動套件還原](#migrate-to-automatic-package-restore-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="163d5-149">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="163d5-150">另請參閱[針對套件還原進行疑難排解](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-150">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="restore-packages-manually-using-visual-studio"></a><span data-ttu-id="163d5-151">使用 Visual Studio 手動還原套件</span><span class="sxs-lookup"><span data-stu-id="163d5-151">Restore packages manually using Visual Studio</span></span>

1. <span data-ttu-id="163d5-152">選擇 [工具] > [選項] > [NuGet 套件管理員] 以啟用套件還原。</span><span class="sxs-lookup"><span data-stu-id="163d5-152">Enable package restore by choosing **Tools** > **Options** > **NuGet Package Manager**.</span></span> <span data-ttu-id="163d5-153">在 [套件還原] 選項下，選取 [允許 NuGet 下載遺漏的套件]。</span><span class="sxs-lookup"><span data-stu-id="163d5-153">Under **Package Restore** options, select **Allow NuGet to download missing packages**.</span></span>

1. <span data-ttu-id="163d5-154">在 [方案總管] 中，請以滑鼠右鍵按一下解決方案，然後選取 [還原 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="163d5-154">In **Solution Explorer**, right click the solution and select **Restore NuGet Packages**.</span></span>

   <span data-ttu-id="163d5-155">如果一或多個個別套件仍未正確安裝，則 [方案總管] 會顯示錯誤圖示。</span><span class="sxs-lookup"><span data-stu-id="163d5-155">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="163d5-156">以滑鼠右鍵按一下並選取 [管理 NuGet 套件]，然後使用 [套件管理員] 先解除安裝再重新安裝受影響的套件。</span><span class="sxs-lookup"><span data-stu-id="163d5-156">Right-click and select **Manage NuGet Packages**, and then use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="163d5-157">如需詳細資訊，請參閱[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="163d5-157">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="163d5-158">如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請[啟用自動還原](#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="163d5-158">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="163d5-159">針對較舊的專案，另請參閱[移轉至自動套件還原](#migrate-to-automatic-package-restore-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="163d5-159">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="163d5-160">另請參閱[針對套件還原進行疑難排解](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-160">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="enable-and-disable-package-restore-in-visual-studio"></a><span data-ttu-id="163d5-161">在 Visual Studio 中啟用及停用套件還原</span><span class="sxs-lookup"><span data-stu-id="163d5-161">Enable and disable package restore in Visual Studio</span></span>

<span data-ttu-id="163d5-162">在 Visual Studio 中，您主要是透過 [工具] > [選項] > [NuGet 套件管理員] 來控制套件還原：</span><span class="sxs-lookup"><span data-stu-id="163d5-162">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![透過 NuGet 套件管理員選項控制套件還原](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="163d5-164">**允許 NuGet 下載遺漏的套件**會藉由變更 `packageRestore/enabled` 檔案 (在 Windows 上為 [，在 Mac/Linux 上則為 ](../reference/nuget-config-file.md#packagerestore-section)) `NuGet.Config`packageRestore 區段`%AppData%\NuGet\`的 `~/.nuget/NuGet/` 設定，控制所有形式的套件還原。</span><span class="sxs-lookup"><span data-stu-id="163d5-164">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="163d5-165">此設定也會啟用 Visual Studio 中解決方案操作功能表上的 [還原 NuGet 套件] 命令。</span><span class="sxs-lookup"><span data-stu-id="163d5-165">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

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
  > <span data-ttu-id="163d5-166">在啟動 Visual Studio 或啟動組建之前，若要全域覆寫 `packageRestore/enabled` 設定，可以用值 True 或 False 來設定 **EnableNuGetPackageRestore** 環境變數。</span><span class="sxs-lookup"><span data-stu-id="163d5-166">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="163d5-167">**在 Visual Studio 建置期間自動檢查遺漏的套件**會藉由變更 `packageRestore/automatic` 檔案 [packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)中的 `NuGet.Config` 設定來控制自動還原。</span><span class="sxs-lookup"><span data-stu-id="163d5-167">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="163d5-168">將此選項設為 True 時，從 Visual Studio 中執行組建會自動還原任何遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="163d5-168">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="163d5-169">此設定不會影響從 MSBuild 命令列執行的組建。</span><span class="sxs-lookup"><span data-stu-id="163d5-169">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="163d5-170">若要針對電腦上的所有使用者啟用或停用套件還原，開發人員或公司可以將組態設定新增到全域 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="163d5-170">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="163d5-171">全域 `nuget.config` 是在 Windows 中的 `%ProgramData%\NuGet\Config`，有時在特定 `\{IDE}\{Version}\{SKU}\` Visual Studio 資料夾中，或在 Mac/Linux 的 `~/.local/share`。</span><span class="sxs-lookup"><span data-stu-id="163d5-171">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="163d5-172">個別使用者接著可以視需要選擇性地啟用專案層級的還原。</span><span class="sxs-lookup"><span data-stu-id="163d5-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="163d5-173">如需 NuGet 如何排定多個組態檔優先順序的詳細資料，請參閱[常見的 NuGet 行為](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="163d5-173">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="163d5-174">如果您直接在 `packageRestore` 中編輯 `nuget.config` 設定，請重新啟動 Visual Studio，讓 [選項] 對話方塊顯示目前的值。</span><span class="sxs-lookup"><span data-stu-id="163d5-174">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

### <a name="choose-default-package-management-format"></a><span data-ttu-id="163d5-175">選擇預設套件管理格式</span><span class="sxs-lookup"><span data-stu-id="163d5-175">Choose default package management format</span></span>

![以 NuGet 套件管理員選項控制預設的套件管理格式](media/Restore-02-PackageFormatOptions.png)

<span data-ttu-id="163d5-177">NuGet 有兩種格式，可供專案使用封裝： [`PackageReference`](package-references-in-project-files.md)和[`packages.config`](../reference/packages-config.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-177">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="163d5-178">您可以從 [**套件管理**] 標題下的下拉式選單中選取預設格式。</span><span class="sxs-lookup"><span data-stu-id="163d5-178">The default format can be selected from the drop-down under the **Package Management** heading.</span></span> <span data-ttu-id="163d5-179">同時也提供在專案中安裝第一個套件時，所要提示的選項。</span><span class="sxs-lookup"><span data-stu-id="163d5-179">An option to be prompted when the first package is installed in a project is also available.</span></span>

> [!Note]
> <span data-ttu-id="163d5-180">如果專案不支援這兩種套件管理格式，則使用的套件管理格式會與專案相容，因此可能不是選項中的預設設定。</span><span class="sxs-lookup"><span data-stu-id="163d5-180">If a project does not support both package management formats, the package management format used will be the one that's compatible with the project, and therefore may not be the default set in the options.</span></span> <span data-ttu-id="163d5-181">此外，即使在 [選項] 視窗中選取選項，NuGet 也不會在第一次套件安裝時提示您選取。</span><span class="sxs-lookup"><span data-stu-id="163d5-181">Additionally, NuGet will not prompt for selection on first package installation, even if the option is selected in the options window.</span></span>
>
> <span data-ttu-id="163d5-182">如果使用 [套件管理員主控台] 來安裝專案中的第一個套件，即使在 [選項] 視窗中選取選項，NuGet 也不會提示您選取格式。</span><span class="sxs-lookup"><span data-stu-id="163d5-182">If Package Manager Console is used to install the first package in a project, NuGet will not prompt for format selection, even if the option is selected in the options window.</span></span>

## <a name="restore-using-the-dotnet-cli"></a><span data-ttu-id="163d5-183">使用 dotnet CLI 進行還原</span><span class="sxs-lookup"><span data-stu-id="163d5-183">Restore using the dotnet CLI</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="163d5-184">若要將遺漏的套件參考新增至專案檔，請使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)，這也會執行 `restore` 命令。</span><span class="sxs-lookup"><span data-stu-id="163d5-184">To add a missing package reference to the project file, use [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), which also runs the `restore` command.</span></span>

## <a name="restore-using-the-nugetexe-cli"></a><span data-ttu-id="163d5-185">使用 nuget.exe CLI 進行還原</span><span class="sxs-lookup"><span data-stu-id="163d5-185">Restore using the nuget.exe CLI</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="163d5-186">`restore`命令不會修改專案檔或*封裝 .config*。若要新增相依性，請在 Visual Studio 中透過套件管理員 UI 或主控台新增封裝，*或修改 package，然後*執行 `install` 或 `restore`。</span><span class="sxs-lookup"><span data-stu-id="163d5-186">The `restore`command does not modify a project file or *packages.config*. To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

## <a name="restore-using-msbuild"></a><span data-ttu-id="163d5-187">使用 MSBuild 進行還原</span><span class="sxs-lookup"><span data-stu-id="163d5-187">Restore using MSBuild</span></span>

<span data-ttu-id="163d5-188">若要使用 PackageReference 來還原專案檔中所列的套件，請使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令。</span><span class="sxs-lookup"><span data-stu-id="163d5-188">To restore packages listed in the project file with PackageReference, use the the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command.</span></span> <span data-ttu-id="163d5-189">這個命令只適用於 NuGet 4.x+ 和 MSBuild 15.1+ (兩者均隨附於 Visual Studio 2017 和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="163d5-189">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="163d5-190">`nuget restore` 和 `dotnet restore` 都會將這個命令用於適用的專案。</span><span class="sxs-lookup"><span data-stu-id="163d5-190">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

1. <span data-ttu-id="163d5-191">開啟開發人員命令提示字元 (在 [搜尋] 方塊中，輸入**開發人員命令提示字元**)。</span><span class="sxs-lookup"><span data-stu-id="163d5-191">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="163d5-192">您通常想要從 [開始] 功能表啟動適用於 Visual Studio 的開發人員命令提示字元，因為它將使用適用於 MSBuild 的所有必要路徑來設定。</span><span class="sxs-lookup"><span data-stu-id="163d5-192">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

2. <span data-ttu-id="163d5-193">切換至包含專案檔的資料夾，並輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="163d5-193">Switch to the folder containing the project file and type the following command.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. <span data-ttu-id="163d5-194">輸入下列命令以重建專案。</span><span class="sxs-lookup"><span data-stu-id="163d5-194">Type the following command to rebuild the project.</span></span>

   ```cmd
   msbuild
   ```

   <span data-ttu-id="163d5-195">確定 MSBuild 輸出會指出組建已順利完成。</span><span class="sxs-lookup"><span data-stu-id="163d5-195">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="restore-using-azure-pipelines"></a><span data-ttu-id="163d5-196">使用 Azure Pipelines 進行還原</span><span class="sxs-lookup"><span data-stu-id="163d5-196">Restore using Azure Pipelines</span></span>

<span data-ttu-id="163d5-197">在 Azure Pipelines 中建立組建定義時，在定義中於任何建置工作之前包含 NuGet [還原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)或 .NET Core [還原](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops)工作。</span><span class="sxs-lookup"><span data-stu-id="163d5-197">When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="163d5-198">根據預設，一些建置範本已包含還原工作。</span><span class="sxs-lookup"><span data-stu-id="163d5-198">Some build templates include the restore task by default.</span></span>

## <a name="restore-using-azure-devops-server"></a><span data-ttu-id="163d5-199">使用 Azure DevOps Server 進行還原</span><span class="sxs-lookup"><span data-stu-id="163d5-199">Restore using Azure DevOps Server</span></span>

<span data-ttu-id="163d5-200">Azure DevOps Server 和 TFS 2013 及更新版本會在建置期間自動還原套件，前提是您使用 TFS 2013 或更新版本的 Team Build 範本。</span><span class="sxs-lookup"><span data-stu-id="163d5-200">Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="163d5-201">針對較舊的 TFS 版本，您可以包含一個建置步驟來執行命令列還原選項，或選擇性地將建置範本移轉至較新版本。</span><span class="sxs-lookup"><span data-stu-id="163d5-201">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="163d5-202">如需詳細資訊，請參閱[使用 Team Foundation Build 的套件還原設定](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-202">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="163d5-203">使用還原來限制套件版本</span><span class="sxs-lookup"><span data-stu-id="163d5-203">Constrain package versions with restore</span></span>

<span data-ttu-id="163d5-204">NuGet 透過任何方法還原套件時，會使用 `packages.config` 或專案檔中所指定的任何條件約束：</span><span class="sxs-lookup"><span data-stu-id="163d5-204">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="163d5-205">在 `packages.config` 中，您可以在相依性的 `allowedVersion` 屬性中指定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="163d5-205">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="163d5-206">如需詳細資訊，請參閱[限制升級版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="163d5-206">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="163d5-207">例如，</span><span class="sxs-lookup"><span data-stu-id="163d5-207">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="163d5-208">在專案檔中，您可以使用 PackageReference 來直接指定相依性的範圍。</span><span class="sxs-lookup"><span data-stu-id="163d5-208">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="163d5-209">例如，</span><span class="sxs-lookup"><span data-stu-id="163d5-209">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="163d5-210">在所有情況下，都請使用[套件版本控制](../concepts/package-versioning.md)中所述的標記法。</span><span class="sxs-lookup"><span data-stu-id="163d5-210">In all cases, use the notation described in [Package versioning](../concepts/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="163d5-211">強制從套件來源還原</span><span class="sxs-lookup"><span data-stu-id="163d5-211">Force restore from package sources</span></span>

<span data-ttu-id="163d5-212">根據預設，NuGet 還原作業會使用來自 *global-packages* 和 *http-cache* 資料夾的套件，這在[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中有描述。</span><span class="sxs-lookup"><span data-stu-id="163d5-212">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="163d5-213">若要避免使用 *global-packages* 資料夾，請執行下列任一步驟：</span><span class="sxs-lookup"><span data-stu-id="163d5-213">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="163d5-214">使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除資料夾。</span><span class="sxs-lookup"><span data-stu-id="163d5-214">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="163d5-215">使用下列其中一種方法，在還原作業之前暫時變更 *global-packages* 資料夾的位置：</span><span class="sxs-lookup"><span data-stu-id="163d5-215">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="163d5-216">將 NUGET_PACKAGES 環境變數設定為不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="163d5-216">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="163d5-217">建立將 `NuGet.Config` (如果使用 PackageReference) 或 `globalPackagesFolder` (如果使用 `repositoryPath`) 設定為不同資料夾的 `packages.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="163d5-217">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="163d5-218">如需詳細資訊，請參閱[組態設定](../reference/nuget-config-file.md#config-section)。</span><span class="sxs-lookup"><span data-stu-id="163d5-218">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="163d5-219">僅限 MSBuild：指定具有 `RestorePackagesPath` 屬性的不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="163d5-219">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="163d5-220">若要避免使用 HTTP 來源的快取，請執行下列任一步驟：</span><span class="sxs-lookup"><span data-stu-id="163d5-220">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="163d5-221">使用 `-NoCache` 選項搭配 `nuget restore`，或 `--no-cache` 選項搭配 `dotnet restore`。</span><span class="sxs-lookup"><span data-stu-id="163d5-221">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="163d5-222">這些選項不會影響透過 Visual Studio 套件管理員或主控台進行的還原作業。</span><span class="sxs-lookup"><span data-stu-id="163d5-222">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="163d5-223">使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear`清除快取。</span><span class="sxs-lookup"><span data-stu-id="163d5-223">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="163d5-224">暫時將 NUGET_HTTP_CACHE_PATH 環境變數設定為不同資料夾。</span><span class="sxs-lookup"><span data-stu-id="163d5-224">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="163d5-225">遷移至自動套件還原 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="163d5-225">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="163d5-226">針對 NuGet 2.6 和更早版本，先前支援的 MSBuild 整合套件還原已不再適用。</span><span class="sxs-lookup"><span data-stu-id="163d5-226">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="163d5-227">(通常是在 Visual Studio 中以滑鼠右鍵按一下解決方案，然後選取 [啟用 NuGet 套件還原] 來啟用)。</span><span class="sxs-lookup"><span data-stu-id="163d5-227">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="163d5-228">如果您的專案是使用整合 MSBuild 套件還原，請遷移至自動套件還原。</span><span class="sxs-lookup"><span data-stu-id="163d5-228">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="163d5-229">使用 MSBuild 整合套件還原的專案通常會包含包含三個檔案的*nuget.exe*資料夾： *nuget.exe*、 *nuget.exe*和*nuget.exe*。</span><span class="sxs-lookup"><span data-stu-id="163d5-229">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="163d5-230">*NuGet.targets* 檔案的存在會決定 NuGet 是否繼續使用整合 MSBuild 方法，所以進行遷移時必須移除該檔案。</span><span class="sxs-lookup"><span data-stu-id="163d5-230">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="163d5-231">若要遷移至自動套件還原：</span><span class="sxs-lookup"><span data-stu-id="163d5-231">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="163d5-232">關閉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="163d5-232">Close Visual Studio.</span></span>
2. <span data-ttu-id="163d5-233">刪除 *.nuget/nuget.exe* 和 *.nuget/NuGet.targets*。</span><span class="sxs-lookup"><span data-stu-id="163d5-233">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="163d5-234">針對每個專案檔，移除 `<RestorePackages>` 元素，並移除任何對 *NuGet.targets* 的參考。</span><span class="sxs-lookup"><span data-stu-id="163d5-234">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="163d5-235">若要測試自動套件還原：</span><span class="sxs-lookup"><span data-stu-id="163d5-235">To test the automatic package restore:</span></span>

1. <span data-ttu-id="163d5-236">將 [packages] 資料夾從解決方案中移除。</span><span class="sxs-lookup"><span data-stu-id="163d5-236">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="163d5-237">在 Visual Studio 中開啟方案，並啟動建置。</span><span class="sxs-lookup"><span data-stu-id="163d5-237">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="163d5-238">自動套件還原應該會下載並安裝每個相依性套件，而不會將他們新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="163d5-238">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="163d5-239">疑難排解</span><span class="sxs-lookup"><span data-stu-id="163d5-239">Troubleshooting</span></span>

<span data-ttu-id="163d5-240">請參閱[針對套件還原進行疑難排解](package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="163d5-240">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
