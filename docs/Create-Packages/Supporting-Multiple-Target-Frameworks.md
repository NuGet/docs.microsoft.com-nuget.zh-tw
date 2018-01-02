---
title: "NuGet 套件的多目標 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2646ffcd-83ae-4086-8915-a7fba3f53e45
description: "將目標設為單一 NuGet 套件內多個 .NET Framework 版本之各種方法的描述。"
keywords: "NuGet 套件目標、.NET Framework 版本、NuGet 和 .NET、目標設為多個架構、NuGet 套件建立"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d23158c6dab838b723764994e94fc21cab52f553
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="65a6b-104">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="65a6b-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="65a6b-105">*針對使用 NuGet 4.0+ 的 .NET Core 專案，請參閱 [NuGet 封裝和還原為 MSBuild 目標](../schema/msbuild-targets.md)，以取得跨目標的詳細資料。*</span><span class="sxs-lookup"><span data-stu-id="65a6b-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="65a6b-106">許多程式庫的目標都設為特定 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="65a6b-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="65a6b-107">例如，您可能有一版的程式庫是 UWP 特有的，而另一個版本則利用 .NET Framework 4.6 中的功能。</span><span class="sxs-lookup"><span data-stu-id="65a6b-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="65a6b-108">為了完成此作業，使用[建立套件](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)中所述的慣例工作目錄方法時，NuGet 會支援將相同程式庫的多個版本放入單一套件中。</span><span class="sxs-lookup"><span data-stu-id="65a6b-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

<span data-ttu-id="65a6b-109">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="65a6b-109">In this topic:</span></span>

- [<span data-ttu-id="65a6b-110">架構版本資料夾結構</span><span class="sxs-lookup"><span data-stu-id="65a6b-110">Framework version folder structure</span></span>](#framework-version-folder-structure)
- [<span data-ttu-id="65a6b-111">比對組件版本與專案中的目標架構</span><span class="sxs-lookup"><span data-stu-id="65a6b-111">Matching assembly versions and the target framework in a project</span></span>](#matching-assembly-versions-and-the-target-framework-in-a-project)
- [<span data-ttu-id="65a6b-112">依架構版本來群組組件</span><span class="sxs-lookup"><span data-stu-id="65a6b-112">Grouping assemblies by framework version</span></span>](#grouping-assemblies-by-framework-version)
- [<span data-ttu-id="65a6b-113">判斷要使用的 NuGet 目標</span><span class="sxs-lookup"><span data-stu-id="65a6b-113">Determining which NuGet target to use</span></span>](#determining-which-nuget-target-to-use)
- [<span data-ttu-id="65a6b-114">內容檔案和 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="65a6b-114">Content files and PowerShell scripts</span></span>](#content-files-and-powershell-scripts)


## <a name="framework-version-folder-structure"></a><span data-ttu-id="65a6b-115">架構版本資料夾結構</span><span class="sxs-lookup"><span data-stu-id="65a6b-115">Framework version folder structure</span></span>

<span data-ttu-id="65a6b-116">如果所建置的架構只包含一個版本的程式庫，或將目標設為多個架構，您一律會搭配使用不同的區分大小寫架構名稱與下列慣例，以在 `lib` 下建立子資料夾：</span><span class="sxs-lookup"><span data-stu-id="65a6b-116">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="65a6b-117">如需所支援名稱的完整清單，請參閱[目標架構參考](../schema/target-frameworks.md#supported-frameworks)。</span><span class="sxs-lookup"><span data-stu-id="65a6b-117">For a complete list of supported names, see the [Target Frameworks reference](../schema/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="65a6b-118">您的程式庫版本絕對不應該是架構特有的，而且會直接放在根 `lib` 資料夾中 </span><span class="sxs-lookup"><span data-stu-id="65a6b-118">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="65a6b-119">(過去只有 `packages.config` 才支援此功能)。</span><span class="sxs-lookup"><span data-stu-id="65a6b-119">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="65a6b-120">這麼做可與任何目標架構相容，並使其能夠安裝在任何位置，但可能會導致意外的執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="65a6b-120">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="65a6b-121">使用 PackagesReference 格式時，已取代並忽略在根資料夾 (例如 `lib\abc.dll`) 或子資料夾 (例如 `lib\abc\abc.dll`) 中新增組件。</span><span class="sxs-lookup"><span data-stu-id="65a6b-121">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="65a6b-122">例如，下列資料夾結構支援架構特有的四種版本的組件：</span><span class="sxs-lookup"><span data-stu-id="65a6b-122">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="65a6b-123">若要在建置套件時輕鬆地包含所有這些檔案，請在 `.nuspec` 的 `<files>` 區段中使用遞迴 `**` 萬用字元：</span><span class="sxs-lookup"><span data-stu-id="65a6b-123">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="65a6b-124">架構特有資料夾</span><span class="sxs-lookup"><span data-stu-id="65a6b-124">Architecture-specific folders</span></span> 

<span data-ttu-id="65a6b-125">如果您有架構特有組件 (即目標設為 ARM、x86 和 x64 的不同組件)，則必須將它們放在 `runtimes` 資料夾的 `{platform}-{architecture}\lib\{framework}` 或 `{platform}-{architecture}\native` 子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="65a6b-125">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="65a6b-126">例如，下列資料夾結構將放置原生以及目標設為 Windows 10 和 `uap10.0` 架構的 Managed DLL：</span><span class="sxs-lookup"><span data-stu-id="65a6b-126">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="65a6b-127">如需在 `.nuspec` 資訊清單中參考這些檔案的範例，請參閱[建立 UWP 套件](../Guides/Create-UWP-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="65a6b-127">See [Create UWP Packages](../Guides/Create-UWP-Packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>


## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="65a6b-128">比對組件版本與專案中的目標架構</span><span class="sxs-lookup"><span data-stu-id="65a6b-128">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="65a6b-129">如果 NuGet 所安裝的套件具有多個組件版本，則會嘗試比對組件的架構名稱與專案的目標架構。</span><span class="sxs-lookup"><span data-stu-id="65a6b-129">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="65a6b-130">如果找不到相符項目，則 NuGet 會複製小於或等於專案目標架構 (如果可用) 的最高版本的組件。</span><span class="sxs-lookup"><span data-stu-id="65a6b-130">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="65a6b-131">如果找到不相容的組件，NuGet 會傳回適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="65a6b-131">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="65a6b-132">例如，請考慮在套件中使用下列資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="65a6b-132">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll


<span data-ttu-id="65a6b-133">在目標設為 .NET Framework 4.6 的專案中安裝此套件時，NuGet 會在 `net45` 資料夾中安裝組件，因為這是小於或等於 4.6 的最高可用版本。</span><span class="sxs-lookup"><span data-stu-id="65a6b-133">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="65a6b-134">如果專案的目標設為 .NET Framework 4.6.1，則另一方面，NuGet 會安裝 `net461` 資料夾中的組件。</span><span class="sxs-lookup"><span data-stu-id="65a6b-134">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="65a6b-135">如果專案的目標設為 .NET Framework 4.0 和更早版本，NuGet 會擲回找不到相容組件的適當錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="65a6b-135">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="65a6b-136">依架構版本來群組組件</span><span class="sxs-lookup"><span data-stu-id="65a6b-136">Grouping assemblies by framework version</span></span>

<span data-ttu-id="65a6b-137">NuGet 只會複製套件中單一程式庫資料夾的組件。</span><span class="sxs-lookup"><span data-stu-id="65a6b-137">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="65a6b-138">例如，假設套件具有下列資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="65a6b-138">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="65a6b-139">在目標設為 .NET Framework 4.5 的專案中安裝套件時，`MyAssembly.dll` (2.0 版) 是唯一安裝的組件。</span><span class="sxs-lookup"><span data-stu-id="65a6b-139">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="65a6b-140">未安裝 `MyAssembly.Core.dll` (v1.0)，因為它未列在 `net45` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="65a6b-140">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="65a6b-141">因為 `MyAssembly.Core.dll` 可能已合併至 2.0 版的 `MyAssembly.dll`，所以 NuGet 會以這種方式運作。</span><span class="sxs-lookup"><span data-stu-id="65a6b-141">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="65a6b-142">如果您想要為 .NET Framework 4.5 安裝 `MyAssembly.Core.dll`，請將複本放在 `net45` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="65a6b-142">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="65a6b-143">依架構設定檔來群組組件</span><span class="sxs-lookup"><span data-stu-id="65a6b-143">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="65a6b-144">NuGet 也支援將目標設為特定架構設定檔，方法是將一個破折號和設定檔名稱附加到資料夾結尾。</span><span class="sxs-lookup"><span data-stu-id="65a6b-144">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="65a6b-145">支援的設定檔如下所示：</span><span class="sxs-lookup"><span data-stu-id="65a6b-145">The supported profiles are as follows:</span></span>

- <span data-ttu-id="65a6b-146">`client`：用戶端設定檔</span><span class="sxs-lookup"><span data-stu-id="65a6b-146">`client`: Client Profile</span></span>
- <span data-ttu-id="65a6b-147">`full`：完整設定檔</span><span class="sxs-lookup"><span data-stu-id="65a6b-147">`full`: Full Profile</span></span>
- <span data-ttu-id="65a6b-148">`wp`：Windows Phone</span><span class="sxs-lookup"><span data-stu-id="65a6b-148">`wp`: Windows Phone</span></span>
- <span data-ttu-id="65a6b-149">`cf`：Compact Framework</span><span class="sxs-lookup"><span data-stu-id="65a6b-149">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="65a6b-150">判斷要使用的 NuGet 目標</span><span class="sxs-lookup"><span data-stu-id="65a6b-150">Determining which NuGet target to use</span></span>

<span data-ttu-id="65a6b-151">封裝目標設為可攜式類別庫的程式庫時，可能很難判斷您應該在資料夾名稱和 `.nuspec` 檔案中使用的 NuGet 目標，特別是目標只設為 PCL 子集時。</span><span class="sxs-lookup"><span data-stu-id="65a6b-151">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="65a6b-152">下列外部資源將協助您進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="65a6b-152">The following external resources will help you with this:</span></span>

- <span data-ttu-id="65a6b-153">[.NET 中的架構設定檔](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="65a6b-153">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="65a6b-154">[可攜式類別庫設定檔](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co)：列舉 PCL 設定檔和其對等 NuGet 目標的資料表</span><span class="sxs-lookup"><span data-stu-id="65a6b-154">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="65a6b-155">[可攜式類別庫設定檔工具](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com)：用於判斷系統上可用之 PCL 設定檔的命令列工具</span><span class="sxs-lookup"><span data-stu-id="65a6b-155">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="65a6b-156">內容檔案和 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="65a6b-156">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="65a6b-157">只有使用 `packages.config` 格式才能使用可變動的內容檔案和指令碼執行；可變動的內容檔案和指令碼執行已在使用 `project.json` 和 PackagesReference 格式時遭取代，而且不應該用於任何新套件。</span><span class="sxs-lookup"><span data-stu-id="65a6b-157">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated when using `project.json` and PackagesReference formats and should should not be used for any new packages.</span></span>

<span data-ttu-id="65a6b-158">使用 `packages.config`，可以在 `content` 和 `tools` 資料夾內使用相同的資料夾慣例，以依目標架構來群組內容檔案和 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="65a6b-158">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="65a6b-159">例如: </span><span class="sxs-lookup"><span data-stu-id="65a6b-159">For example:</span></span>

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

<span data-ttu-id="65a6b-160">如果架構資料夾空白，則 NuGet 不會新增組件參考或內容檔案，或執行該架構的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="65a6b-160">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="65a6b-161">因為 `init.ps1` 是在方案層級執行，並且與專案無關，所以必須直接將它放在 `tools` 資料夾下方。</span><span class="sxs-lookup"><span data-stu-id="65a6b-161">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="65a6b-162">如果放在架構資料夾下方，則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="65a6b-162">It's ignored if placed under a framework folder.</span></span>
