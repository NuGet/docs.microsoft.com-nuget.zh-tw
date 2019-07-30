---
title: 使用 dotnet CLI 建立 NuGet 套件
description: NuGet 套件設計和建立程序詳細指南，包含檔案和版本控制這類關鍵決策點。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462462"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>使用 dotnet CLI 建立 NuGet 套件

不論套件的功能或所含程式碼為何，您都可以使用其中一個 CLI 工具 (`nuget.exe` 或 `dotnet.exe`) 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。 此文章說明如何使用 dotnet CLI 建立套件。 若要安裝 `dotnet` CLI，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。 從 Visual Studio 2017 開始，dotnet CLI 隨附於 .NET Core工作負載中。

針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，NuGet 會直接使用專案檔中的資訊來建立套件。 如需逐步教學課程，請參閱[使用 dotnet CLI 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)、[使用 Visual Studio 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)。

`msbuild -t:pack` 在功能上相當於 `dotnet pack`。 若要使用 MSBuild 進行建置，概念與此文章中所述相同，但是命令列命令會稍有不同。 同樣地，對於非 SDK 樣式的專案與 `<PackageReference>`，您可以使用 `msbuild /t:pack`。 在這些情節中，您需要將 NuGet.Build.Tasks.Pack 套件新增至其相依性。 請參閱 [NuGet 套件和還原為 MSBuild 目標](../reference/msbuild-targets.md)。

> [!IMPORTANT]
> 此主題適用於 [SDK 樣式](../resources/check-project-format.md)的專案，這通常是 .NET Core 與 .NET Standard 專案。

## <a name="set-properties"></a>設定屬性

建立套件時需要下列屬性。

- `PackageId`，套件識別碼，這在裝載套件的資源庫內必須是唯一的。 若未指定，則預設值為 `AssemblyName`。
- `Version`，*Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別[發行前版本](prerelease-packages.md)。 若未指定，則預設值為 1.0.0。
- 主機上應該會出現套件標題 (例如 nuget.org)
- `Authors`，作者與擁有者資訊。 若未指定，則預設值為 `AssemblyName`。
- `Company`，您的公司名稱。 若未指定，則預設值為 `AssemblyName`。

在 Visual Studio 中，您可以在專案屬性中設定這些值 (在 [方案總管] 中以滑鼠右鍵按一下專案，選擇 [屬性]  ，然後選取 [套件]  索引標籤)。 您也可以直接在專案檔 (`.csproj`) 中設定這些屬性。

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> 為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何套件資源上都必須是唯一的。

您還可以設定選擇性屬性，例如`Title`、`PackageDescription` 與 `PackageTags`，如 [MSBuild 套件目標](../reference/msbuild-targets.md#pack-target)、[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)，以及 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。

> [!NOTE]
> 針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。

如需宣告相依性以及指定版本號碼的詳細資料，請參閱[套件版本控制](../reference/package-versioning.md)。 使用 `<IncludeAssets>` 與 `<ExcludeAssets>` 屬性，也可以將來自相依性的資產直接用於套件中。 如需詳細資訊，請參閱[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>選擇唯一的套件識別碼並設定版本號碼

套件識別碼與版本號碼是專案中的兩個最重要值，因為它們可以唯一識別套件中所含的確切程式碼。

**套件識別碼的最佳做法：**

- **唯一性**：在 nuget.org 內，或只要資源庫裝載套件時，識別碼就必須是唯一的。 決定識別碼之前，請搜尋適用的資源庫，檢查是否已在使用名稱。 若要避免衝突，不錯的模式是使用您的公司名稱作為識別碼的第一個部分，例如 `Contoso.`。
- **命名空間類似名稱**：遵循與 .NET 中命名空間類似的模式，即使用點標記法，而非連字號。 例如，使用 `Contoso.Utility.UsefulStuff`，而非 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。 套件識別碼符合程式碼中所使用的命名空間時，取用者也會發現它十分有用。
- **範例套件**：如果您產生的範例程式碼套件示範如何使用另一個套件，請將 `.Sample` 附加為識別碼的尾碼，如 `Contoso.Utility.UsefulStuff.Sample` 所示 (範例套件當然會有與另一個套件的相依性)。建立範例套件時，請使用 `<IncludeAssets>` 中的 `contentFiles` 值。 在 `content` 資料夾中，於稱為 `\Samples\<identifier>` 的資料夾中排列範例程式碼，而這與 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相同。

**套件版本的最佳做法：**

- 一般而言，請設定套件版本，使其符合專案 (或組件)，但這不是絕對必要。 當您將套件限制為單一組件時，這很簡單。 整體來說，請記住，解析相依性時，NuGet 本身會處理套件版本，而非組件版本。
- 使用非標準版本方式時，請務必考慮使用 NuGet 版本控制規則，如[套件版本控制](../reference/package-versioning.md)中所述。 NuGet 大多[符合 semver 2 規範](../reference/package-versioning.md#semantic-versioning-200)。

> 如需相依性解析的相關資訊，請參閱[使用 PackageReference 的相依性解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)。 如需更深入了解版本控制的較舊資訊，請參閱這一系列的部落格文章。
>
> - [第 1 部分：接受 DLL 挑戰](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) \(英文\)
> - [第 2 部分：核心演算法](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) \(英文\)
> - [第 3 部分：透過繫結重新導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) \(英文\)

## <a name="run-the-pack-command"></a>執行 pack 命令

若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `dotnet pack` 命令，該命令也會自動建置專案：

```cli
# Uses the project file in the current folder by default
dotnet pack
```

輸出將顯示 `.nupkg` 檔案的路徑：

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

當您在方案上執行 `dotnet pack` 時，這會封裝方案中可封裝的所有專案 ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 屬性設定為 `true`)。

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
