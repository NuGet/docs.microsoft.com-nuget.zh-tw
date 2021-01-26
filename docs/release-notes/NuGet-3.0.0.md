---
title: NuGet 3.0 版本資訊
description: NuGet 3.0.0 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776549"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="10378-103">NuGet 3.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="10378-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="10378-104">[NuGet 3.0 RC2 版本](../release-notes/nuget-3.0-RC2.md)  |  資訊[NuGet 3.1 版本](../release-notes/nuget-3.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="10378-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="10378-105">NuGet 3.0 已于2015年7月20日發行為 Visual Studio 2015 的組合延伸模組。</span><span class="sxs-lookup"><span data-stu-id="10378-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="10378-106">我們推送了 Visual Studio 的版本，讓新的 Visual Studio 使用者可以使用完整的更新 NuGet 3.0 體驗。</span><span class="sxs-lookup"><span data-stu-id="10378-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="10378-107">此 NuGet 擴充功能版本僅適用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="10378-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="10378-108">我們建議可存取 Visual Studio 資源庫的開發人員更新為可用的最新版本，因為我們會在發行包含 Windows 10 開發支援的 Visual Studio 2015 之後，立即發佈更新。</span><span class="sxs-lookup"><span data-stu-id="10378-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="10378-109">總共我們在3.0 版中已關閉240問題，您可以在 [GitHub 上查看問題的完整清單](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="10378-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="10378-110">已知問題</span><span class="sxs-lookup"><span data-stu-id="10378-110">Known Issues</span></span>

<span data-ttu-id="10378-111">此版本提供了許多已知問題，所有這些專案都已在我們的排程3.1 版本中修正，以符合7月29日的 Windows 10 版本。</span><span class="sxs-lookup"><span data-stu-id="10378-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="10378-112">您可以從資源庫中或在該日期之後更新 Visual Studio 延伸模組，以修正這些已知問題。</span><span class="sxs-lookup"><span data-stu-id="10378-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="10378-113">[預覽] 視窗上的 [不要再顯示] 標籤和 [封裝描述] 視窗中的 [作者] 標籤不提供轉譯。</span><span class="sxs-lookup"><span data-stu-id="10378-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="10378-114">當您使用 TFS 原始檔控制來處理專案時，如果 Nuget.Config 檔案標示為唯讀，則 NuGet 無法顯示套件管理員使用者介面。</span><span class="sxs-lookup"><span data-stu-id="10378-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="10378-115">因應措施從 TFS 簽出檔案。</span><span class="sxs-lookup"><span data-stu-id="10378-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="10378-116">當您使用 Visual Studio 深色主題時，不會顯示 [NuGet Powershell] 視窗中黃色「重新開機列」的文字。</span><span class="sxs-lookup"><span data-stu-id="10378-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="10378-117">因應措施使用 Visual Studio 淺色主題。</span><span class="sxs-lookup"><span data-stu-id="10378-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="10378-118">已解決常見問題的摘要</span><span class="sxs-lookup"><span data-stu-id="10378-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="10378-119">當套件管理員視窗重新整理時頻繁的網路更新呼叫</span><span class="sxs-lookup"><span data-stu-id="10378-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="10378-120">在封裝管理員中變更為已安裝的視圖時，延遲捲軸</span><span class="sxs-lookup"><span data-stu-id="10378-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="10378-121">應在背景執行緒上執行網路呼叫</span><span class="sxs-lookup"><span data-stu-id="10378-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* <span data-ttu-id="10378-122">[已新增 [不要顯示預覽視窗] 核取方塊](https://github.com/NuGet/Home/issues/566)</span><span class="sxs-lookup"><span data-stu-id="10378-122">[Added 'Do not show preview window' checkbox](https://github.com/NuGet/Home/issues/566)</span></span>
* [<span data-ttu-id="10378-123">已新增進程節流來降低處理器使用量</span><span class="sxs-lookup"><span data-stu-id="10378-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="10378-124">改良的便攜類別程式庫參考處理</span><span class="sxs-lookup"><span data-stu-id="10378-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="10378-125">自動完成服務區分大小寫</span><span class="sxs-lookup"><span data-stu-id="10378-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="10378-126">更新以重新引入基本驗證認證</span><span class="sxs-lookup"><span data-stu-id="10378-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="10378-127">已改善錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="10378-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="10378-128">已改善呼叫更新套件時的 powershell 錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="10378-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* <span data-ttu-id="10378-129">[已修正 [瞭解選項] 連結，以防止當 Windows 10 時發生損毀](https://github.com/NuGet/Home/issues/822)</span><span class="sxs-lookup"><span data-stu-id="10378-129">[Fixed the 'Learn about Options' link to prevent crashing on Windows 10](https://github.com/NuGet/Home/issues/822)</span></span>
* <span data-ttu-id="10378-130">[[記住發行前版本] 核取方塊設定](https://github.com/NuGet/Home/issues/732)</span><span class="sxs-lookup"><span data-stu-id="10378-130">[Remember pre-release checkbox setting](https://github.com/NuGet/Home/issues/732)</span></span>
* [<span data-ttu-id="10378-131">藉由快取解決方案中各專案的結果來改善收集效能</span><span class="sxs-lookup"><span data-stu-id="10378-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="10378-132">可以平行收集多個封裝</span><span class="sxs-lookup"><span data-stu-id="10378-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="10378-133">已移除安裝封裝-force 命令</span><span class="sxs-lookup"><span data-stu-id="10378-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="10378-134">當我們準備好提供 Windows 10 開發的支援時，請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多的進度和公告。</span><span class="sxs-lookup"><span data-stu-id="10378-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>