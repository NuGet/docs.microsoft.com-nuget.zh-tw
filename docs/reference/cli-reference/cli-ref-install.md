---
title: NuGet CLI 安裝命令
description: nuget.exe install 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779263"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="66188-103"> (NuGet CLI 安裝命令) </span><span class="sxs-lookup"><span data-stu-id="66188-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="66188-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="66188-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="66188-105">使用指定的套件來源，將套件下載並安裝到專案中，預設為目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="66188-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="66188-106">若要直接在專案內容外下載套件，請造訪套件在 [nuget.org](https://www.nuget.org) 上的頁面，然後選取 **下載** 連結。</span><span class="sxs-lookup"><span data-stu-id="66188-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="66188-107">如果未指定任何來源，則會使用全域設定檔中所列的 `%appdata%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="66188-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="66188-108">如需其他詳細資料，請參閱 [常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md) 設定。</span><span class="sxs-lookup"><span data-stu-id="66188-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="66188-109">如果未指定特定的封裝，則會 `install` 安裝專案檔案中列出的所有套件 `packages.config` ，使其類似 [`restore`](cli-ref-restore.md) 。</span><span class="sxs-lookup"><span data-stu-id="66188-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="66188-110">此 `install` 命令不會修改專案檔，或者， `packages.config` 它類似于 `restore` ，它只會將套件新增至磁片，但不會變更專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="66188-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="66188-111">若要加入相依性，請在 Visual Studio 中透過封裝管理員 UI 或主控台加入封裝，或修改 `packages.config` 然後執行 `install` 或 `restore` 。</span><span class="sxs-lookup"><span data-stu-id="66188-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="66188-112">使用方式</span><span class="sxs-lookup"><span data-stu-id="66188-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="66188-113">`<packageID>`使用最新版本) 將套件命名為安裝 (，或 `<configFilePath>` 識別 `packages.config` 列出要安裝之套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="66188-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="66188-114">您可以使用選項來指出特定版本 `-Version` 。</span><span class="sxs-lookup"><span data-stu-id="66188-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="66188-115">選項。</span><span class="sxs-lookup"><span data-stu-id="66188-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="66188-116">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="66188-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="66188-117">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="66188-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="66188-118">*(4.4 +)* 要使用之相依性套件的版本，它可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="66188-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="66188-119">*最低* (預設) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="66188-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="66188-120">*HighestPatch*：最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="66188-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="66188-121">*HighestMinor*：最低主要、最小次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="66188-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="66188-122">*最高*：最高版本</span><span class="sxs-lookup"><span data-stu-id="66188-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="66188-123">*略* 過：將不會使用任何相依性套件</span><span class="sxs-lookup"><span data-stu-id="66188-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="66188-124">直接下載，但不填入任何具有中繼資料或二進位檔的快取。</span><span class="sxs-lookup"><span data-stu-id="66188-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="66188-125">停用平行安裝多個套件。</span><span class="sxs-lookup"><span data-stu-id="66188-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="66188-126">將套件安裝至僅具有套件名稱的資料夾，而不是版本號碼。</span><span class="sxs-lookup"><span data-stu-id="66188-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="66188-127">*(3.2 +)* 在主要或預設來源中找不到封裝時，用來做為回盒的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="66188-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="66188-128">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="66188-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="66188-129">*(4.4 +)* 用來選取相依性的目標架構。</span><span class="sxs-lookup"><span data-stu-id="66188-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="66188-130">如果未指定，則預設為 ' Any '。</span><span class="sxs-lookup"><span data-stu-id="66188-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="66188-131">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="66188-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="66188-132">防止 NuGet 使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="66188-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="66188-133">請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="66188-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="66188-134">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="66188-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="66188-135">指定安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="66188-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="66188-136">如果未指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="66188-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="66188-137">指定封裝安裝之後要儲存的檔案類型：、或的其中一個 `nuspec` `nupkg` `nuspec;nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="66188-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="66188-138">允許安裝發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="66188-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="66188-139">使用還原封裝時，不需要此旗標 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="66188-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="66188-140">確認在下載及安裝封裝之前，已啟用還原的封裝。</span><span class="sxs-lookup"><span data-stu-id="66188-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="66188-141">如需詳細資訊，請參閱 [封裝還原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="66188-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="66188-142">指定要還原封裝之方案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="66188-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="66188-143">指定) 要使用的 Url (套件來源的清單。</span><span class="sxs-lookup"><span data-stu-id="66188-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="66188-144">如果省略，此命令會使用設定檔中提供的來源，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="66188-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="66188-145">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="66188-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="66188-146">指定要安裝的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="66188-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="66188-147">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="66188-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="66188-148">範例</span><span class="sxs-lookup"><span data-stu-id="66188-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
