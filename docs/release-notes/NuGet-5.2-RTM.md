---
title: NuGet 5.2 RTM 版本資訊
description: NuGet 5.2 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776209"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="93b1f-103">NuGet 5.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="93b1f-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="93b1f-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="93b1f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="93b1f-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="93b1f-105">NuGet version</span></span> | <span data-ttu-id="93b1f-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="93b1f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="93b1f-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="93b1f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="93b1f-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="93b1f-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="93b1f-109">Visual Studio 2019 16.2 版</span><span class="sxs-lookup"><span data-stu-id="93b1f-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="93b1f-110">[2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="93b1f-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="93b1f-111"><sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="93b1f-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="93b1f-112"><sup>2</sup>可透過 .NET Core 工作負載，以選用的方式安裝 Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="93b1f-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="93b1f-113">摘要：5.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="93b1f-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="93b1f-114">修正因 Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)上的路徑問題而造成不定期 NuGet 作業失敗的嚴重錯誤</span><span class="sxs-lookup"><span data-stu-id="93b1f-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="93b1f-115">在 Visual Studio 中使用 NuGet 套件管理員 UI 流覽套件時，改善了 UI 回應性，特別是針對緩慢的來源- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="93b1f-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="93b1f-116">許多鎖定檔案的可靠性修正 ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) 和驗證外掛程式 ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271](https://github.com/NuGet/Home/issues/8271)、[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)#7845) [ ](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="93b1f-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="93b1f-117">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="93b1f-117">Issues fixed in this release</span></span>

<span data-ttu-id="93b1f-118">**Bug**</span><span class="sxs-lookup"><span data-stu-id="93b1f-118">**Bugs**</span></span>

* <span data-ttu-id="93b1f-119">效能：封裝管理員主控台： UI 延遲更新「預設專案」 combobox 選取的值- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="93b1f-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="93b1f-120">效能： PM UI 中的效能改進- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="93b1f-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="93b1f-121">效能：在 PMC 中讀取預設專案時的 UI 延遲- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="93b1f-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="93b1f-122">效能： [vsfeedback] 本機套件來源的 [NuGet 更新] 索引標籤凍結- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="93b1f-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="93b1f-123">外掛程式：如果外掛程式無法啟動或終止早期[#8300](https://github.com/NuGet/Home/issues/8300) ，NuGet 會等待完整的交握超時</span><span class="sxs-lookup"><span data-stu-id="93b1f-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="93b1f-124">外掛程式：改善外掛程式啟動失敗的診斷- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="93b1f-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="93b1f-125">外掛程式： nuget.exe 探索內建外掛程式的問題- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="93b1f-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="93b1f-126">外掛程式：快取檔案永遠不會讀取 [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="93b1f-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="93b1f-127">外掛程式：「工作已取消」。</span><span class="sxs-lookup"><span data-stu-id="93b1f-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="93b1f-128">還原期間的驗證外掛程式發生錯誤- [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="93b1f-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="93b1f-129">無法在 linux 平臺上間歇性探索外掛程式快取- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="93b1f-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="93b1f-130">LockFile：使用 ATF 時，由於目標 framework 的相等[#8187](https://github.com/NuGet/Home/issues/8187)檢查不正確，所以會有 false NU1004</span><span class="sxs-lookup"><span data-stu-id="93b1f-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="93b1f-131">LockFile：如果鎖定檔案是空的或格式不正確，則不遵守「--鎖定模式」還原旗標- [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="93b1f-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="93b1f-132">LockFile：在封裝中使用自訂群組件名稱的小寫專案會鎖定 file- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="93b1f-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="93b1f-133">LockFile：讓專案參考在鎖定檔案中的小寫- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="93b1f-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="93b1f-134">還原：安裝已遭篡改的已簽署套件會導致多個失敗的安裝嘗試 (有重複的輸出) - [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="93b1f-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="93b1f-135">VS：方案使用者選項無法在 NuGet 更新後還原序列化- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="93b1f-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="93b1f-136">UnitTest 專案中的 dotnet 清單套件會傳回錯誤 [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="93b1f-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="93b1f-137">建立 VS 安裝程式的 NuGet 套件群組-修正某些 VSIX 安裝問題- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="93b1f-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="93b1f-138">GeneratePackageOnBuild 不應設定 NoBuild。</span><span class="sxs-lookup"><span data-stu-id="93b1f-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="93b1f-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="93b1f-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="93b1f-140">當 nuspec 檔案包含明確元件參考元素時，新的選項 "-SymbolPackageFormat .snupkg" 會產生錯誤- [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="93b1f-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="93b1f-141">Nuget.exe (就是498，5) ：錯誤：找不到路徑 '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)的一部分</span><span class="sxs-lookup"><span data-stu-id="93b1f-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="93b1f-142">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="93b1f-142">**DCR:**</span></span>

* <span data-ttu-id="93b1f-143">新增表示支援 PackageDownload 的 msbuild 屬性- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="93b1f-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="93b1f-144">FrameworkReference 透過 FrameworkReference 隱藏相依性流程。 PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="93b1f-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="93b1f-145">在封裝之外提供 runtime.js的機制- [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="93b1f-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="93b1f-146">**[此版本中所有已修正問題的清單-5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="93b1f-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


