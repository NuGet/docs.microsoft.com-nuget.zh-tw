---
title: NuGet CLI pack 命令
description: Nuget.exe pack 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c3a01b7747be96f02f7b93b3bf66f5d1783ceed7
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842545"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="75d7c-103">pack 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="75d7c-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="75d7c-104">**適用於：** 封裝建立&bullet;**支援的版本：** 2.7+</span><span class="sxs-lookup"><span data-stu-id="75d7c-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="75d7c-105">建立根據指定的 NuGet 套件`.nuspec`或專案檔。</span><span class="sxs-lookup"><span data-stu-id="75d7c-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="75d7c-106">`dotnet pack`命令 (請參閱 < [dotnet 命令](dotnet-Commands.md)) 及`msbuild -t:pack`(請參閱[MSBuild 目標](../reference/msbuild-targets.md)) 可作為替代項目。</span><span class="sxs-lookup"><span data-stu-id="75d7c-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="75d7c-107">在 Mono 下不支援從專案檔中建立封裝。</span><span class="sxs-lookup"><span data-stu-id="75d7c-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="75d7c-108">您也需要調整中的非區域路徑`.nuspec`檔案為 Unix 樣式的路徑，nuget.exe 不會將轉換本身的 Windows 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="75d7c-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="75d7c-109">使用量</span><span class="sxs-lookup"><span data-stu-id="75d7c-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="75d7c-110">何處`<nuspecPath>`並`<projectPath>`指定`.nuspec`或專案檔，分別。</span><span class="sxs-lookup"><span data-stu-id="75d7c-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="75d7c-111">選項</span><span class="sxs-lookup"><span data-stu-id="75d7c-111">Options</span></span>

| <span data-ttu-id="75d7c-112">選項</span><span class="sxs-lookup"><span data-stu-id="75d7c-112">Option</span></span> | <span data-ttu-id="75d7c-113">說明</span><span class="sxs-lookup"><span data-stu-id="75d7c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75d7c-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="75d7c-114">BasePath</span></span> | <span data-ttu-id="75d7c-115">設定檔案中定義的基底路徑`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="75d7c-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="75d7c-116">組建</span><span class="sxs-lookup"><span data-stu-id="75d7c-116">Build</span></span> | <span data-ttu-id="75d7c-117">指定應該在建置封裝之前建置專案。</span><span class="sxs-lookup"><span data-stu-id="75d7c-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="75d7c-118">排除</span><span class="sxs-lookup"><span data-stu-id="75d7c-118">Exclude</span></span> | <span data-ttu-id="75d7c-119">指定建立封裝時所要排除的一個或多個萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="75d7c-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="75d7c-120">若要指定一個以上的模式，請重複-排除旗標。</span><span class="sxs-lookup"><span data-stu-id="75d7c-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="75d7c-121">請參閱以下的範例。</span><span class="sxs-lookup"><span data-stu-id="75d7c-121">See example below.</span></span> |
| <span data-ttu-id="75d7c-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="75d7c-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="75d7c-123">建置套件時，可避免包含空的目錄。</span><span class="sxs-lookup"><span data-stu-id="75d7c-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="75d7c-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="75d7c-124">ForceEnglishOutput</span></span> | <span data-ttu-id="75d7c-125">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="75d7c-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="75d7c-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="75d7c-126">ConfigFile</span></span> | <span data-ttu-id="75d7c-127">指定組件命令的組態檔。</span><span class="sxs-lookup"><span data-stu-id="75d7c-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="75d7c-128">Help</span><span class="sxs-lookup"><span data-stu-id="75d7c-128">Help</span></span> | <span data-ttu-id="75d7c-129">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="75d7c-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="75d7c-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="75d7c-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="75d7c-131">指出已建置的套件應包含參考的專案，做為相依性，或是做為封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="75d7c-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="75d7c-132">如果參考的專案都有對應`.nuspec`有同名的專案，則該參考的專案新增為相依性的檔案。</span><span class="sxs-lookup"><span data-stu-id="75d7c-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="75d7c-133">否則參考的專案新增為套件的一部分。</span><span class="sxs-lookup"><span data-stu-id="75d7c-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="75d7c-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="75d7c-134">MinClientVersion</span></span> | <span data-ttu-id="75d7c-135">設定*minClientVersion*屬性建立的封裝。</span><span class="sxs-lookup"><span data-stu-id="75d7c-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="75d7c-136">這個值會覆寫現有的值*minClientVersion*中的屬性 （如果有的話）`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="75d7c-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="75d7c-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="75d7c-137">MSBuildPath</span></span> | <span data-ttu-id="75d7c-138">*（4.0 +)* 指定要搭配命令，優先於使用 MSBuild 的路徑`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="75d7c-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="75d7c-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="75d7c-139">MSBuildVersion</span></span> | <span data-ttu-id="75d7c-140">*（3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="75d7c-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="75d7c-141">支援的值為 4、 12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7，15.8、 15.9。</span><span class="sxs-lookup"><span data-stu-id="75d7c-141">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="75d7c-142">根據您的路徑中的 MSBuild 會挑出的預設值，否則，預設已安裝的最高的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="75d7c-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="75d7c-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="75d7c-143">NoDefaultExcludes</span></span> | <span data-ttu-id="75d7c-144">會防止預設排除的 NuGet 封裝檔案和檔案和資料夾從一個點，例如`.svn`和`.gitignore`。</span><span class="sxs-lookup"><span data-stu-id="75d7c-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="75d7c-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="75d7c-145">NoPackageAnalysis</span></span> | <span data-ttu-id="75d7c-146">指定封裝不應該在建置套件之後執行套件分析。</span><span class="sxs-lookup"><span data-stu-id="75d7c-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="75d7c-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="75d7c-147">OutputDirectory</span></span> | <span data-ttu-id="75d7c-148">指定建立的封裝儲存所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="75d7c-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="75d7c-149">如果未不指定任何資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="75d7c-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="75d7c-150">屬性</span><span class="sxs-lookup"><span data-stu-id="75d7c-150">Properties</span></span> | <span data-ttu-id="75d7c-151">應該會出現在命令列上的最後一個之後的其他選項。</span><span class="sxs-lookup"><span data-stu-id="75d7c-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="75d7c-152">指定專案檔案中的值會覆寫的屬性的清單請參閱[通用的 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="75d7c-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="75d7c-153">屬性引數是一份權杖 = 值 」 配對，並以分號區隔，其中出現的每個`$token$`在`.nuspec`檔案將會取代指定的值。</span><span class="sxs-lookup"><span data-stu-id="75d7c-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="75d7c-154">值可以是以引號的字串。</span><span class="sxs-lookup"><span data-stu-id="75d7c-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="75d7c-155">請注意，「 組態 」 屬性，預設值是"Debug"。</span><span class="sxs-lookup"><span data-stu-id="75d7c-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="75d7c-156">若要變更的發行組態，使用`-Properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="75d7c-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="75d7c-157">尾碼</span><span class="sxs-lookup"><span data-stu-id="75d7c-157">Suffix</span></span> | <span data-ttu-id="75d7c-158">*(3.4.4+)* 將後置字元附加至內部產生的版本號碼，通常用來附加組建或其他發行前版本識別項。</span><span class="sxs-lookup"><span data-stu-id="75d7c-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="75d7c-159">例如，使用`-suffix nightly`將建立一個封裝的版本號碼的按讚與`1.2.3-nightly`。</span><span class="sxs-lookup"><span data-stu-id="75d7c-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="75d7c-160">後置字元的開頭必須是字母，以避免警告、 錯誤和潛在的不相容，使用不同版本的 NuGet 和 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="75d7c-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="75d7c-161">符號</span><span class="sxs-lookup"><span data-stu-id="75d7c-161">Symbols</span></span> | <span data-ttu-id="75d7c-162">指定封裝包含來源和符號。</span><span class="sxs-lookup"><span data-stu-id="75d7c-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="75d7c-163">當搭配`.nuspec`檔案，這會建立一般的 NuGet 封裝檔案和對應的符號套件。</span><span class="sxs-lookup"><span data-stu-id="75d7c-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="75d7c-164">依預設它會建立[舊版的符號套件](../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="75d7c-164">By default it creates a [legacy symbol package](../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="75d7c-165">為符號套件新建議的格式為 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="75d7c-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="75d7c-166">請參閱[建立符號套件 (.snupkg)](../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="75d7c-166">See [Creating symbol packages (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="75d7c-167">SymbolPackageFormat</span><span class="sxs-lookup"><span data-stu-id="75d7c-167">SymbolPackageFormat</span></span> | <span data-ttu-id="75d7c-168">指定符號套件的格式： *.symbols.nupkg* （舊版） 或*snupkg* （建議選項）。</span><span class="sxs-lookup"><span data-stu-id="75d7c-168">Specifies the symbols package's format: *symbols.nupkg* (legacy) or *snupkg* (recommended).</span></span> <span data-ttu-id="75d7c-169">依預設它會建立[舊版的符號套件](../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="75d7c-169">By default it creates a [legacy symbol package](../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="75d7c-170">請參閱[建立符號套件 (.snupkg)](../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="75d7c-170">See [Creating symbol packages (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="75d7c-171">工具</span><span class="sxs-lookup"><span data-stu-id="75d7c-171">Tool</span></span> | <span data-ttu-id="75d7c-172">指定專案的輸出檔案應該放在`tool`資料夾。</span><span class="sxs-lookup"><span data-stu-id="75d7c-172">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="75d7c-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="75d7c-173">Verbosity</span></span> | <span data-ttu-id="75d7c-174">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="75d7c-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="75d7c-175">版本</span><span class="sxs-lookup"><span data-stu-id="75d7c-175">Version</span></span> | <span data-ttu-id="75d7c-176">覆寫的版本號碼，從`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="75d7c-176">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="75d7c-177">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="75d7c-177">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="75d7c-178">排除開發相依性</span><span class="sxs-lookup"><span data-stu-id="75d7c-178">Excluding development dependencies</span></span>

<span data-ttu-id="75d7c-179">部分 NuGet 套件適合做為開發相依性，協助您撰寫自己的程式庫，但不一定需要做為實際的套件相依性。</span><span class="sxs-lookup"><span data-stu-id="75d7c-179">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="75d7c-180">`pack`命令將會忽略`package`中的項目`packages.config`具有`developmentDependency`屬性設為`true`。</span><span class="sxs-lookup"><span data-stu-id="75d7c-180">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="75d7c-181">這些項目不會包含做為建立的封裝中的相依性。</span><span class="sxs-lookup"><span data-stu-id="75d7c-181">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="75d7c-182">例如，請考慮下列`packages.config`來源專案檔中：</span><span class="sxs-lookup"><span data-stu-id="75d7c-182">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="75d7c-183">此專案中，封裝建立的`nuget pack`會有相依性`jQuery`並`microsoft-web-helpers`而非`netfx-Guard`。</span><span class="sxs-lookup"><span data-stu-id="75d7c-183">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="75d7c-184">範例</span><span class="sxs-lookup"><span data-stu-id="75d7c-184">Examples</span></span>

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
