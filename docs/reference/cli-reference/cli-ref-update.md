---
title: NuGet CLI 更新命令
description: Nuget.exe update 命令的參考
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327505"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="afe9e-103">update 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="afe9e-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="afe9e-104">**適用于:** 套件耗&bullet;用量**支援的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="afe9e-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="afe9e-105">將專案中的所有套件 (使用 `packages.config`) 更新為最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="afe9e-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="afe9e-106">建議先執行「[還原](cli-ref-restore.md)」, 然後再`update`執行。</span><span class="sxs-lookup"><span data-stu-id="afe9e-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="afe9e-107">(若要更新個別的封裝, [`nuget install`](cli-ref-install.md)請使用, 而不指定版本號碼, 在此情況下, NuGet 會安裝最新版本)。</span><span class="sxs-lookup"><span data-stu-id="afe9e-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="afe9e-108">注意: `update`不會使用在 Mono (Mac OSX 或 Linux) 下執行的 CLI, 或使用 PackageReference 格式時。</span><span class="sxs-lookup"><span data-stu-id="afe9e-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="afe9e-109">如果`update`參考已經存在, 此命令也會更新專案檔中的元件參考。</span><span class="sxs-lookup"><span data-stu-id="afe9e-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="afe9e-110">如果更新的封裝有已加入的元件, 則*不*會加入新的參考。</span><span class="sxs-lookup"><span data-stu-id="afe9e-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="afe9e-111">新的封裝相依性也不會新增其元件參考。</span><span class="sxs-lookup"><span data-stu-id="afe9e-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="afe9e-112">若要將這些作業納入做為更新的一部分, 請使用套件管理員 UI 或套件管理員主控台, 更新 Visual Studio 中的封裝。</span><span class="sxs-lookup"><span data-stu-id="afe9e-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="afe9e-113">此命令也可以用來使用 *-self* 旗標來更新 nuget.exe 本身。</span><span class="sxs-lookup"><span data-stu-id="afe9e-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="afe9e-114">使用量</span><span class="sxs-lookup"><span data-stu-id="afe9e-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="afe9e-115">其中`<configPath>` , 會識別`packages.config`列出專案相依性的或方案檔。</span><span class="sxs-lookup"><span data-stu-id="afe9e-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="afe9e-116">選項</span><span class="sxs-lookup"><span data-stu-id="afe9e-116">Options</span></span>

| <span data-ttu-id="afe9e-117">選項</span><span class="sxs-lookup"><span data-stu-id="afe9e-117">Option</span></span> | <span data-ttu-id="afe9e-118">描述</span><span class="sxs-lookup"><span data-stu-id="afe9e-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="afe9e-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="afe9e-119">ConfigFile</span></span> | <span data-ttu-id="afe9e-120">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="afe9e-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="afe9e-121">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="afe9e-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="afe9e-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="afe9e-122">FileConflictAction</span></span> | <span data-ttu-id="afe9e-123">指定當系統提示您覆寫或忽略專案所參考的現有檔案時, 所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="afe9e-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="afe9e-124">值為*overwrite、ignore、none*。</span><span class="sxs-lookup"><span data-stu-id="afe9e-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="afe9e-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="afe9e-125">ForceEnglishOutput</span></span> | <span data-ttu-id="afe9e-126">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="afe9e-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="afe9e-127">Help</span><span class="sxs-lookup"><span data-stu-id="afe9e-127">Help</span></span> | <span data-ttu-id="afe9e-128">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="afe9e-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="afe9e-129">ID</span><span class="sxs-lookup"><span data-stu-id="afe9e-129">Id</span></span> | <span data-ttu-id="afe9e-130">指定要更新之套件識別碼的清單。</span><span class="sxs-lookup"><span data-stu-id="afe9e-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="afe9e-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="afe9e-131">MSBuildPath</span></span> | <span data-ttu-id="afe9e-132">*(4.0 +)* 指定要搭配命令使用之 MSBuild 的路徑, 其優先順序高於`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="afe9e-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="afe9e-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="afe9e-133">MSBuildVersion</span></span> | <span data-ttu-id="afe9e-134">*(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="afe9e-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="afe9e-135">支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="afe9e-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="afe9e-136">根據預設, 會挑選路徑中的 MSBuild, 否則會預設為 MSBuild 的最高安裝版本。</span><span class="sxs-lookup"><span data-stu-id="afe9e-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="afe9e-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="afe9e-137">NonInteractive</span></span> | <span data-ttu-id="afe9e-138">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="afe9e-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="afe9e-139">版</span><span class="sxs-lookup"><span data-stu-id="afe9e-139">PreRelease</span></span> | <span data-ttu-id="afe9e-140">允許更新為發行前版本。</span><span class="sxs-lookup"><span data-stu-id="afe9e-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="afe9e-141">更新已安裝的發行前版本套件時, 不需要此旗標。</span><span class="sxs-lookup"><span data-stu-id="afe9e-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="afe9e-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="afe9e-142">RepositoryPath</span></span> | <span data-ttu-id="afe9e-143">指定安裝封裝的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="afe9e-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="afe9e-144">進入</span><span class="sxs-lookup"><span data-stu-id="afe9e-144">Safe</span></span> | <span data-ttu-id="afe9e-145">指定只會安裝與已安裝的封裝在相同的主要和次要版本中可用的最高版本更新。</span><span class="sxs-lookup"><span data-stu-id="afe9e-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="afe9e-146">供電</span><span class="sxs-lookup"><span data-stu-id="afe9e-146">Self</span></span> | <span data-ttu-id="afe9e-147">將 nuget.exe 更新為最新版本;所有其他引數都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="afe9e-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="afe9e-148">Source</span><span class="sxs-lookup"><span data-stu-id="afe9e-148">Source</span></span> | <span data-ttu-id="afe9e-149">指定要用於更新的套件來源清單 (如 Url)。</span><span class="sxs-lookup"><span data-stu-id="afe9e-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="afe9e-150">如果省略, 此命令會使用設定檔中提供的來源, 請參閱[一般的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="afe9e-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="afe9e-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="afe9e-151">Verbosity</span></span> | <span data-ttu-id="afe9e-152">指定輸出中顯示的詳細資料量: [*一般*] 、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="afe9e-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="afe9e-153">版本</span><span class="sxs-lookup"><span data-stu-id="afe9e-153">Version</span></span> | <span data-ttu-id="afe9e-154">與一個封裝識別碼搭配使用時, 會指定要更新的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="afe9e-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="afe9e-155">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="afe9e-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="afe9e-156">範例</span><span class="sxs-lookup"><span data-stu-id="afe9e-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
