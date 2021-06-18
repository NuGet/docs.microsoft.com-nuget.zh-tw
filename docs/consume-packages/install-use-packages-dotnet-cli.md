---
title: 使用 dotnet CLI 安裝和管理 NuGet 套件
description: 使用 dotnet CLI 以便處理 NuGet 套件的指示。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 62c05aad388c25120d5b9f5143017a2f4f3b276b
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323605"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>使用 dotnet CLI 安裝和管理套件

CLI 工具可讓您輕鬆地在專案和解決方案中安裝、解除安裝及更新 NuGet 套件。 可在 Windows、Mac OS X 及 Linux 上執行。

Dotnet CLI 適用於 .NET Core 和 .NET Standard 專案 (SDK 樣式專案類型)，以及其他任何 SDK 樣式專案 (例如以 .NET Framework 為目標的 SDK 樣式專案)。 如需詳細資訊，請參閱 [SDK 屬性](/dotnet/core/tools/csproj#additions)。

本文顯示一些最常用 dotnet CLI 命令的基本使用方式。 針對這些命令的大部分，CLI 工具會在目前的目錄中尋找專案檔，除非在命令中指定專案檔 (專案檔為選用參數)。 如需您可以使用的命令和引數完整清單，請參閱 [.NET Core 命令列介面 (CLI) 工具](../reference/dotnet-commands.md)。

## <a name="prerequisites"></a>先決條件

- [.NET Core SDK](https://www.microsoft.com/net/download/)，它會提供 `dotnet` 命令列工具。 從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。

## <a name="install-a-package"></a>安裝套件

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 會將套件參考新增到專案檔中，然後執行 `dotnet restore` 安裝套件。

1. 開啟命令列並切換至包含您專案檔的目錄。

2. 使用下列命令來安裝 NuGet 套件：

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    例如，若要安裝 `Newtonsoft.Json` 套件，請使用下列命令

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. 在命令完成之後，請查看專案檔以確定已安裝套件。

   您可以開啟 `.csproj` 檔案來查看已新增的參考：

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>安裝特定版本的套件

如果未指定版本，則 NuGet 會安裝最新版的套件。 您也可以使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 命令來安裝特定版本的 NuGet 套件：

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

例如，若要新增 12.0.1 版的 `Newtonsoft.Json` 套件，請使用此命令：

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a>列出套件參考

您可以使用 [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 命令列出專案的套件參考。

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>移除套件

使用 [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 命令來移除專案檔中的套件參考。

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

例如，若要移除 `Newtonsoft.Json` 套件，請使用下列命令

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>更新套件

除非您指定套件版本 (`-v` 參數)，否則當您使用 `dotnet add package` 命令時 NuGet 會安裝最新版的套件。

## <a name="restore-packages"></a>還原套件

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
