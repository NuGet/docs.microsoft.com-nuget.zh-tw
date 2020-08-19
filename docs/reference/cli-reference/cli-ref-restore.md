---
title: NuGet CLI 還原命令
description: nuget.exe restore 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622825"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="ad0ae-103"> (NuGet CLI 還原命令) </span><span class="sxs-lookup"><span data-stu-id="ad0ae-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="ad0ae-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="ad0ae-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="ad0ae-105">下載並安裝資料夾中遺失的任何套件 `packages` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="ad0ae-106">與 NuGet 4.0 + 和 PackageReference 格式搭配使用時，會 `<project>.nuget.props` 在資料夾中產生檔案（如有需要） `obj` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="ad0ae-107"> (可以從原始檔控制省略檔案。 ) </span><span class="sxs-lookup"><span data-stu-id="ad0ae-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="ad0ae-108">在 Mac OSX 和 Linux 上搭配使用 CLI 與 Mono，PackageReference 不支援還原套件。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="ad0ae-109">使用方式</span><span class="sxs-lookup"><span data-stu-id="ad0ae-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="ad0ae-110">其中 `<projectPath>` 指定方案或檔案的位置 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="ad0ae-111">如需行為詳細資料，請參閱下面的 [備註](#remarks) 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="ad0ae-112">選項。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ad0ae-113">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ad0ae-114">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="ad0ae-115">\* (4.0 +) \* 直接下載套件，而不將任何二進位檔或中繼資料填入快取。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="ad0ae-116">停用平行還原多個封裝。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="ad0ae-117">\* (3.2 +) \* 在主要或預設來源中找不到封裝時，用來做為回盒的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="ad0ae-118">使用分號來分隔清單專案。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="ad0ae-119">在以 PackageReference 為基礎的專案中，即使上次還原成功，仍會強制解析所有相依性。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="ad0ae-120">指定此旗標與刪除檔案類似 `project.assets.json` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="ad0ae-121">這不會略過 HTTP 快取。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ad0ae-122">\* (3.5 +) \* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="ad0ae-123">強制還原重新評估所有的相依性，即使鎖定檔案已存在也一樣。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ad0ae-124">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="ad0ae-125">寫入專案鎖定檔案的輸出位置。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-125">Output location where project lock file is written.</span></span> <span data-ttu-id="ad0ae-126">根據預設，這是 `PROJECT_ROOT\packages.lock.json`。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="ad0ae-127">不允許更新專案鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="ad0ae-128">\* (4.0 +) \* 指定要搭配命令使用的 MSBuild 路徑，優先順序高於 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="ad0ae-129">\* (3.2 +) \* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ad0ae-130">支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="ad0ae-131">依預設，會挑選路徑中的 MSBuild，否則會預設為 MSBuild 的最高安裝版本。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="ad0ae-132">防止 NuGet 使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="ad0ae-133">請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ad0ae-134">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="ad0ae-135">指定安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ad0ae-136">如果未指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="ad0ae-137">`packages.config`除非 `PackagesDirectory` 使用或，否則使用檔案還原時為必要項 `SolutionDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="ad0ae-138">指定封裝安裝之後要儲存的檔案類型：、或的其中一個 `nuspec` `nupkg` `nuspec;nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="ad0ae-139">與 `OutputDirectory` 相同。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="ad0ae-140">`packages.config`除非 `OutputDirectory` 使用或，否則使用檔案還原時為必要項 `SolutionDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="ad0ae-141">解析專案對專案參考的時間（秒）。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="ad0ae-142">\* (4.0 +) \* 還原 UWP 和 .NET Core 專案的所有參考專案。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="ad0ae-143">不會套用至使用 `packages.config` 的專案。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="ad0ae-144">確認在下載及安裝封裝之前，已啟用還原的封裝。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ad0ae-145">如需詳細資訊，請參閱 [封裝還原](../../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="ad0ae-146">指定方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-146">Specifies the solution folder.</span></span> <span data-ttu-id="ad0ae-147">還原解決方案的封裝時無效。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="ad0ae-148">`packages.config`除非 `PackagesDirectory` 使用或，否則使用檔案還原時為必要項 `OutputDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="ad0ae-149">將套件來源的清單指定為用於還原的 Url)  (。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="ad0ae-150">如果省略，此命令會使用設定檔中提供的來源，請參閱設定 [NuGet 行為](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="ad0ae-151">使用分號來分隔清單專案。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="ad0ae-152">可產生專案鎖定檔案並與還原一起使用。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ad0ae-153">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="ad0ae-154">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ad0ae-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="ad0ae-155">備註</span><span class="sxs-lookup"><span data-stu-id="ad0ae-155">Remarks</span></span>

<span data-ttu-id="ad0ae-156">Restore 命令會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ad0ae-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="ad0ae-157">判斷還原命令的操作模式。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="ad0ae-158">projectPath 檔案類型</span><span class="sxs-lookup"><span data-stu-id="ad0ae-158">projectPath file type</span></span> | <span data-ttu-id="ad0ae-159">行為</span><span class="sxs-lookup"><span data-stu-id="ad0ae-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="ad0ae-160">方案 (資料夾) </span><span class="sxs-lookup"><span data-stu-id="ad0ae-160">Solution (folder)</span></span> | <span data-ttu-id="ad0ae-161">NuGet 會尋找檔案 `.sln` 並使用該檔案（如果找到的話），否則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="ad0ae-162">`(SolutionDir)\.nuget` 會當做起始資料夾使用。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="ad0ae-163">`.sln` 檔案</span><span class="sxs-lookup"><span data-stu-id="ad0ae-163">`.sln` file</span></span> | <span data-ttu-id="ad0ae-164">還原解決方案所識別的封裝;如果 `-SolutionDirectory` 使用，則會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="ad0ae-165">`$(SolutionDir)\.nuget` 會當做起始資料夾使用。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="ad0ae-166">`packages.config` 或專案檔</span><span class="sxs-lookup"><span data-stu-id="ad0ae-166">`packages.config` or project file</span></span> | <span data-ttu-id="ad0ae-167">還原檔案中列出的封裝，並解析和安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="ad0ae-168">其他檔案類型</span><span class="sxs-lookup"><span data-stu-id="ad0ae-168">Other file type</span></span> | <span data-ttu-id="ad0ae-169">檔案會假設為上述的檔案 `.sln` ; 如果不是解決方案，NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="ad0ae-170">未指定 (projectPath) </span><span class="sxs-lookup"><span data-stu-id="ad0ae-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="ad0ae-171">NuGet 會在目前的資料夾中尋找方案檔。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="ad0ae-172">如果找到單一檔案，則會使用該檔案來還原套件;如果找到多個解決方案，NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="ad0ae-173">如果沒有解決方案檔，NuGet 會尋找 `packages.config` 並使用該檔案來還原封裝。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="ad0ae-174">如果找不到任何解決方案或檔案 `packages.config` ，NuGet 會提供錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="ad0ae-175">使用下列優先權順序判斷套件資料夾 (如果找不到這些資料夾) ，NuGet 會產生錯誤：</span><span class="sxs-lookup"><span data-stu-id="ad0ae-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="ad0ae-176">使用指定的資料夾 `-PackagesDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="ad0ae-177">`repositoryPath`中的值`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="ad0ae-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="ad0ae-178">使用指定的資料夾 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="ad0ae-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="ad0ae-179">還原解決方案的套件時，NuGet 會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="ad0ae-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="ad0ae-180">載入方案檔。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-180">Loads the solution file.</span></span>
    - <span data-ttu-id="ad0ae-181">將中列出的方案層級封裝還原 `$(SolutionDir)\.nuget\packages.config` 到 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="ad0ae-182">將列出的封裝還原 `$(ProjectDir)\packages.config` 到 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="ad0ae-183">針對指定的每個封裝，以平行方式還原封裝，除非 `-DisableParallelProcessing` 指定了。</span><span class="sxs-lookup"><span data-stu-id="ad0ae-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="ad0ae-184">範例</span><span class="sxs-lookup"><span data-stu-id="ad0ae-184">Examples</span></span>

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
