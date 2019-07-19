---
title: NuGet CLI 還原命令
description: Nuget.exe restore 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327635"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="6cb89-103">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6cb89-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="6cb89-104">**適用于:** 套件耗&bullet;用量**支援的版本:** 2.7+</span><span class="sxs-lookup"><span data-stu-id="6cb89-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="6cb89-105">下載並安裝資料夾中遺失的`packages`任何套件。</span><span class="sxs-lookup"><span data-stu-id="6cb89-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="6cb89-106">與 NuGet 4.0 + 和 PackageReference 格式搭配使用時, 會`<project>.nuget.props` `obj`在資料夾中產生檔案 (如有需要)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="6cb89-107">(可以從原始檔控制省略檔案)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="6cb89-108">在 Mac OSX 和 Linux 上使用 Mono 的 CLI, PackageReference 不支援還原封裝。</span><span class="sxs-lookup"><span data-stu-id="6cb89-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="6cb89-109">使用量</span><span class="sxs-lookup"><span data-stu-id="6cb89-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="6cb89-110">其中`<projectPath>`指定解決方案`packages.config`或檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="6cb89-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="6cb89-111">如需行為詳細資料, 請參閱下面的[備註](#remarks)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="6cb89-112">選項</span><span class="sxs-lookup"><span data-stu-id="6cb89-112">Options</span></span>

| <span data-ttu-id="6cb89-113">選項</span><span class="sxs-lookup"><span data-stu-id="6cb89-113">Option</span></span> | <span data-ttu-id="6cb89-114">說明</span><span class="sxs-lookup"><span data-stu-id="6cb89-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6cb89-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6cb89-115">ConfigFile</span></span> | <span data-ttu-id="6cb89-116">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="6cb89-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6cb89-117">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6cb89-118">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="6cb89-118">DirectDownload</span></span> | <span data-ttu-id="6cb89-119">*(4.0 +)* 直接下載封裝, 而不需以任何二進位檔或中繼資料填入快取。</span><span class="sxs-lookup"><span data-stu-id="6cb89-119">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="6cb89-120">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="6cb89-120">DisableParallelProcessing</span></span> | <span data-ttu-id="6cb89-121">停用平行還原多個封裝。</span><span class="sxs-lookup"><span data-stu-id="6cb89-121">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="6cb89-122">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="6cb89-122">FallbackSource</span></span> | <span data-ttu-id="6cb89-123">*(3.2 +)* 在主要或預設來源中找不到封裝時, 用來做為回退的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="6cb89-123">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="6cb89-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6cb89-124">ForceEnglishOutput</span></span> | <span data-ttu-id="6cb89-125">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="6cb89-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6cb89-126">Help</span><span class="sxs-lookup"><span data-stu-id="6cb89-126">Help</span></span> | <span data-ttu-id="6cb89-127">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="6cb89-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="6cb89-128">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="6cb89-128">MSBuildPath</span></span> | <span data-ttu-id="6cb89-129">*(4.0 +)* 指定要搭配命令使用之 MSBuild 的路徑, 其優先順序高於`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="6cb89-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="6cb89-130">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="6cb89-130">MSBuildVersion</span></span> | <span data-ttu-id="6cb89-131">*(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="6cb89-131">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="6cb89-132">支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="6cb89-132">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="6cb89-133">根據預設, 會挑選路徑中的 MSBuild, 否則會預設為 MSBuild 的最高安裝版本。</span><span class="sxs-lookup"><span data-stu-id="6cb89-133">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="6cb89-134">NoCache</span><span class="sxs-lookup"><span data-stu-id="6cb89-134">NoCache</span></span> | <span data-ttu-id="6cb89-135">防止 NuGet 使用快取的套件。</span><span class="sxs-lookup"><span data-stu-id="6cb89-135">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="6cb89-136">請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cb89-136">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="6cb89-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6cb89-137">NonInteractive</span></span> | <span data-ttu-id="6cb89-138">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="6cb89-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6cb89-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="6cb89-139">OutputDirectory</span></span> | <span data-ttu-id="6cb89-140">指定安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cb89-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="6cb89-141">如果未指定任何資料夾, 則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cb89-141">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="6cb89-142">使用檔案進行還原時`packages.config` , 除非`PackagesDirectory`使用`SolutionDirectory`或, 否則為必要。</span><span class="sxs-lookup"><span data-stu-id="6cb89-142">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="6cb89-143">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="6cb89-143">PackageSaveMode</span></span> | <span data-ttu-id="6cb89-144">指定封裝安裝後要儲存的檔案類型: `nuspec`、 `nupkg`或`nuspec;nupkg`其中之一。</span><span class="sxs-lookup"><span data-stu-id="6cb89-144">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="6cb89-145">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="6cb89-145">PackagesDirectory</span></span> | <span data-ttu-id="6cb89-146">與 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="6cb89-146">Same as `OutputDirectory`.</span></span> <span data-ttu-id="6cb89-147">使用檔案進行還原時`packages.config` , 除非`OutputDirectory`使用`SolutionDirectory`或, 否則為必要。</span><span class="sxs-lookup"><span data-stu-id="6cb89-147">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="6cb89-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="6cb89-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="6cb89-149">解析專案對專案參考的超時 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="6cb89-150">式</span><span class="sxs-lookup"><span data-stu-id="6cb89-150">Recursive</span></span> | <span data-ttu-id="6cb89-151">*(4.0 +)* 還原 UWP 和 .NET Core 專案的所有參考專案。</span><span class="sxs-lookup"><span data-stu-id="6cb89-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="6cb89-152">不適用於使用`packages.config`的專案。</span><span class="sxs-lookup"><span data-stu-id="6cb89-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="6cb89-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="6cb89-153">RequireConsent</span></span> | <span data-ttu-id="6cb89-154">確認在下載並安裝封裝之前, 已啟用還原封裝。</span><span class="sxs-lookup"><span data-stu-id="6cb89-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="6cb89-155">如需詳細資訊, 請參閱[套件還原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-155">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="6cb89-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="6cb89-156">SolutionDirectory</span></span> | <span data-ttu-id="6cb89-157">指定解決方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cb89-157">Specifies the solution folder.</span></span> <span data-ttu-id="6cb89-158">還原方案的封裝時無效。</span><span class="sxs-lookup"><span data-stu-id="6cb89-158">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="6cb89-159">使用檔案進行還原時`packages.config` , 除非`PackagesDirectory`使用`OutputDirectory`或, 否則為必要。</span><span class="sxs-lookup"><span data-stu-id="6cb89-159">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="6cb89-160">Source</span><span class="sxs-lookup"><span data-stu-id="6cb89-160">Source</span></span> | <span data-ttu-id="6cb89-161">指定要用於還原的套件來源清單 (如 Url)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-161">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="6cb89-162">如果省略, 此命令會使用設定檔中提供的來源, 請參閱設定[NuGet 行為](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="6cb89-162">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="6cb89-163">Verbosity</span><span class="sxs-lookup"><span data-stu-id="6cb89-163">Verbosity</span></span> | <span data-ttu-id="6cb89-164">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="6cb89-164">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6cb89-165">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6cb89-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="6cb89-166">備註</span><span class="sxs-lookup"><span data-stu-id="6cb89-166">Remarks</span></span>

<span data-ttu-id="6cb89-167">Restore 命令會執行下列步驟:</span><span class="sxs-lookup"><span data-stu-id="6cb89-167">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="6cb89-168">判斷 restore 命令的操作模式。</span><span class="sxs-lookup"><span data-stu-id="6cb89-168">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="6cb89-169">projectPath 檔案類型</span><span class="sxs-lookup"><span data-stu-id="6cb89-169">projectPath file type</span></span> | <span data-ttu-id="6cb89-170">行為</span><span class="sxs-lookup"><span data-stu-id="6cb89-170">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="6cb89-171">解決方案 (資料夾)</span><span class="sxs-lookup"><span data-stu-id="6cb89-171">Solution (folder)</span></span> | <span data-ttu-id="6cb89-172">NuGet 會尋找`.sln`檔案, 並在找到時使用該檔案, 否則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6cb89-172">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="6cb89-173">`(SolutionDir)\.nuget`會用來做為起始資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cb89-173">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="6cb89-174">`.sln`文字檔</span><span class="sxs-lookup"><span data-stu-id="6cb89-174">`.sln` file</span></span> | <span data-ttu-id="6cb89-175">還原解決方案所識別的套件;如果`-SolutionDirectory`使用, 則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6cb89-175">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="6cb89-176">`$(SolutionDir)\.nuget`會用來做為起始資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cb89-176">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="6cb89-177">`packages.config`或專案檔</span><span class="sxs-lookup"><span data-stu-id="6cb89-177">`packages.config` or project file</span></span> | <span data-ttu-id="6cb89-178">還原檔案中列出的套件、解析和安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="6cb89-178">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="6cb89-179">其他檔案類型</span><span class="sxs-lookup"><span data-stu-id="6cb89-179">Other file type</span></span> | <span data-ttu-id="6cb89-180">檔案會假設`.sln`為上述檔案; 如果不是解決方案, NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="6cb89-180">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="6cb89-181">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="6cb89-181">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="6cb89-182">NuGet 會在目前的資料夾中尋找方案檔。</span><span class="sxs-lookup"><span data-stu-id="6cb89-182">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="6cb89-183">如果找到單一檔案, 則會使用該檔案來還原封裝;如果找到多個解決方案, NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="6cb89-183">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="6cb89-184">如果沒有解決方案檔, NuGet 會尋找`packages.config` , 並使用它來還原套件。</span><span class="sxs-lookup"><span data-stu-id="6cb89-184">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="6cb89-185">如果找不到`packages.config`解決方案或檔案, NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="6cb89-185">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="6cb89-186">使用下列優先順序來判斷套件資料夾 (如果找不到這些資料夾, 則 NuGet 會產生錯誤):</span><span class="sxs-lookup"><span data-stu-id="6cb89-186">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="6cb89-187">使用`-PackagesDirectory`指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cb89-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="6cb89-188">中`repositoryPath`的值`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="6cb89-188">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="6cb89-189">使用指定的資料夾`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="6cb89-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="6cb89-190">還原解決方案的套件時, NuGet 會執行下列動作:</span><span class="sxs-lookup"><span data-stu-id="6cb89-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="6cb89-191">載入方案檔。</span><span class="sxs-lookup"><span data-stu-id="6cb89-191">Loads the solution file.</span></span>
    - <span data-ttu-id="6cb89-192">將中列出的`$(SolutionDir)\.nuget\packages.config` `packages`方案層級封裝還原到資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6cb89-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="6cb89-193">將中列出的`$(ProjectDir)\packages.config` `packages`封裝還原到資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6cb89-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="6cb89-194">針對每個指定的封裝, 請以平行方式`-DisableParallelProcessing`還原封裝, 除非指定了。</span><span class="sxs-lookup"><span data-stu-id="6cb89-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="6cb89-195">範例</span><span class="sxs-lookup"><span data-stu-id="6cb89-195">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
