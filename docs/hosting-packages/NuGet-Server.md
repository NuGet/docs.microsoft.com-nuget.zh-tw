---
title: 使用 NuGet.Server 裝載 NuGet 摘要
description: 如何使用 NuGet.Server 在所有執行 IIS 的伺服器上建立及裝載 NuGet 套件摘要，透過 HTTP 和 OData 提供套件。
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059516"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server 是 .NET Foundation 提供的套件，建立 ASP.NET 應用程式在所有執行 IIS 的伺服器上裝載套件摘要。 簡而言之，NuGet.Server 可透過 HTTP (特別是 OData) 在伺服器上提供資料夾。 設定簡單，而且最適合簡單的情況。

1. 在 Visual Studio 中建立空的 ASP.NET Web 應用程式，並新增 NuGet.Server 套件。
1. 在應用程式中設定 `Packages` 資料夾並新增套件。
1. 將應用程式部署至合適的伺服器。

下列各節會使用 C# 逐步詳加解說。

如果您對 NuGet.Server 有進一步的問題[https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues),請在上創建問題。

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>使用 NuGet.Server 建立及部署 ASP.NET Web 應用程式

1. 在可視化工作室中,選擇 **「檔>」新>專案**」,搜索「ASP.NET Web 應用程式 (.NET 框架))」,為 C# 選擇匹配範本。

    ![選擇 .NET 架構 Web 專案樣本](media/Hosting_00-NuGet.Server-ProjectType.png)

1. **將框架**設置為".NET框架 4.6"。

    ![設定新專案的目標 Framework](media/Hosting_01-NuGet.Server-Set4.6.png)

1. 提供應用程式 NuGet.Server「以外」** 的合適名稱，選取 [確定]，並在下一個對話方塊中選取 [空白]**** 範本，再選取 [確定]****。

    ![選擇空 Web 專案](media/Hosting_02-NuGet.Server-Empty.png)

1. 以滑鼠右鍵按一下專案，選取 [管理 NuGet 套件]****。

1. 如果目標為 .NET Framework 4.6，請在套件管理員 UI 中選取 [瀏覽]**** 索引標籤，再搜尋並安裝最新版的 NuGet.Server 套件。 (您也可以使用`Install-Package NuGet.Server`從包管理器主控台安裝它。如果出現提示,則接受許可條款。

    ![安裝 NuGet.Server 套件](media/Hosting_03-NuGet.Server-Package.png)

1. 安裝 NuGet.Server 會將空的 Web 應用程式轉換成套件來源。 其會安裝其他各種套件、在應用程式中建立 `Packages` 資料夾，並修改 `web.config` 以包含其他設定 (詳細資料請參閱該檔案的註解)。

    > [!Important]
    > 在 NuGet.Server 套件完成對該檔案的修改之後，請仔細檢查 `web.config`。 NuGet.Server 可能不會覆寫現有的項目，而是建立重複的項目。 當您稍後嘗試執行專案時，這些重複項目將會導致「內部伺服器錯誤」。 例如，在安裝 NuGet.Server 之前，如果您的 `web.config` 包含了 `<compilation debug="true" targetFramework="4.5.2" />`，套件就不會加以覆寫，而會插入第二個 `<compilation debug="true" targetFramework="4.6" />`。 在此情況下，請刪除 Framework 版本較舊的項目。

1. 在 Visual Studio 中於本機執行網站 (使用 [偵錯] > [啟動但不偵錯]****，或 Ctrl+F5)。 首頁會提供套件摘要 URL，如下所示。 如果您看到錯誤,請仔細檢查您的`web.config`重複元素,如前面所述。

    ![使用 NuGet.Server 的應用程式預設首頁](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  第一次執行應用程式時，NuGet.Server 會重組 `Packages` 資料夾以包含每個套件的資料夾。 這符合 NuGet 3.3 為改善效能而推出的[本機儲存體配置](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。 新增多個套件時，會繼續遵循此結構。

1. 測試過本機部署後，請視需要將應用程式部署到任何其他內部或外部網站。

1. 一旦部署到 `http://<domain>`，套件來源使用的 URL 就會是 `http://<domain>/nuget`。

## <a name="adding-packages-to-the-feed-externally"></a>將套件新增至外部摘要

NuGet.Server 網站開始執行之後，假設您在 `web.config` 中設定了 API 金鑰值，就可以使用 [nuget push](../reference/cli-reference/cli-ref-push.md) 新增套件。

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

如果您的伺服器已受保護或本就不需要 API 金鑰 (例如，在本機小組網路上使用私用伺服器)，您可以將 `requireApiKey` 設成 `false`。 接著，所有能夠存取伺服器的使用者就都可以推送套件。

從 NuGet.Server 3.0.0 開始,推送`http://<domain>/nuget`套件的網址變更為 。 在 3.0.0 版本之前,推`http://<domain>/api/v2/package`送網址為 。

使用 NuGet 3.2.1`/api/v2/package`和更高版本,`/nuget``enableLegacyPushRoute: true`除了預設透過啟動設定`NuGetODataConfig.cs`中的選項( 預設情況下)中啟用此舊 URL。 請注意,當多個源託管在同一專案中時,此功能不起作用。

## <a name="removing-packages-from-the-feed"></a>從摘要移除套件

透過 NuGet.Server，假如您在註解中包含了 API 金鑰，[nuget delete](../reference/cli-reference/cli-ref-delete.md) 命令會從存放庫移除套件。

如果您想要將行為變更為取消列入套件 (使其可供套件還原使用)，請將 `web.config` 中的 `enableDelisting` 金鑰變更為 True。

## <a name="configuring-the-packages-folder"></a>設定 Packages 資料夾

使用`NuGet.Server`1.5 及更高版本,可以`appSettings/packagesPath``web.config`使用 中的 值自訂套件資料夾:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` 可以是絕對或虛擬路徑。

當 `packagesPath` 省略或留白時，套件資料夾會是預設值 `~/Packages`。

## <a name="making-packages-available-when-you-publish-the-web-app"></a>網頁應用程式時使套件可用

將應用程式發佈至伺服器時，若要在摘要中提供套件，請將每一個 `.nupkg` 檔案新增至 Visual Studio 中的 `Packages` 資料夾，再將每一個檔案的 [建置動作]**** 設成 [內容]****，然後將 [複製到輸出目錄]**** 設成 [一律複製]****：

![將套件複製到專案的 Packages 資料夾](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>版本資訊

NuGet.Server 的發行說明在[GitHub 發佈頁上](https://github.com/NuGet/NuGet.Server/releases)可用。
這包括有關錯誤修復和添加的新功能的詳細資訊。

## <a name="nugetserver-support"></a>NuGet.Server 支援

有關使用 NuGet.Server 的其他説明,[https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)請在上創建問題。
