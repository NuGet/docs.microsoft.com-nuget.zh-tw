---
title: NuGet 4.7 RTM 版本資訊
description: NuGet 4.7.0 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f23cc2973fa6370d9b7513d415fd8151b822c104
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2018
---
# <a name="nuget-47-rtm-release-notes"></a><span data-ttu-id="6ebec-103">NuGet 4.7 RTM 版本資訊</span><span class="sxs-lookup"><span data-stu-id="6ebec-103">NuGet 4.7 RTM Release Notes</span></span>

<span data-ttu-id="6ebec-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)。</span><span class="sxs-lookup"><span data-stu-id="6ebec-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-this-release"></a><span data-ttu-id="6ebec-105">摘要：此版本的新功能</span><span class="sxs-lookup"><span data-stu-id="6ebec-105">Summary: What's New in this Release</span></span>

* <span data-ttu-id="6ebec-106">我們已增強套件簽署，以啟用[存放庫簽署套件](https://github.com/NuGet/Home/wiki/Repository-Signatures) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-106">We have augemented package signing to enable [Repository Signed packages](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span></span>

* <span data-ttu-id="6ebec-107">Visual Studio Version 15.7 引進了一個功能，[讓使用 packages.config 格式的現有專案移轉成改為使用 PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference)。</span><span class="sxs-lookup"><span data-stu-id="6ebec-107">With Visual Studio Version 15.7, we have introduced the capability to [migrate existing projects that use the packages.config format to use PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) instead.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6ebec-108">已知問題</span><span class="sxs-lookup"><span data-stu-id="6ebec-108">Known issues</span></span>

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a><span data-ttu-id="6ebec-109">滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項</span><span class="sxs-lookup"><span data-stu-id="6ebec-109">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span>

#### <a name="issue"></a><span data-ttu-id="6ebec-110">問題</span><span class="sxs-lookup"><span data-stu-id="6ebec-110">Issue</span></span>

<span data-ttu-id="6ebec-111">當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。</span><span class="sxs-lookup"><span data-stu-id="6ebec-111">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="6ebec-112">這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。</span><span class="sxs-lookup"><span data-stu-id="6ebec-112">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span>

#### <a name="workaround"></a><span data-ttu-id="6ebec-113">因應措施</span><span class="sxs-lookup"><span data-stu-id="6ebec-113">Workaround</span></span>

<span data-ttu-id="6ebec-114">執行以下任何一個 NuGet 動作：</span><span class="sxs-lookup"><span data-stu-id="6ebec-114">Peform any one of the following NuGet actions:</span></span>
* <span data-ttu-id="6ebec-115">開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="6ebec-115">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span>
* <span data-ttu-id="6ebec-116">開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="6ebec-116">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span>
* <span data-ttu-id="6ebec-117">執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="6ebec-117">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span>
* <span data-ttu-id="6ebec-118">建置專案也會觸發 NuGet 還原</span><span class="sxs-lookup"><span data-stu-id="6ebec-118">Build the project which also triggers NuGet restore</span></span>

<span data-ttu-id="6ebec-119">您現在應該可以看到移轉選項。</span><span class="sxs-lookup"><span data-stu-id="6ebec-119">You should now be able to see the migration option.</span></span> <span data-ttu-id="6ebec-120">請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。</span><span class="sxs-lookup"><span data-stu-id="6ebec-120">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="6ebec-121">含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題</span><span class="sxs-lookup"><span data-stu-id="6ebec-121">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span>

<span data-ttu-id="6ebec-122">.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。</span><span class="sxs-lookup"><span data-stu-id="6ebec-122">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="6ebec-123">[這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。</span><span class="sxs-lookup"><span data-stu-id="6ebec-123">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="6ebec-124">本版修正的主要問題</span><span class="sxs-lookup"><span data-stu-id="6ebec-124">Top issues fixed in this release</span></span>

### <a name="bugs"></a><span data-ttu-id="6ebec-125">Bug</span><span class="sxs-lookup"><span data-stu-id="6ebec-125">Bugs</span></span>

* <span data-ttu-id="6ebec-126">NuGet 在 .Net Core 專案系統 (新迴歸) 中會進入死結。</span><span class="sxs-lookup"><span data-stu-id="6ebec-126">NuGet runs into a deadlock in .Net Core project system (new regression).</span></span><span data-ttu-id="6ebec-127"> - [#6733](https://github.com/NuGet/Home/issues/6733) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-127"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span></span>
* <span data-ttu-id="6ebec-128">套件：如果搭配使用 TfmSpecificPackageFile 和萬用字元路徑，將會不正確地建構 PackagePath - [#6726](https://github.com/NuGet/Home/issues/6726) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-128">Pack: PackagePath is constructed incorrectly if TfmSpecificPackageFile is used with globbing paths - [#6726](https://github.com/NuGet/Home/issues/6726)</span></span>
* <span data-ttu-id="6ebec-129">套件：除非明確地設定 ispackable，否則 Web API 無法建立套件。</span><span class="sxs-lookup"><span data-stu-id="6ebec-129">Pack: web api project cannot create package unless ispackable is explicitly set.</span></span><span data-ttu-id="6ebec-130"> - [#6156](https://github.com/NuGet/Home/issues/6156) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-130"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span></span>
* <span data-ttu-id="6ebec-131">VS UI 和 PMC 花費 30 分鐘查看新的套件 (nuget.exe 可立刻查看) - [#6657](https://github.com/NuGet/Home/issues/6657) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-131">VS UI and PMC take 30min to see new package (nuget.exe sees it right away) - [#6657](https://github.com/NuGet/Home/issues/6657)</span></span>
* <span data-ttu-id="6ebec-132">簽署：SignatureUtility.GetCertificateChain(...) 不會檢查所有鏈結狀態 - [#6565](https://github.com/NuGet/Home/issues/6565) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-132">Signing:  SignatureUtility.GetCertificateChain(...) does not check all chain statuses - [#6565](https://github.com/NuGet/Home/issues/6565)</span></span>
* <span data-ttu-id="6ebec-133">簽署：改善 DER GeneralizedTime 處理 - [#6564](https://github.com/NuGet/Home/issues/6564) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-133">Signing:  improve DER GeneralizedTime handling - [#6564](https://github.com/NuGet/Home/issues/6564)</span></span>
* <span data-ttu-id="6ebec-134">簽署：安裝遭竄改的套件時，VS 不會顯示 NU3002 錯誤 - [#6337](https://github.com/NuGet/Home/issues/6337) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-134">Signing: VS does not show a NU3002 error when installing a tampered package - [#6337](https://github.com/NuGet/Home/issues/6337)</span></span>
* <span data-ttu-id="6ebec-135">lockFile.GetLibrary 會區分大小寫 - [#6500](https://github.com/NuGet/Home/issues/6500) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-135">lockFile.GetLibrary is case sensitive - [#6500](https://github.com/NuGet/Home/issues/6500)</span></span>
* <span data-ttu-id="6ebec-136">安裝/更新還原程式碼和還原程式碼路徑不一致 - [#3471](https://github.com/NuGet/Home/issues/3471) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-136">Install/update restore code and Restore code paths are not consistent - [#3471](https://github.com/NuGet/Home/issues/3471)</span></span>
* <span data-ttu-id="6ebec-137">方案 PackageManager 版本 ComboBox 可以透過鍵盤選取分隔符號 - [#2606](https://github.com/NuGet/Home/issues/2606) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-137">Solution PackageManager Version ComboBox can select separator via keyboard - [#2606](https://github.com/NuGet/Home/issues/2606)</span></span>
* <span data-ttu-id="6ebec-138">無法載入來源 `https://www.myget.org/F/<id>` 的服務索引 ---> System.Net.Http.HttpRequestException: 回應狀態碼未表示成功: 403 (禁止) - [#2530](https://github.com/NuGet/Home/issues/2530) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-138">Unable to load the service index for source `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Response status code does not indicate success: 403 (Forbidden) - [#2530](https://github.com/NuGet/Home/issues/2530)</span></span>

### <a name="dcrs"></a><span data-ttu-id="6ebec-139">DCR</span><span class="sxs-lookup"><span data-stu-id="6ebec-139">DCRs</span></span>

* <span data-ttu-id="6ebec-140">跨要求發出 X-NuGet-Session-Id 標頭以進行相互關聯 [功能建議] - [#5330](https://github.com/NuGet/Home/issues/5330) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-140">Emit X-NuGet-Session-Id header to correlate across requests [feature proposal] - [#5330](https://github.com/NuGet/Home/issues/5330)</span></span>
* <span data-ttu-id="6ebec-141">針對在 Visual Studio 中透過 IVs API 執行還原作業時，公開等候執行的方式。</span><span class="sxs-lookup"><span data-stu-id="6ebec-141">Expose a way to wait on running restore operation running in Visual Studio via IVs apis.</span></span><span data-ttu-id="6ebec-142"> - [#6029](https://github.com/NuGet/Home/issues/6029) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-142"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span></span>
* <span data-ttu-id="6ebec-143">NuGet.exe -NoServiceEndpoint 會避免附加服務 URL 尾碼 - [#6586](https://github.com/NuGet/Home/issues/6586) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-143">NuGet.exe -NoServiceEndpoint will avoid appending service url suffix - [#6586](https://github.com/NuGet/Home/issues/6586)</span></span>
* <span data-ttu-id="6ebec-144">新增認可雜湊至資訊版本 - [#6492](https://github.com/NuGet/Home/issues/6492) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-144">add commit hash to informational version - [#6492](https://github.com/NuGet/Home/issues/6492)</span></span>
* <span data-ttu-id="6ebec-145">簽署：啟用移除存放庫簽章/副署 - [#6646](https://github.com/NuGet/Home/issues/6646) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-145">Signing:  enable removal of repository signature/countersignature - [#6646](https://github.com/NuGet/Home/issues/6646)</span></span>
* <span data-ttu-id="6ebec-146">簽署：刪除存放庫簽章/副署的 API - [#6589](https://github.com/NuGet/Home/issues/6589) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-146">Signing:  API for stripping repository signature/countersignature - [#6589](https://github.com/NuGet/Home/issues/6589)</span></span>
* <span data-ttu-id="6ebec-147">VS 中的記錄來源 - [#6527](https://github.com/NuGet/Home/issues/6527) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-147">Log source information in VS - [#6527](https://github.com/NuGet/Home/issues/6527)</span></span>
* <span data-ttu-id="6ebec-148">只在 TFM 和 RID 上篩選 /tools，所以設定 XML 可以放在 /tools 資料夾中 - [#6197](https://github.com/NuGet/Home/issues/6197) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-148">Filter /tools on only TFM and RID, so the settings XML can be put in /tools folder - [#6197](https://github.com/NuGet/Home/issues/6197)</span></span>
* <span data-ttu-id="6ebec-149">當 Pack 命令排除開頭為 . 的檔案時發出警告</span><span class="sxs-lookup"><span data-stu-id="6ebec-149">Warn when Pack command excludes a file that starts with .</span></span><span data-ttu-id="6ebec-150">  - [#3308](https://github.com/NuGet/Home/issues/3308) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6ebec-150">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span></span>

[<span data-ttu-id="6ebec-151">本版修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="6ebec-151">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
