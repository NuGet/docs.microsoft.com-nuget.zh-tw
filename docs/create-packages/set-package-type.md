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
# <a name="set-a-nuget-package-type"></a>設定 NuGet 套件類型

您可以使用一個以上的 *封裝類型* 來標記套件，以指出其預定用途。

## <a name="known-package-types"></a>已知的封裝類型

- `Dependency` 類型套件會將建置或執行階段資產新增至程式庫和應用程式，並且可以安裝至任何專案類型 (假設它們相容)。

- `DotnetTool` 類型套件是可由 [DOTNET CLI](/dotnet/articles/core/tools/index)安裝的 .net 工具。

- `Template` 型別套件提供 [自訂範本](/dotnet/core/tools/custom-templates) ，可用來建立應用程式、服務、工具或類別庫等檔案或專案。

未標示類型的套件 (包含使用舊版 NuGet 所建立的所有套件) 預設為 `Dependency` 類型。

> [!NOTE]
> NuGet 3.5 已新增對套件類型的支援。
> 如果您不需要自訂套件類型，最好 *不要* 明確地設定套件類型。
> `Dependency`當未指定任何類型時，NuGet 會預設為類型。

## <a name="custom-package-types"></a>自訂套件類型

您可以使用一或多個自訂套件類型來標記套件（如果其使用不符合 [已知套件類型](#known-package-types)）。

例如，假設 `Contoso` 應用程式的客戶可以安裝延伸模組。 應用程式可能需要延伸模組作者使用自訂套件類型，將 `ContosoExtension` 其套件識別為遵循必要慣例的適當延伸模組。

> [!WARNING]
> Visual Studio 或 nuget.exe 無法安裝具有自訂套件類型的封裝。 如需詳細資訊，請參閱 [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) 。

# <a name="using-dotnet-cli"></a>[使用 dotnet CLI](#tab/dotnet)

封裝類型可以在專案檔 () 中設定 `.csproj` ：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

具有多個預定用途的封裝可以使用分隔符號，以多個套件類型標示 `;` ：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

封裝類型可以使用 `,` 封裝類型和其字串之間的分隔符號進行版本設定 [`Version`](/dotnet/api/system.version) ：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[使用 nuget.exe](#tab/nugetexe)

封裝類型是在專案底下的節點中設定 `.nuspec` `packageTypes\packageType` `<metadata>` ：

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

具有多個預定用途的封裝可能會以多個套件類型標示：

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

封裝類型可以使用字串進行版本設定 [`Version`](/dotnet/api/system.version) ：

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

封裝類型字串的格式與封裝識別碼完全相同。 也就是說，套件類型是符合正則運算式的不區分大小寫字串 `^\w+([_.-]\w+)*$` ，其中至少有一個字元且最多100個字元。

如果有提供，則套件類型版本為 [`Version`](/dotnet/api/system.version) 字串。 封裝類型版本是選擇性的，預設值為 `0.0` 。
