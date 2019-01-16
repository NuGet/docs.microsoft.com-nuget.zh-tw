---
title: NuGet 的.nuspec 檔案參考
description: .nuspec 檔案包含建置套件時使用的套件中繼資料，並向套件取用者提供資訊。
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 009be99a1c6623a00b4bdbe6db3164ca70782212
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324899"
---
# <a name="nuspec-reference"></a>.nuspec 參考

`.nuspec` 檔案是包含套件中繼資料的 XML 資訊清單。 此資訊清單用來建置套件和向取用者提供資訊。 資訊清單一律包含在套件中。

本主題內容：

- [一般格式和結構描述](#general-form-and-schema)
- [取代權杖](#replacement-tokens) (搭配 Visual Studio 專案使用時)
- [相依性](#dependencies)
- [明確的組件參考](#explicit-assembly-references)
- [Framework 組件參考](#framework-assembly-references)
- [包含組件檔](#including-assembly-files)
- [包含內容檔](#including-content-files)
- [範例 nuspec 檔案](#example-nuspec-files)

## <a name="general-form-and-schema"></a>一般格式和結構描述

目前的 `nuspec.xsd` 結構描述檔案位於 [NuGet GitHub 存放庫](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)。

在此結構描述內，`.nuspec` 檔案有下列一般格式：

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

為能清晰呈現結構描述，請在 Visual Studio 中以設計模式開啟結構描述檔案，按一下 [XML 結構描述總管] 連結。 或者，將檔案開啟為程式碼，在編輯器中按一下滑鼠右鍵，選取 [Show XML Schema Explorer] (顯示 XML 結構描述總管)。 任一方式都可取得類似以下的檢視 (大部分展開時)：

![開啟了 nuspec.xsd 的 Visual Studio 結構描述總管](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>必要的中繼資料項目

雖然下列項目是套件的最低需求，但您應該考慮新增[選擇性中繼資料項目](#optional-metadata-elements)以改善開發人員使用套件的整體體驗。 

這些項目必須出現在 `<metadata>` 項目中。

#### <a name="id"></a>id 
不區分大小寫的套件識別碼，在整個 nuget.org 或套件所在的任何組件庫中都必須是唯一的。 識別碼可能不包含對 URL 而言無效的空格或字元，而且通常會遵循 .NET 命名空間規則。 如需指導方針，請參閱[選擇唯一的套件識別碼](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)。
#### <a name="version"></a>版本
套件版本，遵循 *major.minor.patch* 模式。 版本號碼可以包含預先發行版本的後置詞，如[套件版本控制](../reference/package-versioning.md#pre-release-versions)中所述。 
#### <a name="description"></a>描述
UI 顯示中的套件詳細描述。 
#### <a name="authors"></a>authors
以逗號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些名稱會顯示在 nuget.org 的 NuGet 組件庫中，並用來交互參照相同作者的其他套件。 

### <a name="optional-metadata-elements"></a>選擇性中繼資料項目

#### <a name="title"></a>標題
套件的易記標題，通常會用於 UI 顯示，以及 nuget.org 和 Visual Studio 套件管理員中。 如未指定，則使用套件識別碼。 
#### <a name="owners"></a>owners
以逗號分隔的套件作者清單，使用 nuget.org 上的設定檔名稱。這通常和 `authors` 是同一份清單，將套件上傳至 nuget.org 時會忽略。請參閱[在 nuget.org 上管理套件擁有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。 
#### <a name="projecturl"></a>projectUrl
套件首頁的 URL，通常會顯示在 UI 顯示及 nuget.org 中。 
#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl 已被取代。 改為使用授權。

套件授權的 URL，通常會顯示在 UI 顯示及 nuget.org 中。
#### <a name="license"></a>授權
SPDX 授權運算式或套件，通常會顯示在 UI 顯示及 nuget.org 中的授權檔案的路徑。如果您要授權常見例如 BSD 2 子句或 MIT 授權底下的封裝，使用相關聯的 SPDX 授權識別碼。<br>例如： `<license type="expression">MIT</license>`

以下是完整的清單[SPDX 授權識別碼](https://spdx.org/licenses/)。 NuGet.org 接受僅 OSI 或 FSF 核准授權時使用的授權類型的運算式。

如果您的套件係依據多個常見的授權，您可以指定複合的授權，使用[SPDX 運算式語法版本 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)。<br>例如： `<license type="expression">BSD-2-Clause OR MIT</license>`

如果您使用授權未被指派 SPDX 識別項，或是自訂的授權，您就可以封裝授權文字的檔案。 例如: 
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

基於 MSBuild 對等，看看[封裝授權運算式或授權檔案](msbuild-targets.md#packing-a-license-expression-or-a-license-file)。

NuGet 的授權運算式的正確語法是如下中所述[ABNF](https://tools.ietf.org/html/rfc5234)。
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl
具有透明背景之 64x64 映像的 URL，該映像會用作套件在 UI 顯示中的圖示。 確定這個項目包含「直接映像 URL」，不是包含影像的網頁 URL。 例如，若要使用 GitHub 的映像，使用 原始檔 URL，如<em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>。 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。
#### <a name="developmentdependency"></a>developmentDependency
*(2.8+)* 布林值，指定套件是否標示為僅限開發相依性，這可防止套件包含為其他套件的相依性。 使用 PackageReference (NuGet 4.8 +)，這個旗標也表示，它會將排除編譯時期資產編譯。 請參閱[DevelopmentDependency 支援 PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)
#### <a name="summary"></a>摘要
UI 顯示中的套件簡短描述。 如果省略，即使用截斷版本的 `description`。
#### <a name="releasenotes"></a>releaseNotes
*(1.5+)* 此版本套件中的變更描述，通常用於 Visual Studio Package Manager 的 [更新] 索引標籤等 UI 中，以取代套件描述。
#### <a name="copyright"></a>Copyright
*(1.5+)* 套件的著作權詳細資料。
#### <a name="language"></a>語言
套件的地區設定識別碼。 請參閱[建立當地語系化的套件](../create-packages/creating-localized-packages.md)。
#### <a name="tags"></a>標記
以逗號分隔的標記與關鍵字清單，描述套件並透過搜尋和篩選協助探索套件。 
#### <a name="serviceable"></a>可自行維修 
*(3.3+)* 僅供內部 NuGet 使用。
#### <a name="repository"></a>儲存機制
存放庫的中繼資料，其中包含四個選擇性屬性：*型別*並*url* *（4.0 +）*，以及*分支*和*認可* *（4.6 +）*。 這些屬性可讓您將對應至儲存機制，建置它，以取得可能的.nupkg 為個別的分支或認可建置套件所述。 這應該是公開可用的 url，可以是直接由叫用版本控制軟體。 因為這適用於電腦，它不應該是 html 網頁。 對於連結至專案的頁面，使用`projectUrl`欄位中，改為。

#### <a name="minclientversion"></a>minClientVersion
指定可安裝此套件的最低 NuGet 用戶端版本，此作業是由 nuget.exe 和 Visual Studio 套件管理員強制執行。 每當套件依存於 NuGet 用戶端新增的 `.nuspec` 檔案特定功能時，就會使用。 例如，套件使用的 `developmentDependency` 屬性應該為 `minClientVersion` 指定 "2.8"。 同樣地，使用 `contentFiles` 項目的套件 (請參閱下一節) 應將 `minClientVersion` 設定成 "3.3"。 另請注意，因為 2.5 之前的 NuGet 用戶端無法辨識此旗標，所以它們「一律」拒絕安裝套件，無論 `minClientVersion` 包含什麼。

#### <a name="collection-elements"></a>集合項目

#### <a name="packagetypes"></a>packageTypes
*(3.5+)* 零或多個 `<packageType>` 元素的集合，如果不是傳統相依性套件，則會指定套件類型。 每個 packageType 都有「名稱」和「版本」屬性。 請參閱[設定套件類型](../create-packages/creating-a-package.md#setting-a-package-type)。
#### <a name="dependencies"></a>相依性
零或多個 `<dependency>` 項目的集合，指定套件的相依性。 每個相依性都有「識別碼」、「版本」、「包含」(3.x+) 和「排除」(3.x+) 屬性。 請參閱下文的[相依性](#dependencies-element)。
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2+)* 零或多個 `<frameworkAssembly>` 項目的集合，識別此套件需要的 .NET Framework 組件參考，它們可確保參考會新增至取用套件的專案。 每個 frameworkAssembly 都有 *assemblyName* 和 *targetFramework* 屬性。 請參閱下文的[指定 Framework 組件參考 GAC](#specifying-framework-assembly-references-gac)。 |
#### <a name="references"></a>參考
*(1.5+)* 在套件的 `lib` 資料夾中命名組件的零或多個 `<reference>` 項目集合，這些項目可新增為專案參考。 每個參考都有 *file* 屬性。 `<references>` 也可以包含具有 *targetFramework* 屬性的 `<group>` 項目，然後即可包含 `<reference>` 項目。 如果省略，就會包含 `lib` 中的所有參考。 請參閱下文中的[指定明確的組件參考](#specifying-explicit-assembly-references)。
#### <a name="contentfiles"></a>contentFiles
*(3.3+)* `<files>` 項目的集合，可識別要包含在取用專案中的內容檔案。 這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定。 請參閱下文中的[指定要包含在套件中的檔案](#specifying-files-to-include-in-the-package)。
#### <a name="files"></a>個檔案 
`<package>`節點可包含`<files>`同層級節點`<metadata>`，以及`<contentFiles>`下的子系`<metadata>`，指定要包含在封裝中的哪些組件和內容檔案。 如需詳細資料，請參閱本主題下文中的[包含組件檔](#including-assembly-files)和[包含內容檔](#including-content-files)。

## <a name="replacement-tokens"></a>取代權杖

建立套件時，[`nuget pack` 命令](../tools/cli-ref-pack.md) 會使用來自專案檔的值或來自 `pack` 命令的 `-properties` 參數值，取代 `.nuspec` 檔案之 `<metadata>` 節點的 $ 分隔權杖。

在命令列中，您可以使用 `nuget pack -properties <name>=<value>;<name>=<value>` 指定權杖值。 例如，您可以在 `.nuspec` 中使用權杖，例如 `$owners$` 和 `$desc$`，並在封裝階段提供值，如下所示：

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

若要使用專案中的值，請指定下表中描述的權杖 (AssemblyInfo 是指 `Properties` 中的檔案，例如 `AssemblyInfo.cs` 或 `AssemblyInfo.vb`)。

若要使用這些權杖，請執行 `nuget pack` 與專案檔，非僅 `.nuspec`。 例如，使用下列命令時，專案的 `AssemblyName` 和 `AssemblyVersion` 值會取代為 `.nuspec` 檔案中的 `$id$` 和 `$version$` 權杖：

```ps
nuget pack MyProject.csproj
```

通常，當您擁有專案時，一開始會使用自動包含這些標準權杖一部分的 `nuget spec MyProject.csproj` 來建立 `.nuspec`。 不過，如果專案沒有所需之 `.nuspec` 項目的值，則 `nuget pack` 會失敗。 此外，如果變更專案值，請務必在建立套件前重建；使用 pack 命令的 `build` 參數很容易完成此作業。

除 `$configuration$` 以外，專案中值的使用順序優先於任何指派給命令列上相同權杖的值。

| 語彙基元 | 值來源 | 值
| --- | --- | ---
| **$id$** | 專案檔 | 從專案檔的 AssemblyName （標題） |
| **$version$** | AssemblyInfo | 如有則為 AssemblyInformationalVersion，否則為 AssemblyVersion |
| **$authors$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | 組件 DLL | 用以建置組件的組態，預設為偵錯。 請注意，若要建立使用版本組態的套件，命令列上一律要使用 `-properties Configuration=Release`。 |

當您包含[組件檔](#including-assembly-files)和[內容檔](#including-content-files)時，也可使用權杖來解析路徑。 權杖和 MSBuild 屬性有相同的名稱，所以您才能夠根據目前的組建組態選取要包含的檔案。 例如，如果在 `.nuspec` 檔案中使用下列權杖：

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

而您建置的組件，其 `AssemblyName` 是在 MSBuild 中有 `Release` 組態的 `LoggingLibrary`，在套件的 `.nuspec` 檔案中產生的程式碼如下：

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>相依性項目

`<metadata>` 內的 `<dependencies>` 項目包含任意數目的 `<dependency>` 項目，可識別最上層套件依存的其他套件。 每個 `<dependency>` 的屬性如下：

| 屬性 | 描述 |
| --- | --- |
| `id` | (必要) 相依性的套件識別碼，例如 "EntityFramework" 與 "NUnit"，是在套件頁面上顯示的套件 nuget.org 名稱。 |
| `version` | (必要) 可接受為相依性的版本範圍。 如需確切的語法，請參閱[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。 |
| include | 包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要包含的相依性。 預設值為 `all`。 |
| exclude | 包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要排除的相依性。 預設值是`build,analyzers`可能會覆寫。 但`content/ ContentFiles`也會隱含地被排除在最終的套件無法覆寫。 以 `exclude` 指定的標記優先於以 `include` 指定的標記。 例如，`include="runtime, compile" exclude="compile"` 與 `include="runtime"` 相同。 |

| 包含/排除標記 | 目標的受影響資料夾 |
| --- | --- |
| contentFiles | 內容 |
| runtime | 執行階段、資源和 FrameworkAssemblies |
| compile | lib |
| build | 組建 (MSBuild props 和目標) |
| native | native |
| none | 無資料夾 |
| all | 全部資料夾 |

例如，下列幾行程式碼指出 `PackageA`1.1.0 版或更高版本與 `PackageB` 1.x 版的相依性。

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

下列幾行程式碼指出相同套件的相依性，但指定要包含 `PackageA` 的 `contentFiles` 和 `build` 資料夾，以及 `PackageB` 的 `native` 和 `compile` 資料夾以外的所有一切

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

注意:建立時`.nuspec`專案，使用`nuget spec`，在該專案中存在的相依性會自動包含在產生`.nuspec`檔案。

### <a name="dependency-groups"></a>相依性群組

*2.0+ 版*

當作單一一般清單的替代方案，您可以使用 `<dependencies>` 內的 `<group>` 項目，根據目標專案的 Framework 設定檔指定相依性。

每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<dependency>` 項目。 當目標 Framework 與專案的 Framework 設定檔相容時，會同時安裝這些相依性。

沒有 `targetFramework` 屬性的 `<group>` 項目用為預設值或後援相依性清單。 如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。

> [!Important]
> 群組格式無法和一般清單混合使用。

下列範例示範 `<group>` 項目的不同變化：

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>明確的組件參考

`<references>` 項目明確指定使用套件時，目標專案應該參考的組件。 有此項目時，NuGet 只會將參考新增至列出的組件。它不會在套件的 `lib` 資料夾中新增任何其他組件的參考。

例如，以下 `<references>` 項目會指示 NuGet 只將參考新增至 `xunit.dll` 和 `xunit.extensions.dll`，即使套件中有其他組件：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

明確參考通常只用於設計階段的組件。 例如使用 [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts) (程式碼合約) 時，合約組件必須在它們擴大的執行階段組件旁邊，讓 Visual Studio 可以找到它們，但是合約組件不需要被專案參考，或複製到專案的 `bin` 資料夾。

同樣地，明確參考可以用於單元測試 Framework ，例如 XUnit，這需要它的工具組件位在執行階段組件旁邊，但它們不需要包含為專案參考。

### <a name="reference-groups"></a>參考群組

當作單一一般清單的替代方案，您可以使用 `<references>` 內的 `<group>` 項目，根據目標專案的 Framework 設定檔指定參考。

每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<reference>` 項目。 當目標 Framework 與專案的 Framework 設定檔相容時，這些參考會新增至專案。

沒有 `targetFramework` 屬性的 `<group>` 項目用為預設值或後援參考清單。 如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。

> [!Important]
> 群組格式無法和一般清單混合使用。

下列範例示範 `<group>` 項目的不同變化：

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Framework 組件參考

Framework 組件屬於 .NET Framework，應該已經在任何指定電腦的全域組件快取 (GAC) 中。 找出 `<frameworkAssemblies>` 項目內的這些組件，套件可以確保所需的參考已新增至事件的專案，該專案尚未有這類參考。 當然，這類組件不直接包含在套件中。

`<frameworkAssemblies>` 項目包含零或多個 `<frameworkAssembly>` 項目，它們每一個都會指定下列屬性：

| 屬性 | 描述 |
| --- | --- |
| **assemblyName** | (必要) 完整組件名稱。 |
| **targetFramework** | (選擇性) 指定要套用這個參考的目標 Framework。 如果省略，則表示參考適用於所有 Framework。 如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。 |

下列範例會顯示所有目標 Framework 的 `System.Net` 參考，以及僅供 .NET Framework 4.0 使用的 `System.ServiceModel` 參考：

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>包含組件檔

如果遵循[建立套件](../create-packages/creating-a-package.md)中所述的慣例，即不必在 `.nuspec` 檔案中明確指定檔案清單。 `nuget pack` 命令會自動挑選必要的檔案。

> [!Important]
> 當套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，「排除」那些名為 `.resources.dll` 的參考，因為它們假設是當地語系化的附屬組件。 因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。

為略過這項自動行為並明確控制套件要包含哪些檔案，請放置 `<files>` 項目當作 `<package>` 的子系 (和 `<metadata>` 的同層級)，找出每個有不同 `<file>` 項目的檔案。 例如: 

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

使用 NuGet 2.x 及更舊版本，並規劃使用 `packages.config`；在安裝套件時，也會使用 `<files>` 項目包含不可變的內容檔。 使用 NuGet 3.3+ 和專案 PackageReference，則改用 `<contentFiles>` 元素。 如需詳細資料，請參閱下文中的[包含內容檔](#including-content-files)。

### <a name="file-element-attributes"></a>檔案項目屬性

每個 `<file>` 項目都會指定下列屬性：

| 屬性 | 描述 |
| --- | --- |
| **src** | 要包含的檔案位置，會受到 `exclude` 屬性指定的排除項目約束。 路徑相對於 `.nuspec` 檔案，除非指定絕對路徑。 允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。 |
| **目標** | 套件內資料夾的相對路徑是放置原始程式檔的位置，其開頭必須是 `lib`、`content`、`build` 或 `tools`。 請參閱[從慣例的工作目錄建立 .nuspec](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)。 |
| **排除** | `src` 位置要排除之以分號分隔的檔案清單或檔案模式。 允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。 |

### <a name="examples"></a>範例

**單一組件**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**目標 Framework 的特定單一組件**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**使用萬用字元的 DLL 集合**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**不同 Framework 的 DLL**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**排除檔案**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>包含內容檔

內容檔是不可變的檔案，套件必須將它們包含在專案中。 因為不可變，所以取用專案不宜修改它們。 內容檔範例包括：

- 內嵌為資源的映像
- 已編譯原始程式檔
- 需要以專案的組建輸出包含的指令碼
- 套件的組態檔必須包含在專案中，但不需要專門針對任何專案變更

內容檔包含在使用 `<files>` 項目的套件中，指定 `target` 屬性中的 `content` 資料夾。 不過，使用 PackageReference 在專案中安裝套件時，會忽略這類檔案，改用 `<contentFiles>` 元素。

為取得取用專案的最大相容性，套件應該在兩個項目中都指定內容檔。

### <a name="using-the-files-element-for-content-files"></a>內容檔使用 files 項目

內容檔只要使用和組件檔相同的格式即可，但要在 `target` 屬性中指定 `content` 作為基底資料夾，如下列範例所示。

**基本內容檔**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**具有目錄結構的內容檔**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**目標 Framework 的特定內容檔案**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**複製到資料夾，名稱中有點的內容檔**

在此情況下，NuGet 會看到 `target` 的副檔名與 `src` 的副檔名不相符，因此會將 `target` 名稱的該部分視為資料夾：

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**無副檔名的內容檔**

若要包含不含副檔名的檔案，請使用 `*` 或 `**` 萬用字元：

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**有深路徑和深層目標的內容檔**

在此情況下，因為原始程式檔的副檔名和目標相符，所以 NuGet 會假設目標是檔案名稱，不是資料夾：

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**重新命名套件中的內容檔**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**排除檔案**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>內容檔使用 contentFiles 項目

*NuGet 4.0+ 與 PackageReference*

根據預設，套件會將內容放在 `contentFiles` 資料夾 (請參閱下文)，而 `nuget pack` 包含使用預設屬性資料夾中的所有檔案。 在此情況下，`.nuspec` 完全不需要包含 `contentFiles` 節點。

為控制包含哪些檔案，`<contentFiles>` 項目要指定 `<files>` 項目的集合，找出正確的檔案。

這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定：

| 屬性 | 描述 |
| --- | --- |
| **include** | (必要) 要包含的檔案位置，受限於 `exclude` 屬性所指定的排除項目。 路徑相對於 `.nuspec` 檔案，除非指定絕對路徑。 允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。 |
| **排除** | `src` 位置要排除之以分號分隔的檔案清單或檔案模式。 允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。 |
| **buildAction** | 要指派給 MSBuild 內容項目的建置動作，例如 `Content`、`None`、`Embedded Resource`、`Compile` 等等。預設為 `Compile`。 |
| **copyToOutput** | 布林值，指出是否要將內容項目複製到組建 （或發行） 的輸出資料夾。 預設為 false。 |
| **flatten** | 布林值，指出要將內容項目複製到組建輸出的單一資料夾 (true)，或保留套件中的資料夾結構 (false)。 這個旗標僅適用於將 copyToOutput 旗標設為 true 時。 預設為 false。 |

安裝套件時，NuGet 會由上而下套用 `<contentFiles>` 的子項目。 如有多個項目符合同一檔案，則套用所有項目。 如果相同的屬性發生衝突，則最上層項目會覆寫較低的項目。

#### <a name="package-folder-structure"></a>套件資料夾結構

套件專案應該結構化使用下列模式的內容：

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` 可能是 `cs`、`vb`、`fs`、`any`，或指定的 `$(ProjectLanguage)` 小寫對等項
- `TxM` 是 NuGet 支援的任何合法目標 Framework Moniker (請參閱[目標 Framework](../reference/target-frameworks.md))。
- 這個語法的結尾可以附加任何資料夾結構。

例如: 

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

空資料夾可以使用 `.` 選擇不提供特定語言和 TxM 組合的內容，例如：

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>contentFiles 區段範例

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>範例 nuspec 檔案

**簡單的 `.nuspec` 不指定相依性或檔案**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**具有相依性的 `.nuspec`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**具有檔案的 `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**具有 Framework 組件的 `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

在此範例中，特定專案目標會安裝下列項目：

- .NET4 -> `System.Web`、`System.Net`
- .NET4 Client Profile -> `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
