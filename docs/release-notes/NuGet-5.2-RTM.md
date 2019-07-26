---
title: NuGet 5.2 RTM 版本資訊
description: NuGet 5.2 的版本資訊, 包括新功能、bug 修正和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471181"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="466e4-103">NuGet 5.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="466e4-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="466e4-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="466e4-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="466e4-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="466e4-105">NuGet version</span></span> | <span data-ttu-id="466e4-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="466e4-106">Available in Visual Studio version</span></span>| <span data-ttu-id="466e4-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="466e4-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="466e4-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="466e4-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="466e4-109">Visual Studio 2019 16.2 版</span><span class="sxs-lookup"><span data-stu-id="466e4-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="466e4-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="466e4-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="466e4-111"><sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="466e4-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="466e4-112"><sup>2</sup>以含 .NET Core 工作負載的 Visual Studio 2019 的選擇性安裝形式提供</span><span class="sxs-lookup"><span data-stu-id="466e4-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="466e4-113">摘要: 5.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="466e4-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="466e4-114">已修正因 Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)上的路徑問題而造成不定期進行 NuGet 作業失敗的嚴重錯誤 (bug)</span><span class="sxs-lookup"><span data-stu-id="466e4-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="466e4-115">改善使用中的 NuGet 套件管理員 UI 流覽套件時的 UI 回應性 Visual Studio 特別明顯用於緩慢的來源- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="466e4-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="466e4-116">鎖定檔案 ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) 和驗證外掛程式的大量可靠性修正 ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271](https://github.com/NuGet/Home/issues/8271)、[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)、[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="466e4-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="466e4-117">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="466e4-117">Issues fixed in this release</span></span>

<span data-ttu-id="466e4-118">**Bug**</span><span class="sxs-lookup"><span data-stu-id="466e4-118">**Bugs**</span></span>

* <span data-ttu-id="466e4-119">效能套件管理員主控台:UI 延遲更新 [預設專案] combobox 選取的值- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="466e4-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="466e4-120">效能PM UI 中的效能改進- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="466e4-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="466e4-121">效能在 PMC 中讀取預設專案時的 UI 延遲- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="466e4-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="466e4-122">效能: [vsfeedback] 本機套件來源的 [NuGet 更新] 索引標籤凍結- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="466e4-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="466e4-123">外掛程式如果外掛程式無法啟動或提早終止, NuGet 會等待完整的交握超時時間[#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="466e4-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="466e4-124">外掛程式: 改善外掛程式啟動失敗的診斷- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="466e4-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="466e4-125">外掛程式內建外掛程式的 nuget.exe 探索問題- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="466e4-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="466e4-126">外掛程式: 絕對不會讀取快取檔案[#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="466e4-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="466e4-127">外掛程式「工作已取消。」</span><span class="sxs-lookup"><span data-stu-id="466e4-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="466e4-128">還原期間驗證外掛程式的錯誤- [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="466e4-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="466e4-129">在 linux 平臺上的外掛程式快取無法再發現- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="466e4-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="466e4-130">LockFile: 有了 ATF, 因為目標 framework 相等檢查不正確, 所以它有 false NU1004- [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="466e4-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="466e4-131">LockFile: 如果鎖定檔案是空的或格式不正確, 則不遵守「--鎖定模式」還原旗標- [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="466e4-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="466e4-132">LockFile:不使用封裝中的自訂群組件名稱進行小寫專案鎖定檔案- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="466e4-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="466e4-133">LockFile:在鎖定檔案中讓專案參考小寫- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="466e4-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="466e4-134">還原: 安裝遭篡改的簽署套件會導致多次失敗的安裝嘗試 (具有重複的輸出)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="466e4-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="466e4-135">VS: 在 NuGet 更新之後, 解決方案使用者選項無法還原序列化- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="466e4-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="466e4-136">UnitTest 專案中的 dotnet-list 封裝會傳回錯誤- [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="466e4-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="466e4-137">建立 VS 安裝程式的 NuGet 封裝群組-修正某些 VSIX 安裝問題- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="466e4-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="466e4-138">GeneratePackageOnBuild 不應設定 NoBuild。</span><span class="sxs-lookup"><span data-stu-id="466e4-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="466e4-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="466e4-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="466e4-140">當 nuspec 檔案包含明確的元件參考元素時, 新選項 "-SymbolPackageFormat .snupkg" 會產生錯誤- [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="466e4-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="466e4-141">NuGet. 目標 (498, 5): 錯誤:找不到路徑 '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)的一部分</span><span class="sxs-lookup"><span data-stu-id="466e4-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="466e4-142">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="466e4-142">**DCR:**</span></span>

* <span data-ttu-id="466e4-143">新增 msbuild 屬性, 指出支援 PackageDownload- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="466e4-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="466e4-144">FrameworkReference 透過 FrameworkReference 隱藏相依性流程-PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="466e4-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="466e4-145">在封裝外部提供執行時間 json 的機制- [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="466e4-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="466e4-146">**[此版本-5.2 RTM 中已修正的所有問題清單](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="466e4-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


