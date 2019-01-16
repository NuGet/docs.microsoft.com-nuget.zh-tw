---
title: NuGet CLI pack 命令
description: Nuget.exe pack 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d39ec8caf94caa767b6c502cc475e278aa718b95
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324782"
---
# <a name="pack-command-nuget-cli"></a>pack 命令 (NuGet CLI)

**適用於：** 封裝建立&bullet;**支援的版本：** 2.7+

建立根據指定的 NuGet 套件`.nuspec`或專案檔。 `dotnet pack`命令 (請參閱 < [dotnet 命令](dotnet-Commands.md)) 及`msbuild -t:pack`(請參閱[MSBuild 目標](../reference/msbuild-targets.md)) 可作為替代項目。

> [!Important]
> 在 Mono 下不支援從專案檔中建立封裝。 您也需要調整中的非區域路徑`.nuspec`檔案為 Unix 樣式的路徑，nuget.exe 不會將轉換本身的 Windows 路徑名稱。

## <a name="usage"></a>使用量

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

何處`<nuspecPath>`並`<projectPath>`指定`.nuspec`或專案檔，分別。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| BasePath | 設定檔案中定義的基底路徑`.nuspec`檔案。 |
| 組建 | 指定應該在建置封裝之前建置專案。 |
| 排除 | 指定建立封裝時所要排除的一個或多個萬用字元模式。 若要指定一個以上的模式，請重複-排除旗標。 請參閱以下的範例。 |
| ExcludeEmptyDirectories | 建置套件時，可避免包含空的目錄。 |
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| ConfigFile | 指定組件命令的組態檔。 |
| 說明 | 顯示說明命令的資訊。 |
| IncludeReferencedProjects | 指出已建置的套件應包含參考的專案，做為相依性，或是做為封裝的一部分。 如果參考的專案都有對應`.nuspec`有同名的專案，則該參考的專案新增為相依性的檔案。 否則參考的專案新增為套件的一部分。 |
| MinClientVersion | 設定*minClientVersion*屬性建立的封裝。 這個值會覆寫現有的值*minClientVersion*中的屬性 （如果有的話）`.nuspec`檔案。 |
| MSBuildPath | *（4.0 +)* 指定要搭配命令，優先於使用 MSBuild 的路徑`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為 4、 12、 14、 15。 根據您的路徑中的 MSBuild 會挑出的預設值，否則，預設已安裝的最高的 MSBuild 版本。 |
| NoDefaultExcludes | 會防止預設排除的 NuGet 封裝檔案和檔案和資料夾從一個點，例如`.svn`和`.gitignore`。 |
| NoPackageAnalysis | 指定封裝不應該在建置套件之後執行套件分析。 |
| OutputDirectory | 指定建立的封裝儲存所在的資料夾。 如果未不指定任何資料夾，則會使用目前的資料夾。 |
| 屬性 | 應該會出現在命令列上的最後一個之後的其他選項。 指定專案檔案中的值會覆寫的屬性的清單請參閱[通用的 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)屬性名稱。 屬性引數是一份權杖 = 值 」 配對，並以分號區隔，其中出現的每個`$token$`在`.nuspec`檔案將會取代指定的值。 值可以是以引號的字串。 請注意，「 組態 」 屬性，預設值是"Debug"。 若要變更的發行組態，使用`-Properties Configuration=Release`。 |
| 尾碼 | *(3.4.4+)* 將後置字元附加至內部產生的版本號碼，通常用來附加組建或其他發行前版本識別項。 例如，使用`-suffix nightly`將建立一個封裝的版本號碼的按讚與`1.2.3-nightly`。 後置字元的開頭必須是字母，以避免警告、 錯誤和潛在的不相容，使用不同版本的 NuGet 和 NuGet 套件管理員。 |
| 符號 | 指定封裝包含來源和符號。 當搭配`.nuspec`檔案，這會建立一般的 NuGet 封裝檔案和對應的符號套件。 依預設它會建立[舊版的符號套件](../create-packages/Symbol-Packages.md)。 為符號套件新建議的格式為 .snupkg。 請參閱[建立符號套件 (.snupkg)](../create-packages/Symbol-Packages-snupkg.md)。 |
| 工具 | 指定專案的輸出檔案應該放在`tool`資料夾。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |
| 版本 | 覆寫的版本號碼，從`.nuspec`檔案。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>排除開發相依性

部分 NuGet 套件適合做為開發相依性，協助您撰寫自己的程式庫，但不一定需要做為實際的套件相依性。

`pack`命令將會忽略`package`中的項目`packages.config`具有`developmentDependency`屬性設為`true`。 這些項目不會包含做為建立的封裝中的相依性。

例如，請考慮下列`packages.config`來源專案檔中：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

此專案中，封裝建立的`nuget pack`會有相依性`jQuery`並`microsoft-web-helpers`而非`netfx-Guard`。

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
