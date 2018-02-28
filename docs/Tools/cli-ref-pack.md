---
title: "NuGet 的 CLI 組件命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 套件命令參考"
keywords: "nuget 組件參考組件命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9ee5dc87ea33b4419bcd9a09751c41b53ae2f70e
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="09b7a-104">組件命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="09b7a-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="09b7a-105">**適用於：**封裝建立&bullet;**支援的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="09b7a-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="09b7a-106">建立根據指定的 NuGet 套件`.nuspec`或專案檔。</span><span class="sxs-lookup"><span data-stu-id="09b7a-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="09b7a-107">`dotnet pack`命令 (請參閱[dotnet 命令](dotnet-Commands.md)) 和`msbuild /t:pack`(請參閱[MSBuild 目標](../reference/msbuild-targets.md)) 可做為替代項目。</span><span class="sxs-lookup"><span data-stu-id="09b7a-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="09b7a-108">下單聲道，不支援從專案檔中建立封裝。</span><span class="sxs-lookup"><span data-stu-id="09b7a-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="09b7a-109">您也需要調整非區域路徑中的`.nuspec`Unix 樣式的路徑，檔案，如 nuget.exe 未轉換 Windows 路徑名稱本身。</span><span class="sxs-lookup"><span data-stu-id="09b7a-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="09b7a-110">使用量</span><span class="sxs-lookup"><span data-stu-id="09b7a-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="09b7a-111">其中`<nuspecPath>`和`<projectPath>`指定`.nuspec`或專案檔，分別。</span><span class="sxs-lookup"><span data-stu-id="09b7a-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="09b7a-112">選項</span><span class="sxs-lookup"><span data-stu-id="09b7a-112">Options</span></span>

| <span data-ttu-id="09b7a-113">選項</span><span class="sxs-lookup"><span data-stu-id="09b7a-113">Option</span></span> | <span data-ttu-id="09b7a-114">描述</span><span class="sxs-lookup"><span data-stu-id="09b7a-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09b7a-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="09b7a-115">BasePath</span></span> | <span data-ttu-id="09b7a-116">設定檔案中定義的基底路徑`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="09b7a-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="09b7a-117">組建</span><span class="sxs-lookup"><span data-stu-id="09b7a-117">Build</span></span> | <span data-ttu-id="09b7a-118">指定應該建置封裝前，先建置專案。</span><span class="sxs-lookup"><span data-stu-id="09b7a-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="09b7a-119">排除</span><span class="sxs-lookup"><span data-stu-id="09b7a-119">Exclude</span></span> | <span data-ttu-id="09b7a-120">指定建立封裝時所要排除的一個或多個萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="09b7a-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="09b7a-121">若要指定多個模式，請重複-排除旗標。</span><span class="sxs-lookup"><span data-stu-id="09b7a-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="09b7a-122">請參閱以下的範例。</span><span class="sxs-lookup"><span data-stu-id="09b7a-122">See example below.</span></span> |
| <span data-ttu-id="09b7a-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="09b7a-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="09b7a-124">建立封裝時，可避免包含空的目錄。</span><span class="sxs-lookup"><span data-stu-id="09b7a-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="09b7a-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="09b7a-125">ForceEnglishOutput</span></span> | <span data-ttu-id="09b7a-126">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="09b7a-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="09b7a-127">說明</span><span class="sxs-lookup"><span data-stu-id="09b7a-127">Help</span></span> | <span data-ttu-id="09b7a-128">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="09b7a-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="09b7a-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="09b7a-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="09b7a-130">指出已建立的封裝應包含參考的專案做為相依性，或是做為封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="09b7a-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="09b7a-131">如果參考的專案都有對應`.nuspec`檔案具有相同名稱做為專案，則該參考的專案加入做為相依性。</span><span class="sxs-lookup"><span data-stu-id="09b7a-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="09b7a-132">否則，封裝的一部分加入參考的專案。</span><span class="sxs-lookup"><span data-stu-id="09b7a-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="09b7a-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="09b7a-133">MinClientVersion</span></span> | <span data-ttu-id="09b7a-134">設定*minClientVersion*屬性建立的封裝。</span><span class="sxs-lookup"><span data-stu-id="09b7a-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="09b7a-135">這個值會覆寫現有的值*minClientVersion*屬性 （如果有的話） 中`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="09b7a-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="09b7a-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="09b7a-136">MSBuildPath</span></span> | <span data-ttu-id="09b7a-137">*（4.0 +)*指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="09b7a-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="09b7a-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="09b7a-138">MSBuildVersion</span></span> | <span data-ttu-id="09b7a-139">*（3.2 +)*指定要搭配此命令使用 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="09b7a-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="09b7a-140">支援的值為 4，12，14，15。</span><span class="sxs-lookup"><span data-stu-id="09b7a-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="09b7a-141">根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="09b7a-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="09b7a-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="09b7a-142">NoDefaultExcludes</span></span> | <span data-ttu-id="09b7a-143">防止預設排除的 NuGet 封裝檔案和檔案和資料夾的啟動點，如`.svn`和`.gitignore`。</span><span class="sxs-lookup"><span data-stu-id="09b7a-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="09b7a-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="09b7a-144">NoPackageAnalysis</span></span> | <span data-ttu-id="09b7a-145">指定封裝不應該在建置套件之後執行套件分析。</span><span class="sxs-lookup"><span data-stu-id="09b7a-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="09b7a-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="09b7a-146">OutputDirectory</span></span> | <span data-ttu-id="09b7a-147">指定建立的封裝儲存所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="09b7a-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="09b7a-148">如果沒有指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="09b7a-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="09b7a-149">屬性</span><span class="sxs-lookup"><span data-stu-id="09b7a-149">Properties</span></span> | <span data-ttu-id="09b7a-150">指定覆寫專案檔案中的值的屬性的清單請參閱[一般 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="09b7a-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="09b7a-151">屬性引數是一份語彙基元 = value 配對，以分號分隔，其中出現的每個`$token$`中`.nuspec`檔案將會取代為指定的值。</span><span class="sxs-lookup"><span data-stu-id="09b7a-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="09b7a-152">值可以是以引號的字串。</span><span class="sxs-lookup"><span data-stu-id="09b7a-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="09b7a-153">請注意，「 設定 」 屬性，預設值是"Debug"。</span><span class="sxs-lookup"><span data-stu-id="09b7a-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="09b7a-154">若要變更的發行組態，請使用`-Properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="09b7a-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="09b7a-155">尾碼</span><span class="sxs-lookup"><span data-stu-id="09b7a-155">Suffix</span></span> | <span data-ttu-id="09b7a-156">*(3.4.4+)*將後置詞附加至內部產生的版本號碼，通常用於附加建置或其他發行前版本識別項。</span><span class="sxs-lookup"><span data-stu-id="09b7a-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="09b7a-157">例如，使用`-suffix nightly`將建立一個封裝的版本編號的類似`1.2.3-nightly`。</span><span class="sxs-lookup"><span data-stu-id="09b7a-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="09b7a-158">後置字元的開頭必須是字母，若要避免警告、 錯誤和潛在的不相容，使用不同版本的 NuGet 和 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="09b7a-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="09b7a-159">Symbol</span><span class="sxs-lookup"><span data-stu-id="09b7a-159">Symbols</span></span> | <span data-ttu-id="09b7a-160">指定封裝包含來源和符號。</span><span class="sxs-lookup"><span data-stu-id="09b7a-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="09b7a-161">當搭配`.nuspec`檔案，這會建立一般的 NuGet 封裝檔案，而對應符號封裝。</span><span class="sxs-lookup"><span data-stu-id="09b7a-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="09b7a-162">工具</span><span class="sxs-lookup"><span data-stu-id="09b7a-162">Tool</span></span> | <span data-ttu-id="09b7a-163">指定專案的輸出檔應該放在`tool`資料夾。</span><span class="sxs-lookup"><span data-stu-id="09b7a-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="09b7a-164">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="09b7a-164">Verbosity</span></span> | <span data-ttu-id="09b7a-165">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="09b7a-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="09b7a-166">版本</span><span class="sxs-lookup"><span data-stu-id="09b7a-166">Version</span></span> | <span data-ttu-id="09b7a-167">覆寫的版本號碼`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="09b7a-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="09b7a-168">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="09b7a-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="09b7a-169">不含開發依存性</span><span class="sxs-lookup"><span data-stu-id="09b7a-169">Excluding development dependencies</span></span>

<span data-ttu-id="09b7a-170">部分 NuGet 封裝都可用為開發相依性，這可協助您撰寫您自己的程式庫，但不一定需要與實際封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="09b7a-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="09b7a-171">`pack`命令將會忽略`package`中的項目`packages.config`具有`developmentDependency`屬性設為`true`。</span><span class="sxs-lookup"><span data-stu-id="09b7a-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="09b7a-172">這些項目不會包含與建立的封裝中的相依性。</span><span class="sxs-lookup"><span data-stu-id="09b7a-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="09b7a-173">例如，請考慮下列`packages.config`來源專案檔中：</span><span class="sxs-lookup"><span data-stu-id="09b7a-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="09b7a-174">此專案中，為封裝建立`nuget pack`有相依性`jQuery`和`microsoft-web-helpers`但不是`netfx-Guard`。</span><span class="sxs-lookup"><span data-stu-id="09b7a-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="09b7a-175">範例</span><span class="sxs-lookup"><span data-stu-id="09b7a-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
