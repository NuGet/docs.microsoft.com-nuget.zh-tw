---
title: NuGet CLI restore 命令
description: Nuget.exe 還原命令的參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4df7685883fea78428c6744bdbf4c66d83e469bc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817914"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="7785b-103">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7785b-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="7785b-104">**適用於：** 封裝耗用量&bullet;**支援的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="7785b-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="7785b-105">下載並安裝任何遺漏的套件`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="7785b-106">搭配 NuGet 4.0 + 及 PackageReference 格式使用時，會產生`<project>.nuget.props`檔案，如有需要在`obj`資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="7785b-107">（從原始檔控制可以省略檔案）。</span><span class="sxs-lookup"><span data-stu-id="7785b-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="7785b-108">在 Mac OSX 與 Linux 上 Mono CLI 與，還原封裝不支援 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="7785b-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="7785b-109">使用量</span><span class="sxs-lookup"><span data-stu-id="7785b-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="7785b-110">其中`<projectPath>`指定方案的位置或`packages.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="7785b-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="7785b-111">請參閱[備註](#remarks)下方的行為的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7785b-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="7785b-112">選項</span><span class="sxs-lookup"><span data-stu-id="7785b-112">Options</span></span>

| <span data-ttu-id="7785b-113">選項</span><span class="sxs-lookup"><span data-stu-id="7785b-113">Option</span></span> | <span data-ttu-id="7785b-114">描述</span><span class="sxs-lookup"><span data-stu-id="7785b-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7785b-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7785b-115">ConfigFile</span></span> | <span data-ttu-id="7785b-116">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="7785b-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7785b-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="7785b-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7785b-118">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="7785b-118">DirectDownload</span></span> | <span data-ttu-id="7785b-119">*（4.0 +)* 下載套件，直接但不填入任何二進位檔或中繼資料快取。</span><span class="sxs-lookup"><span data-stu-id="7785b-119">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="7785b-120">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="7785b-120">DisableParallelProcessing</span></span> | <span data-ttu-id="7785b-121">還原多個封裝，以平行方式停用。</span><span class="sxs-lookup"><span data-stu-id="7785b-121">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="7785b-122">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="7785b-122">FallbackSource</span></span> | <span data-ttu-id="7785b-123">*（3.2 +)* 作為後援，萬一主要中找不到封裝的封裝來源的清單或預設的來源。</span><span class="sxs-lookup"><span data-stu-id="7785b-123">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="7785b-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7785b-124">ForceEnglishOutput</span></span> | <span data-ttu-id="7785b-125">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="7785b-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7785b-126">說明</span><span class="sxs-lookup"><span data-stu-id="7785b-126">Help</span></span> | <span data-ttu-id="7785b-127">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="7785b-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="7785b-128">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="7785b-128">MSBuildPath</span></span> | <span data-ttu-id="7785b-129">*（4.0 +)* 指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="7785b-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="7785b-130">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="7785b-130">MSBuildVersion</span></span> | <span data-ttu-id="7785b-131">*（3.2 +)* 指定要搭配此命令使用 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="7785b-131">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="7785b-132">支援的值為 4，12，14，15。</span><span class="sxs-lookup"><span data-stu-id="7785b-132">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="7785b-133">根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="7785b-133">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="7785b-134">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="7785b-134">NoCache</span></span> | <span data-ttu-id="7785b-135">NuGet 可防止使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="7785b-135">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="7785b-136">請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="7785b-136">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="7785b-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7785b-137">NonInteractive</span></span> | <span data-ttu-id="7785b-138">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="7785b-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7785b-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="7785b-139">OutputDirectory</span></span> | <span data-ttu-id="7785b-140">指定在其中安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="7785b-141">如果沒有指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-141">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="7785b-142">必要時還原`packages.config`檔案除非`PackagesDirectory`或`SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="7785b-142">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="7785b-143">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="7785b-143">PackageSaveMode</span></span> | <span data-ttu-id="7785b-144">指定要儲存封裝的安裝後的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="7785b-144">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="7785b-145">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="7785b-145">PackagesDirectory</span></span> | <span data-ttu-id="7785b-146">與 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="7785b-146">Same as `OutputDirectory`.</span></span> <span data-ttu-id="7785b-147">必要時還原`packages.config`檔案除非`OutputDirectory`或`SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="7785b-147">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="7785b-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="7785b-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="7785b-149">以秒為單位來解析專案對專案參考的逾時。</span><span class="sxs-lookup"><span data-stu-id="7785b-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="7785b-150">遞迴</span><span class="sxs-lookup"><span data-stu-id="7785b-150">Recursive</span></span> | <span data-ttu-id="7785b-151">*（4.0 +)* 還原所有參考的專案，適用於 UWP 和.NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="7785b-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="7785b-152">不適用於使用專案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="7785b-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="7785b-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="7785b-153">RequireConsent</span></span> | <span data-ttu-id="7785b-154">確認一次還原封裝才能下載和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="7785b-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="7785b-155">如需詳細資訊，請參閱[封裝還原，](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="7785b-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="7785b-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="7785b-156">SolutionDirectory</span></span> | <span data-ttu-id="7785b-157">指定的方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-157">Specifies the solution folder.</span></span> <span data-ttu-id="7785b-158">還原解決方案的封裝時，則不正確。</span><span class="sxs-lookup"><span data-stu-id="7785b-158">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="7785b-159">必要時還原`packages.config`檔案除非`PackagesDirectory`或`OutputDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="7785b-159">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="7785b-160">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="7785b-160">Source</span></span> | <span data-ttu-id="7785b-161">指定封裝來源清單 （Url) 要用於還原。</span><span class="sxs-lookup"><span data-stu-id="7785b-161">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="7785b-162">如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="7785b-162">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="7785b-163">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7785b-163">Verbosity</span></span> |<span data-ttu-id="7785b-164">> 指定輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="7785b-164">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7785b-165">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7785b-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="7785b-166">備註</span><span class="sxs-lookup"><span data-stu-id="7785b-166">Remarks</span></span>

<span data-ttu-id="7785b-167">還原命令會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7785b-167">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="7785b-168">判斷作業模式的 restore 命令。</span><span class="sxs-lookup"><span data-stu-id="7785b-168">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="7785b-169">projectPath 檔案類型</span><span class="sxs-lookup"><span data-stu-id="7785b-169">projectPath file type</span></span> | <span data-ttu-id="7785b-170">行為</span><span class="sxs-lookup"><span data-stu-id="7785b-170">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="7785b-171">方案 （資料夾）</span><span class="sxs-lookup"><span data-stu-id="7785b-171">Solution (folder)</span></span> | <span data-ttu-id="7785b-172">尋找 NuGet`.sln`檔案，並有找到，否則將會提供錯誤的使用。</span><span class="sxs-lookup"><span data-stu-id="7785b-172">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="7785b-173">`(SolutionDir)\.nuget` 做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-173">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="7785b-174">`.sln` 檔案</span><span class="sxs-lookup"><span data-stu-id="7785b-174">`.sln` file</span></span> | <span data-ttu-id="7785b-175">還原方案; 所識別的封裝如果將會提供錯誤`-SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="7785b-175">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="7785b-176">`$(SolutionDir)\.nuget` 做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-176">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="7785b-177">`packages.config` 或專案檔</span><span class="sxs-lookup"><span data-stu-id="7785b-177">`packages.config` or project file</span></span> | <span data-ttu-id="7785b-178">還原檔案，解決和安裝相依性中所列的封裝。</span><span class="sxs-lookup"><span data-stu-id="7785b-178">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="7785b-179">其他檔案類型</span><span class="sxs-lookup"><span data-stu-id="7785b-179">Other file type</span></span> | <span data-ttu-id="7785b-180">檔案被假設為`.sln`檔案做為上述; 如果不是方案時，發生錯誤的 NuGet 提供。</span><span class="sxs-lookup"><span data-stu-id="7785b-180">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="7785b-181">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="7785b-181">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="7785b-182">NuGet 會尋找目前的資料夾中的方案檔。</span><span class="sxs-lookup"><span data-stu-id="7785b-182">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="7785b-183">如果找到單一檔案，則使用該還原封裝。如果找不到多個方案，NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="7785b-183">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="7785b-184">如果沒有方案檔案，NuGet 會尋找`packages.config`並使用該值來還原封裝。</span><span class="sxs-lookup"><span data-stu-id="7785b-184">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="7785b-185">如果沒有解決方案或`packages.config`找不到檔案，NuGet 會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7785b-185">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="7785b-186">判斷使用下列優先順序 （NuGet 如果找不到任何這些資料夾會顯示錯誤） 的封裝資料夾：</span><span class="sxs-lookup"><span data-stu-id="7785b-186">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="7785b-187">使用指定的資料夾`-PackagesDirectory`。</span><span class="sxs-lookup"><span data-stu-id="7785b-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="7785b-188">`repositoryPath`值中的，此值 `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="7785b-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="7785b-189">使用指定的資料夾 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="7785b-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="7785b-190">還原時的方案套件，NuGet 會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="7785b-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="7785b-191">載入方案檔案。</span><span class="sxs-lookup"><span data-stu-id="7785b-191">Loads the solution file.</span></span>
    - <span data-ttu-id="7785b-192">還原方案層級中所列的套件`$(SolutionDir)\.nuget\packages.config`到`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="7785b-193">還原封裝中所列`$(ProjectDir)\packages.config`到`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="7785b-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="7785b-194">指定每一個封裝，還原以平行方式封裝除非`-DisableParallelProcessing`指定。</span><span class="sxs-lookup"><span data-stu-id="7785b-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="7785b-195">範例</span><span class="sxs-lookup"><span data-stu-id="7785b-195">Examples</span></span>

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
