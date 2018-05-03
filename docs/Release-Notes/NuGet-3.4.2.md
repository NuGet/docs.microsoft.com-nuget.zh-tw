---
title: NuGet 3.4.2 版本資訊
description: 版本資訊包含 NuGet 3.4.2 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="4b815-103">NuGet 3.4.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="4b815-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="4b815-104">[NuGet 3.4.1 版本資訊](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 版本資訊](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="4b815-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="4b815-105">NuGet 3.4.2 已於 2016 年 4 月 8 日解決幾個問題中 3.4 和 3.4.1 已識別發行版本。</span><span class="sxs-lookup"><span data-stu-id="4b815-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="4b815-106">現已提供 nuget.exe 3.4.2 RC</span><span class="sxs-lookup"><span data-stu-id="4b815-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="4b815-107">您可以下載的發行候選版本的 nuget.exe 3.4.2[這裡](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="4b815-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="4b815-108">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="4b815-108">Updates and Improvements</span></span>

* <span data-ttu-id="4b815-109">我們已經大幅改善效能的特定案例中，更新封裝名稱中有深入的相依性圖形上花費很長的時間而停止 Visual Studio 中的更新。</span><span class="sxs-lookup"><span data-stu-id="4b815-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="4b815-110">沒有網路流量的 nuget 還原是 2.5 x – 更快速的 Visual Studio 中的 3 倍。</span><span class="sxs-lookup"><span data-stu-id="4b815-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="4b815-111">除了這項變更，我們已修正問題，我們已達到網路 VS UI 中擷取更新計數時，兩次。</span><span class="sxs-lookup"><span data-stu-id="4b815-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="4b815-112">這是部分負責經驗的 3.4/3.4.1 某些逾時問題客戶。</span><span class="sxs-lookup"><span data-stu-id="4b815-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="4b815-113">已新增的支援 no_proxy 設定</span><span class="sxs-lookup"><span data-stu-id="4b815-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="4b815-114">修正程式</span><span class="sxs-lookup"><span data-stu-id="4b815-114">Fixes</span></span>

* <span data-ttu-id="4b815-115">其中 nuget.org 的來源遺漏 NuGet 設定或組態中更新至 3.4.1 之後修正的問題。</span><span class="sxs-lookup"><span data-stu-id="4b815-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="4b815-116">其中 FindPackagesById 3.4.1 中的大小寫變更會中斷 Artifactory 修正的問題。</span><span class="sxs-lookup"><span data-stu-id="4b815-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="4b815-117">已更正 fips 與 nuget.exe NuGet 還原造成失敗的問題。</span><span class="sxs-lookup"><span data-stu-id="4b815-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="4b815-118">瀏覽具有無效的圖示 URL 來源時，請修正損毀。</span><span class="sxs-lookup"><span data-stu-id="4b815-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="4b815-119">已修正的問題合併版本和項目從 「 所有來源 」。</span><span class="sxs-lookup"><span data-stu-id="4b815-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="4b815-120">已知問題 3.4.2 中 Windows x86 命令列 (RC)</span><span class="sxs-lookup"><span data-stu-id="4b815-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="4b815-121">早期的下一週我們叫用 RTM 之前會解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="4b815-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="4b815-122">如果方案檔放在較低的資料夾階層，於專案檔，針對方案執行 nuget 還原將會失敗。</span><span class="sxs-lookup"><span data-stu-id="4b815-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="4b815-123">封裝使用 V2 摘要上執行 nuget delete 命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="4b815-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="4b815-124">請改用 V3 摘要。</span><span class="sxs-lookup"><span data-stu-id="4b815-124">Use V3 feed instead.</span></span>


<span data-ttu-id="4b815-125">如中這一版的修正和改善的完整清單，請參閱問題的清單[這裡](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)。</span><span class="sxs-lookup"><span data-stu-id="4b815-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>