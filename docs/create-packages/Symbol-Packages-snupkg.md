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
ms.openlocfilehash: 43f346dc64ebbc59d02b9c7875b04205d8c5d83a
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852438"
---
# <a name="creating-symbol-packages-snupkg"></a>建立符號套件 (snupkg)

符號套件可讓您改進對 NuGet 套件的偵錯體驗。

## <a name="prerequisites"></a>先決條件

[nuget.exe 第 4.9.0 版或更高版本](https://www.nuget.org/downloads)或是 [dotnet.exe 第 2.2.0 版或更高版本](https://www.microsoft.com/net/download/dotnet-core/2.2)，其實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。

## <a name="creating-a-symbol-package"></a>建立符號套件

您可以使用 dotnet.exe、NuGet.exe 或 MSBuild 建立 snupkg 符號套件。 若使用 NuGet.exe，則除了.nupkg 檔案之外，您還可以使用下列命令來建立 .snupkg 檔案：

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

若使用 dotnet.exe 或 MSBuild，則除了.nupkg 檔案之外，您還可以使用下列步驟來建立 .snupkg 檔案：

1. 新增下列屬性到您的 .csproj 檔案：

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. 使用 `dotnet pack MyPackage.csproj` 或 `msbuild -t:pack MyPackage.csproj` 封裝您的專案。

`SymbolPackageFormat` 屬性可有以下兩個值的其中一個：`symbols.nupkg` (預設值) 或 `snupkg`。 若未指定 `SymbolPackageFormat`，它會預設為 `symbols.nupkg`，且會建立舊版符號套件。

> [!Note]
> 目前仍然支援舊版格式 `.symbols.nupkg`，只是為達到相容性而已 (請參閱[舊版符號套件](Symbol-Packages.md))。 NuGet.org 符號伺服器只接受新的符號套件格式 - `.snupkg`。

## <a name="publishing-a-symbol-package"></a>發行符號套件

1. 為方便起見，請先使用 NuGet 儲存您的 API 金鑰 (請參閱[發佈套件](../create-packages/publish-a-package.md))。

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

## <a name="nugetorg-symbol-server"></a>NuGet.org 符號伺服器

NuGet.org 支援自己的符號伺服器存放庫，且只接受新的符號套件格式 - `.snupkg`。 套件取用者可將 `https://symbols.nuget.org/download/symbols` 新增至其在 Visual Studio 中的符號來源，使用發佈至 nuget.org 符號伺服器的符號，如此即可在 Visual Studio 偵錯工具中，介入套件程式碼。 如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)。

### <a name="nugetorg-symbol-package-constraints"></a>Nuget.org 符號套件條件約束

在 nuget.org 上支援的符號套件，具有以下的條件約束

- 只允許將以下副檔名新增至符號套件。 ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- 目前在 nuget 符號伺服器上，只支援受控[可攜式 PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)。
- PDB 與相關聯的 nupkg dll，必須以 Visual Studio 15.9 版或更高版本中的編譯器建置 (請參閱 [pdb 加密雜湊](https://github.com/dotnet/roslyn/issues/24429))

若 .snupkg 中包含任何其他檔案類型，則在 nuget.org 上進行符號套件發佈將會失敗。

### <a name="symbol-package-validation-and-indexing"></a>符號套件的驗證與製作索引

發佈至 [NuGet.org](https://www.nuget.org/) 的符號套件，會經過多道驗證，例如病毒檢查。

當套件通過所有驗證檢查，符號可能需要花費一些時間才可製作索引，以及從 NuGet.org 符號伺服器取用。 若套件無法通過驗證檢查，.nupkg 的套件詳細資料頁面將會更新，並會顯示出相關錯誤，而您也會收到相關的電子郵件通知。

套件驗證和編製索引通常在 15 分鐘內完成。 如果套件發佈所需的時間超出預期，請前往 [status.nuget.org](https://status.nuget.org/)，以檢查 nuget.org 是否發生任何中斷。 若所有系統皆可運作，但套件未在一小時內成功發佈，請登入 nuget.org 並使用套件詳細資料頁面上的聯絡支援連結，連絡我們。

## <a name="symbol-package-structure"></a>符號套件結構

.nupkg 檔案將保持不變，但 .snupkg 檔案會有如下特性：

1) .snupkg 會與相對應的 .nupkg 有相同的識別碼與版本。
2) .snupkg 會與所有具差異性的 DLL 或 EXE 檔案之 nupkg，有完全相同的資料夾結構，而不會和相同資料夾階層內包含其相對應 PDB 的 DLL/EXE 相同。 含有非 PDB 延伸模組的檔案與資料夾，將會排除在 snupkg 之外。
3) .snupkg 中的 .nuspec 檔案，也會指定新的 PackageType，如下所示。 其應為唯一指定的 PackageType。 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) 如果作者決定使用自訂 nuspec 來建置他們的 nupkg 和 snupkg，snupkg 應會有相同的資料夾階層與檔案，詳細資料位於 2)。
5) ```authors``` 與 ```owners``` 欄位將會從 snupkg 的 nuspec 中排除。

## <a name="see-also"></a>請參閱

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
