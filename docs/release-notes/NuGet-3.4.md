---
title: NuGet 3.4 版本資訊
description: NuGet 3.4 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776418"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="58439-103">NuGet 3.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="58439-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="58439-104">[NuGet 3.4-RC 版本](../release-notes/nuget-3.4-RC.md)  |  資訊[NuGet 3.4.1 版本](../release-notes/nuget-3.4.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="58439-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="58439-105">NuGet 3.4 已于2016年3月30日發行，作為 Visual Studio 2015 Update 2 和 Visual Studio 15 Preview 版本的一部分，並以一些思維原則建立：</span><span class="sxs-lookup"><span data-stu-id="58439-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="58439-106">跨平臺支援</span><span class="sxs-lookup"><span data-stu-id="58439-106">Cross-Platform support</span></span>
* <span data-ttu-id="58439-107">效能改善</span><span class="sxs-lookup"><span data-stu-id="58439-107">Performance improvements</span></span>
* <span data-ttu-id="58439-108">次要 UI 改進</span><span class="sxs-lookup"><span data-stu-id="58439-108">Minor UI improvements</span></span>

<span data-ttu-id="58439-109">先前已在 RC 中新增下列功能，並已針對3.4 版本更新或完成：</span><span class="sxs-lookup"><span data-stu-id="58439-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="58439-110">新功能</span><span class="sxs-lookup"><span data-stu-id="58439-110">New Features</span></span>

* <span data-ttu-id="58439-111">NuGet 用戶端現在支援從存放庫進行 gzip 內容編碼</span><span class="sxs-lookup"><span data-stu-id="58439-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="58439-112">從 xproj 專案中的套件支援 Pdb</span><span class="sxs-lookup"><span data-stu-id="58439-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="58439-113">ContentFiles 元素中的 iOS 和 Android 組建動作支援</span><span class="sxs-lookup"><span data-stu-id="58439-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="58439-114">支援 netstandard 和 netstandardapp 架構的名字標記</span><span class="sxs-lookup"><span data-stu-id="58439-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="58439-115">新的消費者介面功能</span><span class="sxs-lookup"><span data-stu-id="58439-115">New User Interface Features</span></span>

* <span data-ttu-id="58439-116">明顯的效能改進，特別是針對已安裝、更新和合併索引標籤</span><span class="sxs-lookup"><span data-stu-id="58439-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="58439-117">匯總的「所有套件來源」來源可透過適當的搜尋結果合併來使用</span><span class="sxs-lookup"><span data-stu-id="58439-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="58439-118">已安裝和更新索引標籤現在會依字母順序排序</span><span class="sxs-lookup"><span data-stu-id="58439-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="58439-119">已新增可讓您重新整理搜尋的 [重新整理] 按鈕</span><span class="sxs-lookup"><span data-stu-id="58439-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="58439-120">版本清單頂端的最新組建選項</span><span class="sxs-lookup"><span data-stu-id="58439-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="58439-121">更新和改進</span><span class="sxs-lookup"><span data-stu-id="58439-121">Updates and Improvements</span></span>

* <span data-ttu-id="58439-122">中參考的封裝在 `project.json` 每個組建上都不會更新。</span><span class="sxs-lookup"><span data-stu-id="58439-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="58439-123">相反地，只有在強制還原、清除、重建或修改時，才會更新 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="58439-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="58439-124">當您使用 NuGet 設定 UI 時，不會再將 nuget.org 存放庫來源強制進入專案設定。</span><span class="sxs-lookup"><span data-stu-id="58439-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="58439-125">NuGet 不再還原共用專案中的套件，也不會寫入鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="58439-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="58439-126">我們改進了網路失敗，並會重試處理，以找出無法連線或回應緩慢的伺服器。</span><span class="sxs-lookup"><span data-stu-id="58439-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="58439-127">Visual Studio 封裝管理員 UI 中的鍵盤和滑鼠行為已獲得改善。</span><span class="sxs-lookup"><span data-stu-id="58439-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="58439-128">我們現在支援 DNX 中的最新 `project.json` 架構。</span><span class="sxs-lookup"><span data-stu-id="58439-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="58439-129">重大變更</span><span class="sxs-lookup"><span data-stu-id="58439-129">Breaking Changes</span></span>

* <span data-ttu-id="58439-130">套件版本號碼現在會正規化為 *主要* 格式。*次要*。*修補程式* -*發行* 前版本  每個主要、次要和修補程式都會被視為整數，並捨棄任何前置零。</span><span class="sxs-lookup"><span data-stu-id="58439-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="58439-131">發行前版本資訊會視為字串，且不會套用任何變更。</span><span class="sxs-lookup"><span data-stu-id="58439-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="58439-132">NuGet 用戶端和 nuget.org 服務提供的搜尋會在查詢中使用這些數位。</span><span class="sxs-lookup"><span data-stu-id="58439-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="58439-133">您可以在 NuGet 檔的 [發行前版本](../create-packages/prerelease-packages.md)中找到更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="58439-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="58439-134">已知問題</span><span class="sxs-lookup"><span data-stu-id="58439-134">Known Issues</span></span>

* <span data-ttu-id="58439-135">**問題：** 在下列情況下，Windows 10 v1511 使用者可能會在 Visual Studio 中遇到問題，或甚至是使用 Powershell Visual Studio 損毀：</span><span class="sxs-lookup"><span data-stu-id="58439-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="58439-136">安裝/卸載具有 install.ps1/uninstall.ps1 腳本的封裝</span><span class="sxs-lookup"><span data-stu-id="58439-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="58439-137">載入具有 init.ps1 腳本的專案 (例如 EntityFramework) </span><span class="sxs-lookup"><span data-stu-id="58439-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="58439-138">發佈 web 內容</span><span class="sxs-lookup"><span data-stu-id="58439-138">Publishing web content</span></span>

* <span data-ttu-id="58439-139">因應措施 **：** 確定您的 Windows 10 安裝已套用最新的修補程式，請別2016年1月 (KB 3124263) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="58439-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="58439-140">[GitHub 問題](http://github.com/nuget/home/issues/1638)有更多詳細資料 #1638</span><span class="sxs-lookup"><span data-stu-id="58439-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="58439-141">**問題** ：NuGet v2 通訊協定重新導向中斷。</span><span class="sxs-lookup"><span data-stu-id="58439-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="58439-142">將要求重新導向至替代主機的自訂 NuGet 儲存機制不接受重新導向要求。</span><span class="sxs-lookup"><span data-stu-id="58439-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="58439-143">因應措施 **：** 若要解決此問題，請將設定中的套件存放庫 URI 設定為指向重新導向的伺服器位置。</span><span class="sxs-lookup"><span data-stu-id="58439-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="58439-144">如需詳細資訊，請參閱 [GitHub 提取要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。</span><span class="sxs-lookup"><span data-stu-id="58439-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="58439-145">我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="58439-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>