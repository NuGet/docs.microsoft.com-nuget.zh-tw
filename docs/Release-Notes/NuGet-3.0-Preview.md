---
title: "NuGet 3.0 Preview 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.0 預覽的版本資訊。"
keywords: "NuGet 3.0 預覽的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e07bcad2bf713deee0add72663c84b9979f8c5c4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="a2cc7-104">NuGet 3.0 的預覽版本資訊</span><span class="sxs-lookup"><span data-stu-id="a2cc7-104">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="a2cc7-105">[NuGet 2.9 RC 版本資訊](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta 版本資訊](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="a2cc7-105">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="a2cc7-106">NuGet 3.0 預覽版本已發行於 2014 年 11 月 12 日在 Visual Studio 2015 Preview 版本。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-106">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="a2cc7-107">我們發行了 NuGet 3.0 預覽。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-107">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="a2cc7-108">這是我們大發行 （雖然預覽中），以及我們很高興能夠開始取得意見反應，我們變更。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-108">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="a2cc7-109">Visual Studio 2012+</span><span class="sxs-lookup"><span data-stu-id="a2cc7-109">Visual Studio 2012+</span></span>

<span data-ttu-id="a2cc7-110">此 NuGet 3.0 預覽隨附於 Visual Studio 2015 Preview。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-110">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="a2cc7-111">我們正努力預覽卸除的 Visual Studio 2012 和 Visual Studio 2013 很快。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="a2cc7-112">我們先前共用我們意圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，我們沒有做出的決策，困難。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="a2cc7-113">全新的 UI</span><span class="sxs-lookup"><span data-stu-id="a2cc7-113">Brand New UI</span></span>

<span data-ttu-id="a2cc7-114">您會發現有關 NuGet 3.0 預覽第一件事是我們新的 UI。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-114">The first thing you'll notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="a2cc7-115">它不再是強制回應對話方塊。它現在是完整的 Visual Studio 文件視窗。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-115">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="a2cc7-116">這可讓您在一次開啟多個專案 （和/或方案） 的使用者介面、 分離出來視窗至另一個監視器、 將它停駐，不過就像 like 等等。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-116">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="a2cc7-118">超過使用性的差異，因為放棄強制回應對話方塊，我們也有許多新功能的新 UI 中。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-118">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="a2cc7-119">版本選取項目</span><span class="sxs-lookup"><span data-stu-id="a2cc7-119">Version Selection</span></span>

<span data-ttu-id="a2cc7-120">最可能要求 UI 功能可讓版本選取項目套件安裝和更新-這是立即可用。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-120">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![套件版本選取項目](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="a2cc7-122">是否要安裝或更新的封裝，[版本] 下拉式清單可讓您查看所有可用的封裝，版本具有某些值得注意的版本升級為簡單的選取清單的頂端。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-122">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="a2cc7-123">您不再需要使用來取得特定版本，不是最新的 PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-123">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="a2cc7-124">結合安裝/線上/更新工作流程</span><span class="sxs-lookup"><span data-stu-id="a2cc7-124">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="a2cc7-125">我們先前 UI 必須上線，已安裝和更新的 3 個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-125">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="a2cc7-126">封裝列出特定的工作流程，而且可用的動作所特有的工作流程。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-126">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="a2cc7-127">雖然看似邏輯，我們聽到許多您通常會取得這項分隔的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-127">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="a2cc7-128">我們現在有合併的體驗，您可以在其中安裝、 更新或解除安裝封裝，不論您如何到達所選取的封裝。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-128">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="a2cc7-129">為了協助的特定工作流程，我們現在有篩選下拉式清單中，可讓您篩選封裝可見的但然後封裝可用動作一致。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-129">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![解除安裝封裝](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="a2cc7-131">藉由使用 「 安裝 」 篩選器，您可以輕鬆地看見有何者有可用的更新，您已安裝的封裝，並接著您可以解除安裝，或藉由變更版本選取項目，以查看更新的封裝變更可用的動作。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-131">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![更新的套件](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="a2cc7-133">版本彙總</span><span class="sxs-lookup"><span data-stu-id="a2cc7-133">Version Consolidation</span></span>

<span data-ttu-id="a2cc7-134">通常會有相同的封裝安裝到您的方案中的多個專案。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-134">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="a2cc7-135">有時候安裝到每個專案的版本可以分開漂移，則需要彙總中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-135">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="a2cc7-136">NuGet 3.0 Preview 引進的新功能，只要在此案例。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-136">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="a2cc7-137">方案層級封裝的 管理 視窗可以存取方案上按一下滑鼠右鍵，然後選擇 管理方案的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-137">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="a2cc7-138">從該處，如果您選取的封裝安裝到多個專案，但具有不同的版本，在使用中，新的 「 合併 」 動作會變成可用。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-138">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="a2cc7-139">在下列螢幕擷取畫面，`Newtonsoft.Json`安裝`SamplesClassLibrary`版本`6.0.4`且已安裝到`SamplesConsoleApp`版本`5.0.4`。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-139">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![合併版本](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="a2cc7-141">以下是將合併到單一版本的工作流程。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-141">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="a2cc7-142">選取`Newtonsoft.Json`清單中的封裝</span><span class="sxs-lookup"><span data-stu-id="a2cc7-142">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="a2cc7-143">選擇`Consolidate`從`Action`下拉式清單</span><span class="sxs-lookup"><span data-stu-id="a2cc7-143">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="a2cc7-144">使用`Version`下拉式清單來選取要合併到的版本</span><span class="sxs-lookup"><span data-stu-id="a2cc7-144">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="a2cc7-145">核取方塊，應合併到該版本 （請注意，已在選取的版本上的專案會呈現灰色） 的專案</span><span class="sxs-lookup"><span data-stu-id="a2cc7-145">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="a2cc7-146">按一下`Consolidate`按鈕來執行彙總</span><span class="sxs-lookup"><span data-stu-id="a2cc7-146">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="a2cc7-147">作業預覽</span><span class="sxs-lookup"><span data-stu-id="a2cc7-147">Operation Previews</span></span>

<span data-ttu-id="a2cc7-148">不論哪一項作業在執行-安裝/更新/解除安裝-新的使用者介面現在提供一種方式預覽變更，將對您的專案。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-148">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="a2cc7-149">這個預覽會顯示新的封裝將安裝的封裝將會更新，並將封裝將會解除安裝，以及將會在作業期間維持不變的封裝。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-149">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="a2cc7-150">在下列範例中，我們可以看到，安裝 Microsoft.AspNet.SignalR 時會產生極多的變更至專案。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-150">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![安裝 SignalR 的預覽](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="a2cc7-152">安裝選項</span><span class="sxs-lookup"><span data-stu-id="a2cc7-152">Installation Options</span></span>

<span data-ttu-id="a2cc7-153">使用 PowerShell 主控台，您有幾個值得注意的安裝選項的控制權。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-153">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="a2cc7-154">現在我們已將這些功能帶入 UI。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-154">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="a2cc7-155">您現在可以控制如何選取版本的相依性的相依性解析行為。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-155">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![相依性的行為](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="a2cc7-157">您也可以指定要從套件內容檔案衝突的檔案已在您的專案時所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-157">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![檔案 [衝突] 動作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="a2cc7-159">無限捲動</span><span class="sxs-lookup"><span data-stu-id="a2cc7-159">Infinite Scrolling</span></span>

<span data-ttu-id="a2cc7-160">我們用來取得稍微的意見反應，我們的 ui 讓這兩個捲動及列出封裝時，分頁開發架構。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-160">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="a2cc7-161">它是非常普遍能夠捲動的簡短清單底部，按一下 下一步的頁面數字，然後再一次捲動。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-161">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="a2cc7-162">使用新的 UI 中，我們已實作無限捲動封裝清單中，因此您只需要捲動-沒有更多的分頁。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-162">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![無限捲動](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="a2cc7-164">讓工作，使其快速，使其美觀</span><span class="sxs-lookup"><span data-stu-id="a2cc7-164">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="a2cc7-165">我們很高興能夠讓您試用努力這個新的 UI。在此預覽里程碑，我們都遵循的良好俗話說 「 保持運作、 進行快速、 加強美化。 」</span><span class="sxs-lookup"><span data-stu-id="a2cc7-165">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="a2cc7-166">在此預覽中，我們已經完成大部分的該第一個目標-它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-166">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="a2cc7-167">我們知道它尚未相當快速，我們已經知道它尚未相當相當。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-167">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="a2cc7-168">我們會努力這些目標的 RC 版本之間的信任。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-168">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="a2cc7-169">在此同時，我們很希望聽聽您的意見反應的相關*可用性*的新 ui-工作流程、 作業，以及它*感覺*若要使用新的 UI。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-169">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="a2cc7-170">有幾個函式，我們便移除了相較於舊的 UI。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-170">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="a2cc7-171">下列其中一種有意，和另一個只未完成的時間。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-171">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="a2cc7-172">搜尋 「 全部 」 封裝來源</span><span class="sxs-lookup"><span data-stu-id="a2cc7-172">Searching "All" Package Sources</span></span>

<span data-ttu-id="a2cc7-173">舊的 UI 可讓您執行封裝，針對您的封裝來源的所有搜尋。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-173">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="a2cc7-174">我們已移除該功能，在 UI 中，我們將不會使其傳回。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-174">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="a2cc7-175">這項功能，用來執行搜尋作業，針對您的封裝來源的所有組織在一起，，結果，並嘗試根據您排序選取結果。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-175">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="a2cc7-176">我們發現搜尋相關性是很難組織在一起。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-176">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="a2cc7-177">您可以想像執行針對 Google 和 Bing 搜尋，並一起 weaving 結果嗎？</span><span class="sxs-lookup"><span data-stu-id="a2cc7-177">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="a2cc7-178">此外，這項功能已慢速又容易*意外*以及我們認為很少是實際的有用。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-178">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="a2cc7-179">因為發生問題的功能導入，我們收到無法從未已獲得修正的 bug 報告在其上的數的字。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-179">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="a2cc7-180">更新所有</span><span class="sxs-lookup"><span data-stu-id="a2cc7-180">Update All</span></span>

<span data-ttu-id="a2cc7-181">我們使用舊尚有無法在新的 UI 中的 UI 中有 [更新全部] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-181">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="a2cc7-182">我們會重新啟動這項功能，我們的 RC 版本。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-182">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="a2cc7-183">新用戶端/伺服器應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="a2cc7-183">New Client/Server API</span></span>

<span data-ttu-id="a2cc7-184">除了所有我們新的封裝管理 UI 中的新功能，我們已也已在處理某些 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-184">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="a2cc7-185">我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-185">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="a2cc7-186">新的應用程式開發介面以 REST 為基礎和超，我們已選取[JSON LD](http://json-ld.org)為我們的資源格式。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-186">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="a2cc7-187">在 NuGet 3.0 預覽位元為單位，您會看到稱為"preview.nuget.org"的套件來源下拉式清單中的新封裝來源。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-187">In the NuGet 3.0 Preview bits, you'll see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="a2cc7-188">如果您選取的套件來源，我們將使用新 API，而是要連接到 nuget.org。我們已可供預覽來源在 UI 中我們繼續測試、 修訂和改善的新 API。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-188">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="a2cc7-189">在 NuGet 3.0 RC 中，這個新的 API v3 為基礎的套件來源將會取代 v2 為基礎的 」 nuget.org"的套件來源。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-189">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="a2cc7-190">儘管我們正在將放入 API v3 的投資，我們已經讓我們現有 API v2 通訊協定，這表示將使用現有的封裝來源，以及 nuget.org 以外也使用所有這些新功能。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-190">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="a2cc7-191">推出的新功能</span><span class="sxs-lookup"><span data-stu-id="a2cc7-191">New Features Coming</span></span>

<span data-ttu-id="a2cc7-192">之間 3.0 RTM，我們也正在一些基本 NuGet 以外新功能，您會看到在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-192">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you'll see in the UI.</span></span> <span data-ttu-id="a2cc7-193">以下是主要的投資領域的簡短清單：</span><span class="sxs-lookup"><span data-stu-id="a2cc7-193">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="a2cc7-194">我們正在合作與 Visual Studio 和 MSBuild 小組以取得[更深入的平台的 NuGet](http://blog.nuget.org/20141014/in-the-platform.html)。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-194">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="a2cc7-195">我們正努力放棄安裝階段封裝慣例，並改為在封裝階段套用這些慣例，藉由引進新的 「 系統授權 」[封裝資訊清單](http://blog.nuget.org/20141023/package-manifests.html)。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-195">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="a2cc7-196">我們正努力的重構 NuGet 程式碼在 Visual Studio 中的封裝管理以外的不同網域中進行用戶端和伺服器元件可重複使用基底。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-196">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="a2cc7-197">我們正在調查概念的 「 私用相依性 」 封裝可以在其中表示它具有的實作詳細資料，其他套件相依性和這些相依性不應該顯示為最上層的相依性。</span><span class="sxs-lookup"><span data-stu-id="a2cc7-197">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="a2cc7-198">敬請期待</span><span class="sxs-lookup"><span data-stu-id="a2cc7-198">Stay Tuned</span></span>

<span data-ttu-id="a2cc7-199">請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及針對 NuGet 3.0 公告 ！</span><span class="sxs-lookup"><span data-stu-id="a2cc7-199">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>