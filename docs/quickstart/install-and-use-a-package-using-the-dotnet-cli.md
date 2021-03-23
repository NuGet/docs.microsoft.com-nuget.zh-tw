---
title: 利用 dotnet CLI 安裝並使用 NuGet 套件
description: 在 .NET Core 專案中安裝與使用 NuGet 套件程序的逐步解說教學課程。
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: dbe1d3ee8e50a90803140bc2c5cb5821b485a2fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859430"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>快速入門：利用 dotnet CLI 安裝並使用套件

NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。 您可以使用 `dotnet add package` 命令將套件安裝到 .NET Core 專案中，如本文中針對熱門 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) \(英文\) 套件所述的內容。

安裝之後，請在程式碼中參考封裝， `using <namespace>` 其中包含您所使用之 \<namespace\> 套件的特定位置。 然後，您可以使用套件的 API。

> [!Tip]
> **從 nuget.org 開始**：瀏覽 nuget.org 是 .NET 開發人員通常用來尋找可在自己應用程式中重複使用之元件的方式。 您可以直接搜尋 nuget.org，或在 Visual Studio 中尋找並安裝套件，如本文所示。

## <a name="prerequisites"></a>Prerequisites

- [.NET Core SDK](https://www.microsoft.com/net/download/)，它會提供 `dotnet` 命令列工具。 從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。

## <a name="create-a-project"></a>建立專案

您可以將 NuGet 套件安裝到某種類型的 .NET 專案。 針對這個逐步解說，建立簡單的 .NET Core 主控台專案，如下所示：

1. 建立專案的資料夾。

1. 開啟命令提示字元並切換至新的資料夾。

1. 使用下列命令來建立專案：

    ```dotnetcli
    dotnet new console
    ```

1. 使用 `dotnet run` 來測試應用程式已正確建立。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

1. 使用下列命令來安裝 `Newtonsoft.json` 套件：

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. 在命令完成之後，開啟 `.csproj` 檔案來查看已新增的參考：

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在應用程式中使用 Newtonsoft.Json API

1. 開啟 `Program.cs` 檔案，並在檔案頂端新增下列一行：

    ```cs
    using Newtonsoft.Json;
    ```

1. 在 `class Program` 行之前，新增下列程式碼：

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. 使用下列程式碼取代 `Main` 函式：

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. 使用 `dotnet run` 命令，建置並執行應用程式。 在程式碼中，輸出應該是 `Account` 物件的 JSON 表示法：

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>相關影片

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

在 [Channel 9](https://channel9.msdn.com/Series/NuGet-101) 和 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)上尋找更多的 NuGet 影片。

## <a name="next-steps"></a>下一步

恭喜，您安裝並使用了您的第一個 NuGet 套件！

> [!div class="nextstepaction"]
> [使用 dotnet CLI 安裝和使用套件](../consume-packages/install-use-packages-dotnet-cli.md)

若要深入探索 NuGet 所提供的功能，請選取下列連結。

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)
- [專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)
