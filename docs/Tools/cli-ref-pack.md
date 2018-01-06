---
title: "NuGet 的 CLI 組件命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Nuget.exe 套件命令參考"
keywords: "nuget 組件參考組件命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 22643ee4c7d5f858da728ba9d9d2886d600d20f0
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="2763f-104">組件命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2763f-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="2763f-105">**適用於：**封裝建立&bullet;**支援的版本：** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="2763f-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="2763f-106">建立根據指定的 NuGet 套件`.nuspec`或專案檔。</span><span class="sxs-lookup"><span data-stu-id="2763f-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="2763f-107">`dotnet pack`命令 (請參閱[dotnet 命令](dotnet-Commands.md)) 和`msbuild /t:pack`(請參閱[MSBuild 目標](../schema/msbuild-targets.md)) 可做為替代項目。</span><span class="sxs-lookup"><span data-stu-id="2763f-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="2763f-108">下單聲道，不支援從專案檔中建立封裝。</span><span class="sxs-lookup"><span data-stu-id="2763f-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="2763f-109">您也需要調整非區域路徑中的`.nuspec`Unix 樣式的路徑，檔案，如 nuget.exe 未轉換 Windows 路徑名稱本身。</span><span class="sxs-lookup"><span data-stu-id="2763f-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="2763f-110">使用量</span><span class="sxs-lookup"><span data-stu-id="2763f-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="2763f-111">其中`<nuspecPath>`和`<projectPath>`指定`.nuspec`或專案檔，分別。</span><span class="sxs-lookup"><span data-stu-id="2763f-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="2763f-112">選項</span><span class="sxs-lookup"><span data-stu-id="2763f-112">Options</span></span>

| <span data-ttu-id="2763f-113">選項</span><span class="sxs-lookup"><span data-stu-id="2763f-113">Option</span></span> | <span data-ttu-id="2763f-114">描述</span><span class="sxs-lookup"><span data-stu-id="2763f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2763f-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="2763f-115">BasePath</span></span> | <span data-ttu-id="2763f-116">設定檔案中定義的基底路徑`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="2763f-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="2763f-117">組建</span><span class="sxs-lookup"><span data-stu-id="2763f-117">Build</span></span> | <span data-ttu-id="2763f-118">指定應該建置封裝前，先建置專案。</span><span class="sxs-lookup"><span data-stu-id="2763f-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="2763f-119">排除</span><span class="sxs-lookup"><span data-stu-id="2763f-119">Exclude</span></span> | <span data-ttu-id="2763f-120">指定建立封裝時所要排除的一個或多個萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="2763f-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> |
| <span data-ttu-id="2763f-121">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="2763f-121">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="2763f-122">建立封裝時，可避免包含空的目錄。</span><span class="sxs-lookup"><span data-stu-id="2763f-122">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="2763f-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2763f-123">ForceEnglishOutput</span></span> | <span data-ttu-id="2763f-124">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="2763f-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2763f-125">說明</span><span class="sxs-lookup"><span data-stu-id="2763f-125">Help</span></span> | <span data-ttu-id="2763f-126">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="2763f-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="2763f-127">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="2763f-127">IncludeReferencedProjects</span></span> | <span data-ttu-id="2763f-128">指出已建立的封裝應包含參考的專案做為相依性，或是做為封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="2763f-128">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="2763f-129">如果參考的專案都有對應`.nuspec`檔案具有相同名稱做為專案，則該參考的專案加入做為相依性。</span><span class="sxs-lookup"><span data-stu-id="2763f-129">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="2763f-130">否則，封裝的一部分加入參考的專案。</span><span class="sxs-lookup"><span data-stu-id="2763f-130">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="2763f-131">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="2763f-131">MinClientVersion</span></span> | <span data-ttu-id="2763f-132">設定*minClientVersion*屬性建立的封裝。</span><span class="sxs-lookup"><span data-stu-id="2763f-132">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="2763f-133">這個值會覆寫現有的值*minClientVersion*屬性 （如果有的話） 中`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="2763f-133">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="2763f-134">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="2763f-134">MSBuildPath</span></span> | <span data-ttu-id="2763f-135">*（4.0 +)*指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。</span><span class="sxs-lookup"><span data-stu-id="2763f-135">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="2763f-136">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="2763f-136">MSBuildVersion</span></span> | <span data-ttu-id="2763f-137">*（3.2 +)*指定要搭配此命令使用 MSBuild 的版本。</span><span class="sxs-lookup"><span data-stu-id="2763f-137">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="2763f-138">支援的值為 4，12，14，15。</span><span class="sxs-lookup"><span data-stu-id="2763f-138">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="2763f-139">根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="2763f-139">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="2763f-140">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="2763f-140">NoDefaultExcludes</span></span> | <span data-ttu-id="2763f-141">防止預設排除的 NuGet 封裝檔案和檔案和資料夾的啟動點，如`.svn`和`.gitignore`。</span><span class="sxs-lookup"><span data-stu-id="2763f-141">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="2763f-142">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="2763f-142">NoPackageAnalysis</span></span> | <span data-ttu-id="2763f-143">指定封裝不應該在建置套件之後執行套件分析。</span><span class="sxs-lookup"><span data-stu-id="2763f-143">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="2763f-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="2763f-144">OutputDirectory</span></span> | <span data-ttu-id="2763f-145">指定建立的封裝儲存所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2763f-145">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="2763f-146">如果沒有指定資料夾，則會使用目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2763f-146">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="2763f-147">屬性</span><span class="sxs-lookup"><span data-stu-id="2763f-147">Properties</span></span> | <span data-ttu-id="2763f-148">指定覆寫專案檔案中的值的屬性的清單請參閱[一般 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="2763f-148">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="2763f-149">屬性引數是一份語彙基元 = value 配對，以分號分隔，其中出現的每個`$token$`中`.nuspec`檔案將會取代為指定的值。</span><span class="sxs-lookup"><span data-stu-id="2763f-149">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="2763f-150">值可以是以引號的字串。</span><span class="sxs-lookup"><span data-stu-id="2763f-150">Values can be strings in quotation marks.</span></span> <span data-ttu-id="2763f-151">請注意，「 設定 」 屬性，預設值是"Debug"。</span><span class="sxs-lookup"><span data-stu-id="2763f-151">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="2763f-152">若要變更的發行組態，請使用`-Properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="2763f-152">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="2763f-153">尾碼</span><span class="sxs-lookup"><span data-stu-id="2763f-153">Suffix</span></span> | <span data-ttu-id="2763f-154">*(3.4.4+)*將後置詞附加至內部產生的版本號碼，通常用於附加建置或其他發行前版本識別項。</span><span class="sxs-lookup"><span data-stu-id="2763f-154">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="2763f-155">例如，使用`-suffix nightly`將建立一個封裝的版本編號的類似`1.2.3-nightly`。</span><span class="sxs-lookup"><span data-stu-id="2763f-155">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="2763f-156">後置字元的開頭必須是字母，若要避免警告、 錯誤和潛在的不相容，使用不同版本的 NuGet 和 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="2763f-156">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="2763f-157">Symbol</span><span class="sxs-lookup"><span data-stu-id="2763f-157">Symbols</span></span> | <span data-ttu-id="2763f-158">指定封裝包含來源和符號。</span><span class="sxs-lookup"><span data-stu-id="2763f-158">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="2763f-159">當搭配`.nuspec`檔案，這會建立一般的 NuGet 封裝檔案，而對應符號封裝。</span><span class="sxs-lookup"><span data-stu-id="2763f-159">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="2763f-160">工具</span><span class="sxs-lookup"><span data-stu-id="2763f-160">Tool</span></span> | <span data-ttu-id="2763f-161">指定專案的輸出檔應該放在`tool`資料夾。</span><span class="sxs-lookup"><span data-stu-id="2763f-161">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="2763f-162">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="2763f-162">Verbosity</span></span> | <span data-ttu-id="2763f-163">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="2763f-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="2763f-164">版本</span><span class="sxs-lookup"><span data-stu-id="2763f-164">Version</span></span> | <span data-ttu-id="2763f-165">覆寫的版本號碼`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="2763f-165">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="2763f-166">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2763f-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="2763f-167">不含開發依存性</span><span class="sxs-lookup"><span data-stu-id="2763f-167">Excluding development dependencies</span></span>

<span data-ttu-id="2763f-168">部分 NuGet 封裝都可用為開發相依性，這可協助您撰寫您自己的程式庫，但不一定需要與實際封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="2763f-168">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="2763f-169">`pack`命令將會忽略`package`中的項目`packages.config`具有`developmentDependency`屬性設為`true`。</span><span class="sxs-lookup"><span data-stu-id="2763f-169">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="2763f-170">這些項目不會包含與建立的封裝中的相依性。</span><span class="sxs-lookup"><span data-stu-id="2763f-170">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="2763f-171">例如，請考慮下列`packages.config`來源專案檔中：</span><span class="sxs-lookup"><span data-stu-id="2763f-171">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="2763f-172">此專案中，為封裝建立`nuget pack`有相依性`jQuery`和`microsoft-web-helpers`但不是`netfx-Guard`。</span><span class="sxs-lookup"><span data-stu-id="2763f-172">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="2763f-173">範例</span><span class="sxs-lookup"><span data-stu-id="2763f-173">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5
```
