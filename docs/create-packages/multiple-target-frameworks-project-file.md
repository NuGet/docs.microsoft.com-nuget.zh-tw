---
title: 將專案檔中的 NuGet 套件設為多個目標
description: 將目標設為單一 NuGet 套件內多個 .NET Framework 版本之各種方法的描述。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: b7870bb6aac39f0865d88efc8c16751fdbecc3a8
ms.sourcegitcommit: cae759ad8518c049575a30ad3bf04fe5d06244fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2019
ms.locfileid: "68616772"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>在您的專案檔中支援多個 .NET Framework 版本

當您第一次建立專案時，我們建議您建立 .NET Standard 類別庫，因為它可為最廣泛的使用專案提供相容性。 根據預設，若使用 .NET Standard，您必須將[跨平台支援](/dotnet/standard/library-guidance/cross-platform-targeting)新增至 .NET 程式庫。 不過，在某些情節下，您可能也需要包含以特定架構為目標的程式碼。 此文章顯示如何針對 [SDK 樣式](../resources/check-project-format.md)專案執行此作業。

針對 SDK 樣式專案，您可以在專案檔中設定多目標架構 ([TFM](/dotnet/standard/frameworks)) 的支援，然後使用 `dotnet pack` 或 `msbuild /t:pack` 來建立套件。

> [!NOTE]
> nuget.exe CLI 不支援封裝 SDK 樣式專案，因此您應該只使用 `dotnet pack` 或 `msbuild /t:pack`。 我們建議您改為在專案檔中包含通常位於 `.nuspec` 檔案中的[所有屬性](../reference/msbuild-targets.md#pack-target)。 若要在非 SDK 樣式專案中以多個 .NET Framework 版本為目標，請參閱[支援多個 .NET Framework 版本](supporting-multiple-target-frameworks.md)。

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>建立支援多個 .NET Framework 版本的專案

1. 在 Visual Studio 中建立新 .NET Standard 類別庫，或使用 `dotnet new classlib`。

   我們建議您建立 .NET Standard 類別庫，以獲得最佳相容性。

2. 編輯 *.csproj* 檔案以支援目標 Framework。

   例如，將 `<TargetFramework>netstandard2.0</TargetFramework>` 變更為 `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`。

   請務必將 XML 元素從單數變更為複數 (將 "s" 新增至開頭和結束標籤)。

3. 如果您有任何只能在一個 TFM 中運作的程式碼，您可以使用 `#if NET45` 或 `#if NETSTANDARD20` 來分隔 TFM 相依程式碼。 (如需詳細資訊，請參閱[如何使用多目標](/dotnet/core/tutorials/libraries#how-to-multitarget)。)例如，您可以使用下列程式碼：

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. 將任何您想要的 NuGet 中繼資料以 MSBuild 屬性新增至 *.csproj*。

   如需可用套件中繼資料與 MSBuild 屬性名稱的清單，請參閱[套件目標](../reference/msbuild-targets.md#pack-target)。 另請參閱[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

   如果您想要將組建相關屬性與 NuGet 中繼資料分開，您可以使用不同的 `PropertyGroup`，或將 NuGet 屬性放在另一個檔案中，並使用 MSBuild 的 `Import` 指示詞來包含它。 從 MSBuild 15.0 開始也支援 `Directory.Build.Props` 與 `Directory.Build.Targets`。

5. 現在，使用 `dotnet pack`，所產生的 *.nupkg* 會以 .NET Standard 2.0 與 .NET Framework 4.5 為目標。

以下是使用上述步驟與 .NET Core SDK 2.2 所產生的 *.csproj* 檔案。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>另請參閱

* [如何指定目標 Framework](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [跨平台目標](/dotnet/standard/library-guidance/cross-platform-targeting)