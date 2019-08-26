---
title: 如何建立 NuGet 符號套件
description: 如何建立只包含符號的 NuGet 套件，以支援在 Visual Studio 中偵錯其他 NuGet 套件。
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f7503dd413a976997580aa03da26df0c462ff0e1
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564545"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="994be-103">建立符號套件 (舊版)</span><span class="sxs-lookup"><span data-stu-id="994be-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="994be-104">為符號套件新建議的格式為 .snupkg。</span><span class="sxs-lookup"><span data-stu-id="994be-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="994be-105">請參閱[建立符號套件 (.snupkg)](Symbol-Packages-snupkg.md)。</span><span class="sxs-lookup"><span data-stu-id="994be-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="994be-106">目前仍然支援 .symbols.nupkg，只是為達到相容性而已。</span><span class="sxs-lookup"><span data-stu-id="994be-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="994be-107">除了建置 nuget.org 或其他來源的套件之外，NuGet 也支援建立相關聯符號套件以及將它們發行至 SymbolSource 存放庫。</span><span class="sxs-lookup"><span data-stu-id="994be-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="994be-108">套件取用者接著可以在 Visual Studio 中將 `https://nuget.smbsrc.net` 新增至其符號來源，以允許在 Visual Studio 偵錯工具中逐步執行套件程式碼。</span><span class="sxs-lookup"><span data-stu-id="994be-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="994be-109">如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="994be-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="994be-110">建立符號套件</span><span class="sxs-lookup"><span data-stu-id="994be-110">Creating a symbol package</span></span>

<span data-ttu-id="994be-111">若要建立符號套件，請遵循下列慣例：</span><span class="sxs-lookup"><span data-stu-id="994be-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="994be-112">將主要套件 (含您的程式碼) 命名為 `{identifier}.nupkg`，並包含 `.pdb` 檔案以外的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="994be-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="994be-113">將符號套件命名為 `{identifier}.symbols.nupkg`，並包含組件 DLL、`.pdb` 檔案、XMLDOC 檔案、原始程式檔 (請參閱下列各節)。</span><span class="sxs-lookup"><span data-stu-id="994be-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="994be-114">您可以使用 `-Symbols` 選項，從 `.nuspec` 檔案或專案檔建立兩個套件：</span><span class="sxs-lookup"><span data-stu-id="994be-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="994be-115">請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。</span><span class="sxs-lookup"><span data-stu-id="994be-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="994be-116">在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。</span><span class="sxs-lookup"><span data-stu-id="994be-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="994be-117">符號套件結構</span><span class="sxs-lookup"><span data-stu-id="994be-117">Symbol package structure</span></span>

<span data-ttu-id="994be-118">符號套件可以將目標設為多個目標架構，其方式與程式庫套件相同，因此 `lib` 資料夾的結構應該與主要套件完全相同，其只包含 `.pdb` 檔案和 DLL。</span><span class="sxs-lookup"><span data-stu-id="994be-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="994be-119">例如，將目標設為 .NET 4.0 和 Silverlight 4 的符號套件會有下列配置：</span><span class="sxs-lookup"><span data-stu-id="994be-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="994be-120">原始程式檔接著會放在名為 `src` 的個別特殊資料夾中，而此資料夾必須遵循來源存放庫的相對結構。</span><span class="sxs-lookup"><span data-stu-id="994be-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="994be-121">這是因為 PDB 包含用來編譯相符 DLL 之原始程式檔的絕對路徑，而且需要在發行程序期間找到它們。</span><span class="sxs-lookup"><span data-stu-id="994be-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="994be-122">可以移除基底路徑 (通用路徑前置詞)。例如，請考慮使用從這些檔案建置的程式庫：</span><span class="sxs-lookup"><span data-stu-id="994be-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="994be-123">與 `lib` 資料夾不同，符號套件需要包含此配置：</span><span class="sxs-lookup"><span data-stu-id="994be-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="994be-124">參考 nuspec 中的檔案</span><span class="sxs-lookup"><span data-stu-id="994be-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="994be-125">依慣例，可以從上節中所述的資料夾結構，或在資訊清單的 `files` 區段中指定其內容，來建置符號套件。</span><span class="sxs-lookup"><span data-stu-id="994be-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="994be-126">例如，若要建置上節所示的套件，請在 `.nuspec` 檔案中使用下列內容：</span><span class="sxs-lookup"><span data-stu-id="994be-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="994be-127">發行符號套件</span><span class="sxs-lookup"><span data-stu-id="994be-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="994be-128">若要將套件推送到 nuget.org，您必須使用 [nuget.exe v4.9.1 或更新版本](https://www.nuget.org/downloads)，它會實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="994be-128">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="994be-129">為了方便起見，請先使用 NuGet 儲存 API 金鑰 (請參閱[發行套件](../nuget-org/publish-a-package.md)，這適用於 nuget.org 和 symbolsource.org，因為 symbolsource.org 將向 nuget.org 確認，確認您是套件擁有者。</span><span class="sxs-lookup"><span data-stu-id="994be-129">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="994be-130">將主要套件發行至 nuget.org 之後，請如下推送符號套件，因為檔案名稱中有 `.symbols`，所以這樣會自動使用 symbolsource.org 作為目標：</span><span class="sxs-lookup"><span data-stu-id="994be-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="994be-131">若要發行至不同的符號存放庫，或推送未遵循命名慣例的符號套件，請使用 `-Source` 選項：</span><span class="sxs-lookup"><span data-stu-id="994be-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="994be-132">您也可以使用下列項目，同時將主要和符號套件推送至兩個存放庫：</span><span class="sxs-lookup"><span data-stu-id="994be-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="994be-133">使用 nuget.exe 4.5.0 或以上版本，不會將符號套件自動推送至 symbolsource.org。您需要如稍早步驟所述個別推送符號套件。</span><span class="sxs-lookup"><span data-stu-id="994be-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="994be-134">在此情況下，NuGet 將主要套件發行至 nuget.org 之後，會將 `MyPackage.symbols.nupkg` (存在時) 發行至 https://nuget.smbsrc.net/ (symbolsource.org 的推送 URL)。</span><span class="sxs-lookup"><span data-stu-id="994be-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="994be-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="994be-135">See Also</span></span>

<span data-ttu-id="994be-136">[移至新的 SymbolSource 引擎](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="994be-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
