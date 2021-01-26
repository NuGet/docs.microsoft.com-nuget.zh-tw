---
title: NuGet 5.8 版本資訊
description: NuGet 5.8 的版本資訊，包括新功能、bug 修正及 Dcr。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 550971d77ed4b15129fdc58fef95e0cceda8d8d1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776173"
---
# <a name="nuget-58-release-notes"></a><span data-ttu-id="25c0e-103">NuGet 5.8 版本資訊</span><span class="sxs-lookup"><span data-stu-id="25c0e-103">NuGet 5.8 Release Notes</span></span>

<span data-ttu-id="25c0e-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="25c0e-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="25c0e-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="25c0e-105">NuGet version</span></span> | <span data-ttu-id="25c0e-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="25c0e-106">Available in Visual Studio version</span></span> | <span data-ttu-id="25c0e-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="25c0e-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="25c0e-108">**5.8**</span><span class="sxs-lookup"><span data-stu-id="25c0e-108">**5.8**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="25c0e-109">Visual Studio 2019 16.8 版</span><span class="sxs-lookup"><span data-stu-id="25c0e-109">Visual Studio 2019 version 16.8</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="25c0e-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="25c0e-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="25c0e-111">**5.8.1**</span><span class="sxs-lookup"><span data-stu-id="25c0e-111">**5.8.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="25c0e-112">Visual Studio 2019 版本16.8。4</span><span class="sxs-lookup"><span data-stu-id="25c0e-112">Visual Studio 2019 version 16.8.4</span></span>](https://visualstudio.microsoft.com/downloads/) | |

<span data-ttu-id="25c0e-113"><sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="25c0e-113"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="25c0e-114">Visual Studio 16.8、MSBuild 16.8 和 .NET 5.0 需要 NuGet.exe 5.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="25c0e-114">Visual Studio 16.8, MSBuild 16.8, and .NET 5.0 require NuGet.exe 5.8 or later.</span></span>


## <a name="summary-whats-new-in-58"></a><span data-ttu-id="25c0e-115">摘要：5.8 中的新功能</span><span class="sxs-lookup"><span data-stu-id="25c0e-115">Summary: What's New in 5.8</span></span>
<span data-ttu-id="25c0e-116">🎉 **這是為以 .net 5.0 為目標的 NuGet 套件提供完整撰寫和還原支援的第一個版本** 🎉</span><span class="sxs-lookup"><span data-stu-id="25c0e-116">🎉 **This is the first release to offer full authoring and restoring support for NuGet packages targeting .NET 5.0** 🎉</span></span>

* <span data-ttu-id="25c0e-117">使用 mmap/CreateFileMapping 加速 nupkg 的解壓縮- [#9807](https://github.com/NuGet/Home/issues/9807)</span><span class="sxs-lookup"><span data-stu-id="25c0e-117">Speed up nupkg extraction using mmap/CreateFileMapping - [#9807](https://github.com/NuGet/Home/issues/9807)</span></span>

* <span data-ttu-id="25c0e-118">在封裝管理員 UI 套件詳細資料窗格中顯示套件弱點詳細資料- [#9850](https://github.com/NuGet/Home/issues/9850)</span><span class="sxs-lookup"><span data-stu-id="25c0e-118">Display package vulnerability details in the Package Manager UI package details pane - [#9850](https://github.com/NuGet/Home/issues/9850)</span></span>

* <span data-ttu-id="25c0e-119">使用新的命令來確認已簽署的 NuGet 套件 [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) - [#8051](https://github.com/NuGet/Home/issues/8051)</span><span class="sxs-lookup"><span data-stu-id="25c0e-119">Verify signed NuGet packages with the new [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) command - [#8051](https://github.com/NuGet/Home/issues/8051)</span></span>

* <span data-ttu-id="25c0e-120">[`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) 支援 `--prerelease` 新增套件最新版本的選項，包括發行前版本- [#4699](https://github.com/NuGet/Home/issues/4699)</span><span class="sxs-lookup"><span data-stu-id="25c0e-120">[`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) supports `--prerelease` option to add the latest version of a package, including prerelease versions - [#4699](https://github.com/NuGet/Home/issues/4699)</span></span>

* <span data-ttu-id="25c0e-121">使用 [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) 命令[#9704](https://github.com/NuGet/Home/issues/9704)在 CLI 中搜尋套件</span><span class="sxs-lookup"><span data-stu-id="25c0e-121">Search for packages in the CLI with [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) command - [#9704](https://github.com/NuGet/Home/issues/9704)</span></span>

* <span data-ttu-id="25c0e-122">[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 命令支援 `--verbosity` 選項 [#9600](https://github.com/NuGet/Home/issues/9600)</span><span class="sxs-lookup"><span data-stu-id="25c0e-122">[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command supports `--verbosity` option - [#9600](https://github.com/NuGet/Home/issues/9600)</span></span>

* <span data-ttu-id="25c0e-123">在 Visual Studio [#9565](https://github.com/NuGet/Home/issues/9565)中，為 .csproj 樣式的 PackageReference 專案啟用快速 No-Op 還原優化</span><span class="sxs-lookup"><span data-stu-id="25c0e-123">Enable fast No-Op restore optimization for csproj-style, PackageReference-based projects in Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)</span></span>

* <span data-ttu-id="25c0e-124">解決方案層級封裝管理員 UI 作業，例如封裝安裝和更新的速度高達10倍- [#6010](https://github.com/NuGet/Home/issues/6010)</span><span class="sxs-lookup"><span data-stu-id="25c0e-124">Solution level Package Manager UI operations such as package installs and updates are up to 10x faster - [#6010](https://github.com/NuGet/Home/issues/6010)</span></span>

* <span data-ttu-id="25c0e-125">Visual Studio [#9982](https://github.com/NuGet/Home/issues/9982)、 [#9984](https://github.com/NuGet/Home/issues/9984)、 [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)中的數個其他 NuGet 效能改進</span><span class="sxs-lookup"><span data-stu-id="25c0e-125">Several other NuGet performance improvements in Visual Studio - [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)</span></span>


### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="25c0e-126">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="25c0e-126">Issues fixed in this release</span></span>

<span data-ttu-id="25c0e-127">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="25c0e-127">**DCRs:**</span></span>

* <span data-ttu-id="25c0e-128">.NET 5.0 TFM： Framework 優先順序規則- [#9436](https://github.com/NuGet/Home/issues/9436)</span><span class="sxs-lookup"><span data-stu-id="25c0e-128">.NET 5.0 TFM: Framework Precedence Rules - [#9436](https://github.com/NuGet/Home/issues/9436)</span></span>

* <span data-ttu-id="25c0e-129">剖析 TargetFramework 時，NuGet 不應推中斷點平臺版本- [#9842](https://github.com/NuGet/Home/issues/9842)</span><span class="sxs-lookup"><span data-stu-id="25c0e-129">NuGet should not infer dots platform version when parsing TargetFramework - [#9842](https://github.com/NuGet/Home/issues/9842)</span></span>

* <span data-ttu-id="25c0e-130">使用 TargetFrameworkMoniker & TargetPlatformMoniker 來推斷架構，而不是使用個別 TFI、TFV、TPI、TPV 屬性- [#9895](https://github.com/NuGet/Home/issues/9895)</span><span class="sxs-lookup"><span data-stu-id="25c0e-130">Use TargetFrameworkMoniker & TargetPlatformMoniker to infer the frameworks instead of using individual TFI, TFV, TPI, TPV properties - [#9895](https://github.com/NuGet/Home/issues/9895)</span></span>

* <span data-ttu-id="25c0e-131">更新 `GetReferenceNearestTargetFrameworkTask()` 以支援具有平臺 (的目標 framework，例如 net 5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span><span class="sxs-lookup"><span data-stu-id="25c0e-131">Update `GetReferenceNearestTargetFrameworkTask()` to support target frameworks with platforms (such as net5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span></span>

* <span data-ttu-id="25c0e-132">.NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)</span><span class="sxs-lookup"><span data-stu-id="25c0e-132">.NET 5.0 Visual Studio APIs - [#9650](https://github.com/NuGet/Home/issues/9650)</span></span>

* <span data-ttu-id="25c0e-133">封裝管理員 UI：合併或更新套件作業不應封鎖，因為 (封裝降級等錯誤 ) ） [#9224](https://github.com/NuGet/Home/issues/9224)</span><span class="sxs-lookup"><span data-stu-id="25c0e-133">Package Manager UI: Consolidate or Update packages operations should not be blocked due to errors (Package Downgrade, etc.) - [#9224](https://github.com/NuGet/Home/issues/9224)</span></span>

* <span data-ttu-id="25c0e-134">具有此功能的專案應該亮亮 NuGet 功能;"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)</span><span class="sxs-lookup"><span data-stu-id="25c0e-134">NuGet features should light up for projects that have the capability; "PackageReferences" - [#9957](https://github.com/NuGet/Home/issues/9957)</span></span>

* <span data-ttu-id="25c0e-135">在 Visual Studio [#6384](https://github.com/NuGet/Home/issues/6384)中隱藏 No-Op 還原訊息</span><span class="sxs-lookup"><span data-stu-id="25c0e-135">Suppress No-Op Restore messages in Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)</span></span>

<span data-ttu-id="25c0e-136">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="25c0e-136">**Bugs:**</span></span>

* <span data-ttu-id="25c0e-137">在背景執行緒上不應呼叫 OutputWindowTextWriter 的函式- [#9764](https://github.com/NuGet/Home/issues/9764)</span><span class="sxs-lookup"><span data-stu-id="25c0e-137">OutputWindowTextWriter constructor should not be called on background thread - [#9764](https://github.com/NuGet/Home/issues/9764)</span></span>

* <span data-ttu-id="25c0e-138">在 Big Endian Cpu 上還原已簽署的套件- [#9547](https://github.com/NuGet/Home/issues/9547)</span><span class="sxs-lookup"><span data-stu-id="25c0e-138">Restore signed packages on Big Endian CPUs - [#9547](https://github.com/NuGet/Home/issues/9547)</span></span>

* <span data-ttu-id="25c0e-139">OutputConsoleLogger 不應在 MEF 函式中呼叫相似化為方法- [#9591](https://github.com/NuGet/Home/issues/9591)</span><span class="sxs-lookup"><span data-stu-id="25c0e-139">OutputConsoleLogger should not call affinitized methods in MEF constructors - [#9591](https://github.com/NuGet/Home/issues/9591)</span></span>

* <span data-ttu-id="25c0e-140">Nuget.exe 中的 Bug-命令列 `PrintJustified()` 方法- [#9737](https://github.com/NuGet/Home/issues/9737)</span><span class="sxs-lookup"><span data-stu-id="25c0e-140">Bug in NuGet.CommandLine.Console `PrintJustified()` method - [#9737](https://github.com/NuGet/Home/issues/9737)</span></span>

* <span data-ttu-id="25c0e-141">當套件中繼資料因為系結錯誤而被垃圾收集時，封裝管理員 UI 記憶體流失 [#9757](https://github.com/NuGet/Home/issues/9757)</span><span class="sxs-lookup"><span data-stu-id="25c0e-141">Package Manager UI memory leak when package metadata is garbage collected due to a bad binding - [#9757](https://github.com/NuGet/Home/issues/9757)</span></span>

* <span data-ttu-id="25c0e-142">簽名使用封裝管理員 UI 中的 packages.config 格式安裝簽署套件時，不會在錯誤清單中顯示任何警告- [#9798](https://github.com/NuGet/Home/issues/9798)</span><span class="sxs-lookup"><span data-stu-id="25c0e-142">[Signing] No warning is showed in Error List when installing a signed package with packages.config format in Package Manager UI - [#9798](https://github.com/NuGet/Home/issues/9798)</span></span>

* <span data-ttu-id="25c0e-143">XPlat 不應該有公用 Api- [#9821](https://github.com/NuGet/Home/issues/9821)</span><span class="sxs-lookup"><span data-stu-id="25c0e-143">NuGet.CommandLine.XPlat should not have public APIs - [#9821](https://github.com/NuGet/Home/issues/9821)</span></span>

* <span data-ttu-id="25c0e-144">藉由封鎖具有 #9822 的執行緒集區執行緒，來減少解決方案載入時間所造成的資源爭用 `BlockingCollection.Take()`  -  [](https://github.com/NuGet/Home/issues/9822)</span><span class="sxs-lookup"><span data-stu-id="25c0e-144">Reduce resource contention at Solution Load time caused by blocking a threaded-pool thread with `BlockingCollection.Take()` - [#9822](https://github.com/NuGet/Home/issues/9822)</span></span>

* <span data-ttu-id="25c0e-145">在命令列還原中，使用多目標專案時，NuGet 應從內部組建讀取目標 framework 相關資訊- [#9869](https://github.com/NuGet/Home/issues/9869)</span><span class="sxs-lookup"><span data-stu-id="25c0e-145">In command line restore, with multi targeted projects, NuGet should read the target framework related information from the inner build - [#9869](https://github.com/NuGet/Home/issues/9869)</span></span>

* <span data-ttu-id="25c0e-146">透過 TargetFrameworkInformation 專案讀取執行時間識別碼圖形- [#9874](https://github.com/NuGet/Home/issues/9874)</span><span class="sxs-lookup"><span data-stu-id="25c0e-146">Read Runtime Identifier graph through TargetFrameworkInformation item - [#9874](https://github.com/NuGet/Home/issues/9874)</span></span>

* <span data-ttu-id="25c0e-147">相較于 Visual Studio 和一般 MSBuild 評估還原，靜態圖形還原與 CrossTargeting 屬性不一致- [#9881](https://github.com/NuGet/Home/issues/9881)</span><span class="sxs-lookup"><span data-stu-id="25c0e-147">Static graph restore is inconsistent with regards to CrossTargeting property in compared to Visual Studio and regular MSBuild evaluation restore - [#9881](https://github.com/NuGet/Home/issues/9881)</span></span>

* <span data-ttu-id="25c0e-148">在靜態圖形還原中，有多個目標專案時，NuGet 應該從內部組建讀取目標 framework 相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="25c0e-148">In static graph restore, with multi targeted projects, NuGet should read the target framework related information from the inner build.</span></span><span data-ttu-id="25c0e-149"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span><span class="sxs-lookup"><span data-stu-id="25c0e-149"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span></span>

* <span data-ttu-id="25c0e-150">允許 `net5.0-platform` 在 Visual Studio 中載入和還原專案 [#9863](https://github.com/NuGet/Home/issues/9863)</span><span class="sxs-lookup"><span data-stu-id="25c0e-150">Allow `net5.0-platform` projects to be loaded and restored in Visual Studio - [#9863](https://github.com/NuGet/Home/issues/9863)</span></span>

* <span data-ttu-id="25c0e-151">在封裝管理員 UI 中顯示已解決的版本- [#9826](https://github.com/NuGet/Home/issues/9826)</span><span class="sxs-lookup"><span data-stu-id="25c0e-151">Display the resolved version in the Package Manager UI - [#9826](https://github.com/NuGet/Home/issues/9826)</span></span>

* <span data-ttu-id="25c0e-152">封裝管理員 UI：方案總管不會顯示所有 NuGet 套件相依性- [#9898](https://github.com/NuGet/Home/issues/9898)</span><span class="sxs-lookup"><span data-stu-id="25c0e-152">Package Manager UI: Solution Explorer is not showing all NuGet package dependencies - [#9898](https://github.com/NuGet/Home/issues/9898)</span></span>

* <span data-ttu-id="25c0e-153">更新 SPDX 授權清單- [#9946](https://github.com/NuGet/Home/issues/9946)</span><span class="sxs-lookup"><span data-stu-id="25c0e-153">Update the SPDX license list - [#9946](https://github.com/NuGet/Home/issues/9946)</span></span>

* <span data-ttu-id="25c0e-154">開啟管理 NuGet 套件之後的 VS 2019 損毀：圖示會導致映射 conversio 中未處理的例外狀況- [#9696](https://github.com/NuGet/Home/issues/9696)</span><span class="sxs-lookup"><span data-stu-id="25c0e-154">VS 2019 crashes after opening Manage NuGet Packages: icon causes unhandled exception in image conversio - [#9696](https://github.com/NuGet/Home/issues/9696)</span></span>

* <span data-ttu-id="25c0e-155">NuGet。解壓縮需要 ilmerge，以排除 Newtonsoft.Js內部 [#9966](https://github.com/NuGet/Home/issues/9966)</span><span class="sxs-lookup"><span data-stu-id="25c0e-155">NuGet.Packaging.Extraction needs ilmerge to exclude Newtonsoft.Json - [#9966](https://github.com/NuGet/Home/issues/9966)</span></span>

* <span data-ttu-id="25c0e-156">沒有錯誤時，ContinuePackingAfterGeneratingNuspec = false 的封裝不應失敗- [#9786](https://github.com/NuGet/Home/issues/9786)</span><span class="sxs-lookup"><span data-stu-id="25c0e-156">Packing with ContinuePackingAfterGeneratingNuspec=false should not fail when there are no errors - [#9786](https://github.com/NuGet/Home/issues/9786)</span></span>

* <span data-ttu-id="25c0e-157">封裝管理員 UI：圖示未正確地反轉色彩- [#10017](https://github.com/NuGet/Home/issues/10017)</span><span class="sxs-lookup"><span data-stu-id="25c0e-157">Package Manager UI: Icons aren't inverting colors properly - [#10017](https://github.com/NuGet/Home/issues/10017)</span></span>

* <span data-ttu-id="25c0e-158">在還原時，最新和 No-Op 專案的專案計數不正確- [#10026](https://github.com/NuGet/Home/issues/10026)</span><span class="sxs-lookup"><span data-stu-id="25c0e-158">Incorrect project counts for Up-To-Date and No-Op projects at Restore - [#10026](https://github.com/NuGet/Home/issues/10026)</span></span>

* <span data-ttu-id="25c0e-159">使用 `/p:RestoreUseStaticGraphEvaluation=true` 值的結果不可以是 Null- [#9280](https://github.com/NuGet/Home/issues/9280)</span><span class="sxs-lookup"><span data-stu-id="25c0e-159">Using `/p:RestoreUseStaticGraphEvaluation=true` Results in Value Cannot Be Null - [#9280](https://github.com/NuGet/Home/issues/9280)</span></span>

* <span data-ttu-id="25c0e-160">`dotnet pack` 錯誤地使用 WPF 程式庫專案的別名- [#10020](https://github.com/NuGet/Home/issues/10020)</span><span class="sxs-lookup"><span data-stu-id="25c0e-160">`dotnet pack` mistakenly uses alias for WPF Library projects - [#10020](https://github.com/NuGet/Home/issues/10020)</span></span>

* <span data-ttu-id="25c0e-161">封裝管理員 UI：簽章驗證失敗時的 NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)</span><span class="sxs-lookup"><span data-stu-id="25c0e-161">Package Manager UI: NullReferenceException when signature validation fails - [#10042](https://github.com/NuGet/Home/issues/10042)</span></span>

* <span data-ttu-id="25c0e-162">Codespaces：不使用 `object` 類型的專案中繼資料值- [#10055](https://github.com/NuGet/Home/issues/10055)</span><span class="sxs-lookup"><span data-stu-id="25c0e-162">Codespaces: do not use `object` type for project metadata values  - [#10055](https://github.com/NuGet/Home/issues/10055)</span></span>

* <span data-ttu-id="25c0e-163">Codespaces：在 [工具選項] 中儲存套件來源將會覆寫認證- [#9711](https://github.com/NuGet/Home/issues/9711)</span><span class="sxs-lookup"><span data-stu-id="25c0e-163">Codespaces: saving package sources in tools options will overwrite credentials - [#9711](https://github.com/NuGet/Home/issues/9711)</span></span>


<span data-ttu-id="25c0e-164">**[此版本修正的所有問題清單-5。8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span><span class="sxs-lookup"><span data-stu-id="25c0e-164">**[List of all issues fixed in this release - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span></span>

<span data-ttu-id="25c0e-165">**[此版本的問題清單-5。8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span><span class="sxs-lookup"><span data-stu-id="25c0e-165">**[List of issues in this release - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="25c0e-166">社群投稿</span><span class="sxs-lookup"><span data-stu-id="25c0e-166">Community contributions</span></span>

<span data-ttu-id="25c0e-167">感謝所有協助讓此 NuGet 版本絕佳的參與者！</span><span class="sxs-lookup"><span data-stu-id="25c0e-167">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="25c0e-168">人員</span><span class="sxs-lookup"><span data-stu-id="25c0e-168">Who</span></span>|<span data-ttu-id="25c0e-169">Pr</span><span class="sxs-lookup"><span data-stu-id="25c0e-169">PRs</span></span>|<span data-ttu-id="25c0e-170">問題</span><span class="sxs-lookup"><span data-stu-id="25c0e-170">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="25c0e-171">omajid</span><span class="sxs-lookup"><span data-stu-id="25c0e-171">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="25c0e-172">3437</span><span class="sxs-lookup"><span data-stu-id="25c0e-172">3437</span></span>](https://github.com/NuGet/NuGet.Client/pull/3437) | <span data-ttu-id="25c0e-173">錯誤訊息中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="25c0e-173">Typo in error message.</span></span> <span data-ttu-id="25c0e-174">"系統管理員身分" 而不是 "administrator"- [#9662](https://github.com/NuGet/Home/issues/9662)</span><span class="sxs-lookup"><span data-stu-id="25c0e-174">"administator" instead of "administrator" - [#9662](https://github.com/NuGet/Home/issues/9662)</span></span>
[<span data-ttu-id="25c0e-175">odalet</span><span class="sxs-lookup"><span data-stu-id="25c0e-175">odalet</span></span>](https://github.com/odalet) | [<span data-ttu-id="25c0e-176">3341</span><span class="sxs-lookup"><span data-stu-id="25c0e-176">3341</span></span>](https://github.com/NuGet/NuGet.Client/pull/3341) | <span data-ttu-id="25c0e-177">具有無效 AssemblyInformationalVersion 報告的 NuGet 套件「需要描述」- [#5548](https://github.com/NuGet/Home/issues/5548)</span><span class="sxs-lookup"><span data-stu-id="25c0e-177">NuGet Pack with invalid AssemblyInformationalVersion reports "description is required" - [#5548](https://github.com/NuGet/Home/issues/5548)</span></span>
[<span data-ttu-id="25c0e-178">campersau</span><span class="sxs-lookup"><span data-stu-id="25c0e-178">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="25c0e-179">3501</span><span class="sxs-lookup"><span data-stu-id="25c0e-179">3501</span></span>](https://github.com/NuGet/NuGet.Client/pull/3501) | <span data-ttu-id="25c0e-180">`RepositoryMetadata.Equals()` 不會考慮分支和認可屬性- [#9613](https://github.com/NuGet/Home/issues/9613)</span><span class="sxs-lookup"><span data-stu-id="25c0e-180">`RepositoryMetadata.Equals()` does not account for Branch and Commit properties - [#9613](https://github.com/NuGet/Home/issues/9613)</span></span>
[<span data-ttu-id="25c0e-181">Youssef1313</span><span class="sxs-lookup"><span data-stu-id="25c0e-181">Youssef1313</span></span>](https://github.com/Youssef1313) | [<span data-ttu-id="25c0e-182">3599</span><span class="sxs-lookup"><span data-stu-id="25c0e-182">3599</span></span>](https://github.com/NuGet/NuGet.Client/pull/3599) | <span data-ttu-id="25c0e-183">若要在 Visual Studio 錯誤清單視窗中按一下 [NU 程式碼]，請移至 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)</span><span class="sxs-lookup"><span data-stu-id="25c0e-183">Clicking NU code in Visual Studio Error List window should go to https://docs.microsoft.com/nuget/reference/errors-and-warnings/ - [#9934](https://github.com/NuGet/Home/issues/9934)</span></span>
[<span data-ttu-id="25c0e-184">ChrisMaddock</span><span class="sxs-lookup"><span data-stu-id="25c0e-184">ChrisMaddock</span></span>](https://github.com/ChrisMaddock) | [<span data-ttu-id="25c0e-185">3624</span><span class="sxs-lookup"><span data-stu-id="25c0e-185">3624</span></span>](https://github.com/NuGet/NuGet.Client/pull/3624) | <span data-ttu-id="25c0e-186">透過 Visual Studio 選項新增套件來源時，請使用 ' HTTPs://'- [#9974](https://github.com/NuGet/Home/issues/9974)</span><span class="sxs-lookup"><span data-stu-id="25c0e-186">Use 'https://' when adding new package source through Visual Studio options - [#9974](https://github.com/NuGet/Home/issues/9974)</span></span>
[<span data-ttu-id="25c0e-187">Therzok</span><span class="sxs-lookup"><span data-stu-id="25c0e-187">Therzok</span></span>](https://github.com/Therzok) | [<span data-ttu-id="25c0e-188">3636</span><span class="sxs-lookup"><span data-stu-id="25c0e-188">3636</span></span>](https://github.com/NuGet/NuGet.Client/pull/3636) | <span data-ttu-id="25c0e-189">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio` Mono 的效能問題- [#9989](https://github.com/NuGet/Home/issues/9989)</span><span class="sxs-lookup"><span data-stu-id="25c0e-189">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio` performance issue on Mono - [#9989](https://github.com/NuGet/Home/issues/9989)</span></span>
[<span data-ttu-id="25c0e-190">thomaslevesque</span><span class="sxs-lookup"><span data-stu-id="25c0e-190">thomaslevesque</span></span>](https://github.com/thomaslevesque) | [<span data-ttu-id="25c0e-191">3442</span><span class="sxs-lookup"><span data-stu-id="25c0e-191">3442</span></span>](https://github.com/NuGet/NuGet.Client/pull/3442) | <span data-ttu-id="25c0e-192">新增 SemanticVersion 類別的 TypeConverter- [#9125](https://github.com/NuGet/Home/issues/9125)</span><span class="sxs-lookup"><span data-stu-id="25c0e-192">Add a TypeConverter for the SemanticVersion class - [#9125](https://github.com/NuGet/Home/issues/9125)</span></span>

## <a name="summary-whats-new-in-581"></a><span data-ttu-id="25c0e-193">摘要：5.8.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="25c0e-193">Summary: What's New in 5.8.1</span></span>

* <span data-ttu-id="25c0e-194">packages.config package.lock.js在5.8 中使用不正確的目標 framework- [#10257](https://github.com/NuGet/Home/issues/10257)</span><span class="sxs-lookup"><span data-stu-id="25c0e-194">packages.config package.lock.json uses an incorrect target framework in 5.8 - [#10257](https://github.com/NuGet/Home/issues/10257)</span></span>

* <span data-ttu-id="25c0e-195">5.8 + 16.8 無法在混合 PackageReference 和 packages.config 時，解析可轉移的專案相依性 [#10326](https://github.com/NuGet/Home/issues/10326)</span><span class="sxs-lookup"><span data-stu-id="25c0e-195">5.8 + 16.8 Cannot resolve transitive project dependencies when mixing PackageReference and packages.config - [#10326](https://github.com/NuGet/Home/issues/10326)</span></span>

<span data-ttu-id="25c0e-196">**[此版本修正的所有問題清單-5.8。1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**</span><span class="sxs-lookup"><span data-stu-id="25c0e-196">**[List of all issues fixed in this release - 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**</span></span>

<span data-ttu-id="25c0e-197">**[此版本中的認可清單-5.8。1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**</span><span class="sxs-lookup"><span data-stu-id="25c0e-197">**[List of commits in this release - 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="25c0e-198">歡迎意見反應</span><span class="sxs-lookup"><span data-stu-id="25c0e-198">Feedback welcome</span></span>

<span data-ttu-id="25c0e-199">您的意見反應對我們非常寶貴。</span><span class="sxs-lookup"><span data-stu-id="25c0e-199">Your feedback is important to us.</span></span>  <span data-ttu-id="25c0e-200">如果此版本有任何問題，請查看我們的 [GitHub 問題](https://github.com/NuGet/Home/issues) ，並 [Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/) 現有的問題。</span><span class="sxs-lookup"><span data-stu-id="25c0e-200">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="25c0e-201">針對 NuGet 內的新問題，請報告 [GitHub 問題](https://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="25c0e-201">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="25c0e-202">如需一般的 NuGet 體驗問題，請透過 [說明] 下您最愛的 IDE 中的 [回報 [問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ] 選項，讓我們知道 **> 報告問題**。</span><span class="sxs-lookup"><span data-stu-id="25c0e-202">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>