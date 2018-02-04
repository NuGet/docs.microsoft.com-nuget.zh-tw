---
title: "NuGet 3.4 RC 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.4 RC 版本資訊。"
keywords: "NuGet 3.4 RC 版本資訊、 錯誤修正，已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="8ae27-104">NuGet 3.4 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="8ae27-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="8ae27-105">[NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md) | [NuGet 3.4 版本資訊](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="8ae27-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="8ae27-106">NuGet 3.4 RC 2016 年 3 月 3 日與 Visual Studio 2015 Update 2 RC 一起發行，並不在建置中對少數原則：</span><span class="sxs-lookup"><span data-stu-id="8ae27-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="8ae27-107">跨平台支援</span><span class="sxs-lookup"><span data-stu-id="8ae27-107">Cross-Platform support</span></span>
* <span data-ttu-id="8ae27-108">效能改善</span><span class="sxs-lookup"><span data-stu-id="8ae27-108">Performance improvements</span></span>
* <span data-ttu-id="8ae27-109">次要的 UI 增強功能</span><span class="sxs-lookup"><span data-stu-id="8ae27-109">Minor UI improvements</span></span>

<span data-ttu-id="8ae27-110">下列功能可用在 RC 中，具有多個計劃 3.4 最後發行版本。</span><span class="sxs-lookup"><span data-stu-id="8ae27-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="8ae27-111">新功能</span><span class="sxs-lookup"><span data-stu-id="8ae27-111">New Features</span></span>

* <span data-ttu-id="8ae27-112">NuGet 用戶端現在支援 gzip 內容編碼方式從儲存機制</span><span class="sxs-lookup"><span data-stu-id="8ae27-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="8ae27-113">支援從 xproj 專案封裝的 Pdb</span><span class="sxs-lookup"><span data-stu-id="8ae27-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="8ae27-114">適用於 iOS 和 Android 的建置動作 contentFiles 元素中的支援</span><span class="sxs-lookup"><span data-stu-id="8ae27-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="8ae27-115">支援 netstandard 和 netstandardapp framework moniker</span><span class="sxs-lookup"><span data-stu-id="8ae27-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="8ae27-116">新的使用者介面功能</span><span class="sxs-lookup"><span data-stu-id="8ae27-116">New User Interface Features</span></span>

* <span data-ttu-id="8ae27-117">特別是在已安裝、 更新及合併彙算的索引標籤上的顯著效能改善</span><span class="sxs-lookup"><span data-stu-id="8ae27-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="8ae27-118">安裝和更新索引標籤現在會依字母順序排序</span><span class="sxs-lookup"><span data-stu-id="8ae27-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="8ae27-119">新增 [重新整理] 按鈕，可讓重新整理的搜尋</span><span class="sxs-lookup"><span data-stu-id="8ae27-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="8ae27-120">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="8ae27-120">Updates and Improvements</span></span>

* <span data-ttu-id="8ae27-121">封裝中參考`project.json`具有浮點版本將不會在每次建置更新。</span><span class="sxs-lookup"><span data-stu-id="8ae27-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="8ae27-122">相反地，他們會更新只能在強制還原、 清除、 重建或修改時`project.json`。</span><span class="sxs-lookup"><span data-stu-id="8ae27-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="8ae27-123">當您使用的 NuGet 組態 UI，nuget.org 儲存機制來源不會強制到專案組態。</span><span class="sxs-lookup"><span data-stu-id="8ae27-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="8ae27-124">NuGet 無法再還原共用的專案中的封裝，也寫入鎖定檔案。</span><span class="sxs-lookup"><span data-stu-id="8ae27-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="8ae27-125">我們已改進網路失敗，然後重試處理連上或緩慢-到-回應的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8ae27-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="8ae27-126">鍵盤和滑鼠的行為會在 Visual Studio 封裝管理員 UI 改進。</span><span class="sxs-lookup"><span data-stu-id="8ae27-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="8ae27-127">我們現在支援最新`project.json`DNX 中的結構描述。</span><span class="sxs-lookup"><span data-stu-id="8ae27-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="8ae27-128">已知問題</span><span class="sxs-lookup"><span data-stu-id="8ae27-128">Known Issues</span></span>

<span data-ttu-id="8ae27-129">我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="8ae27-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>