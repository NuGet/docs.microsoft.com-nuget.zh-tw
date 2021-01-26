---
title: NuGet 3.4-RC 版本資訊
description: NuGet 3.4 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780244"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="68b15-103">NuGet 3.4-RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="68b15-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="68b15-104">[NuGet 3.3 版本](../release-notes/nuget-3.3.md)  |  資訊[NuGet 3.4 版本](../release-notes/nuget-3.4.md)資訊</span><span class="sxs-lookup"><span data-stu-id="68b15-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="68b15-105">NuGet 3.4-RC 已于2016年3月3日和 Visual Studio 2015 Update 2 RC 發行，並以一些思維原則建立：</span><span class="sxs-lookup"><span data-stu-id="68b15-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="68b15-106">跨平臺支援</span><span class="sxs-lookup"><span data-stu-id="68b15-106">Cross-Platform support</span></span>
* <span data-ttu-id="68b15-107">效能改善</span><span class="sxs-lookup"><span data-stu-id="68b15-107">Performance improvements</span></span>
* <span data-ttu-id="68b15-108">次要 UI 改進</span><span class="sxs-lookup"><span data-stu-id="68b15-108">Minor UI improvements</span></span>

<span data-ttu-id="68b15-109">此 RC 提供下列功能，並已針對3.4 最終版本提供更多規劃。</span><span class="sxs-lookup"><span data-stu-id="68b15-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="68b15-110">新功能</span><span class="sxs-lookup"><span data-stu-id="68b15-110">New Features</span></span>

* <span data-ttu-id="68b15-111">NuGet 用戶端現在支援從存放庫進行 gzip 內容編碼</span><span class="sxs-lookup"><span data-stu-id="68b15-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="68b15-112">從 xproj 專案中的套件支援 Pdb</span><span class="sxs-lookup"><span data-stu-id="68b15-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="68b15-113">ContentFiles 元素中的 iOS 和 Android 組建動作支援</span><span class="sxs-lookup"><span data-stu-id="68b15-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="68b15-114">支援 netstandard 和 netstandardapp 架構的名字標記</span><span class="sxs-lookup"><span data-stu-id="68b15-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="68b15-115">新的消費者介面功能</span><span class="sxs-lookup"><span data-stu-id="68b15-115">New User Interface Features</span></span>

* <span data-ttu-id="68b15-116">明顯的效能改進，特別是針對已安裝、更新和合併索引標籤</span><span class="sxs-lookup"><span data-stu-id="68b15-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="68b15-117">已安裝和更新索引標籤現在會依字母順序排序</span><span class="sxs-lookup"><span data-stu-id="68b15-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="68b15-118">已新增可讓您重新整理搜尋的 [重新整理] 按鈕</span><span class="sxs-lookup"><span data-stu-id="68b15-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="68b15-119">更新和改進</span><span class="sxs-lookup"><span data-stu-id="68b15-119">Updates and Improvements</span></span>

* <span data-ttu-id="68b15-120">中參考的封裝在 `project.json` 每個組建上都不會更新。</span><span class="sxs-lookup"><span data-stu-id="68b15-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="68b15-121">相反地，只有在強制還原、清除、重建或修改時，才會更新 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="68b15-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="68b15-122">當您使用 NuGet 設定 UI 時，不會再將 nuget.org 存放庫來源強制進入專案設定。</span><span class="sxs-lookup"><span data-stu-id="68b15-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="68b15-123">NuGet 不再還原共用專案中的套件，也不會寫入鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="68b15-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="68b15-124">我們改進了網路失敗，並會重試處理，以找出無法連線或回應緩慢的伺服器。</span><span class="sxs-lookup"><span data-stu-id="68b15-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="68b15-125">Visual Studio 封裝管理員 UI 中的鍵盤和滑鼠行為已獲得改善。</span><span class="sxs-lookup"><span data-stu-id="68b15-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="68b15-126">我們現在支援 DNX 中的最新 `project.json` 架構。</span><span class="sxs-lookup"><span data-stu-id="68b15-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="68b15-127">已知問題</span><span class="sxs-lookup"><span data-stu-id="68b15-127">Known Issues</span></span>

<span data-ttu-id="68b15-128">我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="68b15-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>