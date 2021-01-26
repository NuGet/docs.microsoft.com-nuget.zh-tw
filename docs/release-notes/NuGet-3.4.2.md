---
title: NuGet 3.4.2 版本資訊
description: NuGet 3.4.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780255"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="5c9e4-103">NuGet 3.4.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="5c9e4-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="5c9e4-104">[NuGet 3.4.1 版本](../release-notes/nuget-3.4.1.md)  |  資訊[NuGet 3.4.3 版本](../release-notes/nuget-3.4.3.md)資訊</span><span class="sxs-lookup"><span data-stu-id="5c9e4-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="5c9e4-105">NuGet 3.4.2 已于2016年4月8日發行，以解決3.4 和3.4.1 版本中所識別的數個問題。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="5c9e4-106">nuget.exe 3.4.2 RC 現已推出</span><span class="sxs-lookup"><span data-stu-id="5c9e4-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="5c9e4-107">您可以在 [這裡](https://dist.nuget.org/index.html)下載 nuget.exe 3.4.2 的候選版。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="5c9e4-108">更新和改進</span><span class="sxs-lookup"><span data-stu-id="5c9e4-108">Updates and Improvements</span></span>

* <span data-ttu-id="5c9e4-109">我們大幅改善了特定案例中更新的效能，其中具有深度相依性圖形的套件更新會花很長的時間，並使 Visual Studio 無反應。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="5c9e4-110">在 Visual Studio 的情況下，不需要網路流量的 nuget 還原為 2.5 x –3倍。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="5c9e4-111">除了這項變更之外，我們也修正了在 VS UI 中提取更新計數時，達到網路兩次的問題。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="5c9e4-112">這部分負責一些客戶在 3.4/3.4.1 中遇到的超時問題。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="5c9e4-113">已新增 no_proxy 設定的支援</span><span class="sxs-lookup"><span data-stu-id="5c9e4-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="5c9e4-114">修正</span><span class="sxs-lookup"><span data-stu-id="5c9e4-114">Fixes</span></span>

* <span data-ttu-id="5c9e4-115">修正了在更新至3.4.1 之後，NuGet 設定或設定中遺失 nuget.org 來源的問題。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="5c9e4-116">修正3.4.1 中 FindPackagesById 的大小寫變更為中斷 Artifactory 的問題。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="5c9e4-117">修正了使用 nuget.exe 的 NuGet 還原造成失敗的 FIPS 問題。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="5c9e4-118">修正了使用無效圖示 URL 流覽來源時的損毀。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="5c9e4-119">修正了從 [所有來源] 合併版本和專案的問題。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="5c9e4-120">3.4.2 Windows x86 命令列 (RC) 的已知問題</span><span class="sxs-lookup"><span data-stu-id="5c9e4-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="5c9e4-121">這些問題將會在我們按下一周的初期修正。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="5c9e4-122">如果解決方案檔放置於比專案檔還低的資料夾階層中，在方案上執行 nuget 還原將會失敗。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="5c9e4-123">使用 V2 摘要在封裝上執行 nuget 刪除命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="5c9e4-124">請改用 V3 摘要。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-124">Use V3 feed instead.</span></span>


<span data-ttu-id="5c9e4-125">如需此版本中的修正和增強功能的完整清單，請參閱 [此處](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)的問題清單。</span><span class="sxs-lookup"><span data-stu-id="5c9e4-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>