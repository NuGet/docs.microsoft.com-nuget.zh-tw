---
title: 如何使用新的符號套件格式 '.snupkg' 發行 NuGet 符號套件 | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 如何建立 NuGet 符號套件 (snupkg)。
keywords: NuGet 符號套件、NuGet 套件偵錯、支援 NuGet 偵錯、套件符號、符號套件慣例
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: a72b59a391ed25e9617ba3ba3656301a2ed90ddc
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580431"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="6f268-104">建立符號套件 (snupkg)</span><span class="sxs-lookup"><span data-stu-id="6f268-104">Creating symbol packages (.snupkg)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f268-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="6f268-105">Prerequisites</span></span>

<span data-ttu-id="6f268-106">[nuget.exe 第 4.9.0 版或更高版本](https://www.nuget.org/downloads)或是 [dotnet.exe 第 2.2.0 版或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，其實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="6f268-106">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="6f268-107">建立符號套件</span><span class="sxs-lookup"><span data-stu-id="6f268-107">Creating a symbol package</span></span>

<span data-ttu-id="6f268-108">您可以從 .nuspec 檔案或 .csproj 檔案，建立 snupkg 符號套件。</span><span class="sxs-lookup"><span data-stu-id="6f268-108">A snupkg symbol package can be created from a .nuspec file or from a .csproj file.</span></span> <span data-ttu-id="6f268-109">同時支援 NuGet.exe 與 dotnet.exe。</span><span class="sxs-lookup"><span data-stu-id="6f268-109">NuGet.exe and dotnet.exe are both supported.</span></span> <span data-ttu-id="6f268-110">當選項 ```-Symbols -SymbolPackageFormat snupkg``` 用於 nuget.exe 套件命令時，除了 .nupkg 檔案之外，還會建立 .snupkg 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f268-110">When the options ```-Symbols -SymbolPackageFormat snupkg``` are used on the nuget.exe pack command a .snupkg file will be created in additon to the .nupkg file.</span></span>

<span data-ttu-id="6f268-111">建立 .snupkg 檔案的命令範例</span><span class="sxs-lookup"><span data-stu-id="6f268-111">Example commands to create .snupkg files</span></span>
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild /t:pack MyPackage.csproj /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
```

<span data-ttu-id="6f268-112">根據預設，將不會產生 `.snupkgs`。</span><span class="sxs-lookup"><span data-stu-id="6f268-112">`.snupkgs` are not produced by default.</span></span> <span data-ttu-id="6f268-113">如果是 nuget.exe，您必須連同 `-Symbols` 傳遞 `SymbolsPackageFormat` 屬性，如果是 dotnet.exe 則傳遞 `--include-symbols`，如果是 msbuild 則傳遞 `/p:IncludeSymbols`。</span><span class="sxs-lookup"><span data-stu-id="6f268-113">You must pass the `SymbolsPackageFormat` property along with `-Symbols` in case of nuget.exe, `--include-symbols` in case of dotnet.exe, or `/p:IncludeSymbols` in case of msbuild.</span></span>

<span data-ttu-id="6f268-114">SymbolsPackageFormat 屬性可有以下兩個值的其中之一：`symbols.nupkg` (預設值) 或 `snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6f268-114">SymbolsPackageFormat property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="6f268-115">若未指定 SymbolsPackageFormat，它會預設為 `symbols.nupkg`，且會建立舊版符號套件。</span><span class="sxs-lookup"><span data-stu-id="6f268-115">If the SymbolsPackageFormat is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="6f268-116">目前仍然支援舊版格式 `.symbols.nupkg`，只是為達到相容性而已 (請參閱[舊版符號套件](Symbol-Packages.md))。</span><span class="sxs-lookup"><span data-stu-id="6f268-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="6f268-117">NuGet.org 符號伺服器只接受新的符號套件格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6f268-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="6f268-118">發行符號套件</span><span class="sxs-lookup"><span data-stu-id="6f268-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="6f268-119">為方便起見，請先使用 NuGet 儲存您的 API 金鑰 (請參閱[發佈套件](../create-packages/publish-a-package.md))。</span><span class="sxs-lookup"><span data-stu-id="6f268-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="6f268-120">將主要套件發佈至 nuget.org 後，接著推送符號套件。</span><span class="sxs-lookup"><span data-stu-id="6f268-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="6f268-121">您也可以使用以下命令，同時推送主要套件與符號套件。</span><span class="sxs-lookup"><span data-stu-id="6f268-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="6f268-122">.nupkg 和 .snupkg 檔案都必須出現在目前的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6f268-122">Both, .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="6f268-123">在此情況下，NuGet 將會先將 `MyPackage.nupkg` 發佈至 nuget.org，然後再發佈 `MyPackage.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6f268-123">In this case, NuGet will publish to nuget.org the `MyPackage.nupkg` first followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="6f268-124">NuGet.org 符號伺服器</span><span class="sxs-lookup"><span data-stu-id="6f268-124">NuGet.org symbol server</span></span>

<span data-ttu-id="6f268-125">NuGet.org 支援自己的符號伺服器存放庫，且只接受新的符號套件格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6f268-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="6f268-126">套件取用者可將 `https://symbols.nuget.org/download/symbols` 新增至其在 Visual Studio 中的符號來源，使用發佈至 nuget.org 符號伺服器的符號，如此即可在 Visual Studio 偵錯工具中，介入套件程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f268-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="6f268-127">如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)。</span><span class="sxs-lookup"><span data-stu-id="6f268-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="6f268-128">Nuget.org 符號套件條件約束</span><span class="sxs-lookup"><span data-stu-id="6f268-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="6f268-129">在 nuget.org 上支援的符號套件，具有以下的條件約束</span><span class="sxs-lookup"><span data-stu-id="6f268-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="6f268-130">只允許將以下副檔名新增至符號套件。</span><span class="sxs-lookup"><span data-stu-id="6f268-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="6f268-131">目前在 nuget 符號伺服器上，只支援受控[可攜式 PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。</span><span class="sxs-lookup"><span data-stu-id="6f268-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="6f268-132">PDB 與相關聯的 nupkg dll，必須以 Visual Studio 15.9 版或更高版本中的編譯器建置 (請參閱 [pdb 加密雜湊](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="6f268-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="6f268-133">若 .snupkg 中包含任何其他檔案類型，則在 nuget.org 上進行符號套件發佈將會失敗。</span><span class="sxs-lookup"><span data-stu-id="6f268-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="6f268-134">符號套件的驗證與製作索引</span><span class="sxs-lookup"><span data-stu-id="6f268-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="6f268-135">發佈至 [NuGet.org](https://www.nuget.org/) 的符號套件，會經過多道驗證，例如病毒檢查。</span><span class="sxs-lookup"><span data-stu-id="6f268-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="6f268-136">當套件通過所有驗證檢查，符號可能需要花費一些時間才可製作索引，以及從 NuGet.org 符號伺服器取用。</span><span class="sxs-lookup"><span data-stu-id="6f268-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="6f268-137">若套件無法通過驗證檢查，.nupkg 的套件詳細資料頁面將會更新，並會顯示出相關錯誤，而您也會收到相關的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="6f268-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="6f268-138">套件驗證和編製索引通常在 15 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="6f268-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="6f268-139">如果套件發佈所需的時間超出預期，請前往 [status.nuget.org](https://status.nuget.org/)，以檢查 nuget.org 是否發生任何中斷。</span><span class="sxs-lookup"><span data-stu-id="6f268-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="6f268-140">若所有系統皆可運作，但套件未在一小時內成功發佈，請登入 nuget.org 並使用套件詳細資料頁面上的聯絡支援連結，連絡我們。</span><span class="sxs-lookup"><span data-stu-id="6f268-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="6f268-141">符號套件結構</span><span class="sxs-lookup"><span data-stu-id="6f268-141">Symbol package structure</span></span>

<span data-ttu-id="6f268-142">.nupkg 檔案將保持不變，但 .snupkg 檔案會有如下特性：</span><span class="sxs-lookup"><span data-stu-id="6f268-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="6f268-143">.snupkg 會與相對應的 .nupkg 有相同的識別碼與版本。</span><span class="sxs-lookup"><span data-stu-id="6f268-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="6f268-144">.snupkg 會與所有具差異性的 DLL 或 EXE 檔案之 nupkg，有完全相同的資料夾結構，而不會和相同資料夾階層內包含其相對應 PDB 的 DLL/EXE 相同。</span><span class="sxs-lookup"><span data-stu-id="6f268-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="6f268-145">含有非 PDB 延伸模組的檔案與資料夾，將會排除在 snupkg 之外。</span><span class="sxs-lookup"><span data-stu-id="6f268-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="6f268-146">.snupkg 中的 .nuspec 檔案，也會指定新的 PackageType，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6f268-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="6f268-147">其應為唯一指定的 PackageType。</span><span class="sxs-lookup"><span data-stu-id="6f268-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="6f268-148">如果作者決定使用自訂 nuspec 來建置他們的 nupkg 和 snupkg，snupkg 應會有相同的資料夾階層與檔案，詳細資料位於 2)。</span><span class="sxs-lookup"><span data-stu-id="6f268-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="6f268-149">```authors``` 與 ```owners``` 欄位將會從 snupkg 的 nuspec 中排除。</span><span class="sxs-lookup"><span data-stu-id="6f268-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="6f268-150">請參閱</span><span class="sxs-lookup"><span data-stu-id="6f268-150">See Also</span></span>

[<span data-ttu-id="6f268-151">NuGet-Package-Debugging-&-Symbols-Improvements</span><span class="sxs-lookup"><span data-stu-id="6f268-151">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
