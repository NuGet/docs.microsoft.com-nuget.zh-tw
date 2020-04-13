---
title: NuGet 4.5 RTM 版本資訊
description: NuGet 4.5 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496575"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="446f6-103">NuGet 4.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="446f6-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="446f6-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)。</span><span class="sxs-lookup"><span data-stu-id="446f6-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="446f6-105">摘要:4.5.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="446f6-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="446f6-106">摘要:4.5.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="446f6-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="446f6-107">安全修復:在 #/.nuget 中創建的檔案的許可權在[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673)太開放</span><span class="sxs-lookup"><span data-stu-id="446f6-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="446f6-108">摘要:4.5.3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="446f6-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="446f6-109">安全修復:NUPKG 內部的檔可以在 NUPKG 目錄上方具有相對路徑[#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="446f6-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="446f6-110">已知問題</span><span class="sxs-lookup"><span data-stu-id="446f6-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="446f6-111">含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題</span><span class="sxs-lookup"><span data-stu-id="446f6-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="446f6-112">.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。</span><span class="sxs-lookup"><span data-stu-id="446f6-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="446f6-113">[這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。</span><span class="sxs-lookup"><span data-stu-id="446f6-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="446f6-114">您無法使用 NuGet 套件管理員檢視、新增或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="446f6-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="446f6-115">問題</span><span class="sxs-lookup"><span data-stu-id="446f6-115">Issue</span></span>

<span data-ttu-id="446f6-116">NuGet 套件管理員沒有顯示，而且不允許加入/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="446f6-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="446f6-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="446f6-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="446f6-118">因應措施</span><span class="sxs-lookup"><span data-stu-id="446f6-118">Workaround</span></span>

<span data-ttu-id="446f6-119">您必須在專案檔中手動編輯 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="446f6-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="446f6-120">重定目標 Framework 版本可能會導致不完整的 Intellisense</span><span class="sxs-lookup"><span data-stu-id="446f6-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="446f6-121">問題</span><span class="sxs-lookup"><span data-stu-id="446f6-121">Issue</span></span>

<span data-ttu-id="446f6-122">在 Visual Studio 中重定目標 Framework 版本可能會導致不完整的 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="446f6-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="446f6-123">當您使用 PackageReferences 作為套件管理員格式時，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="446f6-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="446f6-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="446f6-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="446f6-125">因應措施</span><span class="sxs-lookup"><span data-stu-id="446f6-125">Workaround</span></span>

<span data-ttu-id="446f6-126">請執行手動還原。</span><span class="sxs-lookup"><span data-stu-id="446f6-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="446f6-127">.NET Core 專案中的套件如包含具有無效簽章的組件，可能會觸發無限的還原迴圈。</span><span class="sxs-lookup"><span data-stu-id="446f6-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="446f6-128">問題</span><span class="sxs-lookup"><span data-stu-id="446f6-128">Issue</span></span>

<span data-ttu-id="446f6-129">有時候，當您使用的套件包含具有無效簽章的組件時，或套件版本使用 'DateTime' 指示器設定時，會導致套件自動還原為在無限迴圈中執行 [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)。</span><span class="sxs-lookup"><span data-stu-id="446f6-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="446f6-130">因應措施</span><span class="sxs-lookup"><span data-stu-id="446f6-130">Workaround</span></span>

<span data-ttu-id="446f6-131">此問題目前沒有因應措施。</span><span class="sxs-lookup"><span data-stu-id="446f6-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="446f6-132">NuGet 4.5 RTM 時間範圍中已修正的問題</span><span class="sxs-lookup"><span data-stu-id="446f6-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="446f6-133">針對 NuGet 4.4 RTM 中已修正的問題，請參閱 [NuGet 4.4 RTM 版本資訊](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="446f6-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="446f6-134">特性</span><span class="sxs-lookup"><span data-stu-id="446f6-134">Features</span></span>

- <span data-ttu-id="446f6-135">停用自動推送符號套件 - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="446f6-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="446f6-136">Bug</span><span class="sxs-lookup"><span data-stu-id="446f6-136">Bugs</span></span>

- <span data-ttu-id="446f6-137">15.5p1 中的 [迴歸]：跳過 Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="446f6-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="446f6-138">還原後遺失套件中的資產 - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="446f6-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="446f6-139">外掛程式認證提供者不會使用包含空格的 URI - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="446f6-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="446f6-140">如果無法還原套件，則即使開啟最少詳細資訊，還是應該在輸出中列印錯誤 - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="446f6-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="446f6-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="446f6-141">dotnet</span></span>
  - <span data-ttu-id="446f6-142">方案層級的 dotnetcore restore 未遵循 ProjectReference 和 ReferenceOutputAssembly，而錯誤導致隨機組建失敗 - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="446f6-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="446f6-143">使用物件方法，PMC 中的自動完成無法正確運作 - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="446f6-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="446f6-144">Visual Studio 2015 工具組的 nuget.exe 還原失敗 - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="446f6-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="446f6-145">perf - pmc 在 vs2017 中具現化極為耗費資源 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="446f6-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="446f6-146">慢速以取得慢速連線的相依性資訊 - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="446f6-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="446f6-147">uninstall-package w/ 如果多個套件共用通用相依性，則 -RemoveDependencies 會失敗 - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="446f6-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="446f6-148">完成 NuGet.Core.nupkg 以進行發行 - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="446f6-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="446f6-149">將 -IncludeProjectReferences 用於 csproj + project.json 時，NuGet 套件會從目錄名稱解析相依性識別碼 - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="446f6-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="446f6-150">'NuGet.ProxyCache' 的類型初始設定式已擲出例外狀況 - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="446f6-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="446f6-151">Kudu 的 Nuget 還原效能問題 - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="446f6-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="446f6-152">搜尋早於註冊 Blob 時，UI 用戶端無法顯示任何錯誤或警告 - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="446f6-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="446f6-153">Get-Packages -更新產生不正確的查詢 - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="446f6-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="446f6-154">4.5 RTM 中已修正之 GitHub 問題的連結</span><span class="sxs-lookup"><span data-stu-id="446f6-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="446f6-155">問題清單</span><span class="sxs-lookup"><span data-stu-id="446f6-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
