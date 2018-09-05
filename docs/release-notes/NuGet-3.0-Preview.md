---
title: NuGet 3.0 版的 Preview 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.0 Preview 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546461"
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="f861e-103">NuGet 3.0 版的 Preview 版本資訊</span><span class="sxs-lookup"><span data-stu-id="f861e-103">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="f861e-104">[NuGet 2.9 RC 版本資訊](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta 版本資訊](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="f861e-104">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="f861e-105">NuGet 3.0 Preview 於 2014 年 11 月 12 日 Visual Studio 2015 Preview 版本發行。</span><span class="sxs-lookup"><span data-stu-id="f861e-105">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="f861e-106">我們發行了 NuGet 3.0 預覽。</span><span class="sxs-lookup"><span data-stu-id="f861e-106">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="f861e-107">這是大型的發表，我們 （雖然預覽中），和我們很高興能夠開始取得意見反應，我們變更。</span><span class="sxs-lookup"><span data-stu-id="f861e-107">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="f861e-108">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="f861e-108">Visual Studio 2012+</span></span>

<span data-ttu-id="f861e-109">這個 NuGet 3.0 預覽包含在 Visual Studio 2015 Preview 中。</span><span class="sxs-lookup"><span data-stu-id="f861e-109">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="f861e-110">我們正努力取得預覽卸除 Visual Studio 2012 和 Visual Studio 2013 推出。</span><span class="sxs-lookup"><span data-stu-id="f861e-110">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="f861e-111">我們之前告訴大家我們試圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，但未將該相當困難的決定。</span><span class="sxs-lookup"><span data-stu-id="f861e-111">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="f861e-112">全新的 UI</span><span class="sxs-lookup"><span data-stu-id="f861e-112">Brand New UI</span></span>

<span data-ttu-id="f861e-113">您會注意到關於 NuGet 3.0 預覽第一件事是我們全新的 UI。</span><span class="sxs-lookup"><span data-stu-id="f861e-113">The first thing you notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="f861e-114">它不再是強制回應對話方塊;它現在是完整的 Visual Studio 文件視窗。</span><span class="sxs-lookup"><span data-stu-id="f861e-114">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="f861e-115">這可讓您一次開啟多個專案 （和/或解決方案） 的 UI、 的視窗切割到另一個監視器、 將它停駐，不過，您會願意等等。</span><span class="sxs-lookup"><span data-stu-id="f861e-115">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="f861e-117">超過使用性的差異，因為放棄強制回應對話方塊，我們也有許多新功能在新的 UI 中。</span><span class="sxs-lookup"><span data-stu-id="f861e-117">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="f861e-118">版本選取項目</span><span class="sxs-lookup"><span data-stu-id="f861e-118">Version Selection</span></span>

<span data-ttu-id="f861e-119">最可能是要求 UI 功能可讓版本選取項目套件安裝和更新，這是立即可用。</span><span class="sxs-lookup"><span data-stu-id="f861e-119">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![套件版本選取項目](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="f861e-121">是否要安裝或更新套件，[版本] 下拉式清單可讓您查看所有具有某些值得注意的版本升級為簡單的選取清單的頂端提供套件的版本。</span><span class="sxs-lookup"><span data-stu-id="f861e-121">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="f861e-122">您不再需要使用 PowerShell 主控台，以取得不是最新的特定版本。</span><span class="sxs-lookup"><span data-stu-id="f861e-122">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="f861e-123">合併的安裝/連線/更新工作流程</span><span class="sxs-lookup"><span data-stu-id="f861e-123">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="f861e-124">我們先前的 UI 有上線，已安裝和更新的 3 個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f861e-124">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="f861e-125">列出的套件所特有的工作流程和可用的動作所特有的工作流程。</span><span class="sxs-lookup"><span data-stu-id="f861e-125">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="f861e-126">雖然看似合理的我們聽到許多您通常會取得挫敗由這種區隔。</span><span class="sxs-lookup"><span data-stu-id="f861e-126">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="f861e-127">我們現在有合併的體驗，您可以用它來安裝、 更新，或解除安裝的封裝，不論您如何取得選取的封裝。</span><span class="sxs-lookup"><span data-stu-id="f861e-127">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="f861e-128">為了協助特定的工作流程，我們現在可以篩選下拉式清單，可讓您篩選可見，封裝，但適用於封裝的動作則一致。</span><span class="sxs-lookup"><span data-stu-id="f861e-128">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![解除安裝套件](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="f861e-130">藉由使用 「 安裝 」 篩選條件，您就可以輕鬆地觀察哪些有可用的更新，您已安裝的封裝，然後您可以解除安裝或變更版本選取項目，以查看更新的封裝變更可用的動作。</span><span class="sxs-lookup"><span data-stu-id="f861e-130">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![更新的套件](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="f861e-132">版本彙總</span><span class="sxs-lookup"><span data-stu-id="f861e-132">Version Consolidation</span></span>

<span data-ttu-id="f861e-133">通常會有相同的套件安裝到您的方案中的多個專案。</span><span class="sxs-lookup"><span data-stu-id="f861e-133">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="f861e-134">有時安裝到每個專案的版本可以相隔漂移，就必須彙總中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="f861e-134">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="f861e-135">NuGet 3.0 Preview 引進了新的功能，只要在此案例。</span><span class="sxs-lookup"><span data-stu-id="f861e-135">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="f861e-136">方案層級套件的 管理 視窗可以存取方案上按一下滑鼠右鍵，然後選擇 管理方案的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="f861e-136">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="f861e-137">在這裡，如果您選取 封裝安裝到多個專案，但使用不同的版本，在使用中，新的 「 合併 」 動作會變成可用。</span><span class="sxs-lookup"><span data-stu-id="f861e-137">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="f861e-138">在下列螢幕擷取畫面，`Newtonsoft.Json`已安裝到`SamplesClassLibrary`版`6.0.4`，並已安裝到`SamplesConsoleApp`版本`5.0.4`。</span><span class="sxs-lookup"><span data-stu-id="f861e-138">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![彙總版本](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="f861e-140">以下是合併到單一版本的工作流程。</span><span class="sxs-lookup"><span data-stu-id="f861e-140">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="f861e-141">選取`Newtonsoft.Json`清單中的封裝</span><span class="sxs-lookup"><span data-stu-id="f861e-141">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="f861e-142">選擇`Consolidate`從`Action`下拉式清單中</span><span class="sxs-lookup"><span data-stu-id="f861e-142">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="f861e-143">使用`Version`下拉式清單，選取要合併到的版本</span><span class="sxs-lookup"><span data-stu-id="f861e-143">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="f861e-144">核取方塊的專案，應該會合併到該版本 （請注意，已在選取的版本上的專案會呈現灰色）</span><span class="sxs-lookup"><span data-stu-id="f861e-144">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="f861e-145">按一下 `Consolidate`按鈕以執行彙總</span><span class="sxs-lookup"><span data-stu-id="f861e-145">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="f861e-146">作業預覽</span><span class="sxs-lookup"><span data-stu-id="f861e-146">Operation Previews</span></span>

<span data-ttu-id="f861e-147">不論您執行-哪一個作業安裝/更新/解除安裝-新的 UI 現在提供一種方式預覽變更，將對您的專案。</span><span class="sxs-lookup"><span data-stu-id="f861e-147">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="f861e-148">此預覽會顯示任何新的套件，將安裝套件，將會更新，並將它封裝，將會解除安裝，以及將會在作業期間維持不變的封裝。</span><span class="sxs-lookup"><span data-stu-id="f861e-148">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="f861e-149">在下列範例中，我們可以看到，安裝 Microsoft.AspNet.SignalR 會導致相當多的變更至專案。</span><span class="sxs-lookup"><span data-stu-id="f861e-149">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![安裝 SignalR 的預覽](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="f861e-151">安裝選項</span><span class="sxs-lookup"><span data-stu-id="f861e-151">Installation Options</span></span>

<span data-ttu-id="f861e-152">使用 PowerShell 主控台中，您有幾個值得注意的安裝選項的控制權。</span><span class="sxs-lookup"><span data-stu-id="f861e-152">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="f861e-153">我們現在已經納入 UI 也加入這些功能。</span><span class="sxs-lookup"><span data-stu-id="f861e-153">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="f861e-154">您現在可以控制如何選取版本的相依性的相依性解析行為。</span><span class="sxs-lookup"><span data-stu-id="f861e-154">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![相依性的行為](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="f861e-156">您也可以指定要從封裝的內容檔案發生衝突的檔案已在您的專案時所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="f861e-156">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![Akce při Konfliktu Souborů](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="f861e-158">無限捲動</span><span class="sxs-lookup"><span data-stu-id="f861e-158">Infinite Scrolling</span></span>

<span data-ttu-id="f861e-159">我們用來取得相當的意見反應，我們的 ui 讓這兩個捲動和列出封裝時，分頁典範。</span><span class="sxs-lookup"><span data-stu-id="f861e-159">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="f861e-160">它是很常見的捲動到底部的簡短清單，按一下 [下一步] 的頁面數目，然後再次捲動。</span><span class="sxs-lookup"><span data-stu-id="f861e-160">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="f861e-161">有新的 UI 中，我們已實作無限捲動套件清單中，您只需要捲動，沒有更多的分頁。</span><span class="sxs-lookup"><span data-stu-id="f861e-161">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![無限捲動](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="f861e-163">使其工作、 快速，讓它很</span><span class="sxs-lookup"><span data-stu-id="f861e-163">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="f861e-164">我們很興奮地一定要記得這個新的 UI 讓您試用。在此預覽的里程碑，我們已經遵循的良好的古訓 「 保持運作、 進行快速、 加強美化。 」</span><span class="sxs-lookup"><span data-stu-id="f861e-164">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="f861e-165">在此預覽中，我們已經完成大部分的第一個目標，它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f861e-165">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="f861e-166">我們知道它尚未相當快速，我們知道它尚未相當相當。</span><span class="sxs-lookup"><span data-stu-id="f861e-166">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="f861e-167">我們將努力於這些目標現在與 RC 版本之間的信任。</span><span class="sxs-lookup"><span data-stu-id="f861e-167">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="f861e-168">在此同時，我們很希望聽聽您的意見反應的相關*可用性*的新 UI--工作流程、 作業，以及它*感覺*若要使用新的 UI。</span><span class="sxs-lookup"><span data-stu-id="f861e-168">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="f861e-169">有幾個相較於舊版的 UI，我們已移除的函式。</span><span class="sxs-lookup"><span data-stu-id="f861e-169">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="f861e-170">其中一種是特意的與另一個只是未完成的時間。</span><span class="sxs-lookup"><span data-stu-id="f861e-170">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="f861e-171">搜尋 「 全部 」 的套件來源</span><span class="sxs-lookup"><span data-stu-id="f861e-171">Searching "All" Package Sources</span></span>

<span data-ttu-id="f861e-172">舊版 UI 可讓您執行封裝的搜尋，針對所有套件來源。</span><span class="sxs-lookup"><span data-stu-id="f861e-172">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="f861e-173">我們已移除該功能在 UI 中，我們將不會被帶回來。</span><span class="sxs-lookup"><span data-stu-id="f861e-173">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="f861e-174">用來執行搜尋作業，針對所有套件來源，這項功能會組織在一起，結果，並嘗試排列取決於您選擇的排序結果。</span><span class="sxs-lookup"><span data-stu-id="f861e-174">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="f861e-175">我們發現搜尋相關性是很難組織在一起。</span><span class="sxs-lookup"><span data-stu-id="f861e-175">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="f861e-176">您可以想像執行對 Google、 Bing 搜尋，並一起編排結果嗎？</span><span class="sxs-lookup"><span data-stu-id="f861e-176">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="f861e-177">此外，這項功能已變慢、 容易*意外*以及我們認為很少是真的很實用。</span><span class="sxs-lookup"><span data-stu-id="f861e-177">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="f861e-178">因為發生問題的功能導入，我們收到數目可能永遠不會有已修正的 bug 報告在其上。</span><span class="sxs-lookup"><span data-stu-id="f861e-178">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="f861e-179">全部更新</span><span class="sxs-lookup"><span data-stu-id="f861e-179">Update All</span></span>

<span data-ttu-id="f861e-180">我們用來在尚未有新的 UI 中將舊版 UI 的 [全部更新] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f861e-180">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="f861e-181">我們將會重新啟動這項功能，我們的 RC 版本。</span><span class="sxs-lookup"><span data-stu-id="f861e-181">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="f861e-182">新用戶端/伺服器 API</span><span class="sxs-lookup"><span data-stu-id="f861e-182">New Client/Server API</span></span>

<span data-ttu-id="f861e-183">除了我們新的套件管理 UI 中的新功能，我們也一直在處理某些 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f861e-183">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="f861e-184">我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="f861e-184">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="f861e-185">新的 API 以 REST 為基礎，並已選取超媒體和我們[JSON-LD](http://json-ld.org)為我們資源的格式。</span><span class="sxs-lookup"><span data-stu-id="f861e-185">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="f861e-186">在 NuGet 3.0 Preview 位元為單位，您會看到新的封裝來源的封裝來源下拉式清單中稱為 「 preview.nuget.org"。</span><span class="sxs-lookup"><span data-stu-id="f861e-186">In the NuGet 3.0 Preview bits, you see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="f861e-187">如果您選取該套件來源，我們將使用我們的新 API，而是要連接到 nuget.org。我們已進行預覽來源可在 UI 中，同時會持續測試、 修訂和提高新的 API。</span><span class="sxs-lookup"><span data-stu-id="f861e-187">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="f861e-188">在 NuGet 3.0 RC 中，這個新的 API v3 套件來源將會取代 v2 為基礎的"nuget.org"套件來源。</span><span class="sxs-lookup"><span data-stu-id="f861e-188">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="f861e-189">儘管我們正在將放入 API v3 的投資，我們已進行所有這些新功能也適用於我們現有 API v2 通訊協定，這表示它們會使用現有的套件來源，以及 nuget.org 以外。</span><span class="sxs-lookup"><span data-stu-id="f861e-189">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="f861e-190">即將推出的新功能</span><span class="sxs-lookup"><span data-stu-id="f861e-190">New Features Coming</span></span>

<span data-ttu-id="f861e-191">現在開始到 3.0 的 RTM，我們也正在一些基本以外的新 NuGet 功能，在 UI 中看到的內容。</span><span class="sxs-lookup"><span data-stu-id="f861e-191">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you see in the UI.</span></span> <span data-ttu-id="f861e-192">以下是一份主要投資領域：</span><span class="sxs-lookup"><span data-stu-id="f861e-192">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="f861e-193">我們合作，使用 Visual Studio 和 MSBuild 小組以取得[平台更深層的 NuGet](http://blog.nuget.org/20141014/in-the-platform.html)。</span><span class="sxs-lookup"><span data-stu-id="f861e-193">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="f861e-194">我們正在放棄安裝階段套件慣例，並改為在藉由引進新的封裝時套用這些慣例 「 授權 」[封裝資訊清單](http://blog.nuget.org/20141023/package-manifests.html)。</span><span class="sxs-lookup"><span data-stu-id="f861e-194">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="f861e-195">我們正在努力的重構 NuGet 程式碼基底進行 Visual Studio 中的套件管理之外的不同網域中的可重複使用的用戶端和伺服器元件。</span><span class="sxs-lookup"><span data-stu-id="f861e-195">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="f861e-196">我們正積極研究概念的 「 私用相依性 」，封裝可能表示它具有相依於其他封裝的實作詳細資料，以及這些相依性不應該顯示為最上層相依性。</span><span class="sxs-lookup"><span data-stu-id="f861e-196">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="f861e-197">敬請期待</span><span class="sxs-lookup"><span data-stu-id="f861e-197">Stay Tuned</span></span>

<span data-ttu-id="f861e-198">請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和 NuGet 3.0 公告 ！</span><span class="sxs-lookup"><span data-stu-id="f861e-198">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>