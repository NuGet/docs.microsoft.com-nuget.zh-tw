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
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>建立舊版符號套件（. 符號. nupkg）

> [!Important]
> 為符號套件新建議的格式為 .snupkg。 請參閱[建立符號套件 (.snupkg)](Symbol-Packages-snupkg.md)。 </br>
> 目前仍然支援 .symbols.nupkg，只是為達到相容性而已。

除了建立 nuget.org 或其他來源的套件之外，NuGet 也支援建立可發行至符號伺服器的相關符號套件。 舊版符號套件格式 nupkg 可推送至 SymbolSource 存放庫。

套件取用者接著可以在 Visual Studio 中將 `https://nuget.smbsrc.net` 新增至其符號來源，以允許在 Visual Studio 偵錯工具中逐步執行套件程式碼。 如需該程序的詳細資料，請參閱[在 Visual Studio Debugger 中指定符號 (.pdb) 和原始程式檔](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。

## <a name="creating-a-legacy-symbol-package"></a>建立舊版符號套件

若要建立舊版符號套件，請遵循下列慣例：

- 將主要套件 (含您的程式碼) 命名為 `{identifier}.nupkg`，並包含 `.pdb` 檔案以外的所有檔案。
- 將舊版符號套件命名為 `{identifier}.symbols.nupkg` 並包含您的元件 DLL、`.pdb` 檔案、XMLDOC 檔、原始程式檔（請參閱下列各節）。

您可以使用 `-Symbols` 選項，從 `.nuspec` 檔案或專案檔建立兩個套件：

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。 在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。

## <a name="legacy-symbol-package-structure"></a>舊版符號套件結構

舊版符號套件可以用與程式庫封裝相同的方式，以多個目標 framework 為目標，因此 `lib` 資料夾的結構應該與主要封裝完全相同，只包括與 DLL `.pdb` 的檔案。

例如，以 .NET 4.0 和 Silverlight 4 為目標的舊版符號套件會有此配置：

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

原始程式檔接著會放在名為 `src` 的個別特殊資料夾中，而此資料夾必須遵循來源存放庫的相對結構。 這是因為 PDB 包含用來編譯相符 DLL 之原始程式檔的絕對路徑，而且需要在發行程序期間找到它們。 可以去除基底路徑（一般路徑前置詞）。例如，假設有一個從這些檔案建立的程式庫：

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

除了 [`lib`] 資料夾之外，舊版符號套件也必須包含此版面配置：

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

## <a name="referring-to-files-in-the-nuspec"></a>參考 nuspec 中的檔案

舊版符號套件可以根據慣例、上一節中所述的資料夾結構，或在資訊清單的 [`files`] 區段中指定其內容來建立。 例如，若要建置上節所示的套件，請在 `.nuspec` 檔案中使用下列內容：

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>發行舊版符號套件

> [!Important]
> 若要將套件推送到 nuget.org，您必須使用 [nuget.exe v4.9.1 或更新版本](https://www.nuget.org/downloads)，它會實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。

1. 為了方便起見，請先使用 NuGet 儲存 API 金鑰 (請參閱[發行套件](../nuget-org/publish-a-package.md)，這適用於 nuget.org 和 symbolsource.org，因為 symbolsource.org 將向 nuget.org 確認，確認您是套件擁有者。

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. 將主要套件發佈至 nuget.org 之後，推送舊版符號套件，如下所示，這會因為檔案名中的 `.symbols` 而自動使用 symbolsource.org 做為目標：

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. 若要發行至不同的符號存放庫，或推送未遵循命名慣例的舊版符號套件，請使用 `-Source` 選項：

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. 您也可以使用下列項目，同時將主要和符號套件推送至兩個存放庫：

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > 使用 nuget.exe 4.5.0 或更高版本時，不會將符號套件自動推送至 symbolsource.org。您需要個別推送符號套件，如先前步驟中所述。
   
在此情況下，NuGet 將主要套件發行至 nuget.org 之後，會將 `MyPackage.symbols.nupkg` (存在時) 發行至 https://nuget.smbsrc.net/ (symbolsource.org 的推送 URL)。

## <a name="see-also"></a>另請參閱

* [建立符號套件（. .snupkg）](Symbol-Packages-snupkg.md) -符號套件的新建議格式
* [移至新的 SymbolSource 引擎](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
