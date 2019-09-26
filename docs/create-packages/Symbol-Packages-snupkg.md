---
title: 如何使用新的符號套件格式 '.snupkg' 發行 NuGet 符號套件 | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
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
ms.openlocfilehash: 0197902e4dbc18893d68833fbcfe4263f185a594
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307191"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="6423a-104">建立符號套件 (snupkg)</span><span class="sxs-lookup"><span data-stu-id="6423a-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="6423a-105">符號套件可讓您改進對 NuGet 套件的偵錯體驗。</span><span class="sxs-lookup"><span data-stu-id="6423a-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6423a-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="6423a-106">Prerequisites</span></span>

<span data-ttu-id="6423a-107">[nuget.exe 第 4.9.0 版或更高版本](https://www.nuget.org/downloads)或是 [dotnet.exe 第 2.2.0 版或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，其實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="6423a-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="6423a-108">建立符號套件</span><span class="sxs-lookup"><span data-stu-id="6423a-108">Creating a symbol package</span></span>

<span data-ttu-id="6423a-109">如果您使用的是 dotnet 或 MSBuild，則除了 nupkg 檔案之外， `IncludeSymbols`您`SymbolPackageFormat`還需要設定和屬性來建立 .snupkg 檔案。</span><span class="sxs-lookup"><span data-stu-id="6423a-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="6423a-110">請將下列屬性新增至 .csproj 檔案：</span><span class="sxs-lookup"><span data-stu-id="6423a-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="6423a-111">或在命令列上指定這些屬性：</span><span class="sxs-lookup"><span data-stu-id="6423a-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="6423a-112">或</span><span class="sxs-lookup"><span data-stu-id="6423a-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="6423a-113">若使用 NuGet.exe，則除了.nupkg 檔案之外，您還可以使用下列命令來建立 .snupkg 檔案：</span><span class="sxs-lookup"><span data-stu-id="6423a-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="6423a-114">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 屬性可有以下兩個值的其中一個：`symbols.nupkg` (預設值) 或 `snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6423a-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="6423a-115">如果未指定此屬性，則會建立舊版符號套件。</span><span class="sxs-lookup"><span data-stu-id="6423a-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="6423a-116">目前仍然支援舊版格式 `.symbols.nupkg`，只是為達到相容性而已 (請參閱[舊版符號套件](Symbol-Packages.md))。</span><span class="sxs-lookup"><span data-stu-id="6423a-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="6423a-117">NuGet.org 的符號伺服器只接受新的符號套件格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6423a-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="6423a-118">發行符號套件</span><span class="sxs-lookup"><span data-stu-id="6423a-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="6423a-119">為方便起見，請先使用 NuGet 儲存您的 API 金鑰 (請參閱[發佈套件](../nuget-org/publish-a-package.md))。</span><span class="sxs-lookup"><span data-stu-id="6423a-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="6423a-120">將主要套件發佈至 nuget.org 後，接著推送符號套件。</span><span class="sxs-lookup"><span data-stu-id="6423a-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="6423a-121">您也可以使用以下命令，同時推送主要套件與符號套件。</span><span class="sxs-lookup"><span data-stu-id="6423a-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="6423a-122">.nupkg 與 .snupkg 檔案都必須出現在目前的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6423a-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="6423a-123">NuGet 會將兩個套件發行到 nuget.org。將會先發行 `MyPackage.nupkg`，再發行 `MyPackage.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6423a-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="6423a-124">若符號套件未發行，請檢查您是否已將 NuGet.org 來源設定為 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="6423a-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="6423a-125">只有 [NuGet V3 API](../api/overview.md#versioning) 才支援符號套件發行。</span><span class="sxs-lookup"><span data-stu-id="6423a-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="6423a-126">NuGet.org 符號伺服器</span><span class="sxs-lookup"><span data-stu-id="6423a-126">NuGet.org symbol server</span></span>

<span data-ttu-id="6423a-127">NuGet.org 支援自己的符號伺服器存放庫，且只接受新的符號套件格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="6423a-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="6423a-128">套件取用者可將 `https://symbols.nuget.org/download/symbols` 新增至其在 Visual Studio 中的符號來源，使用發佈至 nuget.org 符號伺服器的符號，如此即可在 Visual Studio 偵錯工具中，介入套件程式碼。</span><span class="sxs-lookup"><span data-stu-id="6423a-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="6423a-129">如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="6423a-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="6423a-130">NuGet.org 符號套件條件約束</span><span class="sxs-lookup"><span data-stu-id="6423a-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="6423a-131">NuGet.org 具有下列符號套件的條件約束：</span><span class="sxs-lookup"><span data-stu-id="6423a-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="6423a-132">符號套件中只允許下列副檔名： `.pdb`、 `.nuspec`、 `.xml`、 `.psmdcp`、 `.rels`、`.p7s`</span><span class="sxs-lookup"><span data-stu-id="6423a-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="6423a-133">NuGet. 組織的符號伺服器上僅支援受管理的[可移植 pdb](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) 。</span><span class="sxs-lookup"><span data-stu-id="6423a-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="6423a-134">Pdb 及其相關聯的. nupkg Dll 必須以 Visual Studio 15.9 版或更新版本中的編譯器建立（請參閱[PDB 加密雜湊](https://github.com/dotnet/roslyn/issues/24429)）</span><span class="sxs-lookup"><span data-stu-id="6423a-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="6423a-135">如果不符合這些條件約束，發行至 NuGet.org 的符號套件將無法通過驗證。</span><span class="sxs-lookup"><span data-stu-id="6423a-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="6423a-136">符號套件的驗證與製作索引</span><span class="sxs-lookup"><span data-stu-id="6423a-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="6423a-137">發佈至[NuGet.org](https://www.nuget.org/)的符號套件會經歷數個驗證，包括惡意程式碼掃描。</span><span class="sxs-lookup"><span data-stu-id="6423a-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="6423a-138">如果封裝無法通過驗證檢查，其 [套件詳細資料] 頁面將會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6423a-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="6423a-139">此外，套件的擁有者會收到一封電子郵件，其中包含如何修正已識別問題的指示。</span><span class="sxs-lookup"><span data-stu-id="6423a-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="6423a-140">當符號套件通過所有驗證時，這些符號會由 NuGet. 組織的符號伺服器編制索引。</span><span class="sxs-lookup"><span data-stu-id="6423a-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="6423a-141">索引之後，就可以從 NuGet.org 符號伺服器取用符號。</span><span class="sxs-lookup"><span data-stu-id="6423a-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="6423a-142">套件驗證和編製索引通常在 15 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="6423a-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="6423a-143">如果套件發行所需的時間超出預期，請前往[status.nuget.org](https://status.nuget.org/)，以檢查 NuGet.org 是否發生任何中斷。</span><span class="sxs-lookup"><span data-stu-id="6423a-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="6423a-144">若所有系統皆可運作，但套件未在一小時內成功發佈，請登入 nuget.org 並使用套件詳細資料頁面上的聯絡支援連結，連絡我們。</span><span class="sxs-lookup"><span data-stu-id="6423a-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="6423a-145">符號套件結構</span><span class="sxs-lookup"><span data-stu-id="6423a-145">Symbol package structure</span></span>

<span data-ttu-id="6423a-146">.nupkg 檔案將保持不變，但 .snupkg 檔案會有如下特性：</span><span class="sxs-lookup"><span data-stu-id="6423a-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="6423a-147">.snupkg 會與相對應的 .nupkg 有相同的識別碼與版本。</span><span class="sxs-lookup"><span data-stu-id="6423a-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="6423a-148">.snupkg 會與所有具差異性的 DLL 或 EXE 檔案之 nupkg，有完全相同的資料夾結構，而不會和相同資料夾階層內包含其相對應 PDB 的 DLL/EXE 相同。</span><span class="sxs-lookup"><span data-stu-id="6423a-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="6423a-149">含有非 PDB 延伸模組的檔案與資料夾，將會排除在 snupkg 之外。</span><span class="sxs-lookup"><span data-stu-id="6423a-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="6423a-150">.snupkg 中的 .nuspec 檔案，也會指定新的 PackageType，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6423a-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="6423a-151">其應為唯一指定的 PackageType。</span><span class="sxs-lookup"><span data-stu-id="6423a-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="6423a-152">如果作者決定使用自訂 nuspec 來建置他們的 nupkg 和 snupkg，snupkg 應會有相同的資料夾階層與檔案，詳細資料位於 2)。</span><span class="sxs-lookup"><span data-stu-id="6423a-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="6423a-153">```authors``` 與 ```owners``` 欄位將會從 snupkg 的 nuspec 中排除。</span><span class="sxs-lookup"><span data-stu-id="6423a-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="6423a-154">請勿使用 ```<license>``` 元素。</span><span class="sxs-lookup"><span data-stu-id="6423a-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="6423a-155">.snupkg 的授權涵蓋範圍與對應的 .nupkg 相同。</span><span class="sxs-lookup"><span data-stu-id="6423a-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="6423a-156">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6423a-156">See Also</span></span>

<span data-ttu-id="6423a-157">請考慮使用來源連結來啟用 .NET 元件的原始程式碼偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="6423a-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="6423a-158">如需詳細資訊，請參閱[來源連結指引](/dotnet/standard/library-guidance/sourcelink)。</span><span class="sxs-lookup"><span data-stu-id="6423a-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="6423a-159">如需符號套件的詳細資訊，請參閱[NuGet 套件的偵錯工具 & 符號改進](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)設計規格。</span><span class="sxs-lookup"><span data-stu-id="6423a-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
