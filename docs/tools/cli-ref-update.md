---
title: NuGet CLI 更新命令
description: Nuget.exe 更新命令參考
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425912"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="a6764-103">update 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a6764-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="a6764-104">**適用於：** 套件耗用量&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="a6764-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a6764-105">更新專案中的所有封裝 (使用`packages.config`) 為最新可用版本。</span><span class="sxs-lookup"><span data-stu-id="a6764-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="a6764-106">建議您執行['restore'](cli-ref-restore.md)再執行`update`。</span><span class="sxs-lookup"><span data-stu-id="a6764-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="a6764-107">(若要更新個別的封裝，請使用[ `nuget install` ](cli-ref-install.md)但未指定版本號碼，寫 NuGet 會安裝最新版本。)</span><span class="sxs-lookup"><span data-stu-id="a6764-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="a6764-108">注意：`update`不適用於下執行，Mono （Mac OSX 或 Linux） 或使用 PackageReference 格式時的 CLI。</span><span class="sxs-lookup"><span data-stu-id="a6764-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="a6764-109">`update`命令也會更新專案檔中的組件參考，前提是這些參考已經存在。</span><span class="sxs-lookup"><span data-stu-id="a6764-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="a6764-110">已更新的封裝已加入之組件，新的參考是否*不*加入。</span><span class="sxs-lookup"><span data-stu-id="a6764-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="a6764-111">新的套件相依性也不需要加入其組件參考。</span><span class="sxs-lookup"><span data-stu-id="a6764-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="a6764-112">若要更新的組件中包含這些作業，請更新 Visual Studio 中使用套件管理員 UI 或套件管理員主控台中的封裝。</span><span class="sxs-lookup"><span data-stu-id="a6764-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="a6764-113">此命令也可用來更新本身的 nuget.exe 使用 *-自我*旗標。</span><span class="sxs-lookup"><span data-stu-id="a6764-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="a6764-114">使用量</span><span class="sxs-lookup"><span data-stu-id="a6764-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="a6764-115">何處`<configPath>`識別其中`packages.config`或列出專案的相依性的方案檔。</span><span class="sxs-lookup"><span data-stu-id="a6764-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="a6764-116">選項</span><span class="sxs-lookup"><span data-stu-id="a6764-116">Options</span></span>

| <span data-ttu-id="a6764-117">選項</span><span class="sxs-lookup"><span data-stu-id="a6764-117">Option</span></span> | <span data-ttu-id="a6764-118">描述</span><span class="sxs-lookup"><span data-stu-id="a6764-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6764-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a6764-119">ConfigFile</span></span> | <span data-ttu-id="a6764-120">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="a6764-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a6764-121">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="a6764-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a6764-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="a6764-122">FileConflictAction</span></span> | <span data-ttu-id="a6764-123">指定當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="a6764-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="a6764-124">值為*覆寫，請忽略無*。</span><span class="sxs-lookup"><span data-stu-id="a6764-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="a6764-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a6764-125">ForceEnglishOutput</span></span> | <span data-ttu-id="a6764-126">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="a6764-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a6764-127">Help</span><span class="sxs-lookup"><span data-stu-id="a6764-127">Help</span></span> | <span data-ttu-id="a6764-128">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="a6764-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="a6764-129">ID</span><span class="sxs-lookup"><span data-stu-id="a6764-129">Id</span></span> | <span data-ttu-id="a6764-130">指定封裝識別碼，以更新的清單。</span><span class="sxs-lookup"><span data-stu-id="a6764-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="a6764-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="a6764-131">MSBuildPath</span></span> | <span data-ttu-id="a6764-132">*（4.0 +)* 指定要搭配命令，優先於使用 MSBuild 的路徑`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="a6764-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="a6764-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="a6764-133">MSBuildVersion</span></span> | <span data-ttu-id="a6764-134">*（3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="a6764-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="a6764-135">支援的值為 4、 12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7，15.8、 15.9。</span><span class="sxs-lookup"><span data-stu-id="a6764-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="a6764-136">根據您的路徑中的 MSBuild 會挑出的預設值，否則，預設已安裝的最高的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="a6764-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="a6764-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a6764-137">NonInteractive</span></span> | <span data-ttu-id="a6764-138">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="a6764-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a6764-139">發行前版本</span><span class="sxs-lookup"><span data-stu-id="a6764-139">PreRelease</span></span> | <span data-ttu-id="a6764-140">可讓更新為發行前版本。</span><span class="sxs-lookup"><span data-stu-id="a6764-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="a6764-141">更新已安裝的發行前版本套件時，則不需要此旗標。</span><span class="sxs-lookup"><span data-stu-id="a6764-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="a6764-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="a6764-142">RepositoryPath</span></span> | <span data-ttu-id="a6764-143">指定已安裝套件的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="a6764-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="a6764-144">安全</span><span class="sxs-lookup"><span data-stu-id="a6764-144">Safe</span></span> | <span data-ttu-id="a6764-145">指定，只會更新與在相同的主要和次要版本內可用的最高版本將會安裝已安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="a6764-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="a6764-146">自助</span><span class="sxs-lookup"><span data-stu-id="a6764-146">Self</span></span> | <span data-ttu-id="a6764-147">Nuget.exe 更新為最新的版本;所有其他引數會被忽略。</span><span class="sxs-lookup"><span data-stu-id="a6764-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="a6764-148">Source</span><span class="sxs-lookup"><span data-stu-id="a6764-148">Source</span></span> | <span data-ttu-id="a6764-149">指定封裝來源清單 （Url) 若要使用的更新。</span><span class="sxs-lookup"><span data-stu-id="a6764-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="a6764-150">如果省略，則此命令會使用組態檔中提供的來源，請參閱 <<c0> [ 常見的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="a6764-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="a6764-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a6764-151">Verbosity</span></span> | <span data-ttu-id="a6764-152">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="a6764-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="a6764-153">版本</span><span class="sxs-lookup"><span data-stu-id="a6764-153">Version</span></span> | <span data-ttu-id="a6764-154">一個套件識別碼搭配使用時，指定要更新之封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="a6764-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="a6764-155">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a6764-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a6764-156">範例</span><span class="sxs-lookup"><span data-stu-id="a6764-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
