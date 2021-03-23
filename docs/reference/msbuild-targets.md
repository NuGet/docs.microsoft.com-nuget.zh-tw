---
title: NuGet 套件和還原為 MSBuild 目標
description: NuGet pack 和 restore 可以直接做為 MSBuild 4.0 + 的目標使用 NuGet 。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858962"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet 套件和還原為 MSBuild 目標

*NuGet 4.0 +*

使用 [PackageReference](../consume-packages/package-references-in-project-files.md) 格式， NuGet 4.0 + 可以直接將所有資訊清單中繼資料儲存在專案檔中，而不是使用個別的檔案 `.nuspec` 。

使用 MSBuild 15.1 + NuGet 時，也是 MSBuild 具有和目標的第一級公民， `pack` `restore` 如下所述。 這些目標可讓您與 NuGet 任何其他工作或目標一樣使用 MSBuild 。 如需使用建立 NuGet 封裝的指示 MSBuild ，請參閱[ NuGet 使用 MSBuild 建立封裝](../create-packages/creating-a-package-msbuild.md)。  (3.x NuGet 及更早版本，您可以改為使用 [套件](../reference/cli-reference/cli-ref-pack.md) 並透過 CLI [還原](../reference/cli-reference/cli-ref-restore.md) 命令 NuGet 。 ) 

## <a name="target-build-order"></a>目標組建順序

因為 `pack` 和 `restore` 是  MSBuild 目標，所以您可以存取它們來增強您的工作流程。 例如，假設您想要在封裝之後將套件複製到網路共用。 做法是在專案檔中新增下列項目：

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

同樣地，您可以撰寫 MSBuild 工作、撰寫您自己的目標，並使用 NuGet 工作中的屬性 MSBuild 。

> [!NOTE]
> `$(OutputPath)` 是相對的，且預期您是從專案根目錄執行命令。

## <a name="pack-target"></a>封裝目標

針對使用格式的 .NET 專案 `PackageReference` ，使用會 `msbuild -t:pack` 從專案檔繪製輸入，以用於建立 NuGet 封裝。

下表說明 MSBuild 可以加入至第一個節點內之專案檔的屬性 `<PropertyGroup>` 。 以滑鼠右鍵按一下專案，然後選取操作功能表上的 [編輯 {project_name}]，即可在 Visual Studio 2017 和更新版本中輕鬆地進行這些編輯。 為了方便起見，資料表會依照檔案中的對等屬性進行[ `.nuspec` 組織。](../reference/nuspec.md)

> [!NOTE]
> `Owners``Summary`不支援的和屬性 `.nuspec` MSBuild 。

| 屬性/ nuspec 值 | MSBuild 屬性 | 預設 | 備註 |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | 來自 MSBuild 的 `$(AssemblyName)` |
| `Version` | `PackageVersion` | 版本 | 這是 semver 相容的，例如 `1.0.0` ， `1.0.0-beta` 或 `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | empty | 設定 `PackageVersion` 覆寫 `PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | empty | `$(VersionSuffix)` from MSBuild 。 設定 `PackageVersion` 覆寫 `PackageVersionSuffix` |
| `Authors` | `Authors` | 目前使用者的使用者名稱 | 以分號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些會顯示在 nuget.org 的資源 NuGet 庫中，並用來交互參照相同作者的封裝。 |
| `Owners` | N/A | 不存在於 nuspec | |
| `Title` | `Title` | `PackageId` | 套件的易記標題，通常會用於 UI 顯示，以及 nuget.org 和 Visual Studio 套件管理員中。 |
| `Description` | `Description` | "Package Description" | 組件的完整描述。 如果 `PackageDescription` 未指定，則此屬性也會用來做為封裝的描述。 |
| `Copyright` | `Copyright` | empty | 套件的著作權詳細資料。 |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | 布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。 |
| `license` | `PackageLicenseExpression` | empty | 對應至 `<license type="expression">`。 請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。 |
| `license` | `PackageLicenseFile` | empty | 如果您使用自訂授權或未獲指派 SPDX 識別碼的授權，則為套件內的授權檔案路徑。 您必須明確地封裝參考的授權檔案。 對應至 `<license type="file">`。 請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。 |
| `LicenseUrl` | `PackageLicenseUrl` | empty | `PackageLicenseUrl` 已被取代。 請改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。 |
| `ProjectUrl` | `PackageProjectUrl` | empty | |
| `Icon` | `PackageIcon` | empty | 封裝中用來做為封裝圖示的影像路徑。 您必須明確地封裝參考的圖示影像檔案。 如需詳細資訊，請參閱[封裝圖示影像檔](#packing-an-icon-image-file)案和[ `icon` 中繼資料](/nuget/reference/nuspec#icon)。 |
| `IconUrl` | `PackageIconUrl` | empty | `PackageIconUrl` 已被取代，改為使用 `PackageIcon` 。 但是，為了獲得最佳的早期體驗，除了之外，您還應該指定 `PackageIconUrl` `PackageIcon` 。 |
| `Tags` | `PackageTags` | empty | 以分號分隔的標記清單，用以指定套件。 |
| `ReleaseNotes` | `PackageReleaseNotes` | empty | 套件的版本資訊。 |
| `Repository/Url` | `RepositoryUrl` | empty | 用來複製或取出原始程式碼的儲存機制 URL。 範例： *https://github.com/ NuGet / NuGet 。用戶端. git*。 |
| `Repository/Type` | `RepositoryType` | empty | 存放庫類型。 範例： `git` (預設) ， `tfs` 。 |
| `Repository/Branch` | `RepositoryBranch` | empty | 選用的存放庫分支資訊。 `RepositoryUrl` 也必須指定此屬性才能包含。 範例： *master* (NuGet 4.7.0 +) 。 |
| `Repository/Commit` | `RepositoryCommit` | empty | 選用的儲存機制認可或變更集，以指出建立封裝的來源。 `RepositoryUrl` 也必須指定此屬性才能包含。 範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。 |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | 不支援 | | |

### <a name="pack-target-inputs"></a>封裝目標輸入

| 屬性 | 描述 |
| - | - |
| `IsPackable` | 布林值，指定是否可封裝專案。 預設值是 `true`。 |
| `SuppressDependenciesWhenPacking` | 設定為， `true` 以從產生的封裝中隱藏封裝相依性 NuGet 。 |
| `PackageVersion` | 指定所產生之套件的版本。 接受所有形式的 NuGet 版本字串。 預設為 `$(Version)` 的值，也就是專案中的屬性 `Version`。 |
| `PackageId` | 指定所產生之套件的名稱。 如果未指定，`pack` 作業會預設為使用 `AssemblyName` 或目錄名稱作為套件的名稱。 |
| `PackageDescription` | UI 顯示中的套件詳細描述。 |
| `Authors` | 以分號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些會顯示在 nuget.org 的資源 NuGet 庫中，並用來交互參照相同作者的封裝。 |
| `Description` | 組件的完整描述。 如果 `PackageDescription` 未指定，則此屬性也會用來做為封裝的描述。 |
| `Copyright` | 套件的著作權詳細資料。 |
| `PackageRequireLicenseAcceptance` | 布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。 預設為 `false`。 |
| `DevelopmentDependency` | 布林值，指定封裝是否標記為僅限開發的相依性，這可防止封裝作為其他封裝的相依性。 在 `PackageReference` (NuGet 4.8 +) 中，此旗標也表示編譯時期資產已從編譯中排除。 如需詳細資訊，請參閱 [PackageReference 的 DevelopmentDependency 支援](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) \(英文\)。 |
| `PackageLicenseExpression` | [SPDX 授權識別碼](https://spdx.org/licenses/)或運算式，例如 `Apache-2.0` 。 如需詳細資訊，請參閱 [封裝授權運算式或授權檔案](#packing-a-license-expression-or-a-license-file)。 |
| `PackageLicenseFile` | 如果您使用自訂授權或未獲指派 SPDX 識別碼的授權，則為套件內的授權檔案路徑。 |
| `PackageLicenseUrl` | `PackageLicenseUrl` 已被取代。 請改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。 |
| `PackageProjectUrl` | |
| `PackageIcon` | 指定封裝圖示路徑（相對於封裝的根目錄）。 如需詳細資訊，請參閱 [封裝圖示影像檔](#packing-an-icon-image-file)。 |
| `PackageReleaseNotes` | 套件的版本資訊。 |
| `PackageTags` | 以分號分隔的標記清單，用以指定套件。 |
| `PackageOutputPath` | 決定要置放所封裝之套件的輸出路徑。 預設為 `$(OutputPath)`。 |
| `IncludeSymbols` | 此布林值會指出在封裝專案時，套件是否應該建立額外的符號套件。 符號套件的格式由 `SymbolPackageFormat` 屬性控制。 如需詳細資訊，請參閱 [IncludeSymbols](#includesymbols)。 |
| `IncludeSource` | 此布林值會指出封裝處理序是否應該建立來源套件。 來源套件包含程式庫的原始程式碼及 PDB 檔案。 原始程式檔會放在所產生之套件檔案中的 `src/ProjectName` 目錄底下。 如需詳細資訊，請參閱 [IncludeSource](#includesource)。 |
| `PackageType` | |
| `IsTool` | 指定是否要將所有輸出檔複製到 *tools* 資料夾，而不是 *lib* 資料夾。 如需詳細資訊，請參閱 [IsTool](#istool)。 |
| `RepositoryUrl` | 用來複製或取出原始程式碼的儲存機制 URL。 範例： *https://github.com/ NuGet / NuGet 。用戶端. git*。 |
| `RepositoryType` | 存放庫類型。 範例： `git` (預設) ， `tfs` 。 |
| `RepositoryBranch` | 選用的存放庫分支資訊。 `RepositoryUrl` 也必須指定此屬性才能包含。 範例： *master* (NuGet 4.7.0 +) 。 |
| `RepositoryCommit` | 選用的儲存機制認可或變更集，以指出建立封裝的來源。 `RepositoryUrl` 也必須指定此屬性才能包含。 範例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。 |
| `SymbolPackageFormat` | 指定符號套件的格式。 如果是 "nupkg"，則會使用包含 Pdb、Dll 和其他輸出檔的 *nupkg* 副檔名來建立舊版符號套件。 如果是 ".snupkg"，則會建立包含便攜 Pdb 的 .snupkg 符號套件。 預設值為 "nupkg"。 |
| `NoPackageAnalysis` | 指定 `pack` 在建立封裝之後，不應該執行套件分析。 |
| `MinClientVersion` | 指定 NuGet 可安裝此封裝的最小用戶端版本，由 nuget.exe 和 Visual Studio 封裝管理員強制執行。 |
| `IncludeBuildOutput` | 這個布林值會指定是否應將組建輸出元件封裝至 *nupkg* 檔中。 |
| `IncludeContentInPack` | 這個布林值會指定是否 `Content` 要自動在產生的封裝中包含類型為的任何專案。 預設為 `true`。 |
| `BuildOutputTargetFolder` | 指定要放置輸出組件的資料夾。 輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。 如需詳細資訊，請參閱 [輸出元件](#output-assemblies)。 |
| `ContentTargetFolders` | 如果未指定所有內容檔案，則指定其預設位置 `PackagePath` 。 預設值為 "content;contentFiles"。 如需詳細資訊，請參閱 [Including content in a package](#including-content-in-a-package) (在套件中包含內容)。 |
| `NuspecFile` | 用於封裝之檔案的相對或絕對路徑 *.nuspec* 。 如果指定，則會 **專門** 用於封裝資訊，而不會使用專案中的任何資訊。 如需詳細資訊，請參閱[使用 .nuspec 封裝](#packing-using-a-nuspec-file)。 |
| `NuspecBasePath` | 檔案的基底路徑 *.nuspec* 。 如需詳細資訊，請參閱[使用 .nuspec 封裝](#packing-using-a-nuspec-file)。 |
| `NuspecProperties` | 以分號分隔的索引鍵=值組清單。 如需詳細資訊，請參閱[使用 .nuspec 封裝](#packing-using-a-nuspec-file)。 |

## <a name="pack-scenarios"></a>封裝案例

### <a name="suppressing-dependencies"></a>隱藏相關性

若要從產生的封裝隱藏封裝相依性 NuGet ，請將設定 `SuppressDependenciesWhenPacking` 為，以 `true` 允許略過產生的 nupkg 檔中的所有相依性。

### `PackageIconUrl`

`PackageIconUrl` 已被取代為屬性的使用方式 [`PackageIcon`](#packageicon) 。 從5.3 開始， NuGet Visual Studio 2019 16.3 版， `pack` 如果封裝中繼資料僅指定，則會引發 [NU5048](./errors-and-warnings/nu5048.md) 警告 `PackageIconUrl` 。

### `PackageIcon`

> [!Tip]
> 若要維持與尚未支援的用戶端和來源的回溯相容性 `PackageIcon` ，請同時指定 `PackageIcon` 和 `PackageIconUrl` 。 Visual Studio 支援 `PackageIcon` 來自以資料夾為基礎之來源的封裝。

#### <a name="packing-an-icon-image-file"></a>封裝圖示影像檔案

封裝圖示影像檔案時，請使用 `PackageIcon` 屬性來指定圖示檔路徑（相對於封裝的根目錄）。 此外，請確定檔案包含在套件中。 影像檔案大小限制為 1 MB。 支援的檔案格式包括 JPEG 和 PNG。 我們建議使用128x128 的影像解析度。

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

[封裝圖示範例](https://github.com/NuGet/Samples/tree/main/PackageIconExample)。

針對 nuspec 相等的，請查看圖示的[ nuspec 參考](nuspec.md#icon)。

### <a name="output-assemblies"></a>輸出組件

`nuget pack` 會複製副檔名為 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的輸出檔案。 複製的輸出檔案取決於 MSBuild 從目標提供的內容 `BuiltOutputProjectGroup` 。

您 MSBuild  可以在專案檔或命令列中使用兩個屬性來控制輸出元件的位置：

- `IncludeBuildOutput`：布林值，決定是否應該在套件中包含組建輸出組件。
- `BuildOutputTargetFolder`：指定應該在其中放置輸出組件的資料夾。 輸出組件 (及其他輸出檔) 會複製到其相關的架構資料夾中。

### <a name="package-references"></a>套件參考

請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)。

### <a name="project-to-project-references"></a>專案對專案參考

專案對專案的參考預設會被視為 NuGet 封裝參考。 例如：

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

如果您想要將所有內容複寫到僅 (s 的特定根資料夾)  (而非 `content` 和 `contentFiles` 兩者) ，您可以使用 MSBuild 屬性 `ContentTargetFolders` （預設為 "content; contentFiles"），但可以設定為任何其他資料夾名稱。 請注意，根據 `buildAction`，只在 `ContentTargetFolders` 中指定 "contentFiles" 會將檔案放在 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下方。

`PackagePath` 可以是以分號分隔的一組目標路徑。 指定空的套件路徑會將檔案新增至套件的根目錄。 例如，下列會將 `libuv.txt` 新增至 `content\myfiles`、`content\samples` 和套件根目錄：

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

另外還有一個 MSBuild 屬性 `$(IncludeContentInPack)` ，預設為 `true` 。 如果這在任何專案上設定為 `false`，則 NuGet 套件不會包含該專案的內容。

您可以在上述任何專案上設定的其他封裝特定中繼資料，包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` 輸出中專案的集合和值 nuspec 。

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

使用授權運算式時，請使用 `PackageLicenseExpression` 屬性。 如需範例，請參閱 [授權運算式範例](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)。

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

若要深入瞭解由 org 接受的授權運算式和授權 NuGet ，請參閱 [授權中繼資料](nuspec.md#license)。

封裝授權檔案時，請使用 `PackageLicenseFile` 屬性來指定相對於封裝根目錄的封裝路徑。 此外，請確定檔案包含在套件中。 例如：

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

如需範例，請參閱 [授權檔案範例](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)。

> [!NOTE]
> `PackageLicenseExpression`一次只能指定、和中的一個 `PackageLicenseFile` `PackageLicenseUrl` 。

### <a name="packing-a-file-without-an-extension"></a>封裝沒有副檔名的檔案

在某些情況下，例如封裝授權檔案時，您可能會想要包含沒有副檔名的檔案。
基於歷史原因，請 NuGet  &  MSBuild 將沒有副檔名的路徑視為目錄。

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[沒有副檔名範例的](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)檔案。

### <a name="istool"></a>IsTool

使用 `MSBuild -t:pack -p:IsTool=true` 時，會將[輸出組件](#output-assemblies)案例中所指定的所有輸出檔案都複製至 `tools` 資料夾，而非 `lib` 資料夾。 請注意，這與 `DotNetCliTool` 不同，該項目是在 `.csproj` 檔案中設定 `PackageType` 所指定。

### <a name="packing-using-a-nuspec-file"></a>使用 `.nuspec` 檔案進行封裝

雖然建議您將通常是在檔案中的 [所有屬性包含](../reference/msbuild-targets.md#pack-target) 在 `.nuspec` 專案檔中，但您可以選擇使用檔案 `.nuspec` 來封裝專案。 若為使用的非 SDK 樣式專案 `PackageReference` ，您必須匯入， `NuGet.Build.Tasks.Pack.targets` 才能執行封裝工作。 您仍然需要還原專案，才能封裝檔案 nuspec 。  (SDK 樣式專案預設會包含套件目標。 ) 

專案檔的目標 framework 是不相關的，而且不會在封裝時使用 nuspec 。 下列三個 MSBuild 屬性與使用的封裝有關 `.nuspec` ：

1. `NuspecFile`：將用於封裝之 `.nuspec` 檔案的相對或絕對路徑。
1. `NuspecProperties`：以分號分隔的索引鍵=值組清單。 由於 MSBuild 命令列剖析的運作方式，必須指定多個屬性，如下所示： `-p:NuspecProperties="key1=value1;key2=value2"` 。  
1. `NuspecBasePath`：`.nuspec` 檔案的基底路徑。

如果使用 `dotnet.exe` 來封裝您的專案，則請使用下列這類命令：

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

如果使用 MSBuild 來封裝您的專案，則請使用下列這類命令：

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

請注意， nuspec 使用 dotnet.exe 或 msbuild 封裝，預設也會導致建立專案。 將 ```--no-build``` 屬性傳遞給 dotnet.exe （這相當於專案檔中的設定 ```<NoBuild>true</NoBuild> ``` ，以及專案檔中的設定），即可避免此情況 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 。

封裝檔案的 *.csproj* 檔案範例 nuspec 如下：

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

### <a name="advanced-extension-points-to-create-customized-package"></a>用來建立自訂套件的 Advanced 擴充點

`pack`目標提供在內部、目標 framework 特定組建中執行的兩個擴充點。 擴充點支援在套件中包含目標 framework 特定內容和元件：

- `TargetsForTfmSpecificBuildOutput` 目標：用於資料夾內的檔案 `lib` 或使用指定的資料夾 `BuildOutputTargetFolder` 。
- `TargetsForTfmSpecificContentInPackage` 目標：用於以外的檔案 `BuildOutputTargetFolder` 。

#### `TargetsForTfmSpecificBuildOutput`

撰寫自訂目標，並將其指定為屬性的值 `$(TargetsForTfmSpecificBuildOutput)` 。 若為任何需要在預設情況下進入 `BuildOutputTargetFolder` (lib 的檔案) ，目標應該將這些檔案寫入 ItemGroup `BuildOutputInPackage` ，並設定下列兩個中繼資料值：

- `FinalOutputPath`：檔案的絕對路徑;如果未提供，則會使用身分識別來評估來源路徑。
- `TargetPath`：當檔案需要移至內的子資料夾時， (選擇性的) 設定 `lib\<TargetFramework>` ，例如在其個別文化特性資料夾下的附屬元件。 預設為檔案的名稱。

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

#### `TargetsForTfmSpecificContentInPackage`

撰寫自訂目標，並將其指定為屬性的值 `$(TargetsForTfmSpecificContentInPackage)` 。 對於要包含在封裝中的任何檔案，目標應該將這些檔案寫入至 ItemGroup `TfmSpecificPackageFile` ，並設定下列選擇性中繼資料：

- `PackagePath`：檔案應在封裝中輸出的路徑。 NuGet 如果有多個檔案加入至相同的封裝路徑，則會發出警告。
- `BuildAction`：要指派給檔案的組建動作，只有在封裝路徑位於資料夾中時才需要 `contentFiles` 。 預設值為 "None"。

例如：
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
1. MSBuild將資料傳遞給 NuGet.Build.Tasks.dll
1. 執行還原
1. 下載套件
1. 撰寫資產檔案、目標和屬性

`restore`目標適用于使用 PackageReference 格式的專案。
`MSBuild 16.5+` 也提供格式的 [選擇支援](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) `packages.config` 。

> [!NOTE]
> `restore`目標[不應](#restoring-and-building-with-one-msbuild-command)與目標一起執行 `build` 。

### <a name="restore-properties"></a>還原屬性

其他還原設定可能來自 MSBuild 專案檔中的屬性。 您也可以從命令列，使用 `-p:` 參數設定值 (請參閱下列＜範例＞)。

| 屬性 | 描述 |
|--------|--------|
| `RestoreSources` | 以分號分隔的套件來源清單。 |
| `RestorePackagesPath` | 使用者套件資料夾路徑。 |
| `RestoreDisableParallel` | 限制逐一進行下載。 |
| `RestoreConfigFile` | 要套用之 `Nuget.Config` 檔案的路徑。 |
| `RestoreNoCache` | 若為 true，則避免使用快取的封裝。 請參閱 [管理全域封裝和](../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。 |
| `RestoreIgnoreFailedSources` | 如果為 true，請忽略失敗或遺漏的套件來源。 |
| `RestoreFallbackFolders` | 回溯資料夾，使用的方式與使用者套件資料夾相同。 |
| `RestoreAdditionalProjectSources` | 還原期間要使用的其他來源。 |
| `RestoreAdditionalProjectFallbackFolders` | 還原期間要使用的其他回溯資料夾。 |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | 排除指定的回溯資料夾 `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | `NuGet.Build.Tasks.dll` 的路徑。 |
| `RestoreGraphProjectInput` | 要還原的專案清單 (以分號分隔)，其中應包含絕對路徑。 |
| `RestoreUseSkipNonexistentTargets`  | 透過它收集項目時，會 MSBuild 決定是否使用優化來收集項目 `SkipNonexistentTargets` 。 若未設定，則預設為 `true` 。 當無法匯入專案的目標時，結果會是快速失敗的行為。 |
| `MSBuildProjectExtensionsPath` | 輸出檔案夾，預設為 `BaseIntermediateOutputPath` 和 `obj` 資料夾。 |
| `RestoreForce` | 在以 PackageReference 為基礎的專案中，即使上次還原成功，仍會強制解析所有相依性。 指定此旗標與刪除檔案類似 `project.assets.json` 。 這不會略過 HTTP 快取。 |
| `RestorePackagesWithLockFile` | 選擇使用鎖定檔案。 |
| `RestoreLockedMode` | 以鎖定模式執行還原。 這表示還原將不會重新評估相依性。 |
| `NuGetLockFilePath` | 鎖定檔案的自訂位置。 預設位置是專案的旁邊，而且名為 `packages.lock.json` 。 |
| `RestoreForceEvaluate` | 強制還原以重新計算相依性，並更新鎖定檔案而不發出任何警告。 |
| `RestorePackagesConfig` | 可使用 packages.config 還原專案的加入宣告參數。僅支援 `MSBuild -t:restore` 。 |
| `RestoreUseStaticGraphEvaluation` | 加入宣告參數以使用靜態圖形評估， MSBuild 而不是標準評估。 靜態圖表評估是一項實驗性功能，對於大型存放庫和解決方案來說更快。 |

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
| `project.assets.json` | 包含所有封裝參考的相依性圖形。 |
| `{projectName}.projectFileExtension.nuget.g.props` | MSBuild封裝所包含之 .props 的參考 |
| `{projectName}.projectFileExtension.nuget.g.targets` | MSBuild封裝中包含目標的參考 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>使用一個命令來還原和建立 MSBuild

由於 NuGet 可以還原可關閉 MSBuild 目標和 .props 的套件，因此會使用不同的全域屬性來執行還原和建立評估。
這表示下列將會有無法預測且通常不正確的行為。

```cli
msbuild -t:restore,build
```

 建議的方法是：

```cli
msbuild -t:build -restore
```

相同的邏輯也適用于類似的其他目標 `build` 。

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>還原 PackageReference 和 packages.config 專案 MSBuild

使用 MSBuild 16.5 + 時，也支援的 packages.config `msbuild -t:restore` 。

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore 僅適用于 `MSBuild 16.5+` 和 `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>使用 MSBuild 靜態圖形評估還原

> [!NOTE]
> 使用 MSBuild 16.6 版 +， NuGet 已新增實驗性功能，可從命令列使用靜態圖形評估，以大幅改善大型存放庫的還原時間。

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

或者，您可以藉由在 .Props 中設定屬性來啟用它。

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> 自2019年 Visual Studio 2019 和5.x 起 NuGet ，這項功能會被視為實驗性和加入宣告。 依照[ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803)的詳細資訊，以瞭解何時預設會啟用這項功能。

靜態圖形還原會變更還原的 msbuild 部分、專案讀取和評估，但不會變更還原演算法！ 還原演算法在所有工具上都相同， NuGet (NuGet .exe、 MSBuild .exe、dotnet.exe 和 Visual Studio) 。

在極少數的情況下，靜態圖形還原的行為可能會與目前的還原不同，而某些宣告的 PackageReferences 或 ProjectReferences 可能會遺失。

為了簡化您的想法，請在遷移至靜態圖形還原時，考慮執行：

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet*不* 應報告任何變更。 如果您看不到差異，請在[ NuGet /Home](https://github.com/nuget/home/issues/new)提出問題。

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
