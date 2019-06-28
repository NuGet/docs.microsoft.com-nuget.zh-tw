---
title: NuGet CLI 還原命令
description: Nuget.exe restore 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d7a4188de4fb6f812ca19e7f9e302a5a133c58b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425964"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="fcc0f-103">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fcc0f-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="fcc0f-104">**適用於：** 套件耗用量&bullet;**支援的版本：** 2.7+</span><span class="sxs-lookup"><span data-stu-id="fcc0f-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="fcc0f-105">下載並安裝任何遺漏的套件`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="fcc0f-106">NuGet 4.0 + 和 PackageReference 格式搭配使用時，會產生`<project>.nuget.props`檔案，如有需要在`obj`資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="fcc0f-107">（從原始檔控制可以省略檔案）。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="fcc0f-108">Mac OSX 和 Linux 上使用 CLI 在 Mono 上，還原套件不支援使用 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="fcc0f-109">使用量</span><span class="sxs-lookup"><span data-stu-id="fcc0f-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="fcc0f-110">何處`<projectPath>`指定方案的位置或`packages.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="fcc0f-111">請參閱[備註](#remarks)下方的行為的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="fcc0f-112">選項</span><span class="sxs-lookup"><span data-stu-id="fcc0f-112">Options</span></span>

| <span data-ttu-id="fcc0f-113">選項</span><span class="sxs-lookup"><span data-stu-id="fcc0f-113">Option</span></span> | <span data-ttu-id="fcc0f-114">描述</span><span class="sxs-lookup"><span data-stu-id="fcc0f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fcc0f-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fcc0f-115">ConfigFile</span></span> | <span data-ttu-id="fcc0f-116">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fcc0f-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fcc0f-118">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="fcc0f-118">DirectDownload</span></span> | <span data-ttu-id="fcc0f-119">*（4.0 +)* 填入具有任何二進位檔或中繼資料的快取不直接下載套件。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-119">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="fcc0f-120">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="fcc0f-120">DisableParallelProcessing</span></span> | <span data-ttu-id="fcc0f-121">還原多個封裝，以平行方式停用。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-121">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="fcc0f-122">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="fcc0f-122">FallbackSource</span></span> | <span data-ttu-id="fcc0f-123">*（3.2 +)* 作為後援，以防主要中找不到封裝的封裝來源清單或預設來源。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-123">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="fcc0f-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fcc0f-124">ForceEnglishOutput</span></span> | <span data-ttu-id="fcc0f-125">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fcc0f-126">Help</span><span class="sxs-lookup"><span data-stu-id="fcc0f-126">Help</span></span> | <span data-ttu-id="fcc0f-127">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="fcc0f-128">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="fcc0f-128">MSBuildPath</span></span> | <span data-ttu-id="fcc0f-129">*（4.0 +)* 指定要搭配命令，優先於使用 MSBuild 的路徑`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="fcc0f-130">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="fcc0f-130">MSBuildVersion</span></span> | <span data-ttu-id="fcc0f-131">*（3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-131">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="fcc0f-132">支援的值為 4、 12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7，15.8、 15.9。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-132">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="fcc0f-133">根據您的路徑中的 MSBuild 會挑出的預設值，否則，預設已安裝的最高的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-133">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="fcc0f-134">NoCache</span><span class="sxs-lookup"><span data-stu-id="fcc0f-134">NoCache</span></span> | <span data-ttu-id="fcc0f-135">禁止 NuGet 使用的快取的套件。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-135">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="fcc0f-136">請參閱[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-136">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="fcc0f-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fcc0f-137">NonInteractive</span></span> | <span data-ttu-id="fcc0f-138">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fcc0f-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="fcc0f-139">OutputDirectory</span></span> | <span data-ttu-id="fcc0f-140">指定套件安裝所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="fcc0f-141">如果未不指定任何資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-141">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="fcc0f-142">必要時以還原`packages.config`檔案，除非`PackagesDirectory`或`SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-142">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="fcc0f-143">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="fcc0f-143">PackageSaveMode</span></span> | <span data-ttu-id="fcc0f-144">指定要在套件安裝之後儲存的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-144">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="fcc0f-145">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="fcc0f-145">PackagesDirectory</span></span> | <span data-ttu-id="fcc0f-146">與 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-146">Same as `OutputDirectory`.</span></span> <span data-ttu-id="fcc0f-147">必要時以還原`packages.config`檔案，除非`OutputDirectory`或`SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-147">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="fcc0f-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="fcc0f-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="fcc0f-149">以秒為單位來解析專案對專案參考的逾時。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="fcc0f-150">遞迴</span><span class="sxs-lookup"><span data-stu-id="fcc0f-150">Recursive</span></span> | <span data-ttu-id="fcc0f-151">*（4.0 +)* 還原適用於 UWP 和.NET Core 專案的所有參考專案。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="fcc0f-152">不適用於使用專案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="fcc0f-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="fcc0f-153">RequireConsent</span></span> | <span data-ttu-id="fcc0f-154">確認，然後再下載並安裝封裝中啟用還原套件。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="fcc0f-155">如需詳細資訊，請參閱 <<c0> [ 套件還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="fcc0f-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="fcc0f-156">SolutionDirectory</span></span> | <span data-ttu-id="fcc0f-157">指定的方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-157">Specifies the solution folder.</span></span> <span data-ttu-id="fcc0f-158">還原套件的解決方案時，則不正確。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-158">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="fcc0f-159">必要時以還原`packages.config`檔案，除非`PackagesDirectory`或`OutputDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-159">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="fcc0f-160">Source</span><span class="sxs-lookup"><span data-stu-id="fcc0f-160">Source</span></span> | <span data-ttu-id="fcc0f-161">指定封裝來源清單 （Url) 要用於還原。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-161">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="fcc0f-162">如果省略，則此命令會使用組態檔中提供的來源，請參閱 <<c0> [ 設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-162">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="fcc0f-163">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fcc0f-163">Verbosity</span></span> | <span data-ttu-id="fcc0f-164">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-164">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fcc0f-165">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fcc0f-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="fcc0f-166">備註</span><span class="sxs-lookup"><span data-stu-id="fcc0f-166">Remarks</span></span>

<span data-ttu-id="fcc0f-167">Restore 命令會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fcc0f-167">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="fcc0f-168">判斷 restore 命令的作業模式。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-168">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="fcc0f-169">projectPath 檔案類型</span><span class="sxs-lookup"><span data-stu-id="fcc0f-169">projectPath file type</span></span> | <span data-ttu-id="fcc0f-170">行為</span><span class="sxs-lookup"><span data-stu-id="fcc0f-170">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="fcc0f-171">方案 （資料夾）</span><span class="sxs-lookup"><span data-stu-id="fcc0f-171">Solution (folder)</span></span> | <span data-ttu-id="fcc0f-172">NuGet 會尋找`.sln`檔案，並使用，如未找到則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-172">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="fcc0f-173">`(SolutionDir)\.nuget` 做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-173">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="fcc0f-174">`.sln` 檔案</span><span class="sxs-lookup"><span data-stu-id="fcc0f-174">`.sln` file</span></span> | <span data-ttu-id="fcc0f-175">還原方案中; 所識別的套件如果會顯示錯誤`-SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-175">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="fcc0f-176">`$(SolutionDir)\.nuget` 做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-176">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="fcc0f-177">`packages.config` 或專案檔</span><span class="sxs-lookup"><span data-stu-id="fcc0f-177">`packages.config` or project file</span></span> | <span data-ttu-id="fcc0f-178">還原在檔案中，解決並安裝相依性所列的套件。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-178">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="fcc0f-179">其他檔案類型</span><span class="sxs-lookup"><span data-stu-id="fcc0f-179">Other file type</span></span> | <span data-ttu-id="fcc0f-180">檔案會假設為`.sln`檔案儲存為上述的; 如果不是方案時，發生錯誤的 NuGet 提供。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-180">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="fcc0f-181">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="fcc0f-181">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="fcc0f-182">NuGet 會尋找目前資料夾中的方案檔。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-182">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="fcc0f-183">如果找到單一檔案，則使用該還原套件;如果找到多個方案，則 NuGet 會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-183">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="fcc0f-184">如果沒有方案檔案，NuGet 會尋找`packages.config`並使用它來還原套件。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-184">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="fcc0f-185">如果沒有解決方案或`packages.config`找到檔案，NuGet 會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-185">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="fcc0f-186">決定使用下列優先順序 （NuGet 如果找不到任何這些資料夾會顯示錯誤） 的 [packages] 資料夾：</span><span class="sxs-lookup"><span data-stu-id="fcc0f-186">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="fcc0f-187">使用指定的資料夾`-PackagesDirectory`。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="fcc0f-188">`repositoryPath`中的值 `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="fcc0f-188">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="fcc0f-189">使用指定的資料夾 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="fcc0f-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="fcc0f-190">當還原方案的套件，NuGet 會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="fcc0f-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="fcc0f-191">載入方案檔。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-191">Loads the solution file.</span></span>
    - <span data-ttu-id="fcc0f-192">還原方案中所列的層級套件`$(SolutionDir)\.nuget\packages.config`成`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="fcc0f-193">還原套件中所列`$(ProjectDir)\packages.config`成`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="fcc0f-194">指定每一個封裝還原以平行方式封裝除非`-DisableParallelProcessing`指定。</span><span class="sxs-lookup"><span data-stu-id="fcc0f-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="fcc0f-195">範例</span><span class="sxs-lookup"><span data-stu-id="fcc0f-195">Examples</span></span>

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
