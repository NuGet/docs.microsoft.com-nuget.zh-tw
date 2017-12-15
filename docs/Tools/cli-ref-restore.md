---
title: "NuGet CLI restore 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Nuget.exe 還原命令的參考"
keywords: "nuget 還原參考，請還原封裝命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="62e66-104">restore 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="62e66-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="62e66-105">**適用於：**封裝耗用量&bullet;**支援的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="62e66-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="62e66-106">NuGet 2.7 +: 下載並安裝任何遺漏的套件`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="62e66-107">NuGet 3.3 + 搭配使用的專案`project.json`： 產生`project.lock.json`檔案和`<project>.nuget.props`檔案，如有需要。</span><span class="sxs-lookup"><span data-stu-id="62e66-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="62e66-108">（這兩個檔案可以省略從原始檔控制）。</span><span class="sxs-lookup"><span data-stu-id="62e66-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="62e66-109">NuGet 4.0 + 與專案的封裝中包含參考專案檔中直接： 產生`<project>.nuget.props`檔案，如有需要在`obj`資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="62e66-110">（從原始檔控制可以省略檔案）。</span><span class="sxs-lookup"><span data-stu-id="62e66-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="62e66-111">Mac OSX 與 Linux 上 Mono CLI 與，還原封裝不支援使用 PackageReference 格式。</span><span class="sxs-lookup"><span data-stu-id="62e66-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="62e66-112">使用方式</span><span class="sxs-lookup"><span data-stu-id="62e66-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="62e66-113">其中`<projectPath>`指定位置的解決方案，`packages.config`檔案，或`project.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="62e66-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="62e66-114">請參閱[備註](#remarks)下方的行為的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="62e66-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="62e66-115">選項</span><span class="sxs-lookup"><span data-stu-id="62e66-115">Options</span></span>

| <span data-ttu-id="62e66-116">選項</span><span class="sxs-lookup"><span data-stu-id="62e66-116">Option</span></span> | <span data-ttu-id="62e66-117">說明</span><span class="sxs-lookup"><span data-stu-id="62e66-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="62e66-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="62e66-118">ConfigFile</span></span> | <span data-ttu-id="62e66-119">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="62e66-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="62e66-120">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="62e66-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="62e66-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="62e66-121">DirectDownload</span></span> | <span data-ttu-id="62e66-122">*（4.0 +)*下載套件，直接但不填入任何二進位檔或中繼資料快取。</span><span class="sxs-lookup"><span data-stu-id="62e66-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="62e66-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="62e66-123">DisableParallelProcessing</span></span> | <span data-ttu-id="62e66-124">還原多個封裝，以平行方式停用。</span><span class="sxs-lookup"><span data-stu-id="62e66-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="62e66-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="62e66-125">FallbackSource</span></span> | <span data-ttu-id="62e66-126">*（3.2 +)*作為後援，萬一主要中找不到封裝的封裝來源的清單或預設的來源。</span><span class="sxs-lookup"><span data-stu-id="62e66-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="62e66-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="62e66-127">ForceEnglishOutput</span></span> | <span data-ttu-id="62e66-128">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="62e66-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="62e66-129">說明</span><span class="sxs-lookup"><span data-stu-id="62e66-129">Help</span></span> | <span data-ttu-id="62e66-130">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="62e66-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="62e66-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="62e66-131">MSBuildPath</span></span> | <span data-ttu-id="62e66-132">*（4.0 +)*指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="62e66-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="62e66-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="62e66-133">MSBuildVersion</span></span> | <span data-ttu-id="62e66-134">*（3.2 +)*指定要搭配此命令使用 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="62e66-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="62e66-135">支援的值為 4，12，14，15。</span><span class="sxs-lookup"><span data-stu-id="62e66-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="62e66-136">根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="62e66-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="62e66-137">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="62e66-137">NoCache</span></span> | <span data-ttu-id="62e66-138">NuGet 可防止從本機電腦的快取使用的封裝。</span><span class="sxs-lookup"><span data-stu-id="62e66-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="62e66-139">非互動式</span><span class="sxs-lookup"><span data-stu-id="62e66-139">NonInteractive</span></span> | <span data-ttu-id="62e66-140">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="62e66-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="62e66-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="62e66-141">OutputDirectory</span></span> | <span data-ttu-id="62e66-142">指定在其中安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="62e66-143">如果沒有指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="62e66-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="62e66-144">PackageSaveMode</span></span> | <span data-ttu-id="62e66-145">指定要儲存封裝的安裝後的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="62e66-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="62e66-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="62e66-146">PackagesDirectory</span></span> | <span data-ttu-id="62e66-147">與 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="62e66-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="62e66-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="62e66-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="62e66-149">以秒為單位來解析專案對專案參考的逾時。</span><span class="sxs-lookup"><span data-stu-id="62e66-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="62e66-150">遞迴</span><span class="sxs-lookup"><span data-stu-id="62e66-150">Recursive</span></span> | <span data-ttu-id="62e66-151">*（4.0 +)*還原所有參考的專案，適用於 UWP 和.NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="62e66-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="62e66-152">不適用於使用專案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="62e66-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="62e66-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="62e66-153">RequireConsent</span></span> | <span data-ttu-id="62e66-154">確認一次還原封裝才能下載和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="62e66-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="62e66-155">如需詳細資訊，請參閱[封裝還原，](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="62e66-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="62e66-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="62e66-156">SolutionDirectory</span></span> | <span data-ttu-id="62e66-157">指定的方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-157">Specifies the solution folder.</span></span> <span data-ttu-id="62e66-158">還原解決方案的封裝時，則不正確。</span><span class="sxs-lookup"><span data-stu-id="62e66-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="62e66-159">來源</span><span class="sxs-lookup"><span data-stu-id="62e66-159">Source</span></span> | <span data-ttu-id="62e66-160">指定封裝來源清單 （Url) 要用於還原。</span><span class="sxs-lookup"><span data-stu-id="62e66-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="62e66-161">如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../Consume-Packages/Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="62e66-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="62e66-162">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="62e66-162">Verbosity</span></span> |<span data-ttu-id="62e66-163">> 指定輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="62e66-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="62e66-164">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="62e66-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="62e66-165">備註</span><span class="sxs-lookup"><span data-stu-id="62e66-165">Remarks</span></span>

<span data-ttu-id="62e66-166">還原命令會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="62e66-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="62e66-167">判斷作業模式的 restore 命令。</span><span class="sxs-lookup"><span data-stu-id="62e66-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="62e66-168">projectPath 檔案類型</span><span class="sxs-lookup"><span data-stu-id="62e66-168">projectPath file type</span></span> | <span data-ttu-id="62e66-169">行為</span><span class="sxs-lookup"><span data-stu-id="62e66-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="62e66-170">方案 （資料夾）</span><span class="sxs-lookup"><span data-stu-id="62e66-170">Solution (folder)</span></span> | <span data-ttu-id="62e66-171">尋找 NuGet`.sln`檔案，並有找到，否則將會提供錯誤的使用。</span><span class="sxs-lookup"><span data-stu-id="62e66-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="62e66-172">`(SolutionDir)\.nuget`做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="62e66-173">`.sln`檔案</span><span class="sxs-lookup"><span data-stu-id="62e66-173">`.sln` file</span></span> | <span data-ttu-id="62e66-174">還原方案; 所識別的封裝如果將會提供錯誤`-SolutionDirectory`用。</span><span class="sxs-lookup"><span data-stu-id="62e66-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="62e66-175">`$(SolutionDir)\.nuget`做為起始的資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="62e66-176">`packages.config``project.json`，或專案檔</span><span class="sxs-lookup"><span data-stu-id="62e66-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="62e66-177">還原檔案，解決和安裝相依性中所列的封裝。</span><span class="sxs-lookup"><span data-stu-id="62e66-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="62e66-178">其他檔案類型</span><span class="sxs-lookup"><span data-stu-id="62e66-178">Other file type</span></span> | <span data-ttu-id="62e66-179">檔案被假設為`.sln`檔案做為上述; 如果不是方案時，發生錯誤的 NuGet 提供。</span><span class="sxs-lookup"><span data-stu-id="62e66-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="62e66-180">(未指定 projectPath)</span><span class="sxs-lookup"><span data-stu-id="62e66-180">(projectPath not specified)</span></span> | <span data-ttu-id="62e66-181">-NuGet 會尋找目前的資料夾中的方案檔。</span><span class="sxs-lookup"><span data-stu-id="62e66-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="62e66-182">如果找到單一檔案，則使用該還原封裝。如果找不到多個方案，NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="62e66-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="62e66-183">-如果沒有方案檔案，NuGet 會尋找`packages.config`或`project.json`並使用該值來還原封裝。</span><span class="sxs-lookup"><span data-stu-id="62e66-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="62e66-184">-如果沒有方案檔， `packages.config`，或`project.json`找到，NuGet 會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="62e66-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="62e66-185">判斷使用下列優先順序 （NuGet 如果找不到任何這些資料夾會顯示錯誤） 的封裝資料夾：</span><span class="sxs-lookup"><span data-stu-id="62e66-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="62e66-186">`%userprofile%\.nuget\packages`值`project.json`。</span><span class="sxs-lookup"><span data-stu-id="62e66-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="62e66-187">使用指定的資料夾`-PackagesDirectory`。</span><span class="sxs-lookup"><span data-stu-id="62e66-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="62e66-188">`repositoryPath`值中的，此值`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="62e66-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="62e66-189">使用指定的資料夾`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="62e66-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="62e66-190">還原時的方案套件，NuGet 會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="62e66-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="62e66-191">載入方案檔案。</span><span class="sxs-lookup"><span data-stu-id="62e66-191">Loads the solution file.</span></span>
    - <span data-ttu-id="62e66-192">還原方案層級中所列的套件`$(SolutionDir)\.nuget\packages.config`到`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="62e66-193">還原封裝中所列`$(ProjectDir)\packages.config`到`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e66-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="62e66-194">指定每一個封裝，還原以平行方式封裝除非`-DisableParallelProcessing`指定。</span><span class="sxs-lookup"><span data-stu-id="62e66-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="62e66-195">範例</span><span class="sxs-lookup"><span data-stu-id="62e66-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
