---
title: NuGet 3.4 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.4 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551187"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="999ec-103">NuGet 3.4 的版本資訊</span><span class="sxs-lookup"><span data-stu-id="999ec-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="999ec-104">[NuGet 3.4 RC 版本資訊](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 版本資訊](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="999ec-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="999ec-105">NuGet 3.4 2016 年 3 月 30 日發行 Visual Studio 2015 Update 2 和 Visual Studio 15 Preview 版本的過程，並在心中的幾個要件建置：</span><span class="sxs-lookup"><span data-stu-id="999ec-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="999ec-106">跨平台支援</span><span class="sxs-lookup"><span data-stu-id="999ec-106">Cross-Platform support</span></span>
* <span data-ttu-id="999ec-107">效能改善</span><span class="sxs-lookup"><span data-stu-id="999ec-107">Performance improvements</span></span>
* <span data-ttu-id="999ec-108">次要 UI 增強功能</span><span class="sxs-lookup"><span data-stu-id="999ec-108">Minor UI improvements</span></span>

<span data-ttu-id="999ec-109">下列功能先前新增的功能和已更新或完成 3.4 的版本：</span><span class="sxs-lookup"><span data-stu-id="999ec-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="999ec-110">新功能</span><span class="sxs-lookup"><span data-stu-id="999ec-110">New Features</span></span>

* <span data-ttu-id="999ec-111">NuGet 用戶端現在支援 gzip 內容編碼方式從存放庫</span><span class="sxs-lookup"><span data-stu-id="999ec-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="999ec-112">從 xproj 專案封裝的 Pdb 的支援</span><span class="sxs-lookup"><span data-stu-id="999ec-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="999ec-113">適用於 iOS 和 Android 的建置動作 contentFiles 項目中的支援</span><span class="sxs-lookup"><span data-stu-id="999ec-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="999ec-114">支援 netstandard 和 netstandardapp framework moniker</span><span class="sxs-lookup"><span data-stu-id="999ec-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="999ec-115">新的使用者介面功能</span><span class="sxs-lookup"><span data-stu-id="999ec-115">New User Interface Features</span></span>

* <span data-ttu-id="999ec-116">特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善</span><span class="sxs-lookup"><span data-stu-id="999ec-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="999ec-117">彙總的 「 所有套件來源 」 來源會提供適當的搜尋結果合併</span><span class="sxs-lookup"><span data-stu-id="999ec-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="999ec-118">安裝和更新索引標籤現在會依字母順序排序</span><span class="sxs-lookup"><span data-stu-id="999ec-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="999ec-119">新增 [重新整理] 按鈕，可搜尋，以重新整理</span><span class="sxs-lookup"><span data-stu-id="999ec-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="999ec-120">頂端的 [版本] 清單的最新組建選項</span><span class="sxs-lookup"><span data-stu-id="999ec-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="999ec-121">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="999ec-121">Updates and Improvements</span></span>

* <span data-ttu-id="999ec-122">中參考的套件`project.json`具有浮點版本將不會在每個組建上更新。</span><span class="sxs-lookup"><span data-stu-id="999ec-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="999ec-123">相反地，它們會在其中更新時，只強制還原、 清除、 重建或修改`project.json`。</span><span class="sxs-lookup"><span data-stu-id="999ec-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="999ec-124">當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不再強制到專案組態。</span><span class="sxs-lookup"><span data-stu-id="999ec-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="999ec-125">NuGet 不會再還原共用專案中的套件，或寫入鎖定的檔案。</span><span class="sxs-lookup"><span data-stu-id="999ec-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="999ec-126">我們改進了網路連線失敗，並再試一次無法連線或緩慢回覆伺服器處理。</span><span class="sxs-lookup"><span data-stu-id="999ec-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="999ec-127">鍵盤和滑鼠行為有改進 Visual Studio 套件管理員 UI 中。</span><span class="sxs-lookup"><span data-stu-id="999ec-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="999ec-128">我們現在支援最新`project.json`DNX 中的結構描述。</span><span class="sxs-lookup"><span data-stu-id="999ec-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="999ec-129">重大變更</span><span class="sxs-lookup"><span data-stu-id="999ec-129">Breaking Changes</span></span>

* <span data-ttu-id="999ec-130">套件版本號碼現在會正規化格式*主要*。*次要*。*修補*-*發行前版本*每個主要、 次要和修補程式會被視為整數和卸除任何前置的零。</span><span class="sxs-lookup"><span data-stu-id="999ec-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="999ec-131">發行前版本的資訊會被視為字串，並不套用任何變更。</span><span class="sxs-lookup"><span data-stu-id="999ec-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="999ec-132">這些數字會使用 NuGet 用戶端和 nuget.org 服務所提供的搜尋查詢中。</span><span class="sxs-lookup"><span data-stu-id="999ec-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="999ec-133">更多詳細資料，請參閱 NuGet 文件下,[發行前版本版本](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="999ec-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="999ec-134">已知問題</span><span class="sxs-lookup"><span data-stu-id="999ec-134">Known Issues</span></span>

* <span data-ttu-id="999ec-135">**問題：** Windows 10 v1511 使用者可能會遇到問題或甚至是 Visual Studio 損毀在 Visual Studio 中使用 Powershell 在下列情況：</span><span class="sxs-lookup"><span data-stu-id="999ec-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="999ec-136">安裝 / 解除安裝套件有 install.ps1 / uninstall.ps1 指令碼</span><span class="sxs-lookup"><span data-stu-id="999ec-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="999ec-137">正在載入 （例如 EntityFramework) init.ps1 指令碼的專案</span><span class="sxs-lookup"><span data-stu-id="999ec-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="999ec-138">發行的 web 內容</span><span class="sxs-lookup"><span data-stu-id="999ec-138">Publishing web content</span></span>

* <span data-ttu-id="999ec-139">**因應措施：** 請確定您的 Windows 10 安裝具有最新套用的修補程式、 expecially 年 1 月 2016 (KB 3124263) 或更新版的更新。</span><span class="sxs-lookup"><span data-stu-id="999ec-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="999ec-140">更多詳細資料位於[GitHub 問題 # 1638年](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="999ec-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="999ec-141">**問題** ：NuGet v2 通訊協定重新導向中斷。</span><span class="sxs-lookup"><span data-stu-id="999ec-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="999ec-142">將要求重新導向至替代主機的自訂 NuGet 儲存機制不接受重新導向要求。</span><span class="sxs-lookup"><span data-stu-id="999ec-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="999ec-143">**因應措施：** 若要解決此問題，請同時設定套件儲存機制 URI 設定為指向重新導向的伺服器位置。</span><span class="sxs-lookup"><span data-stu-id="999ec-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="999ec-144">如需詳細資訊，請參閱 < [GitHub 提取要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。</span><span class="sxs-lookup"><span data-stu-id="999ec-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="999ec-145">我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="999ec-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>