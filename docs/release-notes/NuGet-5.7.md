---
title: NuGet 5.7 版本資訊
description: NuGet 5.7 的版本資訊，包括新功能、bug 修正及 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508783"
---
# <a name="nuget-57-release-notes"></a><span data-ttu-id="a477d-103">NuGet 5.7 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a477d-103">NuGet 5.7 Release Notes</span></span>

<span data-ttu-id="a477d-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="a477d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a477d-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="a477d-105">NuGet version</span></span> | <span data-ttu-id="a477d-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="a477d-106">Available in Visual Studio version</span></span> | <span data-ttu-id="a477d-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a477d-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="a477d-108">**5.7.0 版**</span><span class="sxs-lookup"><span data-stu-id="a477d-108">**5.7.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a477d-109">Visual Studio 2019 16.7 版</span><span class="sxs-lookup"><span data-stu-id="a477d-109">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a477d-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a477d-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |
| [<span data-ttu-id="a477d-111">**5.7.1**</span><span class="sxs-lookup"><span data-stu-id="a477d-111">**5.7.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a477d-112">Visual Studio 2019 16.7 版</span><span class="sxs-lookup"><span data-stu-id="a477d-112">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a477d-113">[3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a477d-113">[3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="a477d-114"><sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="a477d-114"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-57"></a><span data-ttu-id="a477d-115">摘要：5.7 中的新功能</span><span class="sxs-lookup"><span data-stu-id="a477d-115">Summary: What's New in 5.7</span></span>

### <a name="features-added-in-this-release"></a><span data-ttu-id="a477d-116">此版本中新增的功能</span><span class="sxs-lookup"><span data-stu-id="a477d-116">Features added in this release</span></span>

* <span data-ttu-id="a477d-117">已新增 NuGet 套件參考的外部別名支援- [#4989](https://github.com/NuGet/Home/issues/4989)</span><span class="sxs-lookup"><span data-stu-id="a477d-117">Added extern alias support for NuGet package references - [#4989](https://github.com/NuGet/Home/issues/4989)</span></span>

* <span data-ttu-id="a477d-118">藉由允許它們共用資料來源並減少 resfreshing [#8294](https://github.com/NuGet/Home/issues/8294) ，使已安裝和更新索引標籤之間的切換變得更快</span><span class="sxs-lookup"><span data-stu-id="a477d-118">Made switching between Installed and Updates tabs faster by allowing them to share a data source and reducing resfreshing - [#8294](https://github.com/NuGet/Home/issues/8294)</span></span>

* <span data-ttu-id="a477d-119">藉由呼叫 MSBuild 靜態圖形 api (dotnet.exe) [#9644](https://github.com/NuGet/Home/issues/9644) ，讓還原速度更快。</span><span class="sxs-lookup"><span data-stu-id="a477d-119">Make restore faster - speed up evaluations by calling MSBuild Static Graph apis (dotnet.exe) - [#9644](https://github.com/NuGet/Home/issues/9644)</span></span>

* <span data-ttu-id="a477d-120">已為 PackageReference 專案新增 Visual Studio 部分還原 (無作業 + +) - [#9513](https://github.com/NuGet/Home/issues/9513)</span><span class="sxs-lookup"><span data-stu-id="a477d-120">Added Visual Studio partial restore for PackageReference projects (no-op++) - [#9513](https://github.com/NuGet/Home/issues/9513)</span></span>

* <span data-ttu-id="a477d-121">在搜尋行為不正常的套件來源時，Visual Studio 封裝管理員 UI 的損毀，會傳回超過每個 HTTP 要求所要求的結果數目。</span><span class="sxs-lookup"><span data-stu-id="a477d-121">Visual Studio Package Manager UI will crash less often when searching misbehaving package sources that return more than the requested number of results per HTTP request.</span></span><span data-ttu-id="a477d-122"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span><span class="sxs-lookup"><span data-stu-id="a477d-122"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span></span>

* <span data-ttu-id="a477d-123">在 VS restore- [#9236](https://github.com/NuGet/Home/issues/9236)中加入非 SDK 樣式專案的 PackageVersion 資訊整合</span><span class="sxs-lookup"><span data-stu-id="a477d-123">Added integration of PackageVersion information for non-SDK style projects in VS restore  - [#9236](https://github.com/NuGet/Home/issues/9236)</span></span>

* <span data-ttu-id="a477d-124">已新增 nuget.exe 更新的支援 `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)</span><span class="sxs-lookup"><span data-stu-id="a477d-124">Added support for nuget.exe update `-self -Source` https://feed - [#1783](https://github.com/NuGet/Home/issues/1783)</span></span>

* <span data-ttu-id="a477d-125">在%APPDATA%\NuGet 目錄中新增了多個設定檔的支援- [#9394](https://github.com/NuGet/Home/issues/9394)</span><span class="sxs-lookup"><span data-stu-id="a477d-125">Added support for multiple config files in %APPDATA%\NuGet directory - [#9394](https://github.com/NuGet/Home/issues/9394)</span></span>

* <span data-ttu-id="a477d-126">DeterministicSourcePaths 現在會將 NuGet 來源套件納入帳戶 [#9431](https://github.com/NuGet/Home/issues/9431)</span><span class="sxs-lookup"><span data-stu-id="a477d-126">DeterministicSourcePaths now takes NuGet source packages into account - [#9431](https://github.com/NuGet/Home/issues/9431)</span></span>

* <span data-ttu-id="a477d-127">已新增 INuGetProjectService，GetInstalledPackagesAsync 擴充性 API- [#9702](https://github.com/NuGet/Home/issues/9702)</span><span class="sxs-lookup"><span data-stu-id="a477d-127">Added INuGetProjectService.GetInstalledPackagesAsync extensibility API - [#9702](https://github.com/NuGet/Home/issues/9702)</span></span>

* <span data-ttu-id="a477d-128">已新增 interop API 來列舉回溯資料夾，而不需要方案/專案 [#9395](https://github.com/NuGet/Home/issues/9395)</span><span class="sxs-lookup"><span data-stu-id="a477d-128">Added interop API to enumerate fallback folders without requiring a solution/project - [#9395](https://github.com/NuGet/Home/issues/9395)</span></span>

* <span data-ttu-id="a477d-129">已新增 `latest` `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的選項</span><span class="sxs-lookup"><span data-stu-id="a477d-129">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a477d-130">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="a477d-130">Issues fixed in this release</span></span>

<span data-ttu-id="a477d-131">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="a477d-131">**Bugs:**</span></span>

* <span data-ttu-id="a477d-132">在 dotnet CLI 還原中，啟動認證外掛程式時，如果 `DOTNET_HOST_PATH`  未定義環境變數，請嘗試在系統路徑上使用 DOTNET CLI。</span><span class="sxs-lookup"><span data-stu-id="a477d-132">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="a477d-133"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="a477d-133"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>

* <span data-ttu-id="a477d-134">nuget.exe 規格會產生具有硬式編碼文字的著作權標記，而不是 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="a477d-134">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>

* <span data-ttu-id="a477d-135">NuGet.exe 在元件名稱變更時，會在 .csproj 的封裝期間擲回例外狀況 ' 作者必要項 ' （如果變更元件名稱，則忽略預留位置和 assemblyinfo 屬性[#4234](https://github.com/NuGet/Home/issues/4234) ）</span><span class="sxs-lookup"><span data-stu-id="a477d-135">NuGet.exe throws exception 'authors required' during pack of a csproj ignoring placeholders and assemblyinfo attributes if the assembly name is changed - [#4234](https://github.com/NuGet/Home/issues/4234)</span></span>

* <span data-ttu-id="a477d-136">HttpRequestMessage 會多次重複使用，SocketHttpHandler [#8661](https://github.com/NuGet/Home/issues/8661)不支援</span><span class="sxs-lookup"><span data-stu-id="a477d-136">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>

* <span data-ttu-id="a477d-137">NuGet。 5.6.0 preview 3 和更新版本的索引使用不同的公開金鑰權杖- [#9481](https://github.com/NuGet/Home/issues/9481)</span><span class="sxs-lookup"><span data-stu-id="a477d-137">NuGet.Indexing 5.6.0 preview 3 and later use a different public key token - [#9481](https://github.com/NuGet/Home/issues/9481)</span></span>

* <span data-ttu-id="a477d-138">在建立 NuGet 套件期間接受 TreatWarningsAsErrors- [#7404](https://github.com/NuGet/Home/issues/7404)</span><span class="sxs-lookup"><span data-stu-id="a477d-138">Honor TreatWarningsAsErrors during NuGet Package creation - [#7404](https://github.com/NuGet/Home/issues/7404)</span></span>

* <span data-ttu-id="a477d-139">[CPVM]多個 p2p 專案的假套件降級- [#9549](https://github.com/NuGet/Home/issues/9549)</span><span class="sxs-lookup"><span data-stu-id="a477d-139">[CPVM] Spurious package downgrades for multiple p2p projects  - [#9549](https://github.com/NuGet/Home/issues/9549)</span></span>

* <span data-ttu-id="a477d-140">[流覽] 索引標籤不會靠左對齊搜尋方塊- [#9559](https://github.com/NuGet/Home/issues/9559)</span><span class="sxs-lookup"><span data-stu-id="a477d-140">The “Browse” tab is not aligned left with search box - [#9559](https://github.com/NuGet/Home/issues/9559)</span></span>

* <span data-ttu-id="a477d-141">安裝的版本與解決方案等級 PM UI 中的內嵌圖示不一致，其中一個套件識別碼已安裝多個版本- [#9321](https://github.com/NuGet/Home/issues/9321)</span><span class="sxs-lookup"><span data-stu-id="a477d-141">The installed version is inconsistent with the embedded icon in the solution level PM UI for one package id with multiple versions installed - [#9321](https://github.com/NuGet/Home/issues/9321)</span></span>

* <span data-ttu-id="a477d-142">遺漏： PartCreationPolicy (CreationPolicy。非共用的) SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)</span><span class="sxs-lookup"><span data-stu-id="a477d-142">Leak: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger - [#9595](https://github.com/NuGet/Home/issues/9595)</span></span>

* <span data-ttu-id="a477d-143">避免在無作業還原中讀取資產檔案- [#9693](https://github.com/NuGet/Home/issues/9693)</span><span class="sxs-lookup"><span data-stu-id="a477d-143">Avoid reading the assets file in no-op restores - [#9693](https://github.com/NuGet/Home/issues/9693)</span></span>

* <span data-ttu-id="a477d-144">Nuget.exe 不支援從搜尋[#9086](https://github.com/NuGet/Home/issues/9086)取得版本的下載計數</span><span class="sxs-lookup"><span data-stu-id="a477d-144">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span>

* <span data-ttu-id="a477d-145">藉由減少 JObject 相依性來改善 PackageMetadataResourceV3 的記憶體效能- [#9719](https://github.com/NuGet/Home/issues/9719)</span><span class="sxs-lookup"><span data-stu-id="a477d-145">Improve memory performance of PackageMetadataResourceV3 by reducing the JObject dependencies - [#9719](https://github.com/NuGet/Home/issues/9719)</span></span>

<span data-ttu-id="a477d-146">**設計變更要求：**</span><span class="sxs-lookup"><span data-stu-id="a477d-146">**Design change requests:**</span></span>

* <span data-ttu-id="a477d-147">`<owners>`當元素是多餘的時隱藏元素[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="a477d-147">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>

* <span data-ttu-id="a477d-148">記錄 IntervalTrackers 為 ETW 事件- [#9593](https://github.com/NuGet/Home/issues/9593)</span><span class="sxs-lookup"><span data-stu-id="a477d-148">Log IntervalTrackers as ETW events - [#9593](https://github.com/NuGet/Home/issues/9593)</span></span>

* <span data-ttu-id="a477d-149">在還原時新增了參考用訊息，以通知 CPVM 使用者此功能目前為預覽狀態 [#9340](https://github.com/NuGet/Home/issues/9340)</span><span class="sxs-lookup"><span data-stu-id="a477d-149">Added an informational message on restore to inform CPVM users that the feature is in preview - [#9340](https://github.com/NuGet/Home/issues/9340)</span></span>

* <span data-ttu-id="a477d-150">從資產檔案填入方案總管套件/專案可轉移相依性- [#9580](https://github.com/NuGet/Home/issues/9580)</span><span class="sxs-lookup"><span data-stu-id="a477d-150">Populate Solution Explorer package/project transitive dependencies from assets file - [#9580](https://github.com/NuGet/Home/issues/9580)</span></span>

* <span data-ttu-id="a477d-151">[已安裝的套件] 索引標籤不應將套件清單分頁 [#6995](https://github.com/NuGet/Home/issues/6995)</span><span class="sxs-lookup"><span data-stu-id="a477d-151">Installed packages tab shouldn't paginate the packages list - [#6995](https://github.com/NuGet/Home/issues/6995)</span></span>

<span data-ttu-id="a477d-152">**[此版本修正的所有問題清單-5。7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span><span class="sxs-lookup"><span data-stu-id="a477d-152">**[List of all issues fixed in this release - 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="a477d-153">社群投稿</span><span class="sxs-lookup"><span data-stu-id="a477d-153">Community contributions</span></span>

<span data-ttu-id="a477d-154">感謝所有協助讓此 NuGet 版本絕佳的參與者！</span><span class="sxs-lookup"><span data-stu-id="a477d-154">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="a477d-155">人員</span><span class="sxs-lookup"><span data-stu-id="a477d-155">Who</span></span>|<span data-ttu-id="a477d-156">Pr</span><span class="sxs-lookup"><span data-stu-id="a477d-156">PRs</span></span>|<span data-ttu-id="a477d-157">問題</span><span class="sxs-lookup"><span data-stu-id="a477d-157">Issues</span></span>|
|----|----|----|
|[<span data-ttu-id="a477d-158">campersau</span><span class="sxs-lookup"><span data-stu-id="a477d-158">campersau</span></span>](https://github.com/campersau)|<span data-ttu-id="a477d-159">[3433](https://github.com/NuGet/NuGet.Client/pull/3433)、 [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span><span class="sxs-lookup"><span data-stu-id="a477d-159">[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span></span>|<span data-ttu-id="a477d-160">Nuget.exe 不支援從搜尋[#9086](https://github.com/NuGet/Home/issues/9086)取得版本的下載計數</span><span class="sxs-lookup"><span data-stu-id="a477d-160">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span> </br><span data-ttu-id="a477d-161">HttpRequestMessage 會多次重複使用，SocketHttpHandler [#8661](https://github.com/NuGet/Home/issues/8661)不支援</span><span class="sxs-lookup"><span data-stu-id="a477d-161">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>|
|[<span data-ttu-id="a477d-162">Joseph Musser (jnm2) </span><span class="sxs-lookup"><span data-stu-id="a477d-162">Joseph Musser (jnm2)</span></span>](https://github.com/jnm2)|[<span data-ttu-id="a477d-163">3241</span><span class="sxs-lookup"><span data-stu-id="a477d-163">3241</span></span>](https://github.com/NuGet/NuGet.Client/pull/3241)|<span data-ttu-id="a477d-164">`<owners>`當元素是多餘的時隱藏元素[#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="a477d-164">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>|
|[<span data-ttu-id="a477d-165">Volodymyr Shkolka (BlackGad) </span><span class="sxs-lookup"><span data-stu-id="a477d-165">Volodymyr Shkolka (BlackGad)</span></span>](https://github.com/BlackGad)|[<span data-ttu-id="a477d-166">3273</span><span class="sxs-lookup"><span data-stu-id="a477d-166">3273</span></span>](https://github.com/NuGet/NuGet.Client/pull/3273)|<span data-ttu-id="a477d-167">NuGet 無法從需要用戶端憑證的 HTTPS 來源還原- [#5773](https://github.com/NuGet/Home/issues/5773)</span><span class="sxs-lookup"><span data-stu-id="a477d-167">NuGet cannot restore from HTTPS sources that require Client Certificates - [#5773](https://github.com/NuGet/Home/issues/5773)</span></span>|
|[<span data-ttu-id="a477d-168">Marius Ungureanu (Therzok) </span><span class="sxs-lookup"><span data-stu-id="a477d-168">Marius Ungureanu (Therzok)</span></span>](https://github.com/Therzok)|[<span data-ttu-id="a477d-169">3357</span><span class="sxs-lookup"><span data-stu-id="a477d-169">3357</span></span>](https://github.com/NuGet/NuGet.Client/pull/3357)|<span data-ttu-id="a477d-170">HttpSourceAuthenticationHandler SemaphoreSlim 未來的校對- [#9463](https://github.com/NuGet/Home/issues/9463)</span><span class="sxs-lookup"><span data-stu-id="a477d-170">HttpSourceAuthenticationHandler SemaphoreSlim future proofing - [#9463](https://github.com/NuGet/Home/issues/9463)</span></span>|
|[<span data-ttu-id="a477d-171">Sunner (SuNNjek) </span><span class="sxs-lookup"><span data-stu-id="a477d-171">Sunner (SuNNjek)</span></span>](https://github.com/SuNNjek)|[<span data-ttu-id="a477d-172">3088</span><span class="sxs-lookup"><span data-stu-id="a477d-172">3088</span></span>](https://github.com/NuGet/NuGet.Client/pull/3088)|<span data-ttu-id="a477d-173">nuget.exe 規格會產生具有硬式編碼文字的著作權標記，而不是 `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="a477d-173">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>|
|[<span data-ttu-id="a477d-174">Olivier Spinelli (Olivier-Spinelli) </span><span class="sxs-lookup"><span data-stu-id="a477d-174">Olivier Spinelli (olivier-spinelli)</span></span>](https://github.com/olivier-spinelli)|[<span data-ttu-id="a477d-175">3335</span><span class="sxs-lookup"><span data-stu-id="a477d-175">3335</span></span>](https://github.com/NuGet/NuGet.Client/pull/3335)|<span data-ttu-id="a477d-176">在 dotnet CLI 還原中，啟動認證外掛程式時，如果 `DOTNET_HOST_PATH`  未定義環境變數，請嘗試在系統路徑上使用 DOTNET CLI。</span><span class="sxs-lookup"><span data-stu-id="a477d-176">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="a477d-177"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="a477d-177"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>|
|[<span data-ttu-id="a477d-178">goyzhang</span><span class="sxs-lookup"><span data-stu-id="a477d-178">goyzhang</span></span>](https://github.com/goyzhang)|[<span data-ttu-id="a477d-179">3370</span><span class="sxs-lookup"><span data-stu-id="a477d-179">3370</span></span>](https://github.com/NuGet/NuGet.Client/pull/3370)|<span data-ttu-id="a477d-180">已新增 `latest` `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)的選項</span><span class="sxs-lookup"><span data-stu-id="a477d-180">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>|

## <a name="summary-whats-new-in-571"></a><span data-ttu-id="a477d-181">摘要：5.7.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="a477d-181">Summary: What's New in 5.7.1</span></span>

* <span data-ttu-id="a477d-182">擴充 nupkg 中繼檔以包含安裝來源- [#10354](https://github.com/NuGet/Home/issues/10354)</span><span class="sxs-lookup"><span data-stu-id="a477d-182">Extend the .nupkg.metadata file to include the installation source - [#10354](https://github.com/NuGet/Home/issues/10354)</span></span>

* <span data-ttu-id="a477d-183">記錄檔封裝 contenthash 在) 解壓縮期間的還原記錄 (- [#10384](https://github.com/NuGet/Home/issues/10384)</span><span class="sxs-lookup"><span data-stu-id="a477d-183">Log package contenthash during restore logging (during extraction) - [#10384](https://github.com/NuGet/Home/issues/10384)</span></span>

* <span data-ttu-id="a477d-184">在正常的詳細資訊還原時，記錄要從中還原封裝的來源 [#10461](https://github.com/NuGet/Home/issues/10461)</span><span class="sxs-lookup"><span data-stu-id="a477d-184">When restoring at normal verbosity, log which source a package is being restored from - [#10461](https://github.com/NuGet/Home/issues/10461)</span></span>

<span data-ttu-id="a477d-185">**[此版本中已修正的所有問題清單-5.7。1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**</span><span class="sxs-lookup"><span data-stu-id="a477d-185">**[List of all issues fixed in this release - 5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**</span></span>

<span data-ttu-id="a477d-186">**[此版本中的認可清單-5.7。1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**</span><span class="sxs-lookup"><span data-stu-id="a477d-186">**[List of commits in this release - 5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**</span></span>
