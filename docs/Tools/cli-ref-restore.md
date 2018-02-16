---
title: "NuGet CLI restore 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 還原命令的參考"
keywords: "nuget 還原參考，請還原封裝命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0ad5156a065e20dfced99da6b2e2860dbd748ad5
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="919c1-104">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="919c1-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="919c1-105">**適用於：**封裝耗用量&bullet;**支援的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="919c1-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="919c1-106">下載並安裝任何遺漏的套件`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="919c1-107">搭配 NuGet 4.0 + 及 PackageReference 格式使用時，會產生`<project>.nuget.props`檔案，如有需要在`obj`資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="919c1-108">（從原始檔控制可以省略檔案）。</span><span class="sxs-lookup"><span data-stu-id="919c1-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="919c1-109">在 Mac OSX 與 Linux 上 Mono CLI 與，還原封裝不支援 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="919c1-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="919c1-110">使用量</span><span class="sxs-lookup"><span data-stu-id="919c1-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="919c1-111">其中`<projectPath>`指定方案的位置或`packages.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="919c1-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="919c1-112">請參閱[備註](#remarks)下方的行為的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="919c1-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="919c1-113">選項</span><span class="sxs-lookup"><span data-stu-id="919c1-113">Options</span></span>

| <span data-ttu-id="919c1-114">選項</span><span class="sxs-lookup"><span data-stu-id="919c1-114">Option</span></span> | <span data-ttu-id="919c1-115">描述</span><span class="sxs-lookup"><span data-stu-id="919c1-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="919c1-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="919c1-116">ConfigFile</span></span> | <span data-ttu-id="919c1-117">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="919c1-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="919c1-118">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="919c1-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="919c1-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="919c1-119">DirectDownload</span></span> | <span data-ttu-id="919c1-120">*（4.0 +)*下載套件，直接但不填入任何二進位檔或中繼資料快取。</span><span class="sxs-lookup"><span data-stu-id="919c1-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="919c1-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="919c1-121">DisableParallelProcessing</span></span> | <span data-ttu-id="919c1-122">還原多個封裝，以平行方式停用。</span><span class="sxs-lookup"><span data-stu-id="919c1-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="919c1-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="919c1-123">FallbackSource</span></span> | <span data-ttu-id="919c1-124">*（3.2 +)*作為後援，萬一主要中找不到封裝的封裝來源的清單或預設的來源。</span><span class="sxs-lookup"><span data-stu-id="919c1-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="919c1-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="919c1-125">ForceEnglishOutput</span></span> | <span data-ttu-id="919c1-126">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="919c1-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="919c1-127">說明</span><span class="sxs-lookup"><span data-stu-id="919c1-127">Help</span></span> | <span data-ttu-id="919c1-128">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="919c1-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="919c1-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="919c1-129">MSBuildPath</span></span> | <span data-ttu-id="919c1-130">*（4.0 +)*指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="919c1-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="919c1-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="919c1-131">MSBuildVersion</span></span> | <span data-ttu-id="919c1-132">*（3.2 +)*指定要搭配此命令使用 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="919c1-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="919c1-133">支援的值為 4，12，14，15。</span><span class="sxs-lookup"><span data-stu-id="919c1-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="919c1-134">根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="919c1-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="919c1-135">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="919c1-135">NoCache</span></span> | <span data-ttu-id="919c1-136">NuGet 可防止從本機電腦的快取使用的封裝。</span><span class="sxs-lookup"><span data-stu-id="919c1-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="919c1-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="919c1-137">NonInteractive</span></span> | <span data-ttu-id="919c1-138">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="919c1-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="919c1-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="919c1-139">OutputDirectory</span></span> | <span data-ttu-id="919c1-140">指定在其中安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="919c1-141">如果沒有指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="919c1-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="919c1-142">PackageSaveMode</span></span> | <span data-ttu-id="919c1-143">指定要儲存封裝的安裝後的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="919c1-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="919c1-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="919c1-144">PackagesDirectory</span></span> | <span data-ttu-id="919c1-145">與 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="919c1-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="919c1-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="919c1-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="919c1-147">以秒為單位來解析專案對專案參考的逾時。</span><span class="sxs-lookup"><span data-stu-id="919c1-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="919c1-148">遞迴</span><span class="sxs-lookup"><span data-stu-id="919c1-148">Recursive</span></span> | <span data-ttu-id="919c1-149">*（4.0 +)*還原所有參考的專案，適用於 UWP 和.NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="919c1-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="919c1-150">不適用於使用專案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="919c1-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="919c1-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="919c1-151">RequireConsent</span></span> | <span data-ttu-id="919c1-152">確認一次還原封裝才能下載和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="919c1-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="919c1-153">如需詳細資訊，請參閱[封裝還原，](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="919c1-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="919c1-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="919c1-154">SolutionDirectory</span></span> | <span data-ttu-id="919c1-155">指定的方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-155">Specifies the solution folder.</span></span> <span data-ttu-id="919c1-156">還原解決方案的封裝時，則不正確。</span><span class="sxs-lookup"><span data-stu-id="919c1-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="919c1-157">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="919c1-157">Source</span></span> | <span data-ttu-id="919c1-158">指定封裝來源清單 （Url) 要用於還原。</span><span class="sxs-lookup"><span data-stu-id="919c1-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="919c1-159">如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="919c1-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="919c1-160">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="919c1-160">Verbosity</span></span> |<span data-ttu-id="919c1-161">> 指定輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="919c1-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="919c1-162">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="919c1-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="919c1-163">備註</span><span class="sxs-lookup"><span data-stu-id="919c1-163">Remarks</span></span>

<span data-ttu-id="919c1-164">還原命令會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="919c1-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="919c1-165">判斷作業模式的 restore 命令。</span><span class="sxs-lookup"><span data-stu-id="919c1-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="919c1-166">projectPath 檔案類型</span><span class="sxs-lookup"><span data-stu-id="919c1-166">projectPath file type</span></span> | <span data-ttu-id="919c1-167">行為</span><span class="sxs-lookup"><span data-stu-id="919c1-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="919c1-168">方案 （資料夾）</span><span class="sxs-lookup"><span data-stu-id="919c1-168">Solution (folder)</span></span> | <span data-ttu-id="919c1-169">尋找 NuGet`.sln`檔案，並有找到，否則將會提供錯誤的使用。</span><span class="sxs-lookup"><span data-stu-id="919c1-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="919c1-170">`(SolutionDir)\.nuget` 做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="919c1-171">`.sln` 檔案</span><span class="sxs-lookup"><span data-stu-id="919c1-171">`.sln` file</span></span> | <span data-ttu-id="919c1-172">還原方案; 所識別的封裝如果將會提供錯誤`-SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="919c1-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="919c1-173">`$(SolutionDir)\.nuget` 做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="919c1-174">`packages.config` 或專案檔</span><span class="sxs-lookup"><span data-stu-id="919c1-174">`packages.config` or project file</span></span> | <span data-ttu-id="919c1-175">還原檔案，解決和安裝相依性中所列的封裝。</span><span class="sxs-lookup"><span data-stu-id="919c1-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="919c1-176">其他檔案類型</span><span class="sxs-lookup"><span data-stu-id="919c1-176">Other file type</span></span> | <span data-ttu-id="919c1-177">檔案被假設為`.sln`檔案做為上述; 如果不是方案時，發生錯誤的 NuGet 提供。</span><span class="sxs-lookup"><span data-stu-id="919c1-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="919c1-178">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="919c1-178">(projectPath not specified)</span></span> | <span data-ttu-id="919c1-179">-NuGet 會尋找目前的資料夾中的方案檔。</span><span class="sxs-lookup"><span data-stu-id="919c1-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="919c1-180">如果找到單一檔案，則使用該還原封裝。如果找不到多個方案，NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="919c1-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="919c1-181">-如果沒有方案檔案，NuGet 會尋找`packages.config`並使用該值來還原封裝。</span><span class="sxs-lookup"><span data-stu-id="919c1-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="919c1-182">-如果沒有解決方案或`packages.config`找不到檔案，NuGet 會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="919c1-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="919c1-183">判斷使用下列優先順序 （NuGet 如果找不到任何這些資料夾會顯示錯誤） 的封裝資料夾：</span><span class="sxs-lookup"><span data-stu-id="919c1-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="919c1-184">使用指定的資料夾`-PackagesDirectory`。</span><span class="sxs-lookup"><span data-stu-id="919c1-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="919c1-185">`repositoryPath`值中的，此值 `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="919c1-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="919c1-186">使用指定的資料夾 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="919c1-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="919c1-187">還原時的方案套件，NuGet 會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="919c1-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="919c1-188">載入方案檔案。</span><span class="sxs-lookup"><span data-stu-id="919c1-188">Loads the solution file.</span></span>
    - <span data-ttu-id="919c1-189">還原方案層級中所列的套件`$(SolutionDir)\.nuget\packages.config`到`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="919c1-190">還原封裝中所列`$(ProjectDir)\packages.config`到`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="919c1-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="919c1-191">指定每一個封裝，還原以平行方式封裝除非`-DisableParallelProcessing`指定。</span><span class="sxs-lookup"><span data-stu-id="919c1-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="919c1-192">範例</span><span class="sxs-lookup"><span data-stu-id="919c1-192">Examples</span></span>

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
