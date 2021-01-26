---
title: NuGet 3.0 Preview 版本資訊
description: NuGet 3.0 Preview 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780331"
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="b5da2-103">NuGet 3.0 Preview 版本資訊</span><span class="sxs-lookup"><span data-stu-id="b5da2-103">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="b5da2-104">[NuGet 2.9 RC 版本](../release-notes/nuget-2.9-rc.md)  |  資訊[NuGet 3.0 Beta 版注意事項](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="b5da2-104">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="b5da2-105">NuGet 3.0 Preview 已于2014年11月12日發行，作為 Visual Studio 2015 Preview 版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="b5da2-105">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="b5da2-106">我們已發行 NuGet 3.0 預覽版。</span><span class="sxs-lookup"><span data-stu-id="b5da2-106">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="b5da2-107">這是我們 (的大型版本，雖然預覽) ，但我們很高興能開始取得有關變更的意見反應。</span><span class="sxs-lookup"><span data-stu-id="b5da2-107">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="b5da2-108">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="b5da2-108">Visual Studio 2012+</span></span>

<span data-ttu-id="b5da2-109">此 NuGet 3.0 預覽版包含在 Visual Studio 2015 Preview 中。</span><span class="sxs-lookup"><span data-stu-id="b5da2-109">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="b5da2-110">我們即將致力於取得 Visual Studio 2012 的預覽，並 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="b5da2-110">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="b5da2-111">我們先前已分享我們的意圖，以 [停止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，而我們的確進行了這種困難的決策。</span><span class="sxs-lookup"><span data-stu-id="b5da2-111">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="b5da2-112">全新的 UI</span><span class="sxs-lookup"><span data-stu-id="b5da2-112">Brand New UI</span></span>

<span data-ttu-id="b5da2-113">您注意到 NuGet 3.0 Preview 的第一件事，就是全新的 UI。</span><span class="sxs-lookup"><span data-stu-id="b5da2-113">The first thing you notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="b5da2-114">它不再是強制回應對話方塊;現在是完整的 Visual Studio 文件視窗。</span><span class="sxs-lookup"><span data-stu-id="b5da2-114">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="b5da2-115">如此一來，您就可以開啟多個專案的 UI， (和/或方案) 一次，將視窗移到另一個監視器，並在您想要的情況下停駐）等等。</span><span class="sxs-lookup"><span data-stu-id="b5da2-115">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="b5da2-117">除了可用性差異，由於放棄強制回應對話方塊，我們也在新的 UI 中有許多新功能。</span><span class="sxs-lookup"><span data-stu-id="b5da2-117">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="b5da2-118">版本選取專案</span><span class="sxs-lookup"><span data-stu-id="b5da2-118">Version Selection</span></span>

<span data-ttu-id="b5da2-119">可能是最常要求的 UI 功能，是允許套件安裝和更新的版本選項--這現在已可供使用。</span><span class="sxs-lookup"><span data-stu-id="b5da2-119">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![套件版本選取專案](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="b5da2-121">無論您是安裝或更新套件，[版本] 下拉式清單都可讓您查看套件可用的所有版本，而且有一些值得注意的版本會升級至清單頂端，以便方便選取。</span><span class="sxs-lookup"><span data-stu-id="b5da2-121">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="b5da2-122">您不再需要使用 PowerShell 主控台來取得不是最新版本的特定版本。</span><span class="sxs-lookup"><span data-stu-id="b5da2-122">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="b5da2-123">合併安裝/線上/更新工作流程</span><span class="sxs-lookup"><span data-stu-id="b5da2-123">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="b5da2-124">先前的 UI 有3個已安裝、線上和更新的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b5da2-124">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="b5da2-125">列出的套件是這些工作流程專屬的，而且可用的動作也是針對工作流程所特有。</span><span class="sxs-lookup"><span data-stu-id="b5da2-125">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="b5da2-126">雖然這似乎是合理的，但我們聽說過許多人通常會在這種情況下出現。</span><span class="sxs-lookup"><span data-stu-id="b5da2-126">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="b5da2-127">我們現在有結合的體驗，您可以在其中安裝、更新或卸載套件，而不論您如何選取套件。</span><span class="sxs-lookup"><span data-stu-id="b5da2-127">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="b5da2-128">為了協助特定的工作流程，我們現在有一個篩選下拉式清單，可讓您篩選出可以看見的封裝，但可供封裝使用的動作是一致的。</span><span class="sxs-lookup"><span data-stu-id="b5da2-128">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![卸載套件](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="b5da2-130">藉由使用「已安裝」篩選器，您就可以輕鬆地查看已安裝的套件、哪些套件有可用的更新，然後您可以藉由變更版本選取專案來卸載或更新套件，以查看變更可用的動作。</span><span class="sxs-lookup"><span data-stu-id="b5da2-130">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![更新套件](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="b5da2-132">版本匯總</span><span class="sxs-lookup"><span data-stu-id="b5da2-132">Version Consolidation</span></span>

<span data-ttu-id="b5da2-133">通常會將相同的套件安裝至方案內的多個專案。</span><span class="sxs-lookup"><span data-stu-id="b5da2-133">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="b5da2-134">有時候，安裝在每個專案中的版本可能會脫離，而且必須合併使用中的版本。</span><span class="sxs-lookup"><span data-stu-id="b5da2-134">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="b5da2-135">NuGet 3.0 Preview 為此案例引進了一項新功能。</span><span class="sxs-lookup"><span data-stu-id="b5da2-135">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="b5da2-136">在解決方案上按一下滑鼠右鍵，然後選擇 [管理方案的 NuGet 套件]，即可存取 [方案層級封裝管理] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b5da2-136">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="b5da2-137">從該處，如果您選取的封裝已安裝至多個專案，但使用不同的版本，則會出現新的「合併」動作。</span><span class="sxs-lookup"><span data-stu-id="b5da2-137">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="b5da2-138">在下方的螢幕擷取畫面中， `Newtonsoft.Json` 已安裝至 `SamplesClassLibrary` with 版本， `6.0.4` 並已安裝至 `SamplesConsoleApp` with version `5.0.4` 。</span><span class="sxs-lookup"><span data-stu-id="b5da2-138">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![合併版本](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="b5da2-140">以下是合併到單一版本的工作流程。</span><span class="sxs-lookup"><span data-stu-id="b5da2-140">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="b5da2-141">選取 `Newtonsoft.Json` 清單中的套件</span><span class="sxs-lookup"><span data-stu-id="b5da2-141">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="b5da2-142">`Consolidate`從 `Action` 下拉式清單中選擇</span><span class="sxs-lookup"><span data-stu-id="b5da2-142">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="b5da2-143">使用 `Version` 下拉式清單來選取要合併的版本</span><span class="sxs-lookup"><span data-stu-id="b5da2-143">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="b5da2-144">核取要合併到該版本之專案的方塊 (請注意，已在所選版本上的專案會呈現灰色) </span><span class="sxs-lookup"><span data-stu-id="b5da2-144">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="b5da2-145">按一下 `Consolidate` 按鈕以執行匯總</span><span class="sxs-lookup"><span data-stu-id="b5da2-145">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="b5da2-146">作業預覽</span><span class="sxs-lookup"><span data-stu-id="b5da2-146">Operation Previews</span></span>

<span data-ttu-id="b5da2-147">無論您正在執行哪一項作業（安裝/更新/卸載），新的 UI 現在都提供一種方式來預覽您的專案所做的變更。</span><span class="sxs-lookup"><span data-stu-id="b5da2-147">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="b5da2-148">此預覽會顯示將安裝的任何新封裝、將更新的套件，以及將卸載的封裝，以及作業期間不會變更的套件。</span><span class="sxs-lookup"><span data-stu-id="b5da2-148">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="b5da2-149">在下列範例中，我們可以看到安裝 SignalR 會導致對專案進行相當多的變更。</span><span class="sxs-lookup"><span data-stu-id="b5da2-149">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![預覽安裝 SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="b5da2-151">安裝選項</span><span class="sxs-lookup"><span data-stu-id="b5da2-151">Installation Options</span></span>

<span data-ttu-id="b5da2-152">使用 PowerShell 主控台，您可以控制幾個值得注意的安裝選項。</span><span class="sxs-lookup"><span data-stu-id="b5da2-152">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="b5da2-153">我們現在也將這些功能帶入 UI 中。</span><span class="sxs-lookup"><span data-stu-id="b5da2-153">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="b5da2-154">您現在可以控制如何選取相依性版本的相依性解析行為。</span><span class="sxs-lookup"><span data-stu-id="b5da2-154">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![相依性行為](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="b5da2-156">您也可以指定當套件中的內容檔案與已經在專案中的檔案衝突時，所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="b5da2-156">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![檔案衝突動作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="b5da2-158">無限期滾動</span><span class="sxs-lookup"><span data-stu-id="b5da2-158">Infinite Scrolling</span></span>

<span data-ttu-id="b5da2-159">我們在列出套件時，會在 UI 上取得具有滾動和分頁範例的大量意見反應。</span><span class="sxs-lookup"><span data-stu-id="b5da2-159">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="b5da2-160">很常見的情況是，您必須在簡短清單的底部按一下下一個頁碼，然後再次滾動。</span><span class="sxs-lookup"><span data-stu-id="b5da2-160">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="b5da2-161">在新的 UI 中，我們已在套件清單中執行無限期的滾動，因此您只需要滾動，就不需要再進行分頁。</span><span class="sxs-lookup"><span data-stu-id="b5da2-161">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![無限期滾動](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="b5da2-163">使其正常運作，使其變得更快速，讓它變得很美觀</span><span class="sxs-lookup"><span data-stu-id="b5da2-163">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="b5da2-164">我們很高興能讓您試用這個新的 UI。在此預覽里程碑中，我們已遵循良好的舊」古訓「讓它正常運作，讓它變得相當快速」。</span><span class="sxs-lookup"><span data-stu-id="b5da2-164">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="b5da2-165">在此預覽中，我們已完成大部分的第一個目標，也就是可行的。</span><span class="sxs-lookup"><span data-stu-id="b5da2-165">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="b5da2-166">我們知道它的速度不夠快，而我們也知道它還不太棒。</span><span class="sxs-lookup"><span data-stu-id="b5da2-166">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="b5da2-167">相信我們將在現在和 RC 版本之間處理這些目標。</span><span class="sxs-lookup"><span data-stu-id="b5da2-167">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="b5da2-168">在此同時，我們很樂意聽到您對於新 UI *可用性* 的意見反應 *，也就* 是工作流程、作業，以及使用新 ui 的方式。</span><span class="sxs-lookup"><span data-stu-id="b5da2-168">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="b5da2-169">相較于舊的 UI，我們已移除一些函數。</span><span class="sxs-lookup"><span data-stu-id="b5da2-169">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="b5da2-170">其中一個是故意的，而另一個則不是在時間內完成。</span><span class="sxs-lookup"><span data-stu-id="b5da2-170">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="b5da2-171">搜尋「所有」套件來源</span><span class="sxs-lookup"><span data-stu-id="b5da2-171">Searching "All" Package Sources</span></span>

<span data-ttu-id="b5da2-172">舊的 UI 可讓您針對所有套件來源執行封裝搜尋。</span><span class="sxs-lookup"><span data-stu-id="b5da2-172">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="b5da2-173">我們已在 UI 中移除該功能，而不會將它重新開機。</span><span class="sxs-lookup"><span data-stu-id="b5da2-173">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="b5da2-174">這項功能是用來對您的所有套件來源執行搜尋作業、將結果結合在一起，然後根據您的排序選取專案嘗試排序結果。</span><span class="sxs-lookup"><span data-stu-id="b5da2-174">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="b5da2-175">我們發現搜尋相關性真的很難在一起。</span><span class="sxs-lookup"><span data-stu-id="b5da2-175">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="b5da2-176">您是否可以想像針對 Google 和 Bing 執行搜尋，並將結果統稱在一起？</span><span class="sxs-lookup"><span data-stu-id="b5da2-176">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="b5da2-177">此外，這項功能的速度很慢、很容易不 *小心* 使用，而且我們認為這項功能很少會很有用。</span><span class="sxs-lookup"><span data-stu-id="b5da2-177">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="b5da2-178">由於這項功能所帶來的問題，我們收到了一些可能未曾修正的 bug 報告。</span><span class="sxs-lookup"><span data-stu-id="b5da2-178">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="b5da2-179">全部更新</span><span class="sxs-lookup"><span data-stu-id="b5da2-179">Update All</span></span>

<span data-ttu-id="b5da2-180">在舊的 UI 中，我們已使用新的 UI 中的 [全部更新] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5da2-180">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="b5da2-181">我們會針對 RC 版本 resurrect 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b5da2-181">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="b5da2-182">新用戶端/伺服器 API</span><span class="sxs-lookup"><span data-stu-id="b5da2-182">New Client/Server API</span></span>

<span data-ttu-id="b5da2-183">除了新套件管理 UI 中的所有新功能之外，我們也已經處理 NuGet 用戶端/伺服器通訊協定的一些執行詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b5da2-183">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="b5da2-184">我們所做的工作是建立 NuGet 的「API v3」，這是針對重大案例（例如套件還原和安裝封裝）的高可用性而設計的。</span><span class="sxs-lookup"><span data-stu-id="b5da2-184">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="b5da2-185">新的 API 是以 REST 和超媒體為基礎，而且我們選取了 [JSON-LD](http://json-ld.org) 作為資源格式。</span><span class="sxs-lookup"><span data-stu-id="b5da2-185">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="b5da2-186">在 NuGet 3.0 預覽版本中，您會在 [套件來源] 下拉式清單中看到名為 "preview.nuget.org" 的新套件來源。</span><span class="sxs-lookup"><span data-stu-id="b5da2-186">In the NuGet 3.0 Preview bits, you see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="b5da2-187">如果您選取該套件來源，我們將使用新的 API，而不是連接到 nuget.org。我們已將預覽來源提供給 UI，同時繼續測試、修改和改進新的 API。</span><span class="sxs-lookup"><span data-stu-id="b5da2-187">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="b5da2-188">在 NuGet 3.0 RC 中，這個新的 API v3 套件來源會取代 v2 型的 "nuget.org" 套件來源。</span><span class="sxs-lookup"><span data-stu-id="b5da2-188">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="b5da2-189">儘管我們將投入 API v3 的投資，我們也讓所有這些新功能都能與現有的 API v2 通訊協定搭配使用，這表示它們也會使用 nuget.org 以外的現有套件來源。</span><span class="sxs-lookup"><span data-stu-id="b5da2-189">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="b5da2-190">即將推出新功能</span><span class="sxs-lookup"><span data-stu-id="b5da2-190">New Features Coming</span></span>

<span data-ttu-id="b5da2-191">除了您在 UI 中看到的內容之外，我們也會在現在和 3.0 RTM 之間處理一些基本的新 NuGet 功能。</span><span class="sxs-lookup"><span data-stu-id="b5da2-191">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you see in the UI.</span></span> <span data-ttu-id="b5da2-192">以下是顯著的投資領域的簡短清單：</span><span class="sxs-lookup"><span data-stu-id="b5da2-192">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="b5da2-193">我們與 Visual Studio 和 MSBuild 小組合作，讓 [NuGet 更深入地進入平臺](http://blog.nuget.org/20141014/in-the-platform.html)。</span><span class="sxs-lookup"><span data-stu-id="b5da2-193">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="b5da2-194">我們正致力於放棄安裝階段套件慣例，並藉由引進新的「權威」 [套件資訊清單](http://blog.nuget.org/20141023/package-manifests.html)，在封裝時期套用這些慣例。</span><span class="sxs-lookup"><span data-stu-id="b5da2-194">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="b5da2-195">我們致力於重構 NuGet 程式碼基底，讓用戶端和伺服器元件可在 Visual Studio 的套件管理之外的不同網域中重複使用。</span><span class="sxs-lookup"><span data-stu-id="b5da2-195">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="b5da2-196">我們正在調查「私用相依性」的概念，其中套件可能會指出它相依于其他封裝的相依性，僅供執行詳細資料，而這些相依性不應該呈現為最上層的相依性。</span><span class="sxs-lookup"><span data-stu-id="b5da2-196">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="b5da2-197">持續關注</span><span class="sxs-lookup"><span data-stu-id="b5da2-197">Stay Tuned</span></span>

<span data-ttu-id="b5da2-198">請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多 NuGet 3.0 的進度和公告！</span><span class="sxs-lookup"><span data-stu-id="b5da2-198">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>