---
title: NuGet CLI 套件命令
description: nuget.exe pack 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780041"
---
# <a name="pack-command-nuget-cli"></a> (NuGet CLI 的 pack 命令) 

**適用物件：** 套件建立 &bullet; **支援的版本：** 2.7 +

根據指定的 [nuspec](../nuspec.md) 或專案檔建立 NuGet 套件。 `dotnet pack`命令 (查看[dotnet 命令](../dotnet-Commands.md)) 和 `msbuild -t:pack` (查看[MSBuild 目標](../msbuild-targets.md)) 可作為替代項使用。

> [!Important]
> 使用 [`dotnet pack`](../dotnet-Commands.md) 或 [`msbuild -t:pack`](../msbuild-targets.md) 針對以 [PackageReference](../../consume-packages/package-references-in-project-files.md) 為基礎的專案。
> 在 Mono 下，不支援從專案檔建立套件。 您也需要將檔案中的非本機路徑調整 `.nuspec` 為 Unix 樣式的路徑，因為 nuget.exe 不會轉換 Windows 路徑路徑本身。

## <a name="usage"></a>使用方式

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

where `<nuspecPath>` 和 `<projectPath>` 分別指定 `.nuspec` 或專案檔。

## <a name="options"></a>選項。
- **`-BasePath`**

   設定 [nuspec](../nuspec.md) 檔中定義之檔案的基底路徑。

- **`-Build`**

  指定專案應該在建立封裝之前建立。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-Exclude`**

  指定建立封裝時要排除的一或多個萬用字元模式。 若要指定一個以上的模式，請重複-Exclude 旗標。 請參閱以下的範例。

- **`-ExcludeEmptyDirectories`**

  在建立封裝時防止包含空的目錄。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-IncludeReferencedProjects`**

  表示建立的封裝應該將參考的專案包含為相依性或封裝的一部分。 如果參考的專案具有與專案同名的對應檔案 `.nuspec` ，則會將該參考的專案新增為相依性。 否則，會將參考的專案新增為封裝的一部分。

- **`-InstallPackageToOutputPath`**

  指定命令是否應準備套件輸出目錄，以支援共用作為摘要。

- **`-MinClientVersion`**

  為建立的封裝設定 *minClientVersion* 屬性。 如果檔案中有任何) ，此值會覆寫現有 *minClientVersion* 屬性 (的值 `.nuspec` 。

- **`-MSBuildPath`**

  *(4.0 +)* 指定要搭配命令使用的 MSBuild 路徑，優先順序高於 `-MSBuildVersion` 。

- **`-MSBuildVersion`**

  *(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 依預設，會挑選路徑中的 MSBuild，否則會預設為 MSBuild 的最高安裝版本。

- **`-NoDefaultExcludes`**

  防止預設排除 NuGet 套件檔案，以及以點（例如和）開頭的檔案和 `.svn` 資料夾 `.gitignore` 。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-NoPackageAnalysis`**

  指定封裝不應該在建置套件之後執行套件分析。

- **`-OutputDirectory`**

  指定儲存建立之封裝的資料夾。 如果未指定資料夾，則會使用目前的資料夾。

- **`-OutputFileNamesWithoutVersion`**

  指定命令是否應該在沒有版本的情況下準備套件輸出名稱。

- **`-PackagesDirectory`**

  指定封裝資料夾。

- **`-p|-Properties`**

  在其他選項之後，應該會出現在命令列上。 指定覆寫專案檔中值的屬性清單;請參閱屬性名稱的 [一般 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties) 。 此處的 Properties 引數是 token = 值組的清單（以分號分隔），其中檔案中的每個出現專案 `$token$` `.nuspec` 都會以指定的值取代。 值可以是以引號括住的字串。 請注意，針對 "Configuration" 屬性，預設值為 "Debug"。 若要變更為發行設定，請使用 `-Properties Configuration=Release` 。 **一般而言**，屬性應該與對應的專案組建期間所使用的屬性相同，以避免可能奇怪的行為。

- **`-SolutionDirectory`**

  指定方案目錄。

- **`-Suffix`**

  *(3.4.4 +)* 將尾碼附加至內部產生的版本號碼，通常用於附加組建或其他發行前版本識別碼。 例如，使用 `-suffix nightly` 會建立版本號碼類似的封裝 `1.2.3-nightly` 。 尾碼必須以字母開頭，以避免與不同版本的 NuGet 和 NuGet 封裝管理員的警告、錯誤和潛在不相容。

- **`-SymbolPackageFormat`**

  建立符號封裝時，可讓您選擇 `snupkg` 和 `symbols.nupkg` 格式。

- **`-Symbols`**

  指定封裝包含來源和符號。 搭配檔案使用時 `.nuspec` ，會建立一般的 NuGet 套件檔案和對應的符號套件。 依預設，它會建立 [舊版符號套件](../../create-packages/Symbol-Packages.md)。 為符號套件新建議的格式為 .snupkg。 請參閱[建立符號套件 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。

- **`-Tool`**

   指定專案的輸出檔應放置在 `tool` 資料夾中。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

- **`-Version`**

  覆寫檔案中的版本號碼 `.nuspec` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>排除開發相依性

某些 NuGet 套件相當適合用來作為開發相依性，可協助您撰寫自己的程式庫，但不一定需要作為實際的套件相依性。

此 `pack` 命令會忽略 `package` 中的專案，該專案的 `packages.config` `developmentDependency` 屬性設定為 `true` 。 這些專案不會在建立的封裝中包含為相依性。

例如，請考慮 `packages.config` 來源專案中的下列檔案：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

針對此專案，所建立的封裝 `nuget pack` 將相依于 `jQuery` 和， `microsoft-web-helpers` 而不是 `netfx-Guard` 。

## <a name="suppressing-pack-warnings"></a>隱藏套件警告

雖然建議您在封裝作業期間解決所有的 NuGet 警告，但在某些情況下，這些警告會受到保證。

您可以透過下列方式達成此目的： 

> nuget.exe 套件封裝. nuspec-Properties NoWarn = NU5104

## <a name="examples"></a>範例

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
