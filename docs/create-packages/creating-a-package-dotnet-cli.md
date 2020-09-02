---
title: 使用 dotnet CLI 建立 NuGet 套件
description: NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類索引鍵決策點。
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 87b38d7a707d6175eb3347280784d9dfefd9c17d
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "89359641"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="56f46-103">使用 dotnet CLI 建立 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="56f46-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="56f46-104">不論套件的功能或所含程式碼為何，您都可以使用其中一個 CLI 工具 (`nuget.exe` 或 `dotnet.exe`) 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。</span><span class="sxs-lookup"><span data-stu-id="56f46-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="56f46-105">此文章說明如何使用 dotnet CLI 建立套件。</span><span class="sxs-lookup"><span data-stu-id="56f46-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="56f46-106">若要安裝 `dotnet` CLI，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="56f46-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="56f46-107">從 Visual Studio 2017 開始，dotnet CLI 隨附於 .NET Core工作負載中。</span><span class="sxs-lookup"><span data-stu-id="56f46-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="56f46-108">針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，NuGet 會直接使用專案檔中的資訊來建立套件。</span><span class="sxs-lookup"><span data-stu-id="56f46-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="56f46-109">如需逐步執行教學課程，請參閱[使用 dotnet CLI 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)或[使用 Visual Studio 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="56f46-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="56f46-110">`msbuild -t:pack` 在功能上相當於 `dotnet pack`。</span><span class="sxs-lookup"><span data-stu-id="56f46-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="56f46-111">若要使用 MSBuild 進行建置，請參閱[使用 MSBuild 建立 NuGet 套件](creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="56f46-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56f46-112">此主題適用於 [SDK 樣式](../resources/check-project-format.md)的專案，這通常是 .NET Core 與 .NET Standard 專案。</span><span class="sxs-lookup"><span data-stu-id="56f46-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="56f46-113">設定屬性</span><span class="sxs-lookup"><span data-stu-id="56f46-113">Set properties</span></span>

<span data-ttu-id="56f46-114">建立套件時需要下列屬性。</span><span class="sxs-lookup"><span data-stu-id="56f46-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="56f46-115">`PackageId`，套件識別碼，這在裝載套件的資源庫內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="56f46-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="56f46-116">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="56f46-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="56f46-117">`Version`，*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="56f46-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="56f46-118">若未指定，則預設值為 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="56f46-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="56f46-119">主機上應該會出現套件標題 (例如 nuget.org)</span><span class="sxs-lookup"><span data-stu-id="56f46-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="56f46-120">`Authors`，作者與擁有者資訊。</span><span class="sxs-lookup"><span data-stu-id="56f46-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="56f46-121">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="56f46-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="56f46-122">`Company`，您的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="56f46-122">`Company`, your company name.</span></span> <span data-ttu-id="56f46-123">若未指定，則預設值為 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="56f46-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="56f46-124">在 Visual Studio 中，您可以在專案屬性中設定這些值 (在 [方案總管] 中以滑鼠右鍵按一下專案，選擇 [屬性]\*\*\*\*，然後選取 [套件]\*\*\*\* 索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="56f46-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="56f46-125">您也可以直接在專案檔 (`.csproj`) 中設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="56f46-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="56f46-126">為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何套件資源上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="56f46-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="56f46-127">下列範例顯示一個簡單且完整的專案檔，其中會包含這些屬性。</span><span class="sxs-lookup"><span data-stu-id="56f46-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="56f46-128">(您可以使用 `dotnet new classlib` 命令來建立新的預設專案)。</span><span class="sxs-lookup"><span data-stu-id="56f46-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="56f46-129">您還可以設定選擇性屬性，例如`Title`、`PackageDescription` 與 `PackageTags`，如 [MSBuild 套件目標](../reference/msbuild-targets.md#pack-target)、[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)，以及 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。</span><span class="sxs-lookup"><span data-stu-id="56f46-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="56f46-130">針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="56f46-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="56f46-131">如需宣告相依性及指定版本號碼的詳細資料，請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)和[套件版本控制](../concepts/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="56f46-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="56f46-132">使用 `<IncludeAssets>` 與 `<ExcludeAssets>` 屬性，也可以將來自相依性的資產直接用於套件中。</span><span class="sxs-lookup"><span data-stu-id="56f46-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="56f46-133">如需詳細資訊，請參閱控制相依性 [資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="56f46-133">For more information, see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="56f46-134">新增選擇性的描述欄位</span><span class="sxs-lookup"><span data-stu-id="56f46-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="56f46-135">選擇唯一的套件識別碼並設定版本號碼</span><span class="sxs-lookup"><span data-stu-id="56f46-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="56f46-136">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="56f46-136">Run the pack command</span></span>

<span data-ttu-id="56f46-137">若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `dotnet pack` 命令，該命令也會自動建置專案：</span><span class="sxs-lookup"><span data-stu-id="56f46-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="56f46-138">輸出會顯示 `.nupkg` 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="56f46-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="56f46-139">建置時自動產生套件</span><span class="sxs-lookup"><span data-stu-id="56f46-139">Automatically generate package on build</span></span>

<span data-ttu-id="56f46-140">若要在您執行 `dotnet build` 時自動執行 `dotnet pack`，請將下列程式行加入專案檔的 `<PropertyGroup>` 中：</span><span class="sxs-lookup"><span data-stu-id="56f46-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="56f46-141">當您 `dotnet pack` 在方案上執行時，這會封裝封裝 ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 屬性設定為) 之方案中的所有專案 `true` 。</span><span class="sxs-lookup"><span data-stu-id="56f46-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="56f46-142">當您自動產生套件時，封裝的時間會增加專案的建置時間。</span><span class="sxs-lookup"><span data-stu-id="56f46-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="56f46-143">測試套件安裝</span><span class="sxs-lookup"><span data-stu-id="56f46-143">Test package installation</span></span>

<span data-ttu-id="56f46-144">發行套件之前，您通常會想要測試將套件安裝至專案的程序。</span><span class="sxs-lookup"><span data-stu-id="56f46-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="56f46-145">測試可確保必要的檔案最後都在專案的正確位置。</span><span class="sxs-lookup"><span data-stu-id="56f46-145">The tests make sure that the necessary files all end up in their correct places in the project.</span></span>

<span data-ttu-id="56f46-146">您可以使用一般[套件安裝步驟](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)，以在 Visual Studio 中或命令列上手動測試安裝。</span><span class="sxs-lookup"><span data-stu-id="56f46-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56f46-147">套件是不可變的。</span><span class="sxs-lookup"><span data-stu-id="56f46-147">Packages are immutable.</span></span> <span data-ttu-id="56f46-148">如果您更正了問題，請變更套件的內容並再次封裝，當您重新測試時，仍會使用舊版套件，直到您[清除全域套件](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)資料夾為止。</span><span class="sxs-lookup"><span data-stu-id="56f46-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="56f46-149">在測試每個組建上未使用唯一發行前版本標籤的套件時，這關係重大。</span><span class="sxs-lookup"><span data-stu-id="56f46-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56f46-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56f46-150">Next Steps</span></span>

<span data-ttu-id="56f46-151">建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="56f46-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="56f46-152">您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：</span><span class="sxs-lookup"><span data-stu-id="56f46-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="56f46-153">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="56f46-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="56f46-154">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="56f46-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="56f46-155">新增套件圖示</span><span class="sxs-lookup"><span data-stu-id="56f46-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="56f46-156">原始程式檔和組態檔的轉換</span><span class="sxs-lookup"><span data-stu-id="56f46-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="56f46-157">當地語系化</span><span class="sxs-lookup"><span data-stu-id="56f46-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="56f46-158">發行前版本</span><span class="sxs-lookup"><span data-stu-id="56f46-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="56f46-159">設定套件類型</span><span class="sxs-lookup"><span data-stu-id="56f46-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="56f46-160">建立包含 COM Interop 組件的套件</span><span class="sxs-lookup"><span data-stu-id="56f46-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="56f46-161">最後，請注意其他套件類型：</span><span class="sxs-lookup"><span data-stu-id="56f46-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="56f46-162">原生封裝</span><span class="sxs-lookup"><span data-stu-id="56f46-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="56f46-163">符號套件</span><span class="sxs-lookup"><span data-stu-id="56f46-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
