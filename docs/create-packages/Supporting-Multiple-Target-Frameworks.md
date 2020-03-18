---
title: NuGet 套件的多目標
description: 將目標設為單一 NuGet 套件內多個 .NET Framework 版本之各種方法的描述。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429007"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="5a23b-103">支援多個 .NET 版本</span><span class="sxs-lookup"><span data-stu-id="5a23b-103">Support multiple .NET versions</span></span>

<span data-ttu-id="5a23b-104">許多程式庫的目標都設為特定 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="5a23b-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="5a23b-105">例如，您可能有一版的程式庫是 UWP 特有的，而另一個版本則利用 .NET Framework 4.6 中的功能。</span><span class="sxs-lookup"><span data-stu-id="5a23b-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="5a23b-106">為了配合此功能，NuGet 支援在單一套件中放置相同程式庫的多個版本。</span><span class="sxs-lookup"><span data-stu-id="5a23b-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="5a23b-107">本文描述 NuGet 套件的配置，不論封裝或元件的建立方式為何（也就是使用多個非 SDK 樣式 *.csproj*檔案和自訂*nuspec*檔案，或單一多目標 SDK 樣式 *.csproj*）的版面配置。</span><span class="sxs-lookup"><span data-stu-id="5a23b-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="5a23b-108">針對 SDK 樣式專案，NuGet [套件目標](../reference/msbuild-targets.md)知道套件應如何配置，且會將組件放在正確的 lib 資料夾中自動化，並為每個目標 Framework (TFM) 建立相依性群組。</span><span class="sxs-lookup"><span data-stu-id="5a23b-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="5a23b-109">如需詳細指示，請參閱[在您的專案檔中支援多個 .NET Framework 版本](multiple-target-frameworks-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="5a23b-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="5a23b-110">如果您使用[建立套件](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)中所述的傳統型工作目錄方法，就必須如此文章中所述手動配置套件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="5a23b-111">針對 SDK 樣式專案，建議使用自動化方法，但您也可以選擇如此文章中所述手動配置套件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="5a23b-112">架構版本資料夾結構</span><span class="sxs-lookup"><span data-stu-id="5a23b-112">Framework version folder structure</span></span>

<span data-ttu-id="5a23b-113">如果所建置的架構只包含一個版本的程式庫，或將目標設為多個架構，您一律會搭配使用不同的區分大小寫架構名稱與下列慣例，以在 `lib` 下建立子資料夾：</span><span class="sxs-lookup"><span data-stu-id="5a23b-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="5a23b-114">如需所支援名稱的完整清單，請參閱[目標架構參考](../reference/target-frameworks.md#supported-frameworks)。</span><span class="sxs-lookup"><span data-stu-id="5a23b-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="5a23b-115">您的程式庫版本絕對不應該是架構特有的，而且會直接放在根 `lib` 資料夾中</span><span class="sxs-lookup"><span data-stu-id="5a23b-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="5a23b-116">(過去只有 `packages.config` 才支援此功能)。</span><span class="sxs-lookup"><span data-stu-id="5a23b-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="5a23b-117">如此會讓程式庫與任何目標架構相容，並且能夠安裝在任何位置，因而可能導致意外的執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="5a23b-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="5a23b-118">使用 PackagesReference 格式時，已取代並忽略在根資料夾 (例如 `lib\abc.dll`) 或子資料夾 (例如 `lib\abc\abc.dll`) 中新增組件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="5a23b-119">例如，下列資料夾結構支援架構特有的四種版本的組件：</span><span class="sxs-lookup"><span data-stu-id="5a23b-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="5a23b-120">若要在建置套件時輕鬆地包含所有這些檔案，請在 `**` 的 `<files>` 區段中使用遞迴 `.nuspec` 萬用字元：</span><span class="sxs-lookup"><span data-stu-id="5a23b-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="5a23b-121">架構特有資料夾</span><span class="sxs-lookup"><span data-stu-id="5a23b-121">Architecture-specific folders</span></span>

<span data-ttu-id="5a23b-122">如果您有架構特有組件 (即目標設為 ARM、x86 和 x64 的不同組件)，則必須將它們放在 `runtimes` 資料夾的 `{platform}-{architecture}\lib\{framework}` 或 `{platform}-{architecture}\native` 子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5a23b-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="5a23b-123">例如，下列資料夾結構將放置原生以及目標設為 Windows 10 和 `uap10.0` 架構的 Managed DLL：</span><span class="sxs-lookup"><span data-stu-id="5a23b-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="5a23b-124">這些組件只有在執行階段中可用，因此若您也要提供對應的編譯階段組件，`AnyCPU` 必須位於 `/ref/{tfm}` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5a23b-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="5a23b-125">請注意，NuGet 一律會從一個資料夾挑選這些編譯或執行階段資產，因此若有一些來自 `/ref` 的相容資產，則將忽略 `/lib` 以新增編譯階段組件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="5a23b-126">同樣地，如果 `/runtimes` 有一些相容的資產，則執行時間也會忽略 `/lib`。</span><span class="sxs-lookup"><span data-stu-id="5a23b-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="5a23b-127">如需在 [ 資訊清單中參考這些檔案的範例，請參閱](../guides/create-uwp-packages.md)建立 UWP 套件`.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="5a23b-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="5a23b-128">此外，請參閱[使用 NuGet 封裝 Windows 市集應用程式](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="5a23b-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="5a23b-129">比對組件版本與專案中的目標架構</span><span class="sxs-lookup"><span data-stu-id="5a23b-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="5a23b-130">如果 NuGet 所安裝的套件具有多個組件版本，則會嘗試比對組件的架構名稱與專案的目標架構。</span><span class="sxs-lookup"><span data-stu-id="5a23b-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="5a23b-131">如果找不到相符項目，則 NuGet 會複製小於或等於專案目標架構 (如果可用) 的最高版本的組件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="5a23b-132">如果找到不相容的組件，NuGet 會傳回適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5a23b-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="5a23b-133">例如，請考慮在套件中使用下列資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="5a23b-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="5a23b-134">在目標設為 .NET Framework 4.6 的專案中安裝此套件時，NuGet 會在 `net45` 資料夾中安裝組件，因為這是小於或等於 4.6 的最高可用版本。</span><span class="sxs-lookup"><span data-stu-id="5a23b-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="5a23b-135">如果專案的目標設為 .NET Framework 4.6.1，則另一方面，NuGet 會安裝 `net461` 資料夾中的組件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="5a23b-136">如果專案的目標設為 .NET Framework 4.0 和更早版本，NuGet 會擲回找不到相容組件的適當錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5a23b-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="5a23b-137">依架構版本來群組組件</span><span class="sxs-lookup"><span data-stu-id="5a23b-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="5a23b-138">NuGet 只會複製套件中單一程式庫資料夾的組件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="5a23b-139">例如，假設套件具有下列資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="5a23b-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="5a23b-140">在目標設為 .NET Framework 4.5 的專案中安裝套件時，`MyAssembly.dll` (2.0 版) 是唯一安裝的組件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="5a23b-141">未安裝 `MyAssembly.Core.dll` (v1.0)，因為它未列在 `net45` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5a23b-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="5a23b-142">因為 `MyAssembly.Core.dll` 可能已合併至 2.0 版的 `MyAssembly.dll`，所以 NuGet 會以這種方式運作。</span><span class="sxs-lookup"><span data-stu-id="5a23b-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="5a23b-143">如果您想要為 .NET Framework 4.5 安裝 `MyAssembly.Core.dll`，請將複本放在 `net45` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5a23b-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="5a23b-144">依架構設定檔來群組組件</span><span class="sxs-lookup"><span data-stu-id="5a23b-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="5a23b-145">NuGet 也支援將目標設為特定架構設定檔，方法是將一個破折號和設定檔名稱附加到資料夾結尾。</span><span class="sxs-lookup"><span data-stu-id="5a23b-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="5a23b-146">支援的設定檔如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a23b-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="5a23b-147">`client`：用戶端設定檔</span><span class="sxs-lookup"><span data-stu-id="5a23b-147">`client`: Client Profile</span></span>
- <span data-ttu-id="5a23b-148">`full`：完整設定檔</span><span class="sxs-lookup"><span data-stu-id="5a23b-148">`full`: Full Profile</span></span>
- <span data-ttu-id="5a23b-149">`wp`：Windows Phone</span><span class="sxs-lookup"><span data-stu-id="5a23b-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="5a23b-150">`cf`：Compact Framework</span><span class="sxs-lookup"><span data-stu-id="5a23b-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="5a23b-151">宣告相依性 (進階)</span><span class="sxs-lookup"><span data-stu-id="5a23b-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="5a23b-152">封裝專案檔時，NuGet 會嘗試自動從專案產生相依性。</span><span class="sxs-lookup"><span data-stu-id="5a23b-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="5a23b-153">此節中有關使用 *.nuspec* 檔案來宣告相依性的資訊，通常只有進階情節才需要。</span><span class="sxs-lookup"><span data-stu-id="5a23b-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="5a23b-154">*(2.0 版+)* 您可以使用 *元素內的* 元素，在對應至目標專案之目標 Framework 的 `<group>`.nuspec`<dependencies>` 中宣告套件相依性。</span><span class="sxs-lookup"><span data-stu-id="5a23b-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="5a23b-155">如需詳細資訊，請參閱[相依性元素](../reference/nuspec.md#dependencies-element)。</span><span class="sxs-lookup"><span data-stu-id="5a23b-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="5a23b-156">每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<dependency>` 項目。</span><span class="sxs-lookup"><span data-stu-id="5a23b-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="5a23b-157">當目標 Framework 與專案的 Framework 設定檔相容時，會同時安裝那些相依性。</span><span class="sxs-lookup"><span data-stu-id="5a23b-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="5a23b-158">如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="5a23b-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="5a23b-159">針對 *lib/* 與 *ref/* 資料夾中的檔案，建議針對每個目標 Framework Moniker (TFM) 使用一個群組。</span><span class="sxs-lookup"><span data-stu-id="5a23b-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="5a23b-160">下列範例示範 `<group>` 項目的不同變化：</span><span class="sxs-lookup"><span data-stu-id="5a23b-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="5a23b-161">判斷要使用的 NuGet 目標</span><span class="sxs-lookup"><span data-stu-id="5a23b-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="5a23b-162">封裝目標設為可攜式類別庫的程式庫時，可能很難判斷您應該在資料夾名稱和 `.nuspec` 檔案中使用的 NuGet 目標，特別是目標只設為 PCL 子集時。</span><span class="sxs-lookup"><span data-stu-id="5a23b-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="5a23b-163">下列外部資源將協助您進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="5a23b-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="5a23b-164">[.NET 中的架構設定檔](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="5a23b-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="5a23b-165">[可攜式類別庫設定檔](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co)：列舉 PCL 設定檔和其對等 NuGet 目標的資料表</span><span class="sxs-lookup"><span data-stu-id="5a23b-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="5a23b-166">[可攜式類別庫設定檔工具](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com)：用於判斷系統上可用之 PCL 設定檔的命令列工具</span><span class="sxs-lookup"><span data-stu-id="5a23b-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="5a23b-167">內容檔案和 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="5a23b-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="5a23b-168">只有使用 `packages.config` 格式才能使用可變動的內容檔案和指令碼執行；可變動的內容檔案和指令碼執行已隨所有其他格式遭取代，而且不應該用於任何新套件。</span><span class="sxs-lookup"><span data-stu-id="5a23b-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="5a23b-169">使用 `packages.config`，可以在 `content` 和 `tools` 資料夾內使用相同的資料夾慣例，以依目標架構來群組內容檔案和 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a23b-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="5a23b-170">例如，</span><span class="sxs-lookup"><span data-stu-id="5a23b-170">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="5a23b-171">如果架構資料夾空白，則 NuGet 不會新增組件參考或內容檔案，或執行該架構的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a23b-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="5a23b-172">因為 `init.ps1` 是在方案層級執行，並且與專案無關，所以必須直接將它放在 `tools` 資料夾下方。</span><span class="sxs-lookup"><span data-stu-id="5a23b-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="5a23b-173">如果放在架構資料夾下方，則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="5a23b-173">It's ignored if placed under a framework folder.</span></span>
