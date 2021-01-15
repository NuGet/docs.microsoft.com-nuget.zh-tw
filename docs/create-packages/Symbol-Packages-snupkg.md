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
ms.openlocfilehash: fbcc035a6b800617f995d3bcebd7e1764aa467b0
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235720"
---
# <a name="creating-symbol-packages-snupkg"></a>建立符號套件 (snupkg)

良好的調試經驗會依賴 debug 符號的存在，因為它們提供了重要的資訊，例如已編譯和原始程式碼之間的關聯、區域變數的名稱、堆疊追蹤等等。 您可以使用符號套件 (. .snupkg) 來散發這些符號，並改善 NuGet 套件的偵錯工具體驗。

## <a name="prerequisites"></a>必要條件

[nuget.exe v 4.9.0 或](https://www.nuget.org/downloads) 更新版本，或 [dotnet CLI v 2.2.0 或](https://www.microsoft.com/net/download/dotnet-core/2.2)更新版本，其會執行必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>建立符號套件

如果您使用的是 dotnet CLI 或 MSBuild，除了 nupkg 檔案之外，您還需要設定 `IncludeSymbols` 和 `SymbolPackageFormat` 屬性來建立 .snupkg 檔案。

* 請將下列屬性新增至 .csproj 檔案：

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* 或者，在命令列上指定這些屬性：

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  或

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

若使用 NuGet.exe，則除了.nupkg 檔案之外，您還可以使用下列命令來建立 .snupkg 檔案：

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)屬性可以有兩個值的其中一個： `symbols.nupkg` (預設) 或 `snupkg` 。 如果未指定此屬性，則會建立舊版符號套件。

> [!Note]
> 仍支援舊版格式， `.symbols.nupkg` 但僅基於原生封裝的相容性原因 (查看 [舊版符號套件](Symbol-Packages.md)) 。 NuGet.org 的符號伺服器只接受新的符號套件格式 - `.snupkg`。

## <a name="publishing-a-symbol-package"></a>發行符號套件

1. 為方便起見，請先使用 NuGet 儲存您的 API 金鑰 (請參閱[發佈套件](../nuget-org/publish-a-package.md))。

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. 將主要套件發佈至 nuget.org 後，接著推送符號套件。

    ```cli
    nuget push MyPackage.snupkg
    ```

1. 您也可以使用以下命令，同時推送主要套件與符號套件。 .nupkg 與 .snupkg 檔案都必須出現在目前的資料夾中。

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet 會將兩個套件發行到 nuget.org。將會先發行 `MyPackage.nupkg`，再發行 `MyPackage.snupkg`。

> [!Note]
> 若符號套件未發行，請檢查您是否已將 NuGet.org 來源設定為 `https://api.nuget.org/v3/index.json`。 只有 [NuGet V3 API](../api/overview.md#versioning) 才支援符號套件發行。

## <a name="nugetorg-symbol-server"></a>NuGet.org 符號伺服器

NuGet.org 支援自己的符號伺服器存放庫，且只接受新的符號套件格式 - `.snupkg`。 套件取用者可將 `https://symbols.nuget.org/download/symbols` 新增至其在 Visual Studio 中的符號來源，使用發佈至 nuget.org 符號伺服器的符號，如此即可在 Visual Studio 偵錯工具中，介入套件程式碼。 如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org 符號套件條件約束

NuGet.org 對於符號套件具有下列限制：

- 符號套件中只允許下列副檔名： `.pdb` 、 `.nuspec` 、 `.xml` 、 `.psmdcp` 、 `.rels` 、 `.p7s`
- 在 NuGet. org 的符號伺服器上僅支援受管理的 [便攜 pdb](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) 。
- 在 Visual Studio 15.9 版或更新版本中，必須使用編譯器建立 Pdb 和其相關聯的 nupkg Dll (請參閱 [PDB 加密雜湊](https://github.com/dotnet/roslyn/issues/24429)) 

如果不符合這些條件約束，發佈至 NuGet.org 的符號套件將無法通過驗證。 

> [!NOTE]
> 原生專案（例如 c + + 專案）會產生 Windows Pdb，而不是可移植 Pdb。 這些不受 NuGet. org 的符號伺服器支援。 請改用 [舊版符號套件](Symbol-Packages.md) 。

### <a name="symbol-package-validation-and-indexing"></a>符號套件的驗證與製作索引

發佈至 [NuGet.org](https://www.nuget.org/) 的符號套件會進行數個驗證，包括惡意程式碼掃描。 如果封裝無法通過驗證檢查，其 [套件詳細資料] 頁面將會顯示錯誤訊息。 此外，套件的擁有者會收到一封電子郵件，其中包含如何修正已識別問題的指示。

當符號套件通過所有驗證之後，將會以 NuGet. org 的符號伺服器來編制符號的索引，而且將可供取用。

套件驗證和編製索引通常在 15 分鐘內完成。 如果封裝發佈花費的時間超出預期，請造訪 [status.nuget.org](https://status.nuget.org/) 來檢查 NuGet.org 是否遇到任何中斷。 若所有系統皆可運作，但套件未在一小時內成功發佈，請登入 nuget.org 並使用套件詳細資料頁面上的聯絡支援連結，連絡我們。

## <a name="symbol-package-structure"></a>符號套件結構

符號套件 ( .snupkg) 具有下列特性：

1) .Snupkg 的識別碼和版本與對應的 NuGet 套件 ( nupkg) 相同。
2) .Snupkg 與任何 DLL 或 EXE 檔案的對應 nupkg 具有相同的資料夾結構，而不是 Dll/Exe，其對應的 Pdb 將會包含在相同的資料夾階層中。 含有非 PDB 延伸模組的檔案與資料夾，將會排除在 snupkg 之外。
3) 符號套件的 nuspec 檔案具有 `SymbolsPackage` 套件類型：

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 如果作者決定使用自訂 nuspec 來建置他們的 nupkg 和 snupkg，snupkg 應會有相同的資料夾階層與檔案，詳細資料位於 2)。
5) 下欄欄位將從 .snupkg 的 nuspec 中排除： ```authors``` 、 ```owners``` 、 ```requireLicenseAcceptance``` 、 ```license type``` 、 ```licenseUrl``` 和  ```icon``` 。
6) 請勿使用 ```<license>``` 元素。 .snupkg 的授權涵蓋範圍與對應的 .nupkg 相同。

## <a name="see-also"></a>另請參閱

請考慮使用來源連結來啟用 .NET 元件的原始程式碼偵錯工具。 如需詳細資訊，請參閱 [來源連結指引](/dotnet/standard/library-guidance/sourcelink)。

如需符號套件的詳細資訊，請參閱 [NuGet 套件偵錯工具 & 符號增強](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) 設計規格。
