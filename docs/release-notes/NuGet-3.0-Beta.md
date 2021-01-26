---
title: NuGet 3.0 Beta 版注意事項
description: NuGet 3.0 搶鮮版（Beta）的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776623"
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="f1c2a-103">NuGet 3.0 Beta 版注意事項</span><span class="sxs-lookup"><span data-stu-id="f1c2a-103">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="f1c2a-104">[NuGet 3.0 Preview 版本](../release-notes/nuget-3.0-preview.md)  |  資訊[NuGet 3.0 RC 版本](../release-notes/nuget-3.0-rc.md)資訊</span><span class="sxs-lookup"><span data-stu-id="f1c2a-104">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="f1c2a-105">NuGet 3.0 Beta 發行于2015年2月23日，適用于 Visual Studio 2015 CTP 6 版。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-105">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="f1c2a-106">這一版對我們的團隊來說很多，因為我們有許多可共用的架構和效能改進，而我們很高興能開始調整 nuget.org 服務的效能設定。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-106">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="f1c2a-107">強烈建議您先卸載任何舊版的 NuGet Visual Studio 2015 延伸模組，再安裝這個新版本。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-107">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="f1c2a-108">如果您在此版本的延伸模組中遇到任何問題，建議您還原為 [先前的版本](http://nuget.codeplex.com/downloads/get/909582) ，以搭配 Visual Studio 2015 preview 使用。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-108">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="f1c2a-109">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="f1c2a-109">Visual Studio 2012+</span></span>

<span data-ttu-id="f1c2a-110">此 NuGet 3.0 Beta 版可在 Visual Studio 2015 CTP 6 擴充功能資源庫中進行安裝。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-110">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="f1c2a-111">我們即將致力於取得 Visual Studio 2012 的預覽，並 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="f1c2a-112">我們先前已分享我們的意圖，以 [停止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，而我們的確進行了這種困難的決策。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="f1c2a-113">新用戶端/伺服器 API</span><span class="sxs-lookup"><span data-stu-id="f1c2a-113">New Client/Server API</span></span>

<span data-ttu-id="f1c2a-114">我們已處理 NuGet 用戶端/伺服器通訊協定的一些執行詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-114">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="f1c2a-115">我們所做的工作是建立 NuGet 的「API v3」，這是針對重大案例（例如套件還原和安裝封裝）的高可用性而設計的。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-115">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="f1c2a-116">新的 API 是以 REST 和超媒體為基礎，而且我們選取了 [JSON-LD](http://json-ld.org) 作為資源格式。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-116">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="f1c2a-117">在 NuGet 3.0 搶鮮版（Beta）中，您會在 [套件來源] 下拉式清單中看到名為 "api.nuget.org" 的新套件來源。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-117">In the NuGet 3.0 Beta bits, you see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="f1c2a-118">如果您選取該套件來源，我們將使用新的 API，而不是連接到 nuget.org。在 NuGet 3.0 RC 中，這個新的 API v3 套件來源會取代 v2 型的 "nuget.org" 套件來源。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-118">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="f1c2a-119">建議您停用所有其他公用套件來源，並只將 api.nuget.org 保留為您唯一的公用套件存放庫。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-119">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="f1c2a-120">我們花了很多時間來建立 v3 API，並會繼續為舊版用戶端維護標準 v2 API，以存取公用存放庫。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-120">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="f1c2a-121">更新的 UI</span><span class="sxs-lookup"><span data-stu-id="f1c2a-121">Updated UI</span></span>

<span data-ttu-id="f1c2a-122">我們已增強此版本中的使用者介面，以包含一個下拉式方塊，可讓您選擇要對封裝執行的動作，並將 [預覽] 按鈕轉換成螢幕上 [選項] 區域中的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-122">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="f1c2a-123">[選項] 區域不再是可折迭的，現在會提供說明連結來描述可用的選項。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-123">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="f1c2a-125">作業記錄</span><span class="sxs-lookup"><span data-stu-id="f1c2a-125">Operation Logging</span></span>

<span data-ttu-id="f1c2a-126">我們已移除具有記錄資訊的強制回應視窗，這些資訊會在安裝或卸載時快速顯示及隱藏。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-126">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="f1c2a-127">當您真正想要查看資訊或從中複製和貼上時，此視窗不會加入任何值。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-127">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="f1c2a-128">相反地，我們現在會將所有輸出記錄重新導向至 [輸出] 視窗的封裝管理員窗格。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-128">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="f1c2a-129">我們認為這比較熟悉，而且類似于您想要檢查的一般組建報告。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-129">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="f1c2a-130">專注于效能</span><span class="sxs-lookup"><span data-stu-id="f1c2a-130">Focus on Performance</span></span>

<span data-ttu-id="f1c2a-131">我們對改善 NuGet 搜尋和提取的效能進行了許多變更。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-131">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="f1c2a-132">這是我們的客戶所關注的，我們想要確定我們已在此版本中解決這種問題。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-132">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="f1c2a-133">我們已調整伺服器、建立新的 CDN，並改進了查詢符合邏輯，以提供更相關且更快速的封裝搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-133">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="f1c2a-134">隨著我們在開發 NuGet 3.0 的這個階段進行，我們將會調整並監視 nuget.org 服務，以確保我們能提供更佳的體驗。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-134">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="f1c2a-135">我們不打算參與任何停機時間，但會在服務中新增和變更資源。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-135">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="f1c2a-136">請留意我們的 [twitter](http://twitter.com/nuget) 摘要，以取得何時變更服務設定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-136">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="f1c2a-137">使用 NuGet 建立 NuGet</span><span class="sxs-lookup"><span data-stu-id="f1c2a-137">Building NuGet with NuGet</span></span>

<span data-ttu-id="f1c2a-138">我們現在已將 NuGet 用戶端重新架構至多個元件，而這些元件本身內建于 NuGet 套件中。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-138">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="f1c2a-139">這種重複使用的程式庫會強制我們建立可重複使用且可正確封裝的元件。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-139">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="f1c2a-140">我們可以消除重複的程式碼，並瞭解如何以更好的方式設定開發流程，以支援在整個解決方案中建立套件的需求。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-140">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="f1c2a-141">請在稍後探討程式碼專案的結構化方式，以及我們的組建程式如何運作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f1c2a-141">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="f1c2a-142">持續關注</span><span class="sxs-lookup"><span data-stu-id="f1c2a-142">Stay Tuned</span></span>

<span data-ttu-id="f1c2a-143">請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多 NuGet 3.0 的進度和公告！</span><span class="sxs-lookup"><span data-stu-id="f1c2a-143">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>
