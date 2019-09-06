---
title: NuGet 封裝和還原為 MSBuild 目標
description: 使用 NuGet 4.0+，NuGet 封裝和還原就可以直接作為 MSBuild 目標。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: a9331ad2ea0482737d84f4ea9a9babf95da8d66f
ms.sourcegitcommit: d5cc3f01a92c2d69b794343c09aff07ba9e912e5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2019
ms.locfileid: "70385896"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet 封裝和還原為 MSBuild 目標

*NuGet 4.0+*

使用[PackageReference](../consume-packages/package-references-in-project-files.md)格式時，NuGet 4.0 + 可以直接在專案檔中儲存所有資訊清單中繼資料，而不`.nuspec`是使用個別的檔案。

使用 MSBuild 15.1+，NuGet 也是含 `pack` 和 `restore` 目標的第一級 MSBuild 公民，如下所述。 這些目標可讓您使用 NuGet，就像使用任何其他 MSBuild 工作或目標一樣。 如需使用 MSBuild 建立 NuGet 套件的指示，請參閱[使用 Msbuild 建立 nuget 套件](../create-packages/creating-a-package-msbuild.md)。 (在 NuGet 3.x 和更早版本中，您可以改成透過 NuGet CLI 來使用 [pack](../reference/cli-reference/cli-ref-pack.md) 和 [restore](../reference/cli-reference/cli-ref-restore.md) 命令)。

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

> [!NOTE]
> `$(OutputPath)`是相對的，而且預期您是從專案根目錄執行命令。

## <a name="pack-target"></a>封裝目標

對於使用 PackageReference 格式的 .NET Standard 專案，使用`msbuild -t:pack`會從專案檔繪製輸入，以用來建立 NuGet 套件。

下表描述可新增至第一個 `<PropertyGroup>` 節點內之專案檔的 MSBuild 屬性。 以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。 為了方便起見，資料表是依 [`.nuspec` 檔案](../reference/nuspec.md)中的對等屬性進行組織。

請注意，MSBuild 不支援 `.nuspec` 中的 `Owners` 和 `Summary` 屬性。

| 屬性/NuSpec 值 | MSBuild 屬性 | 預設 | 注意 |
|--------|--------|--------|--------|
| ID | PackageId | AssemblyName | MSBuild 中的 $(AssemblyName) |
| Version | PackageVersion | Version | 這與 SemVer 相容，例如 “1.0.0”、“1.0.0-beta” 或 “1.0.0-beta-00345” |
| VersionPrefix | PackageVersionPrefix | 空白 | 設定 PackageVersion 會覆寫 PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | 空白 | MSBuild 中的 $(VersionSuffix)。 設定 PackageVersion 會覆寫 PackageVersionSuffix |
| 作者 | 作者 | 目前使用者的使用者名稱 | |
| Owners | N/A | NuSpec 中沒有 | |
| 標題 | 標題 | PackageId| |
| 描述 | 說明 | "Package Description" | |
| Copyright | Copyright | 空白 | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| 執照 | PackageLicenseExpression | 空白 | 對應至`<license type="expression">` |
| 執照 | PackageLicenseFile | 空白 | 對應至 `<license type="file">`。 您可能需要明確地封裝參考的授權檔案。 |
| LicenseUrl | PackageLicenseUrl | 空白 | `PackageLicenseUrl`已被取代，請使用 PackageLicenseExpression 或 PackageLicenseFile 屬性 |
| ProjectUrl | PackageProjectUrl | 空白 | |
| 圖示 | PackageIcon | 空白 | 您可能需要明確地封裝參考的圖示影像檔案。|
| IconUrl | PackageIconUrl | 空白 | `PackageIconUrl`已被取代，請使用 PackageIcon 屬性 |
| Tags | PackageTags | 空白 | 以分號來分隔標記。 |
| ReleaseNotes | PackageReleaseNotes | 空白 | |
| 存放庫/Url | RepositoryUrl | 空白 | 用來複製或取出原始程式碼的存放庫 URL。 實例 *https://github.com/NuGet/NuGet.Client.git* |
| 存放庫/類型 | RepositoryType | 空白 | 存放庫類型。 範例： *git*、 *tfs*。 |
| 存放庫/分支 | RepositoryBranch | 空白 | 選擇性的存放庫分支資訊。 您也必須指定*RepositoryUrl* ，才能包含這個屬性。 範例： *master* （NuGet 4.7.0 +） |
| 存放庫/認可 | RepositoryCommit | 空白 | 選擇性存放庫認可或變更集，用來指出要建立封裝的來源。 您也必須指定*RepositoryUrl* ，才能包含這個屬性。 範例：*0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
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

若要隱藏產生的 NuGet 套件中的套件`SuppressDependenciesWhenPacking`相依`true`性，請將設定為，允許從產生的 nupkg 檔略過所有相依性。

### <a name="packageiconurl"></a>PackageIconUrl

> [!Important]
> PackageIconUrl 已被取代。 請改用[PackageIcon](#packing-an-icon-image-file) 。

### <a name="packing-an-icon-image-file"></a>封裝圖示影像檔案

封裝圖示影像檔時，您必須使用 PackageIcon 屬性來指定相對於封裝根目錄的封裝路徑。 此外，您必須確定檔案已包含在封裝中。 影像檔案大小限制為 1 MB。 支援的檔案格式包括 JPEG 和 PNG。 我們建議使用64x64 的映射解析度。

例如：

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[封裝圖示範例](https://github.com/NuGet/Samples/tree/master/PackageIconExample)。

如需對等的 nuspec，請參閱[圖示的 nuspec 參考](nuspec.md#icon)。

### <a name="output-assemblies"></a>輸出組件

`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。 所複製的輸出檔案取決於 MSBuild 從 `BuiltOutputProjectGroup` 目標所提供的項目。

在專案檔或命令列中，您可以使用兩種 MSBuild 屬性來控制放置輸出組件的位置：

- `IncludeBuildOutput`：布林值，判斷組建輸出元件是否應包含在封裝中。
- `BuildOutputTargetFolder`：指定應該放置輸出元件的資料夾。 輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。

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

[深入瞭解 NuGet.org 所接受的授權運算式和](nuspec.md#license)授權。

封裝授權檔案時，您必須使用 PackageLicenseFile 屬性來指定相對於封裝根目錄的封裝路徑。 此外，您必須確定檔案已包含在封裝中。 例如：

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

雖然建議您改為在專案檔中包含檔案中的[所有屬性](../reference/msbuild-targets.md#pack-target) `.nuspec` ，但您可以`.nuspec`選擇使用檔案來封裝專案。 若為使用`PackageReference`的非 SDK 樣式專案，您必須匯入`NuGet.Build.Tasks.Pack.targets` ，才能執行封裝工作。 您仍然需要還原專案，才能封裝 nuspec 檔案。 （根據預設，SDK 樣式專案包含套件目標）。

專案檔的目標 framework 不相關，也不會在封裝 nuspec 時使用。 下列三個 MSBuild 屬性與使用 `.nuspec` 進行封裝有關：

1. `NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。
1. `NuspecProperties`：以分號分隔的索引鍵=值組清單。 基於 MSBuild 命令列剖析的運作方式，必須如下指定多個屬性：`-p:NuspecProperties=\"key1=value1;key2=value2\"`。  
1. `NuspecBasePath`：檔案的`.nuspec`基底路徑。

如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

請注意，使用 dotnet 封裝 nuspec 或 msbuild 也會導致預設建立專案。 藉由將屬性傳遞```--no-build```至 dotnet，即可避免這種情況，這相當於您專案檔中的設定```<NoBuild>true</NoBuild> ``` ，以及專案```<IncludeBuildOutput>false</IncludeBuildOutput> ```檔中的設定。

封裝 nuspec 檔案的 *.csproj*檔案範例如下：

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

### <a name="advanced-extension-points-to-create-customized-package"></a>用來建立自訂套件的先進擴充功能點

`pack`目標提供兩個擴充點，可在內部、目標 framework 特定組建中執行。 擴充點支援將目標 framework 特定的內容和元件包含在封裝中：

- `TargetsForTfmSpecificBuildOutput`設定用於資料夾內的`lib`檔案，或使用`BuildOutputTargetFolder`指定的資料夾。
- `TargetsForTfmSpecificContentInPackage`設定用於以外的`BuildOutputTargetFolder`檔案。

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

撰寫自訂目標，並將它指定為`$(TargetsForTfmSpecificBuildOutput)`屬性的值。 對於需要移入的`BuildOutputTargetFolder`任何檔案（預設為 lib），目標應該將這些檔案寫入至 ItemGroup `BuildOutputInPackage` ，並設定下列兩個中繼資料值：

- `FinalOutputPath`：檔案的絕對路徑;如果未提供，則會使用身分識別來評估來源路徑。
- `TargetPath`：選擇性當檔案需要進入中`lib\<TargetFramework>`的子資料夾時設定，例如在其各自的文化特性資料夾下的附屬元件。 預設為檔案名。

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

撰寫自訂目標，並將它指定為`$(TargetsForTfmSpecificContentInPackage)`屬性的值。 針對要包含在封裝中的任何檔案，目標應該將這些檔案寫入 ItemGroup `TfmSpecificPackageFile` ，並設定下列選擇性中繼資料：

- `PackagePath`：封裝中應該輸出檔案的路徑。 如果將多個檔案新增至相同的封裝路徑，NuGet 就會發出警告。
- `BuildAction`：要指派給檔案的組建動作，只有在封裝路徑位於`contentFiles`資料夾中時才需要。 預設值為 "None"。

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
1. 將 MSBuild 資料傳遞至 Nuget.exe。 .dll
1. 執行還原
1. 下載套件
1. 撰寫資產檔案、目標和屬性

目標僅適用于使用 PackageReference 格式的專案。 `restore` 其不適**用於**使用格式的`packages.config`專案; 請改用[nuget 還原](../reference/cli-reference/cli-ref-restore.md)。

### <a name="restore-properties"></a>還原屬性

其他還原設定可能來自專案檔中的 MSBuild 屬性。 您也可以從命令列，使用 `-p:` 參數設定值 (請參閱下列＜範例＞)。

| 屬性 | 描述 |
|--------|--------|
| RestoreSources | 以分號分隔的套件來源清單。 |
| RestorePackagesPath | 使用者套件資料夾路徑。 |
| RestoreDisableParallel | 限制逐一進行下載。 |
| RestoreConfigFile | 要套用之 `Nuget.Config` 檔案的路徑。 |
| RestoreNoCache | 若為 true，則避免使用快取的封裝。 請參閱[管理全域套件和](../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。 |
| RestoreIgnoreFailedSources | 如果為 true，請忽略失敗或遺漏的套件來源。 |
| RestoreFallbackFolders | 回溯資料夾，其使用方式與使用者套件資料夾相同。 |
| RestoreAdditionalProjectSources | 還原期間要使用的其他來源。 |
| RestoreAdditionalProjectFallbackFolders | 還原期間要使用的其他 fallback 資料夾。 |
| RestoreAdditionalProjectFallbackFoldersExcludes | 排除在中指定的 fallback 資料夾`RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll` 的路徑。 |
| RestoreGraphProjectInput | 要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。 |
| RestoreUseSkipNonexistentTargets  | 透過 MSBuild 收集項目時，它會決定是否使用`SkipNonexistentTargets`優化進行收集。 [未設定] 時， `true`預設為。 當無法匯入專案的目標時，結果會是失敗快速的行為。 |
| MSBuildProjectExtensionsPath | 輸出檔案夾，預設為`BaseIntermediateOutputPath` `obj`和資料夾。 |

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

| 檔案 | 說明 |
|--------|--------|
| `project.assets.json` | 包含所有封裝參考的相依性圖形。 |
| `{projectName}.projectFileExtension.nuget.g.props` | 套件中所含 MSBuild 屬性的參考 |
| `{projectName}.projectFileExtension.nuget.g.targets` | 套件中所含 MSBuild 目標的參考 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>使用一個 MSBuild 命令還原和建立

因為 NuGet 可以還原會導致 MSBuild 目標和 .props 的封裝，所以還原和組建評估會以不同的全域屬性執行。
這表示下列程式將會有無法預測且通常不正確的行為。

```cli
msbuild -t:restore,build
```

 相反地，建議的方法是：

```cli
msbuild -t:build -restore
```

相同的邏輯也適用于類似`build`的其他目標。

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
