---
title: 使用 nuget.exe CLI 建立 NuGet 套件
description: 設計和建立 NuGet 套件的詳細指南，包括檔案和版本控制。
author: JonDouglas
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ebaa14325e477c7d864f5c5e88d99f467194e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774712"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="76d57-103">使用 nuget.exe CLI 建立套件</span><span class="sxs-lookup"><span data-stu-id="76d57-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="76d57-104">不論套件的功能或所含程式碼為何，您都可以使用其中一個 CLI 工具 (`nuget.exe` 或 `dotnet.exe`) 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。</span><span class="sxs-lookup"><span data-stu-id="76d57-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="76d57-105">若要安裝 NuGet CLI 工具，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="76d57-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="76d57-106">請注意，Visual Studio 不會自動包含 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="76d57-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="76d57-107">針對非 SDK 樣式的專案 (通常是 .NET Framework 專案)，請依照此文章中所述的步驟建立套件。</span><span class="sxs-lookup"><span data-stu-id="76d57-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="76d57-108">如需使用 Visual Studio 與 `nuget.exe` CLI 的逐步指示，請參閱[建立及發佈 .NET Framework 套件](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="76d57-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="76d57-109">針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，請參閱[使用 dotnet CLI 建立 NuGet 套件](creating-a-package-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="76d57-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="76d57-110">針對從 `packages.config` 移轉至 [PackageReference](../consume-packages/package-references-in-project-files.md) 的專案，請使用 [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)。</span><span class="sxs-lookup"><span data-stu-id="76d57-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="76d57-111">技術上而言，NuGet 套件就只是已重新命名為 `.nupkg` 副檔名且其內容符合特定慣例的 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="76d57-112">本主題描述如何建立符合這些慣例之套件的詳細程序。</span><span class="sxs-lookup"><span data-stu-id="76d57-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="76d57-113">封裝開始於已編譯的程式碼 (組件)、符號 (和) 您想要以套件形式傳遞的其他檔案 (請參閱[概觀和工作流程](overview-and-workflow.md))。</span><span class="sxs-lookup"><span data-stu-id="76d57-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="76d57-114">此流程與編譯或產生進入套件的檔案無關，但您可以擷取專案檔中的資訊保持已編譯的組件與套件同步。</span><span class="sxs-lookup"><span data-stu-id="76d57-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="76d57-115">此主題適用於非 SDK 樣式的專案，通常是使用 Visual Studio 2017 及更新版本與 NuGet 4.0+ 的 .NET Core 與 .NET Standard 專案以外的專案。</span><span class="sxs-lookup"><span data-stu-id="76d57-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="76d57-116">決定要封裝的組件</span><span class="sxs-lookup"><span data-stu-id="76d57-116">Decide which assemblies to package</span></span>

<span data-ttu-id="76d57-117">大部分的一般用途套件都會包含其他開發人員可以在其專屬專案中使用的一或多個組件。</span><span class="sxs-lookup"><span data-stu-id="76d57-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="76d57-118">一般而言，最好一個 NuGet 套件一個組件，前提是每個組件都可以獨立使用。</span><span class="sxs-lookup"><span data-stu-id="76d57-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="76d57-119">例如，如果您有與 `Parser.dll` 相依的 `Utilities.dll`，而且 `Parser.dll` 可以單獨使用，則會為每個項目建立一個套件。</span><span class="sxs-lookup"><span data-stu-id="76d57-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="76d57-120">這樣做可讓開發人員單獨使用 `Parser.dll` 和 `Utilities.dll`。</span><span class="sxs-lookup"><span data-stu-id="76d57-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="76d57-121">如果您的程式庫包含多個無法單獨使用的組件，則最好將它們結合成單一套件。</span><span class="sxs-lookup"><span data-stu-id="76d57-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="76d57-122">使用上述範例時，如果 `Parser.dll` 所包含的程式碼僅供 `Utilities.dll` 使用，則最好將 `Parser.dll` 放在相同的套件中。</span><span class="sxs-lookup"><span data-stu-id="76d57-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="76d57-123">同樣地，如果 `Utilities.dll` 與 `Utilities.resources.dll` 相依 (再提醒一次，後者無法單獨使用)，則請將這兩個放在相同的套件中。</span><span class="sxs-lookup"><span data-stu-id="76d57-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="76d57-124">資源其實是特殊案例。</span><span class="sxs-lookup"><span data-stu-id="76d57-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="76d57-125">將套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，但「排除」名為 `.resources.dll` 的參考，因為它們假設為當地語系化附屬組件 (請參閱[建立當地語系化套件](creating-localized-packages.md))。</span><span class="sxs-lookup"><span data-stu-id="76d57-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="76d57-126">因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="76d57-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="76d57-127">如果您的程式庫包含 COM Interop 組件，請遵循[建立包含 COM Interop 組件的套件](author-packages-with-com-interop-assemblies.md)中的其他指導方針。</span><span class="sxs-lookup"><span data-stu-id="76d57-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="76d57-128">.nuspec 檔案的角色和結構</span><span class="sxs-lookup"><span data-stu-id="76d57-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="76d57-129">知道您想要封裝的檔案之後，下個步驟就是在 `.nuspec` XML 檔案中建立套件資訊清單。</span><span class="sxs-lookup"><span data-stu-id="76d57-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="76d57-130">資訊清單：</span><span class="sxs-lookup"><span data-stu-id="76d57-130">The manifest:</span></span>

1. <span data-ttu-id="76d57-131">描述套件內容而且本身包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="76d57-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="76d57-132">驅使建立套件並指示 NuGet 如何將套件安裝至專案。</span><span class="sxs-lookup"><span data-stu-id="76d57-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="76d57-133">例如，資訊清單會識別其他套件相依性；因此，安裝主要套件時，NuGet 也可以安裝這些相依性。</span><span class="sxs-lookup"><span data-stu-id="76d57-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="76d57-134">包含必要和選擇性屬性，如下所述。</span><span class="sxs-lookup"><span data-stu-id="76d57-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="76d57-135">如需確切詳細資料 (包含這裡未提及的其他屬性)，請參閱 [.nuspec 參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="76d57-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="76d57-136">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="76d57-136">Required properties:</span></span>

- <span data-ttu-id="76d57-137">套件識別碼，其在裝載套件的資源庫內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="76d57-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="76d57-138">*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別 [發行前版本](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="76d57-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="76d57-139">主機上應該會出現套件標題 (例如 nuget.org)</span><span class="sxs-lookup"><span data-stu-id="76d57-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="76d57-140">作者和擁有者資訊。</span><span class="sxs-lookup"><span data-stu-id="76d57-140">Author and owner information.</span></span>
- <span data-ttu-id="76d57-141">套件的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="76d57-141">A long description of the package.</span></span>

<span data-ttu-id="76d57-142">常見的選擇性屬性：</span><span class="sxs-lookup"><span data-stu-id="76d57-142">Common optional properties:</span></span>

- <span data-ttu-id="76d57-143">版本資訊</span><span class="sxs-lookup"><span data-stu-id="76d57-143">Release notes</span></span>
- <span data-ttu-id="76d57-144">著作權資訊</span><span class="sxs-lookup"><span data-stu-id="76d57-144">Copyright information</span></span>
- <span data-ttu-id="76d57-145">[Visual Studio 中的套件管理員 UI](../consume-packages/install-use-packages-visual-studio.md) 的簡短描述</span><span class="sxs-lookup"><span data-stu-id="76d57-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="76d57-146">地區設定識別碼</span><span class="sxs-lookup"><span data-stu-id="76d57-146">A locale ID</span></span>
- <span data-ttu-id="76d57-147">專案 URL</span><span class="sxs-lookup"><span data-stu-id="76d57-147">Project URL</span></span>
- <span data-ttu-id="76d57-148">授權為運算式或檔案 (`licenseUrl` 已被取代，請改用[ `license` nuspec 中繼資料元素](../reference/nuspec.md#license)) </span><span class="sxs-lookup"><span data-stu-id="76d57-148">License as an expression or file (`licenseUrl` is deprecated, use [`license` nuspec metadata element](../reference/nuspec.md#license) instead)</span></span>
- <span data-ttu-id="76d57-149"> (的圖示檔 `iconUrl` 已被取代，請改用[ `icon` nuspec 中繼資料元素](../reference/nuspec.md#icon)) </span><span class="sxs-lookup"><span data-stu-id="76d57-149">An icon file (`iconUrl` is deprecated use [`icon` nuspec metadata element](../reference/nuspec.md#icon) instead)</span></span>
- <span data-ttu-id="76d57-150">相依性和參考的清單</span><span class="sxs-lookup"><span data-stu-id="76d57-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="76d57-151">協助進行資源庫搜尋的標記</span><span class="sxs-lookup"><span data-stu-id="76d57-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="76d57-152">下列一般 (但虛構的) `.nuspec` 檔案具有可描述屬性的註解：</span><span class="sxs-lookup"><span data-stu-id="76d57-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

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
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

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
        <file src="icon.png" target="" />
    </files>
</package>
```

<span data-ttu-id="76d57-153">如需宣告相依性及指定版本號碼的詳細資料，請參閱 [packages.config](../reference/packages-config.md) 和[套件版本控制](../concepts/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="76d57-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="76d57-154">在 `dependency` 項目上使用 `include` 和 `exclude` 屬性，也可以將相依性中的資產直接用於套件中。</span><span class="sxs-lookup"><span data-stu-id="76d57-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="76d57-155">請參閱 [.nu-/spec 參考 - 相依性](../reference/nuspec.md#dependencies)。</span><span class="sxs-lookup"><span data-stu-id="76d57-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="76d57-156">因為資訊清單會包含在透過它所建立的套件中，所以檢查現有套件就可以找到任意數目的其他範例。</span><span class="sxs-lookup"><span data-stu-id="76d57-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="76d57-157">不錯的來源是您電腦上的 *global-packages* 資料夾，即下列命令所傳回的位置：</span><span class="sxs-lookup"><span data-stu-id="76d57-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="76d57-158">移至任何 *package\version* 資料夾，並將 `.nupkg` 檔案複製至 `.zip` 檔案，然後開啟該 `.zip` 檔案，並檢查其內的 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="76d57-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="76d57-159">從 Visual Studio 專案建立 `.nuspec` 時，資訊清單會包含建置套件時取代為專案中資訊的權杖。</span><span class="sxs-lookup"><span data-stu-id="76d57-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="76d57-160">請參閱[從 Visual Studio 專案建立 .nuspec](#from-a-visual-studio-project)。</span><span class="sxs-lookup"><span data-stu-id="76d57-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="76d57-161">建立 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-161">Create the .nuspec file</span></span>

<span data-ttu-id="76d57-162">建立完整資訊清單一般是從透過下列其中一種方法所產生的基本 `.nuspec` 檔案開始：</span><span class="sxs-lookup"><span data-stu-id="76d57-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="76d57-163">以慣例為基礎的工作目錄</span><span class="sxs-lookup"><span data-stu-id="76d57-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="76d57-164">組件 DLL</span><span class="sxs-lookup"><span data-stu-id="76d57-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="76d57-165">Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="76d57-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="76d57-166">含預設值的新檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="76d57-167">您接著手動編輯檔案，讓它描述您在最終套件中想要的確切內容。</span><span class="sxs-lookup"><span data-stu-id="76d57-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="76d57-168">產生的 `.nuspec` 檔案會包含在使用 `nuget pack` 命令建立套件之前必須修改的預留位置。</span><span class="sxs-lookup"><span data-stu-id="76d57-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="76d57-169">如果 `.nuspec` 包含任何預留位置，則該命令會失敗。</span><span class="sxs-lookup"><span data-stu-id="76d57-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="76d57-170">從以慣例為基礎的工作目錄</span><span class="sxs-lookup"><span data-stu-id="76d57-170">From a convention-based working directory</span></span>

<span data-ttu-id="76d57-171">因為 NuGet 套件只是使用 `.nupkg` 副檔名重新命名的 ZIP 檔案，所以通常很容易即可在本機檔系統上，建立所需的資料夾結構，然後直接從該結構建立 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="76d57-172">`nuget pack` 命令接著會自動在該資料夾結構中新增所有檔案 (不包含任何以 `.` 開頭的資料夾，供您以相同的結構保留私人檔案)。</span><span class="sxs-lookup"><span data-stu-id="76d57-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="76d57-173">這種方法的優點是您不需要在資訊清單中指定想要包含在套件中的檔案 (如本主題中稍後所述)。</span><span class="sxs-lookup"><span data-stu-id="76d57-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="76d57-174">您可以只讓建置程序產生套件中完全相同的資料夾結構，而且可以輕鬆地包含可能不屬於專案的其他檔案：</span><span class="sxs-lookup"><span data-stu-id="76d57-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="76d57-175">應該插入至目標專案的內容和原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="76d57-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="76d57-176">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="76d57-176">PowerShell scripts</span></span>
- <span data-ttu-id="76d57-177">專案中現有組態檔和原始程式碼檔案的轉換。</span><span class="sxs-lookup"><span data-stu-id="76d57-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="76d57-178">資料夾慣例如下：</span><span class="sxs-lookup"><span data-stu-id="76d57-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="76d57-179">資料夾</span><span class="sxs-lookup"><span data-stu-id="76d57-179">Folder</span></span> | <span data-ttu-id="76d57-180">描述</span><span class="sxs-lookup"><span data-stu-id="76d57-180">Description</span></span> | <span data-ttu-id="76d57-181">套件安裝時的動作</span><span class="sxs-lookup"><span data-stu-id="76d57-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76d57-182">(root)</span><span class="sxs-lookup"><span data-stu-id="76d57-182">(root)</span></span> | <span data-ttu-id="76d57-183">readme.txt 的位置</span><span class="sxs-lookup"><span data-stu-id="76d57-183">Location for readme.txt</span></span> | <span data-ttu-id="76d57-184">安裝套件時，Visual Studio 會顯示套件根目錄中的 readme.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="76d57-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="76d57-185">lib/{tfm}</span></span> | <span data-ttu-id="76d57-186">所指定目標架構 Moniker (TFM) 的組件 (`.dll`)、文件 (`.xml`) 和符號 (`.pdb`) 檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="76d57-187">組件會新增為編譯與執行階段的參考；`.xml` 與 `.pdb` 則會複製到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="76d57-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="76d57-188">請參閱[支援多個目標架構](supporting-multiple-target-frameworks.md)，以了解如何建立架構目標特定子資料夾。</span><span class="sxs-lookup"><span data-stu-id="76d57-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="76d57-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="76d57-189">ref/{tfm}</span></span> | <span data-ttu-id="76d57-190">所指定目標 Framework Moniker (TFM) 的組件 (`.dll`) 與符號 (`.pdb`) 檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="76d57-191">組件只會針對編譯階段新增為參考；因此不會有任何項目被複製到專案 bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="76d57-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="76d57-192">runtimes</span><span class="sxs-lookup"><span data-stu-id="76d57-192">runtimes</span></span> | <span data-ttu-id="76d57-193">架構特定組件 (`.dll`)、符號 (`.pdb`) 和原生資源 (`.pri`) 檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="76d57-194">組件只會針對執行階段新增為參考；其他檔案則會複製至專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="76d57-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="76d57-195">`/ref/{tfm}` 資料夾下一律必須有對應的 (TFM) `AnyCPU` 特定組件，才能提供對應的編譯階段組件。</span><span class="sxs-lookup"><span data-stu-id="76d57-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="76d57-196">請參閱[支援多個目標架構](supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="76d57-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="76d57-197">內容</span><span class="sxs-lookup"><span data-stu-id="76d57-197">content</span></span> | <span data-ttu-id="76d57-198">任意檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-198">Arbitrary files</span></span> | <span data-ttu-id="76d57-199">內容會複製至專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="76d57-199">Contents are copied to the project root.</span></span> <span data-ttu-id="76d57-200">請將 **content** 資料夾視為最後使用套件的目標應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="76d57-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="76d57-201">若要讓套件在應用程式的 */images* 資料夾中新增映像，請將它放在套件的 *content/images* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="76d57-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="76d57-202">build</span><span class="sxs-lookup"><span data-stu-id="76d57-202">build</span></span> | <span data-ttu-id="76d57-203">*(3.x+)* MSBuild `.targets` 與 `.props` 檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="76d57-204">自動插入到專案中。</span><span class="sxs-lookup"><span data-stu-id="76d57-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="76d57-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="76d57-205">buildMultiTargeting</span></span> | <span data-ttu-id="76d57-206">用於跨架構目標的 *(4.0+)* MSBuild `.targets` 與 `.props` 檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="76d57-207">自動插入到專案中。</span><span class="sxs-lookup"><span data-stu-id="76d57-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="76d57-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="76d57-208">buildTransitive</span></span> | <span data-ttu-id="76d57-209">*(5.0+)* 可傳遞至任何取用專案的 MSBuild `.targets` 與 `.props` 檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="76d57-210">請參閱[功能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)頁面 \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="76d57-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="76d57-211">自動插入到專案中。</span><span class="sxs-lookup"><span data-stu-id="76d57-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="76d57-212">tools</span><span class="sxs-lookup"><span data-stu-id="76d57-212">tools</span></span> | <span data-ttu-id="76d57-213">可從套件管理員主控台存取的 Powershell 指令碼和程式</span><span class="sxs-lookup"><span data-stu-id="76d57-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="76d57-214">`tools` 資料夾只會新增至套件管理員主控台的 `PATH` 環境變數 (具體而言，建置專案時 *「不」* 會新增至針對 MSBuild 所設定的 `PATH`)。</span><span class="sxs-lookup"><span data-stu-id="76d57-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="76d57-215">因為您的資料夾結構可包含任意數目之目標架構的任意數目組件，所以建立可支援多重架構的套件時，需要使用此種方法。</span><span class="sxs-lookup"><span data-stu-id="76d57-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="76d57-216">在任何情況下，您擁有所要的資料夾結構之後，請在該資料夾中執行下列命令來建立 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="76d57-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="76d57-217">同樣地，產生的 `.nuspec` 不會包含資料夾結構中檔案的明確參考。</span><span class="sxs-lookup"><span data-stu-id="76d57-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="76d57-218">建立套件時，NuGet 會自動包含所有檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="76d57-219">不過，您仍然需要編輯資訊清單之其他部分中的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="76d57-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="76d57-220">從組件 DLL</span><span class="sxs-lookup"><span data-stu-id="76d57-220">From an assembly DLL</span></span>

<span data-ttu-id="76d57-221">在從組件建立套件的簡單案例中，您可以使用下列命令，透過組件的中繼資料產生 `.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="76d57-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="76d57-222">使用這種形式會將資訊清單中的少數預留位置取代為組件中的特定值。</span><span class="sxs-lookup"><span data-stu-id="76d57-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="76d57-223">例如，`<id>` 屬性設定為組件名稱，而且 `<version>` 設定為組件版本。</span><span class="sxs-lookup"><span data-stu-id="76d57-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="76d57-224">不過，資訊清單中的其他屬性在組件中沒有相符值，因此仍然會包含預留位置。</span><span class="sxs-lookup"><span data-stu-id="76d57-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="76d57-225">從 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="76d57-225">From a Visual Studio project</span></span>

<span data-ttu-id="76d57-226">從 `.csproj` 或 `.vbproj` 檔案建立 `.nuspec` 十分方便，因為已安裝至這些專案的其他套件會自動參照為相依性。</span><span class="sxs-lookup"><span data-stu-id="76d57-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="76d57-227">只需要在與專案檔相同的資料夾中使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="76d57-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="76d57-228">產生的 `<project-name>.nuspec` 檔案包含「權杖」，而權杖會在封裝時取代為專案中的值，包含已安裝之任何其他套件的參考。</span><span class="sxs-lookup"><span data-stu-id="76d57-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="76d57-229">如果您有要包含在 *.nuspec* 中的套件相依性，請改為使用 `nuget pack` 並從產生的 *.nupkg* 檔案內取得 *.nuspec* 檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="76d57-230">例如，使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="76d57-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="76d57-231">在專案屬性的兩側，使用 `$` 符號分隔權杖。</span><span class="sxs-lookup"><span data-stu-id="76d57-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="76d57-232">例如，透過此方式產生之資訊清單中的 `<id>` 值一般會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="76d57-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="76d57-233">在封裝時間，會將此權杖取代為專案檔中的 `AssemblyName` 值。</span><span class="sxs-lookup"><span data-stu-id="76d57-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="76d57-234">若要將專案值完全對應至 `.nuspec` 權杖，請參閱[取代權杖參考](../reference/nuspec.md#replacement-tokens)。</span><span class="sxs-lookup"><span data-stu-id="76d57-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="76d57-235">更新專案時，權杖可讓您不需要更新 `.nuspec` 中這類版本號碼的重要值 </span><span class="sxs-lookup"><span data-stu-id="76d57-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="76d57-236">(如有需要，您一律可以將權杖取代為常值)。</span><span class="sxs-lookup"><span data-stu-id="76d57-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="76d57-237">請注意，從 Visual Studio 專案工作時，有數個其他封裝選項可用，如後面的[執行 nuget pack 以產生 .nupkg 檔案](#run-nuget-pack-to-generate-the-nupkg-file)所述。</span><span class="sxs-lookup"><span data-stu-id="76d57-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="76d57-238">方案層級套件</span><span class="sxs-lookup"><span data-stu-id="76d57-238">Solution-level packages</span></span>

<span data-ttu-id="76d57-239">*僅限 NuGet 2.x。無法在 NuGet 3.0 + 中使用。*</span><span class="sxs-lookup"><span data-stu-id="76d57-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="76d57-240">NuGet 2.x 支援可安裝套件管理員主控台工具或其他命令的方案層級套件概念 (`tools` 資料夾內容)，但不會將參考、內容或組建自訂新增至方案中的任何專案。</span><span class="sxs-lookup"><span data-stu-id="76d57-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="76d57-241">這類套件在其直接 `lib`、`content` 或 `build` 資料夾中未包含任何檔案，而其相依性在各自的 `lib`、`content` 或 `build` 資料夾中沒有檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="76d57-242">NuGet 會追蹤 `.nuget` 資料夾的 `packages.config` 檔案中的已安裝方案層級套件，而不是專案的 `packages.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="76d57-243">含預設值的新檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-243">New file with default values</span></span>

<span data-ttu-id="76d57-244">下列命令會建立含預留位置的預設資訊清單，確保您是從正確的檔案結構開始：</span><span class="sxs-lookup"><span data-stu-id="76d57-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="76d57-245">如果您省略 \<package-name\> ，則產生的檔案 `Package.nuspec` 為。</span><span class="sxs-lookup"><span data-stu-id="76d57-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="76d57-246">如果您提供 `Contoso.Utility.UsefulStuff` 這類名稱，則檔案是 `Contoso.Utility.UsefulStuff.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="76d57-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="76d57-247">產生的 `.nuspec` 包含 `projectUrl` 這類值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="76d57-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="76d57-248">請務必先編輯檔案，再用它來建立最終 `.nupkg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="76d57-249">選擇唯一的套件識別碼並設定版本號碼</span><span class="sxs-lookup"><span data-stu-id="76d57-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="76d57-250">套件識別碼 (`<id>` 項目) 和版本號碼 (`<version>` 項目) 是資訊清單中的兩個最重要值，因為它們可以唯一識別套件中所含的確切程式碼。</span><span class="sxs-lookup"><span data-stu-id="76d57-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="76d57-251">**套件識別碼的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="76d57-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="76d57-252">**唯一性**：在 nuget.org 內，或只要資源庫裝載套件時，識別碼就必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="76d57-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="76d57-253">決定識別碼之前，請搜尋適用的資源庫，檢查是否已在使用名稱。</span><span class="sxs-lookup"><span data-stu-id="76d57-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="76d57-254">若要避免衝突，不錯的模式是使用您的公司名稱作為識別碼的第一個部分，例如 `Contoso.`。</span><span class="sxs-lookup"><span data-stu-id="76d57-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="76d57-255">**命名空間類似名稱**：遵循與 .NET 中命名空間類似的模式，即使用點標記法，而非連字號。</span><span class="sxs-lookup"><span data-stu-id="76d57-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="76d57-256">例如，使用 `Contoso.Utility.UsefulStuff`，而非 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。</span><span class="sxs-lookup"><span data-stu-id="76d57-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="76d57-257">套件識別碼符合程式碼中所使用的命名空間時，取用者也會發現它十分有用。</span><span class="sxs-lookup"><span data-stu-id="76d57-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="76d57-258">**範例套件**：如果您產生的範例程式碼套件示範如何使用另一個套件，請將 `.Sample` 附加為識別碼的尾碼，如 `Contoso.Utility.UsefulStuff.Sample` 所示 </span><span class="sxs-lookup"><span data-stu-id="76d57-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="76d57-259"> (範例套件當然會相依于另一個套件。建立範例套件時，請 ) 使用稍早所述的慣例型工作目錄方法。</span><span class="sxs-lookup"><span data-stu-id="76d57-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="76d57-260">在 `content` 資料夾中，於稱為 `\Samples\<identifier>` 的資料夾中排列範例程式碼，而這與 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相同。</span><span class="sxs-lookup"><span data-stu-id="76d57-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="76d57-261">**套件版本的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="76d57-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="76d57-262">一般而言，請設定套件版本，使其符合程式庫，但這不是絕對必要。</span><span class="sxs-lookup"><span data-stu-id="76d57-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="76d57-263">將套件限制為單一組件時，這相當簡單，如[決定要封裝的組件](#decide-which-assemblies-to-package)稍早所述。</span><span class="sxs-lookup"><span data-stu-id="76d57-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="76d57-264">整體來說，請記住，解析相依性時，NuGet 本身會處理套件版本，而非組件版本。</span><span class="sxs-lookup"><span data-stu-id="76d57-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="76d57-265">使用非標準版本方式時，請務必考慮使用 NuGet 版本控制規則，如[套件版本控制](../concepts/package-versioning.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="76d57-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="76d57-266">下面一系列的簡短部落格文章也有助於了解版本控制：</span><span class="sxs-lookup"><span data-stu-id="76d57-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="76d57-267">第 1 部分：接受 DLL 挑戰</span><span class="sxs-lookup"><span data-stu-id="76d57-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="76d57-268">第 2 部分：核心演算法</span><span class="sxs-lookup"><span data-stu-id="76d57-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="76d57-269">第 3 部分：透過繫結重新導向的統一</span><span class="sxs-lookup"><span data-stu-id="76d57-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="76d57-270">新增讀我檔案和其他檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-270">Add a readme and other files</span></span>

<span data-ttu-id="76d57-271">若要直接指定要包含在套件中的檔案，請在 `.nuspec` 檔案中使用 `<files>` 節點，而這在 `<metadata>` 標記「後面」：</span><span class="sxs-lookup"><span data-stu-id="76d57-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> <span data-ttu-id="76d57-272">使用以慣例為基礎的工作目錄方法時，您可以將 readme.txt 放在套件根目錄中，而將其他內容放在 `content` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="76d57-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="76d57-273">資訊清單中不需要任何 `<file>` 項目。</span><span class="sxs-lookup"><span data-stu-id="76d57-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="76d57-274">當您在套件根目錄中包含名為 `readme.txt` 的檔案時，Visual Studio 會在直接安裝套件之後立即以純文字形式顯示該檔案的內容 </span><span class="sxs-lookup"><span data-stu-id="76d57-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="76d57-275">(不會針對安裝為相依性的套件顯示讀我檔案)。</span><span class="sxs-lookup"><span data-stu-id="76d57-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="76d57-276">例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：</span><span class="sxs-lookup"><span data-stu-id="76d57-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安裝時 NuGet 套件的讀我檔案顯示](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="76d57-278">如果您在 `.nuspec` 檔案中包含空 `<files>` 節點，則 NuGet 不會包含不在 `lib` 資料夾套件中的任何其他內容。</span><span class="sxs-lookup"><span data-stu-id="76d57-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="76d57-279">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="76d57-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="76d57-280">在某些情況下，您可能想要在取用您套件的專案中新增自訂組建目標或屬性，例如在建置期間執行自訂工具或程序。</span><span class="sxs-lookup"><span data-stu-id="76d57-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="76d57-281">做法是在專案的 `\build` 資料夾內以 `<package_id>.targets` 或 `<package_id>.props` 形式放置檔案 (例如 `Contoso.Utility.UsefulStuff.targets`)。</span><span class="sxs-lookup"><span data-stu-id="76d57-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="76d57-282">根 `\build` 資料夾中的檔案視為適合所有目標架構。</span><span class="sxs-lookup"><span data-stu-id="76d57-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="76d57-283">若要提供架構專屬的檔案，請先將其置於適當的子資料夾中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="76d57-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

<span data-ttu-id="76d57-284">接著，在 `.nuspec` 檔案中，請務必於 `<files>` 節點中參照這些檔案：</span><span class="sxs-lookup"><span data-stu-id="76d57-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="76d57-285">[NuGet 2.5 引進了](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)在套件中包含 MSBuild pros 和 targets 的做法，因此建議您將 `minClientVersion="2.5"` 屬性新增到 `metadata` 元素，以指出使用套件所需的最低 NuGet 用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="76d57-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="76d57-286">當 NuGet 安裝含有 `\build` 檔案的套件時，會在指向 `.targets` 和 `.props` 檔案的專案檔中新增 MSBuild `<Import>` 項目。</span><span class="sxs-lookup"><span data-stu-id="76d57-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="76d57-287"> (`.props` 會新增至專案檔頂端， `.targets` 並新增至底部。 ) 為 `<Import>` 每個目標 framework 新增個別的條件式 MSBuild 元素。</span><span class="sxs-lookup"><span data-stu-id="76d57-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="76d57-288">用於跨框架目標的 MSBuild `.props` 和 `.targets` 檔案可以放在 `\buildMultiTargeting` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="76d57-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="76d57-289">在套件安裝期間，NuGet 會將對應的 `<Import>` 元素新增到有條件的專案檔中，即未設定目標框架 (MSBuild 屬性 `$(TargetFramework)` 必須是空的)。</span><span class="sxs-lookup"><span data-stu-id="76d57-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="76d57-290">使用 NuGet 3.x 時，目標不會新增至專案，但會透過 `{projectName}.nuget.g.targets` 與 `{projectName}.nuget.g.props` 提供。</span><span class="sxs-lookup"><span data-stu-id="76d57-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="76d57-291">執行 nuget pack 以產生 .nupkg 檔案</span><span class="sxs-lookup"><span data-stu-id="76d57-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="76d57-292">使用組件或以慣例為基礎的工作目錄時，搭配執行 `nuget pack` 與 `.nuspec` 檔案，並將 `<project-name>` 取代為特定檔案名稱，以建立套件：</span><span class="sxs-lookup"><span data-stu-id="76d57-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="76d57-293">使用 Visual Studio 專案時，請搭配執行 `nuget pack` 與專案檔，這樣會自動載入專案的 `.nuspec` 檔案，並使用專案檔中的值來取代其內的任何權杖：</span><span class="sxs-lookup"><span data-stu-id="76d57-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="76d57-294">因為專案是權杖值的來源，所以需要直接使用專案檔來進行權杖取代。</span><span class="sxs-lookup"><span data-stu-id="76d57-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="76d57-295">如果您搭配使用 `nuget pack` 與 `.nuspec` 檔案，則不會進行權杖取代。</span><span class="sxs-lookup"><span data-stu-id="76d57-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="76d57-296">在所有情況下，`nuget pack` 都會排除開頭為句點的資料夾；例如 `.git` 或 `.hg`。</span><span class="sxs-lookup"><span data-stu-id="76d57-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="76d57-297">NuGet 指出 `.nuspec` 檔案中是否有任何需要修正的錯誤；例如，忘記變更資訊清單中的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="76d57-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="76d57-298">`nuget pack` 成功之後，您會有可發行至適合資源庫的 `.nupkg` 檔案，如[發行套件](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="76d57-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="76d57-299">套件在建立後對其檢查的有用方式是在[套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)工具中開啟它。</span><span class="sxs-lookup"><span data-stu-id="76d57-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="76d57-300">這可提供套件內容和其資訊清單的圖形化檢視。</span><span class="sxs-lookup"><span data-stu-id="76d57-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="76d57-301">您也可以將所產生的 `.nupkg` 檔案重新命名為 `.zip` 檔案，並直接探索其內容。</span><span class="sxs-lookup"><span data-stu-id="76d57-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="76d57-302">其他選項</span><span class="sxs-lookup"><span data-stu-id="76d57-302">Additional options</span></span>

<span data-ttu-id="76d57-303">您可以搭配使用各種命令列參數與 `nuget pack` 來排除檔案、覆寫資訊清單中的版本號碼、變更輸出資料夾，以及其他功能。</span><span class="sxs-lookup"><span data-stu-id="76d57-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="76d57-304">如需完整清單，請參閱 [pack 命令參考](../reference/cli-reference/cli-ref-pack.md)。</span><span class="sxs-lookup"><span data-stu-id="76d57-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="76d57-305">下列選項是 Visual Studio 專案通用的幾個選項：</span><span class="sxs-lookup"><span data-stu-id="76d57-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="76d57-306">**參考的專案**：如果專案參考其他專案，則您可以使用 `-IncludeReferencedProjects` 選項，將參考的專案新增為套件的一部分或相依性：</span><span class="sxs-lookup"><span data-stu-id="76d57-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="76d57-307">這個包含程序是遞迴式，因此，如果 `MyProject.csproj` 參考專案 B 和 C，然後這些專案參考 D、E 和 F，則套件中會包含 B、C、D、E 和 F 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="76d57-308">如果參考的專案包含專屬 `.nuspec` 檔案，則 NuGet 會改為將該參考的專案新增為相依性。</span><span class="sxs-lookup"><span data-stu-id="76d57-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="76d57-309">您需要個別封裝和發行該專案。</span><span class="sxs-lookup"><span data-stu-id="76d57-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="76d57-310">**組建組態**：NuGet 預設會使用專案檔中所設定的預設組建組態，通常是「偵錯」。</span><span class="sxs-lookup"><span data-stu-id="76d57-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="76d57-311">若要從不同組建組態來封裝檔案 (例如「發行」)，請搭配使用 `-properties` 選項與下列組態：</span><span class="sxs-lookup"><span data-stu-id="76d57-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="76d57-312">**符號**：若要包含可讓取用者在偵錯工具中逐步執行您套件程式碼的符號，請使用 `-Symbols` 選項：</span><span class="sxs-lookup"><span data-stu-id="76d57-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="76d57-313">測試套件安裝</span><span class="sxs-lookup"><span data-stu-id="76d57-313">Test package installation</span></span>

<span data-ttu-id="76d57-314">發行套件之前，您通常會想要測試將套件安裝至專案的程序。</span><span class="sxs-lookup"><span data-stu-id="76d57-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="76d57-315">測試可確定必要檔案最後都在專案的正確位置。</span><span class="sxs-lookup"><span data-stu-id="76d57-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="76d57-316">您可以使用一般[套件安裝步驟](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)，以在 Visual Studio 中或命令列上手動測試安裝。</span><span class="sxs-lookup"><span data-stu-id="76d57-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="76d57-317">自動化測試的基本程序如下：</span><span class="sxs-lookup"><span data-stu-id="76d57-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="76d57-318">將 `.nupkg` 檔案複製至本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="76d57-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="76d57-319">使用 `nuget sources add -name <name> -source <path>` 命令，將資料夾新增至套件來源 (請參閱 [nuget sources](../reference/cli-reference/cli-ref-sources.md))。</span><span class="sxs-lookup"><span data-stu-id="76d57-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="76d57-320">請注意，您只需要在任何指定電腦上設定此本機來源一次。</span><span class="sxs-lookup"><span data-stu-id="76d57-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="76d57-321">使用 `nuget install <packageID> -source <name>` 以從該來源安裝套件，其中 `<name>` 符合您指定至 `nuget sources` 的來源名稱。</span><span class="sxs-lookup"><span data-stu-id="76d57-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="76d57-322">指定來源可確保單獨從該來源安裝套件。</span><span class="sxs-lookup"><span data-stu-id="76d57-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="76d57-323">檢查您的檔案系統，確認已正確安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="76d57-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76d57-324">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76d57-324">Next Steps</span></span>

<span data-ttu-id="76d57-325">建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="76d57-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="76d57-326">您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：</span><span class="sxs-lookup"><span data-stu-id="76d57-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="76d57-327">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="76d57-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="76d57-328">支援多個目標 Framework</span><span class="sxs-lookup"><span data-stu-id="76d57-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="76d57-329">原始程式檔和組態檔的轉換</span><span class="sxs-lookup"><span data-stu-id="76d57-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="76d57-330">當地語系化</span><span class="sxs-lookup"><span data-stu-id="76d57-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="76d57-331">發行前版本</span><span class="sxs-lookup"><span data-stu-id="76d57-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="76d57-332">設定套件類型</span><span class="sxs-lookup"><span data-stu-id="76d57-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="76d57-333">建立包含 COM Interop 組件的套件</span><span class="sxs-lookup"><span data-stu-id="76d57-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="76d57-334">最後，請注意其他套件類型：</span><span class="sxs-lookup"><span data-stu-id="76d57-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="76d57-335">原生封裝</span><span class="sxs-lookup"><span data-stu-id="76d57-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="76d57-336">符號套件</span><span class="sxs-lookup"><span data-stu-id="76d57-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
