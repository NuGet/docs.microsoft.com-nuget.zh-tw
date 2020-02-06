---
title: NuGet CLI 安裝命令
description: Nuget.exe install 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036938"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="4dbb4-103">安裝命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="4dbb4-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="4dbb4-104">**適用物件：** 套件耗用量 &bullet;**支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="4dbb4-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4dbb4-105">使用指定的套件來源，將套件下載並安裝到專案中，並預設為目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="4dbb4-106">若要直接在專案內容之外下載套件，請流覽[nuget.org](https://www.nuget.org)上的套件頁面，然後選取 [**下載**] 連結。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="4dbb4-107">如果未指定任何來源，則會使用全域設定檔中所列的 `%appdata%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="4dbb4-108">如需其他詳細資料，請參閱[常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="4dbb4-109">如果未指定特定的封裝，`install` 會安裝專案的 `packages.config` 檔案中列出的所有套件，使其類似于[`restore`](cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="4dbb4-110">`install` 命令不會修改專案檔或 `packages.config`;如此一來，它就類似于 `restore`，因為它只會將套件新增至磁片，但不會變更專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="4dbb4-111">若要新增相依性，請在 Visual Studio 中透過套件管理員 UI 或主控台新增封裝，或修改 `packages.config` 然後執行 `install` 或 `restore`。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="4dbb4-112">使用方式</span><span class="sxs-lookup"><span data-stu-id="4dbb4-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="4dbb4-113">其中 `<packageID>` 為要安裝的套件命名（使用最新版本），或 `<configFilePath>` 識別列出要安裝之套件的 `packages.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="4dbb4-114">您可以使用 `-Version` 選項來指定特定版本。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="4dbb4-115">選項</span><span class="sxs-lookup"><span data-stu-id="4dbb4-115">Options</span></span>

| <span data-ttu-id="4dbb4-116">選項</span><span class="sxs-lookup"><span data-stu-id="4dbb4-116">Option</span></span> | <span data-ttu-id="4dbb4-117">描述</span><span class="sxs-lookup"><span data-stu-id="4dbb4-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4dbb4-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4dbb4-118">ConfigFile</span></span> | <span data-ttu-id="4dbb4-119">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4dbb4-120">如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4dbb4-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="4dbb4-121">DependencyVersion</span></span> | <span data-ttu-id="4dbb4-122">*（4.4 +）* 要使用的相依性套件版本，它可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="4dbb4-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="4dbb4-123">*最低*（預設值）：最低版本</span><span class="sxs-lookup"><span data-stu-id="4dbb4-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="4dbb4-124">*HighestPatch*：具有最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="4dbb4-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="4dbb4-125">*HighestMinor*：具有最低主要、最高次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="4dbb4-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="4dbb4-126">*最高*：最高版本</span><span class="sxs-lookup"><span data-stu-id="4dbb4-126">*Highest*: the highest version</span></span></li><li><span data-ttu-id="4dbb4-127">*忽略*：不會使用任何相依性套件</span><span class="sxs-lookup"><span data-stu-id="4dbb4-127">*Ignore*: No dependency packages will be used</span></span></li></ul> |
| <span data-ttu-id="4dbb4-128">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="4dbb4-128">DisableParallelProcessing</span></span> | <span data-ttu-id="4dbb4-129">停用平行安裝多個套件。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-129">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="4dbb4-130">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="4dbb4-130">ExcludeVersion</span></span> | <span data-ttu-id="4dbb4-131">將套件安裝到名為的資料夾，只包含套件名稱，而不是版本號碼。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-131">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="4dbb4-132">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="4dbb4-132">FallbackSource</span></span> | <span data-ttu-id="4dbb4-133">*（3.2 +）* 在主要或預設來源中找不到封裝時，用來做為回退的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-133">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="4dbb4-134">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4dbb4-134">ForceEnglishOutput</span></span> | <span data-ttu-id="4dbb4-135">*（3.5 +）* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-135">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4dbb4-136">架構</span><span class="sxs-lookup"><span data-stu-id="4dbb4-136">Framework</span></span> | <span data-ttu-id="4dbb4-137">*（4.4 +）* 用來選取相依性的目標架構。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-137">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="4dbb4-138">如果未指定，則預設為「任何」。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-138">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="4dbb4-139">說明</span><span class="sxs-lookup"><span data-stu-id="4dbb4-139">Help</span></span> | <span data-ttu-id="4dbb4-140">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-140">Displays help information for the command.</span></span> |
| <span data-ttu-id="4dbb4-141">NoCache</span><span class="sxs-lookup"><span data-stu-id="4dbb4-141">NoCache</span></span> | <span data-ttu-id="4dbb4-142">防止 NuGet 使用快取的套件。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-142">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="4dbb4-143">請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-143">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="4dbb4-144">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4dbb4-144">NonInteractive</span></span> | <span data-ttu-id="4dbb4-145">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-145">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4dbb4-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="4dbb4-146">OutputDirectory</span></span> | <span data-ttu-id="4dbb4-147">指定安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-147">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="4dbb4-148">如果未指定任何資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="4dbb4-149">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="4dbb4-149">PackageSaveMode</span></span> | <span data-ttu-id="4dbb4-150">指定封裝安裝後要儲存的檔案類型： `nuspec`、`nupkg`或 `nuspec;nupkg`的其中一個。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-150">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="4dbb4-151">PreRelease</span><span class="sxs-lookup"><span data-stu-id="4dbb4-151">PreRelease</span></span> | <span data-ttu-id="4dbb4-152">允許安裝發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-152">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="4dbb4-153">還原具有 `packages.config`的封裝時，不需要此旗標。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-153">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="4dbb4-154">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="4dbb4-154">RequireConsent</span></span> | <span data-ttu-id="4dbb4-155">確認在下載並安裝封裝之前，已啟用還原封裝。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-155">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="4dbb4-156">如需詳細資訊，請參閱[套件還原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-156">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="4dbb4-157">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="4dbb4-157">SolutionDirectory</span></span> | <span data-ttu-id="4dbb4-158">指定要還原封裝之方案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-158">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="4dbb4-159">來源</span><span class="sxs-lookup"><span data-stu-id="4dbb4-159">Source</span></span> | <span data-ttu-id="4dbb4-160">指定要使用的套件來源清單（如 Url）。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-160">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="4dbb4-161">如果省略，此命令會使用設定檔中提供的來源，請參閱[一般的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-161">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="4dbb4-162">詳細程度</span><span class="sxs-lookup"><span data-stu-id="4dbb4-162">Verbosity</span></span> | <span data-ttu-id="4dbb4-163">指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="4dbb4-164">版本</span><span class="sxs-lookup"><span data-stu-id="4dbb4-164">Version</span></span> | <span data-ttu-id="4dbb4-165">指定要安裝的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="4dbb4-165">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="4dbb4-166">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4dbb4-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4dbb4-167">範例</span><span class="sxs-lookup"><span data-stu-id="4dbb4-167">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
