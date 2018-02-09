---
title: "使用 NuGet.Server 裝載 NuGet 摘要 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "如何使用 NuGet.Server 在所有執行 IIS 的伺服器上建立及裝載 NuGet 套件摘要，透過 HTTP 和 OData 提供套件。"
keywords: "NuGet 摘要, NuGet 資源庫, 遠端套件摘要, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a><span data-ttu-id="c05aa-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="c05aa-104">NuGet.Server</span></span>

<span data-ttu-id="c05aa-105">NuGet.Server 是 .NET Foundation 提供的套件，建立 ASP.NET 應用程式在所有執行 IIS 的伺服器上裝載套件摘要。</span><span class="sxs-lookup"><span data-stu-id="c05aa-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="c05aa-106">簡而言之，NuGet.Server 可透過 HTTP (特別是 OData) 在伺服器上提供資料夾。</span><span class="sxs-lookup"><span data-stu-id="c05aa-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="c05aa-107">設定簡單，而且最適合簡單的情況。</span><span class="sxs-lookup"><span data-stu-id="c05aa-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="c05aa-108">在 Visual Studio 中建立空的 ASP.NET Web 應用程式，並新增 NuGet.Server 套件。</span><span class="sxs-lookup"><span data-stu-id="c05aa-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="c05aa-109">在應用程式中設定 `Packages` 資料夾並新增套件。</span><span class="sxs-lookup"><span data-stu-id="c05aa-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="c05aa-110">將應用程式部署至合適的伺服器。</span><span class="sxs-lookup"><span data-stu-id="c05aa-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="c05aa-111">下列各節會使用 C# 逐步詳加解說。</span><span class="sxs-lookup"><span data-stu-id="c05aa-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="c05aa-112">使用 NuGet.Server 建立及部署 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c05aa-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="c05aa-113">在 Visual Studio 中，選取 [檔案] > [新增] > [專案]、將目標 Framework 設定為 .NET Framework 4.6 (請參閱下文)、搜尋 "ASP.NET"，然後選取 C# 的 [ASP.NET Web 應用程式 (.NET Framework)] 範本。</span><span class="sxs-lookup"><span data-stu-id="c05aa-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![將 .NET Framework 目標設定為 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="c05aa-115">提供應用程式 NuGet.Server 以外的合適名稱，選取 [確定]，並在下一個對話方塊中選取 [空] 範本並選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c05aa-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="c05aa-116">如果目標為 .NET Framework 4.6，請以滑鼠右鍵按一下專案，選取 [管理 NuGet 套件]，在套件管理員 UI 中搜尋並安裝最新版的 NuGet.Server 套件。</span><span class="sxs-lookup"><span data-stu-id="c05aa-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="c05aa-117">(您也可以從套件管理員主控台使用 `Install-Package NuGet.Server` 來安裝它。)</span><span class="sxs-lookup"><span data-stu-id="c05aa-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![安裝 NuGet.Server 套件](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="c05aa-119">如果您的 Web 應用程式以 .NET Framework 4.5.2 為目標，您必須改安裝 NuGet 伺服器 **2.10.3**。</span><span class="sxs-lookup"><span data-stu-id="c05aa-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="c05aa-120">安裝 NuGet.Server 會將空的 Web 應用程式轉換成套件來源。</span><span class="sxs-lookup"><span data-stu-id="c05aa-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="c05aa-121">它會在應用程式中建立 `Packages` 資料夾，並覆寫 `web.config` 以包含其他設定 (詳細資料請參閱該檔案的註解)。</span><span class="sxs-lookup"><span data-stu-id="c05aa-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="c05aa-122">將應用程式發佈至伺服器時，以在摘要中提供套件，請將其 `.nupkg` 檔案新增至 Visual Studio 中的 `Packages` 資料夾，再將其 [建置動作] 設成 [內容]，然後將 [複製到輸出目錄] 設成 [一律複製]：</span><span class="sxs-lookup"><span data-stu-id="c05aa-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![將套件複製到專案的 Packages 資料夾](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="c05aa-124">在 Visual Studio 中於本機執行網站 (但不偵錯，即 Ctrl+F5)。</span><span class="sxs-lookup"><span data-stu-id="c05aa-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="c05aa-125">首頁會提供套件摘要 URL：</span><span class="sxs-lookup"><span data-stu-id="c05aa-125">The home page provides the package feed URLs:</span></span>

    ![使用 NuGet.Server 的應用程式預設首頁](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="c05aa-127">按一下上文所列區域的**這裡**，查看套件的 OData 摘要。</span><span class="sxs-lookup"><span data-stu-id="c05aa-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="c05aa-128">第一次執行應用程式時，NuGet.Server 會重組 `Packages` 資料夾以包含每個套件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c05aa-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="c05aa-129">這符合 NuGet 3.3 為改善效能而推出的[本機儲存體配置](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。</span><span class="sxs-lookup"><span data-stu-id="c05aa-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="c05aa-130">新增多個套件時，會繼續遵循此結構。</span><span class="sxs-lookup"><span data-stu-id="c05aa-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="c05aa-131">測試過本機部署後，請視需要將應用程式部署到任何其他內部或外部網站。</span><span class="sxs-lookup"><span data-stu-id="c05aa-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="c05aa-132">一旦部署到 `http://<domain>`，套件來源使用的 URL 就會是 `http://<domain>/nuget`。</span><span class="sxs-lookup"><span data-stu-id="c05aa-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="c05aa-133">設定 Packages 資料夾</span><span class="sxs-lookup"><span data-stu-id="c05aa-133">Configuring the Packages folder</span></span>

<span data-ttu-id="c05aa-134">使用 `NuGet.Server` 1.5 及更新版本，您可以更明確地使用 `web.config` 的 `appSetting/packagesPath` 值來設定套件資料夾：</span><span class="sxs-lookup"><span data-stu-id="c05aa-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="c05aa-135">`packagesPath` 可以是絕對或虛擬路徑。</span><span class="sxs-lookup"><span data-stu-id="c05aa-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="c05aa-136">當 `packagesPath` 省略或留白時，套件資料夾會是預設值 `~/Packages`。</span><span class="sxs-lookup"><span data-stu-id="c05aa-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="c05aa-137">將套件新增至外部摘要</span><span class="sxs-lookup"><span data-stu-id="c05aa-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="c05aa-138">NuGet.Server 網站開始執行之後，假設您在 `web.config` 中設定了 API 金鑰值，就可以使用 nuget.exe 新增或刪除套件。</span><span class="sxs-lookup"><span data-stu-id="c05aa-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="c05aa-139">安裝 NuGet.Server 套件之後，`web.config` 包含空的 `appSetting/apiKey` 值：</span><span class="sxs-lookup"><span data-stu-id="c05aa-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="c05aa-140">當 `apiKey` 省略或空白時，會停用將套件推送至摘要。</span><span class="sxs-lookup"><span data-stu-id="c05aa-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="c05aa-141">若要啟用這項功能，請將 `apiKey` 設成值 (最好是強式密碼)，並新增有 `true` 值的 `appSettings/requireApiKey` 金鑰：</span><span class="sxs-lookup"><span data-stu-id="c05aa-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="c05aa-142">如果您的伺服器已受保護或本就不需要 API 金鑰 (例如，在本機小組網路上使用私用伺服器)，您可以將 `requireApiKey` 設成 `false`。</span><span class="sxs-lookup"><span data-stu-id="c05aa-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="c05aa-143">然後，所有可以存取伺服器的使用者都可以推送或刪除套件。</span><span class="sxs-lookup"><span data-stu-id="c05aa-143">All users with access to the server can then push or delete packages.</span></span>