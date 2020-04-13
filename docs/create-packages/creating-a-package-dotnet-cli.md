---
title: 使用 dotnet CLI 建立 NuGet 套件
description: NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類索引鍵決策點。
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230569"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>使用 dotnet CLI 建立 NuGet 套件

不論套件的功能或所含程式碼為何，您都可以使用其中一個 CLI 工具 (`nuget.exe` 或 `dotnet.exe`) 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。 此文章說明如何使用 dotnet CLI 建立套件。 若要安裝 `dotnet` CLI，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。 從 Visual Studio 2017 開始，dotnet CLI 隨附於 .NET Core工作負載中。

針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，NuGet 會直接使用專案檔中的資訊來建立套件。 如需逐步執行教學課程，請參閱[使用 dotnet CLI 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)或[使用 Visual Studio 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)。

`msbuild -t:pack` 在功能上相當於 `dotnet pack`。 若要使用 MSBuild 進行建置，請參閱[使用 MSBuild 建立 NuGet 套件](creating-a-package-msbuild.md)。

> [!IMPORTANT]
> 此主題適用於 [SDK 樣式](../resources/check-project-format.md)的專案，這通常是 .NET Core 與 .NET Standard 專案。

## <a name="set-properties"></a>設定屬性

建立套件時需要下列屬性。

- `PackageId`，套件識別碼，這在裝載套件的資源庫內必須是唯一的。 若未指定，則預設值為 `AssemblyName`。
- `Version`，*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](prerelease-packages.md)。 若未指定，則預設值為 1.0.0。
- 主機上應該會出現套件標題 (例如 nuget.org)
- `Authors`，作者與擁有者資訊。 若未指定，則預設值為 `AssemblyName`。
- `Company`，您的公司名稱。 若未指定，則預設值為 `AssemblyName`。

在 Visual Studio 中，您可以在專案屬性中設定這些值 (在 [方案總管] 中以滑鼠右鍵按一下專案，選擇 [屬性]****，然後選取 [套件]**** 索引標籤)。 您也可以直接在專案檔 (`.csproj`) 中設定這些屬性。

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> 為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何套件資源上都必須是唯一的。

下列範例顯示一個簡單且完整的專案檔，其中會包含這些屬性。 (您可以使用 `dotnet new classlib` 命令來建立新的預設專案)。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

您還可以設定選擇性屬性，例如`Title`、`PackageDescription` 與 `PackageTags`，如 [MSBuild 套件目標](../reference/msbuild-targets.md#pack-target)、[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)，以及 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。

> [!NOTE]
> 針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。

如需宣告相依性及指定版本號碼的詳細資料，請參閱[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)和[套件版本控制](../concepts/package-versioning.md)。 使用 `<IncludeAssets>` 與 `<ExcludeAssets>` 屬性，也可以將來自相依性的資產直接用於套件中。 如需詳細資訊，請參閱[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

## <a name="add-an-optional-description-field"></a>新增選擇的標題欄位

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>選擇唯一的套件識別碼並設定版本號碼

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>執行 pack 命令

若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `dotnet pack` 命令，該命令也會自動建置專案：

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

輸出會顯示 `.nupkg` 檔案的路徑。

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>建置時自動產生套件

若要在您執行 `dotnet build` 時自動執行 `dotnet pack`，請將下列程式行加入專案檔的 `<PropertyGroup>` 中：

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

在解決方案`dotnet pack`上執行時,這將打包解決方案中可打包的所有專案[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties)(屬性設置`true`為)。

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

- [套件版本控制](../concepts/package-versioning.md)
- [支援多個目標 Framework](../create-packages/multiple-target-frameworks-project-file.md)
- [新增包圖示](../reference/nuspec.md#icon)
- [原始程式檔和組態檔的轉換](../create-packages/source-and-config-file-transformations.md)
- [當地語系化](../create-packages/creating-localized-packages.md)
- [預發行版本](../create-packages/prerelease-packages.md)
- [設定套件類型](../create-packages/set-package-type.md)
- [建立包含 COM Interop 組件的套件](../create-packages/author-packages-with-COM-interop-assemblies.md)

最後，請注意其他套件類型：

- [本機包](../guides/native-packages.md)
- [符號套件](../create-packages/symbol-packages-snupkg.md)
