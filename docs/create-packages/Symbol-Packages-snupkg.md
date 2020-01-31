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
ms.openlocfilehash: 0109aea95ec255b3e0abcdff4cf51b4bfeafbb8c
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813477"
---
# <a name="creating-symbol-packages-snupkg"></a>建立符號套件 (snupkg)

符號套件可讓您改進對 NuGet 套件的偵錯體驗。

## <a name="prerequisites"></a>必要條件：

[nuget.exe 第 4.9.0 版或更高版本](https://www.nuget.org/downloads)或是 [dotnet.exe 第 2.2.0 版或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，其實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>建立符號套件

如果您使用的是 dotnet 或 MSBuild，則除了 nupkg 檔案之外，您還需要設定 `IncludeSymbols` 和 `SymbolPackageFormat` 屬性來建立 .snupkg 檔案。

* 請將下列屬性新增至 .csproj 檔案：

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* 或在命令列上指定這些屬性：

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

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 屬性可有以下兩個值的其中一個：`symbols.nupkg` (預設值) 或 `snupkg`。 如果未指定此屬性，則會建立舊版符號套件。

> [!Note]
> 目前仍然支援舊版格式 `.symbols.nupkg`，只是為達到相容性而已 (請參閱[舊版符號套件](Symbol-Packages.md))。 NuGet.org 的符號伺服器只接受新的符號套件格式 - `.snupkg`。

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

NuGet.org 具有下列符號套件的條件約束：

- 符號套件中只允許下列副檔名： `.pdb`、`.nuspec`、`.xml`、`.psmdcp`、`.rels`、`.p7s`
- NuGet. 組織的符號伺服器上僅支援受管理的[可移植 pdb](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) 。
- Pdb 及其相關聯的. nupkg Dll 必須以 Visual Studio 15.9 版或更新版本中的編譯器建立（請參閱[PDB 加密雜湊](https://github.com/dotnet/roslyn/issues/24429)）

如果不符合這些條件約束，發行至 NuGet.org 的符號套件將無法通過驗證。 

### <a name="symbol-package-validation-and-indexing"></a>符號套件的驗證與製作索引

發佈至[NuGet.org](https://www.nuget.org/)的符號套件會經歷數個驗證，包括惡意程式碼掃描。 如果封裝無法通過驗證檢查，其 [套件詳細資料] 頁面將會顯示錯誤訊息。 此外，套件的擁有者會收到一封電子郵件，其中包含如何修正已識別問題的指示。

當符號套件通過所有驗證時，這些符號會由 NuGet. 組織的符號伺服器編制索引。 索引之後，就可以從 NuGet.org 符號伺服器取用符號。

套件驗證和編製索引通常在 15 分鐘內完成。 如果套件發行所需的時間超出預期，請前往[status.nuget.org](https://status.nuget.org/)，以檢查 NuGet.org 是否發生任何中斷。 若所有系統皆可運作，但套件未在一小時內成功發佈，請登入 nuget.org 並使用套件詳細資料頁面上的聯絡支援連結，連絡我們。

## <a name="symbol-package-structure"></a>符號套件結構

.nupkg 檔案將保持不變，但 .snupkg 檔案會有如下特性：

1) .snupkg 會與相對應的 .nupkg 有相同的識別碼與版本。
2) .snupkg 會與所有具差異性的 DLL 或 EXE 檔案之 nupkg，有完全相同的資料夾結構，而不會和相同資料夾階層內包含其相對應 PDB 的 DLL/EXE 相同。 含有非 PDB 延伸模組的檔案與資料夾，將會排除在 snupkg 之外。
3) .snupkg 中的 .nuspec 檔案，也會指定新的 PackageType，如下所示。 其應為唯一指定的 PackageType。

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 如果作者決定使用自訂 nuspec 來建置他們的 nupkg 和 snupkg，snupkg 應會有相同的資料夾階層與檔案，詳細資料位於 2)。
5) 下欄欄位將會從 .snupkg 的 nuspec 中排除： ```authors```、```owners```、```requireLicenseAcceptance```、```license type```、```licenseUrl```和 ```icon```。
6) 請勿使用 ```<license>``` 元素。 .snupkg 的授權涵蓋範圍與對應的 .nupkg 相同。

## <a name="see-also"></a>請參閱

請考慮使用來源連結來啟用 .NET 元件的原始程式碼偵錯工具。 如需詳細資訊，請參閱[來源連結指引](/dotnet/standard/library-guidance/sourcelink)。

如需符號套件的詳細資訊，請參閱[NuGet 套件的偵錯工具 & 符號改進](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)設計規格。
