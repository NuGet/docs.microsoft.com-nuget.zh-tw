---
title: 選取專案所參考的組件
description: 讓套件中的部分組件可供編譯器使用，而所有組件在執行階段皆可用。
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859027"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="a5a97-103">選取專案所參考的組件</span><span class="sxs-lookup"><span data-stu-id="a5a97-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="a5a97-104">明確的組件參考可讓部分組件用於 IntelliSense 及編譯，而所有組件在執行階段皆可用。</span><span class="sxs-lookup"><span data-stu-id="a5a97-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="a5a97-105">`PackageReference` 和 `packages.config` 的運作方式不同，因此套件作者必須費心建立套件，以便與這兩種專案類型相容。</span><span class="sxs-lookup"><span data-stu-id="a5a97-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="a5a97-106">明確的組件參考與 .NET 組件有關。</span><span class="sxs-lookup"><span data-stu-id="a5a97-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="a5a97-107">它不是受控組件 P/叫用原生組件的散發方法。</span><span class="sxs-lookup"><span data-stu-id="a5a97-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="a5a97-108">`PackageReference` 支援</span><span class="sxs-lookup"><span data-stu-id="a5a97-108">`PackageReference` support</span></span>

<span data-ttu-id="a5a97-109">當專案使用 `PackageReference` 來搭配套件且套件包含 `ref\<tfm>\` 目錄時，NuGet 會將那些組合分類為編譯時期資產，而 `lib\<tfm>\` 組件會分類為執行階段資產。</span><span class="sxs-lookup"><span data-stu-id="a5a97-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="a5a97-110">`ref\<tfm>\` 中的組件不會在執行階段使用。</span><span class="sxs-lookup"><span data-stu-id="a5a97-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="a5a97-111">這表示 `ref\<tfm>\` 中的任何組件必須要在 `lib\<tfm>\` 或相關 `runtime\` 目錄中有符合的組件，否則可能會發生執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="a5a97-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="a5a97-112">由於 `ref\<tfm>\` 中的組件不會在執行階段使用，因此它們可以是[僅限中繼資料的組件](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md)，以便縮減套件大小。</span><span class="sxs-lookup"><span data-stu-id="a5a97-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="a5a97-113">如果套件包含 nuspec `<references>` 元素 (由 `packages.config` 使用，如下所示)，且在 `ref\<tfm>\` 中不包含組件，則 NuGet 會將 nuspec `<references>` 元素中列出的組件通告為編譯和執行階段資產。</span><span class="sxs-lookup"><span data-stu-id="a5a97-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="a5a97-114">這表示當參考的組件需要載入 `lib\<tfm>\` 目錄中任何其他組件時，會有執行階段例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a5a97-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="a5a97-115">如果套件包含 `runtime\` 目錄，則 NuGet 不能使用 `lib\` 目錄中的資產。</span><span class="sxs-lookup"><span data-stu-id="a5a97-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="a5a97-116">`packages.config` 支援</span><span class="sxs-lookup"><span data-stu-id="a5a97-116">`packages.config` support</span></span>

<span data-ttu-id="a5a97-117">使用 `packages.config` 管理 NuGet 套件的專案，通常會新增對 `lib\<tfm>\` 目錄中所有組件的參考。</span><span class="sxs-lookup"><span data-stu-id="a5a97-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="a5a97-118">已新增 `ref\` 目錄來支援 `PackageReference`，因此在使用 `packages.config` 時不會考慮它。</span><span class="sxs-lookup"><span data-stu-id="a5a97-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="a5a97-119">若要明確設定使用的專案參考的元件 `packages.config` ，封裝必須使用 nuspec 檔[ `<references>` 中的元素](../reference/nuspec.md#explicit-assembly-references)。</span><span class="sxs-lookup"><span data-stu-id="a5a97-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="a5a97-120">例如：</span><span class="sxs-lookup"><span data-stu-id="a5a97-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="a5a97-121">`packages.config` 專案使用稱為 [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) 的處理序來將組件複製到 `bin\<configuration>\` 輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="a5a97-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="a5a97-122">會複製您專案的組件，然後建置系統會查看所參考組件的組件資訊清單，然後複製這些組件並以遞迴方式針對所有組件重複執行。</span><span class="sxs-lookup"><span data-stu-id="a5a97-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="a5a97-123">這表示，如果 `lib\<tfm>\` 目錄中的任何組件未列在任何其他組件資訊清單中作為相依性 (如果在執行階段使用 `Assembly.Load`、MEF 或另一個相依性插入架構來載入組件)，則它可能不會複製到您專案的 `bin\<configuration>\` 輸出目錄，即使它在 `bin\<tfm>\` 中。</span><span class="sxs-lookup"><span data-stu-id="a5a97-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="a5a97-124">範例</span><span class="sxs-lookup"><span data-stu-id="a5a97-124">Example</span></span>

<span data-ttu-id="a5a97-125">我的套件會包含三個組件：`MyLib.dll`、`MyHelpers.dll` 和 `MyUtilities.dll`，它們以 .NET Framework 4.7.2 為目標。</span><span class="sxs-lookup"><span data-stu-id="a5a97-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="a5a97-126">`MyUtilities.dll` 包含的類別只為了供其他兩個組件使用，因此我不想要在 IntelliSense 中提供這些類別，或在編譯時期提供給使用我套件的專案。</span><span class="sxs-lookup"><span data-stu-id="a5a97-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="a5a97-127">我的 `nuspec` 檔案必須包含下列 XML 元素：</span><span class="sxs-lookup"><span data-stu-id="a5a97-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="a5a97-128">且套件中的檔案將為：</span><span class="sxs-lookup"><span data-stu-id="a5a97-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
