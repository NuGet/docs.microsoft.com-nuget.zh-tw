---
title: 透過 dotnet CLI 使用 NuGet 套件的入門指南
description: 在 .NET Core 專案中安裝與使用 NuGet 套件程序的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 4b593cc215ad68629e5a93d1f17c90e53c0b4f4f
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324626"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>快速入門：利用 dotnet CLI 安裝並使用套件

NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。 您可以使用 `dotnet add package` 命令將套件安裝到 .NET Core 專案中，如本文中針對熱門 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) \(英文\) 套件所述的內容。

安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。 然後，您可以使用套件的 API。

> [!Tip]
> **從 nuget.org 開始**：瀏覽 nuget.org 是 .NET 開發人員通常用來尋找可在自己應用程式中重複使用之元件的方式。 您可以直接搜尋 nuget.org，或在 Visual Studio 中尋找並安裝套件，如本文所示。

## <a name="prerequisites"></a>必要條件

- [.NET Core SDK](https://www.microsoft.com/net/download/)，它會提供 `dotnet` 命令列工具。

## <a name="create-a-project"></a>建立專案

您可以將 NuGet 套件安裝到某種類型的 .NET 專案。 針對這個逐步解說，建立簡單的 .NET Core 主控台專案，如下所示：

1. 建立專案的資料夾。

1. 使用下列命令來建立專案：

    ```cli
    dotnet new console
    ```

1. 使用 `dotnet run` 來測試應用程式已正確建立。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

1. 使用下列命令來安裝 `Newtonsoft.json` 套件：

    ```cli
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

## <a name="related-articles"></a>相關文章

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)
- [安裝套件的方式](../consume-packages/ways-to-install-a-package.md)
- [設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)
