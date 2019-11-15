---
title: 使用 dotnet CLI 建立及發佈 NuGet 套件
description: 使用 .NET Core CLI、dotnet 建立和發行 NuGet 套件的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8727f67608593e6ae8b96daa81b7423782dfc219
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096935"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>快速入門：建立及發佈套件 (dotnet CLI)

使用 `dotnet` 命令列介面 (CLI) 從 .NET 類別庫建立 NuGet 套件，並將它發行到 nuget.org 是個簡單的程序。

## <a name="prerequisites"></a>Prerequisites

1. 安裝 [.NET Core SDK](https://www.microsoft.com/net/download/)，其中包括 `dotnet` CLI。 從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。

1. 如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) \(英文\)。 建立新的帳戶會傳送一封確認電子郵件。 您必須確認帳戶，才可以上傳套件。

## <a name="create-a-class-library-project"></a>建立類別庫專案

您可以針對要封裝的程式碼使用現有的 .NET 類別庫專案，或建立一個簡單的專案，如下所示：

1. 建立一個名為 `AppLogger` 的資料夾。

1. 開啟命令提示字元並切換至 `AppLogger` 資料夾。

1. 輸入 `dotnet new classlib`，它會針對專案使用目前資料夾的名稱。

   這會建立新的專案。

## <a name="add-package-metadata-to-the-project-file"></a>將套件中繼資料新增至專案檔

每個 NuGet 套件都需要資訊清單來描述套件的內容和相依性。 在最後一個套件中，資訊清單是一個 `.nuspec` 檔案，這是從您納入專案檔中的 NuGet 中繼資料屬性所產生的檔案。

1. 開啟專案檔 (`.csproj`)，並在現有的 `<PropertyGroup>` 標籤內新增下列基本屬性，適當地變更值：

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > 為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。 針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。

1. 新增任何選擇性的屬性，如 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。

    > [!Note]
    > 針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。

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

## <a name="publish-the-package"></a>發行套件

一旦擁有 `.nupkg` 檔案之後，您會使用 `dotnet nuget push` 命令以及從 nuget.org 取得的 API 金鑰，將它發行到 nuget.org。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>取得 API 金鑰

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>使用 dotnet nuget push 發行

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>發行錯誤

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>管理已發行的套件

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>後續步驟

恭喜，您建立了您的第一個 NuGet 套件！

> [!div class="nextstepaction"]
> [建立套件](../create-packages/creating-a-package-dotnet-cli.md)

若要深入探索 NuGet 所提供的功能，請選取下列連結。

- [發行套件](../nuget-org/publish-a-package.md)
- [發行前套件](../create-packages/Prerelease-Packages.md)
- [支援多個目標架構](../create-packages/multiple-target-frameworks-project-file.md)
- [套件版本控制](../concepts/package-versioning.md)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)
- [建立符號套件](../create-packages/symbol-packages-snupkg.md)
- [正在簽署套件](../create-packages/Sign-a-package.md)
