---
title: NuGet CLI 套件命令
description: nuget.exe pack 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780041"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="89a7e-103"> (NuGet CLI 的 pack 命令) </span><span class="sxs-lookup"><span data-stu-id="89a7e-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="89a7e-104">**適用物件：** 套件建立 &bullet; **支援的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="89a7e-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="89a7e-105">根據指定的 [nuspec](../nuspec.md) 或專案檔建立 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="89a7e-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="89a7e-106">`dotnet pack`命令 (查看[dotnet 命令](../dotnet-Commands.md)) 和 `msbuild -t:pack` (查看[MSBuild 目標](../msbuild-targets.md)) 可作為替代項使用。</span><span class="sxs-lookup"><span data-stu-id="89a7e-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="89a7e-107">使用 [`dotnet pack`](../dotnet-Commands.md) 或 [`msbuild -t:pack`](../msbuild-targets.md) 針對以 [PackageReference](../../consume-packages/package-references-in-project-files.md) 為基礎的專案。</span><span class="sxs-lookup"><span data-stu-id="89a7e-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="89a7e-108">在 Mono 下，不支援從專案檔建立套件。</span><span class="sxs-lookup"><span data-stu-id="89a7e-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="89a7e-109">您也需要將檔案中的非本機路徑調整 `.nuspec` 為 Unix 樣式的路徑，因為 nuget.exe 不會轉換 Windows 路徑路徑本身。</span><span class="sxs-lookup"><span data-stu-id="89a7e-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="89a7e-110">使用方式</span><span class="sxs-lookup"><span data-stu-id="89a7e-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="89a7e-111">where `<nuspecPath>` 和 `<projectPath>` 分別指定 `.nuspec` 或專案檔。</span><span class="sxs-lookup"><span data-stu-id="89a7e-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="89a7e-112">選項。</span><span class="sxs-lookup"><span data-stu-id="89a7e-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="89a7e-113">設定 [nuspec](../nuspec.md) 檔中定義之檔案的基底路徑。</span><span class="sxs-lookup"><span data-stu-id="89a7e-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="89a7e-114">指定專案應該在建立封裝之前建立。</span><span class="sxs-lookup"><span data-stu-id="89a7e-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="89a7e-115">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="89a7e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="89a7e-116">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="89a7e-117">指定建立封裝時要排除的一或多個萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="89a7e-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="89a7e-118">若要指定一個以上的模式，請重複-Exclude 旗標。</span><span class="sxs-lookup"><span data-stu-id="89a7e-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="89a7e-119">請參閱以下的範例。</span><span class="sxs-lookup"><span data-stu-id="89a7e-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="89a7e-120">在建立封裝時防止包含空的目錄。</span><span class="sxs-lookup"><span data-stu-id="89a7e-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="89a7e-121">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="89a7e-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="89a7e-122">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="89a7e-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="89a7e-123">表示建立的封裝應該將參考的專案包含為相依性或封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="89a7e-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="89a7e-124">如果參考的專案具有與專案同名的對應檔案 `.nuspec` ，則會將該參考的專案新增為相依性。</span><span class="sxs-lookup"><span data-stu-id="89a7e-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="89a7e-125">否則，會將參考的專案新增為封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="89a7e-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="89a7e-126">指定命令是否應準備套件輸出目錄，以支援共用作為摘要。</span><span class="sxs-lookup"><span data-stu-id="89a7e-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="89a7e-127">為建立的封裝設定 *minClientVersion* 屬性。</span><span class="sxs-lookup"><span data-stu-id="89a7e-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="89a7e-128">如果檔案中有任何) ，此值會覆寫現有 *minClientVersion* 屬性 (的值 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="89a7e-129">*(4.0 +)* 指定要搭配命令使用的 MSBuild 路徑，優先順序高於 `-MSBuildVersion` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="89a7e-130">*(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。</span><span class="sxs-lookup"><span data-stu-id="89a7e-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="89a7e-131">支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。</span><span class="sxs-lookup"><span data-stu-id="89a7e-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="89a7e-132">依預設，會挑選路徑中的 MSBuild，否則會預設為 MSBuild 的最高安裝版本。</span><span class="sxs-lookup"><span data-stu-id="89a7e-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="89a7e-133">防止預設排除 NuGet 套件檔案，以及以點（例如和）開頭的檔案和 `.svn` 資料夾 `.gitignore` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="89a7e-134">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="89a7e-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="89a7e-135">指定封裝不應該在建置套件之後執行套件分析。</span><span class="sxs-lookup"><span data-stu-id="89a7e-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="89a7e-136">指定儲存建立之封裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="89a7e-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="89a7e-137">如果未指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="89a7e-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="89a7e-138">指定命令是否應該在沒有版本的情況下準備套件輸出名稱。</span><span class="sxs-lookup"><span data-stu-id="89a7e-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="89a7e-139">指定封裝資料夾。</span><span class="sxs-lookup"><span data-stu-id="89a7e-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="89a7e-140">在其他選項之後，應該會出現在命令列上。</span><span class="sxs-lookup"><span data-stu-id="89a7e-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="89a7e-141">指定覆寫專案檔中值的屬性清單;請參閱屬性名稱的 [一般 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties) 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="89a7e-142">此處的 Properties 引數是 token = 值組的清單（以分號分隔），其中檔案中的每個出現專案 `$token$` `.nuspec` 都會以指定的值取代。</span><span class="sxs-lookup"><span data-stu-id="89a7e-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="89a7e-143">值可以是以引號括住的字串。</span><span class="sxs-lookup"><span data-stu-id="89a7e-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="89a7e-144">請注意，針對 "Configuration" 屬性，預設值為 "Debug"。</span><span class="sxs-lookup"><span data-stu-id="89a7e-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="89a7e-145">若要變更為發行設定，請使用 `-Properties Configuration=Release` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="89a7e-146">**一般而言**，屬性應該與對應的專案組建期間所使用的屬性相同，以避免可能奇怪的行為。</span><span class="sxs-lookup"><span data-stu-id="89a7e-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="89a7e-147">指定方案目錄。</span><span class="sxs-lookup"><span data-stu-id="89a7e-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="89a7e-148">*(3.4.4 +)* 將尾碼附加至內部產生的版本號碼，通常用於附加組建或其他發行前版本識別碼。</span><span class="sxs-lookup"><span data-stu-id="89a7e-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="89a7e-149">例如，使用 `-suffix nightly` 會建立版本號碼類似的封裝 `1.2.3-nightly` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="89a7e-150">尾碼必須以字母開頭，以避免與不同版本的 NuGet 和 NuGet 封裝管理員的警告、錯誤和潛在不相容。</span><span class="sxs-lookup"><span data-stu-id="89a7e-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="89a7e-151">建立符號封裝時，可讓您選擇 `snupkg` 和 `symbols.nupkg` 格式。</span><span class="sxs-lookup"><span data-stu-id="89a7e-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="89a7e-152">指定封裝包含來源和符號。</span><span class="sxs-lookup"><span data-stu-id="89a7e-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="89a7e-153">搭配檔案使用時 `.nuspec` ，會建立一般的 NuGet 套件檔案和對應的符號套件。</span><span class="sxs-lookup"><span data-stu-id="89a7e-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="89a7e-154">依預設，它會建立 [舊版符號套件](../../create-packages/Symbol-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="89a7e-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="89a7e-155">為符號套件新建議的格式為 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="89a7e-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="89a7e-156">請參閱[建立符號套件 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="89a7e-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="89a7e-157">指定專案的輸出檔應放置在 `tool` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="89a7e-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="89a7e-158">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="89a7e-159">覆寫檔案中的版本號碼 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="89a7e-160">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="89a7e-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="89a7e-161">排除開發相依性</span><span class="sxs-lookup"><span data-stu-id="89a7e-161">Excluding development dependencies</span></span>

<span data-ttu-id="89a7e-162">某些 NuGet 套件相當適合用來作為開發相依性，可協助您撰寫自己的程式庫，但不一定需要作為實際的套件相依性。</span><span class="sxs-lookup"><span data-stu-id="89a7e-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="89a7e-163">此 `pack` 命令會忽略 `package` 中的專案，該專案的 `packages.config` `developmentDependency` 屬性設定為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="89a7e-164">這些專案不會在建立的封裝中包含為相依性。</span><span class="sxs-lookup"><span data-stu-id="89a7e-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="89a7e-165">例如，請考慮 `packages.config` 來源專案中的下列檔案：</span><span class="sxs-lookup"><span data-stu-id="89a7e-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="89a7e-166">針對此專案，所建立的封裝 `nuget pack` 將相依于 `jQuery` 和， `microsoft-web-helpers` 而不是 `netfx-Guard` 。</span><span class="sxs-lookup"><span data-stu-id="89a7e-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="89a7e-167">隱藏套件警告</span><span class="sxs-lookup"><span data-stu-id="89a7e-167">Suppressing pack warnings</span></span>

<span data-ttu-id="89a7e-168">雖然建議您在封裝作業期間解決所有的 NuGet 警告，但在某些情況下，這些警告會受到保證。</span><span class="sxs-lookup"><span data-stu-id="89a7e-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="89a7e-169">您可以透過下列方式達成此目的：</span><span class="sxs-lookup"><span data-stu-id="89a7e-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="89a7e-170">nuget.exe 套件封裝. nuspec-Properties NoWarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="89a7e-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="89a7e-171">範例</span><span class="sxs-lookup"><span data-stu-id="89a7e-171">Examples</span></span>

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
