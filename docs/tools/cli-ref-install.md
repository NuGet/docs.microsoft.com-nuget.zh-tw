---
title: NuGet CLI 安裝命令
description: Nuget.exe install 命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e609b01bc14083ce212f6d4d4c6d3412f0ee316b
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508318"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="52057-103">install 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="52057-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="52057-104">**適用於：** 套件耗用量&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="52057-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="52057-105">下載並安裝至專案時，預設為目前的資料夾中，使用指定的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="52057-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="52057-106">若要下載封裝，以直接在專案的內容之外，請瀏覽套件頁面上[nuget.org](https://www.nuget.org) ，然後選取**下載**連結。</span><span class="sxs-lookup"><span data-stu-id="52057-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="52057-107">如果未不指定任何來源，所列在 全域設定檔中， `%appdata%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，會使用。</span><span class="sxs-lookup"><span data-stu-id="52057-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="52057-108">請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="52057-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="52057-109">如果未不指定任何特定的套件，`install`會安裝在專案中所列出的所有套件`packages.config`檔案，讓它變成類似[ `restore` ](cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="52057-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="52057-110">`install`命令不會修改專案檔或`packages.config`; 如此一來，類似於`restore`，因為它只會將套件新增至磁碟，但不會變更專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="52057-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="52057-111">若要加入相依性，請在 Visual Studio 中，新增套件，以透過套件管理員 UI 或主控台，或是修改`packages.config`，然後執行`install`或`restore`。</span><span class="sxs-lookup"><span data-stu-id="52057-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="52057-112">使用量</span><span class="sxs-lookup"><span data-stu-id="52057-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="52057-113">何處`<packageID>`名稱來安裝 （使用最新版本），或`<configFilePath>`識別`packages.config`檔案，其中列出要安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="52057-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="52057-114">您可以指定特定版本`-Version`選項。</span><span class="sxs-lookup"><span data-stu-id="52057-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="52057-115">選項</span><span class="sxs-lookup"><span data-stu-id="52057-115">Options</span></span>

| <span data-ttu-id="52057-116">選項</span><span class="sxs-lookup"><span data-stu-id="52057-116">Option</span></span> | <span data-ttu-id="52057-117">描述</span><span class="sxs-lookup"><span data-stu-id="52057-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52057-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="52057-118">ConfigFile</span></span> | <span data-ttu-id="52057-119">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="52057-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="52057-120">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="52057-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="52057-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="52057-121">DependencyVersion</span></span> | <span data-ttu-id="52057-122">*（4.4 +)* 的相依性套件使用，它可以是下列其中一種版本：</span><span class="sxs-lookup"><span data-stu-id="52057-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="52057-123">*最低*（預設值）： 最低版本</span><span class="sxs-lookup"><span data-stu-id="52057-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="52057-124">*HighestPatch*： 具有最低的主要、 次要最低、 最高的修補程式版本</span><span class="sxs-lookup"><span data-stu-id="52057-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="52057-125">*HighestMinor*： 具有最低的主要版本、 最小、 最高的修補程式</span><span class="sxs-lookup"><span data-stu-id="52057-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="52057-126">*最高*： 最高版本</span><span class="sxs-lookup"><span data-stu-id="52057-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="52057-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="52057-127">DisableParallelProcessing</span></span> | <span data-ttu-id="52057-128">安裝多個封裝，以平行方式停用。</span><span class="sxs-lookup"><span data-stu-id="52057-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="52057-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="52057-129">ExcludeVersion</span></span> | <span data-ttu-id="52057-130">安裝封裝到資料夾，名為封裝名稱和版本號碼。</span><span class="sxs-lookup"><span data-stu-id="52057-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="52057-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="52057-131">FallbackSource</span></span> | <span data-ttu-id="52057-132">*（3.2 +)* 作為後援，以防主要中找不到封裝的封裝來源清單或預設來源。</span><span class="sxs-lookup"><span data-stu-id="52057-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="52057-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="52057-133">ForceEnglishOutput</span></span> | <span data-ttu-id="52057-134">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="52057-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="52057-135">架構</span><span class="sxs-lookup"><span data-stu-id="52057-135">Framework</span></span> | <span data-ttu-id="52057-136">*（4.4 +)* 用於選取相依性的目標 framework。</span><span class="sxs-lookup"><span data-stu-id="52057-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="52057-137">預設值是 'Any' 如果未指定。</span><span class="sxs-lookup"><span data-stu-id="52057-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="52057-138">說明</span><span class="sxs-lookup"><span data-stu-id="52057-138">Help</span></span> | <span data-ttu-id="52057-139">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="52057-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="52057-140">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="52057-140">NoCache</span></span> | <span data-ttu-id="52057-141">禁止 NuGet 使用的快取的套件。</span><span class="sxs-lookup"><span data-stu-id="52057-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="52057-142">請參閱[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="52057-142">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="52057-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="52057-143">NonInteractive</span></span> | <span data-ttu-id="52057-144">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="52057-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="52057-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="52057-145">OutputDirectory</span></span> | <span data-ttu-id="52057-146">指定套件安裝所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="52057-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="52057-147">如果未不指定任何資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="52057-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="52057-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="52057-148">PackageSaveMode</span></span> | <span data-ttu-id="52057-149">指定要在套件安裝之後儲存的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="52057-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="52057-150">發行前版本</span><span class="sxs-lookup"><span data-stu-id="52057-150">PreRelease</span></span> | <span data-ttu-id="52057-151">允許發行前版本套件進行安裝。</span><span class="sxs-lookup"><span data-stu-id="52057-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="52057-152">還原套件時，不需要此旗標`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="52057-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="52057-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="52057-153">RequireConsent</span></span> | <span data-ttu-id="52057-154">確認，然後再下載並安裝封裝中啟用還原套件。</span><span class="sxs-lookup"><span data-stu-id="52057-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="52057-155">如需詳細資訊，請參閱 <<c0> [ 套件還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="52057-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="52057-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="52057-156">SolutionDirectory</span></span> | <span data-ttu-id="52057-157">指定要還原套件解決方案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="52057-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="52057-158">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="52057-158">Source</span></span> | <span data-ttu-id="52057-159">指定封裝來源清單 （Url) 來使用。</span><span class="sxs-lookup"><span data-stu-id="52057-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="52057-160">如果省略，則此命令會使用組態檔中提供的來源，請參閱 <<c0> [ 設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="52057-160">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="52057-161">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="52057-161">Verbosity</span></span> | <span data-ttu-id="52057-162">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="52057-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="52057-163">版本</span><span class="sxs-lookup"><span data-stu-id="52057-163">Version</span></span> | <span data-ttu-id="52057-164">指定要安裝的套件版本。</span><span class="sxs-lookup"><span data-stu-id="52057-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="52057-165">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="52057-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="52057-166">範例</span><span class="sxs-lookup"><span data-stu-id="52057-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
