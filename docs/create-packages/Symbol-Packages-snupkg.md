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
# <a name="creating-symbol-packages-snupkg"></a>建立符號套件 (snupkg)

良好的調試體驗依賴於調試符號的存在,因為它們提供關鍵資訊,如編譯和原始程式碼之間的關聯、本地變數的名稱、堆疊跟蹤等。 您可以使用符號包 (.snupkg) 來分發這些符號並改進 NuGet 包的調試體驗。

## <a name="prerequisites"></a>Prerequisites

[nuget.exe v4.9.0 或以上](https://www.nuget.org/downloads)或[點網 CLI v2.2.0 或以上](https://www.microsoft.com/net/download/dotnet-core/2.2),它們實現所需的[NuGet 協定](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>建立符號套件

如果使用 dotnet CLI 或 MSBuild,則需要設定`IncludeSymbols`和`SymbolPackageFormat`屬性以創建 .snupkg 檔以及 .nupkg 檔。

* 將以下屬性加入 .csproj 檔:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* 或在命令列上指定這些屬性:

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

屬性[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)可以具有兩個值之一`symbols.nupkg`( 預設值`snupkg`) 或 。 如果未指定此屬性,將創建舊符號包。

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

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org 符號包限制

NuGet.org符號套件具有以下規範:

- 符號`.pdb`套件中只允許以下檔案副檔名`.nuspec`: `.xml` `.psmdcp` `.rels`、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、 、`.p7s`
- NuGet.org的符號伺服器上僅支援託管[便攜式 PDB。](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)
- PDB 及其關聯的 .nupkg DLL 需要與 Visual Studio 版本 15.9 或以上版本的編譯器一起構建(請參閱[PDB 加密哈希](https://github.com/dotnet/roslyn/issues/24429))

如果不滿足這些限制,發佈到NuGet.org的符號包將失敗驗證。 

### <a name="symbol-package-validation-and-indexing"></a>符號套件的驗證與製作索引

發佈到[NuGet.org](https://www.nuget.org/)的符號包要經過多次驗證,包括惡意軟體掃描。 如果包未通過驗證檢查,其包詳細資訊頁將顯示一條錯誤消息。 此外,包的所有者將收到一封電子郵件,其中包含有關如何修復已識別問題的說明。

當符號包通過所有驗證后,符號將由 NuGet.org的符號伺服器編制索引,並可供使用。

套件驗證和編製索引通常在 15 分鐘內完成。 如果包發佈時間比預期長,請造[訪status.nuget.org](https://status.nuget.org/)檢查NuGet.org是否遇到任何中斷。 若所有系統皆可運作，但套件未在一小時內成功發佈，請登入 nuget.org 並使用套件詳細資料頁面上的聯絡支援連結，連絡我們。

## <a name="symbol-package-structure"></a>符號套件結構

符號包 (.snupkg) 具有以下特徵:

1) .snupkg 的 ID 和版本與其相應的 NuGet 包 (.nupkg) 相同。
2) .snupkg 具有與其對應的 .nupkg 相同的資料夾結構,適用於任何 DLL 或 EXE 檔,其區別是,其相應的 PB 將包含在相同的資料夾層次結構中,而不是 DLL/EXE。 含有非 PDB 延伸模組的檔案與資料夾，將會排除在 snupkg 之外。
3) 符號套件的 .nuspec`SymbolsPackage`檔案具有 套件類型:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 如果作者決定使用自訂 nuspec 來建置他們的 nupkg 和 snupkg，snupkg 應會有相同的資料夾階層與檔案，詳細資料位於 2)。
5) 以下欄位將排除在 snupkg 的 nuspec ```requireLicenseAcceptance``` ```license type``````licenseUrl```中```icon```: ```authors``` ```owners```、 、 、 , , 和 。
6) 請勿使用 ```<license>``` 元素。 .snupkg 的授權涵蓋範圍與對應的 .nupkg 相同。

## <a name="see-also"></a>另請參閱

請考慮使用源連結啟用 .NET 程式集的原始程式碼偵錯。 有關詳細資訊,請參閱[源連結指南](/dotnet/standard/library-guidance/sourcelink)。

有關符號包的詳細資訊,請參閱[NuGet 包調試&符號改進](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)設計規範。
