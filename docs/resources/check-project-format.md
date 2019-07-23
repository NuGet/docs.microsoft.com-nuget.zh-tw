---
title: 識別專案格式
description: 說明如何識別您的專案格式
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843440"
---
# <a name="identify-the-project-format"></a>識別專案格式

NuGet 可搭配所有 .NET 專案使用。 不過，專案格式 (SDK 樣式或非 SDK 樣式) 決定取用及建立 NuGet 套件時所需的一些工具與方法。 SDK 樣式專案使用 [SDK 屬性](/dotnet/core/tools/csproj#additions)。 識別您的專案類型非常重要，因為您用於取用及建立 NuGet 套件的方法與工具取決於專案格式。 針對非 SDK 樣式專案，方法與工具也取決於專案是否已移轉為 `PackageReference` 格式。

您的專案是否為 SDK 樣式取決於用於建立專案的方法。 下表顯示預設專案格式與專案的關聯 CLI 工具 (當您使用 Visual Studio 2017 或更新版本建立專案時)。

| 專案&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 預設專案格式 | CLI 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 注意 |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK 樣式 | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | 使用 Visual Studio 2017 之前版本建立的專案是非 SDK 樣式。 使用 `nuget.exe` CLI。 |
| .NET Core | SDK 樣式 | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | 使用 Visual Studio 2017 之前版本建立的專案是非 SDK 樣式。 使用 `nuget.exe` CLI。 |
| .NET Framework | 非 SDK 樣式 | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | 使用其他方法建立的 .NET Framework 專案可能是 SDK 樣式專案。 針對那些專案，請改為使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。 |
| [已移轉](../reference/migrate-packages-config-to-package-reference.md) .NET 專案 | 非 SDK 樣式| 若要建立套件，請使用 [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) 來建立套件。 | 若要建立套件，建議使用 `msbuild -t:pack`。 否則，請使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。 已移轉的專案不是 SDK 樣式專案。 |

## <a name="check-the-project-format"></a>檢查專案格式

若您不確定專案是否為 SDK 樣式格式，請查看專案檔 (針對 C#，這是 *.csproj 檔案) 中 `<Project>` 元素中是否有 SDK 屬性。 若它存在，則專案為 SDK 樣式專案。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>在 Visual Studio 中檢查專案格式

若您在 Visual Studio 中工作，您可以使用下列其中一種方法快速檢查專案格式：

- 以滑鼠右鍵按一下 [方案總管] 中的專案，然後選取 [編輯 myprojectname.csproj]  。

   只有使用 SDK 樣式屬性的專案 (且必須使用 Visual Studio 2017 與更新版本) 才能使用此選項。 否則，請使用其他方法。

   ![編輯專案檔](media/edit-project-file.png)

   SDK 樣式專案會在專案檔中顯示 [SDK 屬性](/dotnet/core/tools/csproj#additions)。
   
- 從 [專案]  功能表，選擇 [卸載專案]  (或以滑鼠右鍵按一下專案並選擇 [卸載專案]  )。

   此專案將不會在專案檔中包括 SDK 屬性。 它不是 SDK 樣式專案。

   ![卸載專案](media/unload-project.png)

   接著，以滑鼠右鍵按一下卸載的專案並選擇 [編輯 myprojectname.csproj]  。

## <a name="see-also"></a>另請參閱

- [使用 dotnet CLI 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [使用 Visual Studio 建立 .NET Standard 套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [建立及發行 .NET Framework 套件 (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [NuGet 封裝和還原為 MSBuild 目標](../reference/msbuild-targets.md)
