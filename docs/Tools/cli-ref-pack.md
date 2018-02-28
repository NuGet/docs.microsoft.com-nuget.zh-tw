---
title: "NuGet 的 CLI 組件命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 套件命令參考"
keywords: "nuget 組件參考組件命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9ee5dc87ea33b4419bcd9a09751c41b53ae2f70e
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2018
---
# <a name="pack-command-nuget-cli"></a>組件命令 (NuGet CLI)

**適用於：**封裝建立&bullet;**支援的版本：** 2.7 +

建立根據指定的 NuGet 套件`.nuspec`或專案檔。 `dotnet pack`命令 (請參閱[dotnet 命令](dotnet-Commands.md)) 和`msbuild /t:pack`(請參閱[MSBuild 目標](../reference/msbuild-targets.md)) 可做為替代項目。

> [!Important]
> 下單聲道，不支援從專案檔中建立封裝。 您也需要調整非區域路徑中的`.nuspec`Unix 樣式的路徑，檔案，如 nuget.exe 未轉換 Windows 路徑名稱本身。

## <a name="usage"></a>使用量

```cli
nuget pack <nuspecPath | projectPath> [options]
```

其中`<nuspecPath>`和`<projectPath>`指定`.nuspec`或專案檔，分別。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| BasePath | 設定檔案中定義的基底路徑`.nuspec`檔案。 |
| 組建 | 指定應該建置封裝前，先建置專案。 |
| 排除 | 指定建立封裝時所要排除的一個或多個萬用字元模式。 若要指定多個模式，請重複-排除旗標。 請參閱以下的範例。 |
| ExcludeEmptyDirectories | 建立封裝時，可避免包含空的目錄。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| IncludeReferencedProjects | 指出已建立的封裝應包含參考的專案做為相依性，或是做為封裝的一部分。 如果參考的專案都有對應`.nuspec`檔案具有相同名稱做為專案，則該參考的專案加入做為相依性。 否則，封裝的一部分加入參考的專案。 |
| MinClientVersion | 設定*minClientVersion*屬性建立的封裝。 這個值會覆寫現有的值*minClientVersion*屬性 （如果有的話） 中`.nuspec`檔案。 |
| MSBuildPath | *（4.0 +)*指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)*指定要搭配此命令使用 MSBuild 的版本。 支援的值為 4，12，14，15。 根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。 |
| NoDefaultExcludes | 防止預設排除的 NuGet 封裝檔案和檔案和資料夾的啟動點，如`.svn`和`.gitignore`。 |
| NoPackageAnalysis | 指定封裝不應該在建置套件之後執行套件分析。 |
| OutputDirectory | 指定建立的封裝儲存所在的資料夾。 如果沒有指定資料夾，則會使用目前的資料夾。 |
| 屬性 | 指定覆寫專案檔案中的值的屬性的清單請參閱[一般 MSBuild 專案屬性](/visualstudio/msbuild/common-msbuild-project-properties)屬性名稱。 屬性引數是一份語彙基元 = value 配對，以分號分隔，其中出現的每個`$token$`中`.nuspec`檔案將會取代為指定的值。 值可以是以引號的字串。 請注意，「 設定 」 屬性，預設值是"Debug"。 若要變更的發行組態，請使用`-Properties Configuration=Release`。 |
| 尾碼 | *(3.4.4+)*將後置詞附加至內部產生的版本號碼，通常用於附加建置或其他發行前版本識別項。 例如，使用`-suffix nightly`將建立一個封裝的版本編號的類似`1.2.3-nightly`。 後置字元的開頭必須是字母，若要避免警告、 錯誤和潛在的不相容，使用不同版本的 NuGet 和 NuGet 套件管理員。 |
| Symbol | 指定封裝包含來源和符號。 當搭配`.nuspec`檔案，這會建立一般的 NuGet 封裝檔案，而對應符號封裝。 |
| 工具 | 指定專案的輸出檔應該放在`tool`資料夾。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |
| 版本 | 覆寫的版本號碼`.nuspec`檔案。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>不含開發依存性

部分 NuGet 封裝都可用為開發相依性，這可協助您撰寫您自己的程式庫，但不一定需要與實際封裝的相依性。

`pack`命令將會忽略`package`中的項目`packages.config`具有`developmentDependency`屬性設為`true`。 這些項目不會包含與建立的封裝中的相依性。

例如，請考慮下列`packages.config`來源專案檔中：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

此專案中，為封裝建立`nuget pack`有相依性`jQuery`和`microsoft-web-helpers`但不是`netfx-Guard`。

## <a name="examples"></a>範例

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
