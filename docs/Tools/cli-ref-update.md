---
title: "NuGet CLI 更新命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 更新命令的參考"
keywords: "nuget 更新參考更新套件 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a788244d23354b980e8fa86fa170740c18f17b2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="f3f50-104">update 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f3f50-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="f3f50-105">**適用於：**封裝耗用量&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="f3f50-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f3f50-106">更新專案中的所有封裝 (使用`packages.config`) 為其最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="f3f50-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="f3f50-107">建議您執行['restore'](cli-ref-restore.md)再執行`update`。</span><span class="sxs-lookup"><span data-stu-id="f3f50-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="f3f50-108">(若要更新個別的封裝，請使用[ `nuget install` ](cli-ref-install.md)但未指定版本號碼，case NuGet 會安裝最新版本。)</span><span class="sxs-lookup"><span data-stu-id="f3f50-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="f3f50-109">注意：`update`不適用於 CLI 下執行，單聲道 （Mac OSX 或 Linux） 或使用 PackageReference 格式時。</span><span class="sxs-lookup"><span data-stu-id="f3f50-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="f3f50-110">`update`命令也會更新專案檔中的組件參考、 提供的參考已經存在。</span><span class="sxs-lookup"><span data-stu-id="f3f50-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="f3f50-111">如果已更新的封裝加入組件，新的參考是*不*加入。</span><span class="sxs-lookup"><span data-stu-id="f3f50-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="f3f50-112">新的封裝相依性也不需要加入其組件參考。</span><span class="sxs-lookup"><span data-stu-id="f3f50-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="f3f50-113">若要更新的組件中包含這些作業，請更新 Visual Studio 中使用封裝管理員 UI 或 Package Manager Console 中的封裝。</span><span class="sxs-lookup"><span data-stu-id="f3f50-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="f3f50-114">此命令也可用來更新本身 nuget.exe 使用*-自我*旗標。</span><span class="sxs-lookup"><span data-stu-id="f3f50-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="f3f50-115">使用量</span><span class="sxs-lookup"><span data-stu-id="f3f50-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="f3f50-116">其中`<configPath>`識別其中`packages.config`或列出專案的相依性的方案檔。</span><span class="sxs-lookup"><span data-stu-id="f3f50-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="f3f50-117">選項</span><span class="sxs-lookup"><span data-stu-id="f3f50-117">Options</span></span>

| <span data-ttu-id="f3f50-118">選項</span><span class="sxs-lookup"><span data-stu-id="f3f50-118">Option</span></span> | <span data-ttu-id="f3f50-119">描述</span><span class="sxs-lookup"><span data-stu-id="f3f50-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3f50-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f3f50-120">ConfigFile</span></span> | <span data-ttu-id="f3f50-121">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="f3f50-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f3f50-122">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="f3f50-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f3f50-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f3f50-123">FileConflictAction</span></span> | <span data-ttu-id="f3f50-124">指定當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="f3f50-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f3f50-125">值為*覆寫，忽略無*。</span><span class="sxs-lookup"><span data-stu-id="f3f50-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="f3f50-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f3f50-126">ForceEnglishOutput</span></span> | <span data-ttu-id="f3f50-127">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="f3f50-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f3f50-128">說明</span><span class="sxs-lookup"><span data-stu-id="f3f50-128">Help</span></span> | <span data-ttu-id="f3f50-129">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="f3f50-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="f3f50-130">ID</span><span class="sxs-lookup"><span data-stu-id="f3f50-130">Id</span></span> | <span data-ttu-id="f3f50-131">指定封裝識別碼，以更新的清單。</span><span class="sxs-lookup"><span data-stu-id="f3f50-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="f3f50-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="f3f50-132">MSBuildPath</span></span> | <span data-ttu-id="f3f50-133">*（4.0 +)*指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="f3f50-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="f3f50-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="f3f50-134">MSBuildVersion</span></span> | <span data-ttu-id="f3f50-135">*（3.2 +)*指定要搭配此命令使用 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="f3f50-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="f3f50-136">支援的值為 4，12，14，15。</span><span class="sxs-lookup"><span data-stu-id="f3f50-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="f3f50-137">根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="f3f50-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="f3f50-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f3f50-138">NonInteractive</span></span> | <span data-ttu-id="f3f50-139">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="f3f50-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f3f50-140">發行前版本</span><span class="sxs-lookup"><span data-stu-id="f3f50-140">PreRelease</span></span> | <span data-ttu-id="f3f50-141">可讓更新的發行前版本。</span><span class="sxs-lookup"><span data-stu-id="f3f50-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="f3f50-142">更新已安裝的套件發行前版本時，則不需要此旗標。</span><span class="sxs-lookup"><span data-stu-id="f3f50-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="f3f50-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="f3f50-143">RepositoryPath</span></span> | <span data-ttu-id="f3f50-144">指定已安裝的套件的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3f50-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="f3f50-145">安全</span><span class="sxs-lookup"><span data-stu-id="f3f50-145">Safe</span></span> | <span data-ttu-id="f3f50-146">指定，只更新相同的主要和次要版本中可用的最高版本時已安裝的封裝將會安裝。</span><span class="sxs-lookup"><span data-stu-id="f3f50-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="f3f50-147">自我</span><span class="sxs-lookup"><span data-stu-id="f3f50-147">Self</span></span> | <span data-ttu-id="f3f50-148">Nuget.exe 更新為最新版本。所有其他引數會被忽略。</span><span class="sxs-lookup"><span data-stu-id="f3f50-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="f3f50-149">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="f3f50-149">Source</span></span> | <span data-ttu-id="f3f50-150">指定封裝來源清單 （Url) 若要使用的更新。</span><span class="sxs-lookup"><span data-stu-id="f3f50-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="f3f50-151">如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="f3f50-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="f3f50-152">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f3f50-152">Verbosity</span></span> | <span data-ttu-id="f3f50-153">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="f3f50-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="f3f50-154">版本</span><span class="sxs-lookup"><span data-stu-id="f3f50-154">Version</span></span> | <span data-ttu-id="f3f50-155">一個封裝識別碼搭配使用時，指定要更新之封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="f3f50-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="f3f50-156">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f3f50-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f3f50-157">範例</span><span class="sxs-lookup"><span data-stu-id="f3f50-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
