---
title: 建立舊版符號套件（. 符號. nupkg）
description: 如何建立只包含符號的 NuGet 套件，以支援在 Visual Studio 中偵錯其他 NuGet 套件。
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476265"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="63efb-103">建立舊版符號套件（. 符號. nupkg）</span><span class="sxs-lookup"><span data-stu-id="63efb-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="63efb-104">為符號套件新建議的格式為 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="63efb-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="63efb-105">請參閱[建立符號套件 (.snupkg)](Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="63efb-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="63efb-106">目前仍然支援 .symbols.nupkg，只是為達到相容性而已。</span><span class="sxs-lookup"><span data-stu-id="63efb-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="63efb-107">除了建立 nuget.org 或其他來源的套件之外，NuGet 也支援建立可發行至符號伺服器的相關符號套件。</span><span class="sxs-lookup"><span data-stu-id="63efb-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="63efb-108">舊版符號套件格式 nupkg 可推送至 SymbolSource 存放庫。</span><span class="sxs-lookup"><span data-stu-id="63efb-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="63efb-109">套件取用者接著可以在 Visual Studio 中將 `https://nuget.smbsrc.net` 新增至其符號來源，以允許在 Visual Studio 偵錯工具中逐步執行套件程式碼。</span><span class="sxs-lookup"><span data-stu-id="63efb-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="63efb-110">如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="63efb-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="63efb-111">建立舊版符號套件</span><span class="sxs-lookup"><span data-stu-id="63efb-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="63efb-112">若要建立舊版符號套件，請遵循下列慣例：</span><span class="sxs-lookup"><span data-stu-id="63efb-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="63efb-113">將主要套件 (含您的程式碼) 命名為 `{identifier}.nupkg`，並包含 `.pdb` 檔案以外的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="63efb-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="63efb-114">將舊版符號套件命名為 `{identifier}.symbols.nupkg` 並包含您的元件 DLL、`.pdb` 檔案、XMLDOC 檔、原始程式檔（請參閱下列各節）。</span><span class="sxs-lookup"><span data-stu-id="63efb-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="63efb-115">您可以使用 `-Symbols` 選項，從 `.nuspec` 檔案或專案檔建立兩個套件：</span><span class="sxs-lookup"><span data-stu-id="63efb-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="63efb-116">請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。</span><span class="sxs-lookup"><span data-stu-id="63efb-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="63efb-117">在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。</span><span class="sxs-lookup"><span data-stu-id="63efb-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="63efb-118">舊版符號套件結構</span><span class="sxs-lookup"><span data-stu-id="63efb-118">Legacy symbol package structure</span></span>

<span data-ttu-id="63efb-119">舊版符號套件可以用與程式庫封裝相同的方式，以多個目標 framework 為目標，因此 `lib` 資料夾的結構應該與主要封裝完全相同，只包括與 DLL `.pdb` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="63efb-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="63efb-120">例如，以 .NET 4.0 和 Silverlight 4 為目標的舊版符號套件會有此配置：</span><span class="sxs-lookup"><span data-stu-id="63efb-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="63efb-121">原始程式檔接著會放在名為 `src` 的個別特殊資料夾中，而此資料夾必須遵循來源存放庫的相對結構。</span><span class="sxs-lookup"><span data-stu-id="63efb-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="63efb-122">這是因為 PDB 包含用來編譯相符 DLL 之原始程式檔的絕對路徑，而且需要在發行程序期間找到它們。</span><span class="sxs-lookup"><span data-stu-id="63efb-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="63efb-123">可以去除基底路徑（一般路徑前置詞）。例如，假設有一個從這些檔案建立的程式庫：</span><span class="sxs-lookup"><span data-stu-id="63efb-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="63efb-124">除了 [`lib`] 資料夾之外，舊版符號套件也必須包含此版面配置：</span><span class="sxs-lookup"><span data-stu-id="63efb-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="63efb-125">參考 nuspec 中的檔案</span><span class="sxs-lookup"><span data-stu-id="63efb-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="63efb-126">舊版符號套件可以根據慣例、上一節中所述的資料夾結構，或在資訊清單的 [`files`] 區段中指定其內容來建立。</span><span class="sxs-lookup"><span data-stu-id="63efb-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="63efb-127">例如，若要建置上節所示的套件，請在 `.nuspec` 檔案中使用下列內容：</span><span class="sxs-lookup"><span data-stu-id="63efb-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="63efb-128">發行舊版符號套件</span><span class="sxs-lookup"><span data-stu-id="63efb-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="63efb-129">若要將套件推送到 nuget.org，您必須使用 [nuget.exe v4.9.1 或更新版本](https://www.nuget.org/downloads)，它會實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="63efb-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="63efb-130">為了方便起見，請先使用 NuGet 儲存 API 金鑰 (請參閱[發行套件](../nuget-org/publish-a-package.md)，這適用於 nuget.org 和 symbolsource.org，因為 symbolsource.org 將向 nuget.org 確認，確認您是套件擁有者。</span><span class="sxs-lookup"><span data-stu-id="63efb-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="63efb-131">將主要套件發佈至 nuget.org 之後，推送舊版符號套件，如下所示，這會因為檔案名中的 `.symbols` 而自動使用 symbolsource.org 做為目標：</span><span class="sxs-lookup"><span data-stu-id="63efb-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="63efb-132">若要發行至不同的符號存放庫，或推送未遵循命名慣例的舊版符號套件，請使用 `-Source` 選項：</span><span class="sxs-lookup"><span data-stu-id="63efb-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="63efb-133">您也可以使用下列項目，同時將主要和符號套件推送至兩個存放庫：</span><span class="sxs-lookup"><span data-stu-id="63efb-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="63efb-134">使用 nuget.exe 4.5.0 或更高版本時，不會將符號套件自動推送至 symbolsource.org。您需要個別推送符號套件，如先前步驟中所述。</span><span class="sxs-lookup"><span data-stu-id="63efb-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="63efb-135">在此情況下，NuGet 將主要套件發行至 nuget.org 之後，會將 `MyPackage.symbols.nupkg` (存在時) 發行至 https://nuget.smbsrc.net/ (symbolsource.org 的推送 URL)。</span><span class="sxs-lookup"><span data-stu-id="63efb-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="63efb-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="63efb-136">See also</span></span>

* <span data-ttu-id="63efb-137">[建立符號套件（. .snupkg）](Symbol-Packages-snupkg.md) -符號套件的新建議格式</span><span class="sxs-lookup"><span data-stu-id="63efb-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="63efb-138">[移至新的 SymbolSource 引擎](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="63efb-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
