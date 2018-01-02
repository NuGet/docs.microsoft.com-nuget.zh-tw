---
title: "使用 NuGet.Server 裝載 NuGet 摘要 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 45138f80-9717-42c2-8b34-9a1bc1fb3eab
description: "如何使用 NuGet.Server 在所有執行 IIS 的伺服器上建立及裝載 NuGet 套件摘要，透過 HTTP 和 OData 提供套件。"
keywords: "NuGet 摘要, NuGet 資源庫, 遠端套件摘要, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f37b9b711a2bc8c39314214113045a6485f297a8
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server 是 .NET Foundation 提供的套件，建立 ASP.NET 應用程式在所有執行 IIS 的伺服器上裝載套件摘要。 簡而言之，NuGet.Server 可透過 HTTP (特別是 OData) 在伺服器上提供資料夾。 設定簡單，而且最適合簡單的情況。

1. 在 Visual Studio 中建立空的 ASP.NET Web 應用程式，並新增 NuGet.Server 套件。
1. 在應用程式中設定 `Packages` 資料夾並新增套件。
1. 將應用程式部署至合適的伺服器。

下列各節會使用 C# 逐步詳加解說。

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>使用 NuGet.Server 建立及部署 ASP.NET Web 應用程式

1. 在 Visual Studio 中，選取 [檔案] > [新增] > [專案]、將目標 Framework 設定為 .NET Framework 4.6 (請參閱下文)、搜尋 "ASP.NET"，然後選取 C# 的 [ASP.NET Web 應用程式 (.NET Framework)] 範本。

    ![將 .NET Framework 目標設定為 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. 提供應用程式 NuGet.Server 以外的合適名稱，選取 [確定]，並在下一個對話方塊中選取 [空] 範本並選取 [確定]。

1. 如果目標為 .NET Framework 4.6，請以滑鼠右鍵按一下專案，選取 [管理 NuGet 套件]，在套件管理員 UI 中搜尋並安裝最新版的 NuGet.Server 套件。 (您也可以從套件管理員主控台使用 `Install-Package NuGet.Server` 來安裝它。)

    ![安裝 NuGet.Server 套件](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > 如果您的 Web 應用程式以 .NET Framework 4.5.2 為目標，您必須改安裝 NuGet 伺服器 **2.10.3**。

1. 安裝 NuGet.Server 會將空的 Web 應用程式轉換成套件來源。 它會在應用程式中建立 `Packages` 資料夾，並覆寫 `web.config` 以包含其他設定 (詳細資料請參閱該檔案的註解)。

1. 將應用程式發佈至伺服器時，以在摘要中提供套件，請將其 `.nupkg` 檔案新增至 Visual Studio 中的 `Packages` 資料夾，再將其 [建置動作] 設成 [內容]，然後將 [複製到輸出目錄] 設成 [一律複製]：

    ![將套件複製到專案的 Packages 資料夾](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. 在 Visual Studio 中於本機執行網站 (但不偵錯，即 Ctrl+F5)。 首頁會提供套件摘要 URL：

    ![使用 NuGet.Server 的應用程式預設首頁](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. 按一下上文所列區域的**這裡**，查看套件的 OData 摘要。

1. 第一次執行應用程式時，NuGet.Server 會重組 `Packages` 資料夾以包含每個套件的資料夾。 這符合 NuGet 3.3 為改善效能而推出的[本機儲存體配置](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。 新增多個套件時，會繼續遵循此結構。

1. 測試過本機部署後，請視需要將應用程式部署到任何其他內部或外部網站。
1. 一旦部署到 `http://<domain>`，套件來源使用的 URL 就會是 `http://<domain>/nuget`。

## <a name="configuring-the-packages-folder"></a>設定 Packages 資料夾

使用 `NuGet.Server` 1.5 及更新版本，您可以更明確地使用 `web.config` 的 `appSetting/packagesPath` 值來設定套件資料夾：

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` 可以是絕對或虛擬路徑。

當 `packagesPath` 省略或留白時，套件資料夾會是預設值 `~/Packages`。

## <a name="adding-packages-to-the-feed-externally"></a>將套件新增至外部摘要

NuGet.Server 網站開始執行之後，假設您在 `web.config` 中設定了 API 金鑰值，就可以使用 nuget.exe 新增或刪除套件。

安裝 NuGet.Server 套件之後，`web.config` 包含空的 `appSetting/apiKey` 值：

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

當 `apiKey` 省略或空白時，會停用將套件推送至摘要。

若要啟用這項功能，請將 `apiKey` 設成值 (最好是強式密碼)，並新增有 `true` 值的 `appSettings/requireApiKey` 金鑰：

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

如果您的伺服器已受保護或本就不需要 API 金鑰 (例如，在本機小組網路上使用私用伺服器)，您可以將 `requireApiKey` 設成 `false`。 然後，所有可以存取伺服器的使用者都可以推送或刪除套件。