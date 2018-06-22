---
title: NuGet 3.4 RC 版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.4 RC 版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820816"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="001d4-103">NuGet 3.4 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="001d4-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="001d4-104">[NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md) | [NuGet 3.4 版本資訊](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="001d4-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="001d4-105">NuGet 3.4 RC 2016 年 3 月 3 日與 Visual Studio 2015 Update 2 RC 一起發行，並不在建置中對少數原則：</span><span class="sxs-lookup"><span data-stu-id="001d4-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="001d4-106">跨平台支援</span><span class="sxs-lookup"><span data-stu-id="001d4-106">Cross-Platform support</span></span>
* <span data-ttu-id="001d4-107">效能改善</span><span class="sxs-lookup"><span data-stu-id="001d4-107">Performance improvements</span></span>
* <span data-ttu-id="001d4-108">次要的 UI 增強功能</span><span class="sxs-lookup"><span data-stu-id="001d4-108">Minor UI improvements</span></span>

<span data-ttu-id="001d4-109">下列功能可用在 RC 中，具有多個計劃 3.4 最後發行版本。</span><span class="sxs-lookup"><span data-stu-id="001d4-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="001d4-110">新功能</span><span class="sxs-lookup"><span data-stu-id="001d4-110">New Features</span></span>

* <span data-ttu-id="001d4-111">NuGet 用戶端現在支援 gzip 內容編碼方式從儲存機制</span><span class="sxs-lookup"><span data-stu-id="001d4-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="001d4-112">支援從 xproj 專案封裝的 Pdb</span><span class="sxs-lookup"><span data-stu-id="001d4-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="001d4-113">適用於 iOS 和 Android 的建置動作 contentFiles 元素中的支援</span><span class="sxs-lookup"><span data-stu-id="001d4-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="001d4-114">支援 netstandard 和 netstandardapp framework moniker</span><span class="sxs-lookup"><span data-stu-id="001d4-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="001d4-115">新的使用者介面功能</span><span class="sxs-lookup"><span data-stu-id="001d4-115">New User Interface Features</span></span>

* <span data-ttu-id="001d4-116">特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善</span><span class="sxs-lookup"><span data-stu-id="001d4-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="001d4-117">安裝和更新索引標籤現在會依字母順序排序</span><span class="sxs-lookup"><span data-stu-id="001d4-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="001d4-118">新增 [重新整理] 按鈕，可讓重新整理的搜尋</span><span class="sxs-lookup"><span data-stu-id="001d4-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="001d4-119">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="001d4-119">Updates and Improvements</span></span>

* <span data-ttu-id="001d4-120">封裝中參考`project.json`具有浮點版本將不會在每次建置更新。</span><span class="sxs-lookup"><span data-stu-id="001d4-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="001d4-121">相反地，他們會更新只能在強制還原、 清除、 重建或修改時`project.json`。</span><span class="sxs-lookup"><span data-stu-id="001d4-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="001d4-122">當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不會強制到專案組態。</span><span class="sxs-lookup"><span data-stu-id="001d4-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="001d4-123">NuGet 無法再還原共用的專案中的封裝，也寫入鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="001d4-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="001d4-124">我們已改進網路失敗，然後重試處理連上或緩慢-到-回應的伺服器。</span><span class="sxs-lookup"><span data-stu-id="001d4-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="001d4-125">鍵盤和滑鼠的行為會在 Visual Studio 封裝管理員 UI 改進。</span><span class="sxs-lookup"><span data-stu-id="001d4-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="001d4-126">我們現在支援最新`project.json`DNX 中的結構描述。</span><span class="sxs-lookup"><span data-stu-id="001d4-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="001d4-127">已知問題</span><span class="sxs-lookup"><span data-stu-id="001d4-127">Known Issues</span></span>

<span data-ttu-id="001d4-128">我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="001d4-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>