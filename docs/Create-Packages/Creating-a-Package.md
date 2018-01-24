---
title: "如何建立 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類索引鍵決策點。"
keywords: "NuGet 套件建立, 建立套件, nuspec 資訊清單, NuGet 套件慣例、NuGet 套件版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6675d21a2900a1b61e17c08518b328732f4472c5
ms.sourcegitcommit: 1cb047b24b3b69d80e808c23b2ace0d98d2dfdcc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="0ef38-104">建立 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="0ef38-104">Creating NuGet packages</span></span>

<span data-ttu-id="0ef38-105">不論套件的功能或所含程式碼為何，您都可以使用 `nuget.exe` 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。</span><span class="sxs-lookup"><span data-stu-id="0ef38-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="0ef38-106">若要安裝 `nuget.exe`，請參閱[安裝 NuGet CLI](../guides/Install-NuGet.md#nuget-cli)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="0ef38-107">請注意，Visual Studio 不會自動包含 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="0ef38-108">技術上而言，NuGet 套件就只是已重新命名為 `.nupkg` 副檔名且其內容符合特定慣例的 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="0ef38-109">本主題描述如何建立符合這些慣例之套件的詳細程序。</span><span class="sxs-lookup"><span data-stu-id="0ef38-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="0ef38-110">如需詳細的逐步解說，請參閱[建立和發行套件快速入門](../quickstart/create-and-publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="0ef38-111">封裝開始於已編譯的程式碼 (組件)、符號 (和) 您想要以套件形式傳遞的其他檔案 (請參閱[概觀和工作流程](Overview-and-Workflow.md))。</span><span class="sxs-lookup"><span data-stu-id="0ef38-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="0ef38-112">此程序與編譯或產生進入套件的檔案無關，但您可以使用專案檔中的資訊保持已編譯的組件與套件同步。</span><span class="sxs-lookup"><span data-stu-id="0ef38-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="0ef38-113">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="0ef38-113">In this topic:</span></span>

- [<span data-ttu-id="0ef38-114">決定要封裝的組件</span><span class="sxs-lookup"><span data-stu-id="0ef38-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="0ef38-115">`.nuspec` 檔案的角色和結構</span><span class="sxs-lookup"><span data-stu-id="0ef38-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="0ef38-116">從下列項目[建立 `.nuspec` 檔案](#creating-the-nuspec-file)：</span><span class="sxs-lookup"><span data-stu-id="0ef38-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - [<span data-ttu-id="0ef38-117">以慣例為基礎的工作目錄</span><span class="sxs-lookup"><span data-stu-id="0ef38-117">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
    - [<span data-ttu-id="0ef38-118">組件 DLL</span><span class="sxs-lookup"><span data-stu-id="0ef38-118">An assembly DLL</span></span>](#from-an-assembly-dll)
    - [<span data-ttu-id="0ef38-119">Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="0ef38-119">A Visual Studio project</span></span>](#from-a-visual-studio-project)
    - [<span data-ttu-id="0ef38-120">含預設值的新檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-120">New file with default values</span></span>](#new-file-with-default-values)    
- [<span data-ttu-id="0ef38-121">選擇唯一的套件識別碼並設定版本號碼</span><span class="sxs-lookup"><span data-stu-id="0ef38-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="0ef38-122">[設定套件類型](#setting-a-package-type) (NuGet 3.5 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="0ef38-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="0ef38-123">新增讀我檔案和其他檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="0ef38-124">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="0ef38-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="0ef38-125">撰寫包含 COM Interop 組件的套件</span><span class="sxs-lookup"><span data-stu-id="0ef38-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="0ef38-126">執行nuget pack 以產生 .nupkg 檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="0ef38-127">在這些核心步驟之後，您可以併入各種其他功能，如這份文件中所述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="0ef38-128">請參閱下方的[後續步驟](#next-steps)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="0ef38-129">本主題適用於使用 Visual Studio 2017 和 NuGet 4.0+ 的 .NET Core 專案以外的專案類型。</span><span class="sxs-lookup"><span data-stu-id="0ef38-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="0ef38-130">在這些 .NET Core 專案中，NuGet 會直接使用 `.csproj` 檔案中的資訊。</span><span class="sxs-lookup"><span data-stu-id="0ef38-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="0ef38-131">如需詳細資料，請參閱[使用 Visual Studio 2017 建立 .NET Standard 套件](../guides/create-net-standard-packages-vs2017.md)和 [NuGet 封裝和還原為 MSBuild 目標](../schema/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="0ef38-132">決定要封裝的組件</span><span class="sxs-lookup"><span data-stu-id="0ef38-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="0ef38-133">大部分的一般用途套件都會包含其他開發人員可以在其專屬專案中使用的一或多個組件。</span><span class="sxs-lookup"><span data-stu-id="0ef38-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="0ef38-134">一般而言，最好一個 NuGet 套件一個組件，前提是每個組件都可以獨立使用。</span><span class="sxs-lookup"><span data-stu-id="0ef38-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="0ef38-135">例如，如果您有與 `Parser.dll` 相依的 `Utilities.dll`，而且 `Parser.dll` 可以單獨使用，則會為每個項目建立一個套件。</span><span class="sxs-lookup"><span data-stu-id="0ef38-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="0ef38-136">這樣做可讓開發人員單獨使用 `Parser.dll` 和 `Utilities.dll`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="0ef38-137">如果您的程式庫包含多個無法單獨使用的組件，則最好將它們結合成單一套件。</span><span class="sxs-lookup"><span data-stu-id="0ef38-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="0ef38-138">使用上述範例時，如果 `Parser.dll` 所包含的程式碼僅供 `Utilities.dll` 使用，則最好將 `Parser.dll` 放在相同的套件中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="0ef38-139">同樣地，如果 `Utilities.dll` 與 `Utilities.resources.dll` 相依 (再提醒一次，後者無法單獨使用)，則請將這兩個放在相同的套件中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="0ef38-140">資源其實是特殊案例。</span><span class="sxs-lookup"><span data-stu-id="0ef38-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="0ef38-141">將套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，但「排除」名為 `.resources.dll` 的參考，因為它們假設為當地語系化附屬組件 (請參閱[建立當地語系化套件](creating-localized-packages.md))。</span><span class="sxs-lookup"><span data-stu-id="0ef38-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="0ef38-142">因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="0ef38-143">如果您的程式庫包含 COM Interop 組件，請遵循[撰寫包含 COM Interop 組件的套件](#authoring-packages-with-com-interop-assemblies)中的其他指導方針。</span><span class="sxs-lookup"><span data-stu-id="0ef38-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="0ef38-144">.nuspec 檔案的角色和結構</span><span class="sxs-lookup"><span data-stu-id="0ef38-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="0ef38-145">知道您想要封裝的檔案之後，下個步驟就是在 `.nuspec` XML 檔案中建立套件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="0ef38-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="0ef38-146">資訊清單：</span><span class="sxs-lookup"><span data-stu-id="0ef38-146">The manifest:</span></span>

1. <span data-ttu-id="0ef38-147">描述套件內容而且本身包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="0ef38-148">驅使建立套件並指示 NuGet 如何將套件安裝至專案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="0ef38-149">例如，資訊清單會識別其他套件相依性；因此，安裝主要套件時，NuGet 也可以安裝這些相依性。</span><span class="sxs-lookup"><span data-stu-id="0ef38-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="0ef38-150">包含必要和選擇性屬性，如下所述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="0ef38-151">如需確切詳細資料 (包含這裡未提及的其他屬性)，請參閱 [.nuspec 參考](../schema/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="0ef38-152">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0ef38-152">Required properties:</span></span>

- <span data-ttu-id="0ef38-153">套件識別碼，其在裝載套件的資源庫內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0ef38-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="0ef38-154">*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](Prerelease-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="0ef38-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="0ef38-155">它應該出現在主機上的套件標題 (例如 nuget.org)</span><span class="sxs-lookup"><span data-stu-id="0ef38-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="0ef38-156">作者和擁有者資訊。</span><span class="sxs-lookup"><span data-stu-id="0ef38-156">Author and owner information.</span></span>
- <span data-ttu-id="0ef38-157">套件的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-157">A long description of the package.</span></span>

<span data-ttu-id="0ef38-158">常見的選擇性屬性：</span><span class="sxs-lookup"><span data-stu-id="0ef38-158">Common optional properties:</span></span>

- <span data-ttu-id="0ef38-159">版本資訊</span><span class="sxs-lookup"><span data-stu-id="0ef38-159">Release notes</span></span>
- <span data-ttu-id="0ef38-160">著作權資訊</span><span class="sxs-lookup"><span data-stu-id="0ef38-160">Copyright information</span></span>
- <span data-ttu-id="0ef38-161">[Visual Studio 中的套件管理員 UI](../Tools/Package-Manager-UI.md) 的簡短描述</span><span class="sxs-lookup"><span data-stu-id="0ef38-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="0ef38-162">地區設定識別碼</span><span class="sxs-lookup"><span data-stu-id="0ef38-162">A locale ID</span></span>
- <span data-ttu-id="0ef38-163">首頁和授權 URL</span><span class="sxs-lookup"><span data-stu-id="0ef38-163">Home page and license URLs</span></span>
- <span data-ttu-id="0ef38-164">圖示 URL</span><span class="sxs-lookup"><span data-stu-id="0ef38-164">An icon URL</span></span>
- <span data-ttu-id="0ef38-165">相依性和參考的清單</span><span class="sxs-lookup"><span data-stu-id="0ef38-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="0ef38-166">協助進行資源庫搜尋的標記</span><span class="sxs-lookup"><span data-stu-id="0ef38-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="0ef38-167">下列一般 (但虛構的) `.nuspec` 檔案具有可描述屬性的註解：</span><span class="sxs-lookup"><span data-stu-id="0ef38-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- The identifier that must be unique within the hosting gallery -->
    <id>Contoso.Utility.UsefulStuff</id>

    <!-- The package version number that is used when resolving dependencies -->
    <version>1.8.3-beta</version>

    <!-- Authors contain text that appears directly on the gallery -->
    <authors>Dejana Tesic, Rajeev Dey</authors>

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
    <description>Core utility functions for web applications</description>

    <!-- Copyright information -->
    <copyright>Copyright ©2016 Contoso Corporation</copyright>

    <!-- Tags appear in the gallery and can be used for tag searches -->
    <tags>web utility http json url parsing</tags>

    <!-- Dependencies are automatically installed when the package is installed -->
    <dependencies>
        <dependency id="Newtonsoft.Json" version="9.0" />
    </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="0ef38-168">如需宣告相依性以及指定版本號碼的詳細資料，請參閱[套件版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="0ef38-169">在 `dependency` 項目上使用 `include` 和 `exclude` 屬性，也可以將相依性中的資產直接用於套件中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="0ef38-170">請參閱 [.nuspec 參考 - 相依性](../Schema/nuspec.md#dependencies)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="0ef38-171">因為資訊清單會包含在透過它所建立的套件中，所以檢查現有套件就可以找到任意數目的其他範例。</span><span class="sxs-lookup"><span data-stu-id="0ef38-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="0ef38-172">不錯的來源是您電腦上的全域套件快取，即下列命令所傳回的位置：</span><span class="sxs-lookup"><span data-stu-id="0ef38-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="0ef38-173">移至任何 *package\version* 資料夾，並將 `.nupkg` 檔案複製至 `.zip` 檔案，然後開啟該 `.zip` 檔案，並檢查其內的 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="0ef38-174">從 Visual Studio 專案建立 `.nuspec` 時，資訊清單會包含建置套件時取代為專案中資訊的權杖。</span><span class="sxs-lookup"><span data-stu-id="0ef38-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="0ef38-175">請參閱[從 Visual Studio 專案建立 .nuspec](#from-a-visual-studio-project)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="0ef38-176">建立 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-176">Creating the .nuspec file</span></span>

<span data-ttu-id="0ef38-177">建立完整資訊清單一般是從透過下列其中一種方法所產生的基本 `.nuspec` 檔案開始：</span><span class="sxs-lookup"><span data-stu-id="0ef38-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="0ef38-178">以慣例為基礎的工作目錄</span><span class="sxs-lookup"><span data-stu-id="0ef38-178">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="0ef38-179">組件 DLL</span><span class="sxs-lookup"><span data-stu-id="0ef38-179">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="0ef38-180">Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="0ef38-180">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="0ef38-181">含預設值的新檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-181">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="0ef38-182">您接著手動編輯檔案，讓它描述您在最終套件中想要的確切內容。</span><span class="sxs-lookup"><span data-stu-id="0ef38-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="0ef38-183">產生的 `.nuspec` 檔案會包含在使用 `nuget pack` 命令建立套件之前必須修改的預留位置。</span><span class="sxs-lookup"><span data-stu-id="0ef38-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="0ef38-184">如果 `.nuspec` 包含任何預留位置，則該命令會失敗。</span><span class="sxs-lookup"><span data-stu-id="0ef38-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="0ef38-185">從以慣例為基礎的工作目錄</span><span class="sxs-lookup"><span data-stu-id="0ef38-185">From a convention-based working directory</span></span>

<span data-ttu-id="0ef38-186">因為 NuGet 套件只是使用 `.nupkg` 副檔名重新命名的 ZIP 檔案，所以通常最容易在檔案系統上建立您想要的資料夾結構，然後直接從該結構建立 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="0ef38-187">`nuget pack` 命令接著會自動在該資料夾結構中新增所有檔案 (不含任何開頭為 `.` 的資料夾)，以讓您將私人檔案保留在相同的結構中)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="0ef38-188">這種方法的優點是您不需要在資訊清單中指定想要包含在套件中的檔案 (如本主題中稍後所述)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="0ef38-189">您可以只讓建置程序產生套件中完全相同的資料夾結構，而且可以輕鬆地包含可能不屬於專案的其他檔案：</span><span class="sxs-lookup"><span data-stu-id="0ef38-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="0ef38-190">應該插入至目標專案的內容和原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="0ef38-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="0ef38-191">PowerShell 指令碼 (NuGet 2.x 中所使用的套件也可以包含 NuGet 3.x 和更新版本不支援的安裝指令碼)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="0ef38-192">專案中現有組態檔和原始程式碼檔案的轉換。</span><span class="sxs-lookup"><span data-stu-id="0ef38-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="0ef38-193">資料夾慣例如下：</span><span class="sxs-lookup"><span data-stu-id="0ef38-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="0ef38-194">資料夾</span><span class="sxs-lookup"><span data-stu-id="0ef38-194">Folder</span></span> | <span data-ttu-id="0ef38-195">描述</span><span class="sxs-lookup"><span data-stu-id="0ef38-195">Description</span></span> | <span data-ttu-id="0ef38-196">套件安裝時的動作</span><span class="sxs-lookup"><span data-stu-id="0ef38-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ef38-197">(root)</span><span class="sxs-lookup"><span data-stu-id="0ef38-197">(root)</span></span> | <span data-ttu-id="0ef38-198">readme.txt 的位置</span><span class="sxs-lookup"><span data-stu-id="0ef38-198">Location for readme.txt</span></span> | <span data-ttu-id="0ef38-199">安裝套件時，Visual Studio 會顯示套件根目錄中的 readme.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="0ef38-200">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="0ef38-200">lib/{tfm}</span></span> | <span data-ttu-id="0ef38-201">所指定目標架構 Moniker (TFM) 的組件 (`.dll`)、文件 (`.xml`) 和符號 (`.pdb`) 檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="0ef38-202">組件會新增為參考；`.xml` 和 `.pdb` 則會複製至專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="0ef38-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="0ef38-203">請參閱[支援多個目標架構](Supporting-Multiple-Target-Frameworks.md)，以了解如何建立架構目標特定子資料夾。</span><span class="sxs-lookup"><span data-stu-id="0ef38-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="0ef38-204">runtimes</span><span class="sxs-lookup"><span data-stu-id="0ef38-204">runtimes</span></span> | <span data-ttu-id="0ef38-205">架構特定組件 (`.dll`)、符號 (`.pdb`) 和原生資源 (`.pri`) 檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="0ef38-206">組件會新增為參考；其他檔案則會複製至專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="0ef38-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="0ef38-207">請參閱[支援多個目標架構](Supporting-Multiple-Target-Frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="0ef38-208">content</span><span class="sxs-lookup"><span data-stu-id="0ef38-208">content</span></span> | <span data-ttu-id="0ef38-209">任意檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-209">Arbitrary files</span></span> | <span data-ttu-id="0ef38-210">內容會複製至專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="0ef38-210">Contents are copied to the project root.</span></span> <span data-ttu-id="0ef38-211">請將 **content** 資料夾視為最後使用套件的目標應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="0ef38-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="0ef38-212">若要讓套件在應用程式的 */images* 資料夾中新增映像，請將它放在套件的 *content/images* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="0ef38-213">build</span><span class="sxs-lookup"><span data-stu-id="0ef38-213">build</span></span> | <span data-ttu-id="0ef38-214">MSBuild `.targets` 和 `.props` 檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="0ef38-215">自動插入專案檔 (NuGet 2.x) 或 `project.lock.json` (NuGet 3.x+) 中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="0ef38-216">tools</span><span class="sxs-lookup"><span data-stu-id="0ef38-216">tools</span></span> | <span data-ttu-id="0ef38-217">可從套件管理員主控台存取的 Powershell 指令碼和程式</span><span class="sxs-lookup"><span data-stu-id="0ef38-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="0ef38-218">`tools` 資料夾只會新增至套件管理員主控台的 `PATH` 環境變數 (具體而言，建置專案時*「不」*會新增至針對 MSBuild 所設定的 `PATH`)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="0ef38-219">因為您的資料夾結構可以包含任意數目之目標架構的任意數目組件，所以建立可支援多個架構的套件時需要這種方法</span><span class="sxs-lookup"><span data-stu-id="0ef38-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="0ef38-220">在任何情況下，您擁有所要的資料夾結構之後，請在該資料夾中執行下列命令來建立 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="0ef38-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="0ef38-221">同樣地，產生的 `.nuspec` 不會包含資料夾結構中檔案的明確參考。</span><span class="sxs-lookup"><span data-stu-id="0ef38-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="0ef38-222">建立套件時，NuGet 會自動包含所有檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="0ef38-223">不過，您仍然需要編輯資訊清單之其他部分中的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="0ef38-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="0ef38-224">從組件 DLL</span><span class="sxs-lookup"><span data-stu-id="0ef38-224">From an assembly DLL</span></span>

<span data-ttu-id="0ef38-225">在從組件建立套件的簡單案例中，您可以使用下列命令，透過組件的中繼資料產生 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="0ef38-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="0ef38-226">使用這種形式會將資訊清單中的少數預留位置取代為組件中的特定值。</span><span class="sxs-lookup"><span data-stu-id="0ef38-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="0ef38-227">例如，`<id>` 屬性設定為組件名稱，而且 `<version>` 設定為組件版本。</span><span class="sxs-lookup"><span data-stu-id="0ef38-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="0ef38-228">不過，資訊清單中的其他屬性在組件中沒有相符值，因此仍然會包含預留位置。</span><span class="sxs-lookup"><span data-stu-id="0ef38-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="0ef38-229">從 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="0ef38-229">From a Visual Studio project</span></span>

<span data-ttu-id="0ef38-230">從 `.csproj` 或 `.vbproj` 檔案建立 `.nuspec` 十分方便，因為已安裝至這些專案的其他套件會自動參照為相依性。</span><span class="sxs-lookup"><span data-stu-id="0ef38-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="0ef38-231">只需要在與專案檔相同的資料夾中使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="0ef38-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="0ef38-232">產生的 `<project-name>.nuspec` 檔案包含「權杖」，而權杖會在封裝時取代為專案中的值，包含已安裝之任何其他套件的參考。</span><span class="sxs-lookup"><span data-stu-id="0ef38-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="0ef38-233">在專案屬性的兩側，使用 `$` 符號分隔權杖。</span><span class="sxs-lookup"><span data-stu-id="0ef38-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="0ef38-234">例如，透過此方式產生之資訊清單中的 `<id>` 值一般會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="0ef38-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="0ef38-235">在封裝時間，會將此權杖取代為專案檔中的 `AssemblyName` 值。</span><span class="sxs-lookup"><span data-stu-id="0ef38-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="0ef38-236">若要將專案值完全對應至 `.nuspec` 權杖，請參閱[取代權杖參考](../schema/nuspec.md#replacement-tokens)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="0ef38-237">更新專案時，權杖可讓您不需要更新 `.nuspec` 中這類版本號碼的重要值 </span><span class="sxs-lookup"><span data-stu-id="0ef38-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="0ef38-238">(如有需要，您一律可以將權杖取代為常值)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="0ef38-239">請注意，從 Visual Studio 專案工作時，有數個其他封裝選項可用，如後面的[執行 nuget pack 以產生 .nupkg 檔案](#running-nuget-pack-to-generate-the-nupkg-file)所述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="0ef38-240">方案層級套件</span><span class="sxs-lookup"><span data-stu-id="0ef38-240">Solution-level packages</span></span>

<span data-ttu-id="0ef38-241">*僅限 NuGet 2.x。在 NuGet 3.0+ 中無法使用。*</span><span class="sxs-lookup"><span data-stu-id="0ef38-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="0ef38-242">NuGet 2.x 支援可安裝套件管理員主控台工具或其他命令的方案層級套件概念 (`tools` 資料夾內容)，但不會將參考、內容或組建自訂新增至方案中的任何專案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="0ef38-243">這類套件在其直接 `lib`、`content` 或 `build` 資料夾中未包含任何檔案，而其相依性在各自的 `lib`、`content` 或 `build` 資料夾中沒有檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="0ef38-244">NuGet 會追蹤 `.nuget` 資料夾的 `packages.config` 檔案中的已安裝方案層級套件，而不是專案的 `packages.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="0ef38-245">含預設值的新檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-245">New file with default values</span></span>

<span data-ttu-id="0ef38-246">下列命令會建立含預留位置的預設資訊清單，確保您是從正確的檔案結構開始：</span><span class="sxs-lookup"><span data-stu-id="0ef38-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="0ef38-247">如果您省略 \<package-name\>，則產生的檔案是 `Package.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="0ef38-248">如果您提供 `Contoso.Utility.UsefulStuff` 這類名稱，則檔案是 `Contoso.Utility.UsefulStuff.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="0ef38-249">產生的 `.nuspec` 包含 `projectUrl` 這類值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="0ef38-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="0ef38-250">請務必先編輯檔案，再用它來建立最終 `.nupkg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="0ef38-251">選擇唯一的套件識別碼並設定版本號碼</span><span class="sxs-lookup"><span data-stu-id="0ef38-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="0ef38-252">套件識別碼 (`<id>` 項目) 和版本號碼 (`<version>` 項目) 是資訊清單中的兩個最重要值，因為它們可以唯一識別套件中所含的確切程式碼。</span><span class="sxs-lookup"><span data-stu-id="0ef38-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="0ef38-253">**套件識別碼的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="0ef38-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="0ef38-254">**唯一性**：在 nuget.org 內，或只要資源庫裝載套件時，識別碼就必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0ef38-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="0ef38-255">決定識別碼之前，請搜尋適用的資源庫，檢查是否已在使用名稱。</span><span class="sxs-lookup"><span data-stu-id="0ef38-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="0ef38-256">若要避免衝突，不錯的模式是使用您的公司名稱作為識別碼的第一個部分，例如 `Contoso.`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="0ef38-257">**命名空間類似名稱**：遵循與 .NET 中命名空間類似的模式，即使用點標記法，而非連字號。</span><span class="sxs-lookup"><span data-stu-id="0ef38-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="0ef38-258">例如，使用 `Contoso.Utility.UsefulStuff`，而非 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="0ef38-259">套件識別碼符合程式碼中所使用的命名空間時，取用者也會發現它十分有用。</span><span class="sxs-lookup"><span data-stu-id="0ef38-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="0ef38-260">**範例套件**：如果您產生的範例程式碼套件示範如何使用另一個套件，請將 `.Sample` 附加為識別碼的尾碼，如 `Contoso.Utility.UsefulStuff.Sample` 所示 </span><span class="sxs-lookup"><span data-stu-id="0ef38-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="0ef38-261">(範例套件當然會有與另一個套件的相依性)。建立範例套件時，請使用稍早所述以慣例為基礎的工作目錄方法。</span><span class="sxs-lookup"><span data-stu-id="0ef38-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="0ef38-262">在 `content` 資料夾中，於稱為 `\Samples\<identifier>` 的資料夾中排列範例程式碼，而這與 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相同。</span><span class="sxs-lookup"><span data-stu-id="0ef38-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="0ef38-263">**套件版本的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="0ef38-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="0ef38-264">一般而言，請設定套件版本，使其符合程式庫，但這不是絕對必要。</span><span class="sxs-lookup"><span data-stu-id="0ef38-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="0ef38-265">將套件限制為單一組件時，這相當簡單，如[決定要封裝的組件](#deciding-which-assemblies-to-package)稍早所述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="0ef38-266">整體來說，請記住，解析相依性時，NuGet 本身會處理套件版本，而非組件版本。</span><span class="sxs-lookup"><span data-stu-id="0ef38-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="0ef38-267">使用非標準版本方式時，請務必考慮使用 NuGet 版本控制規則，如[套件版本控制](../reference/package-versioning.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="0ef38-268">下面一系列的簡短部落格文章也有助於了解版本控制：</span><span class="sxs-lookup"><span data-stu-id="0ef38-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="0ef38-269">第 1 部分：接受 DLL 挑戰</span><span class="sxs-lookup"><span data-stu-id="0ef38-269">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="0ef38-270">第 2 部分：核心演算法</span><span class="sxs-lookup"><span data-stu-id="0ef38-270">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="0ef38-271">第 3 部分：透過繫結重新導向的統一</span><span class="sxs-lookup"><span data-stu-id="0ef38-271">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="0ef38-272">設定套件類型</span><span class="sxs-lookup"><span data-stu-id="0ef38-272">Setting a package type</span></span>

<span data-ttu-id="0ef38-273">使用 NuGet 3.5+，可以將套件標上特定「套件類型」，指出其預定用途。</span><span class="sxs-lookup"><span data-stu-id="0ef38-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="0ef38-274">未標示類型的套件 (包含使用舊版 NuGet 所建立的所有套件) 預設為 `Dependency` 類型。</span><span class="sxs-lookup"><span data-stu-id="0ef38-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="0ef38-275">`Dependency` 類型套件會將建置或執行階段資產新增至程式庫和應用程式，並且可以安裝至任何專案類型 (假設它們相容)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="0ef38-276">`DotnetCliTool` 類型套件是 [.NET CLI](/dotnet/articles/core/tools/index) 的延伸模組，並且會從命令列予以叫用。</span><span class="sxs-lookup"><span data-stu-id="0ef38-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="0ef38-277">這類套件只能安裝在 .NET Core 專案中，而且不會影響還原作業。</span><span class="sxs-lookup"><span data-stu-id="0ef38-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="0ef38-278">[.NET Core 擴充性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文件提供所有這些專案延伸模組的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0ef38-278">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="0ef38-279">安裝 DotnetCliTool 套件時，Visual Studio 會將套件放入 `project.json` `tools` 節點中，而不是 `dependencies` 節點。</span><span class="sxs-lookup"><span data-stu-id="0ef38-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="0ef38-280">自訂類型套件會使用任意類型識別碼，而其符合與套件識別碼相同的格式規則。</span><span class="sxs-lookup"><span data-stu-id="0ef38-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="0ef38-281">不過，Visual Studio 中的 NuGet 套件管理員無法辨識 `Dependency` 和 `DotnetCliTool` 以外的任何類型。</span><span class="sxs-lookup"><span data-stu-id="0ef38-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="0ef38-282">套件類型設定於 `.nuspec` 檔案或 `project.json` 中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="0ef38-283">在這兩種情況下，針對回溯相容性，最好「不」要明確設定 `Dependency` 類型，而是在未指定類型時改為依賴採用此類型的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="0ef38-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="0ef38-284">`.nuspec`：指出 `<metadata>` 項目的 `packageTypes\packageType` 節點內的套件類型：</span><span class="sxs-lookup"><span data-stu-id="0ef38-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

- <span data-ttu-id="0ef38-285">`project.json`：指出 `packOptions.packageType` 屬性 json 內的套件類型：</span><span class="sxs-lookup"><span data-stu-id="0ef38-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="0ef38-286">新增讀我檔案和其他檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-286">Adding a readme and other files</span></span>

<span data-ttu-id="0ef38-287">若要直接指定要包含在套件中的檔案，請在 `.nuspec` 檔案中使用 `<files>` 節點，而這在 `<metadata>` 標記「後面」：</span><span class="sxs-lookup"><span data-stu-id="0ef38-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Add a readme -->
    <file src="readme.txt" target="" />

    <!-- Add files from an arbitrary folder that's not necessarily in the project -->
    <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="0ef38-288">使用以慣例為基礎的工作目錄方法時，您可以將 readme.txt 放在套件根目錄中，而將其他內容放在 `content` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="0ef38-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="0ef38-289">資訊清單中不需要任何 `<file>` 項目。</span><span class="sxs-lookup"><span data-stu-id="0ef38-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="0ef38-290">當您在套件根目錄中包含名為 `readme.txt` 的檔案時，Visual Studio 會在直接安裝套件之後立即以純文字形式顯示該檔案的內容 </span><span class="sxs-lookup"><span data-stu-id="0ef38-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="0ef38-291">(不會針對安裝為相依性的套件顯示讀我檔案)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="0ef38-292">例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：</span><span class="sxs-lookup"><span data-stu-id="0ef38-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安裝時 NuGet 套件的讀我檔案顯示](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="0ef38-294">如果您在 `.nuspec` 檔案中包含空 `<files>` 節點，則 NuGet 不會包含不在 `lib` 資料夾套件中的任何其他內容。</span><span class="sxs-lookup"><span data-stu-id="0ef38-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="0ef38-295">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="0ef38-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="0ef38-296">在某些情況下，您可能想要在取用您套件的專案中新增自訂組建目標或屬性，例如在建置期間執行自訂工具或程序。</span><span class="sxs-lookup"><span data-stu-id="0ef38-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="0ef38-297">做法是在專案的 `\build` 資料夾內以 `<package_id>.targets` 或 `<package_id>.props` 形式放置檔案 (例如 `Contoso.Utility.UsefulStuff.targets`)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="0ef38-298">根 `\build` 資料夾中的檔案視為適合所有目標架構。</span><span class="sxs-lookup"><span data-stu-id="0ef38-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="0ef38-299">若要提供架構特定檔案，請先將這些檔案放入適當的子資料夾中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0ef38-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="0ef38-300">接著，在 `.nuspec` 檔案中，請務必於 `<files>` 節點中參照這些檔案：</span><span class="sxs-lookup"><span data-stu-id="0ef38-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Include everything in \build -->
    <file src="build\**" target="build" />

    <!-- Other files -->
    <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="0ef38-301">NuGet 2.x 使用 `\build` 檔案安裝套件時，會在指向 `.targets` 和 `.props` 檔案的專案檔中新增 MSBuild `<Import>` 項目 </span><span class="sxs-lookup"><span data-stu-id="0ef38-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="0ef38-302">(`.props` 新增於專案檔頂端；`.targets` 則新增於底端)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="0ef38-303">使用 NuGet 3.x 時，目標不會新增至專案，但可透過 `project.lock.json` 提供。</span><span class="sxs-lookup"><span data-stu-id="0ef38-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="0ef38-304">撰寫包含 COM Interop 組件的套件</span><span class="sxs-lookup"><span data-stu-id="0ef38-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="0ef38-305">包含 COM Interop 組件的套件必須包含適當的[目標檔案](#including-msbuild-props-and-targets-in-a-package)，因此會使用 PackageReference 格式將正確的 `EmbedInteropTypes` 中繼資料新增至專案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="0ef38-306">根據預設，使用 PackageReference 時，所有組件的 `EmbedInteropTypes` 中繼資料一律為 false，因此目標檔案會明確新增此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0ef38-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="0ef38-307">若要避免衝突，目標名稱應該是唯一的；在理想狀況下，使用套件名稱和所內嵌組件的組合，並將下列範例中的 `{InteropAssemblyName}` 取代為該值 </span><span class="sxs-lookup"><span data-stu-id="0ef38-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="0ef38-308">(如需範例，請參閱 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop))。</span><span class="sxs-lookup"><span data-stu-id="0ef38-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="0ef38-309">請注意，使用 `packages.config` 參考格式時，新增套件中組件的參考會讓 NuGet 和 Visual Studio 檢查 COM Interop 組件，並將專案檔中的 `EmbedInteropTypes` 設定為 true。</span><span class="sxs-lookup"><span data-stu-id="0ef38-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="0ef38-310">在此情況下，會覆寫目標。</span><span class="sxs-lookup"><span data-stu-id="0ef38-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="0ef38-311">此外，根據預設，[組建資產不會轉移流動](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="0ef38-312">如這裡所述而撰寫的套件從專案對專案參考提取為可轉移相依性時，即會以不同的方式運作。</span><span class="sxs-lookup"><span data-stu-id="0ef38-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="0ef38-313">套件取用者允許它們流動的方式，是將 PrivateAssets 預設值修改為不包含組建。</span><span class="sxs-lookup"><span data-stu-id="0ef38-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="0ef38-314">執行 nuget pack 以產生 .nupkg 檔案</span><span class="sxs-lookup"><span data-stu-id="0ef38-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="0ef38-315">使用組件或以慣例為基礎的工作目錄時，搭配執行 `nuget pack` 與 `.nuspec` 檔案，並將 `<manifest-name>` 取代為特定檔案名稱，以建立套件：</span><span class="sxs-lookup"><span data-stu-id="0ef38-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="0ef38-316">使用 Visual Studio 專案時，請搭配執行 `nuget pack` 與專案檔，這樣會自動載入專案的 `.nuspec` 檔案，並使用專案檔中的值來取代其內的任何權杖：</span><span class="sxs-lookup"><span data-stu-id="0ef38-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="0ef38-317">因為專案是權杖值的來源，所以需要直接使用專案檔來進行權杖取代。</span><span class="sxs-lookup"><span data-stu-id="0ef38-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="0ef38-318">如果您搭配使用 `nuget pack` 與 `.nuspec` 檔案，則不會進行權杖取代。</span><span class="sxs-lookup"><span data-stu-id="0ef38-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="0ef38-319">在所有情況下，`nuget pack` 都會排除開頭為句點的資料夾；例如 `.git` 或 `.hg`。</span><span class="sxs-lookup"><span data-stu-id="0ef38-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="0ef38-320">NuGet 指出 `.nuspec` 檔案中是否有任何需要修正的錯誤；例如，忘記變更資訊清單中的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="0ef38-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="0ef38-321">`nuget pack` 成功之後，您會有可發行至適合資源庫的 `.nupkg` 檔案，如[發行套件](../create-packages/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="0ef38-322">套件在建立後對其檢查的有用方式是在[套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)工具中開啟它。</span><span class="sxs-lookup"><span data-stu-id="0ef38-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="0ef38-323">這可提供套件內容和其資訊清單的圖形化檢視。</span><span class="sxs-lookup"><span data-stu-id="0ef38-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="0ef38-324">您也可以將所產生的 `.nupkg` 檔案重新命名為 `.zip` 檔案，並直接探索其內容。</span><span class="sxs-lookup"><span data-stu-id="0ef38-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="0ef38-325">其他選項</span><span class="sxs-lookup"><span data-stu-id="0ef38-325">Additional options</span></span>

<span data-ttu-id="0ef38-326">您可以搭配使用各種命令列參數與 `nuget pack` 來排除檔案、覆寫資訊清單中的版本號碼、變更輸出資料夾，以及其他功能。</span><span class="sxs-lookup"><span data-stu-id="0ef38-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="0ef38-327">如需完整清單，請參閱 [pack 命令參考](../tools/cli-ref-pack.md)。</span><span class="sxs-lookup"><span data-stu-id="0ef38-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="0ef38-328">下列選項是 Visual Studio 專案通用的幾個選項：</span><span class="sxs-lookup"><span data-stu-id="0ef38-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="0ef38-329">**參考的專案**：如果專案參考其他專案，則您可以使用 `-IncludeReferencedProjects` 選項，將參考的專案新增為套件的一部分或相依性：</span><span class="sxs-lookup"><span data-stu-id="0ef38-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="0ef38-330">這個包含程序是遞迴式，因此，如果 `MyProject.csproj` 參考專案 B 和 C，然後這些專案參考 D、E 和 F，則套件中會包含 B、C、D、E 和 F 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="0ef38-331">如果參考的專案包含專屬 `.nuspec` 檔案，則 NuGet 會改為將該參考的專案新增為相依性。</span><span class="sxs-lookup"><span data-stu-id="0ef38-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="0ef38-332">您需要個別封裝和發行該專案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="0ef38-333">**組建組態**：NuGet 預設會使用專案檔中所設定的預設組建組態，通常是「偵錯」。</span><span class="sxs-lookup"><span data-stu-id="0ef38-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="0ef38-334">若要從不同組建組態來封裝檔案 (例如「發行」)，請搭配使用 `-properties` 選項與下列組態：</span><span class="sxs-lookup"><span data-stu-id="0ef38-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="0ef38-335">**符號**：若要包含可讓取用者在偵錯工具中逐步執行您套件程式碼的符號，請使用 `-Symbols` 選項：</span><span class="sxs-lookup"><span data-stu-id="0ef38-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="0ef38-336">測試套件安裝</span><span class="sxs-lookup"><span data-stu-id="0ef38-336">Testing package installation</span></span>

<span data-ttu-id="0ef38-337">發行套件之前，您通常會想要測試將套件安裝至專案的程序。</span><span class="sxs-lookup"><span data-stu-id="0ef38-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="0ef38-338">測試可確定必要檔案最後都在專案的正確位置。</span><span class="sxs-lookup"><span data-stu-id="0ef38-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="0ef38-339">您可以使用一般[套件安裝步驟](../Quickstart/Use-a-Package.md)，以在 Visual Studio 中或命令列上手動測試安裝。</span><span class="sxs-lookup"><span data-stu-id="0ef38-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="0ef38-340">自動化測試的基本程序如下：</span><span class="sxs-lookup"><span data-stu-id="0ef38-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="0ef38-341">將 `.nupkg` 檔案複製至本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="0ef38-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="0ef38-342">使用 `nuget sources -name <name> -source <path>` 命令，將資料夾新增至套件來源 (請參閱 [nuget sources](../tools/cli-ref-sources.md))。</span><span class="sxs-lookup"><span data-stu-id="0ef38-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="0ef38-343">請注意，您只需要在任何指定電腦上設定此本機來源一次。</span><span class="sxs-lookup"><span data-stu-id="0ef38-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="0ef38-344">使用 `nuget install <packageID> -source <name>` 以從該來源安裝套件，其中 `<name>` 符合您指定至 `nuget sources` 的來源名稱。</span><span class="sxs-lookup"><span data-stu-id="0ef38-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="0ef38-345">指定來源可確保單獨從該來源安裝套件。</span><span class="sxs-lookup"><span data-stu-id="0ef38-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="0ef38-346">檢查檔案系統，確認已正確安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef38-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ef38-347">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ef38-347">Next Steps</span></span>

<span data-ttu-id="0ef38-348">建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../create-packages/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0ef38-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="0ef38-349">您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：</span><span class="sxs-lookup"><span data-stu-id="0ef38-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="0ef38-350">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="0ef38-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="0ef38-351">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="0ef38-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="0ef38-352">原始程式檔和組態檔的轉換</span><span class="sxs-lookup"><span data-stu-id="0ef38-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="0ef38-353">當地語系化</span><span class="sxs-lookup"><span data-stu-id="0ef38-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="0ef38-354">發行前版本</span><span class="sxs-lookup"><span data-stu-id="0ef38-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="0ef38-355">最後，請注意其他套件類型：</span><span class="sxs-lookup"><span data-stu-id="0ef38-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="0ef38-356">原生套件</span><span class="sxs-lookup"><span data-stu-id="0ef38-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="0ef38-357">符號套件</span><span class="sxs-lookup"><span data-stu-id="0ef38-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
