---
title: 建立包含 COM Interop 組件的套件
description: 描述如何建立包含 COM Interop 組件的套件
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: d0e368f43171ce71abc60b3e09d08b010d2d8880
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843480"
---
## <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="e4729-103">建立包含 COM Interop 組件的 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e4729-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="e4729-104">包含 COM Interop 組件的套件必須包含適當的[目標檔案](creating-a-package.md#include-msbuild-props-and-targets-in-a-package)，因此會使用 PackageReference 格式將正確的 `EmbedInteropTypes` 中繼資料新增至專案。</span><span class="sxs-lookup"><span data-stu-id="e4729-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="e4729-105">根據預設，使用 PackageReference 時，所有組件的 `EmbedInteropTypes` 中繼資料一律為 false，因此目標檔案會明確新增此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e4729-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="e4729-106">若要避免衝突，目標名稱應該是唯一的；在理想狀況下，使用套件名稱和所內嵌組件的組合，並將下列範例中的 `{InteropAssemblyName}` 取代為該值</span><span class="sxs-lookup"><span data-stu-id="e4729-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="e4729-107">(如需範例，請參閱 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop))。</span><span class="sxs-lookup"><span data-stu-id="e4729-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="e4729-108">請注意，使用 `packages.config` 管理格式時，新增套件中組件的參考會讓 NuGet 和 Visual Studio 檢查 COM Interop 組件，並將專案檔中的 `EmbedInteropTypes` 設定為 true。</span><span class="sxs-lookup"><span data-stu-id="e4729-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="e4729-109">在此情況下，會覆寫目標。</span><span class="sxs-lookup"><span data-stu-id="e4729-109">In this case the targets are overriden.</span></span>

<span data-ttu-id="e4729-110">此外，根據預設，[組建資產不會轉移流動](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="e4729-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="e4729-111">如這裡所述而撰寫的套件從專案對專案參考提取為可轉移相依性時，即會以不同的方式運作。</span><span class="sxs-lookup"><span data-stu-id="e4729-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="e4729-112">套件取用者允許它們流動的方式，是將 PrivateAssets 預設值修改為不包含組建。</span><span class="sxs-lookup"><span data-stu-id="e4729-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>