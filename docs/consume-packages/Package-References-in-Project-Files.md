---
title: NuGet PackageReference 格式 (專案檔中的套件參考)
description: NuGet 4.0+ 和 VS2017 及 .NET Core 2.0 所支援之專案檔中的 NuGet PackageReference 詳細資料
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230612"
---
# <a name="package-references-packagereference-in-project-files"></a>專案檔中的套件參考 (PackageReference)

套件參考使用 `PackageReference` 節點，直接在專案檔中管理 NuGet 相依性 (而不是在個別的 `packages.config` 檔案中)。 使用 PackageReference 不會影響 NuGet 的其他方面；例如，仍會套用 `NuGet.config` 檔案中的設定 (包括套件來源)，如[常用的 NuGet 組態](configuring-nuget-behavior.md)中所述。

透過 PackageReference，您也可以使用 MSBuild 條件來選擇每個目標 framework 或其他群組的套件參考。 它也允許對相依性和內容流動進行細微控制。 (如需詳細資訊，請參閱 [NuGet pack and restore as MSBuild targetsNuGet](../reference/msbuild-targets.md) (NuGet 以 pack 與 restore 作為 MSBuild 目標)。)

## <a name="project-type-support"></a>專案類型支援

根據預設，PackageReference 會用於以 Windows 10 組建 15063 (Creators Update) 及更新版本為目標的 .NET Core 專案、.NET Standard 專案和 UWP 專案 (C++ UWP 專案除外)。 .NET Framework 專案支援 PackageReference，但目前預設為 `packages.config`。 若要使用 PackageReference，請將相依性從 `packages.config`[移轉](../consume-packages/migrate-packages-config-to-package-reference.md)至您的專案檔，然後移除 packages.config。

以完整的 .NET Framework 為目標的 ASP.NET 應用程式僅包含 PackageReference 的[有限支援](https://github.com/NuGet/Home/issues/5877) \(英文\)。 不支援 C++ 和 JavaScript 專案類型。

## <a name="adding-a-packagereference"></a>新增 PackageReference

使用下列語法在專案檔中新增相依性：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>控制相依性版本

指定套件版本的慣例和使用 `packages.config` 時一樣：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

在上述範例中，3.6.0 表示 >=3.6.0 的任何版本，但偏好最低版本，如[套件版本控制](../concepts/package-versioning.md#version-ranges)中所述。

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>針對沒有任何 PackageReference 的專案使用 PackageReference

進階：如果專案中未安裝任何套件 (專案檔中沒有 PackageReference，也沒有 packages.config 檔案)，但希望專案能還原為 PackageReference 樣式，您可以在您的專案檔中將專案屬性 RestoreProjectStyle 設定為 PackageReference。

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

如果您的參考專案為 PackageReference 樣式 (現有的 csproj 或 SDK 樣式專案)，這會很有用。 這會讓這些專案參考的套件成為您專案「過渡性」參考的套件。

## <a name="packagereference-and-sources"></a>PackageReference 和來源

在 PackageReference 專案中，可轉移的相依性版本會在還原時解析。 因此，在 PackageReference projects 中，所有來源都必須可供所有還原使用。 

## <a name="floating-versions"></a>浮動版本

[浮動版本](../concepts/dependency-resolution.md#floating-versions)支援 `PackageReference`：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>控制相依性資產

您可能純粹使用相依性作為開發載入器，不想要對取用套件的專案公開。 在此案例中，您可以使用 `PrivateAssets` 中繼資料控制這個行為。

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

下列中繼資料標記控制相依性資產：

| 標記 | 描述 | 預設值 |
| --- | --- | --- |
| IncludeAssets | 會取用這些資產 | all |
| ExcludeAssets | 不會取用這些資產 | none |
| PrivateAssets | 會取用這些資產，但不會流動至父專案 | contentfiles;分析器;建置 |

這些標記的可允許值如下，使用分號隔開多個值，但 `all` 和 `none` 必須單獨出現：

| 值 | 描述 |
| --- | ---
| compile | `lib` 資料夾的內容，以及專案是否能對該資料夾內的組件進行編譯的控制項 |
| runtime | `lib` 與 `runtimes` 資料夾的內容，以及是否能將這些組件複製到組建輸出目錄的控制項 |
| contentFiles | `contentfiles` 資料夾的內容 |
| build | `build` 資料夾中的 `.props` 與 `.targets` |
| buildMultitargeting | *（4.0）* `.props` 和 `.targets` 在 `buildMultitargeting` 資料夾中，適用于跨架構目標 |
| buildTransitive | *（5.0 +）* 在 `buildTransitive` 資料夾中 `.props` 和 `.targets`，適用于以可轉移方式傳遞至任何取用專案的資產。 請參閱[功能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)頁面 \(英文\)。 |
| analyzers | .NET 分析器 |
| native | `native` 資料夾的內容 |
| none | 以上皆不使用。 |
| all | 以上全部 (除了`none`) |

在下列範例中，除來自套件的內容檔案之外的所有項目都會被專案取用，除內容檔案和分析器之外的所有項目都會流動至父專案。

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

請注意，因為 `build` 不隨附於 `PrivateAssets`，所以目標與 props「會」流動至父專案。 例如，考慮到上述參考會用在建置名為 AppLogger 之 NuGet 套件的專案中。 AppLogger 可從 `Contoso.Utility.UsefulStuff` 取用目標與 props，如同專案可以取用 AppLogger。

> [!NOTE]
> 在 `.nuspec` 檔案中，當 `developmentDependency` 設定為 `true` 時可讓套件成為僅限開發相依性，這可防止套件被包含為其他套件的相依性。 使用 PackageReference *(NuGet 4.8+)* 時，此旗標也表示它在編譯時會排除編譯時間資產。 如需詳細資訊，請參閱 [PackageReference 的 DevelopmentDependency 支援](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) \(英文\)。

## <a name="adding-a-packagereference-condition"></a>新增 PackageReference 條件

您可以使用條件來控制是否包含套件，這些條件可以使用任何 MSBuild 變數或在目標或 props 檔案中定義的變數。 但目前只支援 `TargetFramework` 變數。

例如，假設您的目標是 `netstandard1.4` 以及 `net452`，但所擁有的相依性只適用於 `net452`。 在此情況下，您不希望取用套件的 `netstandard1.4` 專案新增該項不必要的相依性。 為避免這個問題，您要在 `PackageReference` 指定條件，如下所示：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

使用此專案的套件組建會顯示 Newtonsoft.Json 隨附為相依性，但僅適用於 `net452` 目標：

![使用 VS2017 對 PackageReference 套用條件的結果](media/PackageReference-Condition.png)

條件也可以套用在 `ItemGroup` 層級，並且套用至所有子系 `PackageReference` 項目：

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

這項功能適用 NuGet **5.0**或更新版本，以及 Visual Studio 2019 **16.0**或更高版本。

有時候，最好是從 MSBuild 目標參考封裝中的檔案。
在以 `packages.config` 為基礎的專案中，套件會安裝在相對於專案檔的資料夾中。 不過，在 PackageReference 中，套件[會從](../concepts/package-installation-process.md)[*全域套件*] 資料夾取用，這可能會因電腦而異。

為了橋樑該缺口，NuGet 引進了一個屬性，指向將取用套件的位置。

範例：

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

此外，NuGet 會自動為包含 [工具] 資料夾的套件產生屬性。

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

MSBuild 屬性和封裝身分識別的限制不相同，因此必須將封裝身分識別變更為 MSBuild 易記名稱，並在前面加上 `Pkg`一字。
若要確認所產生之屬性的確切名稱，請查看產生的[.props](../reference/msbuild-targets.md#restore-outputs)檔案。

## <a name="nuget-warnings-and-errors"></a>NuGet 警告和錯誤

*這項功能適用 NuGet **4.3**或更新版本，以及 Visual Studio 2017 **15.3**或更高版本。*

對於許多套件和還原案例，所有 NuGet 警告和錯誤都會進行編碼，並從 `NU****`開始。 所有的 NuGet 警告和錯誤都會列在[參考](../reference/errors-and-warnings.md)檔中。

NuGet 會觀察下列警告屬性：

- `TreatWarningsAsErrors`，將所有警告視為錯誤
- `WarningsAsErrors`，將特定警告視為錯誤
- `NoWarn`，隱藏整個專案或整個套件的特定警告。

例如：

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>隱藏 NuGet 警告

雖然建議您在套件和還原作業期間解決所有的 NuGet 警告，但在某些情況下，不一定要將它們強制執行。
若要隱藏警告專案範圍，請考慮執行下列動作：

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

有時警告只適用于圖形中的特定套件。 我們可以選擇在 PackageReference 專案上加入 `NoWarn`，以更有選擇性地隱藏該警告。 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>隱藏 Visual Studio 中的 NuGet 套件警告

在 Visual Studio 中，您也可以 [隱藏透過 IDE](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) 的警告。

## <a name="locking-dependencies"></a>鎖定相依性

*NuGet **4.9** 或更新版本搭配 Visual Studio 2017 **15.9** 或更新版本提供此功能。*

對 NuGet 還原的輸入是一組來自專案檔 (頂層或直接相依性) 的套件參考，而輸出是完整的套件相依性終止，包括可轉移相依性。 若輸入 PackageReference 清單未變更，NuGet 會嘗試一律產生相同的完整套件相依性終止。 不過，在一些情況下，無法這樣做。 例如:

* 當您使用如 `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 的浮動版本時。 雖然這裡的目的是在次套件還原時浮動到最新版本，在某些案例中，使用者在收到明確手勢時需要圖形鎖定為特定最新版本並浮動到更新的版本 (如果可用)。
* 會發行符合 PackageReference 版本需求的的較新套件版本。 例如， 

  * 第 1 天：若您指定 `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`，但 NuGet 存放庫上可用的版本是 4.1.0、4.2.0 與 4.3.0。 在此案例中，NuGet would 將會解析為 4.1.0 (最接近的最小版本)

  * 第 2 天：版本 4.0.0 發行。 NuGet 現在將會尋找精確相符項目並開始解析為 4.0.0

* 給定套件版本會從存放庫移除。 雖然 nuget.org 不允許套件刪除，但並非所有套件存放庫都有此限制式。 這會導致 NuGet 在無法解析為已刪除版本時尋找最佳相符項目。

### <a name="enabling-lock-file"></a>啟用鎖定檔案

若要保存完整的套件相依性終止，您可以透過設定專案的 MSBuild 屬性 `RestorePackagesWithLockFile` 來選擇啟用鎖定檔案功能：

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

若已設定此屬性，NuGet 還原將會產生鎖定檔案，也就是專案根目錄中列出所有套件相依性的 `packages.lock.json` 檔案。 

> [!Note]
> 一旦專案的根目錄中有 `packages.lock.json` 檔案，就一律會使用鎖定檔案來進行還原，即使是未設定 `RestorePackagesWithLockFile` 屬性也一樣。 因此，選擇啟用此功能的另一個方式在專案根目錄中建立虛設空白 `packages.lock.json` 檔案。

### <a name="restore-behavior-with-lock-file"></a>具有鎖定檔案的 `restore` 行為
若專案有鎖定檔案存在，NuGet 會使用此所鎖定檔案來執行 `restore`。 NuGet 會執行快速檢查以查看套件相依性中是否有變更，如專案檔 (或相依專案的檔案) 所述，而且若沒有變更，它只會還原鎖定檔案中所述的套件。 不會重新評估套件相依性。

若 NuGet 偵測到定義相依性中的變更 (如專案檔中所述)，它會重新評估套件圖表並更新鎖定檔案以反映專案的新套件終止。

針對 CI/CD 與其他案例，若不想即時變更套件相依性，您可以將 `lockedmode` 設定為 `true`：

針對 dotnet.exe，請執行：

```
> dotnet.exe restore --locked-mode
```

針對 msbuild.exe，請執行：

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

您也可以在您的專案檔中設定此條件式 MSBuild 屬性：

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

若鎖定模式是 `true`，還原將會還原鎖定檔案中所列的精確套件；若您在鎖定檔案建立之後更新專案的已定義套件相依性，則會失敗。

### <a name="make-lock-file-part-of-your-source-repository"></a>讓鎖定檔案成為您來源存放庫的一部分
若您要建置應用程式，可執行檔與討論的專案是相依性鏈結的開頭，則請將鎖定檔案存回原始程式碼存放庫，讓 NuGet 可以在還原期間使用。

不過，若您的專案是您不會發行的程式庫專案，或是其他專案所相依的一般程式碼專案，您**不應該**將鎖定檔案存回為您原始程式碼的一部分。 保留鎖定檔案並不會造成傷害，但在還原/建置相依於此一般程式碼專案的專案時，無法使用一般程式碼專案的鎖定套件相依性，如鎖定檔案中所列。

例如：

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

若 `ProjectA` 有對 `PackageX` 版本 `2.0.0` 的相依性，而且也參考相依於 `PackageX` 版本 `1.0.0` 的 `ProjectB`，則 `ProjectB` 的鎖定檔案將會列出對 `PackageX` 版本 `1.0.0` 的相依性。 不過，當 `ProjectA` 建立時，其鎖定檔案會包含 `PackageX` 版本 **`2.0.0`** 的相依性，而**不**是 `1.0.0` 如 `ProjectB`的鎖定檔案中所列。 因此，一般程式碼專案的鎖定檔案對於相依於它之專案的解析套件沒有多大決定權。

### <a name="lock-file-extensibility"></a>鎖定檔案擴充性

您使用鎖定檔案來控制還原的各種行為，如下所述：

| Nuget.exe 選項 | dotnet 選項 | MSBuild 同等選項 | 描述 |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | 選擇使用鎖定檔案。 |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | 針對還原啟用鎖定模式。 這在您想要可重複組建的 CI/CD 案例中很有用。|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | 對於專案中已定義浮動版本的套件而言，此選項非常實用。 根據預設，除非您使用此選項執行還原，否則 NuGet 還原將不會在每次還原時自動更新套件版本。 |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | 為專案定義自訂鎖定檔案位置。 根據預設，NuGet 支援根目錄的 `packages.lock.json`。 若您在相同的目錄中有多個專案，NuGet 支援專案特定鎖定檔案 `packages.<project_name>.lock.json` |
