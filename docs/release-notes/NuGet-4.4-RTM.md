---
title: NuGet 4.4 RTM 版本資訊
description: NuGet 4.3 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821664"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="a908c-103">NuGet 4.4 RTM 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a908c-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="a908c-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 NuGet 4.4 RTM。</span><span class="sxs-lookup"><span data-stu-id="a908c-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a908c-105">已知問題</span><span class="sxs-lookup"><span data-stu-id="a908c-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="a908c-106">含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題</span><span class="sxs-lookup"><span data-stu-id="a908c-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="a908c-107">.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。</span><span class="sxs-lookup"><span data-stu-id="a908c-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="a908c-108">[這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。</span><span class="sxs-lookup"><span data-stu-id="a908c-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="a908c-109">使用套件管理員主控台時，'Enter' 鍵可能無法運作</span><span class="sxs-lookup"><span data-stu-id="a908c-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="a908c-110">問題</span><span class="sxs-lookup"><span data-stu-id="a908c-110">Issue</span></span>

<span data-ttu-id="a908c-111">有時候，Enter 鍵無法在套件管理員主控台中運作。</span><span class="sxs-lookup"><span data-stu-id="a908c-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="a908c-112">如果您遇到此問題，請查看本修正的進度，並針對您的重新產生步驟提供任何有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="a908c-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="a908c-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="a908c-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="a908c-114">因應措施</span><span class="sxs-lookup"><span data-stu-id="a908c-114">Workaround</span></span>

<span data-ttu-id="a908c-115">重新啟動 Visual Studio 並在開啟解決方案之前開啟 PMC。</span><span class="sxs-lookup"><span data-stu-id="a908c-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="a908c-116">或者，嘗試刪除 `project.lock.json` 並再次還原。</span><span class="sxs-lookup"><span data-stu-id="a908c-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="a908c-117">您無法使用 NuGet 套件管理員檢視、新增或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="a908c-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="a908c-118">問題</span><span class="sxs-lookup"><span data-stu-id="a908c-118">Issue</span></span>

<span data-ttu-id="a908c-119">NuGet 套件管理員沒有顯示，而且不允許加入/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="a908c-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="a908c-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="a908c-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="a908c-121">因應措施</span><span class="sxs-lookup"><span data-stu-id="a908c-121">Workaround</span></span>

<span data-ttu-id="a908c-122">您必須在專案檔中手動編輯 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="a908c-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="a908c-123">重定目標 Framework 版本可能會導致不完整的 Intellisense</span><span class="sxs-lookup"><span data-stu-id="a908c-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="a908c-124">問題</span><span class="sxs-lookup"><span data-stu-id="a908c-124">Issue</span></span>

<span data-ttu-id="a908c-125">在 Visual Studio 中重定目標 Framework 版本可能會導致不完整的 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="a908c-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="a908c-126">當您使用 PackageReferences 作為套件管理員格式時，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="a908c-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="a908c-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="a908c-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="a908c-128">因應措施</span><span class="sxs-lookup"><span data-stu-id="a908c-128">Workaround</span></span>

<span data-ttu-id="a908c-129">請執行手動還原。</span><span class="sxs-lookup"><span data-stu-id="a908c-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="a908c-130">.NET Core 專案中的套件如包含具有無效簽章的組件，可能會觸發無限的還原迴圈。</span><span class="sxs-lookup"><span data-stu-id="a908c-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="a908c-131">問題</span><span class="sxs-lookup"><span data-stu-id="a908c-131">Issue</span></span>

<span data-ttu-id="a908c-132">有時候，當您使用的套件包含具有無效簽章的組件時，或套件版本使用 'DateTime' 指示器設定時，會導致套件自動還原為在無限迴圈中執行 (dotnet/project-system#1457)。</span><span class="sxs-lookup"><span data-stu-id="a908c-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="a908c-133">因應措施</span><span class="sxs-lookup"><span data-stu-id="a908c-133">Workaround</span></span>

<span data-ttu-id="a908c-134">此問題目前沒有因應措施。</span><span class="sxs-lookup"><span data-stu-id="a908c-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="a908c-135">NuGet 4.4 RTM 時間範圍中已修正的問題</span><span class="sxs-lookup"><span data-stu-id="a908c-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="a908c-136">[NuGet 4.3 RTM 版本資訊](../release-notes/nuget-4.3-RTM.md) - 列出所有 NuGet 4.3 RTM 修正的問題</span><span class="sxs-lookup"><span data-stu-id="a908c-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="a908c-137">功能</span><span class="sxs-lookup"><span data-stu-id="a908c-137">Features</span></span>

- <span data-ttu-id="a908c-138">PMC 和 NuGet PM UI 案例中的輕量型解決方案載入支援 - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="a908c-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="a908c-139">msbuild 封裝目標在其前面應該有執行使用者目標的公用勾點 - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="a908c-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="a908c-140">功能：將 dependencyVersion 參數新增至 nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="a908c-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="a908c-141">uap10.0.TODO.0 應該對應至 .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="a908c-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="a908c-142">使用 msbuild /t:restore 支援 Visual Studio Build Tools SKU - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="a908c-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="a908c-143">在還原期間，如果需要但未安裝 .NET Standard 2.0 的 .NET 4.6.1 支援，則會產生錯誤 - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="a908c-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="a908c-144">套件識別碼前置詞保留用戶端 UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="a908c-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="a908c-145">提供當地語系化 Nuget 元件以支援 dotnet.exe 當地語系化 - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="a908c-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="a908c-146">Bug</span><span class="sxs-lookup"><span data-stu-id="a908c-146">Bugs</span></span>

- <span data-ttu-id="a908c-147">不同的專案路徑轉換可能會導致還原遺失 PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="a908c-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="a908c-148">將含警告號碼的錯誤碼移至錯誤範圍 - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="a908c-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="a908c-149">當 .NET Standard 版本不知道是否與目標架構相容時發生誤導錯誤 - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="a908c-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="a908c-150">含混淆授權的測試檔案 - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="a908c-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="a908c-151">EndToEnd 測試範本中遺漏授權標頭 - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="a908c-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="a908c-152">packages.config restore 將錯誤顯示為 NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="a908c-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="a908c-153">nuget.exe install 在 mono 上應該有 DisableParallelProcessing - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="a908c-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="a908c-154">nuget.exe install 不正確地停用快取 - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="a908c-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="a908c-155">VS 停用還原時針對 packages.config 執行 restore 命令會顯示不正確的訊息 - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="a908c-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="a908c-156">VS；停用還原時執行 restore 命令會顯示混淆的訊息 - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="a908c-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="a908c-157">GetRestoreDotnetCliToolsTask 在遺失版本中繼資料時失敗 - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="a908c-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="a908c-158">dotnet</span><span class="sxs-lookup"><span data-stu-id="a908c-158">dotnet</span></span>
  - <span data-ttu-id="a908c-159">dotnetcore add package 可以清除 csproj 中的空行  - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="a908c-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="a908c-160">NuGet.Config 中認證設定的來源名稱區分大小寫 - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="a908c-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="a908c-161">啟用 GeneratePackageOnBuild 已刪除我的整個套件歷程記錄 - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="a908c-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="a908c-162">還原無法還原 mono.cecil 或 semver 套件，但會還原所有其他套件。</span><span class="sxs-lookup"><span data-stu-id="a908c-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="a908c-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="a908c-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="a908c-164">錯誤和警告 - 來源無法使用時發生嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="a908c-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="a908c-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="a908c-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="a908c-166">[DesignConsistency] NuGet 安裝狀態文字目前在暗色調佈景主題上看起來不正確。</span><span class="sxs-lookup"><span data-stu-id="a908c-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="a908c-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="a908c-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="a908c-168">在所有專案的方案更新/安裝時更新套件 - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="a908c-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="a908c-169">dotnet</span><span class="sxs-lookup"><span data-stu-id="a908c-169">dotnet</span></span>
  - <span data-ttu-id="a908c-170">dotnetcore pack 的行為會根據 TargetFramework 與 TargetFrameworks 而不同 - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="a908c-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="a908c-171">工具資料夾內所含的 DLL 擲回警告 - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="a908c-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="a908c-172">NuGet.ContentModel 使用太多記憶體來執行字串作業 - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="a908c-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="a908c-173">OSX 的 RuntimeEnvironmentHelper.IsLinux 傳回 true - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="a908c-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="a908c-174">'dotnet pack' 會將 nuspec 放在 obj 下方，而不是 obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="a908c-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="a908c-175">Nuget 的套件升級極為緩慢 - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="a908c-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="a908c-176">CPS 與具有尚未開啟 LSL (輕量型解決方案還原) 的大型方案的還原不同步 - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="a908c-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="a908c-177">SemVer 2.0 - 含所提供版本的 Nuget 封裝會忽略中繼資料 (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="a908c-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="a908c-178">含版本號碼和 ExcludeVersion 旗標的 Nuget.exe (3.+) 安裝套件不會將套件更新為較新版本 - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="a908c-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="a908c-179">Project.json restore 應該會在最上層套件違反條件約束時發出警告 - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="a908c-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="a908c-180">-ConfigFile 未在 install 命令上設定自訂組態 - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="a908c-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="a908c-181">nuget.exe install 不接受 '-DisableParallelProcessing' 參數 - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="a908c-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="a908c-182">DotNet.exe 或 msbuild.exe 仍然會使用已停用來源 - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="a908c-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="a908c-183">修正 LSL 案例中的當機 - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="a908c-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="a908c-184">DCR</span><span class="sxs-lookup"><span data-stu-id="a908c-184">DCRs</span></span>

- <span data-ttu-id="a908c-185">nuget.exe install TargetFramework 支援 - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="a908c-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="a908c-186">新增不同 msbuild 工作 UserAgent 字串 (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="a908c-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="a908c-187">PackagePathResolver.GetPackageDirectoryName 應該是虛擬的 - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="a908c-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="a908c-188">[DesignConsistency] 新增 NuGet 套件時發生混淆的訊息 - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="a908c-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="a908c-189">[警告和錯誤] NoWarn 不會以可轉移方式流過 P2P 參考 - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="a908c-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="a908c-190">輕量型解決方案載入：PM UI、PMC 和 IV 的通用核心 - - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="a908c-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="a908c-191">輕量型解決方案載入：支援 - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="a908c-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="a908c-192">新增 Visual Studio 所觸發的預先還原 MSBuild 目標支援 - [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="a908c-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="a908c-193">將公用目標新增至可使用 BeforeTargets 參考的 NuGet.targets - [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="a908c-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="a908c-194">封裝目標無法使用建置動作正確地建立 contentFiles - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="a908c-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="a908c-195">RestoreOperationLogger.Do 封鎖執行緒集區執行緒 - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="a908c-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="a908c-196">Docs</span><span class="sxs-lookup"><span data-stu-id="a908c-196">Docs</span></span>

- <span data-ttu-id="a908c-197">install 命令 DependencyVersion 和 Framework 旗標的文件 - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="a908c-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="a908c-198">NuGet 警告和錯誤文件更新 - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="a908c-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="a908c-199">4.4 RTM 中已修正之 GitHub 問題的連結</span><span class="sxs-lookup"><span data-stu-id="a908c-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="a908c-200">問題清單 1</span><span class="sxs-lookup"><span data-stu-id="a908c-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="a908c-201">問題清單 2</span><span class="sxs-lookup"><span data-stu-id="a908c-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="a908c-202">問題清單 3</span><span class="sxs-lookup"><span data-stu-id="a908c-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
