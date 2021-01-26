---
title: 建立包含 COM Interop 組件的套件
description: 描述如何建立包含 COM Interop 組件的套件
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 0c663863673b50d0ba4969adf3a5d95151b2ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774496"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>建立包含 COM Interop 組件的 NuGet 套件

包含 COM Interop 組件的套件必須包含適當的[目標檔案](creating-a-package.md#include-msbuild-props-and-targets-in-a-package)，因此會使用 PackageReference 格式將正確的 `EmbedInteropTypes` 中繼資料新增至專案。 根據預設，使用 PackageReference 時，所有組件的 `EmbedInteropTypes` 中繼資料一律為 false，因此目標檔案會明確新增此中繼資料。 若要避免衝突，目標名稱應該是唯一的；在理想狀況下，使用套件名稱和所內嵌組件的組合，並將下列範例中的 `{InteropAssemblyName}` 取代為該值  (如需範例，請參閱 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop))。

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

請注意，使用 `packages.config` 管理格式時，新增套件中組件的參考會讓 NuGet 和 Visual Studio 檢查 COM Interop 組件，並將專案檔中的 `EmbedInteropTypes` 設定為 true。 在此情況下，會覆寫目標。

此外，根據預設，[組建資產不會轉移流動](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。 如這裡所述而撰寫的套件從專案對專案參考提取為可轉移相依性時，即會以不同的方式運作。 套件取用者允許它們流動的方式，是將 PrivateAssets 預設值修改為不包含組建。

<a name="creating-the-package"></a>