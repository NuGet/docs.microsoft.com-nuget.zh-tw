---
title: "尋找及選擇 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8886f899-797b-4704-9d16-820b55b71186
description: "如何尋找和選擇專案之最佳 NuGet 套件的概觀，包含 NuGet 搜尋語法的詳細資料。"
keywords: "NuGet 套件使用, NuGet 套件探索, 最佳 NuGet 套件, 在套件上決定, 使用套件, 評估套件, NuGet 搜尋語法"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c52fa237a663fcf227e8336534d344e432523b4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a><span data-ttu-id="69649-104">尋找和評估您專案的 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="69649-104">Finding and evaluating NuGet packages for your project</span></span>

<span data-ttu-id="69649-105">啟動任何 .NET 專案時，或只要識別到您應用程式或服務的功能需求時，就可以使用滿足這項需求的現有 NuGet 套件來節省大量時間和麻煩。</span><span class="sxs-lookup"><span data-stu-id="69649-105">When starting any .NET project, or whenever you identify a functional need for your app or service, you can save yourself lots of time and trouble by using existing NuGet packages that fulfill that need.</span></span> <span data-ttu-id="69649-106">這些套件可以來自 [nuget.org](http://www.nuget.org/packages/) 上的公用集合，或是您組織或其他協力廠商所提供的私人來源。</span><span class="sxs-lookup"><span data-stu-id="69649-106">These packages can come from the public collection on [nuget.org](http://www.nuget.org/packages/), or a private source that's provided by your organization or another third party.</span></span>

## <a name="finding-packages"></a><span data-ttu-id="69649-107">尋找套件</span><span class="sxs-lookup"><span data-stu-id="69649-107">Finding packages</span></span>

<span data-ttu-id="69649-108">當您前往 nuget.org 或在 Visual Studio 中開啟套件管理員 UI 時，會看到依總下載次數排序的套件清單。</span><span class="sxs-lookup"><span data-stu-id="69649-108">When you visit nuget.org or open the Package Manager UI in Visual Studio, you see a list of packages sorted by total downloads.</span></span> <span data-ttu-id="69649-109">這會立即顯示數百萬個 .NET 專案中您最廣泛使用的套件。</span><span class="sxs-lookup"><span data-stu-id="69649-109">This immediately shows you the most widely-used packages across the millions of .NET projects.</span></span> <span data-ttu-id="69649-110">接著，前幾個頁面上列出的套件至少有一些可能適用於您的專案。</span><span class="sxs-lookup"><span data-stu-id="69649-110">There's a good chance, then, that at least some of the packages listed on the first few pages will be useful in your projects.</span></span>

![顯示最常用套件的 nuget.org/套件的預設檢視](media/Finding-01-Popularity.png)

<span data-ttu-id="69649-112">請注意頁面右上方的 [包含發行前版本] 選項。</span><span class="sxs-lookup"><span data-stu-id="69649-112">Notice the **Include prerelease** option on the upper right of the page.</span></span> <span data-ttu-id="69649-113">選取時，nuget.org 會顯示套件的所有版本，包含搶鮮版 (Beta) 和其他早期版本。</span><span class="sxs-lookup"><span data-stu-id="69649-113">When selected, nuget.org shows all versions of packages including beta and other early releases.</span></span> <span data-ttu-id="69649-114">若只要顯示穩定發行的版本，請清除此選項。</span><span class="sxs-lookup"><span data-stu-id="69649-114">To show only stable released, clear the option.</span></span>

<span data-ttu-id="69649-115">針對特定需求，依標記搜尋 (在 Visual Studio 的套件管理員內或在 nuget.org 這類入口網站上) 是探索適合套件的最常見方法。</span><span class="sxs-lookup"><span data-stu-id="69649-115">For specific needs, searching by tags (within Visual Studio's Package Manager or on a portal like nuget.org) is the most common means of discovering a suitable package.</span></span> <span data-ttu-id="69649-116">例如，搜尋 "json" 會列出所有標上該關鍵字的 NuGet 套件，因此具有與 JSON 資料格式的某種關聯性。</span><span class="sxs-lookup"><span data-stu-id="69649-116">For example, searching on "json" lists all NuGet packages that are tagged with that keyword and thus have some relationship to the JSON data format.</span></span>

![nuget.org 上 'json' 的搜尋結果](media/Finding-02-SearchResults.png)

<span data-ttu-id="69649-118">您也可以使用已知的套件識別碼進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="69649-118">You can also search using the package ID, if you know it.</span></span> <span data-ttu-id="69649-119">請參閱下面的[搜尋語法](#search-syntax)。</span><span class="sxs-lookup"><span data-stu-id="69649-119">See [Search Syntax](#search-syntax) below.</span></span>

<span data-ttu-id="69649-120">此時，只會依相關性來排序搜尋結果，因此您一般至少會想要查看符合您需求的前幾頁套件結果，或將您的搜尋字詞精簡為更為具體。</span><span class="sxs-lookup"><span data-stu-id="69649-120">At this time, search results are sorted only by relevance, so you generally want to look through at least the first few pages of results for packages that suit your needs, or refine your search terms to be more specific.</span></span>

### <a name="does-the-package-support-my-projects-target-framework"></a><span data-ttu-id="69649-121">套件支援我專案的目標架構嗎？</span><span class="sxs-lookup"><span data-stu-id="69649-121">Does the package support my project's target framework?</span></span>

<span data-ttu-id="69649-122">只有在套件支援的架構包含專案的目標架構時，NuGet 才會將該套件安裝至專案 </span><span class="sxs-lookup"><span data-stu-id="69649-122">NuGet installs a package into a project only if that package's supported frameworks include the project's target framework.</span></span> <span data-ttu-id="69649-123">(如需在建立套件時如何完成這項作業的資訊，請參閱[支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md))。如果套件不相容，NuGet 就會發出錯誤。</span><span class="sxs-lookup"><span data-stu-id="69649-123">(See [Supporting multiple target frameworks](../create-packages/supporting-multiple-target-frameworks.md) for how this is done when creating a package.) If the package is not compatible, NuGet issues an error.</span></span>

<span data-ttu-id="69649-124">部分套件會直接在 nuget.org 資源庫中列出其支援的架構，但因為不需要這類資料，所以許多套件都不會包含該清單。</span><span class="sxs-lookup"><span data-stu-id="69649-124">Some packages list their supported frameworks directly in the nuget.org gallery, but because such data is not required, many packages do not include that list.</span></span> <span data-ttu-id="69649-125">目前沒有方法可以搜尋 nuget.org 中是否有支援特定目標架構的套件 (這項功能已列入考量，請參閱 [NuGet 問題 2936](https://github.com/NuGet/NuGetGallery/issues/2936))。</span><span class="sxs-lookup"><span data-stu-id="69649-125">At present there is no means to search nuget.org for packages that support a specific target framework (the feature is under consideration, see [NuGet Issue 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).</span></span>

<span data-ttu-id="69649-126">幸運的是，您可以透過其他兩種方法來判斷支援的架構：</span><span class="sxs-lookup"><span data-stu-id="69649-126">Fortunately, you can determine supported frameworks through two other means:</span></span>

1. <span data-ttu-id="69649-127">嘗試在 NuGet 套件管理員主控台中使用 [`Install-Package`](../tools/ps-ref-install-package.md) 命令，以將套件安裝至專案。</span><span class="sxs-lookup"><span data-stu-id="69649-127">Attempt to install a package into a project using the [`Install-Package`](../tools/ps-ref-install-package.md) command in the NuGet Package Manager Console.</span></span> <span data-ttu-id="69649-128">如果套件不相容，則此命令會顯示套件所支援的架構。</span><span class="sxs-lookup"><span data-stu-id="69649-128">If the package is incompatible, this command shows you the package's supported frameworks.</span></span>

1. <span data-ttu-id="69649-129">使用 [資訊] 下的 [手動下載] 連結，以從套件在 nuget.org 上的頁面下載套件。</span><span class="sxs-lookup"><span data-stu-id="69649-129">Download the package from its page on nuget.org using the **Manual download** link under **Info**.</span></span> <span data-ttu-id="69649-130">將副檔名從 `.nupkg` 變更為 `.zip`，並開啟檔案來檢查其 `lib` 資料夾的內容。</span><span class="sxs-lookup"><span data-stu-id="69649-130">Change the extension from `.nupkg` to `.zip`, and open the file to examine the content of its `lib` folder.</span></span> <span data-ttu-id="69649-131">您會在那裡看到每個所支援架構的子資料夾，其中使用目標 Framework Moniker (TFM；請參閱[目標 Framework](../reference/target-frameworks.md)) 來命名每個子資料夾。</span><span class="sxs-lookup"><span data-stu-id="69649-131">There you see subfolders for each of the supported frameworks, where each subfolder is named with a target framework moniker (TFM; see [Target Frameworks](../reference/target-frameworks.md)).</span></span> <span data-ttu-id="69649-132">如果您在 `lib` 下看不到任何子資料夾，而且只有單一 DLL，則必須嘗試將套件安裝至您的專案，以探索其相容性。</span><span class="sxs-lookup"><span data-stu-id="69649-132">If you see no subfolders under `lib` and only a single DLL, then you must attempt to install the package in your project to discover its compatibility.</span></span>

## <a name="pre-release-packages"></a><span data-ttu-id="69649-133">發行前套件</span><span class="sxs-lookup"><span data-stu-id="69649-133">Pre-release packages</span></span>

<span data-ttu-id="69649-134">許多套件作者都會將預覽和搶鮮版 (Beta) 版本設為可用，因為他們會繼續進行改善並搜尋其最新版本的意見。</span><span class="sxs-lookup"><span data-stu-id="69649-134">Many package authors make preview and beta releases available as they continue to make improvements and seek feedback on their latest revisions.</span></span>

<span data-ttu-id="69649-135">nuget.org 預設會在搜尋結果中顯示發行前套件。</span><span class="sxs-lookup"><span data-stu-id="69649-135">By default, nuget.org shows pre-release packages in search results.</span></span> <span data-ttu-id="69649-136">若只要搜尋穩定發行版本，請清除頁面右上方的 [包含發行前版本] 選項</span><span class="sxs-lookup"><span data-stu-id="69649-136">To search only stable releases, clear the **Include prerelease** option on the upper right of the page</span></span>

![nuget.org 上的 [包含發行前版本] 核取方塊](media/Finding-06-include-prerelease.png)

<span data-ttu-id="69649-138">在 Visual Studio 中，並且使用 NuGet CLI 時，NuGet 預設不會包含發行前版本。</span><span class="sxs-lookup"><span data-stu-id="69649-138">In Visual Studio and when using the NuGet CLI, NuGet does not include pre-release versions by default.</span></span> <span data-ttu-id="69649-139">若要變更此行為，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="69649-139">To change this behavior, do the following steps:</span></span>

- <span data-ttu-id="69649-140">**Visual Studio 中的套件管理員 UI**：在 [管理 NuGet 套件] UI 中，設定 [包含發行前版本] 方塊。</span><span class="sxs-lookup"><span data-stu-id="69649-140">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, set the **Include prerelease** box.</span></span> <span data-ttu-id="69649-141">設定或清除此方塊時，會重新整理套件管理員 UI 以及您可以安裝的可用版本清單。</span><span class="sxs-lookup"><span data-stu-id="69649-141">Setting or clearing this box refreshes the Package Manager UI and the list of available versions you can install.</span></span>

    ![Visual Studio 中的 [包含發行前版本] 核取方塊](media/Prerelease_02-CheckPrerelease.png)

- <span data-ttu-id="69649-143">**套件管理員主控台**：使用 `-IncludePrerelease` 參數搭配 `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package` 和 `Update-Package` 命令。</span><span class="sxs-lookup"><span data-stu-id="69649-143">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="69649-144">請參閱 [PowerShell 參考](../tools/powershell-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="69649-144">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="69649-145">**NuGet CLI**：使用 `-prerelease` 參數搭配 `install`、`update`、`delete` 和 `mirror` 命令。</span><span class="sxs-lookup"><span data-stu-id="69649-145">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="69649-146">請參閱 [NuGet CLI 參考](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="69649-146">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a><span data-ttu-id="69649-147">原生 C++ 套件</span><span class="sxs-lookup"><span data-stu-id="69649-147">Native C++ packages</span></span>

<span data-ttu-id="69649-148">NuGet 支援可在 Visual Studio 中用於 C++ 專案的原生 C++ 套件。</span><span class="sxs-lookup"><span data-stu-id="69649-148">NuGet supports native C++ packages can that can be used in C++ projects in Visual Studio.</span></span> <span data-ttu-id="69649-149">這會啟用專案的 [管理 NuGet 套件] 操作功能表命令、引進 `native` 目標架構，並提供 MSBuild 整合。</span><span class="sxs-lookup"><span data-stu-id="69649-149">This enables the **Manage NuGet Packages** context-menu command for projects, introduces a `native` target framework, and provides MSBuild integration.</span></span>

<span data-ttu-id="69649-150">若要在 [nuget.org](https://www.nuget.org/packages) 上尋找原生套件，請使用 `tag:native` 進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="69649-150">To find native packages on [nuget.org](https://www.nuget.org/packages), search using `tag:native`.</span></span> <span data-ttu-id="69649-151">這類套件一般會提供 `.targets` 和 `.props` 檔案，而 NuGet 會在將套件新增至專案時自動匯入這些檔案。</span><span class="sxs-lookup"><span data-stu-id="69649-151">Such packages typically provide `.targets` and `.props` files, which NuGet imports automatically when the package is added to a project.</span></span>

## <a name="evaluating-packages"></a><span data-ttu-id="69649-152">評估套件</span><span class="sxs-lookup"><span data-stu-id="69649-152">Evaluating packages</span></span>

<span data-ttu-id="69649-153">評估套件實用性的最佳方式是下載套件並在您的程式碼中進行試用。</span><span class="sxs-lookup"><span data-stu-id="69649-153">The best way to evaluate the usefulness of a package is to download it and try it out in your code.</span></span> <span data-ttu-id="69649-154">畢竟，只有少數使用高度常用之套件的開發人員才能啟動高度常用的套件，而且您可能是早期採用者 </span><span class="sxs-lookup"><span data-stu-id="69649-154">After all, every highly popular package got started with only a few developers using it, and you might be one of the early adopters!</span></span> <span data-ttu-id="69649-155">(請注意，nuget.org 上的所有套件都會定期掃描是否有病毒)。</span><span class="sxs-lookup"><span data-stu-id="69649-155">(Note that all packages on nuget.org are routinely scanned for viruses.)</span></span>

<span data-ttu-id="69649-156">同時，使用 NuGet 套件表示與其相依，因此您想要確定其為穩定且可靠。</span><span class="sxs-lookup"><span data-stu-id="69649-156">At the same time, using a NuGet package means taking a dependency on it, so you want to make sure it's robust and reliable.</span></span> <span data-ttu-id="69649-157">因為安裝和直接測試套件相當耗時，所以您也可以使用套件清單頁面上的資訊來深入了解套件品質：</span><span class="sxs-lookup"><span data-stu-id="69649-157">Because installing and directly testing a package is time-consuming, you can also learn a lot about a package's quality by using the information on a package's listing page:</span></span>

- <span data-ttu-id="69649-158">*下載統計資料*：在 nuget.org 的套件頁面上，[統計資料] 區段會顯示總下載次數、最新版的下載，以及每天的平均下載次數。</span><span class="sxs-lookup"><span data-stu-id="69649-158">*Downloads statistics*: on the package page on nuget.org, the **Statistics** section shows total downloads, downloads of the most recent version, and average downloads per day.</span></span> <span data-ttu-id="69649-159">較大的數字指出許多其他開發人員都具有與套件的相依性，這表示它已證明它自己。</span><span class="sxs-lookup"><span data-stu-id="69649-159">Larger numbers indicate that many other developers have taken a dependency on the package, which means that it has proven itself.</span></span>

    ![下載套件清單頁面上的統計資料](media/Finding-03-Downloads.png)

- <span data-ttu-id="69649-161">*版本歷程記錄*：在套件頁面上，查看 [資訊] 下的最新更新日期，並檢查 [版本歷程記錄]。</span><span class="sxs-lookup"><span data-stu-id="69649-161">*Version history*: on the package page, look under **Info** for the date of the most recent update and examine the **Version History**.</span></span> <span data-ttu-id="69649-162">維護良好的套件具有新的更新和豐富的版本歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="69649-162">A well-maintained package has recent updates and a rich version history.</span></span> <span data-ttu-id="69649-163">忽略的套件有幾個更新，而且有時通常尚未更新。</span><span class="sxs-lookup"><span data-stu-id="69649-163">Neglected packages have few updates and often haven't been updated in some time.</span></span>

    ![套件清單頁面上的版本歷程記錄](media/Finding-04-VersionHistory.png)

- <span data-ttu-id="69649-165">*最近安裝*：在套件頁面的 [統計資料] 下方，選取 [View full stats] (檢視完整統計資料)。完整統計資料頁面會依版本號碼顯示過去六週的套件安裝。</span><span class="sxs-lookup"><span data-stu-id="69649-165">*Recent installs*: on the package page under **Statistics**, select **View full stats**. The full stats page shows the package installs over the last six weeks by version number.</span></span> <span data-ttu-id="69649-166">其他開發人員主動使用的套件一般是比未使用的套件還適合的選擇。</span><span class="sxs-lookup"><span data-stu-id="69649-166">A package that other developers are actively using is typically a better choice than one that's not.</span></span>

- <span data-ttu-id="69649-167">*支援*：在套件頁面的 [資訊] 下方，選取 [專案網站] \(如果有的話) 以查看可用的支援選項。</span><span class="sxs-lookup"><span data-stu-id="69649-167">*Support*: on the package page under **Info**, select **Project Site** (if available) to see what support options are available.</span></span> <span data-ttu-id="69649-168">具有專用網站的專案通常有較佳的支援。</span><span class="sxs-lookup"><span data-stu-id="69649-168">A project with a dedicated site is generally better supported.</span></span>

- <span data-ttu-id="69649-169">*開發人員歷程記錄*：在套件頁面的 [擁有者] 下方，選取擁有者以查看他們已發行的其他套件。</span><span class="sxs-lookup"><span data-stu-id="69649-169">*Developer history*: on the package page under **Owners**, select an owner to see what other packages they've published.</span></span> <span data-ttu-id="69649-170">具有多個套件的擁有者未來較可能繼續支援其工作。</span><span class="sxs-lookup"><span data-stu-id="69649-170">Those with multiple packages are more likely to continue supporting their work in the future.</span></span>

- <span data-ttu-id="69649-171">*開放原始碼參與*：開放原始碼存放庫會維護許多套件，因此與其相依的開發人員可以直接參與 Bug 修正和功能改善。</span><span class="sxs-lookup"><span data-stu-id="69649-171">*Open source contributions*: many packages are maintained in open-source repositories, making it possible for developers depending on them to directly contribute bug fixes and feature improvements.</span></span> <span data-ttu-id="69649-172">任何指定套件的參與歷程記錄也是有多少開發人員主動參與的不錯指標。</span><span class="sxs-lookup"><span data-stu-id="69649-172">The contribution history of any given package is also a good indicator of how many developers are actively involved.</span></span>

- <span data-ttu-id="69649-173">*訪談擁有者*：可以肯定平均認可新的開發人員，以產生您可使用的不錯套件，讓它們有機會帶入 NuGet 生態系統的新項目。</span><span class="sxs-lookup"><span data-stu-id="69649-173">*Interview the owners*: new developers can certainly be equally committed to producing great packages for you to use, and it's good to give them a chance to bring something new to the NuGet ecosystem.</span></span> <span data-ttu-id="69649-174">請記住，透過清單頁面的 [資訊] 下方的 [連絡擁有者] 選項直接聯繫套件開發人員。</span><span class="sxs-lookup"><span data-stu-id="69649-174">With this in mind, reach out directly to the package developers through the **Contact Owners** option under **Info** on the listing page.</span></span> <span data-ttu-id="69649-175">而且他們很樂意與您合作來滿足您的需求！</span><span class="sxs-lookup"><span data-stu-id="69649-175">Chances are, they'll be happy to work with you to serve your needs!</span></span>

> [!Note]
> <span data-ttu-id="69649-176">請一律留意套件的授權條款，而選取 nuget.org 的套件清單頁面上的 [授權資訊] 即可看到授權條款。如果套件未指定授權條款，請使用套件頁面上的 [連絡擁有者] 連結直接連絡套件擁有者。</span><span class="sxs-lookup"><span data-stu-id="69649-176">Always be mindful of a package's license terms, which you can see by selecting **License Info** on a package's listing page on nuget.org. If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="69649-177">Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="69649-177">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="search-syntax"></a><span data-ttu-id="69649-178">搜尋語法</span><span class="sxs-lookup"><span data-stu-id="69649-178">Search Syntax</span></span>

<span data-ttu-id="69649-179">在 nuget.org 上、從 NuGet CLI 中，以及 Visual Studio 的 NuGet 套件管理員延伸模組內，NuGet 套件搜尋的運作都相同。</span><span class="sxs-lookup"><span data-stu-id="69649-179">NuGet package search works the same on nuget.org, from the NuGet CLI, and within the NuGet Package Manager extension in Visual Studio.</span></span> <span data-ttu-id="69649-180">一般而言，會將搜尋套用至關鍵字和套件描述。</span><span class="sxs-lookup"><span data-stu-id="69649-180">In general, search is applied to keywords as well as package descriptions.</span></span>

- <span data-ttu-id="69649-181">**關鍵字**：搜尋會尋找包含所有已提供關鍵字的相關套件。</span><span class="sxs-lookup"><span data-stu-id="69649-181">**Keywords**: Search looks for relevant packages that contain all the provided keywords.</span></span> <span data-ttu-id="69649-182">範例：</span><span class="sxs-lookup"><span data-stu-id="69649-182">Example:</span></span>

    ```
    modern UI javascript
    ```

- <span data-ttu-id="69649-183">**詞組**：輸入以雙引號括住的字詞會尋找與這些字詞完全相同且不區分大小寫的相符項。</span><span class="sxs-lookup"><span data-stu-id="69649-183">**Phrases**: Entering terms within quotation marks looks for exact case-insensitive matches to those terms.</span></span> <span data-ttu-id="69649-184">範例：</span><span class="sxs-lookup"><span data-stu-id="69649-184">Example:</span></span>

    ```
    "modern UI" package
    ```

- <span data-ttu-id="69649-185">**篩選**：您可以使用 `<property>:<term>` 語法，將搜尋字詞套用至特定屬性，其中 `<property>` (不區分大小寫) 可以是 `id`、`packageid`、`version`、`title`、`tags`、`author`、`description`、`summary` 和 `owner`。</span><span class="sxs-lookup"><span data-stu-id="69649-185">**Filtering**: You can apply a search term to a specific property by using the syntax `<property>:<term>` where `<property>` (case-insensitive) can be `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, and `owner`.</span></span> <span data-ttu-id="69649-186">必要時，可以使用引號括住字詞，而且您可以同時搜尋多個屬性。</span><span class="sxs-lookup"><span data-stu-id="69649-186">Terms can be contained in quotes if needed, and you can search for multiple properties at the same time.</span></span> <span data-ttu-id="69649-187">此外，對 `id` 屬性的搜尋是子字串比對，而 `packageid` 使用精確比對。</span><span class="sxs-lookup"><span data-stu-id="69649-187">Also, searches on the `id` property are substring matches, whereas `packageid` uses an exact match.</span></span> <span data-ttu-id="69649-188">例如：</span><span class="sxs-lookup"><span data-stu-id="69649-188">Examples:</span></span>

    ```
    id:NuGet.Core                //Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 //Searches title as shown on the package listing
    PackageId:jquery             //Match the package id exactly
    id:jquery id:ui              //Search for multiple terms in the id
    id:jquery tags:validation    //Search multiple properties
    id:"jquery.ui"               //Phrase search
    invalid:jquery ui            //Unsupported properties are ignored, so this
                                 //is the same as searching on jquery ui
    ```