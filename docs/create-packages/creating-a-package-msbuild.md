---
title: 使用 MSBuild 建立 NuGet 套件
description: NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類索引鍵決策點。
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231314"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="fa9ac-103">使用 MSBuild 建立 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="fa9ac-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="fa9ac-104">當您從程式碼建立 NuGet 套件時，會將該功能封裝至可由任意數目的其他開發人員共用和使用的元件。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="fa9ac-105">本文說明如何使用 MSBuild 建立套件。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="fa9ac-106">MSBuild 會使用每個包含 NuGet 的 Visual Studio 工作負載來進行預先安裝。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="fa9ac-107">此外,您也可以使用MSBuild通過點網CLI與[點網msbuild。](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild)</span><span class="sxs-lookup"><span data-stu-id="fa9ac-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="fa9ac-108">針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，NuGet 會直接使用專案檔中的資訊來建立套件。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="fa9ac-109">針對使用 `<PackageReference>` 的非 SDK 樣式專案，NuGet 也會使用專案檔來建立套件。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="fa9ac-110">SDK 樣式的專案預設會提供套件功能。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="fa9ac-111">針對非 SDK 樣式的 PackageReference 專案，您必須將 NuGet.Build.Tasks.Pack 套件新增至專案相依性。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="fa9ac-112">如需 MSBuild 套件目標的詳細資訊，請參閱 [NuGet 套件和還原為 MSBuild 目標](../reference/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="fa9ac-113">建立套件的命令 `msbuild -t:pack` 是相當於 `dotnet pack` 的功能。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa9ac-114">本主題適用於 [SDK 樣式](../resources/check-project-format.md)的專案 (通常是 .NET Core 和 .NET Standard 專案)，以及適用於使用 PackageReference 的非 SDK 樣式專案。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="fa9ac-115">設定屬性</span><span class="sxs-lookup"><span data-stu-id="fa9ac-115">Set properties</span></span>

<span data-ttu-id="fa9ac-116">建立套件時需要下列屬性。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="fa9ac-117">`PackageId`，套件識別碼，這在裝載套件的資源庫內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="fa9ac-118">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="fa9ac-119">`Version`，*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="fa9ac-120">若未指定，則預設值為 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="fa9ac-121">主機上應該會出現套件標題 (例如 nuget.org)</span><span class="sxs-lookup"><span data-stu-id="fa9ac-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="fa9ac-122">`Authors`，作者與擁有者資訊。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="fa9ac-123">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="fa9ac-124">`Company`，您的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-124">`Company`, your company name.</span></span> <span data-ttu-id="fa9ac-125">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="fa9ac-126">此外,如果要打包使用包參考的非 SDK 樣式專案,則需要:</span><span class="sxs-lookup"><span data-stu-id="fa9ac-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="fa9ac-127">`PackageOutputPath`,調用包時生成的包的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="fa9ac-128">在 Visual Studio 中，您可以在專案屬性中設定這些值 (在 [方案總管] 中以滑鼠右鍵按一下專案，選擇 [屬性]\*\*\*\*，然後選取 [套件]\*\*\*\* 索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="fa9ac-129">您也可以直接在專案檔 (*.csproj*) 中設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="fa9ac-130">為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何套件資源上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="fa9ac-131">下列範例顯示一個簡單且完整的專案檔，其中會包含這些屬性。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-131">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="fa9ac-132">您還可以設定選擇性屬性，例如`Title`、`PackageDescription` 與 `PackageTags`，如 [MSBuild 套件目標](../reference/msbuild-targets.md#pack-target)、[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)，以及 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="fa9ac-133">針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="fa9ac-134">如需宣告相依性及指定版本號碼的詳細資料，請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)和[套件版本控制](../concepts/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="fa9ac-135">使用 `<IncludeAssets>` 與 `<ExcludeAssets>` 屬性，也可以將來自相依性的資產直接用於套件中。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="fa9ac-136">如需詳細資訊，請參閱[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="fa9ac-137">新增選擇的標題欄位</span><span class="sxs-lookup"><span data-stu-id="fa9ac-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="fa9ac-138">選擇唯一的套件識別碼並設定版本號碼</span><span class="sxs-lookup"><span data-stu-id="fa9ac-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="fa9ac-139">新增 NuGet.Build.Tasks.Pack 套件</span><span class="sxs-lookup"><span data-stu-id="fa9ac-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="fa9ac-140">如果您使用 MSBuild 搭配非 SDK 樣式的專案和 PackageReference，請將 NuGet.Build.Tasks.Pack 套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="fa9ac-141">開啟專案檔，並在 `<PropertyGroup>` 元素之後新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="fa9ac-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="fa9ac-142">開啟開發人員命令提示字元 (在 [搜尋]\*\*\*\* 方塊中，輸入**開發人員命令提示字元**)。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="fa9ac-143">您通常想要從 [開始]\*\*\*\* 功能表啟動適用於 Visual Studio 的開發人員命令提示字元，因為它將使用適用於 MSBuild 的所有必要路徑來設定。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="fa9ac-144">切換至包含專案檔的資料夾，並輸入下列命令以安裝 NuGet.Build.Tasks.Pack 套件。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="fa9ac-145">確定 MSBuild 輸出會指出組建已順利完成。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="fa9ac-146">執行 msbuild -t:pack 命令</span><span class="sxs-lookup"><span data-stu-id="fa9ac-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="fa9ac-147">若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `msbuild -t:pack` 命令，該命令也會自動建置專案：</span><span class="sxs-lookup"><span data-stu-id="fa9ac-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="fa9ac-148">在 Visual Studio 開發人員命令提示字元中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="fa9ac-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="fa9ac-149">輸出會顯示 `.nupkg` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-149">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="fa9ac-150">建置時自動產生套件</span><span class="sxs-lookup"><span data-stu-id="fa9ac-150">Automatically generate package on build</span></span>

<span data-ttu-id="fa9ac-151">若要在您建置或還原專案時自動執行 `msbuild -t:pack`，請將下一行新增至專案檔的 `<PropertyGroup>` 中：</span><span class="sxs-lookup"><span data-stu-id="fa9ac-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="fa9ac-152">在解決方案`msbuild -t:pack`上執行時,這將打包解決方案中可打包的所有專案[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties)(屬性設置`true`為)。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="fa9ac-153">當您自動產生套件時，封裝的時間會增加專案的建置時間。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="fa9ac-154">測試套件安裝</span><span class="sxs-lookup"><span data-stu-id="fa9ac-154">Test package installation</span></span>

<span data-ttu-id="fa9ac-155">發行套件之前，您通常會想要測試將套件安裝至專案的程序。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="fa9ac-156">測試可確定必要檔案最後都在專案的正確位置。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="fa9ac-157">您可以使用一般[套件安裝步驟](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)，以在 Visual Studio 中或命令列上手動測試安裝。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa9ac-158">套件是不可變的。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-158">Packages are immutable.</span></span> <span data-ttu-id="fa9ac-159">如果您更正了問題，請變更套件的內容並再次封裝，當您重新測試時，仍會使用舊版套件，直到您[清除全域套件](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)資料夾為止。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="fa9ac-160">在測試每個組建上未使用唯一發行前版本標籤的套件時，這關係重大。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa9ac-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa9ac-161">Next Steps</span></span>

<span data-ttu-id="fa9ac-162">建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="fa9ac-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="fa9ac-163">您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：</span><span class="sxs-lookup"><span data-stu-id="fa9ac-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="fa9ac-164">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="fa9ac-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="fa9ac-165">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="fa9ac-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="fa9ac-166">支援多個目標 Framework</span><span class="sxs-lookup"><span data-stu-id="fa9ac-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="fa9ac-167">原始程式檔和組態檔的轉換</span><span class="sxs-lookup"><span data-stu-id="fa9ac-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="fa9ac-168">當地語系化</span><span class="sxs-lookup"><span data-stu-id="fa9ac-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="fa9ac-169">預發行版本</span><span class="sxs-lookup"><span data-stu-id="fa9ac-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="fa9ac-170">設定套件類型</span><span class="sxs-lookup"><span data-stu-id="fa9ac-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="fa9ac-171">建立包含 COM Interop 組件的套件</span><span class="sxs-lookup"><span data-stu-id="fa9ac-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="fa9ac-172">最後，請注意其他套件類型：</span><span class="sxs-lookup"><span data-stu-id="fa9ac-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="fa9ac-173">本機包</span><span class="sxs-lookup"><span data-stu-id="fa9ac-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="fa9ac-174">符號套件</span><span class="sxs-lookup"><span data-stu-id="fa9ac-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
