---
title: NuGet 3.0 Beta 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.0 Beta 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550909"
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="9928d-103">NuGet 3.0 Beta 版本資訊</span><span class="sxs-lookup"><span data-stu-id="9928d-103">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="9928d-104">[NuGet 3.0 Preview 版本資訊](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 版本資訊](../release-notes/nuget-3.0-rc.md)</span><span class="sxs-lookup"><span data-stu-id="9928d-104">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="9928d-105">NuGet 3.0 beta 版於 2015 年 2 月 23 日發行 Visual Studio 2015 CTP 6 版本。</span><span class="sxs-lookup"><span data-stu-id="9928d-105">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="9928d-106">此版本給我們的團隊，表示很多，因為我們有一些架構和效能增強功能，若要共用，而且我們很高興能夠開始微調我們 nuget.org 的服務上的效能設定。</span><span class="sxs-lookup"><span data-stu-id="9928d-106">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="9928d-107">我們強烈建議您先解除安裝任何舊版的 NuGet Visual Studio 2015 延伸模組，再安裝此新版本。</span><span class="sxs-lookup"><span data-stu-id="9928d-107">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="9928d-108">如果您有與此版本的延伸模組的任何問題，我們建議您還原[舊版](http://nuget.codeplex.com/downloads/get/909582)搭配 Visual Studio 2015 preview。</span><span class="sxs-lookup"><span data-stu-id="9928d-108">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="9928d-109">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="9928d-109">Visual Studio 2012+</span></span>

<span data-ttu-id="9928d-110">若要安裝 Visual Studio 2015 CTP 6 延伸模組組件庫中使用此 NuGet 3.0 beta 版。</span><span class="sxs-lookup"><span data-stu-id="9928d-110">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="9928d-111">我們正努力取得預覽卸除 Visual Studio 2012 和 Visual Studio 2013 推出。</span><span class="sxs-lookup"><span data-stu-id="9928d-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="9928d-112">我們之前告訴大家我們試圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，但未將該相當困難的決定。</span><span class="sxs-lookup"><span data-stu-id="9928d-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="9928d-113">新用戶端/伺服器 API</span><span class="sxs-lookup"><span data-stu-id="9928d-113">New Client/Server API</span></span>

<span data-ttu-id="9928d-114">我們一直在處理某些 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9928d-114">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="9928d-115">我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="9928d-115">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="9928d-116">新的 API 以 REST 為基礎，並已選取超媒體和我們[JSON-LD](http://json-ld.org)為我們資源的格式。</span><span class="sxs-lookup"><span data-stu-id="9928d-116">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="9928d-117">在 NuGet 3.0 Beta 位元為單位，您會看到新的封裝來源的封裝來源下拉式清單中稱為 「 api.nuget.org"。</span><span class="sxs-lookup"><span data-stu-id="9928d-117">In the NuGet 3.0 Beta bits, you see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="9928d-118">如果您選取該套件來源，我們將使用我們的新 API，而是要連接到 nuget.org。在 NuGet 3.0 RC 中，這個新的 API v3 套件來源將會取代 v2 為基礎的"nuget.org"套件來源。</span><span class="sxs-lookup"><span data-stu-id="9928d-118">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="9928d-119">我們建議您停用的所有其他公用套件來源，並將僅 api.nuget.org 保留為僅針對公用套件存放庫。</span><span class="sxs-lookup"><span data-stu-id="9928d-119">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="9928d-120">我們已經放了很多時間建置我們的 v3 API，並將繼續維護舊的用戶端想要存取的公用存放庫的標準 v2 API。</span><span class="sxs-lookup"><span data-stu-id="9928d-120">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="9928d-121">更新的 UI</span><span class="sxs-lookup"><span data-stu-id="9928d-121">Updated UI</span></span>

<span data-ttu-id="9928d-122">我們已增強這一版包含可讓您選擇要與封裝執行的動作，而轉換至螢幕的 [選項] 區域中的核取方塊的 [預覽] 按鈕的下拉式方塊中的使用者介面。</span><span class="sxs-lookup"><span data-stu-id="9928d-122">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="9928d-123">[選項] 區域不再可摺疊，而且現在會提供說明可用選項的 [說明] 連結。</span><span class="sxs-lookup"><span data-stu-id="9928d-123">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="9928d-125">作業記錄</span><span class="sxs-lookup"><span data-stu-id="9928d-125">Operation Logging</span></span>

<span data-ttu-id="9928d-126">我們已移除強制回應視窗會快速顯示及隱藏在安裝或解除安裝時的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="9928d-126">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="9928d-127">您真正想看到的資訊，或是能夠複製並貼上從它時，此視窗會新增任何值。</span><span class="sxs-lookup"><span data-stu-id="9928d-127">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="9928d-128">相反地，我們會立即重新導向所有輸出記錄到輸出 視窗的 套件管理員 窗格。</span><span class="sxs-lookup"><span data-stu-id="9928d-128">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="9928d-129">我們認為這是更自在，類似於標準的建置報表，您會想要檢查。</span><span class="sxs-lookup"><span data-stu-id="9928d-129">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="9928d-130">著重在效能</span><span class="sxs-lookup"><span data-stu-id="9928d-130">Focus on Performance</span></span>

<span data-ttu-id="9928d-131">我們加入了許多變更，改善效能，NuGet 搜尋，以及提取的名稱。</span><span class="sxs-lookup"><span data-stu-id="9928d-131">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="9928d-132">這是從我們的客戶，我們首要考量，我們想要確定我們在此版本中已解決。</span><span class="sxs-lookup"><span data-stu-id="9928d-132">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="9928d-133">我們已調整我們的伺服器，建立新的 CDN 和更佳的查詢比對希望傳遞給您更多相關的邏輯，並更快的套件搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="9928d-133">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="9928d-134">當我們繼續透過 NuGet 3.0 開發的這個階段，我們將會調整並監視 [nuget.org] 服務，以確保我們提供較佳的體驗。</span><span class="sxs-lookup"><span data-stu-id="9928d-134">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="9928d-135">我們執行未計劃參與任何停機時間，但會新增及變更在服務中的資源。</span><span class="sxs-lookup"><span data-stu-id="9928d-135">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="9928d-136">敬請期待我們[twitter 摘要](http://twitter.com/nuget)如當我們變更服務組態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9928d-136">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="9928d-137">使用 NuGet 建置 NuGet</span><span class="sxs-lookup"><span data-stu-id="9928d-137">Building NuGet with NuGet</span></span>

<span data-ttu-id="9928d-138">我們現在有重新我們 NuGet 用戶端架構本身內建 NuGet 套件的數個元件。</span><span class="sxs-lookup"><span data-stu-id="9928d-138">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="9928d-139">此重複使用我們自己的程式庫會強制我們建立可重複使用，而且，可以正確地將它封裝的元件。</span><span class="sxs-lookup"><span data-stu-id="9928d-139">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="9928d-140">我們已能夠消除重複的程式碼，並已了解如何進一步設定我們的開發程序，以支援需要建置整個解決方案的封裝。</span><span class="sxs-lookup"><span data-stu-id="9928d-140">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="9928d-141">尋找推出的部落格文章，我們會討論程式碼專案的結構方式，以及我們的建置程序的運作方式。</span><span class="sxs-lookup"><span data-stu-id="9928d-141">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="9928d-142">敬請期待</span><span class="sxs-lookup"><span data-stu-id="9928d-142">Stay Tuned</span></span>

<span data-ttu-id="9928d-143">請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和 NuGet 3.0 公告 ！</span><span class="sxs-lookup"><span data-stu-id="9928d-143">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>
