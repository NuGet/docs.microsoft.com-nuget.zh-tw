---
title: NuGet 3.0 版本資訊
description: 版本資訊 NuGet 3.0.0 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551859"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="0aacc-103">NuGet 3.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="0aacc-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="0aacc-104">[NuGet 3.0 RC2 版本資訊](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 版本資訊](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="0aacc-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="0aacc-105">NuGet 3.0 已於 2015 年 7 月 20 日發行，為 Visual Studio 2015 的套件組合擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0aacc-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="0aacc-106">我們推入來傳遞此版本中的使用 Visual Studio，以便完成更新的 NuGet 3.0 體驗可供新的 Visual Studio 使用者。</span><span class="sxs-lookup"><span data-stu-id="0aacc-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="0aacc-107">這個 NuGet 擴充功能版本僅適用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="0aacc-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="0aacc-108">我們建議開發人員可存取 Visual Studio 組件庫更新，可供使用，因為我們會包含支援 Windows 10 開發的 Visual Studio 2015 發行後，馬上來發佈更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="0aacc-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="0aacc-109">總計中，我們關閉 240 問題在 3.0 版的版本中，且您可以檢閱[GitHub 上的問題的完整清單](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="0aacc-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0aacc-110">已知問題</span><span class="sxs-lookup"><span data-stu-id="0aacc-110">Known Issues</span></span>

<span data-ttu-id="0aacc-111">有幾個與此版本中，傳遞的已知問題，所有這些項目固定的排程與 Windows 10 版本一致。 在 7 月 29 3.1 版本中。</span><span class="sxs-lookup"><span data-stu-id="0aacc-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="0aacc-112">您就能夠更新您的 Visual Studio 延伸模組，從資源庫來修正這些已知的問題該日期當天或之後。</span><span class="sxs-lookup"><span data-stu-id="0aacc-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="0aacc-113">未提供轉譯為 「 不要再顯示此訊息 」 標籤上預覽 視窗，並封裝的 說明 視窗中的 「 著作人 」 標籤。</span><span class="sxs-lookup"><span data-stu-id="0aacc-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="0aacc-114">當您使用 TFS 使用的專案原始檔控制時，NuGet 無法呈現的套件管理員的使用者介面如果 Nuget.Config 檔案標示為唯讀。</span><span class="sxs-lookup"><span data-stu-id="0aacc-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="0aacc-115">**因應措施**查看 TFS 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="0aacc-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="0aacc-116">以黃色 NuGet Powershell 視窗中的 「 重新啟動列 」 的文字不是可見的當您使用 Visual Studio 暗色調佈景主題。</span><span class="sxs-lookup"><span data-stu-id="0aacc-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="0aacc-117">**因應措施**使用 Visual Studio 的淺色佈景主題。</span><span class="sxs-lookup"><span data-stu-id="0aacc-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="0aacc-118">最常發生的問題已解決的摘要</span><span class="sxs-lookup"><span data-stu-id="0aacc-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="0aacc-119">常見網路更新呼叫時重新整理套件管理員視窗</span><span class="sxs-lookup"><span data-stu-id="0aacc-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="0aacc-120">變更為安裝套件管理員中的檢視時，延遲捲軸</span><span class="sxs-lookup"><span data-stu-id="0aacc-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="0aacc-121">網路呼叫應該在背景執行緒上執行</span><span class="sxs-lookup"><span data-stu-id="0aacc-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* <span data-ttu-id="0aacc-122">[已新增 [不顯示預覽視窗] 的核取方塊](https://github.com/NuGet/Home/issues/566)</span><span class="sxs-lookup"><span data-stu-id="0aacc-122">[Added 'Do not show preview window' checkbox](https://github.com/NuGet/Home/issues/566)</span></span>
* [<span data-ttu-id="0aacc-123">已新增的處理程序節流來降低處理器使用量</span><span class="sxs-lookup"><span data-stu-id="0aacc-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="0aacc-124">改良的可攜式類別庫參考處理</span><span class="sxs-lookup"><span data-stu-id="0aacc-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="0aacc-125">自動完成 service 已區分大小寫</span><span class="sxs-lookup"><span data-stu-id="0aacc-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="0aacc-126">引進基本驗證認證的更新</span><span class="sxs-lookup"><span data-stu-id="0aacc-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="0aacc-127">已改善的錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="0aacc-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="0aacc-128">呼叫更新套件時，改善的 powershell 錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="0aacc-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="0aacc-129">已修正 深入了解選項' 連結，以防止在 Windows 10 上損毀</span><span class="sxs-lookup"><span data-stu-id="0aacc-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="0aacc-130">請記住發行前版本 核取方塊設定</span><span class="sxs-lookup"><span data-stu-id="0aacc-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="0aacc-131">依方案中專案的快取結果的改良蒐集效能</span><span class="sxs-lookup"><span data-stu-id="0aacc-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="0aacc-132">您可以以平行方式收集多個封裝</span><span class="sxs-lookup"><span data-stu-id="0aacc-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="0aacc-133">安裝套件中移除-強制執行命令</span><span class="sxs-lookup"><span data-stu-id="0aacc-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="0aacc-134">請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和宣布，我們準備好提供適用於 Windows 10 開發的支援。</span><span class="sxs-lookup"><span data-stu-id="0aacc-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>