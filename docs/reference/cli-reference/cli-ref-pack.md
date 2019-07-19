---
title: NuGet CLI 套件命令
description: Nuget.exe pack 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e12944bdd5d43b8b9e84908be480a5249dd924f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327655"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="80d65-103">pack 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="80d65-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="80d65-104">**適用于:** 套件建立&bullet; **支援的版本:** 2.7+</span><span class="sxs-lookup"><span data-stu-id="80d65-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="80d65-105">根據指定`.nuspec`的或專案檔, 建立 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="80d65-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="80d65-106">命令 (請參閱[dotnet 命令](../dotnet-Commands.md)) 和`msbuild -t:pack` (請參閱[MSBuild 目標](../msbuild-targets.md)) 可用來做為替代。 `dotnet pack`</span><span class="sxs-lookup"><span data-stu-id="80d65-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="80d65-107">在 Mono 底下, 不支援從專案檔建立封裝。</span><span class="sxs-lookup"><span data-stu-id="80d65-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="80d65-108">您也需要將檔案中的`.nuspec`非本機路徑調整為 Unix 樣式的路徑, 因為 nuget.exe 不會轉換 Windows 路徑類型本身。</span><span class="sxs-lookup"><span data-stu-id="80d65-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="80d65-109">使用量</span><span class="sxs-lookup"><span data-stu-id="80d65-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="80d65-110">其中`<nuspecPath>` , `<projectPath>`和分別`.nuspec`指定或專案檔。</span><span class="sxs-lookup"><span data-stu-id="80d65-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="80d65-111">選項</span><span class="sxs-lookup"><span data-stu-id="80d65-111">Options</span></span>

| <span data-ttu-id="80d65-112">選項</span><span class="sxs-lookup"><span data-stu-id="80d65-112">Option</span></span> | <span data-ttu-id="80d65-113">描述</span><span class="sxs-lookup"><span data-stu-id="80d65-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80d65-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="80d65-114">BasePath</span></span> | <span data-ttu-id="80d65-115">設定檔案中`.nuspec`定義之檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="80d65-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="80d65-116">組建</span><span class="sxs-lookup"><span data-stu-id="80d65-116">Build</span></span> | <span data-ttu-id="80d65-117">指定在建立封裝之前, 應該先建立專案。</span><span class="sxs-lookup"><span data-stu-id="80d65-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="80d65-118">排除</span><span class="sxs-lookup"><span data-stu-id="80d65-118">Exclude</span></span> | <span data-ttu-id="80d65-119">指定建立封裝時要排除的一或多個萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="80d65-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="80d65-120">若要指定一個以上的模式, 請重複-Exclude 旗標。</span><span class="sxs-lookup"><span data-stu-id="80d65-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="80d65-121">請參閱下列範例。</span><span class="sxs-lookup"><span data-stu-id="80d65-121">See example below.</span></span> |
| <span data-ttu-id="80d65-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="80d65-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="80d65-123">在建立封裝時, 防止包含空的目錄。</span><span class="sxs-lookup"><span data-stu-id="80d65-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="80d65-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="80d65-124">ForceEnglishOutput</span></span> | <span data-ttu-id="80d65-125">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="80d65-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="80d65-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="80d65-126">ConfigFile</span></span> | <span data-ttu-id="80d65-127">指定 pack 命令的設定檔案。</span><span class="sxs-lookup"><span data-stu-id="80d65-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="80d65-128">Help</span><span class="sxs-lookup"><span data-stu-id="80d65-128">Help</span></span> | <span data-ttu-id="80d65-129">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="80d65-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="80d65-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="80d65-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="80d65-131">表示建立的封裝應該將參考的專案包含為相依性或封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="80d65-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="80d65-132">如果參考的專案有與專案`.nuspec`同名的對應檔案, 則會將該參考的專案新增為相依性。</span><span class="sxs-lookup"><span data-stu-id="80d65-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="80d65-133">否則, 會將參考的專案新增為封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="80d65-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="80d65-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="80d65-134">MinClientVersion</span></span> | <span data-ttu-id="80d65-135">為已建立的封裝設定*minClientVersion*屬性。</span><span class="sxs-lookup"><span data-stu-id="80d65-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="80d65-136">這個值會覆寫檔案中`.nuspec`現有*minClientVersion*屬性的值 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="80d65-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="80d65-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="80d65-137">MSBuildPath</span></span> | <span data-ttu-id="80d65-138">*(4.0 +)* 指定要搭配命令使用之 MSBuild 的路徑, 其優先順序高於`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="80d65-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="80d65-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="80d65-139">MSBuildVersion</span></span> | <span data-ttu-id="80d65-140">*(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="80d65-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="80d65-141">支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="80d65-141">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="80d65-142">根據預設, 會挑選路徑中的 MSBuild, 否則會預設為 MSBuild 的最高安裝版本。</span><span class="sxs-lookup"><span data-stu-id="80d65-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="80d65-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="80d65-143">NoDefaultExcludes</span></span> | <span data-ttu-id="80d65-144">防止預設排除 NuGet 套件檔案和檔案和資料夾 (以點為`.svn`開頭), 例如和。 `.gitignore`</span><span class="sxs-lookup"><span data-stu-id="80d65-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="80d65-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="80d65-145">NoPackageAnalysis</span></span> | <span data-ttu-id="80d65-146">指定封裝不應該在建置套件之後執行套件分析。</span><span class="sxs-lookup"><span data-stu-id="80d65-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="80d65-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="80d65-147">OutputDirectory</span></span> | <span data-ttu-id="80d65-148">指定用來儲存所建立封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="80d65-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="80d65-149">如果未指定任何資料夾, 則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="80d65-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="80d65-150">屬性</span><span class="sxs-lookup"><span data-stu-id="80d65-150">Properties</span></span> | <span data-ttu-id="80d65-151">在其他選項之後, 應該會出現在命令列上的最後一個。</span><span class="sxs-lookup"><span data-stu-id="80d65-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="80d65-152">指定覆寫專案檔中值的屬性清單;請參閱屬性名稱的[一般 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)。</span><span class="sxs-lookup"><span data-stu-id="80d65-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="80d65-153">這裡的 Properties 引數是 token = 值組的清單 (以分號分隔), 其中每個`$token$`出現`.nuspec`在檔案中的會取代為指定的值。</span><span class="sxs-lookup"><span data-stu-id="80d65-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="80d65-154">值可以是以引號括住的字串。</span><span class="sxs-lookup"><span data-stu-id="80d65-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="80d65-155">請注意, 對於 "Configuration" 屬性, 預設值為 "Debug"。</span><span class="sxs-lookup"><span data-stu-id="80d65-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="80d65-156">若要變更為發行設定, 請`-Properties Configuration=Release`使用。</span><span class="sxs-lookup"><span data-stu-id="80d65-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="80d65-157">尾碼</span><span class="sxs-lookup"><span data-stu-id="80d65-157">Suffix</span></span> | <span data-ttu-id="80d65-158">*(3.4.4 +)* 將尾碼附加至內部產生的版本號碼, 通常用於附加組建或其他預先發行識別碼。</span><span class="sxs-lookup"><span data-stu-id="80d65-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="80d65-159">例如, 使用`-suffix nightly`將會建立具有版本號碼 (例如`1.2.3-nightly`) 的套件。</span><span class="sxs-lookup"><span data-stu-id="80d65-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="80d65-160">尾碼必須以字母開頭, 以避免與不同版本 NuGet 和 NuGet 套件管理員的警告、錯誤和潛在的不相容。</span><span class="sxs-lookup"><span data-stu-id="80d65-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="80d65-161">符號</span><span class="sxs-lookup"><span data-stu-id="80d65-161">Symbols</span></span> | <span data-ttu-id="80d65-162">指定封裝包含來源和符號。</span><span class="sxs-lookup"><span data-stu-id="80d65-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="80d65-163">搭配檔案使用`.nuspec`時, 這會建立一般的 NuGet 套件檔案和對應的符號套件。</span><span class="sxs-lookup"><span data-stu-id="80d65-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="80d65-164">根據預設, 它會建立[舊版符號套件](../../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="80d65-164">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="80d65-165">為符號套件新建議的格式為 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="80d65-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="80d65-166">請參閱[建立符號套件 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="80d65-166">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="80d65-167">工具</span><span class="sxs-lookup"><span data-stu-id="80d65-167">Tool</span></span> | <span data-ttu-id="80d65-168">指定專案的輸出檔案應該放在`tool`資料夾中。</span><span class="sxs-lookup"><span data-stu-id="80d65-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="80d65-169">Verbosity</span><span class="sxs-lookup"><span data-stu-id="80d65-169">Verbosity</span></span> | <span data-ttu-id="80d65-170">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="80d65-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="80d65-171">版本</span><span class="sxs-lookup"><span data-stu-id="80d65-171">Version</span></span> | <span data-ttu-id="80d65-172">覆寫檔案中`.nuspec`的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="80d65-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="80d65-173">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="80d65-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="80d65-174">排除開發相依性</span><span class="sxs-lookup"><span data-stu-id="80d65-174">Excluding development dependencies</span></span>

<span data-ttu-id="80d65-175">某些 NuGet 套件可作為開發相依性, 協助您撰寫自己的程式庫, 但不一定需要做為實際的封裝相依性。</span><span class="sxs-lookup"><span data-stu-id="80d65-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="80d65-176">此`pack`命令會忽略`package`中`packages.config` `developmentDependency`屬性設定為`true`的專案。</span><span class="sxs-lookup"><span data-stu-id="80d65-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="80d65-177">這些專案將不會包含在建立的封裝中做為相依性。</span><span class="sxs-lookup"><span data-stu-id="80d65-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="80d65-178">例如, 請考慮來源專案`packages.config`中的下列檔案:</span><span class="sxs-lookup"><span data-stu-id="80d65-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="80d65-179">針對此專案`nuget pack` , 所建立的封裝會相依于`jQuery`和, `microsoft-web-helpers`但不`netfx-Guard`會。</span><span class="sxs-lookup"><span data-stu-id="80d65-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="80d65-180">範例</span><span class="sxs-lookup"><span data-stu-id="80d65-180">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
