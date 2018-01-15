---
title: "Visual Studio 專案檔中的 NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "NuGet 4.0+ 和 VS2017 所支援之專案檔中的 NuGet PackageReference 詳細資料"
keywords: "NuGet 套件相依性, 套件參考, 專案檔, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a>專案檔中的套件參考 (PackageReference)

使用 `PackageReference` 節點的套件參考，可讓您直接在專案檔中管理 NuGet 相依性，不需要個別的 `packages.config` 或 `project.json` 檔案。 這個方法不會影響 NuGet 的其他方面，例如，仍會套用 `NuGet.Config` 檔案中的設定 (包括套件來源)，如[設定 NuGet 行為](Configuring-NuGet-Behavior.md)中所述。

> [!Important]
> 目前，Visual Studio 2017 僅支援以 Windows 10 組建 15063 (Creators Update) 為目標的 .NET Core 專案、.NET Standard 專案和 UWP 專案套件參考。

`PackageReference` 方法可讓您使用 MSBuild 條件，依目標 Framework、組態、平台或其他分組來選擇套件參考。 它也允許對相依性和內容流動進行細微控制。 就行為和[相依性解析](Dependency-Resolution.md)而言，這和使用 `project.json` 相同。

如需 MSBuild 與專案檔中套件參考整合的詳細資料，請參閱 [NuGet 套件與還原為 MSBuild 目標](../schema/msbuild-targets.md)。

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

指定套件版本的慣例和使用 `packages.config` 或 `project.json` 一樣：

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

在上述範例中，3.6.0 表示 >=3.6.0 的任何版本，但偏好最低版本，如[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中所述。

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

| 標記 | 描述 | 預設值 |
| --- | --- | --- |
| IncludeAssets | 會取用這些資產 | 全部 |
| ExcludeAssets | 不會取用這些資產 | 無 | 
| PrivateAssets | 會取用這些資產，但不會流動至父專案 | contentfiles;分析器;建置 |


這些標記的可允許值如下，使用分號隔開多個值，但 `all` 和 `none` 必須單獨出現：

| 值 | 描述 |
| --- | ---
| compile | `lib` 資料夾的內容 |
| 執行階段 | `runtime` 資料夾的內容 |
| contentFiles | `contentfiles` 資料夾的內容 |
| 組建 | `build` 資料夾中的 props 和目標 |
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
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

使用此專案的套件組建會顯示 Newtonsoft.json 隨附為相依性，但僅適用於 `net452` 目標：

![使用 VS2017 對 PackageReference 套用條件的結果](media/PackageReference-Condition.png)

條件也可以套用在 `ItemGroup` 層級，並且套用至所有子系 `PackageReference` 項目：

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
