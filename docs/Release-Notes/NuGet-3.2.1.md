---
title: "NuGet 3.2.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d27c3bb9-8db1-439a-a134-54e20b7a7766
description: "版本資訊包含 NuGet 3.2.1 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 3.2.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2001d9518a34bbd5f2879de6123ec13abf4ae08
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="75e94-104">NuGet 3.2.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="75e94-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="75e94-105">[NuGet 3.2 版本資訊](../release-notes/nuget-3.2.md) | [NuGet 3.3 版本資訊](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="75e94-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="75e94-106">NuGet 3.2.1 的命令列發行 2015 年 10 月 12 日少數幾個最佳化和 3.2 版的修正程式，且可從[dist.nuget.org](http://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="75e94-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="75e94-107">增強功能</span><span class="sxs-lookup"><span data-stu-id="75e94-107">Improvements</span></span>

* <span data-ttu-id="75e94-108">NuGet 現在會使用組態檔的原始大小寫`NuGet.Config`。</span><span class="sxs-lookup"><span data-stu-id="75e94-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="75e94-109">這是很重要，在區分大小寫的作業系統上[1427年](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="75e94-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="75e94-110">NuGet 還原現在將會忽略 dnx 專案 (`*.xproj`)，應具有處理`dnu` [1227年](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="75e94-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="75e94-111">使用時，最佳化網路使用量`index.json`和封裝註冊資料[1426年](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="75e94-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="75e94-112">改善的資源下載較強大 v2 服務與處理[1448年](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="75e94-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="75e94-113">修正程式</span><span class="sxs-lookup"><span data-stu-id="75e94-113">Fixes</span></span>

* <span data-ttu-id="75e94-114">NuGet 更新已正確更新`.csproj` / `.vcxproj`參考[1483年](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="75e94-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="75e94-115">現在防止本機.nuget 資料夾建立時找不到 SpecialFolders.UserProfile [1531年](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="75e94-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="75e94-116">改善的本機快取中的封裝下載期間損毀的處理[1405年](https://github.com/NuGet/Home/issues/1405) [1157年](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="75e94-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="75e94-117">命令列與 Visual Studio 擴充功能可以找到 NuGet GitHub 中解決問題的完整清單[3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="75e94-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="75e94-118">已知問題</span><span class="sxs-lookup"><span data-stu-id="75e94-118">Known Issues</span></span>

<span data-ttu-id="75e94-119">我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="75e94-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>