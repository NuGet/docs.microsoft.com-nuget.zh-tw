---
title: NuGet CLI 更新命令
description: nuget.exe update 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323644"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="302b8-103"> (NuGet CLI 更新命令) </span><span class="sxs-lookup"><span data-stu-id="302b8-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="302b8-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="302b8-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="302b8-105">將專案中的所有套件 (使用 `packages.config`) 更新為最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="302b8-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="302b8-106">建議您先執行「 [還原](cli-ref-restore.md) 」，再執行 `update` 。</span><span class="sxs-lookup"><span data-stu-id="302b8-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="302b8-107"> (若要更新個別套件，請使用 [`nuget install`](cli-ref-install.md) 但不指定版本號碼，在此情況下，NuGet 會安裝最新版本。 ) </span><span class="sxs-lookup"><span data-stu-id="302b8-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="302b8-108">注意： `update` 無法使用在 Mono (MAC OSX 或 Linux) 下執行的 CLI，或使用 PackageReference 格式時。</span><span class="sxs-lookup"><span data-stu-id="302b8-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="302b8-109">此 `update` 命令也會更新專案檔中的元件參考，前提是這些參考已存在。</span><span class="sxs-lookup"><span data-stu-id="302b8-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="302b8-110">如果更新的封裝具有已加入的元件，則 *不* 會加入新的參考。</span><span class="sxs-lookup"><span data-stu-id="302b8-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="302b8-111">新的封裝相依性也不會新增其元件參考。</span><span class="sxs-lookup"><span data-stu-id="302b8-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="302b8-112">若要在更新過程中包含這些作業，請使用封裝管理員 UI 或封裝管理員主控台更新 Visual Studio 中的套件。</span><span class="sxs-lookup"><span data-stu-id="302b8-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="302b8-113">此命令也可以用來使用 *-self* 旗標來更新 nuget.exe 本身。</span><span class="sxs-lookup"><span data-stu-id="302b8-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="302b8-114">使用方式</span><span class="sxs-lookup"><span data-stu-id="302b8-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="302b8-115">其中 `<configPath>` 會識別列出專案相依性的 `packages.config` 或方案檔。</span><span class="sxs-lookup"><span data-stu-id="302b8-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="302b8-116">選項</span><span class="sxs-lookup"><span data-stu-id="302b8-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="302b8-117">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="302b8-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="302b8-118">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="302b8-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="302b8-119">指定要使用之相依性套件的版本，它可以是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="302b8-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="302b8-120">*最低* (預設) ：最低版本</span><span class="sxs-lookup"><span data-stu-id="302b8-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="302b8-121">*HighestPatch*：最低主要、最低次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="302b8-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="302b8-122">*HighestMinor*：最低主要、最小次要、最高修補程式的版本</span><span class="sxs-lookup"><span data-stu-id="302b8-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="302b8-123">*最高*：最高版本</span><span class="sxs-lookup"><span data-stu-id="302b8-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="302b8-124">*略* 過：將不會使用任何相依性套件</span><span class="sxs-lookup"><span data-stu-id="302b8-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="302b8-125">當封裝中的檔案已經存在於目標專案時，指定預設動作。</span><span class="sxs-lookup"><span data-stu-id="302b8-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="302b8-126">設定為 [ `Overwrite` 永遠覆寫檔案]。</span><span class="sxs-lookup"><span data-stu-id="302b8-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="302b8-127">設定為 `Ignore` 以略過檔案。</span><span class="sxs-lookup"><span data-stu-id="302b8-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="302b8-128">`PromptUser`除非提供或，否則動作（預設值）會提示您輸入每個衝突的檔案 `OverwriteAll` `IgnoreAll` ，這些檔案將會套用到所有剩餘的檔案。</span><span class="sxs-lookup"><span data-stu-id="302b8-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="302b8-129">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="302b8-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="302b8-130">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="302b8-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="302b8-131">指定要更新之套件識別碼的清單。</span><span class="sxs-lookup"><span data-stu-id="302b8-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="302b8-132">*(4.0 +)* 指定要搭配命令使用的 MSBuild 路徑，優先順序高於 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="302b8-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="302b8-133">*(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="302b8-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="302b8-134">支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="302b8-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="302b8-135">依預設，會挑選路徑中的 MSBuild，否則會預設為 MSBuild 的最高安裝版本。</span><span class="sxs-lookup"><span data-stu-id="302b8-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="302b8-136">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="302b8-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="302b8-137">允許更新為發行前版本。</span><span class="sxs-lookup"><span data-stu-id="302b8-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="302b8-138">更新已安裝的發行前版本套件時，不需要此旗標。</span><span class="sxs-lookup"><span data-stu-id="302b8-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="302b8-139">指定安裝封裝的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="302b8-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="302b8-140">指定在安裝套件的主要和次要版本中，只會安裝具有最高版本的更新。</span><span class="sxs-lookup"><span data-stu-id="302b8-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="302b8-141">`nuget.exe`最新版本的更新。</span><span class="sxs-lookup"><span data-stu-id="302b8-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="302b8-142">`-Source` 可以使用，但會忽略所有其他引數。</span><span class="sxs-lookup"><span data-stu-id="302b8-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="302b8-143">如果未提供任何來源，則會檢查是否 `nuget.org` 有更新，不論 `NuGet.Config` 設定為何。</span><span class="sxs-lookup"><span data-stu-id="302b8-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="302b8-144">指定要用於更新的 Url)  (套件來源的清單。</span><span class="sxs-lookup"><span data-stu-id="302b8-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="302b8-145">如果省略，此命令會使用設定檔中提供的來源，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="302b8-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="302b8-146">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="302b8-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="302b8-147">與一個封裝識別碼搭配使用時，會指定要更新的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="302b8-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="302b8-148">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="302b8-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="302b8-149">範例</span><span class="sxs-lookup"><span data-stu-id="302b8-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
