---
title: "NuGet 3.0 Beta 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.0 Beta。"
keywords: "NuGet 3.0 Beta 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3a595d002e385ff0330c2eebd0e8439f5dbefbd9
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="a9ff1-104">NuGet 3.0 Beta 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a9ff1-104">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="a9ff1-105">[NuGet 3.0 Preview 版本資訊](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 版本資訊](../release-notes/nuget-3.0-rc.md)</span><span class="sxs-lookup"><span data-stu-id="a9ff1-105">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="a9ff1-106">NuGet 3.0 Beta 已於 2015 年 2 月 23 日發行 Visual Studio 2015 CTP 6 版本。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-106">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="a9ff1-107">此版本代表許多我們的團隊，我們有多個架構和效能改進的共用，以及我們很高興能夠開始微調我們 nuget.org 的服務上的效能設定。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-107">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="a9ff1-108">我們強烈建議您先解除安裝任何舊版的 NuGet Visual Studio 2015 延伸模組，再安裝此新的版本。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-108">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="a9ff1-109">如果您有與此版本的擴充功能的任何問題，我們建議您還原為[舊版](http://nuget.codeplex.com/downloads/get/909582)搭配 Visual Studio 2015 預覽。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-109">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="a9ff1-110">Visual Studio 2012+</span><span class="sxs-lookup"><span data-stu-id="a9ff1-110">Visual Studio 2012+</span></span>

<span data-ttu-id="a9ff1-111">若要安裝 Visual Studio 2015 CTP 6 延伸模組組件庫中使用此 NuGet 3.0 Beta。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-111">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="a9ff1-112">我們正努力預覽卸除的 Visual Studio 2012 和 Visual Studio 2013 很快。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-112">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="a9ff1-113">我們先前共用我們意圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，我們沒有做出的決策，困難。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-113">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="a9ff1-114">新用戶端/伺服器應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="a9ff1-114">New Client/Server API</span></span>

<span data-ttu-id="a9ff1-115">我們已尚未處理部分 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-115">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="a9ff1-116">我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-116">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="a9ff1-117">新的應用程式開發介面以 REST 為基礎和超，我們已選取[JSON LD](http://json-ld.org)為我們的資源格式。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-117">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="a9ff1-118">在 NuGet 3.0 Beta 位元為單位，您會看到稱為"api.nuget.org"的套件來源下拉式清單中的新封裝來源。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-118">In the NuGet 3.0 Beta bits, you see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="a9ff1-119">如果您選取的套件來源，我們將使用新 API，而是要連接到 nuget.org。在 NuGet 3.0 RC 中，這個新的 API v3 為基礎的套件來源將會取代 v2 為基礎的 」 nuget.org"的套件來源。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-119">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="a9ff1-120">我們建議您停用所有的其他公用封裝來源，將只 api.nuget.org 保留為您的封裝只公用儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-120">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="a9ff1-121">我們已放入建置 v3 API 的許多時間，而且將會繼續維護舊的用戶端來存取公用儲存機制尋找標準 v2 API。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-121">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="a9ff1-122">更新的 UI</span><span class="sxs-lookup"><span data-stu-id="a9ff1-122">Updated UI</span></span>

<span data-ttu-id="a9ff1-123">我們已增強使用者介面在本版中要包含下拉式方塊，可讓您選擇要與封裝所採取的動作，並轉換至螢幕的 [選項] 區域中的核取方塊的 [預覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-123">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="a9ff1-124">[選項] 區域不再可摺疊，而且現在會提供說明可用選項的說明連結。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-124">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="a9ff1-126">作業記錄</span><span class="sxs-lookup"><span data-stu-id="a9ff1-126">Operation Logging</span></span>

<span data-ttu-id="a9ff1-127">我們會移除強制回應視窗會快速顯示和隱藏安裝或解除安裝時的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-127">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="a9ff1-128">您真的想要看到的資訊，或是能夠複製並貼上它，此視窗會加入任何值。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-128">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="a9ff1-129">相反地，我們現在將重新導向所有輸出記錄到輸出 視窗的 封裝管理員 窗格。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-129">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="a9ff1-130">我們認為這是更舒適且類似於標準的建置報表，您會想要檢查。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-130">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="a9ff1-131">專注於效能</span><span class="sxs-lookup"><span data-stu-id="a9ff1-131">Focus on Performance</span></span>

<span data-ttu-id="a9ff1-132">我們進行許多變更，改善效能的 NuGet 搜尋及擷取的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-132">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="a9ff1-133">這是從我們的客戶，我們數字一項考量，我們想確定我們在此版本中解決它。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-133">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="a9ff1-134">我們已微調我們的伺服器，建立新的 CDN，並改善比對邏輯希望傳遞給您更有相關性的查詢，更快速的封裝搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-134">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="a9ff1-135">當我們繼續透過這個階段中的 NuGet 3.0 開發時，我們將會調整和監視 nuget.org 服務，以確保我們提供較佳的體驗。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-135">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="a9ff1-136">我們執行未進行任何停機時間，以計劃，但會新增及變更服務中的資源。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-136">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="a9ff1-137">請注意我們[twitter 摘要](http://twitter.com/nuget)如當我們變更服務組態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-137">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="a9ff1-138">建置隨 NuGet 的 NuGet</span><span class="sxs-lookup"><span data-stu-id="a9ff1-138">Building NuGet with NuGet</span></span>

<span data-ttu-id="a9ff1-139">我們現在有重新我們 NuGet 用戶端架構本身正在建置為 NuGet 封裝的數個元件。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-139">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="a9ff1-140">這個重複使用我們自己的程式庫會強制我們建立可重複使用，而且可以適當地封裝的元件。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-140">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="a9ff1-141">我們已能夠消除重複的程式碼，並已經學會如何進一步設定我們的開發程序，以支援需要建置整個解決方案的封裝。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-141">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="a9ff1-142">尋找推出的部落格文章，我們將討論如何結構化程式碼專案及我們的建置程序的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a9ff1-142">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="a9ff1-143">敬請期待</span><span class="sxs-lookup"><span data-stu-id="a9ff1-143">Stay Tuned</span></span>

<span data-ttu-id="a9ff1-144">請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及針對 NuGet 3.0 公告 ！</span><span class="sxs-lookup"><span data-stu-id="a9ff1-144">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>
