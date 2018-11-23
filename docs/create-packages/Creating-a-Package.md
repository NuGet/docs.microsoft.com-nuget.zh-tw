---
title: 如何建立 NuGet 套件
description: NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類索引鍵決策點。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: db02089bec3d2b8c001518fa0542375dc5418eb8
ms.sourcegitcommit: c825eb7e222d4a551431643f5b5617ae868ebe0a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/19/2018
ms.locfileid: "51944063"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="85a7e-103">建立 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="85a7e-103">Creating NuGet packages</span></span>

<span data-ttu-id="85a7e-104">不論套件的功能或所含程式碼為何，您都可以使用 `nuget.exe` 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。</span><span class="sxs-lookup"><span data-stu-id="85a7e-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="85a7e-105">若要安裝 `nuget.exe`，請參閱[安裝 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="85a7e-106">請注意，Visual Studio 不會自動包含 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="85a7e-107">技術上而言，NuGet 套件就只是已重新命名為 `.nupkg` 副檔名且其內容符合特定慣例的 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="85a7e-108">本主題描述如何建立符合這些慣例之套件的詳細程序。</span><span class="sxs-lookup"><span data-stu-id="85a7e-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="85a7e-109">如需詳細的逐步解說，請參閱[快速入門：建立和發行套件](../quickstart/create-and-publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="85a7e-110">封裝開始於已編譯的程式碼 (組件)、符號 (和) 您想要以套件形式傳遞的其他檔案 (請參閱[概觀和工作流程](overview-and-workflow.md))。</span><span class="sxs-lookup"><span data-stu-id="85a7e-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="85a7e-111">此流程與編譯或產生進入套件的檔案無關，但您可以擷取專案檔中的資訊保持已編譯的組件與套件同步。</span><span class="sxs-lookup"><span data-stu-id="85a7e-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="85a7e-112">本主題適用於使用 Visual Studio 2017 和 NuGet 4.0+ 的 .NET Core 專案以外的專案類型。</span><span class="sxs-lookup"><span data-stu-id="85a7e-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="85a7e-113">在這些 .NET Core 專案中，NuGet 會直接使用專案檔中的資訊。</span><span class="sxs-lookup"><span data-stu-id="85a7e-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="85a7e-114">如需詳細資料，請參閱[使用 Visual Studio 2017 建立 .NET Standard 套件](../guides/create-net-standard-packages-vs2017.md)和 [NuGet 封裝和還原為 MSBuild 目標](../reference/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="85a7e-115">決定要封裝的組件</span><span class="sxs-lookup"><span data-stu-id="85a7e-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="85a7e-116">大部分的一般用途套件都會包含其他開發人員可以在其專屬專案中使用的一或多個組件。</span><span class="sxs-lookup"><span data-stu-id="85a7e-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="85a7e-117">一般而言，最好一個 NuGet 套件一個組件，前提是每個組件都可以獨立使用。</span><span class="sxs-lookup"><span data-stu-id="85a7e-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="85a7e-118">例如，如果您有與 `Parser.dll` 相依的 `Utilities.dll`，而且 `Parser.dll` 可以單獨使用，則會為每個項目建立一個套件。</span><span class="sxs-lookup"><span data-stu-id="85a7e-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="85a7e-119">這樣做可讓開發人員單獨使用 `Parser.dll` 和 `Utilities.dll`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="85a7e-120">如果您的程式庫包含多個無法單獨使用的組件，則最好將它們結合成單一套件。</span><span class="sxs-lookup"><span data-stu-id="85a7e-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="85a7e-121">使用上述範例時，如果 `Parser.dll` 所包含的程式碼僅供 `Utilities.dll` 使用，則最好將 `Parser.dll` 放在相同的套件中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="85a7e-122">同樣地，如果 `Utilities.dll` 與 `Utilities.resources.dll` 相依 (再提醒一次，後者無法單獨使用)，則請將這兩個放在相同的套件中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="85a7e-123">資源其實是特殊案例。</span><span class="sxs-lookup"><span data-stu-id="85a7e-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="85a7e-124">將套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，但「排除」名為 `.resources.dll` 的參考，因為它們假設為當地語系化附屬組件 (請參閱[建立當地語系化套件](creating-localized-packages.md))。</span><span class="sxs-lookup"><span data-stu-id="85a7e-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="85a7e-125">因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="85a7e-126">如果您的程式庫包含 COM Interop 組件，請遵循[撰寫包含 COM Interop 組件的套件](#authoring-packages-with-com-interop-assemblies)中的其他指導方針。</span><span class="sxs-lookup"><span data-stu-id="85a7e-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="85a7e-127">.nuspec 檔案的角色和結構</span><span class="sxs-lookup"><span data-stu-id="85a7e-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="85a7e-128">知道您想要封裝的檔案之後，下個步驟就是在 `.nuspec` XML 檔案中建立套件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="85a7e-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="85a7e-129">資訊清單：</span><span class="sxs-lookup"><span data-stu-id="85a7e-129">The manifest:</span></span>

1. <span data-ttu-id="85a7e-130">描述套件內容而且本身包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="85a7e-131">驅使建立套件並指示 NuGet 如何將套件安裝至專案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="85a7e-132">例如，資訊清單會識別其他套件相依性；因此，安裝主要套件時，NuGet 也可以安裝這些相依性。</span><span class="sxs-lookup"><span data-stu-id="85a7e-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="85a7e-133">包含必要和選擇性屬性，如下所述。</span><span class="sxs-lookup"><span data-stu-id="85a7e-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="85a7e-134">如需確切詳細資料 (包含這裡未提及的其他屬性)，請參閱 [.nuspec 參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="85a7e-135">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="85a7e-135">Required properties:</span></span>

- <span data-ttu-id="85a7e-136">套件識別碼，其在裝載套件的資源庫內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="85a7e-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="85a7e-137">*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="85a7e-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="85a7e-138">主機上應該會出現套件標題 (例如 nuget.org)</span><span class="sxs-lookup"><span data-stu-id="85a7e-138">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="85a7e-139">作者和擁有者資訊。</span><span class="sxs-lookup"><span data-stu-id="85a7e-139">Author and owner information.</span></span>
- <span data-ttu-id="85a7e-140">套件的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="85a7e-140">A long description of the package.</span></span>

<span data-ttu-id="85a7e-141">常見的選擇性屬性：</span><span class="sxs-lookup"><span data-stu-id="85a7e-141">Common optional properties:</span></span>

- <span data-ttu-id="85a7e-142">版本資訊</span><span class="sxs-lookup"><span data-stu-id="85a7e-142">Release notes</span></span>
- <span data-ttu-id="85a7e-143">著作權資訊</span><span class="sxs-lookup"><span data-stu-id="85a7e-143">Copyright information</span></span>
- <span data-ttu-id="85a7e-144">[Visual Studio 中的套件管理員 UI](../tools/package-manager-ui.md) 的簡短描述</span><span class="sxs-lookup"><span data-stu-id="85a7e-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="85a7e-145">地區設定識別碼</span><span class="sxs-lookup"><span data-stu-id="85a7e-145">A locale ID</span></span>
- <span data-ttu-id="85a7e-146">專案 URL</span><span class="sxs-lookup"><span data-stu-id="85a7e-146">Project URL</span></span>
- <span data-ttu-id="85a7e-147">運算式或檔案形式的授權 (`licenseUrl` 即將淘汰，請使用 [`license` nuspec 中繼資料元素](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="85a7e-147">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="85a7e-148">圖示 URL</span><span class="sxs-lookup"><span data-stu-id="85a7e-148">An icon URL</span></span>
- <span data-ttu-id="85a7e-149">相依性和參考的清單</span><span class="sxs-lookup"><span data-stu-id="85a7e-149">Lists of dependencies and references</span></span>
- <span data-ttu-id="85a7e-150">協助進行資源庫搜尋的標記</span><span class="sxs-lookup"><span data-stu-id="85a7e-150">Tags that assist in gallery searches</span></span>

<span data-ttu-id="85a7e-151">下列一般 (但虛構的) `.nuspec` 檔案具有可描述屬性的註解：</span><span class="sxs-lookup"><span data-stu-id="85a7e-151">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
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

<span data-ttu-id="85a7e-152">如需宣告相依性以及指定版本號碼的詳細資料，請參閱[套件版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-152">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="85a7e-153">在 `dependency` 項目上使用 `include` 和 `exclude` 屬性，也可以將相依性中的資產直接用於套件中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-153">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="85a7e-154">請參閱 [.nuspec 參考 - 相依性](../reference/nuspec.md#dependencies)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-154">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="85a7e-155">因為資訊清單會包含在透過它所建立的套件中，所以檢查現有套件就可以找到任意數目的其他範例。</span><span class="sxs-lookup"><span data-stu-id="85a7e-155">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="85a7e-156">不錯的來源是您電腦上的 *global-packages* 資料夾，即下列命令所傳回的位置：</span><span class="sxs-lookup"><span data-stu-id="85a7e-156">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="85a7e-157">移至任何 *package\version* 資料夾，並將 `.nupkg` 檔案複製至 `.zip` 檔案，然後開啟該 `.zip` 檔案，並檢查其內的 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-157">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="85a7e-158">從 Visual Studio 專案建立 `.nuspec` 時，資訊清單會包含建置套件時取代為專案中資訊的權杖。</span><span class="sxs-lookup"><span data-stu-id="85a7e-158">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="85a7e-159">請參閱[從 Visual Studio 專案建立 .nuspec](#from-a-visual-studio-project)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-159">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="85a7e-160">建立 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-160">Creating the .nuspec file</span></span>

<span data-ttu-id="85a7e-161">建立完整資訊清單一般是從透過下列其中一種方法所產生的基本 `.nuspec` 檔案開始：</span><span class="sxs-lookup"><span data-stu-id="85a7e-161">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="85a7e-162">以慣例為基礎的工作目錄</span><span class="sxs-lookup"><span data-stu-id="85a7e-162">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="85a7e-163">組件 DLL</span><span class="sxs-lookup"><span data-stu-id="85a7e-163">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="85a7e-164">Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="85a7e-164">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="85a7e-165">含預設值的新檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-165">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="85a7e-166">您接著手動編輯檔案，讓它描述您在最終套件中想要的確切內容。</span><span class="sxs-lookup"><span data-stu-id="85a7e-166">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="85a7e-167">產生的 `.nuspec` 檔案會包含在使用 `nuget pack` 命令建立套件之前必須修改的預留位置。</span><span class="sxs-lookup"><span data-stu-id="85a7e-167">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="85a7e-168">如果 `.nuspec` 包含任何預留位置，則該命令會失敗。</span><span class="sxs-lookup"><span data-stu-id="85a7e-168">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="85a7e-169">從以慣例為基礎的工作目錄</span><span class="sxs-lookup"><span data-stu-id="85a7e-169">From a convention-based working directory</span></span>

<span data-ttu-id="85a7e-170">因為 NuGet 套件只是使用 `.nupkg` 副檔名重新命名的 ZIP 檔案，所以通常很容易即可在本機檔系統上，建立所需的資料夾結構，然後直接從該結構建立 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-170">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="85a7e-171">`nuget pack` 命令接著會自動在該資料夾結構中新增所有檔案 (不包含任何以 `.` 開頭的資料夾，供您以相同的結構保留私人檔案)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-171">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="85a7e-172">這種方法的優點是您不需要在資訊清單中指定想要包含在套件中的檔案 (如本主題中稍後所述)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-172">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="85a7e-173">您可以只讓建置程序產生套件中完全相同的資料夾結構，而且可以輕鬆地包含可能不屬於專案的其他檔案：</span><span class="sxs-lookup"><span data-stu-id="85a7e-173">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="85a7e-174">應該插入至目標專案的內容和原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="85a7e-174">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="85a7e-175">PowerShell 指令碼 (NuGet 2.x 中所使用的套件也可以包含 NuGet 3.x 和更新版本不支援的安裝指令碼)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-175">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="85a7e-176">專案中現有組態檔和原始程式碼檔案的轉換。</span><span class="sxs-lookup"><span data-stu-id="85a7e-176">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="85a7e-177">資料夾慣例如下：</span><span class="sxs-lookup"><span data-stu-id="85a7e-177">The folder conventions are as follows:</span></span>

| <span data-ttu-id="85a7e-178">資料夾</span><span class="sxs-lookup"><span data-stu-id="85a7e-178">Folder</span></span> | <span data-ttu-id="85a7e-179">描述</span><span class="sxs-lookup"><span data-stu-id="85a7e-179">Description</span></span> | <span data-ttu-id="85a7e-180">套件安裝時的動作</span><span class="sxs-lookup"><span data-stu-id="85a7e-180">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85a7e-181">(root)</span><span class="sxs-lookup"><span data-stu-id="85a7e-181">(root)</span></span> | <span data-ttu-id="85a7e-182">readme.txt 的位置</span><span class="sxs-lookup"><span data-stu-id="85a7e-182">Location for readme.txt</span></span> | <span data-ttu-id="85a7e-183">安裝套件時，Visual Studio 會顯示套件根目錄中的 readme.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-183">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="85a7e-184">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="85a7e-184">lib/{tfm}</span></span> | <span data-ttu-id="85a7e-185">所指定目標架構 Moniker (TFM) 的組件 (`.dll`)、文件 (`.xml`) 和符號 (`.pdb`) 檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-185">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="85a7e-186">組件會新增為編譯與執行階段的參考；`.xml` 與 `.pdb` 則會複製到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="85a7e-186">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="85a7e-187">請參閱[支援多個目標架構](supporting-multiple-target-frameworks.md)，以了解如何建立架構目標特定子資料夾。</span><span class="sxs-lookup"><span data-stu-id="85a7e-187">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="85a7e-188">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="85a7e-188">ref/{tfm}</span></span> | <span data-ttu-id="85a7e-189">所指定目標 Framework Moniker (TFM) 的組件 (`.dll`) 與符號 (`.pdb`) 檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-189">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="85a7e-190">組件只會針對編譯階段新增為參考；因此不會有任何項目被複製到專案 bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="85a7e-190">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="85a7e-191">runtimes</span><span class="sxs-lookup"><span data-stu-id="85a7e-191">runtimes</span></span> | <span data-ttu-id="85a7e-192">架構特定組件 (`.dll`)、符號 (`.pdb`) 和原生資源 (`.pri`) 檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-192">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="85a7e-193">組件只會針對執行階段新增為參考；其他檔案則會複製至專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="85a7e-193">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="85a7e-194">`/ref/{tfm}` 資料夾下一律必須有對應的 (TFM) `AnyCPU` 特定組件，才能提供對應的編譯階段組件。</span><span class="sxs-lookup"><span data-stu-id="85a7e-194">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="85a7e-195">請參閱[支援多個目標架構](supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-195">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="85a7e-196">content</span><span class="sxs-lookup"><span data-stu-id="85a7e-196">content</span></span> | <span data-ttu-id="85a7e-197">任意檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-197">Arbitrary files</span></span> | <span data-ttu-id="85a7e-198">內容會複製至專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="85a7e-198">Contents are copied to the project root.</span></span> <span data-ttu-id="85a7e-199">請將 **content** 資料夾視為最後使用套件的目標應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="85a7e-199">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="85a7e-200">若要讓套件在應用程式的 */images* 資料夾中新增映像，請將它放在套件的 *content/images* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-200">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="85a7e-201">build</span><span class="sxs-lookup"><span data-stu-id="85a7e-201">build</span></span> | <span data-ttu-id="85a7e-202">MSBuild `.targets` 和 `.props` 檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-202">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="85a7e-203">自動插入專案檔或 `project.lock.json` (NuGet 3.x+) 中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-203">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="85a7e-204">tools</span><span class="sxs-lookup"><span data-stu-id="85a7e-204">tools</span></span> | <span data-ttu-id="85a7e-205">可從套件管理員主控台存取的 Powershell 指令碼和程式</span><span class="sxs-lookup"><span data-stu-id="85a7e-205">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="85a7e-206">`tools` 資料夾只會新增至套件管理員主控台的 `PATH` 環境變數 (具體而言，建置專案時 *「不」* 會新增至針對 MSBuild 所設定的 `PATH`)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-206">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="85a7e-207">因為您的資料夾結構可包含任意數目之目標架構的任意數目組件，所以建立可支援多重架構的套件時，需要使用此種方法。</span><span class="sxs-lookup"><span data-stu-id="85a7e-207">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="85a7e-208">在任何情況下，您擁有所要的資料夾結構之後，請在該資料夾中執行下列命令來建立 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="85a7e-208">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="85a7e-209">同樣地，產生的 `.nuspec` 不會包含資料夾結構中檔案的明確參考。</span><span class="sxs-lookup"><span data-stu-id="85a7e-209">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="85a7e-210">建立套件時，NuGet 會自動包含所有檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-210">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="85a7e-211">不過，您仍然需要編輯資訊清單之其他部分中的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="85a7e-211">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="85a7e-212">從組件 DLL</span><span class="sxs-lookup"><span data-stu-id="85a7e-212">From an assembly DLL</span></span>

<span data-ttu-id="85a7e-213">在從組件建立套件的簡單案例中，您可以使用下列命令，透過組件的中繼資料產生 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="85a7e-213">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="85a7e-214">使用這種形式會將資訊清單中的少數預留位置取代為組件中的特定值。</span><span class="sxs-lookup"><span data-stu-id="85a7e-214">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="85a7e-215">例如，`<id>` 屬性設定為組件名稱，而且 `<version>` 設定為組件版本。</span><span class="sxs-lookup"><span data-stu-id="85a7e-215">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="85a7e-216">不過，資訊清單中的其他屬性在組件中沒有相符值，因此仍然會包含預留位置。</span><span class="sxs-lookup"><span data-stu-id="85a7e-216">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="85a7e-217">從 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="85a7e-217">From a Visual Studio project</span></span>

<span data-ttu-id="85a7e-218">從 `.csproj` 或 `.vbproj` 檔案建立 `.nuspec` 十分方便，因為已安裝至這些專案的其他套件會自動參照為相依性。</span><span class="sxs-lookup"><span data-stu-id="85a7e-218">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="85a7e-219">只需要在與專案檔相同的資料夾中使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="85a7e-219">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="85a7e-220">產生的 `<project-name>.nuspec` 檔案包含「權杖」，而權杖會在封裝時取代為專案中的值，包含已安裝之任何其他套件的參考。</span><span class="sxs-lookup"><span data-stu-id="85a7e-220">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="85a7e-221">在專案屬性的兩側，使用 `$` 符號分隔權杖。</span><span class="sxs-lookup"><span data-stu-id="85a7e-221">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="85a7e-222">例如，透過此方式產生之資訊清單中的 `<id>` 值一般會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="85a7e-222">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="85a7e-223">在封裝時間，會將此權杖取代為專案檔中的 `AssemblyName` 值。</span><span class="sxs-lookup"><span data-stu-id="85a7e-223">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="85a7e-224">若要將專案值完全對應至 `.nuspec` 權杖，請參閱[取代權杖參考](../reference/nuspec.md#replacement-tokens)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-224">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="85a7e-225">更新專案時，權杖可讓您不需要更新 `.nuspec` 中這類版本號碼的重要值 </span><span class="sxs-lookup"><span data-stu-id="85a7e-225">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="85a7e-226">(如有需要，您一律可以將權杖取代為常值)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-226">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="85a7e-227">請注意，從 Visual Studio 專案工作時，有數個其他封裝選項可用，如後面的[執行 nuget pack 以產生 .nupkg 檔案](#running-nuget-pack-to-generate-the-nupkg-file)所述。</span><span class="sxs-lookup"><span data-stu-id="85a7e-227">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="85a7e-228">方案層級套件</span><span class="sxs-lookup"><span data-stu-id="85a7e-228">Solution-level packages</span></span>

<span data-ttu-id="85a7e-229">*僅限 NuGet 2.x。在 NuGet 3.0+ 中無法使用。*</span><span class="sxs-lookup"><span data-stu-id="85a7e-229">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="85a7e-230">NuGet 2.x 支援可安裝套件管理員主控台工具或其他命令的方案層級套件概念 (`tools` 資料夾內容)，但不會將參考、內容或組建自訂新增至方案中的任何專案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-230">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="85a7e-231">這類套件在其直接 `lib`、`content` 或 `build` 資料夾中未包含任何檔案，而其相依性在各自的 `lib`、`content` 或 `build` 資料夾中沒有檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-231">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="85a7e-232">NuGet 會追蹤 `.nuget` 資料夾的 `packages.config` 檔案中的已安裝方案層級套件，而不是專案的 `packages.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-232">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="85a7e-233">含預設值的新檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-233">New file with default values</span></span>

<span data-ttu-id="85a7e-234">下列命令會建立含預留位置的預設資訊清單，確保您是從正確的檔案結構開始：</span><span class="sxs-lookup"><span data-stu-id="85a7e-234">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="85a7e-235">如果您省略 \<package-name\>，則產生的檔案是 `Package.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-235">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="85a7e-236">如果您提供 `Contoso.Utility.UsefulStuff` 這類名稱，則檔案是 `Contoso.Utility.UsefulStuff.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-236">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="85a7e-237">產生的 `.nuspec` 包含 `projectUrl` 這類值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="85a7e-237">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="85a7e-238">請務必先編輯檔案，再用它來建立最終 `.nupkg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-238">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="85a7e-239">選擇唯一的套件識別碼並設定版本號碼</span><span class="sxs-lookup"><span data-stu-id="85a7e-239">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="85a7e-240">套件識別碼 (`<id>` 項目) 和版本號碼 (`<version>` 項目) 是資訊清單中的兩個最重要值，因為它們可以唯一識別套件中所含的確切程式碼。</span><span class="sxs-lookup"><span data-stu-id="85a7e-240">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="85a7e-241">**套件識別碼的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="85a7e-241">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="85a7e-242">**唯一性**：在 nuget.org 內，或只要資源庫裝載套件時，識別碼就必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="85a7e-242">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="85a7e-243">決定識別碼之前，請搜尋適用的資源庫，檢查是否已在使用名稱。</span><span class="sxs-lookup"><span data-stu-id="85a7e-243">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="85a7e-244">若要避免衝突，不錯的模式是使用您的公司名稱作為識別碼的第一個部分，例如 `Contoso.`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-244">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="85a7e-245">**命名空間類似名稱**：遵循與 .NET 中命名空間類似的模式，即使用點標記法，而非連字號。</span><span class="sxs-lookup"><span data-stu-id="85a7e-245">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="85a7e-246">例如，使用 `Contoso.Utility.UsefulStuff`，而非 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-246">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="85a7e-247">套件識別碼符合程式碼中所使用的命名空間時，取用者也會發現它十分有用。</span><span class="sxs-lookup"><span data-stu-id="85a7e-247">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="85a7e-248">**範例套件**：如果您產生的範例程式碼套件示範如何使用另一個套件，請將 `.Sample` 附加為識別碼的尾碼，如 `Contoso.Utility.UsefulStuff.Sample` 所示 </span><span class="sxs-lookup"><span data-stu-id="85a7e-248">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="85a7e-249">(範例套件當然會有與另一個套件的相依性)。建立範例套件時，請使用稍早所述以慣例為基礎的工作目錄方法。</span><span class="sxs-lookup"><span data-stu-id="85a7e-249">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="85a7e-250">在 `content` 資料夾中，於稱為 `\Samples\<identifier>` 的資料夾中排列範例程式碼，而這與 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相同。</span><span class="sxs-lookup"><span data-stu-id="85a7e-250">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="85a7e-251">**套件版本的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="85a7e-251">**Best practices for the package version:**</span></span>

- <span data-ttu-id="85a7e-252">一般而言，請設定套件版本，使其符合程式庫，但這不是絕對必要。</span><span class="sxs-lookup"><span data-stu-id="85a7e-252">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="85a7e-253">將套件限制為單一組件時，這相當簡單，如[決定要封裝的組件](#deciding-which-assemblies-to-package)稍早所述。</span><span class="sxs-lookup"><span data-stu-id="85a7e-253">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="85a7e-254">整體來說，請記住，解析相依性時，NuGet 本身會處理套件版本，而非組件版本。</span><span class="sxs-lookup"><span data-stu-id="85a7e-254">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="85a7e-255">使用非標準版本方式時，請務必考慮使用 NuGet 版本控制規則，如[套件版本控制](../reference/package-versioning.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="85a7e-255">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="85a7e-256">下面一系列的簡短部落格文章也有助於了解版本控制：</span><span class="sxs-lookup"><span data-stu-id="85a7e-256">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="85a7e-257">第 1 部分：接受 DLL 挑戰</span><span class="sxs-lookup"><span data-stu-id="85a7e-257">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="85a7e-258">第 2 部分：核心演算法</span><span class="sxs-lookup"><span data-stu-id="85a7e-258">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="85a7e-259">第 3 部分：透過繫結重新導向的統一</span><span class="sxs-lookup"><span data-stu-id="85a7e-259">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="85a7e-260">設定套件類型</span><span class="sxs-lookup"><span data-stu-id="85a7e-260">Setting a package type</span></span>

<span data-ttu-id="85a7e-261">使用 NuGet 3.5+，可以將套件標上特定「套件類型」，指出其預定用途。</span><span class="sxs-lookup"><span data-stu-id="85a7e-261">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="85a7e-262">未標示類型的套件 (包含使用舊版 NuGet 所建立的所有套件) 預設為 `Dependency` 類型。</span><span class="sxs-lookup"><span data-stu-id="85a7e-262">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="85a7e-263">`Dependency` 類型套件會將建置或執行階段資產新增至程式庫和應用程式，並且可以安裝至任何專案類型 (假設它們相容)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-263">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="85a7e-264">`DotnetCliTool` 類型套件是 [.NET CLI](/dotnet/articles/core/tools/index) 的延伸模組，並且會從命令列予以叫用。</span><span class="sxs-lookup"><span data-stu-id="85a7e-264">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="85a7e-265">這類套件只能安裝在 .NET Core 專案中，而且不會影響還原作業。</span><span class="sxs-lookup"><span data-stu-id="85a7e-265">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="85a7e-266">[.NET Core 擴充性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文件提供所有這些專案延伸模組的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="85a7e-266">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="85a7e-267">自訂類型套件會使用任意類型識別碼，而其符合與套件識別碼相同的格式規則。</span><span class="sxs-lookup"><span data-stu-id="85a7e-267">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="85a7e-268">不過，Visual Studio 中的 NuGet 套件管理員無法辨識 `Dependency` 和 `DotnetCliTool` 以外的任何類型。</span><span class="sxs-lookup"><span data-stu-id="85a7e-268">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="85a7e-269">套件類型是設定在 `.nuspec` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-269">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="85a7e-270">針對回溯相容性，最好「不要」明確設定 `Dependency` 類型，而是在未指定類型時改為依賴採用此類型的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="85a7e-270">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="85a7e-271">`.nuspec`：指出 `<metadata>` 項目的 `packageTypes\packageType` 節點內的套件類型：</span><span class="sxs-lookup"><span data-stu-id="85a7e-271">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="85a7e-272">新增讀我檔案和其他檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-272">Adding a readme and other files</span></span>

<span data-ttu-id="85a7e-273">若要直接指定要包含在套件中的檔案，請在 `.nuspec` 檔案中使用 `<files>` 節點，而這在 `<metadata>` 標記「後面」：</span><span class="sxs-lookup"><span data-stu-id="85a7e-273">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="85a7e-274">使用以慣例為基礎的工作目錄方法時，您可以將 readme.txt 放在套件根目錄中，而將其他內容放在 `content` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-274">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="85a7e-275">資訊清單中不需要任何 `<file>` 項目。</span><span class="sxs-lookup"><span data-stu-id="85a7e-275">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="85a7e-276">當您在套件根目錄中包含名為 `readme.txt` 的檔案時，Visual Studio 會在直接安裝套件之後立即以純文字形式顯示該檔案的內容 </span><span class="sxs-lookup"><span data-stu-id="85a7e-276">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="85a7e-277">(不會針對安裝為相依性的套件顯示讀我檔案)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-277">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="85a7e-278">例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：</span><span class="sxs-lookup"><span data-stu-id="85a7e-278">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安裝時 NuGet 套件的讀我檔案顯示](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="85a7e-280">如果您在 `.nuspec` 檔案中包含空 `<files>` 節點，則 NuGet 不會包含不在 `lib` 資料夾套件中的任何其他內容。</span><span class="sxs-lookup"><span data-stu-id="85a7e-280">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="85a7e-281">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="85a7e-281">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="85a7e-282">在某些情況下，您可能想要在取用您套件的專案中新增自訂組建目標或屬性，例如在建置期間執行自訂工具或程序。</span><span class="sxs-lookup"><span data-stu-id="85a7e-282">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="85a7e-283">做法是在專案的 `\build` 資料夾內以 `<package_id>.targets` 或 `<package_id>.props` 形式放置檔案 (例如 `Contoso.Utility.UsefulStuff.targets`)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-283">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="85a7e-284">根 `\build` 資料夾中的檔案視為適合所有目標架構。</span><span class="sxs-lookup"><span data-stu-id="85a7e-284">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="85a7e-285">若要提供架構專屬的檔案，請先將其置於適當的子資料夾中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85a7e-285">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="85a7e-286">接著，在 `.nuspec` 檔案中，請務必於 `<files>` 節點中參照這些檔案：</span><span class="sxs-lookup"><span data-stu-id="85a7e-286">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
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

<span data-ttu-id="85a7e-287">[NuGet 2.5 引進了](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)在套件中包含 MSBuild pros 和 targets 的做法，因此建議您將 `minClientVersion="2.5"` 屬性新增到 `metadata` 元素，以指出使用套件所需的最低 NuGet 用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="85a7e-287">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="85a7e-288">當 NuGet 安裝含有 `\build` 檔案的套件時，會在指向 `.targets` 和 `.props` 檔案的專案檔中新增 MSBuild `<Import>` 項目。</span><span class="sxs-lookup"><span data-stu-id="85a7e-288">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="85a7e-289">(`.props` 新增於專案檔頂端；`.targets` 則新增於底端)。針對每個目標框架新增不同的條件式 MSBuild`<Import>` 元素。</span><span class="sxs-lookup"><span data-stu-id="85a7e-289">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="85a7e-290">用於跨框架目標的 MSBuild `.props` 和 `.targets` 檔案可以放在 `\buildCrossTargeting` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="85a7e-290">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="85a7e-291">在套件安裝期間，NuGet 會將對應的 `<Import>` 元素新增到有條件的專案檔中，即未設定目標框架 (MSBuild 屬性 `$(TargetFramework)` 必須是空的)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-291">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="85a7e-292">使用 NuGet 3.x 時，目標不會新增至專案，但可透過 `project.lock.json` 提供。</span><span class="sxs-lookup"><span data-stu-id="85a7e-292">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="85a7e-293">撰寫包含 COM Interop 組件的套件</span><span class="sxs-lookup"><span data-stu-id="85a7e-293">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="85a7e-294">包含 COM Interop 組件的套件必須包含適當的[目標檔案](#including-msbuild-props-and-targets-in-a-package)，因此會使用 PackageReference 格式將正確的 `EmbedInteropTypes` 中繼資料新增至專案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-294">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="85a7e-295">根據預設，使用 PackageReference 時，所有組件的 `EmbedInteropTypes` 中繼資料一律為 false，因此目標檔案會明確新增此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="85a7e-295">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="85a7e-296">若要避免衝突，目標名稱應該是唯一的；在理想狀況下，使用套件名稱和所內嵌組件的組合，並將下列範例中的 `{InteropAssemblyName}` 取代為該值 </span><span class="sxs-lookup"><span data-stu-id="85a7e-296">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="85a7e-297">(如需範例，請參閱 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop))。</span><span class="sxs-lookup"><span data-stu-id="85a7e-297">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="85a7e-298">請注意，使用 `packages.config` 管理格式時，新增套件中組件的參考會讓 NuGet 和 Visual Studio 檢查 COM Interop 組件，並將專案檔中的 `EmbedInteropTypes` 設定為 true。</span><span class="sxs-lookup"><span data-stu-id="85a7e-298">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="85a7e-299">在此情況下，會覆寫目標。</span><span class="sxs-lookup"><span data-stu-id="85a7e-299">In this case the targets are overriden.</span></span>

<span data-ttu-id="85a7e-300">此外，根據預設，[組建資產不會轉移流動](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-300">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="85a7e-301">如這裡所述而撰寫的套件從專案對專案參考提取為可轉移相依性時，即會以不同的方式運作。</span><span class="sxs-lookup"><span data-stu-id="85a7e-301">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="85a7e-302">套件取用者允許它們流動的方式，是將 PrivateAssets 預設值修改為不包含組建。</span><span class="sxs-lookup"><span data-stu-id="85a7e-302">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="85a7e-303">執行 nuget pack 以產生 .nupkg 檔案</span><span class="sxs-lookup"><span data-stu-id="85a7e-303">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="85a7e-304">使用組件或以慣例為基礎的工作目錄時，搭配執行 `nuget pack` 與 `.nuspec` 檔案，並將 `<project-name>` 取代為特定檔案名稱，以建立套件：</span><span class="sxs-lookup"><span data-stu-id="85a7e-304">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="85a7e-305">使用 Visual Studio 專案時，請搭配執行 `nuget pack` 與專案檔，這樣會自動載入專案的 `.nuspec` 檔案，並使用專案檔中的值來取代其內的任何權杖：</span><span class="sxs-lookup"><span data-stu-id="85a7e-305">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="85a7e-306">因為專案是權杖值的來源，所以需要直接使用專案檔來進行權杖取代。</span><span class="sxs-lookup"><span data-stu-id="85a7e-306">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="85a7e-307">如果您搭配使用 `nuget pack` 與 `.nuspec` 檔案，則不會進行權杖取代。</span><span class="sxs-lookup"><span data-stu-id="85a7e-307">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="85a7e-308">在所有情況下，`nuget pack` 都會排除開頭為句點的資料夾；例如 `.git` 或 `.hg`。</span><span class="sxs-lookup"><span data-stu-id="85a7e-308">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="85a7e-309">NuGet 指出 `.nuspec` 檔案中是否有任何需要修正的錯誤；例如，忘記變更資訊清單中的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="85a7e-309">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="85a7e-310">`nuget pack` 成功之後，您會有可發行至適合資源庫的 `.nupkg` 檔案，如[發行套件](../create-packages/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="85a7e-310">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="85a7e-311">套件在建立後對其檢查的有用方式是在[套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)工具中開啟它。</span><span class="sxs-lookup"><span data-stu-id="85a7e-311">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="85a7e-312">這可提供套件內容和其資訊清單的圖形化檢視。</span><span class="sxs-lookup"><span data-stu-id="85a7e-312">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="85a7e-313">您也可以將所產生的 `.nupkg` 檔案重新命名為 `.zip` 檔案，並直接探索其內容。</span><span class="sxs-lookup"><span data-stu-id="85a7e-313">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="85a7e-314">其他選項</span><span class="sxs-lookup"><span data-stu-id="85a7e-314">Additional options</span></span>

<span data-ttu-id="85a7e-315">您可以搭配使用各種命令列參數與 `nuget pack` 來排除檔案、覆寫資訊清單中的版本號碼、變更輸出資料夾，以及其他功能。</span><span class="sxs-lookup"><span data-stu-id="85a7e-315">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="85a7e-316">如需完整清單，請參閱 [pack 命令參考](../tools/cli-ref-pack.md)。</span><span class="sxs-lookup"><span data-stu-id="85a7e-316">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="85a7e-317">下列選項是 Visual Studio 專案通用的幾個選項：</span><span class="sxs-lookup"><span data-stu-id="85a7e-317">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="85a7e-318">**參考的專案**：如果專案參考其他專案，則您可以使用 `-IncludeReferencedProjects` 選項，將參考的專案新增為套件的一部分或相依性：</span><span class="sxs-lookup"><span data-stu-id="85a7e-318">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="85a7e-319">這個包含程序是遞迴式，因此，如果 `MyProject.csproj` 參考專案 B 和 C，然後這些專案參考 D、E 和 F，則套件中會包含 B、C、D、E 和 F 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-319">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="85a7e-320">如果參考的專案包含專屬 `.nuspec` 檔案，則 NuGet 會改為將該參考的專案新增為相依性。</span><span class="sxs-lookup"><span data-stu-id="85a7e-320">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="85a7e-321">您需要個別封裝和發行該專案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-321">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="85a7e-322">**組建組態**：NuGet 預設會使用專案檔中所設定的預設組建組態，通常是「偵錯」。</span><span class="sxs-lookup"><span data-stu-id="85a7e-322">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="85a7e-323">若要從不同組建組態來封裝檔案 (例如「發行」)，請搭配使用 `-properties` 選項與下列組態：</span><span class="sxs-lookup"><span data-stu-id="85a7e-323">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="85a7e-324">**符號**：若要包含可讓取用者在偵錯工具中逐步執行您套件程式碼的符號，請使用 `-Symbols` 選項：</span><span class="sxs-lookup"><span data-stu-id="85a7e-324">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="85a7e-325">測試套件安裝</span><span class="sxs-lookup"><span data-stu-id="85a7e-325">Testing package installation</span></span>

<span data-ttu-id="85a7e-326">發行套件之前，您通常會想要測試將套件安裝至專案的程序。</span><span class="sxs-lookup"><span data-stu-id="85a7e-326">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="85a7e-327">測試可確定必要檔案最後都在專案的正確位置。</span><span class="sxs-lookup"><span data-stu-id="85a7e-327">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="85a7e-328">您可以使用一般[套件安裝步驟](../consume-packages/ways-to-install-a-package.md)，以在 Visual Studio 中或命令列上手動測試安裝。</span><span class="sxs-lookup"><span data-stu-id="85a7e-328">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="85a7e-329">自動化測試的基本程序如下：</span><span class="sxs-lookup"><span data-stu-id="85a7e-329">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="85a7e-330">將 `.nupkg` 檔案複製至本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="85a7e-330">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="85a7e-331">使用 `nuget sources add -name <name> -source <path>` 命令，將資料夾新增至套件來源 (請參閱 [nuget sources](../tools/cli-ref-sources.md))。</span><span class="sxs-lookup"><span data-stu-id="85a7e-331">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="85a7e-332">請注意，您只需要在任何指定電腦上設定此本機來源一次。</span><span class="sxs-lookup"><span data-stu-id="85a7e-332">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="85a7e-333">使用 `nuget install <packageID> -source <name>` 以從該來源安裝套件，其中 `<name>` 符合您指定至 `nuget sources` 的來源名稱。</span><span class="sxs-lookup"><span data-stu-id="85a7e-333">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="85a7e-334">指定來源可確保單獨從該來源安裝套件。</span><span class="sxs-lookup"><span data-stu-id="85a7e-334">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="85a7e-335">檢查您的檔案系統，確認已正確安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="85a7e-335">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85a7e-336">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85a7e-336">Next Steps</span></span>

<span data-ttu-id="85a7e-337">建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../create-packages/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="85a7e-337">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="85a7e-338">您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：</span><span class="sxs-lookup"><span data-stu-id="85a7e-338">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="85a7e-339">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="85a7e-339">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="85a7e-340">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="85a7e-340">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="85a7e-341">原始程式檔和組態檔的轉換</span><span class="sxs-lookup"><span data-stu-id="85a7e-341">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="85a7e-342">當地語系化</span><span class="sxs-lookup"><span data-stu-id="85a7e-342">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="85a7e-343">發行前版本</span><span class="sxs-lookup"><span data-stu-id="85a7e-343">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="85a7e-344">最後，請注意其他套件類型：</span><span class="sxs-lookup"><span data-stu-id="85a7e-344">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="85a7e-345">原生套件</span><span class="sxs-lookup"><span data-stu-id="85a7e-345">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="85a7e-346">符號套件</span><span class="sxs-lookup"><span data-stu-id="85a7e-346">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
