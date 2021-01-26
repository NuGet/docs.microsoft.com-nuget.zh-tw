---
title: NuGet 2.1 版本資訊
description: NuGet 2.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777033"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="9bbb0-103">NuGet 2.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="9bbb0-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="9bbb0-104">[NuGet 2.0 版本](../release-notes/nuget-2.0.md)  |  資訊[NuGet 2.2 版本](../release-notes/nuget-2.2.md)資訊</span><span class="sxs-lookup"><span data-stu-id="9bbb0-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="9bbb0-105">NuGet 2.1 發行于2012年10月4日。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="9bbb0-106">階層式 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="9bbb0-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="9bbb0-107">NuGet 2.1 透過以遞迴方式流覽資料夾結構來尋找檔案 `NuGet.Config` ，然後從所有找到的檔案集中建立設定，讓您更有彈性地控制 NuGet 設定。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="9bbb0-108">例如，假設某個小組具有其他內部相依性 CI 組建的內部套件存放庫。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="9bbb0-109">個別專案的資料夾結構看起來可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bbb0-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="9bbb0-110">此外，如果解決方案已啟用套件還原，下列資料夾也將存在：</span><span class="sxs-lookup"><span data-stu-id="9bbb0-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="9bbb0-111">若要讓小組的內部封裝存放庫可供小組使用的所有專案使用，但無法將它提供給電腦上的每個專案，我們可以建立新的 Nuget.Config 檔，並將它放在 c:\myteam 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="9bbb0-112">沒有任何方法可指定每個專案的封裝資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="9bbb0-113">現在，我們可以從 c:\myteam 下的任何資料夾執行 ' nuget.exe source ' 命令，以查看已新增來源，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bbb0-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![從父 nuget 設定封裝來源](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="9bbb0-115">`NuGet.Config` 系統會以下列順序搜尋檔案：</span><span class="sxs-lookup"><span data-stu-id="9bbb0-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="9bbb0-116">從專案資料夾到根的遞迴逐步解說</span><span class="sxs-lookup"><span data-stu-id="9bbb0-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="9bbb0-117">全域 `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`) </span><span class="sxs-lookup"><span data-stu-id="9bbb0-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="9bbb0-118">這些設定會以 *相反順序* 套用，也就是說，根據上述順序，全域 Nuget.Config 會先套用，接著會先套用從根到專案資料夾的探索 Nuget.Config 檔案，接著是 `.nuget\Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="9bbb0-119">如果您要使用 `<clear/>` 元素從設定中移除一組專案，這點特別重要。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="9bbb0-120">指定 [套件] 資料夾位置</span><span class="sxs-lookup"><span data-stu-id="9bbb0-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="9bbb0-121">在過去，NuGet 已從方案根資料夾底下的已知「套件」資料夾管理解決方案的套件。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="9bbb0-122">針對有許多不同方案已安裝 NuGet 套件的開發小組，這可能會導致在檔案系統上的許多不同位置中安裝相同的套件。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="9bbb0-123">NuGet 2.1 透過檔案中的專案，讓您更精確地控制套件資料夾的位置 `repositoryPath` `NuGet.Config` 。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="9bbb0-124">以階層式 Nuget.Config 支援的先前範例為基礎，假設我們想要讓 C:\myteam\ 下的所有專案共用相同的封裝資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="9bbb0-125">若要完成這項工作，只要將下列專案加入至 `c:\myteam\Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="9bbb0-126">在此範例中，共用檔案 `Nuget.Config` 會針對在 C:\myteam 底下建立的每個專案（不論深度）指定共用封裝資料夾。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="9bbb0-127">請注意，如果您的解決方案根目錄底下有現有的套件資料夾，您必須先將其刪除，NuGet 才會將套件放在新的位置。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="9bbb0-128">支援可移植程式庫</span><span class="sxs-lookup"><span data-stu-id="9bbb0-128">Support for Portable Libraries</span></span>

<span data-ttu-id="9bbb0-129">[便攜程式庫](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 是 .net 4 首次引進的功能，可讓您建立可在不同的 Microsoft 平臺上執行的元件，從 the.NET Framework 的版本到 Silverlight，再 Windows Phone 甚至是 Xbox 360 (但目前 NuGet 並不支援 Xbox 便攜程式庫目標) 。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="9bbb0-130">藉由擴充 framework 版本和設定檔的 [套件慣例](../create-packages/supporting-multiple-target-frameworks.md) ，NuGet 2.1 現在可讓您建立具有複合架構和設定檔目的檔案夾的封裝，藉此支援便攜程式庫 `lib` 。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="9bbb0-131">例如，請考慮下列可移植類別庫的可用目標平臺。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![便攜程式庫建立對話方塊](./media/releasenotes-21-plib.png)

<span data-ttu-id="9bbb0-133">建立程式庫並執行命令之後 `nuget.exe pack MyPortableProject.csproj` ，您可以藉由檢查所產生 NuGet 套件的內容，來查看新的便攜程式庫套件資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![便攜程式庫套件配置](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="9bbb0-135">如您所見，便攜程式庫資料夾名稱慣例遵循模式 ' 便攜-{framework 1} + {framework n} '，其中的 framework 識別碼遵循現有的 [framework 名稱和版本慣例](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="9bbb0-136">名稱和版本慣例有一個例外狀況，可在用於 Windows Phone 的 framework 識別碼中找到。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="9bbb0-137">這個標記應使用架構名稱 ' wp ' (wp7、wp71 或 wp8) 。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="9bbb0-138">例如，使用 ' silverlight-wp7 ' 將會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="9bbb0-139">安裝從此資料夾結構建立的封裝時，NuGet 現在可以將其架構和設定檔規則套用至多個目標，如資料夾名稱中所指定。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="9bbb0-140">NuGet 比對規則背後的原則是「更明確的」目標優先于「較不明確」的目標。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="9bbb0-141">這表示，如果以特定平臺為目標的名字，將一律優先于可移植的專案（如果它們兩者都與專案相容）。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="9bbb0-142">此外，如果有多個可移植目標與某個專案相容，則 NuGet 會偏好一組支援的平臺「最接近」至參考封裝的專案。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="9bbb0-143">以 Windows 8 和 Windows Phone 8 專案為目標</span><span class="sxs-lookup"><span data-stu-id="9bbb0-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="9bbb0-144">除了新增以可移植程式庫專案為目標的支援之外，NuGet 2.1 還為 Windows 8 存放區和 Windows Phone 8 專案提供了新的架構名字，以及一些新的 Windows Store 和 Windows Phone 專案的一般名字標記，可讓您更輕鬆地在各平臺的未來版本中進行管理。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="9bbb0-145">針對 Windows 8 存放區應用程式，識別碼看起來如下：</span><span class="sxs-lookup"><span data-stu-id="9bbb0-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="9bbb0-146">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="9bbb0-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9bbb0-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9bbb0-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="9bbb0-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="9bbb0-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="9bbb0-149">Windows、Windows8、win、win8</span><span class="sxs-lookup"><span data-stu-id="9bbb0-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="9bbb0-150">針對 Windows Phone 專案，識別碼看起來會如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bbb0-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="9bbb0-151">電話作業系統</span><span class="sxs-lookup"><span data-stu-id="9bbb0-151">Phone OS</span></span> | <span data-ttu-id="9bbb0-152">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="9bbb0-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9bbb0-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9bbb0-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9bbb0-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="9bbb0-154">Windows Phone 7</span></span> | <span data-ttu-id="9bbb0-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="9bbb0-155">silverlight3-wp</span></span> | <span data-ttu-id="9bbb0-156">wp、wp7、WindowsPhone、WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="9bbb0-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="9bbb0-157">Windows Phone 7.5 (Mango) </span><span class="sxs-lookup"><span data-stu-id="9bbb0-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="9bbb0-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="9bbb0-158">silverlight4-wp71</span></span> | <span data-ttu-id="9bbb0-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="9bbb0-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="9bbb0-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="9bbb0-160">Windows Phone 8</span></span> | <span data-ttu-id="9bbb0-161">(不支援)</span><span class="sxs-lookup"><span data-stu-id="9bbb0-161">(not supported)</span></span> | <span data-ttu-id="9bbb0-162">wp8、WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="9bbb0-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="9bbb0-163">在上述所有變更中，NuGet 2.1 將繼續完整支援舊的架構名稱。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="9bbb0-164">接下來，您應該使用新的名稱，因為它們在個別平臺的未來版本中將會更穩定。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="9bbb0-165">不過，在2.1 之前的 NuGet 版本中將 *不* 支援新的名稱，因此請視需要規劃何時進行切換。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="9bbb0-166">改善封裝管理員對話方塊中的搜尋</span><span class="sxs-lookup"><span data-stu-id="9bbb0-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="9bbb0-167">在過去幾個反復專案中，已引進 NuGet 資源庫的變更，以大幅提升封裝搜尋的速度和相關性。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="9bbb0-168">不過，這些改良功能僅限於 nuget.org 網站。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="9bbb0-169">NuGet 2.1 透過 [NuGet 套件管理員] 對話方塊，讓您獲得改良的搜尋體驗。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="9bbb0-170">例如，假設您想要尋找 Windows Azure Caching Preview 套件。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="9bbb0-171">此套件的合理搜尋查詢可能是「Azure 快取」。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="9bbb0-172">在舊版的 [套件管理員] 對話方塊中，所需的套件甚至不會列在結果的第一頁。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="9bbb0-173">不過，在 NuGet 2.1 中，所需的套件現在會顯示在搜尋結果的頂端。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![套件管理員對話方塊搜尋](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="9bbb0-175">強制更新套件</span><span class="sxs-lookup"><span data-stu-id="9bbb0-175">Force Package Update</span></span>

<span data-ttu-id="9bbb0-176">在 NuGet 2.1 之前，如果沒有較高的版本號碼，NuGet 會略過更新套件。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="9bbb0-177">這對某些案例引進了一些衝突，特別是在組建或 CI 案例中，小組不想要將套件版本號碼與每個組建遞增。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="9bbb0-178">所需的行為是強制進行更新，而不是。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="9bbb0-179">NuGet 2.1 使用「重新安裝」旗標解決此情況。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="9bbb0-180">例如，當您嘗試更新的套件版本不是較新的套件時，舊版的 NuGet 會導致下列情況：</span><span class="sxs-lookup"><span data-stu-id="9bbb0-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="9bbb0-181">使用 [重新安裝] 旗標時，無論是否有較新的版本，套件都會更新。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="9bbb0-182">重新安裝旗標的另一個案例，是架構重新設為目標。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="9bbb0-183">當您變更專案的目標 framework 時 (例如，從 .NET 4 到 .NET 4.5) ，Update-Package-重新安裝可以針對在專案中安裝的所有 NuGet 套件，更新正確元件的參考。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="9bbb0-184">在 Visual Studio 中編輯套件來源</span><span class="sxs-lookup"><span data-stu-id="9bbb0-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="9bbb0-185">在舊版的 NuGet 中，從 [Visual Studio 選項] 對話方塊內更新套件來源需要刪除並重新加入套件來源。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="9bbb0-186">NuGet 2.1 藉由支援 update 做為設定使用者介面的第一個類別功能，來改善此工作流程。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![套件管理員設定對話方塊](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="9bbb0-188">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="9bbb0-188">Bug Fixes</span></span>

<span data-ttu-id="9bbb0-189">NuGet 2.1 包含許多 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="9bbb0-190">如需 NuGet 2.0 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="9bbb0-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
