---
title: 使用 dotnet CLI 建立及發佈 NuGet 套件
description: 使用 .NET Core CLI、dotnet 建立和發行 NuGet 套件的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: f663b1b2176a5f0ae5bc6d82873193638e0efdaa
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833379"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="5304a-103">快速入門：建立及發行套件 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="5304a-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="5304a-104">使用 `dotnet` 命令列介面 (CLI) 從 .NET 類別庫建立 NuGet 套件，並將它發行到 nuget.org 是個簡單的程序。</span><span class="sxs-lookup"><span data-stu-id="5304a-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5304a-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="5304a-105">Prerequisites</span></span>

1. <span data-ttu-id="5304a-106">安裝 [.NET Core SDK](https://www.microsoft.com/net/download/)，其中包括 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="5304a-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="5304a-107">從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。</span><span class="sxs-lookup"><span data-stu-id="5304a-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="5304a-108">如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="5304a-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="5304a-109">建立新的帳戶會傳送一封確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="5304a-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="5304a-110">您必須確認帳戶，才可以上傳套件。</span><span class="sxs-lookup"><span data-stu-id="5304a-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="5304a-111">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="5304a-111">Create a class library project</span></span>

<span data-ttu-id="5304a-112">您可以針對要封裝的程式碼使用現有的 .NET 類別庫專案，或建立一個簡單的專案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5304a-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="5304a-113">建立一個名為 `AppLogger` 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5304a-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="5304a-114">開啟命令提示字元並切換至 `AppLogger` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5304a-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="5304a-115">輸入 `dotnet new classlib`，它會針對專案使用目前資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="5304a-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="5304a-116">這會建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="5304a-116">This creates the new project.</span></span>

1. <span data-ttu-id="5304a-117">使用 `dotnet run` 來測試應用程式已正確建立。</span><span class="sxs-lookup"><span data-stu-id="5304a-117">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="5304a-118">將套件中繼資料新增至專案檔</span><span class="sxs-lookup"><span data-stu-id="5304a-118">Add package metadata to the project file</span></span>

<span data-ttu-id="5304a-119">每個 NuGet 套件都需要資訊清單來描述套件的內容和相依性。</span><span class="sxs-lookup"><span data-stu-id="5304a-119">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="5304a-120">在最後一個套件中，資訊清單是一個 `.nuspec` 檔案，這是從您納入專案檔中的 NuGet 中繼資料屬性所產生的檔案。</span><span class="sxs-lookup"><span data-stu-id="5304a-120">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="5304a-121">開啟專案檔 (`.csproj`)，並在現有的 `<PropertyGroup>` 標籤內新增下列基本屬性，適當地變更值：</span><span class="sxs-lookup"><span data-stu-id="5304a-121">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="5304a-122">為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="5304a-122">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="5304a-123">針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。</span><span class="sxs-lookup"><span data-stu-id="5304a-123">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="5304a-124">新增任何選擇性的屬性，如 [NuGet 中繼資料屬性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。</span><span class="sxs-lookup"><span data-stu-id="5304a-124">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="5304a-125">針對公眾取用而建置的套件，請特別注意 **PackageTags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="5304a-125">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="5304a-126">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="5304a-126">Run the pack command</span></span>

<span data-ttu-id="5304a-127">若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `dotnet pack` 命令，該命令也會自動建置專案：</span><span class="sxs-lookup"><span data-stu-id="5304a-127">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="5304a-128">輸出將顯示 `.nupkg` 檔案的路徑：</span><span class="sxs-lookup"><span data-stu-id="5304a-128">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="5304a-129">建置時自動產生套件</span><span class="sxs-lookup"><span data-stu-id="5304a-129">Automatically generate package on build</span></span>

<span data-ttu-id="5304a-130">若要在您執行 `dotnet build` 時自動執行 `dotnet pack`，請將下列程式行加入專案檔的 `<PropertyGroup>` 中：</span><span class="sxs-lookup"><span data-stu-id="5304a-130">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="5304a-131">發行套件</span><span class="sxs-lookup"><span data-stu-id="5304a-131">Publish the package</span></span>

<span data-ttu-id="5304a-132">一旦擁有 `.nupkg` 檔案之後，您會使用 `dotnet nuget push` 命令以及從 nuget.org 取得的 API 金鑰，將它發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="5304a-132">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="5304a-133">取得 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="5304a-133">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="5304a-134">使用 dotnet nuget push 發行</span><span class="sxs-lookup"><span data-stu-id="5304a-134">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="5304a-135">發行錯誤</span><span class="sxs-lookup"><span data-stu-id="5304a-135">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="5304a-136">管理已發行的套件</span><span class="sxs-lookup"><span data-stu-id="5304a-136">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="5304a-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5304a-137">Next steps</span></span>

<span data-ttu-id="5304a-138">恭喜，您建立了您的第一個 NuGet 套件！</span><span class="sxs-lookup"><span data-stu-id="5304a-138">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5304a-139">建立套件</span><span class="sxs-lookup"><span data-stu-id="5304a-139">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="5304a-140">若要深入探索 NuGet 所提供的功能，請選取下列連結。</span><span class="sxs-lookup"><span data-stu-id="5304a-140">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="5304a-141">套件</span><span class="sxs-lookup"><span data-stu-id="5304a-141">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="5304a-142">發行前套件</span><span class="sxs-lookup"><span data-stu-id="5304a-142">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="5304a-143">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="5304a-143">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="5304a-144">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="5304a-144">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="5304a-145">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="5304a-145">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="5304a-146">建立符號套件</span><span class="sxs-lookup"><span data-stu-id="5304a-146">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="5304a-147">正在簽署套件</span><span class="sxs-lookup"><span data-stu-id="5304a-147">Signing packages</span></span>](../create-packages/Sign-a-package.md)
