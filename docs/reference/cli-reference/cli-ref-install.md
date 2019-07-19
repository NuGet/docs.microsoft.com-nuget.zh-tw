---
title: NuGet CLI 安裝命令
description: Nuget.exe install 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327785"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="d29b4-103">install 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d29b4-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="d29b4-104">**適用于:** 套件耗&bullet;用量**支援的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="d29b4-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d29b4-105">使用指定的套件來源, 將套件下載並安裝到專案中, 並預設為目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d29b4-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="d29b4-106">若要直接在專案內容之外下載套件, 請流覽[nuget.org](https://www.nuget.org)上的套件頁面, 然後選取 [**下載**] 連結。</span><span class="sxs-lookup"><span data-stu-id="d29b4-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="d29b4-107">如果未指定任何來源, 則會使用全域設定檔`%appdata%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 中所列的來源。</span><span class="sxs-lookup"><span data-stu-id="d29b4-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="d29b4-108">如需其他詳細資料, 請參閱[常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="d29b4-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="d29b4-109">如果未指定特定套件, `install`會安裝`packages.config`專案檔案中列出的所有套件[`restore`](cli-ref-restore.md), 使其類似。</span><span class="sxs-lookup"><span data-stu-id="d29b4-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="d29b4-110">此命令不會修改專案檔或`packages.config`, 其`restore`方式類似于, 因為它只會將套件新增至磁片, 但不會變更專案的相依性。 `install`</span><span class="sxs-lookup"><span data-stu-id="d29b4-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="d29b4-111">若要新增相依性, 請在 Visual Studio 中透過套件管理員 UI 或主控台新增封裝, 或修改`packages.config` , 然後`install`執行或`restore`。</span><span class="sxs-lookup"><span data-stu-id="d29b4-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="d29b4-112">使用量</span><span class="sxs-lookup"><span data-stu-id="d29b4-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="d29b4-113">其中`<packageID>`的名稱是要安裝的封裝 (使用最新版本) `<configFilePath>` , 或`packages.config`識別列出要安裝之套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="d29b4-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="d29b4-114">您可以使用`-Version`選項來指定特定版本。</span><span class="sxs-lookup"><span data-stu-id="d29b4-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="d29b4-115">選項</span><span class="sxs-lookup"><span data-stu-id="d29b4-115">Options</span></span>

| <span data-ttu-id="d29b4-116">選項</span><span class="sxs-lookup"><span data-stu-id="d29b4-116">Option</span></span> | <span data-ttu-id="d29b4-117">描述</span><span class="sxs-lookup"><span data-stu-id="d29b4-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d29b4-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d29b4-118">ConfigFile</span></span> | <span data-ttu-id="d29b4-119">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="d29b4-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d29b4-120">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="d29b4-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d29b4-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="d29b4-121">DependencyVersion</span></span> | <span data-ttu-id="d29b4-122">*(4.4 +)* 要使用的相依性套件版本, 它可以是下列其中一項:</span><span class="sxs-lookup"><span data-stu-id="d29b4-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="d29b4-123">*最低*(預設值): 最低版本</span><span class="sxs-lookup"><span data-stu-id="d29b4-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="d29b4-124">*HighestPatch*: 具有最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="d29b4-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="d29b4-125">*HighestMinor*: 具有最低主要、最高次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="d29b4-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="d29b4-126">*最高*: 最高版本</span><span class="sxs-lookup"><span data-stu-id="d29b4-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="d29b4-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="d29b4-127">DisableParallelProcessing</span></span> | <span data-ttu-id="d29b4-128">停用平行安裝多個套件。</span><span class="sxs-lookup"><span data-stu-id="d29b4-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="d29b4-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="d29b4-129">ExcludeVersion</span></span> | <span data-ttu-id="d29b4-130">將套件安裝到名為的資料夾, 只包含套件名稱, 而不是版本號碼。</span><span class="sxs-lookup"><span data-stu-id="d29b4-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="d29b4-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="d29b4-131">FallbackSource</span></span> | <span data-ttu-id="d29b4-132">*(3.2 +)* 在主要或預設來源中找不到封裝時, 用來做為回退的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="d29b4-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="d29b4-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d29b4-133">ForceEnglishOutput</span></span> | <span data-ttu-id="d29b4-134">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="d29b4-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d29b4-135">架構</span><span class="sxs-lookup"><span data-stu-id="d29b4-135">Framework</span></span> | <span data-ttu-id="d29b4-136">*(4.4 +)* 用來選取相依性的目標架構。</span><span class="sxs-lookup"><span data-stu-id="d29b4-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="d29b4-137">如果未指定, 則預設為「任何」。</span><span class="sxs-lookup"><span data-stu-id="d29b4-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="d29b4-138">Help</span><span class="sxs-lookup"><span data-stu-id="d29b4-138">Help</span></span> | <span data-ttu-id="d29b4-139">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="d29b4-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="d29b4-140">NoCache</span><span class="sxs-lookup"><span data-stu-id="d29b4-140">NoCache</span></span> | <span data-ttu-id="d29b4-141">防止 NuGet 使用快取的套件。</span><span class="sxs-lookup"><span data-stu-id="d29b4-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="d29b4-142">請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="d29b4-142">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="d29b4-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d29b4-143">NonInteractive</span></span> | <span data-ttu-id="d29b4-144">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="d29b4-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d29b4-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="d29b4-145">OutputDirectory</span></span> | <span data-ttu-id="d29b4-146">指定安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d29b4-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="d29b4-147">如果未指定任何資料夾, 則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d29b4-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="d29b4-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="d29b4-148">PackageSaveMode</span></span> | <span data-ttu-id="d29b4-149">指定封裝安裝後要儲存的檔案類型: `nuspec`、 `nupkg`或`nuspec;nupkg`其中之一。</span><span class="sxs-lookup"><span data-stu-id="d29b4-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="d29b4-150">版</span><span class="sxs-lookup"><span data-stu-id="d29b4-150">PreRelease</span></span> | <span data-ttu-id="d29b4-151">允許安裝發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="d29b4-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="d29b4-152">使用`packages.config`還原套件時, 不需要此旗標。</span><span class="sxs-lookup"><span data-stu-id="d29b4-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="d29b4-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="d29b4-153">RequireConsent</span></span> | <span data-ttu-id="d29b4-154">確認在下載並安裝封裝之前, 已啟用還原封裝。</span><span class="sxs-lookup"><span data-stu-id="d29b4-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="d29b4-155">如需詳細資訊, 請參閱[套件還原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="d29b4-155">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="d29b4-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="d29b4-156">SolutionDirectory</span></span> | <span data-ttu-id="d29b4-157">指定要還原封裝之方案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="d29b4-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="d29b4-158">Source</span><span class="sxs-lookup"><span data-stu-id="d29b4-158">Source</span></span> | <span data-ttu-id="d29b4-159">指定要使用的套件來源清單 (如 Url)。</span><span class="sxs-lookup"><span data-stu-id="d29b4-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="d29b4-160">如果省略, 此命令會使用設定檔中提供的來源, 請參閱[一般的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="d29b4-160">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="d29b4-161">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d29b4-161">Verbosity</span></span> | <span data-ttu-id="d29b4-162">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="d29b4-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="d29b4-163">版本</span><span class="sxs-lookup"><span data-stu-id="d29b4-163">Version</span></span> | <span data-ttu-id="d29b4-164">指定要安裝的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="d29b4-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="d29b4-165">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d29b4-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d29b4-166">範例</span><span class="sxs-lookup"><span data-stu-id="d29b4-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
