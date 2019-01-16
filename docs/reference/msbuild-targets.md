---
title: NuGet 封裝和還原為 MSBuild 目標
description: 使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8132595cbfaf553736fbcc81aada283a44d6cdbf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324847"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet 封裝和還原為 MSBuild 目標

*NuGet 4.0+*

利用 PackageReference 格式，NuGet 4.0+ 可以在專案檔內直接儲存所有資訊清單中繼資料，而非使用個別的 `.nuspec` 檔案。

使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。 這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。 (在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令)。

## <a name="target-build-order"></a>目標組建順序

因為 `pack` 和 `restore` 是 MSBuild 目標，所以您可以存取它們，以加強工作流程。 例如，假設您想要在封裝套件之後，將套件複製至網路共用。 做法是在專案檔中新增下列項目：

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，以及在 MSBuild 工作中使用 NuGet 屬性。

## <a name="pack-target"></a>封裝目標

.NET Standard 專案使用 PackageReference 格式，請使用`msbuild -t:pack`獲得從要用來建立 NuGet 套件的專案檔的輸入。

下表描述可新增至第一個 `<PropertyGroup>` 節點內之專案檔的 MSBuild 屬性。 以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。 為了方便起見，資料表是依 [`.nuspec` 檔案](../reference/nuspec.md)中的對等屬性進行組織。

請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。

| 屬性/NuSpec 值 | MSBuild 屬性 | 預設 | 注意 |
|--------|--------|--------|--------|
| ID | PackageId | AssemblyName | MSBuild 中的 $(AssemblyName) |
| 版本 | PackageVersion | 版本 | 這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345” |
| VersionPrefix | PackageVersionPrefix | 空白 | 設定 PackageVersion 會覆寫 PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | 空白 | MSBuild 中的 $(VersionSuffix)。 設定 PackageVersion 會覆寫 PackageVersionSuffix |
| 作者 | 作者 | 目前使用者的使用者名稱 | |
| Owners | N/A | NuSpec 中沒有 | |
| 標題 | 標題 | PackageId| |
| 描述 | 描述 | "Package Description" | |
| Copyright | Copyright | 空白 | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| 授權 | PackageLicenseExpression | 空白 | 對應至 `<license type="expression">` |
| 授權 | PackageLicenseFile | 空白 | 對應至 `<license type="file">`。 您可能需要明確組件參考的授權檔案。 |
| LicenseUrl | PackageLicenseUrl | 空白 | `licenseUrl` 已被取代，使用 [PackageLicenseExpression] 或 PackageLicenseFile 屬性 |
| ProjectUrl | PackageProjectUrl | 空白 | |
| IconUrl | PackageIconUrl | 空白 | |
| Tags | PackageTags | 空白 | 以分號來分隔標記。 |
| ReleaseNotes | PackageReleaseNotes | 空白 | |
| 存放庫/Url | RepositoryUrl | 空白 | 用來複製或擷取原始程式碼存放庫 URL。 範例： *https://github.com/NuGet/NuGet.Client.git* |
| 存放庫/類型 | RepositoryType | 空白 | 存放庫類型。 範例： *git*， *tfs*。 |
| 存放庫/分支 | RepositoryBranch | 空白 | 選擇性的存放庫分支資訊。 *RepositoryUrl*也必須指定要包含此屬性。 範例：*主要*(NuGet 4.7.0+) |
| 存放庫/認可 | RepositoryCommit | 空白 | 選擇性的儲存機制認可或變更集，以表示其來源的套件建置。 *RepositoryUrl*也必須指定要包含此屬性。 範例：*0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| 總結 | 不支援 | | |

### <a name="pack-target-inputs"></a>封裝目標輸入

- IsPackable
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- 作者
- 描述
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>封裝案例

### <a name="suppress-dependencies"></a>隱藏相依性

若要抑制來自產生的 NuGet 套件的套件相依性，將`SuppressDependenciesWhenPacking`至`true`這會允許略過從產生的 nupkg 檔案的所有相依性。

### <a name="packageiconurl"></a>PackageIconUrl

一部分的變更[NuGet 問題 352](https://github.com/NuGet/Home/issues/352)，`PackageIconUrl`最後會變更為`PackageIconUri`而且可以是圖示檔會包含在產生的封裝根目錄的相對路徑。

### <a name="output-assemblies"></a>輸出組件

`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。 所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。

在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：

- `IncludeBuildOutput`：布林值，決定是否要將組建輸出組件包含在封裝中。
- `BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。 輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。

### <a name="package-references"></a>套件參考

請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。

### <a name="project-to-project-references"></a>專案對專案參考

預設會將專案對專案參考視為 NuGet 套件參考，例如：

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

您也可以將下列中繼資料新增至您的專案參考：

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>在套件內包含內容

若要包含內容，請將額外的中繼資料新增至現有的 `<Content>` 項目。 除非您覆寫為下列這類項目，否則 "Content" 類型的所有項目預設都會包含在套件中：

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

除非您指定套件路徑，否則所有項目預設都會新增至套件內的 `content` 和 `contentFiles\any\<target_framework>` 資料夾根目錄，並保留相對資料夾結構：

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

如果您想要將所有內容都只複製至特定根資料夾 (而不是 `content` 和 `contentFiles`)，則可以使用 MSBuild 屬性 `ContentTargetFolders`，其預設為 "content;contentFiles"，但可以設定為任何其他資料夾名稱。 請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。

`PackagePath` 可以是以分號分隔的一組目標路徑。 指定空的套件路徑會將檔案新增至套件的根目錄。 例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

另有 MSBuild 屬性 `$(IncludeContentInPack)` 預設為 `true`。 如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。

您可在上述任何項目上設定的其他封裝特定中繼資料包含 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，其在輸出 nuspec 的 ```contentFiles``` 項目上設定 ```CopyToOutput``` 和 ```Flatten``` 值。

> [!Note]
> 除了 Content 項目之外，還可以在建置動作為 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 的檔案上設定 `<Pack>` 和 `<PackagePath>` 中繼資料。
>
> 針對封裝，若要在使用萬用字元模式時將檔案名稱附加至套件路徑，您套件路徑的結尾必須是資料夾分隔符號字元，否則會將套件路徑視為包含檔案名稱的完整路徑。

### <a name="includesymbols"></a>IncludeSymbols

使用 `MSBuild -t:pack -p:IncludeSymbols=true` 時，會複製對應的 `.pdb` 檔案與其他輸出檔案 (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`)。 請注意，設定 `IncludeSymbols=true` 時會建立一般套件「和」符號套件。

### <a name="includesource"></a>IncludeSource

這與 `IncludeSymbols` 相同，差異在於它也會複製原始程式檔和 `.pdb` 檔案。 所有 `Compile` 類型的檔案都會覆寫 `src\<ProjectName>\`，並保留所產生套件中的相對路徑資料夾結構。 這也適用於任何 `ProjectReference` 的原始程式檔，而這些原始程式檔將 `TreatAsPackageReference` 設定為 `false`。

若類型為 Compile 的檔案位於專案資料夾之外，就只會將其新增至 `src\<ProjectName>\`。

### <a name="packing-a-license-expression-or-a-license-file"></a>封裝授權運算式或授權檔案

使用授權運算式時，應該使用 PackageLicenseExpression 屬性。 
[授權運算式範例](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[進一步了解授權運算式和接受的 NuGet.org 的授權](nuspec.md#license)。

當封裝的授權檔案，您需要使用 PackageLicenseFile 屬性來指定封裝路徑，相對於封裝根目錄。 此外，您需要確定在封裝中包含的檔案。 例如: 

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
[授權檔案範例](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。

### <a name="istool"></a>IsTool

使用 `MSBuild -t:pack -p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。 請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。

### <a name="packing-using-a-nuspec"></a>使用 .nuspec 封裝

您可以使用`.nuspec`檔案來封裝您的專案，前提是您要匯入的 SDK 專案檔案`NuGet.Build.Tasks.Pack.targets`，這樣可以執行封裝工作。 您仍然需要先還原專案，才可以 pack nuspec 檔案。 專案檔的目標 framework 無關，不使用封裝 nuspec 時。 下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：

1. `NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。
1. `NuspecProperties`：以分號分隔的索引鍵=值組清單。 基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`-p:NuspecProperties=\"key1=value1;key2=value2\"`。  
1. `NuspecBasePath`：基底路徑`.nuspec`檔案。

如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

請注意，封裝 nuspec 使用 dotnet.exe 或 msbuild 也會導致建置預設的專案。 可以避免此一傳遞```--no-build```屬性就相當於設定的 dotnet.exe```<NoBuild>true</NoBuild> ```在您的專案檔，以及設定```<IncludeBuildOutput>false</IncludeBuildOutput> ```專案檔中

Csproj 檔案組件 nuspec 檔案的範例為：

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>進階延伸模組點來建立自訂的套件

`pack`目標會提供在內部的目標 framework 特定組建中執行的兩個擴充點。 包含特定內容的目標 framework 和組件載入封裝，支援的擴充點：

- `TargetsForTfmSpecificBuildOutput` 目標：使用檔案內`lib`資料夾或使用指定的資料夾`BuildOutputTargetFolder`。
- `TargetsForTfmSpecificContentInPackage` 目標：用於外部檔案`BuildOutputTargetFolder`。

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

撰寫自訂目標，並將其指定的值為`$(TargetsForTfmSpecificBuildOutput)`屬性。 針對需要進入的任何檔案`BuildOutputTargetFolder`（預設程式庫），目標應該寫入 ItemGroup 的那些檔案`BuildOutputInPackage`並設定下列兩個中繼資料值：

- `FinalOutputPath`：檔案的絕對路徑如果未提供，身分識別用來評估來源路徑。
- `TargetPath`：（選擇性）需要移至的子資料夾內的檔案時，設定`lib\<TargetFramework>`，例如在其各自的文化特性資料夾底下，移至附屬組件。 預設值是檔案的名稱。

範例：

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

撰寫自訂目標，並將其指定的值為`$(TargetsForTfmSpecificContentInPackage)`屬性。 要包含在封裝中的任何檔案，目標應該寫入這些檔案的 ItemGroup`TfmSpecificPackageFile`並設定下列選擇性的中繼資料：

- `PackagePath`：其中的檔案應該是在封裝中的輸出路徑。 如果多個檔案新增至相同的封裝路徑，NuGet 就會發出警告。
- `BuildAction`：若要指派給檔案的建置動作只需要封裝路徑是否在`contentFiles`資料夾。 預設為 「 無 」。

範例：
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>還原目標

`MSBuild -t:restore` (`nuget restore` 和 `dotnet restore` 與 .NET Core 專案搭配使用) 會還原專案檔中所參考的套件，如下所示：

1. 讀取所有專案對專案參考
1. 讀取專案屬性來尋找中繼資料夾和目標架構
1. 將 msbuild 資料傳遞至 NuGet.Build.Tasks.dll
1. 執行還原
1. 下載套件
1. 撰寫資產檔案、目標和屬性

`restore`目標 works**只有**對於使用 PackageReference 格式的專案。 它會**未**工作使用的專案`packages.config`格式; 請改用[nuget 還原](../tools/cli-ref-restore.md)改為。

### <a name="restore-properties"></a>還原屬性

其他還原設定可能來自專案檔中的 MSBuild 屬性。 您也可以從命令列，使用 `-p:` 參數設定值 (請參閱下列＜範例＞)。

| 屬性 | 描述 |
|--------|--------|
| RestoreSources | 以分號分隔的套件來源清單。 |
| RestorePackagesPath | 使用者套件資料夾路徑。 |
| RestoreDisableParallel | 限制逐一進行下載。 |
| RestoreConfigFile | 要套用之 `Nuget.Config` 檔案的路徑。 |
| RestoreNoCache | 如果為 true，可避免使用快取的套件。 請參閱[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| RestoreIgnoreFailedSources | 如果為 true，請忽略失敗或遺漏的套件來源。 |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll` 的路徑。 |
| RestoreGraphProjectInput | 要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。 |
| RestoreOutputPath | 輸出資料夾，預設為 `obj` 資料夾。 |

#### <a name="examples"></a>範例

命令列：

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

專案檔：

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Restore outputs

還原會在組建 `obj` 資料夾中建立下列檔案：

| 檔案 | 描述 |
|--------|--------|
| `project.assets.json` | 包含封裝的所有參考的相依性圖形。 |
| `{projectName}.projectFileExtension.nuget.g.props` | 套件中所含 MSBuild 屬性的參考 |
| `{projectName}.projectFileExtension.nuget.g.targets` | 套件中所含 MSBuild 目標的參考 |

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` 項目可讓您指定一組要在還原套件時使用的相容目標。 其設計目的是要讓使用 dotnet [TxM](../reference/target-frameworks.md) 的套件可以與未宣告 dotnet TxM 的相容套件一起運作。 也就是說，如果您的專案使用 dotnet TxM，除非您將 `<PackageTargetFallback>` 新增至專案，以讓非 dotnet 平台變成與 dotnet 相容，否則其相依的所有套件也必須要有 dotnet TxM。

例如，如果專案使用 `netstandard1.6` TxM，而且相依套件僅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，則無法建置專案。 如果您想要匯入的是第二個 DLL，則可以如下新增 `PackageTargetFallback`，指出 `portable-net45+win81` DLL 相容：

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

若要宣告專案中所有目標的後援，請省略 `Condition` 屬性。 您也可以包含 `$(PackageTargetFallback)` 來擴充任何現有 `PackageTargetFallback`，如下所示：

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>取代還原圖形中的一個程式庫

如果還原內含錯誤的組件，您可以排除該套件預設選項，並將其取代為您自己的選項。 首先，會有最上層 `PackageReference`，但排除所有資產：

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

接下來，新增您自己對 DLL 之適當本機複本的參考：

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
