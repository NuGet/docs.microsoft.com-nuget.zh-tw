---
title: NuGet 4.7 RTM 版本資訊
description: NuGet 4.7.0 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 2290025d42dcd5704b6b019c17346201fe6a990d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813789"
---
# <a name="nuget-47-release-notes"></a><span data-ttu-id="a7bf9-103">NuGet 4.7 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a7bf9-103">NuGet 4.7 Release Notes</span></span>

<span data-ttu-id="a7bf9-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-470"></a><span data-ttu-id="a7bf9-105">摘要:4.7.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="a7bf9-105">Summary: What's New in 4.7.0</span></span>

* <span data-ttu-id="a7bf9-106">我們已增強套件簽署，以啟用[存放庫簽署套件](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-106">We have augmented package signing to enable [Repository Signed packages](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span></span>

* <span data-ttu-id="a7bf9-107">Visual Studio Version 15.7 引進了一個功能，[讓使用 packages.config 格式的現有專案移轉成改為使用 PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-107">With Visual Studio Version 15.7, we have introduced the capability to [migrate existing projects that use the packages.config format to use PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md) instead.</span></span>

## <a name="summary-whats-new-in-472"></a><span data-ttu-id="a7bf9-108">摘要:4.7.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="a7bf9-108">Summary: What's New in 4.7.2</span></span>

* <span data-ttu-id="a7bf9-109">安全修復:在 #/.nuget 中創建的檔案的許可權在[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673)太開放</span><span class="sxs-lookup"><span data-stu-id="a7bf9-109">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-473"></a><span data-ttu-id="a7bf9-110">摘要:4.7.3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="a7bf9-110">Summary: What's New in 4.7.3</span></span>

* <span data-ttu-id="a7bf9-111">安全修復:NUPKG 內部的檔可以在 NUPKG 目錄上方具有相對路徑[#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-111">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="a7bf9-112">已知問題</span><span class="sxs-lookup"><span data-stu-id="a7bf9-112">Known issues</span></span>

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a><span data-ttu-id="a7bf9-113">滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項</span><span class="sxs-lookup"><span data-stu-id="a7bf9-113">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span>

#### <a name="issue"></a><span data-ttu-id="a7bf9-114">問題</span><span class="sxs-lookup"><span data-stu-id="a7bf9-114">Issue</span></span>

<span data-ttu-id="a7bf9-115">當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-115">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="a7bf9-116">這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-116">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span>

#### <a name="workaround"></a><span data-ttu-id="a7bf9-117">因應措施</span><span class="sxs-lookup"><span data-stu-id="a7bf9-117">Workaround</span></span>

<span data-ttu-id="a7bf9-118">執行以下任何一個 NuGet 動作：</span><span class="sxs-lookup"><span data-stu-id="a7bf9-118">Perform any one of the following NuGet actions:</span></span>
* <span data-ttu-id="a7bf9-119">開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="a7bf9-119">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span>
* <span data-ttu-id="a7bf9-120">開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="a7bf9-120">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span>
* <span data-ttu-id="a7bf9-121">執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="a7bf9-121">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span>
* <span data-ttu-id="a7bf9-122">建置專案也會觸發 NuGet 還原</span><span class="sxs-lookup"><span data-stu-id="a7bf9-122">Build the project which also triggers NuGet restore</span></span>

<span data-ttu-id="a7bf9-123">您現在應該可以看到移轉選項。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-123">You should now be able to see the migration option.</span></span> <span data-ttu-id="a7bf9-124">請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-124">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="a7bf9-125">含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題</span><span class="sxs-lookup"><span data-stu-id="a7bf9-125">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span>

<span data-ttu-id="a7bf9-126">.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-126">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="a7bf9-127">[這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-127">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="a7bf9-128">本版修正的主要問題</span><span class="sxs-lookup"><span data-stu-id="a7bf9-128">Top issues fixed in this release</span></span>

### <a name="bugs"></a><span data-ttu-id="a7bf9-129">Bug</span><span class="sxs-lookup"><span data-stu-id="a7bf9-129">Bugs</span></span>

* <span data-ttu-id="a7bf9-130">NuGet 在 .Net Core 專案系統 (新迴歸) 中會進入死結。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-130">NuGet runs into a deadlock in .Net Core project system (new regression).</span></span><span data-ttu-id="a7bf9-131"> - [#6733](https://github.com/NuGet/Home/issues/6733) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-131"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span></span>
* <span data-ttu-id="a7bf9-132">套件：如果搭配使用 TfmSpecificPackageFile 和萬用字元路徑，將會不正確地建構 PackagePath - [#6726](https://github.com/NuGet/Home/issues/6726) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-132">Pack: PackagePath is constructed incorrectly if TfmSpecificPackageFile is used with globbing paths - [#6726](https://github.com/NuGet/Home/issues/6726)</span></span>
* <span data-ttu-id="a7bf9-133">套件：除非明確地設定 ispackable，否則 Web API 無法建立套件。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-133">Pack: web api project cannot create package unless ispackable is explicitly set.</span></span><span data-ttu-id="a7bf9-134"> - [#6156](https://github.com/NuGet/Home/issues/6156) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-134"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span></span>
* <span data-ttu-id="a7bf9-135">VS UI 和 PMC 花費 30 分鐘查看新的套件 (nuget.exe 可立刻查看) - [#6657](https://github.com/NuGet/Home/issues/6657) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-135">VS UI and PMC take 30min to see new package (nuget.exe sees it right away) - [#6657](https://github.com/NuGet/Home/issues/6657)</span></span>
* <span data-ttu-id="a7bf9-136">簽署：SignatureUtility.GetCertificateChain(...) 不會檢查所有鏈結狀態 - [#6565](https://github.com/NuGet/Home/issues/6565) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-136">Signing:  SignatureUtility.GetCertificateChain(...) does not check all chain statuses - [#6565](https://github.com/NuGet/Home/issues/6565)</span></span>
* <span data-ttu-id="a7bf9-137">簽署：改善 DER GeneralizedTime 處理 - [#6564](https://github.com/NuGet/Home/issues/6564) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-137">Signing:  improve DER GeneralizedTime handling - [#6564](https://github.com/NuGet/Home/issues/6564)</span></span>
* <span data-ttu-id="a7bf9-138">簽署：安裝遭竄改的套件時，VS 不會顯示 NU3002 錯誤 - [#6337](https://github.com/NuGet/Home/issues/6337) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-138">Signing: VS does not show a NU3002 error when installing a tampered package - [#6337](https://github.com/NuGet/Home/issues/6337)</span></span>
* <span data-ttu-id="a7bf9-139">lockFile.GetLibrary 會區分大小寫 - [#6500](https://github.com/NuGet/Home/issues/6500) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-139">lockFile.GetLibrary is case sensitive - [#6500](https://github.com/NuGet/Home/issues/6500)</span></span>
* <span data-ttu-id="a7bf9-140">安裝/更新還原程式碼和還原程式碼路徑不一致 - [#3471](https://github.com/NuGet/Home/issues/3471) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-140">Install/update restore code and Restore code paths are not consistent - [#3471](https://github.com/NuGet/Home/issues/3471)</span></span>
* <span data-ttu-id="a7bf9-141">方案 PackageManager 版本 ComboBox 可以透過鍵盤選取分隔符號 - [#2606](https://github.com/NuGet/Home/issues/2606) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-141">Solution PackageManager Version ComboBox can select separator via keyboard - [#2606](https://github.com/NuGet/Home/issues/2606)</span></span>
* <span data-ttu-id="a7bf9-142">無法載入來源 `https://www.myget.org/F/<id>` 的服務索引 ---> System.Net.Http.HttpRequestException: 回應狀態碼未表示成功: 403 (禁止) - [#2530](https://github.com/NuGet/Home/issues/2530) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-142">Unable to load the service index for source `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Response status code does not indicate success: 403 (Forbidden) - [#2530](https://github.com/NuGet/Home/issues/2530)</span></span>

### <a name="dcrs"></a><span data-ttu-id="a7bf9-143">DCR</span><span class="sxs-lookup"><span data-stu-id="a7bf9-143">DCRs</span></span>

* <span data-ttu-id="a7bf9-144">跨要求發出 X-NuGet-Session-Id 標頭以進行相互關聯 [功能建議] - [#5330](https://github.com/NuGet/Home/issues/5330) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-144">Emit X-NuGet-Session-Id header to correlate across requests [feature proposal] - [#5330](https://github.com/NuGet/Home/issues/5330)</span></span>
* <span data-ttu-id="a7bf9-145">針對在 Visual Studio 中透過 IVs API 執行還原作業時，公開等候執行的方式。</span><span class="sxs-lookup"><span data-stu-id="a7bf9-145">Expose a way to wait on running restore operation running in Visual Studio via IVs apis.</span></span><span data-ttu-id="a7bf9-146"> - [#6029](https://github.com/NuGet/Home/issues/6029) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-146"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span></span>
* <span data-ttu-id="a7bf9-147">NuGet.exe -NoServiceEndpoint 會避免附加服務 URL 尾碼 - [#6586](https://github.com/NuGet/Home/issues/6586) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-147">NuGet.exe -NoServiceEndpoint will avoid appending service url suffix - [#6586](https://github.com/NuGet/Home/issues/6586)</span></span>
* <span data-ttu-id="a7bf9-148">新增認可雜湊至資訊版本 - [#6492](https://github.com/NuGet/Home/issues/6492) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-148">add commit hash to informational version - [#6492](https://github.com/NuGet/Home/issues/6492)</span></span>
* <span data-ttu-id="a7bf9-149">簽署：啟用移除存放庫簽章/副署 - [#6646](https://github.com/NuGet/Home/issues/6646) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-149">Signing:  enable removal of repository signature/countersignature - [#6646](https://github.com/NuGet/Home/issues/6646)</span></span>
* <span data-ttu-id="a7bf9-150">簽署：刪除存放庫簽章/副署的 API - [#6589](https://github.com/NuGet/Home/issues/6589) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-150">Signing:  API for stripping repository signature/countersignature - [#6589](https://github.com/NuGet/Home/issues/6589)</span></span>
* <span data-ttu-id="a7bf9-151">VS 中的記錄來源 - [#6527](https://github.com/NuGet/Home/issues/6527) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-151">Log source information in VS - [#6527](https://github.com/NuGet/Home/issues/6527)</span></span>
* <span data-ttu-id="a7bf9-152">只在 TFM 和 RID 上篩選 /tools，所以設定 XML 可以放在 /tools 資料夾中 - [#6197](https://github.com/NuGet/Home/issues/6197) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-152">Filter /tools on only TFM and RID, so the settings XML can be put in /tools folder - [#6197](https://github.com/NuGet/Home/issues/6197)</span></span>
* <span data-ttu-id="a7bf9-153">當 Pack 命令排除開頭為 . 的檔案時發出警告</span><span class="sxs-lookup"><span data-stu-id="a7bf9-153">Warn when Pack command excludes a file that starts with .</span></span><span data-ttu-id="a7bf9-154">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span><span class="sxs-lookup"><span data-stu-id="a7bf9-154">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span></span>

[<span data-ttu-id="a7bf9-155">本版修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="a7bf9-155">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
