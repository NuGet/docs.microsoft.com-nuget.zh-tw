---
title: NuGet 3.5 Beta 版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.5 版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="b1108-103">NuGet 3.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="b1108-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="b1108-104">[NuGet 3.5 RC 版本資訊](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 版本資訊](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="b1108-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b1108-105">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="b1108-105">Bug Fixes</span></span>

* <span data-ttu-id="b1108-106">組件不會使用 MSBuild 14.1 上 mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="b1108-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="b1108-107">更新索引標籤不會選取最新可用版本，來更新改為選取目前安裝的版本- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="b1108-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="b1108-108">驗證摘要的 MyGet 私用 v2 後按一下 [顯示更多結果 x] 中修正損毀- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="b1108-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="b1108-109">記錄檔訊息看起來是反向順序 ui- [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="b1108-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="b1108-110">v3.4.4-Nuget 還原就會擲回 「 不支援指定的路徑格式 」- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="b1108-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="b1108-111">NuGet cmdLine 3.6 beta 就不會接受-p o p Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="b1108-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="b1108-112">在大型專案-安裝 Nuget IKVM 緩慢[#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="b1108-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="b1108-113">nuget.exe 本身會保留在更新本身的更新[#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="b1108-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="b1108-114">3.5 安裝/還原從 UNC 共用具有 3.4.4-迴歸效能[#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="b1108-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="b1108-115">從封裝管理 UI net451 專案-安裝 Moq 時的錯誤[#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="b1108-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="b1108-116">安裝在解決方案層級的索引標籤不會顯示封裝的版本- [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="b1108-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="b1108-117">xproj`project.json`更新從已安裝 索引標籤將會遺失狀態- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="b1108-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="b1108-118">在 NuGet 套件`.csproj`會忽略空的檔案中的項目`.nuspec`檔案- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="b1108-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="b1108-119">在 IIS 中裝載的網站專案不會導致還原失敗- [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="b1108-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="b1108-120">認證不時，從擷取 Nuget.Config v3 端點重新導向至 v2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="b1108-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="b1108-121">NuGet 套件無法解析組件時擷取可攜式的組件中繼資料- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="b1108-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="b1108-122">找不到 Nuget`msbuild.exe`上 Mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="b1108-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="b1108-123">nuget.exe 組件不允許開頭數字集的發行前版本標記[# 1743年](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="b1108-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="b1108-124">nuget 套件安裝失敗上 VS2015E- [# 1298年](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="b1108-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="b1108-125">allowedVersions 篩選不在方案層級的工作[#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="b1108-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="b1108-126">還原隨機失敗與具有相同的項目已加入索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b1108-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="b1108-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="b1108-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="b1108-128">無法安裝在 Nuget.Common `.csproj`  -  [# 2635年](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="b1108-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="b1108-129">FindPackagesById 時您可以使用 UI 來搜尋 V2 來源，會呼叫兩次的每個識別碼- [# 2517年](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="b1108-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="b1108-130">封裝不能相依於專案- [# 2490年](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="b1108-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="b1108-131">nuget.exe 套件-排除適記載，但不是支援- [# 2284年](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="b1108-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="b1108-132">問題的錯誤訊息 'contentFiles' 區段`.nuspec`無效- [# 1686年](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="b1108-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="b1108-133">推入一律會傳送整個封裝兩次與已驗證的封裝來源- [# 1501年](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="b1108-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="b1108-134">沒有資訊時呼叫 nuget.exe 更新 \*.csproj 專案時沒有指定`packages.config`  -  [# 1496年](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="b1108-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="b1108-135">`packages.config` 還原不會重試在來源 V2-5xx 狀態碼[# 1217年](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="b1108-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="b1108-136">在檔案中的 src 雙點`.nuspec`無法運作- [# 2947年](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="b1108-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="b1108-137">CoreCLR 還原需要略過使用加密-摘要[# 2942年](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="b1108-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="b1108-138">nuget.exe 推送 403 處理-錯誤提示輸入認證- [# 2910年](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="b1108-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="b1108-139">NuGet 更新程式，透過封裝管理員會從內容`project.json`  -  [# 2888年](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="b1108-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="b1108-140">NuGet.PackageManagement.VisualStudio 嘗試載入"NuGet.TeamFoundationServer14"，但是的 DLL 名稱變更為"NuGet.TeamFoundationServer"- [# 2857年](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="b1108-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="b1108-141">封裝管理員 UI 不會顯示新的更新版本- [# 2828年](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="b1108-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="b1108-142">更新封裝嘗試使用 packageid，而不是 package.version-版本[# 2771年](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="b1108-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="b1108-143">如果專案不使用 nuget，nuget 還原 csproj 應該錯誤 (`packages.config`或`project.json`)- [# 2766年](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="b1108-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="b1108-144">TFS 錯誤 「 [檔案] 會在您的工作區中找不到，或您沒有存取權限 」 期間升級或解除安裝方案/專案繫結至 TFS 原始檔控制-時[# 2739年](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="b1108-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="b1108-145">更新套件不會取得非目標的封裝的相依性[# 2724年](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="b1108-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="b1108-146">沒有任何方法來設定記錄檔詳細等級 Nuget 封裝管理員 UI 動作- [# 2705年](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="b1108-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="b1108-147">nuget 組態無效-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="b1108-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="b1108-148">在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 無法運作- [# 2653年](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="b1108-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="b1108-149">nuget 3.4.3 版本取得值不可為 null 上封裝組建- [# 2648年](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="b1108-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="b1108-150">還原並未使用來自 Nuget.Config 預存的認證的 VSTS 摘要- [# 2647年](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="b1108-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="b1108-151">[dotnet 還原]-configfile 是相對於專案目錄，而不是 cmd dir- [# 2639年](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="b1108-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="b1108-152">版本 comparsion 碼-過度配置[# 2632年](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="b1108-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="b1108-153">Nuget.exe 嘗試安裝相同的多個執行個體的封裝將平行會導致重複的寫入- [# 2628年](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="b1108-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="b1108-154">相依性資訊不會快取的多重專案作業- [# 2619年](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="b1108-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="b1108-155">安裝及更新下載的封裝，而不先檢查 [packages] 資料夾[# 2618年](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="b1108-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="b1108-156">如果套件來源清單是空的無法新增套件來源透過 UI (NuGet 3.4.x)- [# 2617年](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="b1108-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="b1108-157">誤導錯誤時嘗試安裝封裝相依於設計階段外貌- [# 2594年](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="b1108-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="b1108-158">設定"All"PackageManager 主控台從安裝封裝會嘗試第一個來源- [# 2557年](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="b1108-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="b1108-159">無法解壓縮的最新 beta ModernHttpClient- [# 2518年](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="b1108-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="b1108-160">在具有內建自我 NuGet 3.4.1-啟動 VS2015 損毀[# 2419年](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="b1108-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="b1108-161">更新命令可能是一個位元更多詳細資料如果 i 要求它能所以...- [# 2418年](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="b1108-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="b1108-162">在本機上建立 VSIX 應該 CI 組建與具有相同的 Dll 和檔案。</span><span class="sxs-lookup"><span data-stu-id="b1108-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="b1108-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="b1108-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="b1108-164">組建-中修正 NuGet 降級警告[# 2396年](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="b1108-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="b1108-165">無法驗證封裝來源 （3 次） 會永久-封鎖[# 2362年](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="b1108-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="b1108-166">從 nuget v3.3 + 安裝的套件摘要與引數時未正確地還原套件內容-NoCache 當封裝包含`.nupkg`檔案- [# 2354年](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="b1108-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="b1108-167">所有的封裝來源，但遺漏了 1 個來源，封裝 Nuget 安裝失敗- [# 2322年](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="b1108-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="b1108-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="b1108-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="b1108-169">如果單一來源授權-就會失敗，請安裝區塊[# 2034年](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="b1108-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="b1108-170">`.nuspec` 版本範圍應該覆寫-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="b1108-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="b1108-171">更新套件 super 緩慢-「 嘗試收集相依性資訊 」- [# 1909年](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="b1108-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="b1108-172">NuGet 的鏃形降級封裝時批次更新其相依性- [# 1903年](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="b1108-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="b1108-173">此組件強式名稱和私用屬性，會卸除 nuget.exe 更新。</span><span class="sxs-lookup"><span data-stu-id="b1108-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="b1108-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="b1108-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="b1108-175">相對檔案路徑的"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="b1108-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="b1108-176">改善解析程式失敗的訊息- [# 1373年](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="b1108-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="b1108-177">v3 封裝失敗並不在指定的來源封裝[# 1013年](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="b1108-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="b1108-178">封裝來源中使用相對路徑會有問題，才能使用[#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="b1108-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="b1108-179">遺漏 NUPKG 檔如果間接相依性已經存在具有較低的版本需求-產生從專案中的相依性[#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="b1108-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="b1108-180">刪除專案關閉對應的 UI 視窗中，但重新命名專案並不會重新命名 UI 視窗。</span><span class="sxs-lookup"><span data-stu-id="b1108-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="b1108-181">請注意 PMC 接聽重新命名專案和專案移除事件- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="b1108-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="b1108-182">[柳樹 Web 工作負載]建立 Razor v3 WSP 懸置- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="b1108-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="b1108-183">特定封裝安裝/還原失敗的 「 封裝包含多個 nuspec 檔案。 」</span><span class="sxs-lookup"><span data-stu-id="b1108-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="b1108-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="b1108-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="b1108-185">小寫識別碼 （& s)`packages.config`案例- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="b1108-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="b1108-186">[beta2 前 3.5]封裝還原失敗時還原 「 舊版 」 封裝- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="b1108-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="b1108-187">nuget 套件強制將.tt 檔案加入至內容的資料夾，不論什麼- [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="b1108-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="b1108-188">更新套件的 ASP.NET web 應用程式會產生與檔案相關的警告： 來源- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="b1108-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="b1108-189">nuget 套件 csproj (與`project.json`) 損毀，如果有任何 packOptions 和擁有者，在 JSON 檔案- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="b1108-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="b1108-190">nuget 套件`project.json`會忽略摘要、 作者、 等位的擁有者等 packOptions 標記[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="b1108-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="b1108-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="b1108-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="b1108-192">NuGet 套件會忽略輸出中的相依性`.nuspec`如`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="b1108-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="b1108-193">使用回復更新多個封裝保持專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="b1108-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="b1108-194">Netstandard 專案-不會新增任何 ContentFiles [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="b1108-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="b1108-195">無法封裝以.Net 為目標的程式庫標準正確[#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="b1108-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="b1108-196">檔案]-> [新增專案]-> [類別庫 （可攜式） 專案失敗 VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="b1108-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="b1108-197">NuGet 錯誤-1.0.0-\* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="b1108-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="b1108-198">尋找套件無法顯示，但是 Install-package works- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="b1108-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="b1108-199">錯誤時 dev15 層上的 「 安裝套件 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="b1108-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="b1108-200">nuget 套件的 xproj 會預設為無效的目標路徑- [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="b1108-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="b1108-201">當已安裝的 VS 2015 更新 3 上使用的 NuGet 版本 3.5.0 錯誤，就會發生-VS [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="b1108-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="b1108-202">「 被封鎖的 packages.config 」 `project.json` (UWP，又稱為組建整合) 專案- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="b1108-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="b1108-203">更新 dotnet cli 安裝 preview2-003121，這是官方 preview2 組建的組建指令碼。</span><span class="sxs-lookup"><span data-stu-id="b1108-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="b1108-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="b1108-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="b1108-205">封裝管理員 UI： 更新封裝之後，不會顯示新的版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="b1108-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="b1108-206">-ApiKey delete 命令列上不會讀取/傳送中 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="b1108-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="b1108-207">不正確的字串： 一個穩定的套件版本不應該在發行前版本相依性。</span><span class="sxs-lookup"><span data-stu-id="b1108-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="b1108-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="b1108-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="b1108-209">OptimizedZipPackage 快取中留下空資料夾- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="b1108-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="b1108-210">建立 （net46 和 windows 10） 的 PCL 專案 get NullRef 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b1108-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="b1108-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="b1108-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="b1108-212">Nuget 更新應該提供具有資訊價值訊息時更高的版本受到 allowedVersions 條件約束- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="b1108-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="b1108-213">Nuget v3 還原問題- [# 2891年](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="b1108-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="b1108-214">認證外掛程式已結束，錯誤碼為-1 / 錯誤下載封裝使用多個來源的認證提供者時[# 2885年](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="b1108-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="b1108-215">`project.json` nuget 還原會造成重新編譯時不變更- [# 2817年](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="b1108-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="b1108-216">符號套件永遠不能用於安裝或更新- [# 2807年](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="b1108-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="b1108-217">VS 不支援環境變數中 repositoryPath （nuget.exe 運作）- [# 2763年](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="b1108-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="b1108-218">標示未加上標籤的 Uielement 封裝管理員 UI 中的協助工具： [# 2745年](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="b1108-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="b1108-219">可攜式架構來使用連字號連接的設定檔會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="b1108-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="b1108-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="b1108-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="b1108-221">NuGet 封裝管理員可以讓您清楚該詳細不適用於封裝中的選項清單`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="b1108-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="b1108-222">nuget.exe 推送/刪除不會使用 API 金鑰- [# 2627年](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="b1108-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="b1108-223">鎖定的屬性移除鎖定檔案- [# 2379年](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="b1108-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="b1108-224">NuGet 3.3.0 更新無法使用 '...額外的條件約束中定義 packages.config 阻止了此作業。 '</span><span class="sxs-lookup"><span data-stu-id="b1108-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="b1108-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="b1108-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="b1108-226">假的訊息-不存在則會擲回的本機來源從安裝封裝[# 1674年](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="b1108-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="b1108-227">[可升級] 篩選條件會顯示升級違反版本條件約束- [# 1094年](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="b1108-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="b1108-228">無法更新原生封裝- [# 1291年](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="b1108-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="b1108-229">功能</span><span class="sxs-lookup"><span data-stu-id="b1108-229">Features</span></span>

* <span data-ttu-id="b1108-230">支援為 false 的設定 CopyLocal 參考加入 nuget- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="b1108-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="b1108-231">MSBuild 15-nuget.exe 支援[# 1937年](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="b1108-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="b1108-232">組件支援。`csproj`</span><span class="sxs-lookup"><span data-stu-id="b1108-232">Pack support for .`csproj`</span></span><span data-ttu-id="b1108-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="b1108-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="b1108-234">正在執行的使用者動作時，停用使用者動作- [# 1440年](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="b1108-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="b1108-235">NuGet 應該加入支援`runtimes/{rid}/nativeassets/{txm}/`  -  [# 2782年](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="b1108-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="b1108-236">加入遺漏的 NuGet 中的架構相容性 （也就是已在 3.x） 2.x- [# 2720年](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="b1108-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="b1108-237">支援後援封裝資料夾- [# 2899年](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="b1108-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="b1108-238">設計和實作封裝類型的概念，以支援工具套件- [# 2476年](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="b1108-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="b1108-239">新增 API 來取得全域套件資料夾的路徑[# 2403年](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="b1108-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="b1108-240">啟用在組件-SemVer 2.0.0 [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="b1108-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="b1108-241">DCR</span><span class="sxs-lookup"><span data-stu-id="b1108-241">DCRs</span></span>

* <span data-ttu-id="b1108-242">nuget.exe 推送的逾時參數無法運作- [# 2785年](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="b1108-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="b1108-243">封裝描述文字應該是可選取- [# 1769年](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="b1108-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="b1108-244">啟用產生 nuget.exe`.props`和`.targets`檔案`.nuproj`專案[# 2711年](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="b1108-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="b1108-245">加入擴充性 API 來比較架構來使用匯入- [# 2633年](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="b1108-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="b1108-246">隱藏相依性的選項，當使用`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="b1108-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="b1108-247">列印出 nuget.exe 版本標頭中詳細的輸出- [# 1887年](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="b1108-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="b1108-248">若要讓使用者知道，在基礎 dotnet tfm 升級/安裝 PCL 可能會導致問題-需要 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="b1108-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="b1108-249">警告錯誤安裝/升級專案以 tfm ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="b1108-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="b1108-250">NuGet ReShaper 與修正效能問題的更新- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="b1108-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="b1108-251">新增 netcoreapp11 和 netstandard17 支援- [# 2998年](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="b1108-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="b1108-252">運用 AssemblyMetadata 屬性`.nuspec`語彙基元取代- [# 2851年](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="b1108-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
