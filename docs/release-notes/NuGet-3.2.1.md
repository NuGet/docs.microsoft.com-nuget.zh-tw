---
title: NuGet 3.2.1 版本資訊
description: NuGet 3.2.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776521"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="98538-103">NuGet 3.2.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="98538-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="98538-104">[NuGet 3.2 版本](../release-notes/nuget-3.2.md)  |  資訊[NuGet 3.3 版本](../release-notes/nuget-3.3.md)資訊</span><span class="sxs-lookup"><span data-stu-id="98538-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="98538-105">命令列的 NuGet 3.2.1 已于2015年10月12日發行，其中包含一些3.2 版本的優化和修正程式，可從 [dist.nuget.org](http://dist.nuget.org/index.html)取得。</span><span class="sxs-lookup"><span data-stu-id="98538-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="98538-106">改善</span><span class="sxs-lookup"><span data-stu-id="98538-106">Improvements</span></span>

* <span data-ttu-id="98538-107">NuGet 現在會使用原始大小寫的設定檔 `NuGet.Config` 。</span><span class="sxs-lookup"><span data-stu-id="98538-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="98538-108">這在區分大小寫的作業系統上很重要 [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="98538-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="98538-109">NuGet 還原現在會忽略 dnx 專案 (`*.xproj`) 應使用1227進行處理 `dnu` [](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="98538-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="98538-110">使用 `index.json` 和封裝註冊資料時優化網路使用量 [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="98538-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="98538-111">使用 v2 服務[1448](https://github.com/NuGet/Home/issues/1448)改進資源下載處理功能更強大</span><span class="sxs-lookup"><span data-stu-id="98538-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="98538-112">修正</span><span class="sxs-lookup"><span data-stu-id="98538-112">Fixes</span></span>

* <span data-ttu-id="98538-113">NuGet 更新正確更新 `.csproj` / `.vcxproj` 參考[1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="98538-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="98538-114">現在防止在 SpecialFolders 時建立本機的 nuget 資料夾 [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="98538-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="98538-115">改進在本機快取中的封裝處理在下載[1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)期間損毀的程式</span><span class="sxs-lookup"><span data-stu-id="98538-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="98538-116">您可以在 NuGet GitHub [3.2.1 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)中找到針對命令列和 Visual Studio 擴充功能所解決之問題的完整清單。</span><span class="sxs-lookup"><span data-stu-id="98538-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="98538-117">已知問題</span><span class="sxs-lookup"><span data-stu-id="98538-117">Known Issues</span></span>

<span data-ttu-id="98538-118">我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="98538-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>