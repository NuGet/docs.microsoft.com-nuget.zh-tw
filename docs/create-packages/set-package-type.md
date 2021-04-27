---
title: 設定 NuGet 套件類型
description: 描述套件類型以指出套件的預定用途。
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067269"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="9f12a-103">設定 NuGet 套件類型</span><span class="sxs-lookup"><span data-stu-id="9f12a-103">Set a NuGet package type</span></span>

<span data-ttu-id="9f12a-104">您可以使用一個以上的 *封裝類型* 來標記套件，以指出其預定用途。</span><span class="sxs-lookup"><span data-stu-id="9f12a-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="9f12a-105">已知的封裝類型</span><span class="sxs-lookup"><span data-stu-id="9f12a-105">Known package types</span></span>

- <span data-ttu-id="9f12a-106">`Dependency` 類型套件會將建置或執行階段資產新增至程式庫和應用程式，並且可以安裝至任何專案類型 (假設它們相容)。</span><span class="sxs-lookup"><span data-stu-id="9f12a-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="9f12a-107">`DotnetTool` 類型套件是可由 [DOTNET CLI](/dotnet/articles/core/tools/index)安裝的 .net 工具。</span><span class="sxs-lookup"><span data-stu-id="9f12a-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="9f12a-108">`Template` 型別套件提供 [自訂範本](/dotnet/core/tools/custom-templates) ，可用來建立應用程式、服務、工具或類別庫等檔案或專案。</span><span class="sxs-lookup"><span data-stu-id="9f12a-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="9f12a-109">未標示類型的套件 (包含使用舊版 NuGet 所建立的所有套件) 預設為 `Dependency` 類型。</span><span class="sxs-lookup"><span data-stu-id="9f12a-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="9f12a-110">NuGet 3.5 已新增對套件類型的支援。</span><span class="sxs-lookup"><span data-stu-id="9f12a-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="9f12a-111">如果您不需要自訂套件類型，最好 *不要* 明確地設定套件類型。</span><span class="sxs-lookup"><span data-stu-id="9f12a-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="9f12a-112">`Dependency`當未指定任何類型時，NuGet 會預設為類型。</span><span class="sxs-lookup"><span data-stu-id="9f12a-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="9f12a-113">自訂套件類型</span><span class="sxs-lookup"><span data-stu-id="9f12a-113">Custom package types</span></span>

<span data-ttu-id="9f12a-114">您可以使用一或多個自訂套件類型來標記套件（如果其使用不符合 [已知套件類型](#known-package-types)）。</span><span class="sxs-lookup"><span data-stu-id="9f12a-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="9f12a-115">例如，假設 `Contoso` 應用程式的客戶可以安裝延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9f12a-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="9f12a-116">應用程式可能需要延伸模組作者使用自訂套件類型，將 `ContosoExtension` 其套件識別為遵循必要慣例的適當延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9f12a-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="9f12a-117">Visual Studio 或 nuget.exe 無法安裝具有自訂套件類型的封裝。</span><span class="sxs-lookup"><span data-stu-id="9f12a-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="9f12a-118">如需詳細資訊，請參閱 [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) 。</span><span class="sxs-lookup"><span data-stu-id="9f12a-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="9f12a-119">使用 dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="9f12a-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="9f12a-120">封裝類型可以在專案檔 () 中設定 `.csproj` ：</span><span class="sxs-lookup"><span data-stu-id="9f12a-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="9f12a-121">具有多個預定用途的封裝可以使用分隔符號，以多個套件類型標示 `;` ：</span><span class="sxs-lookup"><span data-stu-id="9f12a-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="9f12a-122">封裝類型可以使用 `,` 封裝類型和其字串之間的分隔符號進行版本設定 [`Version`](/dotnet/api/system.version) ：</span><span class="sxs-lookup"><span data-stu-id="9f12a-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="9f12a-123">使用 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="9f12a-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="9f12a-124">封裝類型是在專案底下的節點中設定 `.nuspec` `packageTypes\packageType` `<metadata>` ：</span><span class="sxs-lookup"><span data-stu-id="9f12a-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="9f12a-125">具有多個預定用途的封裝可能會以多個套件類型標示：</span><span class="sxs-lookup"><span data-stu-id="9f12a-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="9f12a-126">封裝類型可以使用字串進行版本設定 [`Version`](/dotnet/api/system.version) ：</span><span class="sxs-lookup"><span data-stu-id="9f12a-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="9f12a-127">封裝類型字串的格式與封裝識別碼完全相同。</span><span class="sxs-lookup"><span data-stu-id="9f12a-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="9f12a-128">也就是說，套件類型是符合正則運算式的不區分大小寫字串 `^\w+([_.-]\w+)*$` ，其中至少有一個字元且最多100個字元。</span><span class="sxs-lookup"><span data-stu-id="9f12a-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="9f12a-129">如果有提供，則套件類型版本為 [`Version`](/dotnet/api/system.version) 字串。</span><span class="sxs-lookup"><span data-stu-id="9f12a-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="9f12a-130">封裝類型版本是選擇性的，預設值為 `0.0` 。</span><span class="sxs-lookup"><span data-stu-id="9f12a-130">The package type version is optional and defaults to `0.0`.</span></span>
