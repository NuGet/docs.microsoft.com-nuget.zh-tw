---
title: NuGet PackageReference 格式 (專案檔中的套件參考)
description: NuGet 4.0+ 和 VS2017 及 .NET Core 2.0 所支援之專案檔中的 NuGet PackageReference 詳細資料
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: e4df15be1f29e2c611876aaa49e16ac7d1823938
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248451"
---
# <a name="package-references-packagereference-in-project-files"></a>專案檔中的套件參考 (PackageReference)

套件參考使用 `PackageReference` 節點，直接在專案檔中管理 NuGet 相依性 (而不是在個別的 `packages.config` 檔案中)。 使用 PackageReference 不會影響 NuGet 的其他方面；例如，仍會套用 `NuGet.config` 檔案中的設定 (包括套件來源)，如[設定 NuGet 行為](configuring-nuget-behavior.md)中所述。

使用 PackageReference 也可讓您使用 MSBuild 條件，依目標 Framework、組態、平台或其他群組來選擇套件參考。 它也允許對相依性和內容流動進行細微控制。 (如需詳細資訊，請參閱 [NuGet pack and restore as MSBuild targetsNuGet](../reference/msbuild-targets.md) (NuGet 以 pack 與 restore 作為 MSBuild 目標)。)

根據預設，PackageReference 會用於以 Windows 10 組建 15063 (Creators Update) 及更新版本為目標的 .NET Core 專案、.NET Standard 專案和 UWP 專案 (C++ UWP 專案除外)。 .NET Framework 專案支援 PackageReference，但目前預設為 `packages.config`。 若要使用 PackageReference，請將相依性從 `packages.config` 移轉至您的專案檔，然後移除 packages.config。

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

在上述範例中，3.6.0 表示 >=3.6.0 的任何版本，但偏好最低版本，如[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中所述。

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

## <a name="floating-versions"></a>浮動版本

[浮動版本](../consume-packages/dependency-resolution.md#floating-versions)支援 `PackageReference`：

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

| 標記 | 說明 | 預設值 |
| --- | --- | --- |
| IncludeAssets | 會取用這些資產 | 全部 |
| ExcludeAssets | 不會取用這些資產 | 無 |
| PrivateAssets | 會取用這些資產，但不會流動至父專案 | contentfiles;分析器;建置 |

這些標記的可允許值如下，使用分號隔開多個值，但 `all` 和 `none` 必須單獨出現：

| 值 | 說明 |
| --- | ---
| compile | `lib` 資料夾的內容，以及專案是否能對該資料夾內的組件進行編譯的控制項 |
| 執行階段 | `lib` 與 `runtimes` 資料夾的內容，以及是否能將這些組件複製到組建輸出目錄的控制項 |
| contentFiles | `contentfiles` 資料夾的內容 |
| build | `build` 資料夾中的 props 和目標 |
| 分析器 | .NET 分析器 |
| native | `native` 資料夾的內容 |
| 無 | 以上皆不使用。 |
| 全部 | 以上全部 (除了`none`) |

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

## <a name="locking-dependencies"></a>鎖定相依性
*NuGet **4.9** 或更新版本搭配 Visual Studio 2017 **15.9** 或更新版本提供此功能。*

對 NuGet 還原的輸入是一組來自專案檔 (頂層或直接相依性) 的套件參考，而輸出是完整的套件相依性終止，包括可轉移相依性。 若輸入 PackageReference 清單未變更，NuGet 會嘗試一律產生相同的完整套件相依性終止。 不過，在一些情況下，無法這樣做。 例如：

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
若 `ProjectA` 有對 `PackageX` 版本 `2.0.0` 的相依性，而且也參考相依於 `PackageX` 版本 `1.0.0` 的 `ProjectB`，則 `ProjectB` 的鎖定檔案將會列出對 `PackageX` 版本 `1.0.0` 的相依性。 不過，當建置 `ProjectA` 時，其鎖定檔案將會包含對 `PackageX` 版本 **`2.0.0`** 的相依性，而**非** `1.0.0` (如 `ProjectB` 的鎖定檔案所列)。 因此，一般程式碼專案的鎖定檔案對於相依於它之專案的解析套件沒有多大決定權。

### <a name="lock-file-extensibility"></a>鎖定檔案擴充性
您使用鎖定檔案來控制還原的各種行為，如下所述：

| 選項 | MSBuild 同等選項 | 
|:---  |:--- |
| `--use-lock-file` | 專案的鎖定檔案啟動程序使用。 或者，您可以在專案檔中設定 `RestorePackagesWithLockFile` 屬性 | 
| `--locked-mode` | 針對還原啟用鎖定模式。 這在您想要取得可重複組建的 CI/CD 案例中非常實用。 透過將 `RestoreLockedMode` MSBuild 屬性設定為 `true`，就可以達到這個目的 |  
| `--force-evaluate` | 對於專案中已定義浮動版本的套件而言，此選項非常實用。 根據預設，NuGet 還原將不會在每次還原時自動更新套件版本，除非您搭配 `--force-evaluate` 選項執行還原。 |
| `--lock-file-path` | 為專案定義自訂鎖定檔案位置。 這也可以透過設定 MSBuild 屬性 `NuGetLockFilePath` 來完成。 根據預設，NuGet 支援根目錄的 `packages.lock.json`。 若您在相同的目錄中有多個專案，NuGet 支援專案特定鎖定檔案 `packages.<project_name>.lock.json` |
