---
title: 透過 dotnet CLI 使用 NuGet 套件的入門指南
description: 在 .NET Core 專案中安裝與使用 NuGet 套件程序的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1060d98278fed89ac63ee17c1896ae8bdce72a9e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426157"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="c9c85-103">快速入門：利用 dotnet CLI 安裝並使用套件</span><span class="sxs-lookup"><span data-stu-id="c9c85-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="c9c85-104">NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。</span><span class="sxs-lookup"><span data-stu-id="c9c85-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="c9c85-105">請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。</span><span class="sxs-lookup"><span data-stu-id="c9c85-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="c9c85-106">您可以使用 `dotnet add package` 命令將套件安裝到 .NET Core 專案中，如本文中針對熱門 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) \(英文\) 套件所述的內容。</span><span class="sxs-lookup"><span data-stu-id="c9c85-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="c9c85-107">安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。</span><span class="sxs-lookup"><span data-stu-id="c9c85-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="c9c85-108">然後，您可以使用套件的 API。</span><span class="sxs-lookup"><span data-stu-id="c9c85-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="c9c85-109">**從 nuget.org 開始**：瀏覽 nuget.org 是 .NET 開發人員通常用來尋找可在自己應用程式中重複使用之元件的方式。</span><span class="sxs-lookup"><span data-stu-id="c9c85-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="c9c85-110">您可以直接搜尋 nuget.org，或在 Visual Studio 中尋找並安裝套件，如本文所示。</span><span class="sxs-lookup"><span data-stu-id="c9c85-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9c85-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="c9c85-111">Prerequisites</span></span>

- <span data-ttu-id="c9c85-112">[.NET Core SDK](https://www.microsoft.com/net/download/)，它會提供 `dotnet` 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="c9c85-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="c9c85-113">建立專案</span><span class="sxs-lookup"><span data-stu-id="c9c85-113">Create a project</span></span>

<span data-ttu-id="c9c85-114">您可以將 NuGet 套件安裝到某種類型的 .NET 專案。</span><span class="sxs-lookup"><span data-stu-id="c9c85-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="c9c85-115">針對這個逐步解說，建立簡單的 .NET Core 主控台專案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c9c85-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="c9c85-116">建立專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c9c85-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="c9c85-117">使用下列命令來建立專案：</span><span class="sxs-lookup"><span data-stu-id="c9c85-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="c9c85-118">使用 `dotnet run` 來測試應用程式已正確建立。</span><span class="sxs-lookup"><span data-stu-id="c9c85-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="c9c85-119">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c9c85-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="c9c85-120">使用下列命令來安裝 `Newtonsoft.json` 套件：</span><span class="sxs-lookup"><span data-stu-id="c9c85-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="c9c85-121">在命令完成之後，開啟 `.csproj` 檔案來查看已新增的參考：</span><span class="sxs-lookup"><span data-stu-id="c9c85-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="c9c85-122">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="c9c85-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="c9c85-123">開啟 `Program.cs` 檔案，並在檔案頂端新增下列一行：</span><span class="sxs-lookup"><span data-stu-id="c9c85-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="c9c85-124">在 `class Program` 行之前，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c9c85-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="c9c85-125">使用下列程式碼取代 `Main` 函式：</span><span class="sxs-lookup"><span data-stu-id="c9c85-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="c9c85-126">使用 `dotnet run` 命令，建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9c85-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="c9c85-127">在程式碼中，輸出應該是 `Account` 物件的 JSON 表示法：</span><span class="sxs-lookup"><span data-stu-id="c9c85-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="c9c85-128">相關文章</span><span class="sxs-lookup"><span data-stu-id="c9c85-128">Related articles</span></span>

- [<span data-ttu-id="c9c85-129">使用 dotnet CLI 安裝和使用套件</span><span class="sxs-lookup"><span data-stu-id="c9c85-129">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="c9c85-130">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="c9c85-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="c9c85-131">尋找及選擇套件</span><span class="sxs-lookup"><span data-stu-id="c9c85-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="c9c85-132">常用的 NuGet 設定</span><span class="sxs-lookup"><span data-stu-id="c9c85-132">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
