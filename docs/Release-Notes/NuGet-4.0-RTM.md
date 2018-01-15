---
title: "NuGet 4.0 RC 版本資訊 | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3
description: "NuGet 4.0 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。"
keywords: "NuGet 4.0 RTM 版本資訊, Bug 修正, 已知問題, 新增功能, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2cdee8b736fa2c651da803be9a10a6114936134a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="40-rtm-release-notes"></a><span data-ttu-id="e0ceb-104">4.0 RTM 版本資訊</span><span class="sxs-lookup"><span data-stu-id="e0ceb-104">4.0 RTM Release Notes</span></span>

<span data-ttu-id="e0ceb-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附於 NuGet 4.0，後者新增 .NET Core 支援、有許多品質修正，以及改善了效能。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="e0ceb-106">此版本也帶來幾項改善，像是支援 PackageReference，以及 MSBuild 目標、背景套件還原等多項 NuGet 命令。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e0ceb-107">已知問題</span><span class="sxs-lookup"><span data-stu-id="e0ceb-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="e0ceb-108">當您有多個專案參考方案中的另一個專案時，NuGet 還原可能會失敗</span><span class="sxs-lookup"><span data-stu-id="e0ceb-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="e0ceb-109">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-109">Issue:</span></span>
<span data-ttu-id="e0ceb-110">如果方案中的專案參考大小寫不同或相對路徑不同的專案，NuGet 還原可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="e0ceb-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="e0ceb-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="e0ceb-112">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-112">Workaround:</span></span>
<span data-ttu-id="e0ceb-113">將所有專案參考的大小寫或相對路徑修正為一致。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="e0ceb-114">使用套件管理員主控台時，'Enter' 鍵可能無法運作</span><span class="sxs-lookup"><span data-stu-id="e0ceb-114">While using Package Manager Console, 'Enter' key may not work</span></span>
#### <a name="issue"></a><span data-ttu-id="e0ceb-115">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-115">Issue:</span></span>
<span data-ttu-id="e0ceb-116">有時候，Enter 鍵無法在套件管理員主控台中運作。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="e0ceb-117">如果您遇到此問題，請查看本修正的進度，並針對您的重新產生步驟提供任何有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="e0ceb-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="e0ceb-119">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-119">Workaround:</span></span>
<span data-ttu-id="e0ceb-120">重新啟動 Visual Studio 並在開啟解決方案之前開啟 PMC。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="e0ceb-121">或者，嘗試刪除 `project.lock.json` 並再次還原。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="e0ceb-122">在 .NET Core 專案中，當您使用的套件包含具有無效簽章的組件時，可能會得到無限還原迴圈</span><span class="sxs-lookup"><span data-stu-id="e0ceb-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>
#### <a name="issue"></a><span data-ttu-id="e0ceb-123">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-123">Issue:</span></span>
<span data-ttu-id="e0ceb-124">有時候，當您使用的套件包含具有無效簽章的組件時，或套件版本使用 'DateTime' 指示器設定時，會導致套件自動還原在無限迴圈中執行。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="e0ceb-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="e0ceb-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="e0ceb-126">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-126">Workaround:</span></span>
<span data-ttu-id="e0ceb-127">此問題目前沒有因應措施。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-127">There is no workaround at this time.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="e0ceb-128">您將無法使用 NuGet 套件管理員檢視、新增或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="e0ceb-128">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>
#### <a name="issue"></a><span data-ttu-id="e0ceb-129">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-129">Issue:</span></span>
<span data-ttu-id="e0ceb-130">NuGet 套件管理員沒有顯示，而且不允許加入/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="e0ceb-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="e0ceb-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

* #### <a name="workaround"></a><span data-ttu-id="e0ceb-132">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-132">Workaround:</span></span>
<span data-ttu-id="e0ceb-133">您必須在專案檔中手動編輯 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="e0ceb-134">當您設定專案的 PackageId 屬性時，NuGet 還原將會失敗</span><span class="sxs-lookup"><span data-stu-id="e0ceb-134">NuGet restore will fail when you set PackageId property for projects</span></span>
#### <a name="issue"></a><span data-ttu-id="e0ceb-135">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-135">Issue:</span></span>
<span data-ttu-id="e0ceb-136">針對 .NET Core 專案，Visual Studio 中的 NuGet 還原不遵守專案的 PackageId 屬性。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="e0ceb-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="e0ceb-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="e0ceb-138">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-138">Workaround:</span></span>
<span data-ttu-id="e0ceb-139">使用命令列執行還原。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="e0ceb-140">當您的專案沒有 'obj' 資料夾時，套件還原可能會失敗</span><span class="sxs-lookup"><span data-stu-id="e0ceb-140">When your project does not have 'obj' folder, package restore may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="e0ceb-141">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-141">Issue:</span></span>
<span data-ttu-id="e0ceb-142">當 'obj' 資料夾已刪除時，Visual Studio 無法還原 PackageReferences。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="e0ceb-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="e0ceb-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="e0ceb-144">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-144">Workaround:</span></span>
<span data-ttu-id="e0ceb-145">手動建立 'obj' 資料夾，應該就能執行還原。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-145">Create 'obj' folder manually and the restore should work.</span></span> 

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="e0ceb-146">在主控台中使用 Update-Package 手動更新套件可能會失敗</span><span class="sxs-lookup"><span data-stu-id="e0ceb-146">Manually updating packages using Update-Package in console may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="e0ceb-147">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-147">Issue:</span></span>
<span data-ttu-id="e0ceb-148">對於剛轉換的 PackageReferences 專案，在主控台中手動使用 Update-Package 僅一次有效。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="e0ceb-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="e0ceb-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="e0ceb-150">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-150">Workaround:</span></span>
<span data-ttu-id="e0ceb-151">此問題目前沒有因應措施。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="e0ceb-152">重定目標 Framework 版本可能會導致不完整的 Intellisense</span><span class="sxs-lookup"><span data-stu-id="e0ceb-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>
#### <a name="issue"></a><span data-ttu-id="e0ceb-153">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-153">Issue:</span></span>
<span data-ttu-id="e0ceb-154">在 Visual Studio 中重定目標 Framework 版本可能會導致不完整的 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="e0ceb-155">當您使用 PackageReferences 作為套件管理員格式時，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="e0ceb-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="e0ceb-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="e0ceb-157">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-157">Workaround:</span></span>
<span data-ttu-id="e0ceb-158">請執行手動還原。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="e0ceb-159">當以 .NET461 為目標的專案參考另一個以 .NETStandard 為目標的專案時，`msbuild /t:restore` 就會失敗</span><span class="sxs-lookup"><span data-stu-id="e0ceb-159">`msbuild /t:restore` fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="e0ceb-160">問題：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-160">Issue:</span></span>
<span data-ttu-id="e0ceb-161">當以 .NET461 為目標的 PackageReferenece 型專案參考另一個以 .NETStandard 為目標的 PackageReference 型專案時，msbuild /t:restore 就會失敗。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="e0ceb-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="e0ceb-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="e0ceb-163">因應措施：</span><span class="sxs-lookup"><span data-stu-id="e0ceb-163">Workaround:</span></span>
<span data-ttu-id="e0ceb-164">此問題目前沒有因應措施。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="e0ceb-165">NuGet 4.0 RTM 時間範圍中已修正的問題</span><span class="sxs-lookup"><span data-stu-id="e0ceb-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="e0ceb-166">[NuGet 4.0 RC 版本資訊](../release-notes/nuget-4.0-RC.md) - 列出所有 NuGet 4.0 RC 修正的問題</span><span class="sxs-lookup"><span data-stu-id="e0ceb-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

<span data-ttu-id="e0ceb-167">**ug：**</span><span class="sxs-lookup"><span data-stu-id="e0ceb-167">**Bug:**</span></span>

* <span data-ttu-id="e0ceb-168">Visual Studio 中的 NuGet 還原不遵守專案的 PackageId 屬性 - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-168">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

* <span data-ttu-id="e0ceb-169">在 vsix 套件中新增套件時，發生 NuGet ProjectSystemCache 錯誤 - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-169">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

* <span data-ttu-id="e0ceb-170">如果在有多個 TFM 的專案中使用 IncludeSource，套件會擲回例外狀況 - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-170">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

* <span data-ttu-id="e0ceb-171">VS 2017 RC3 在使用全解決方案套件管理更新時當機 - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-171">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

* <span data-ttu-id="e0ceb-172">無法解除安裝新安裝的套件 - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-172">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

* <span data-ttu-id="e0ceb-173">移轉至 PackageRef 時，混合式解決方案有奇怪的還原行為 - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-173">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

* <span data-ttu-id="e0ceb-174">一開始 NuGet 作業 (安裝、更新、還原) 即建置，將會導致 VS 停止回應 - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-174">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

* <span data-ttu-id="e0ceb-175">UI 停止回應 - 鎖死初始化 NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-175">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

* <span data-ttu-id="e0ceb-176">新增套件命令應該會將版本新增為屬性，而不是項目 - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-176">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

* <span data-ttu-id="e0ceb-177">Dotnet 還原 foo.sln - SLN 中的組態造成還原圖形出現重複 (不是 diff config) 的專案時會失敗 - [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-177">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

* <span data-ttu-id="e0ceb-178">僅套件內容 - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-178">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

* <span data-ttu-id="e0ceb-179">根據預設，選擇不使用套件格式選取器選項 - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-179">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

* <span data-ttu-id="e0ceb-180">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span><span class="sxs-lookup"><span data-stu-id="e0ceb-180">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="e0ceb-181">基準 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-181">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

* <span data-ttu-id="e0ceb-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span><span class="sxs-lookup"><span data-stu-id="e0ceb-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="e0ceb-183">基準 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-183">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

* <span data-ttu-id="e0ceb-184">在多重 TFM 專案中提名失敗 -[#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-184">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

* <span data-ttu-id="e0ceb-185">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span><span class="sxs-lookup"><span data-stu-id="e0ceb-185">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="e0ceb-186">基準 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-186">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

* <span data-ttu-id="e0ceb-187">vsfeedback - 以 netcoreapp1.1 為目標時發生套件警告 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-187">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

* <span data-ttu-id="e0ceb-188">嘗試在空的 ASP.NET Core Web 應用程式中新增 NuGet 套件時發生 PathTooLongException - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-188">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

* <span data-ttu-id="e0ceb-189">套件執行太頻繁 -- 與目標「套件」有關的目標相依性圖形中有循環相依性時，dotnet 套件會失敗 - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-189">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

* <span data-ttu-id="e0ceb-190">套件執行太頻繁 -- 產生的 NuGet 套件不包含所有組態 - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-190">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

* <span data-ttu-id="e0ceb-191">在 C++ 專案中，NullReferenceException 新增 Nuget 與 packageref - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-191">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

* <span data-ttu-id="e0ceb-192">協助工具：朗讀程式不讀出核取方塊來選取要安裝套件的專案 - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-192">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

* <span data-ttu-id="e0ceb-193">NuGet VS17 偶爾無法連線至 VSO/VSTS 摘要 - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-193">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

* <span data-ttu-id="e0ceb-194">如果 PackagePath 指定路徑為 "contentFiles"contentFiles，會取得錯誤位置的輸出 - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-194">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

* <span data-ttu-id="e0ceb-195">套件目標附加有 VersionSuffix 的 PackageVersion 屬性 - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-195">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

* <span data-ttu-id="e0ceb-196">指定套件路徑對 dotnet 套件無效 - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-196">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

* <span data-ttu-id="e0ceb-197">NuGet 在還原期間輸出一堆重複匯入的警告 - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-197">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

* <span data-ttu-id="e0ceb-198">在暗色調佈景主題下選擇不正確的 [NuGet 套件管理員格式] 對話方塊 - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-198">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

* <span data-ttu-id="e0ceb-199">還原組建時發生 VS 損毀 - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-199">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

* <span data-ttu-id="e0ceb-200">如果將 TFM 新增至 targetframeworks、儲存，然後建置，Visual Studio 就會鎖死。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-200">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="e0ceb-201">10% 的時間 - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-201">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

* <span data-ttu-id="e0ceb-202">成功封裝專案時，NuGet 套件不會輸出成功訊息 - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-202">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

* <span data-ttu-id="e0ceb-203">PackTask 失敗，因為找不到 System.IO.Compression 4.1 - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-203">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

* <span data-ttu-id="e0ceb-204">套件執行太頻繁 - PackTask 經常因檔案存取衝突而失敗 - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-204">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

* <span data-ttu-id="e0ceb-205">NuGet 在背景還原期間開啟輸出視窗 - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-205">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

* <span data-ttu-id="e0ceb-206">將 ServiceProvider 視為危險的程式碼撰寫模式予以排除 (這可能會造成停止回應) - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-206">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

* <span data-ttu-id="e0ceb-207">Perf/UIHang - 改善 DownloadTimeoutStream 讀取 - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-207">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

* <span data-ttu-id="e0ceb-208">如果在 NuGet 還原完成前企圖關閉專案，Visual Studio 會鎖死 - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-208">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

* <span data-ttu-id="e0ceb-209">PackTask 與封裝 `.nuspec` 的問題 - [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-209">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

* <span data-ttu-id="e0ceb-210">[vsfeedback] 無法對新專案解析 NuGet 套件 (需要重新啟動 Visual Studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-210">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

* <span data-ttu-id="e0ceb-211">[vsfeedback] 顯示可用套件版本的 [版本] 下拉式清單，不斷與所選的 NuGet 套件保持同步 - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-211">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

* <span data-ttu-id="e0ceb-212">與 CPS 互動以防止發生鎖死時，Nuget.Client 應該使用 CPS JoinableTaskFactory - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-212">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

* <span data-ttu-id="e0ceb-213">NuGet 3.5.0 不從套件解除封裝 `.targets` - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-213">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

* <span data-ttu-id="e0ceb-214">dotnet 套件不支援 `.csproj` 中的標題 - [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-214">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

* <span data-ttu-id="e0ceb-215">Install-Package 會導致 VS2017 RC 的錯誤對話方塊 - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-215">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

* <span data-ttu-id="e0ceb-216">更新 .net core 專案的套件似乎無效，因為 UI 不會從提名取得 CPS 更新。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-216">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="e0ceb-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

* <span data-ttu-id="e0ceb-218">改善未解決的參考警告 - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-218">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

* <span data-ttu-id="e0ceb-219">dotnet 套件 - ProjectReference 遺失版本資訊 - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-219">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

* <span data-ttu-id="e0ceb-220">建立 UWP 應用程式會建立專案並重建已耗用時間總和迴歸 - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-220">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

* <span data-ttu-id="e0ceb-221">還原期間即使發生錯誤仍會顯示成功還原訊息。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-221">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="e0ceb-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

* <span data-ttu-id="e0ceb-223">將 Nuget.CommandLine 3.4.4 重新發佈至 Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-223">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

* <span data-ttu-id="e0ceb-224">在移轉時，專案從 `project.json` 變更至 `.csproj` --- 還原失敗 - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-224">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

* <span data-ttu-id="e0ceb-225">新建立的 xunit 測試專案還原失敗 - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-225">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

* <span data-ttu-id="e0ceb-226">核心專案可以在開啟時停止回應、鎖死 UI - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-226">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

* <span data-ttu-id="e0ceb-227">修正組建工作的目標檔案 - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-227">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

* <span data-ttu-id="e0ceb-228">組建卸載已參考專案的解決方案後，錯誤清單發生錯誤 - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-228">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

* <span data-ttu-id="e0ceb-229">MSB4057：專案中沒有目標 "_GenerateRestoreGraphProjectEntry"。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-229">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="e0ceb-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

* <span data-ttu-id="e0ceb-231">vsfeedback：當您選取所有專案時，解決方案的 Nuget 管理員 UI 當機 - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-231">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

* <span data-ttu-id="e0ceb-232">沒有尾端斜線時 nuget.exe msbuildpath 失敗 - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-232">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

* <span data-ttu-id="e0ceb-233">vsfeedback：NuGet 還原提供數個 LinqToTwitter 專案的專案參考警告 - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-233">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

* <span data-ttu-id="e0ceb-234">`.csproj` 的套件不包含 minClientVersion 屬性 - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-234">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

* <span data-ttu-id="e0ceb-235">VS2017 中簽署的 NuGet.Build.Tasks.Pack.dll 運送延遲 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-235">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

* <span data-ttu-id="e0ceb-236">VSFeedback：無法還原以 CMake 3.7.1 產生的 VS 2015 專案 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-236">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

* <span data-ttu-id="e0ceb-237">VSFeedback：還原錯誤可能會混淆組建可能提供的更多完整錯誤訊息 - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-237">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

* <span data-ttu-id="e0ceb-238">[VSFeedback] 還原網站專案的 NuGet 套件時發生錯誤：值不可為 Null。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-238">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="e0ceb-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

* <span data-ttu-id="e0ceb-240">在 NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker 中移轉會擲回「物件參考例外狀況」 - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-240">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

* <span data-ttu-id="e0ceb-241">dotnet 套件應該以建置套件所用的版本來封裝工具 - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-241">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

* <span data-ttu-id="e0ceb-242">新的背景還原在狀態列寫入毫秒，但還原時間以秒計 - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-242">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

* <span data-ttu-id="e0ceb-243">因為錯字無法解析所有的專案參考 - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-243">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

* <span data-ttu-id="e0ceb-244">在套件參考案例中啟用 PCM 工作流程 - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-244">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

* <span data-ttu-id="e0ceb-245">套件管理員 UI 中找不到已安裝的套件 - [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-245">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

* <span data-ttu-id="e0ceb-246">當 PackagePath 為空時，dotnet 套件會失敗 - [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-246">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

* <span data-ttu-id="e0ceb-247">多使用者案例中的還原工作失敗 - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-247">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

* <span data-ttu-id="e0ceb-248">使用 NuGet 套件工作進行封裝時，無法變更內容類型 - [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-248">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

* <span data-ttu-id="e0ceb-249">MsBuild /t:pack 的預設複本 ContentFiles 不正確 - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-249">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

* <span data-ttu-id="e0ceb-250">安裝套件還原記錄兩次還原套件訊息 - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-250">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

* <span data-ttu-id="e0ceb-251">移除 [執行階段] 區段的 [Guardrails - Restore] \(防撞欄 - 還原) 僅適用於目前的專案 - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-251">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

* <span data-ttu-id="e0ceb-252">套件工作會將內容檔放在 'content/' 和 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-252">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

* <span data-ttu-id="e0ceb-253">dotnet pack3 會額外標記分割 - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-253">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

* <span data-ttu-id="e0ceb-254">dotnet pack：以套件參考封裝專案會造成匯入警告重複出現 - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-254">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

* <span data-ttu-id="e0ceb-255">VS 中的還原記錄不一定顯示 - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-255">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

* <span data-ttu-id="e0ceb-256">Nuget 區域變數說明文字仍然提及套件快取 - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-256">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

* <span data-ttu-id="e0ceb-257">Restore3 結合 PackageReferences 與 TargetFrameworks。</span><span class="sxs-lookup"><span data-stu-id="e0ceb-257">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="e0ceb-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

* <span data-ttu-id="e0ceb-259">Nuget 在 VS "15" Preview 4 dev. 中挑選了非預期的 MSBuild 版本</span><span class="sxs-lookup"><span data-stu-id="e0ceb-259">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="e0ceb-260">命令提示字元 - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-260">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

* <span data-ttu-id="e0ceb-261">在失敗的還原上寫出目標/props 檔案 - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-261">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

* <span data-ttu-id="e0ceb-262">在 VS 15 命令提示字元中執行時，NuGet 在還原期間不遵守與 MSBuild 相同的相容性填充碼 - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-262">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

* <span data-ttu-id="e0ceb-263">重新啟用 VS15 的 PackFromProjectWithDevelopmentDependencySet - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-263">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

* <span data-ttu-id="e0ceb-264">NuGet 的 Blend 問題 - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-264">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

* <span data-ttu-id="e0ceb-265">將 4.0.0.2067 整合到 CLI 和 SDK 的存放庫以隨附 RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-265">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

* <span data-ttu-id="e0ceb-266">當您建立新的核心主控台應用程式、關閉解決方案、開啟解決方案和關閉解決方案時，VS 停止回應 - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-266">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

* <span data-ttu-id="e0ceb-267">針對 d15prerel.25916.01 叫用停止回應開啟專案 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-267">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

* <span data-ttu-id="e0ceb-268">修正 dotnet/nuget.exe 區域變數 doc/help 訊息 - [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-268">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

* <span data-ttu-id="e0ceb-269">檢查 PackTask 的開頭或結尾空格問題 - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-269">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

* <span data-ttu-id="e0ceb-270">dotnet 套件是從 obj 壓縮，不是 bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-270">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

* <span data-ttu-id="e0ceb-271">dotnet 套件似乎一律將 ProjectReference 版本設定為 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-271">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

* <span data-ttu-id="e0ceb-272">dotnet 套件因專案參考和 <TargetFramework> 而失敗 - [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-272">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

* <span data-ttu-id="e0ceb-273">ProjectSystemCache.TryGetProjectNameByShortName 中的 LockRecursionException - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-273">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

* <span data-ttu-id="e0ceb-274">修剪 MSBuild 屬性的空白字元 - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-274">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

* <span data-ttu-id="e0ceb-275">合併專案載入時引發的兩個專案事件 - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-275">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

* <span data-ttu-id="e0ceb-276">`project.assets.json` 檔案中的 P2P 程式庫版本不正確 - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-276">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

* <span data-ttu-id="e0ceb-277">還原損毀，因為沒有會回應的摘要，也無法使用套件 - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-277">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

* <span data-ttu-id="e0ceb-278">發生大量 MSBuild 錯誤輸出時，nuget.exe 可能停止回應 - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-278">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

* <span data-ttu-id="e0ceb-279">Blend 的建置時還原第一次失敗，第二次成功 (VS 案例已修正) - [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-279">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

<span data-ttu-id="e0ceb-280">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="e0ceb-280">**DCR:**</span></span>

* <span data-ttu-id="e0ceb-281">將 vsix 從 v2 vsix 移轉至 v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-281">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

* <span data-ttu-id="e0ceb-282">NuGet 應有取得 MSBuild 之鎖定檔案路徑的機制 - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-282">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

* <span data-ttu-id="e0ceb-283">將組建資產新增至 TFM 相容性檢查和資產檔案 - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-283">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

* <span data-ttu-id="e0ceb-284">定義套件目標中的新 ProjectCapability「套件」以啟用套件的相關功能 - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-284">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

* <span data-ttu-id="e0ceb-285">根據 "GeneratePackageOnBuild" MSBuild 屬性的條件，將套件 執行為後組建目標 - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-285">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

* <span data-ttu-id="e0ceb-286">使用 NuGet 屬性 RestoreProjectStyle 建立特定的 NuGet 專案 - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-286">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

* <span data-ttu-id="e0ceb-287">可轉移的專案參考變更為調整還原 - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-287">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

* <span data-ttu-id="e0ceb-288">在非 UWP 專案的目標檔案中新增 NuGet 屬性 - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-288">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

* <span data-ttu-id="e0ceb-289">UWP TargetPlatformVersion 支援 - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-289">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

* <span data-ttu-id="e0ceb-290">進行專案參考中繼資料和 NuGet 專案系統的通訊 - [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-290">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

* <span data-ttu-id="e0ceb-291">將 UI 新增至封裝模式 - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-291">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

* <span data-ttu-id="e0ceb-292">舊版的 `.csproj` 需要在 proj/目標中設定 NugetTargetMoniker 和 RuntimeIdentifiers - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-292">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

* <span data-ttu-id="e0ceb-293">安裝套件可能會與自動還原重疊 - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-293">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

* <span data-ttu-id="e0ceb-294">未載入 VSPackage 時不會發生操作功能表 QueryStatus - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-294">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

* <span data-ttu-id="e0ceb-295">解決方案還原和組建還原仍會顯示對話方塊 - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-295">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

* <span data-ttu-id="e0ceb-296">隔離 NuGet.Clients 解決方案組建中的 VSSDK 版本 - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-296">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

<span data-ttu-id="e0ceb-297">**功能**</span><span class="sxs-lookup"><span data-stu-id="e0ceb-297">**Feature:**</span></span>

* <span data-ttu-id="e0ceb-298">NuGet.Core.sln 中的當地語系化字串 - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-298">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

* <span data-ttu-id="e0ceb-299">Nuget 強制以 LSL 模式載入 Web 應用程式專案 - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-299">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

* <span data-ttu-id="e0ceb-300">AutoReferenced PackageReference 支援封鎖「已安裝 SDK」套件 UI 中的版本變更 - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-300">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

* <span data-ttu-id="e0ceb-301">正確進行任何專案相依性的 PackageSpec.Version 通訊 - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-301">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

* <span data-ttu-id="e0ceb-302">支援從命令列將參考移入 `.csproj` - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-302">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

* <span data-ttu-id="e0ceb-303">支援還原 PackageReference 專案 (一般和 xplat) 以及輕量型解決方案負載 - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-303">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

* <span data-ttu-id="e0ceb-304">支援從命令列將參考新增至 `.csproj` - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-304">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

* <span data-ttu-id="e0ceb-305">支援 `packages.config` 或 `project.json` 的輕量型解決方案負載 NuGet 還原 - [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-305">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

* <span data-ttu-id="e0ceb-306">Nuget 產生之目標檔案中的 contentFiles 支援 - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-306">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

* <span data-ttu-id="e0ceb-307">使用 MSBuild 在 Mac 上建立 nuget.exe 驗證的 Mono CI - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-307">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

* <span data-ttu-id="e0ceb-308">移開 v2 NuGet.Core 相依性的 NuGet - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="e0ceb-308">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>


## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="e0ceb-309">RTM 中已修正的 GitHub 問題連結</span><span class="sxs-lookup"><span data-stu-id="e0ceb-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="e0ceb-310">問題清單 1</span><span class="sxs-lookup"><span data-stu-id="e0ceb-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="e0ceb-311">問題清單 2</span><span class="sxs-lookup"><span data-stu-id="e0ceb-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="e0ceb-312">問題清單 3</span><span class="sxs-lookup"><span data-stu-id="e0ceb-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="e0ceb-313">問題清單 4</span><span class="sxs-lookup"><span data-stu-id="e0ceb-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="e0ceb-314">問題清單 5</span><span class="sxs-lookup"><span data-stu-id="e0ceb-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")

