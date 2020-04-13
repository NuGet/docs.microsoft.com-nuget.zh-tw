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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380414"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="b33b6-104">建立符號套件 (snupkg)</span><span class="sxs-lookup"><span data-stu-id="b33b6-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="b33b6-105">良好的調試體驗依賴於調試符號的存在,因為它們提供關鍵資訊,如編譯和原始程式碼之間的關聯、本地變數的名稱、堆疊跟蹤等。</span><span class="sxs-lookup"><span data-stu-id="b33b6-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="b33b6-106">您可以使用符號包 (.snupkg) 來分發這些符號並改進 NuGet 包的調試體驗。</span><span class="sxs-lookup"><span data-stu-id="b33b6-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b33b6-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b33b6-107">Prerequisites</span></span>

<span data-ttu-id="b33b6-108">[nuget.exe v4.9.0 或以上](https://www.nuget.org/downloads)或[點網 CLI v2.2.0 或以上](https://www.microsoft.com/net/download/dotnet-core/2.2),它們實現所需的[NuGet 協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="b33b6-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="b33b6-109">建立符號套件</span><span class="sxs-lookup"><span data-stu-id="b33b6-109">Creating a symbol package</span></span>

<span data-ttu-id="b33b6-110">如果使用 dotnet CLI 或 MSBuild,則需要設定`IncludeSymbols`和`SymbolPackageFormat`屬性以創建 .snupkg 檔以及 .nupkg 檔。</span><span class="sxs-lookup"><span data-stu-id="b33b6-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="b33b6-111">將以下屬性加入 .csproj 檔:</span><span class="sxs-lookup"><span data-stu-id="b33b6-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="b33b6-112">或在命令列上指定這些屬性:</span><span class="sxs-lookup"><span data-stu-id="b33b6-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="b33b6-113">或</span><span class="sxs-lookup"><span data-stu-id="b33b6-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="b33b6-114">若使用 NuGet.exe，則除了.nupkg 檔案之外，您還可以使用下列命令來建立 .snupkg 檔案：</span><span class="sxs-lookup"><span data-stu-id="b33b6-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="b33b6-115">屬性[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)可以具有兩個值之一`symbols.nupkg`( 預設值`snupkg`) 或 。</span><span class="sxs-lookup"><span data-stu-id="b33b6-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="b33b6-116">如果未指定此屬性,將創建舊符號包。</span><span class="sxs-lookup"><span data-stu-id="b33b6-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="b33b6-117">目前仍然支援舊版格式 `.symbols.nupkg`，只是為達到相容性而已 (請參閱[舊版符號套件](Symbol-Packages.md))。</span><span class="sxs-lookup"><span data-stu-id="b33b6-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="b33b6-118">NuGet.org 的符號伺服器只接受新的符號套件格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="b33b6-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="b33b6-119">發行符號套件</span><span class="sxs-lookup"><span data-stu-id="b33b6-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="b33b6-120">為方便起見，請先使用 NuGet 儲存您的 API 金鑰 (請參閱[發佈套件](../nuget-org/publish-a-package.md))。</span><span class="sxs-lookup"><span data-stu-id="b33b6-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="b33b6-121">將主要套件發佈至 nuget.org 後，接著推送符號套件。</span><span class="sxs-lookup"><span data-stu-id="b33b6-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="b33b6-122">您也可以使用以下命令，同時推送主要套件與符號套件。</span><span class="sxs-lookup"><span data-stu-id="b33b6-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="b33b6-123">.nupkg 與 .snupkg 檔案都必須出現在目前的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="b33b6-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="b33b6-124">NuGet 會將兩個套件發行到 nuget.org。將會先發行 `MyPackage.nupkg`，再發行 `MyPackage.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="b33b6-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="b33b6-125">若符號套件未發行，請檢查您是否已將 NuGet.org 來源設定為 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="b33b6-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="b33b6-126">只有 [NuGet V3 API](../api/overview.md#versioning) 才支援符號套件發行。</span><span class="sxs-lookup"><span data-stu-id="b33b6-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="b33b6-127">NuGet.org 符號伺服器</span><span class="sxs-lookup"><span data-stu-id="b33b6-127">NuGet.org symbol server</span></span>

<span data-ttu-id="b33b6-128">NuGet.org 支援自己的符號伺服器存放庫，且只接受新的符號套件格式 - `.snupkg`。</span><span class="sxs-lookup"><span data-stu-id="b33b6-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="b33b6-129">套件取用者可將 `https://symbols.nuget.org/download/symbols` 新增至其在 Visual Studio 中的符號來源，使用發佈至 nuget.org 符號伺服器的符號，如此即可在 Visual Studio 偵錯工具中，介入套件程式碼。</span><span class="sxs-lookup"><span data-stu-id="b33b6-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="b33b6-130">如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。</span><span class="sxs-lookup"><span data-stu-id="b33b6-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="b33b6-131">NuGet.org 符號包限制</span><span class="sxs-lookup"><span data-stu-id="b33b6-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="b33b6-132">NuGet.org符號套件具有以下規範:</span><span class="sxs-lookup"><span data-stu-id="b33b6-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="b33b6-133">符號`.pdb`套件中只允許以下檔案副檔名`.nuspec`: `.xml` `.psmdcp` `.rels`、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、`.p7s`</span><span class="sxs-lookup"><span data-stu-id="b33b6-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="b33b6-134">NuGet.org的符號伺服器上僅支援託管[便攜式 PDB。](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)</span><span class="sxs-lookup"><span data-stu-id="b33b6-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="b33b6-135">PDB 及其關聯的 .nupkg DLL 需要與 Visual Studio 版本 15.9 或以上版本的編譯器一起構建(請參閱[PDB 加密哈希](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="b33b6-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="b33b6-136">如果不滿足這些限制,發佈到NuGet.org的符號包將失敗驗證。</span><span class="sxs-lookup"><span data-stu-id="b33b6-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="b33b6-137">符號套件的驗證與製作索引</span><span class="sxs-lookup"><span data-stu-id="b33b6-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="b33b6-138">發佈到[NuGet.org](https://www.nuget.org/)的符號包要經過多次驗證,包括惡意軟體掃描。</span><span class="sxs-lookup"><span data-stu-id="b33b6-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="b33b6-139">如果包未通過驗證檢查,其包詳細資訊頁將顯示一條錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="b33b6-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="b33b6-140">此外,包的所有者將收到一封電子郵件,其中包含有關如何修復已識別問題的說明。</span><span class="sxs-lookup"><span data-stu-id="b33b6-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="b33b6-141">當符號包通過所有驗證后,符號將由 NuGet.org的符號伺服器編制索引,並可供使用。</span><span class="sxs-lookup"><span data-stu-id="b33b6-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="b33b6-142">套件驗證和編製索引通常在 15 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="b33b6-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="b33b6-143">如果包發佈時間比預期長,請造[訪status.nuget.org](https://status.nuget.org/)檢查NuGet.org是否遇到任何中斷。</span><span class="sxs-lookup"><span data-stu-id="b33b6-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="b33b6-144">若所有系統皆可運作，但套件未在一小時內成功發佈，請登入 nuget.org 並使用套件詳細資料頁面上的聯絡支援連結，連絡我們。</span><span class="sxs-lookup"><span data-stu-id="b33b6-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="b33b6-145">符號套件結構</span><span class="sxs-lookup"><span data-stu-id="b33b6-145">Symbol package structure</span></span>

<span data-ttu-id="b33b6-146">符號包 (.snupkg) 具有以下特徵:</span><span class="sxs-lookup"><span data-stu-id="b33b6-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="b33b6-147">.snupkg 的 ID 和版本與其相應的 NuGet 包 (.nupkg) 相同。</span><span class="sxs-lookup"><span data-stu-id="b33b6-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="b33b6-148">.snupkg 具有與其對應的 .nupkg 相同的資料夾結構,適用於任何 DLL 或 EXE 檔,其區別是,其相應的 PB 將包含在相同的資料夾層次結構中,而不是 DLL/EXE。</span><span class="sxs-lookup"><span data-stu-id="b33b6-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="b33b6-149">含有非 PDB 延伸模組的檔案與資料夾，將會排除在 snupkg 之外。</span><span class="sxs-lookup"><span data-stu-id="b33b6-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="b33b6-150">符號套件的 .nuspec`SymbolsPackage`檔案具有 套件類型:</span><span class="sxs-lookup"><span data-stu-id="b33b6-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="b33b6-151">如果作者決定使用自訂 nuspec 來建置他們的 nupkg 和 snupkg，snupkg 應會有相同的資料夾階層與檔案，詳細資料位於 2)。</span><span class="sxs-lookup"><span data-stu-id="b33b6-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="b33b6-152">以下欄位將排除在 snupkg 的 nuspec ```requireLicenseAcceptance``` ```license type``````licenseUrl```中```icon```: ```authors``` ```owners```、 、 、 , , 和 。</span><span class="sxs-lookup"><span data-stu-id="b33b6-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="b33b6-153">請勿使用 ```<license>``` 元素。</span><span class="sxs-lookup"><span data-stu-id="b33b6-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="b33b6-154">.snupkg 的授權涵蓋範圍與對應的 .nupkg 相同。</span><span class="sxs-lookup"><span data-stu-id="b33b6-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="b33b6-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b33b6-155">See also</span></span>

<span data-ttu-id="b33b6-156">請考慮使用源連結啟用 .NET 程式集的原始程式碼偵錯。</span><span class="sxs-lookup"><span data-stu-id="b33b6-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="b33b6-157">有關詳細資訊,請參閱[源連結指南](/dotnet/standard/library-guidance/sourcelink)。</span><span class="sxs-lookup"><span data-stu-id="b33b6-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="b33b6-158">有關符號包的詳細資訊,請參閱[NuGet 包調試&符號改進](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)設計規範。</span><span class="sxs-lookup"><span data-stu-id="b33b6-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
