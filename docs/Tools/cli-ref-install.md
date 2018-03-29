---
title: NuGet CLI 安裝命令 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 安裝命令的參考
keywords: nuget 安裝參考時，安裝套件 命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 121d7b50767f1d466d6d0d8494f324b02d8ff6f1
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="f399f-104">安裝命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f399f-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="f399f-105">**適用於：**封裝耗用量&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="f399f-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f399f-106">下載並安裝到專案，將預設為目前的資料夾，使用指定的封裝來源的封裝。</span><span class="sxs-lookup"><span data-stu-id="f399f-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="f399f-107">若要下載的封裝，直接在專案內容之外，請瀏覽封裝的頁面上[nuget.org](https://www.nuget.org)選取**下載**連結。</span><span class="sxs-lookup"><span data-stu-id="f399f-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="f399f-108">如果未不指定任何來源，列出全域組態檔中， `%appdata%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，會使用。</span><span class="sxs-lookup"><span data-stu-id="f399f-108">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="f399f-109">請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f399f-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="f399f-110">如果未不指定任何特定的封裝，`install`將列在專案中的所有封裝都安裝`packages.config`檔案，讓它變成類似[ `restore` ](cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="f399f-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="f399f-111">`install`命令不會修改專案檔或`packages.config`; 如此一來，類似於`restore`，只能將封裝新增至磁碟，但不會變更專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="f399f-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="f399f-112">若要加入相依性，請在 Visual Studio 中，將透過封裝管理員 UI 或主控台專案，或是修改`packages.config`，然後執行 `install`或`restore`。</span><span class="sxs-lookup"><span data-stu-id="f399f-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="f399f-113">使用量</span><span class="sxs-lookup"><span data-stu-id="f399f-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="f399f-114">其中`<packageID>`名稱 （使用最新版本） 來安裝封裝或`<configFilePath>`識別`packages.config`檔案，其中列出要安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="f399f-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="f399f-115">您可以指定特定版本與`-Version`選項。</span><span class="sxs-lookup"><span data-stu-id="f399f-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="f399f-116">選項</span><span class="sxs-lookup"><span data-stu-id="f399f-116">Options</span></span>

| <span data-ttu-id="f399f-117">選項</span><span class="sxs-lookup"><span data-stu-id="f399f-117">Option</span></span> | <span data-ttu-id="f399f-118">描述</span><span class="sxs-lookup"><span data-stu-id="f399f-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f399f-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f399f-119">ConfigFile</span></span> | <span data-ttu-id="f399f-120">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="f399f-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f399f-121">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="f399f-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f399f-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f399f-122">DependencyVersion</span></span> | <span data-ttu-id="f399f-123">*（4.4 +)*指定特定版本，覆寫預設相依性解析行為。</span><span class="sxs-lookup"><span data-stu-id="f399f-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="f399f-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="f399f-124">DisableParallelProcessing</span></span> | <span data-ttu-id="f399f-125">安裝多個封裝，以平行方式停用。</span><span class="sxs-lookup"><span data-stu-id="f399f-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="f399f-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="f399f-126">ExcludeVersion</span></span> | <span data-ttu-id="f399f-127">會封裝安裝到名為與封裝名稱和版本號碼。</span><span class="sxs-lookup"><span data-stu-id="f399f-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="f399f-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="f399f-128">FallbackSource</span></span> | <span data-ttu-id="f399f-129">*（3.2 +)*作為後援，萬一主要中找不到封裝的封裝來源的清單或預設的來源。</span><span class="sxs-lookup"><span data-stu-id="f399f-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="f399f-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f399f-130">ForceEnglishOutput</span></span> | <span data-ttu-id="f399f-131">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="f399f-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f399f-132">架構</span><span class="sxs-lookup"><span data-stu-id="f399f-132">Framework</span></span> | <span data-ttu-id="f399f-133">*（4.4 +)*用於選取的相依性的目標 framework。</span><span class="sxs-lookup"><span data-stu-id="f399f-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="f399f-134">預設值是 'Any' 如果未指定。</span><span class="sxs-lookup"><span data-stu-id="f399f-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="f399f-135">說明</span><span class="sxs-lookup"><span data-stu-id="f399f-135">Help</span></span> | <span data-ttu-id="f399f-136">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="f399f-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="f399f-137">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="f399f-137">NoCache</span></span> | <span data-ttu-id="f399f-138">NuGet 可防止使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="f399f-138">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="f399f-139">請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="f399f-139">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="f399f-140">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f399f-140">NonInteractive</span></span> | <span data-ttu-id="f399f-141">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="f399f-141">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f399f-142">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="f399f-142">OutputDirectory</span></span> | <span data-ttu-id="f399f-143">指定在其中安裝封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f399f-143">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="f399f-144">如果沒有指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f399f-144">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="f399f-145">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="f399f-145">PackageSaveMode</span></span> | <span data-ttu-id="f399f-146">指定要儲存封裝的安裝後的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。</span><span class="sxs-lookup"><span data-stu-id="f399f-146">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="f399f-147">發行前版本</span><span class="sxs-lookup"><span data-stu-id="f399f-147">PreRelease</span></span> | <span data-ttu-id="f399f-148">允許安裝的套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="f399f-148">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="f399f-149">還原的封裝時，不需要此旗標`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="f399f-149">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="f399f-150">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="f399f-150">RequireConsent</span></span> | <span data-ttu-id="f399f-151">確認一次還原封裝才能下載和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="f399f-151">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="f399f-152">如需詳細資訊，請參閱[封裝還原，](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="f399f-152">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="f399f-153">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="f399f-153">SolutionDirectory</span></span> | <span data-ttu-id="f399f-154">指定要還原封裝方案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="f399f-154">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="f399f-155">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="f399f-155">Source</span></span> | <span data-ttu-id="f399f-156">指定封裝來源清單 （Url) 使用。</span><span class="sxs-lookup"><span data-stu-id="f399f-156">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="f399f-157">如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="f399f-157">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="f399f-158">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f399f-158">Verbosity</span></span> | <span data-ttu-id="f399f-159">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="f399f-159">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="f399f-160">版本</span><span class="sxs-lookup"><span data-stu-id="f399f-160">Version</span></span> | <span data-ttu-id="f399f-161">指定要安裝之封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="f399f-161">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="f399f-162">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f399f-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f399f-163">範例</span><span class="sxs-lookup"><span data-stu-id="f399f-163">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
