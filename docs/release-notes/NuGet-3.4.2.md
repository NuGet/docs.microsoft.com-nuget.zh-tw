---
title: NuGet 3.4.2 版本資訊
description: NuGet 3.4.2 中包含的版本資訊的已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549147"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="19554-103">NuGet 3.4.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="19554-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="19554-104">[NuGet 3.4.1 版本資訊](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 版本資訊](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="19554-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="19554-105">NuGet 3.4.2 已於 2016 年 4 月 8 日解決在 3.4 和 3.4.1 中識別的幾個問題發行版本。</span><span class="sxs-lookup"><span data-stu-id="19554-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="19554-106">nuget.exe 3.4.2 RC 已正式發行</span><span class="sxs-lookup"><span data-stu-id="19554-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="19554-107">您可以下載的發行候選版本的 nuget.exe 3.4.2[此處](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="19554-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="19554-108">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="19554-108">Updates and Improvements</span></span>

* <span data-ttu-id="19554-109">我們大幅改善效能的特定案例中，更新封裝名稱中有深入的相依性圖形，花了很長的時間和停止 Visual Studio 中的更新。</span><span class="sxs-lookup"><span data-stu-id="19554-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="19554-110">nuget 還原，而不需要網路流量是 2.5 倍快 Visual Studio 中的 3 倍。</span><span class="sxs-lookup"><span data-stu-id="19554-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="19554-111">除了這項變更，我們已修正的問題，我們已達到網路 VS UI 中擷取更新計數時，兩次。</span><span class="sxs-lookup"><span data-stu-id="19554-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="19554-112">這是部分負責一些逾時問題的客戶經驗 3.4/3.4.1。</span><span class="sxs-lookup"><span data-stu-id="19554-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="19554-113">已新增的支援 no_proxy 設定</span><span class="sxs-lookup"><span data-stu-id="19554-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="19554-114">修正</span><span class="sxs-lookup"><span data-stu-id="19554-114">Fixes</span></span>

* <span data-ttu-id="19554-115">Nuget.org 來源的 NuGet 設定或組態中遺漏更新至 3.4.1 之後修正的問題。</span><span class="sxs-lookup"><span data-stu-id="19554-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="19554-116">其中 FindPackagesById 3.4.1 中的大小寫變更會中斷 Artifactory 修正的問題。</span><span class="sxs-lookup"><span data-stu-id="19554-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="19554-117">已更正 fips，nuget.exe 與 NuGet 還原導致失敗的問題。</span><span class="sxs-lookup"><span data-stu-id="19554-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="19554-118">瀏覽具有無效的圖示 URL 來源時，請修正損毀。</span><span class="sxs-lookup"><span data-stu-id="19554-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="19554-119">已修正合併版本和項目從 「 所有來源 」 的問題。</span><span class="sxs-lookup"><span data-stu-id="19554-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="19554-120">已知問題 3.4.2 中 Windows x86 命令列 (RC)</span><span class="sxs-lookup"><span data-stu-id="19554-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="19554-121">早期的下一週我們按下 RTM 之前，將會修正這些問題。</span><span class="sxs-lookup"><span data-stu-id="19554-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="19554-122">如果方案檔放在較低的資料夾階層，於專案檔，在方案上的執行 nuget 還原將會失敗。</span><span class="sxs-lookup"><span data-stu-id="19554-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="19554-123">使用 V2 摘要的套件上執行 nuget delete 命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="19554-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="19554-124">請改用 V3 摘要。</span><span class="sxs-lookup"><span data-stu-id="19554-124">Use V3 feed instead.</span></span>


<span data-ttu-id="19554-125">如中此版本的修正和改善的完整清單，請參閱的問題清單[此處](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。</span><span class="sxs-lookup"><span data-stu-id="19554-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>