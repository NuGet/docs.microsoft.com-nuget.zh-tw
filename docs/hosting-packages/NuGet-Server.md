---
title: 使用 NuGet.Server 裝載 NuGet 摘要
description: 如何使用 NuGet.Server 在所有執行 IIS 的伺服器上建立及裝載 NuGet 套件摘要，透過 HTTP 和 OData 提供套件。
author: JonDouglas
ms.author: jodou
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 3a9fb843f071eda72b9469292a7276ad81f8c24d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774082"
---
# <a name="nugetserver"></a><span data-ttu-id="c3d23-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="c3d23-103">NuGet.Server</span></span>

<span data-ttu-id="c3d23-104">NuGet.Server 是 .NET Foundation 提供的套件，建立 ASP.NET 應用程式在所有執行 IIS 的伺服器上裝載套件摘要。</span><span class="sxs-lookup"><span data-stu-id="c3d23-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="c3d23-105">簡而言之，NuGet.Server 可透過 HTTP (特別是 OData) 在伺服器上提供資料夾。</span><span class="sxs-lookup"><span data-stu-id="c3d23-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="c3d23-106">設定簡單，而且最適合簡單的情況。</span><span class="sxs-lookup"><span data-stu-id="c3d23-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="c3d23-107">在 Visual Studio 中建立空的 ASP.NET Web 應用程式，並新增 NuGet.Server 套件。</span><span class="sxs-lookup"><span data-stu-id="c3d23-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="c3d23-108">在應用程式中設定 `Packages` 資料夾並新增套件。</span><span class="sxs-lookup"><span data-stu-id="c3d23-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="c3d23-109">將應用程式部署至合適的伺服器。</span><span class="sxs-lookup"><span data-stu-id="c3d23-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="c3d23-110">下列各節會使用 C# 逐步詳加解說。</span><span class="sxs-lookup"><span data-stu-id="c3d23-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="c3d23-111">如果您對 Nuget.exe 有進一步的疑問，請在上建立問題 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) 。</span><span class="sxs-lookup"><span data-stu-id="c3d23-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="c3d23-112">使用 NuGet.Server 建立及部署 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c3d23-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="c3d23-113">在 Visual Studio 中，選取 [檔案] **> [新的 > 專案**]、搜尋 [ASP.NET Web 應用程式 ( .NET Framework) ]，然後選取符合的 **c #** 範本。</span><span class="sxs-lookup"><span data-stu-id="c3d23-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for **C#**.</span></span>

    ![選取 .NET Framework Web 專案範本](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="c3d23-115">將 **架構** 設定為 ".NET Framework 4.6"。</span><span class="sxs-lookup"><span data-stu-id="c3d23-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![設定新專案的目標 Framework](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="c3d23-117">提供應用程式 NuGet.Server「以外」的合適名稱，選取 [確定]，並在下一個對話方塊中選取 [空白] 範本，再選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c3d23-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![選取空白 Web 專案](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="c3d23-119">以滑鼠右鍵按一下專案，選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="c3d23-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="c3d23-120">如果目標為 .NET Framework 4.6，請在套件管理員 UI 中選取 [瀏覽] 索引標籤，再搜尋並安裝最新版的 NuGet.Server 套件。</span><span class="sxs-lookup"><span data-stu-id="c3d23-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="c3d23-121"> (您也可以從封裝管理員主控台安裝它 `Install-Package NuGet.Server` 。如果出現提示，) 接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="c3d23-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![安裝 NuGet.Server 套件](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="c3d23-123">安裝 NuGet.Server 會將空的 Web 應用程式轉換成套件來源。</span><span class="sxs-lookup"><span data-stu-id="c3d23-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="c3d23-124">其會安裝其他各種套件、在應用程式中建立 `Packages` 資料夾，並修改 `web.config` 以包含其他設定 (詳細資料請參閱該檔案的註解)。</span><span class="sxs-lookup"><span data-stu-id="c3d23-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="c3d23-125">在 NuGet.Server 套件完成對該檔案的修改之後，請仔細檢查 `web.config`。</span><span class="sxs-lookup"><span data-stu-id="c3d23-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="c3d23-126">NuGet.Server 可能不會覆寫現有的項目，而是建立重複的項目。</span><span class="sxs-lookup"><span data-stu-id="c3d23-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="c3d23-127">當您稍後嘗試執行專案時，這些重複項目將會導致「內部伺服器錯誤」。</span><span class="sxs-lookup"><span data-stu-id="c3d23-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="c3d23-128">例如，在安裝 NuGet.Server 之前，如果您的 `web.config` 包含了 `<compilation debug="true" targetFramework="4.5.2" />`，套件就不會加以覆寫，而會插入第二個 `<compilation debug="true" targetFramework="4.6" />`。</span><span class="sxs-lookup"><span data-stu-id="c3d23-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="c3d23-129">在此情況下，請刪除 Framework 版本較舊的項目。</span><span class="sxs-lookup"><span data-stu-id="c3d23-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="c3d23-130">在 Visual Studio 中於本機執行網站 (使用 [偵錯] > [啟動但不偵錯]，或 Ctrl+F5)。</span><span class="sxs-lookup"><span data-stu-id="c3d23-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="c3d23-131">首頁會提供套件摘要 URL，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c3d23-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="c3d23-132">如果您看到錯誤，請仔細檢查 `web.config` 是否有重複的專案，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="c3d23-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![使用 NuGet.Server 的應用程式預設首頁](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="c3d23-134">第一次執行應用程式時，NuGet.Server 會重組 `Packages` 資料夾以包含每個套件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c3d23-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="c3d23-135">這符合 NuGet 3.3 為改善效能而推出的[本機儲存體配置](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。</span><span class="sxs-lookup"><span data-stu-id="c3d23-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="c3d23-136">新增多個套件時，會繼續遵循此結構。</span><span class="sxs-lookup"><span data-stu-id="c3d23-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="c3d23-137">測試過本機部署後，請視需要將應用程式部署到任何其他內部或外部網站。</span><span class="sxs-lookup"><span data-stu-id="c3d23-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="c3d23-138">一旦部署到 `http://<domain>`，套件來源使用的 URL 就會是 `http://<domain>/nuget`。</span><span class="sxs-lookup"><span data-stu-id="c3d23-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="c3d23-139">將套件新增至外部摘要</span><span class="sxs-lookup"><span data-stu-id="c3d23-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="c3d23-140">NuGet.Server 網站開始執行之後，假設您在 `web.config` 中設定了 API 金鑰值，就可以使用 [nuget push](../reference/cli-reference/cli-ref-push.md) 新增套件。</span><span class="sxs-lookup"><span data-stu-id="c3d23-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="c3d23-141">安裝 NuGet.Server 套件之後，`web.config` 包含空的 `appSetting/apiKey` 值：</span><span class="sxs-lookup"><span data-stu-id="c3d23-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="c3d23-142">當 `apiKey` 省略或空白時，會停用將套件推送至摘要。</span><span class="sxs-lookup"><span data-stu-id="c3d23-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="c3d23-143">若要啟用這項功能，請將 `apiKey` 設成值 (最好是強式密碼)，並新增有 `true` 值的 `appSettings/requireApiKey` 金鑰：</span><span class="sxs-lookup"><span data-stu-id="c3d23-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="c3d23-144">如果您的伺服器已受保護或本就不需要 API 金鑰 (例如，在本機小組網路上使用私用伺服器)，您可以將 `requireApiKey` 設成 `false`。</span><span class="sxs-lookup"><span data-stu-id="c3d23-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="c3d23-145">接著，所有能夠存取伺服器的使用者就都可以推送套件。</span><span class="sxs-lookup"><span data-stu-id="c3d23-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="c3d23-146">從3.0.0 開始，推送套件的 URL 會變更為 `http://<domain>/nuget` 。</span><span class="sxs-lookup"><span data-stu-id="c3d23-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="c3d23-147">在3.0.0 版本之前，推送 URL 為 `http://<domain>/api/v2/package` 。</span><span class="sxs-lookup"><span data-stu-id="c3d23-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="c3d23-148">使用 NuGet 3.2.1 和更新版本時，預設會啟用此舊版 URL，預設 `/api/v2/package` 會在 `/nuget` 啟動設定 (預設為 `enableLegacyPushRoute: true` `NuGetODataConfig.cs`) 。</span><span class="sxs-lookup"><span data-stu-id="c3d23-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="c3d23-149">請注意，當多個摘要裝載于同一個專案時，這項功能無法運作。</span><span class="sxs-lookup"><span data-stu-id="c3d23-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="c3d23-150">從摘要移除套件</span><span class="sxs-lookup"><span data-stu-id="c3d23-150">Removing packages from the feed</span></span>

<span data-ttu-id="c3d23-151">透過 NuGet.Server，假如您在註解中包含了 API 金鑰，[nuget delete](../reference/cli-reference/cli-ref-delete.md) 命令會從存放庫移除套件。</span><span class="sxs-lookup"><span data-stu-id="c3d23-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="c3d23-152">如果您想要將行為變更為取消列入套件 (使其可供套件還原使用)，請將 `web.config` 中的 `enableDelisting` 金鑰變更為 True。</span><span class="sxs-lookup"><span data-stu-id="c3d23-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="c3d23-153">設定 Packages 資料夾</span><span class="sxs-lookup"><span data-stu-id="c3d23-153">Configuring the Packages folder</span></span>

<span data-ttu-id="c3d23-154">使用 `NuGet.Server` 1.5 和更新版本時，您可以使用中的值來自訂封裝資料夾 `appSettings/packagesPath` `web.config` ：</span><span class="sxs-lookup"><span data-stu-id="c3d23-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="c3d23-155">`packagesPath` 可以是絕對或虛擬路徑。</span><span class="sxs-lookup"><span data-stu-id="c3d23-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="c3d23-156">當 `packagesPath` 省略或留白時，套件資料夾會是預設值 `~/Packages`。</span><span class="sxs-lookup"><span data-stu-id="c3d23-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="c3d23-157">在發佈 web 應用程式時讓套件可供使用</span><span class="sxs-lookup"><span data-stu-id="c3d23-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="c3d23-158">將應用程式發佈至伺服器時，若要在摘要中提供套件，請將每一個 `.nupkg` 檔案新增至 Visual Studio 中的 `Packages` 資料夾，再將每一個檔案的 [建置動作] 設成 [內容]，然後將 [複製到輸出目錄] 設成 [一律複製]：</span><span class="sxs-lookup"><span data-stu-id="c3d23-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![將套件複製到專案的 Packages 資料夾](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="c3d23-160">版本資訊</span><span class="sxs-lookup"><span data-stu-id="c3d23-160">Release Notes</span></span>

<span data-ttu-id="c3d23-161">您可以在 [GitHub 版本頁面](https://github.com/NuGet/NuGet.Server/releases)上取得適用于 nuget.exe 的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="c3d23-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="c3d23-162">這包括 bug 修正的詳細資料，以及新增的新功能。</span><span class="sxs-lookup"><span data-stu-id="c3d23-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="c3d23-163">NuGet.Server 支援</span><span class="sxs-lookup"><span data-stu-id="c3d23-163">NuGet.Server support</span></span>

<span data-ttu-id="c3d23-164">如需使用 Nuget.exe 的其他說明，請在上建立問題 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) 。</span><span class="sxs-lookup"><span data-stu-id="c3d23-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
