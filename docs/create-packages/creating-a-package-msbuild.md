---
title: 使用 MSBuild 建立 NuGet 套件
description: NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類索引鍵決策點。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: a0db6dc95ffa5ad73741ae53a6be9d6f937c1dbf
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833224"
---
# <a name="create-a-nuget-package-using-msbuild"></a>使用 MSBuild 建立 NuGet 套件

當您從程式碼建立 NuGet 套件時，會將該功能封裝至可由任意數目的其他開發人員共用和使用的元件。 本文說明如何使用 MSBuild 建立套件。 MSBuild 會使用每個包含 NuGet 的 Visual Studio 工作負載來進行預先安裝。 此外，您也可以透過 dotnet CLI，搭配 [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild) 使用 MSBuild。

針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，NuGet 會直接使用專案檔中的資訊來建立套件。  針對使用 `<PackageReference>` 的非 SDK 樣式專案，NuGet 也會使用專案檔來建立套件。

SDK 樣式的專案預設會提供套件功能。 針對非 SDK 樣式的 PackageReference 專案，您必須將 NuGet.Build.Tasks.Pack 套件新增至專案相依性。 如需 MSBuild 套件目標的詳細資訊，請參閱 [NuGet 套件和還原為 MSBuild 目標](../reference/msbuild-targets.md)。

建立套件的命令 `msbuild -t:pack` 是相當於 `dotnet pack` 的功能。

> [!IMPORTANT]
> 本主題適用於 [SDK 樣式](../resources/check-project-format.md)的專案 (通常是 .NET Core 和 .NET Standard 專案)，以及適用於使用 PackageReference 的非 SDK 樣式專案。

## <a name="set-properties"></a>設定屬性

建立套件時需要下列屬性。

- `PackageId`，套件識別碼，這在裝載套件的資源庫內必須是唯一的。 若未指定，則預設值為 `AssemblyName`。
- `Version`，*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](prerelease-packages.md)。 若未指定，則預設值為 1.0.0。
- 主機上應該會出現套件標題 (例如 nuget.org)
- `Authors`，作者與擁有者資訊。 若未指定，則預設值為 `AssemblyName`。
- `Company`，您的公司名稱。 若未指定，則預設值為 `AssemblyName`。

在 Visual Studio 中，您可以在專案屬性中設定這些值 (在 [方案總管] 中以滑鼠右鍵按一下專案，選擇 [屬性]  ，然後選取 [套件]  索引標籤)。 您也可以直接在專案檔 ( *.csproj*) 中設定這些屬性。

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> 為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何套件資源上都必須是唯一的。

下列範例顯示一個簡單且完整的專案檔，其中會包含這些屬性。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

您還可以設定選擇性屬性，例如`Title`、`PackageDescription` 與 `PackageTags`，如 [MSBuild 套件目標](../reference/msbuild-targets.md#pack-target)、[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)，以及 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。

> [!NOTE]
> 針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。

如需宣告相依性及指定版本號碼的詳細資料，請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)和[套件版本控制](../reference/package-versioning.md)。 使用 `<IncludeAssets>` 與 `<ExcludeAssets>` 屬性，也可以將來自相依性的資產直接用於套件中。 如需詳細資訊，請參閱[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>選擇唯一的套件識別碼並設定版本號碼

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>新增 NuGet.Build.Tasks.Pack 套件

如果您使用 MSBuild 搭配非 SDK 樣式的專案和 PackageReference，請將 NuGet.Build.Tasks.Pack 套件新增至您的專案。

1. 開啟專案檔，並在 `<PropertyGroup>` 元素之後新增下列內容：

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. 開啟開發人員命令提示字元 (在 [搜尋]  方塊中，輸入**開發人員命令提示字元**)。

   您通常想要從 [開始]  功能表啟動適用於 Visual Studio 的開發人員命令提示字元，因為它將使用適用於 MSBuild 的所有必要路徑來設定。

3. 切換至包含專案檔的資料夾，並輸入下列命令以安裝 NuGet.Build.Tasks.Pack 套件。

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   確定 MSBuild 輸出會指出組建已順利完成。

## <a name="run-the-msbuild--tpack-command"></a>執行 msbuild -t:pack 命令

若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `msbuild -t:pack` 命令，該命令也會自動建置專案：

在開發人員命令提示字元中，輸入下列命令：

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

輸出會顯示 `.nupkg` 檔案的路徑。

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>建置時自動產生套件

若要在您建置或還原專案時自動執行 `msbuild -t:pack`，請將下一行新增至專案檔的 `<PropertyGroup>` 中：

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

當您在解決方案上執行 `msbuild -t:pack` 時，這會封裝解決方案中可封裝的所有專案 ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 屬性會設定為 `true`)。

> [!NOTE]
> 當您自動產生套件時，封裝的時間會增加專案的建置時間。

### <a name="test-package-installation"></a>測試套件安裝

發行套件之前，您通常會想要測試將套件安裝至專案的程序。 測試可確定必要檔案最後都在專案的正確位置。

您可以使用一般[套件安裝步驟](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)，以在 Visual Studio 中或命令列上手動測試安裝。

> [!IMPORTANT]
> 套件是不可變的。 如果您更正了問題，請變更套件的內容並再次封裝，當您重新測試時，仍會使用舊版套件，直到您[清除全域套件](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)資料夾為止。 在測試每個組建上未使用唯一發行前版本標籤的套件時，這關係重大。

## <a name="next-steps"></a>後續步驟

建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../nuget-org/publish-a-package.md)中所述。

您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：

- [NuGet 封裝和還原為 MSBuild 目標](../reference/msbuild-targets.md)
- [套件版本控制](../reference/package-versioning.md)
- [支援多個目標架構](../create-packages/multiple-target-frameworks-project-file.md)
- [原始程式檔和組態檔的轉換](../create-packages/source-and-config-file-transformations.md)
- [當地語系化](../create-packages/creating-localized-packages.md)
- [發行前版本](../create-packages/prerelease-packages.md)
- [設定套件類型](../create-packages/set-package-type.md)
- [建立包含 COM Interop 組件的套件](../create-packages/author-packages-with-COM-interop-assemblies.md)

最後，請注意其他套件類型：

- [原生套件](../create-packages/native-packages.md)
- [符號套件](../create-packages/symbol-packages.md)
