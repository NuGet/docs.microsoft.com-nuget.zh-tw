---
title: NuGet CLI 套件命令
description: Nuget.exe pack 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 2358cedc05520a3ec82a39aef34b6d467e44460b
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231158"
---
# <a name="pack-command-nuget-cli"></a>pack 命令（NuGet CLI）

**適用于：** 套件建立 &bullet;**支援的版本：** 2.7 +

根據指定的[nuspec](../nuspec.md)或專案檔，建立 NuGet 套件。 `dotnet pack` 命令（請參閱[Dotnet 命令](../dotnet-Commands.md)）和 `msbuild -t:pack` （請參閱[MSBuild 目標](../msbuild-targets.md)）可用來做為替代項。

> [!Important]
> 針對以[PackageReference](../../consume-packages/package-references-in-project-files.md)為基礎的專案，請使用[`dotnet pack`](../dotnet-Commands.md)或[`msbuild -t:pack`](../msbuild-targets.md) 。
> 在 Mono 底下，不支援從專案檔建立封裝。 您也需要將 `.nuspec` 檔案中的非本機路徑調整為 Unix 樣式路徑，因為 nuget.exe 不會轉換 Windows 路徑路徑本身。

## <a name="usage"></a>使用量

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

其中 `<nuspecPath>` 和 `<projectPath>` 分別指定 `.nuspec` 或專案檔。

## <a name="options"></a>選項。

| 選項 | 描述 |
| --- | --- |
| 基本路徑 | 設定[nuspec](../nuspec.md)檔案中定義之檔案的基底路徑。 |
| Build | 指定在建立封裝之前，應該先建立專案。 |
| 排除 | 指定建立封裝時要排除的一或多個萬用字元模式。 若要指定一個以上的模式，請重複-Exclude 旗標。 請參閱以下的範例。 |
| ExcludeEmptyDirectories | 在建立封裝時，防止包含空的目錄。 |
| ForceEnglishOutput | *（3.5 +）* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| ConfigFile | 指定 pack 命令的設定檔案。 |
| 説明 | 顯示命令的說明資訊。 |
| IncludeReferencedProjects | 表示建立的封裝應該將參考的專案包含為相依性或封裝的一部分。 如果參考的專案有與專案同名的對應 `.nuspec` 檔案，則會將該參考的專案新增為相依性。 否則，會將參考的專案新增為封裝的一部分。 |
| MinClientVersion | 為已建立的封裝設定*minClientVersion*屬性。 這個值會覆寫 `.nuspec` 檔案中現有的*minClientVersion*屬性值（如果有的話）。 |
| MSBuildPath | *（4.0 +）* 指定要搭配命令使用之 MSBuild 的路徑，其優先順序高於 `-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +）* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 根據預設，會挑選路徑中的 MSBuild，否則會預設為 MSBuild 的最高安裝版本。 |
| NoDefaultExcludes | 防止預設排除 NuGet 套件檔案和檔案和資料夾，以點為開頭，例如 `.svn` 和 `.gitignore`。 |
| NoPackageAnalysis | 指定封裝不應該在建置套件之後執行套件分析。 |
| OutputDirectory | 指定用來儲存所建立封裝的資料夾。 如果未指定任何資料夾，則會使用目前的資料夾。 |
| 屬性 | 在其他選項之後，應該會出現在命令列上的最後一個。 指定覆寫專案檔中值的屬性清單;請參閱屬性名稱的[一般 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)。 這裡的 Properties 引數是 token = 值組的清單（以分號分隔），其中 `.nuspec` 檔案中的每個 `$token$` 都會被指定的值取代。 值可以是以引號括住的字串。 請注意，對於 "Configuration" 屬性，預設值為 "Debug"。 若要變更為發行設定，請使用 `-Properties Configuration=Release`。 **一般而言**，屬性應該與對應 `nuget build`期間所使用的相同，以避免潛在的異常行為。 |
| 後置詞 | *（3.4.4 +）* 將尾碼附加至內部產生的版本號碼，通常用於附加組建或其他預先發行識別碼。 例如，使用 `-suffix nightly` 將會建立版本號碼類似 `1.2.3-nightly`的套件。 尾碼必須以字母開頭，以避免與不同版本 NuGet 和 NuGet 套件管理員的警告、錯誤和潛在的不相容。 |
| Symbols | 指定封裝包含來源和符號。 與 `.nuspec` 檔案搭配使用時，這會建立一般的 NuGet 套件檔案和對應的符號套件。 根據預設，它會建立[舊版符號套件](../../create-packages/Symbol-Packages.md)。 為符號套件新建議的格式為 .snupkg。 請參閱[建立符號套件 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。 |
| 工具 | 指定專案的輸出檔應該放在 `tool` 資料夾中。 |
| 詳細程度 | 指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。 |
| 版本 | 覆寫 `.nuspec` 檔案中的版本號碼。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>排除開發相依性

某些 NuGet 套件可作為開發相依性，協助您撰寫自己的程式庫，但不一定需要做為實際的封裝相依性。

`pack` 命令會忽略 `packages.config` 中 `developmentDependency` 屬性設為 `true`的 `package` 專案。 這些專案將不會包含在建立的封裝中做為相依性。

例如，請考慮來源專案中的下列 `packages.config` 檔案：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

針對此專案，`nuget pack` 所建立的封裝會相依于 `jQuery` 和 `microsoft-web-helpers` 但不會 `netfx-Guard`。

## <a name="suppressing-pack-warnings"></a>隱藏套件警告

雖然建議您在封裝作業期間解析所有的 NuGet 警告，但在某些情況下，不一定要將它們強制執行。

您可以透過下列方式達到此目的： 

> nuget.exe pack package. nuspec-Properties NoWarn = NU5104

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
