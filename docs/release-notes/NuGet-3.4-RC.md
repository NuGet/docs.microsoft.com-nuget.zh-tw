---
title: NuGet 3.4 RC 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.4 RC 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546750"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="ab857-103">NuGet 3.4 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="ab857-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="ab857-104">[NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md) | [NuGet 3.4 的版本資訊](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="ab857-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="ab857-105">NuGet 3.4 RC 發行 2016 年 3 月 3 日與 Visual Studio 2015 Update 2 RC，並在心中的幾個要件建置：</span><span class="sxs-lookup"><span data-stu-id="ab857-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="ab857-106">跨平台支援</span><span class="sxs-lookup"><span data-stu-id="ab857-106">Cross-Platform support</span></span>
* <span data-ttu-id="ab857-107">效能改善</span><span class="sxs-lookup"><span data-stu-id="ab857-107">Performance improvements</span></span>
* <span data-ttu-id="ab857-108">次要 UI 增強功能</span><span class="sxs-lookup"><span data-stu-id="ab857-108">Minor UI improvements</span></span>

<span data-ttu-id="ab857-109">下列功能時才可在這個 RC 中，使用更有計劃 3.4 版的最終發行版本。</span><span class="sxs-lookup"><span data-stu-id="ab857-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="ab857-110">新功能</span><span class="sxs-lookup"><span data-stu-id="ab857-110">New Features</span></span>

* <span data-ttu-id="ab857-111">NuGet 用戶端現在支援 gzip 內容編碼方式從存放庫</span><span class="sxs-lookup"><span data-stu-id="ab857-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="ab857-112">從 xproj 專案封裝的 Pdb 的支援</span><span class="sxs-lookup"><span data-stu-id="ab857-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="ab857-113">適用於 iOS 和 Android 的建置動作 contentFiles 項目中的支援</span><span class="sxs-lookup"><span data-stu-id="ab857-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="ab857-114">支援 netstandard 和 netstandardapp framework moniker</span><span class="sxs-lookup"><span data-stu-id="ab857-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ab857-115">新的使用者介面功能</span><span class="sxs-lookup"><span data-stu-id="ab857-115">New User Interface Features</span></span>

* <span data-ttu-id="ab857-116">特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善</span><span class="sxs-lookup"><span data-stu-id="ab857-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="ab857-117">安裝和更新索引標籤現在會依字母順序排序</span><span class="sxs-lookup"><span data-stu-id="ab857-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="ab857-118">新增 [重新整理] 按鈕，可搜尋，以重新整理</span><span class="sxs-lookup"><span data-stu-id="ab857-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ab857-119">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="ab857-119">Updates and Improvements</span></span>

* <span data-ttu-id="ab857-120">中參考的套件`project.json`具有浮點版本將不會在每個組建上更新。</span><span class="sxs-lookup"><span data-stu-id="ab857-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="ab857-121">相反地，它們會在其中更新時，只強制還原、 清除、 重建或修改`project.json`。</span><span class="sxs-lookup"><span data-stu-id="ab857-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="ab857-122">當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不再強制到專案組態。</span><span class="sxs-lookup"><span data-stu-id="ab857-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="ab857-123">NuGet 不會再還原共用專案中的套件，或寫入鎖定的檔案。</span><span class="sxs-lookup"><span data-stu-id="ab857-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="ab857-124">我們改進了網路連線失敗，並再試一次無法連線或緩慢回覆伺服器處理。</span><span class="sxs-lookup"><span data-stu-id="ab857-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="ab857-125">鍵盤和滑鼠行為有改進 Visual Studio 套件管理員 UI 中。</span><span class="sxs-lookup"><span data-stu-id="ab857-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="ab857-126">我們現在支援最新`project.json`DNX 中的結構描述。</span><span class="sxs-lookup"><span data-stu-id="ab857-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="ab857-127">已知問題</span><span class="sxs-lookup"><span data-stu-id="ab857-127">Known Issues</span></span>

<span data-ttu-id="ab857-128">我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ab857-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>