---
title: NuGet 3.5 RTM 版本資訊
description: NuGet 3.5 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776354"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="9a5e8-103">NuGet 3.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="9a5e8-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="9a5e8-104">[NuGet 3.5-RC 版本](../release-notes/nuget-3.5-RC.md)  |  資訊[NuGet 4.0 RC 版本](../release-notes/nuget-4.0-RC.md)資訊</span><span class="sxs-lookup"><span data-stu-id="9a5e8-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9a5e8-105">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="9a5e8-105">Bug Fixes</span></span>

* <span data-ttu-id="9a5e8-106">套件未在 mono 上使用 MSBuild 14.1- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="9a5e8-107">[更新] 索引標籤未選取要更新的最新可用版本，改為選取 [目前安裝的版本- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="9a5e8-108">修正驗證私用 v2 MyGet 摘要之後的損毀，並按一下 [顯示更多結果]- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="9a5e8-109">[#3446](https://github.com/NuGet/Home/issues/3446) UI 的記錄訊息看似反向順序</span><span class="sxs-lookup"><span data-stu-id="9a5e8-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="9a5e8-110">v 3.4.4-Nuget 還原會擲回「不支援指定路徑的格式」- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="9a5e8-111">NuGet cmdLine 3.6 搶鮮版（Beta）不接受-a-a Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="9a5e8-112">IKVM 大型專案的 Nuget 慢安裝- [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="9a5e8-113">nuget.exe 更新-自行持續更新- [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="9a5e8-114">3.5 從 UNC 共用安裝/還原具有從 3.4.4 [#3355](https://github.com/NuGet/Home/issues/3355)的效能回歸</span><span class="sxs-lookup"><span data-stu-id="9a5e8-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="9a5e8-115">從 net451 專案的封裝管理 UI 安裝 Moq 時發生錯誤- [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="9a5e8-116">解決方案層級的 [安裝] 索引標籤不會顯示套件的版本 [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="9a5e8-117">從 [已安裝] 索引標籤的 [xproj `project.json` 更新] 失去狀態- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="9a5e8-118">NuGet 套件 on 會 `.csproj` 忽略檔案 `.nuspec` - [#3257](https://github.com/NuGet/Home/issues/3257)中的空檔案元素</span><span class="sxs-lookup"><span data-stu-id="9a5e8-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="9a5e8-119">裝載在 IIS 中的網站專案不應導致還原失敗 [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="9a5e8-120">V3 端點重新導向至 v2- [#3179](https://github.com/NuGet/Home/issues/3179)時，不會從 Nuget.Config 取出認證</span><span class="sxs-lookup"><span data-stu-id="9a5e8-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="9a5e8-121">NuGet 套件在抓取可移植元件中繼資料時無法解析元件- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="9a5e8-122">在 Mono 上找不到 Nuget `msbuild.exe` - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="9a5e8-123">nuget.exe 套件不允許以數位開頭的發行前標記- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="9a5e8-124">在 VS2015E 上安裝 nuget 套件失敗- [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="9a5e8-125">allowedVersions 篩選無法在解決方案層級運作- [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="9a5e8-126">因為已新增具有相同索引鍵的專案，所以隨機還原失敗。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="9a5e8-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="9a5e8-128">無法安裝 Nuget。 `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)中常見</span><span class="sxs-lookup"><span data-stu-id="9a5e8-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="9a5e8-129">使用 UI 來搜尋 V2 來源時，會針對每個識別碼呼叫 FindPackagesById 兩次- [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="9a5e8-130">套件無法相依于專案- [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="9a5e8-131">nuget.exe 套件-排除已記載但不受支援- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="9a5e8-132">當的 ' contentFiles ' 區段無效時，出現錯誤訊息的問題 `.nuspec` - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="9a5e8-133">推送一律會使用已驗證的套件來源傳送整個套件兩次- [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="9a5e8-134">當專案沒有 #1496 時，在呼叫 nuget.exe update \* .csproj 時未提供任何資訊。 `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="9a5e8-135">`packages.config` restore 不會重試來自 V2 來源的5xx 狀態碼- [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="9a5e8-136">File src 中的雙點 `.nuspec` 無法運作- [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="9a5e8-137">CoreCLR restore 需要使用加密來忽略摘要- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="9a5e8-138">nuget.exe 推送403處理-錯誤地提示輸入認證- [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="9a5e8-139">透過套件管理員的 NuGet 更新會移除 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)的屬性</span><span class="sxs-lookup"><span data-stu-id="9a5e8-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="9a5e8-140">VisualStudio 嘗試載入 "Nuget.exe. TeamFoundationServer14"，但該 DLL 名稱變更為 "TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="9a5e8-141">套件管理員 UI 未顯示新更新的版本- [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="9a5e8-142">更新套件嘗試使用 packageid、版本而非套件。版本- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="9a5e8-143">如果專案未使用 nuget (`packages.config` 或 `project.json`) [#2766](https://github.com/NuGet/Home/issues/2766) ，nuget restore .csproj 應該會發生錯誤</span><span class="sxs-lookup"><span data-stu-id="9a5e8-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="9a5e8-144">在您的工作區中找不到 TFS 錯誤 "[file]，或您沒有許可權可在方案/專案系結至 TFS 原始檔控制時，于升級或卸載期間進行存取- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="9a5e8-145">更新套件不會取得非目標套件的相依性- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="9a5e8-146">沒有任何方法可以設定 Nuget 套件管理員 UI 動作的記錄詳細資訊層級- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="9a5e8-147">nuget 設定無效-VS 2015 VSIX (v 3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="9a5e8-148">`NuGetDefaults.Config` () 中 `ProgramData\NuGet` 的 DefaultPushSource 無法運作- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="9a5e8-149">nuget 3.4.3 在套件組建上的版本取得值不可以是 null- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="9a5e8-150">還原未使用來自 Nuget.Config 的 VSTS 摘要預存認證- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="9a5e8-151">[dotnet restore]--get-help 相對於專案目錄，而非 cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="9a5e8-152">版本比較程式碼中的過度配置- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="9a5e8-153">nuget.exe 嘗試以平行方式安裝相同封裝的多個實例會導致雙重寫入 [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="9a5e8-154">不會快取多專案作業的相依性資訊- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="9a5e8-155">安裝並更新下載套件，而不需先檢查套件資料夾 [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="9a5e8-156">如果 [套件來源] 清單是空的，則無法透過 UI 新增套件來源 (NuGet 3.4. x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="9a5e8-157">嘗試安裝相依于設計階段 facade 的封裝時發生誤導錯誤- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="9a5e8-158">從 >packagemanager 主控台安裝具有「全部」設定的封裝，只會嘗試第一個來源 [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="9a5e8-159">最新 Beta 未解壓縮 ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="9a5e8-160">在啟動時使用自行建立的 NuGet 3.4.1 VS2015 損毀- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="9a5e8-161">如果我要求，Update 命令可能有點詳細資訊 ...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="9a5e8-162">在本機建立的 VSIX 應該與 CI 組建具有相同的 Dll 和檔案。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="9a5e8-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="9a5e8-164">修正組建- [#2396](https://github.com/NuGet/Home/issues/2396)中的 NuGet 降級警告</span><span class="sxs-lookup"><span data-stu-id="9a5e8-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="9a5e8-165">無法驗證套件來源 (3 次) 將永遠封鎖 [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="9a5e8-166">當套件包含檔案時，從 nuget v1.0 + 摘要安裝套件時，無法正確還原套件內容 `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354) -NoCache</span><span class="sxs-lookup"><span data-stu-id="9a5e8-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="9a5e8-167">使用所有套件來源安裝 Nuget，但從1來源遺失套件，失敗- [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="9a5e8-168">PerfWatsonUIDelay： nuget.packagemanagement.visualstudio.dll！Nuget.exe. VisualStudio. VSMSBuildNuGetProjectSystem + \* lt; &gt;c__DisplayClass_0 + &lt; &lt; AddReference &gt; b__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="9a5e8-169">如果單一來源失敗授權，請安裝區塊- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="9a5e8-170">`.nuspec` 版本範圍應覆寫-IncludeReferencedProjects 版本- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="9a5e8-171">Update-Package 超級緩慢-「嘗試收集相依性資訊」- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="9a5e8-172">當批次更新其相依性時，NuGet 隱形降級套件- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="9a5e8-173">nuget.exe 更新會卸載元件強式名稱和私用屬性。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="9a5e8-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="9a5e8-175">"DefaultPushSource" 的相對檔案路徑- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="9a5e8-176">改善解析程式失敗訊息- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="9a5e8-177">v3 中的更新套件失敗，套件不在指定的來源中- [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="9a5e8-178">使用套件來源的相對路徑對使用有問題- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="9a5e8-179">缺少 NUPKG 中的相依性-如果間接相依性已存在，且版本需求較低，則會從專案產生： [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="9a5e8-180">刪除專案會關閉對應的 UI 視窗，但是重新命名專案並不會重新命名 UI 視窗。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="9a5e8-181">請注意，PMC 會接聽專案重新命名和專案移除事件- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="9a5e8-182">[Willow Web 工作負載]建立 Razor v3 WSP 停止回應- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="9a5e8-183">特定套件的安裝/還原失敗，並出現「封裝包含多個 nuspec 檔案」。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="9a5e8-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="9a5e8-185">小寫識別碼 & `packages.config` 案例- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="9a5e8-186">[3.5-Beta2]封裝還原無法還原「舊版」套件- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="9a5e8-187">無論什麼[#3203](https://github.com/NuGet/Home/issues/3203) ，nuget 套件都會強制將 tt 檔新增至內容資料夾</span><span class="sxs-lookup"><span data-stu-id="9a5e8-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="9a5e8-188">ASP.NET web 應用程式的更新套件會產生與檔案相關的警告：來源- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="9a5e8-189">nuget 套件 .csproj (`project.json` 如果沒有 JSON 檔案中的 packOptions 和擁有者，) 會當機- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="9a5e8-190">的 nuget 套件會 `project.json` 忽略 packOptions 標記，例如摘要、作者、擁有者等 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="9a5e8-191">NullReferenceException via PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="9a5e8-192">NuGet 套件會忽略 #3145 輸出 `.nuspec` 的 `project.json`  -  [](https://github.com/NuGet/Home/issues/3145)相依性</span><span class="sxs-lookup"><span data-stu-id="9a5e8-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="9a5e8-193">使用 rollback 更新多個封裝會讓專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="9a5e8-194">未針對 netstandard 專案新增任何的 ContentFiles- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="9a5e8-195">無法正確封裝以 .Net Standard 為目標的程式庫- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="9a5e8-196">檔案-> 新專案 > 類別庫 (便攜) 專案在 VS2015 和 Dev15 中失敗- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="9a5e8-197">nuGet 錯誤-1.0.0-\* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="9a5e8-198">Find-Package 無法顯示，但 Install-Package 運作- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="9a5e8-199">在 dev15 上「安裝套件 jquery. 驗證」時發生錯誤- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="9a5e8-200">xproj 的 nuget 套件預設為不正確目標路徑- [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="9a5e8-201">在使用 NuGet 版本3.5.0 的 VS 上安裝 VS 2015 update 3 時發生錯誤- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="9a5e8-202"> (UWP 中的「封鎖者」 packages.config」，也就 `project.json` 是整合) 專案的組建- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="9a5e8-203">將組建腳本所安裝的 dotnet cli 更新為 preview2-003121，也就是官方 preview2 組建。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="9a5e8-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="9a5e8-205">套件管理員 UI：更新封裝之後不會顯示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="9a5e8-206">-在3.5.0 中不會讀取/傳送 ApiKey on delete 命令列-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="9a5e8-207">不正確的字串：套件的穩定版本不應具有發行前版本的相依性。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="9a5e8-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="9a5e8-209">OptimizedZipPackage 快取會保留空的資料夾- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="9a5e8-210">建立 PCL (net46 和 windows 10) project get NullRef 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="9a5e8-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="9a5e8-212">當較高的版本受限於 allowedVersions 條件約束時，Nuget 更新應提供資訊性訊息 [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="9a5e8-213">Nuget v3 還原問題- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="9a5e8-214">認證外掛程式結束，發生錯誤-1/在使用具有多個來源的認證提供者時下載封裝時發生錯誤- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="9a5e8-215">`project.json` 當沒有任何變更時，nuget 還原會導致重新編譯- [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="9a5e8-216">符號套件絕不能用在安裝或更新- [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="9a5e8-217">VS 不支援 repositoryPath ( # A0) [#2763](https://github.com/NuGet/Home/issues/2763)的環境變數</span><span class="sxs-lookup"><span data-stu-id="9a5e8-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="9a5e8-218">針對協助工具將未標記的 UIElements 標示為封裝管理員 UI- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="9a5e8-219">具有斷字元設定檔的可移植架構會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="9a5e8-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="9a5e8-221">NuGet 套件管理員應該確定套件詳細資料的選項清單不適用 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="9a5e8-222">nuget.exe 推送/刪除不會使用 API 金鑰- [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="9a5e8-223">從鎖定檔案中移除鎖定的屬性- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="9a5e8-224">NuGet 3.3.0 更新失敗，並出現「額外的條件約束 .。。在 packages.config 中定義會防止這項作業。</span><span class="sxs-lookup"><span data-stu-id="9a5e8-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="9a5e8-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="9a5e8-226">從不存在的本機來源安裝套件會擲回假訊息 [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="9a5e8-227">「可用升級」篩選器會顯示違反版本條件約束的升級- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="9a5e8-228">無法更新原生封裝- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="9a5e8-229">功能</span><span class="sxs-lookup"><span data-stu-id="9a5e8-229">Features</span></span>

* <span data-ttu-id="9a5e8-230">支援在 NuGet 新增的參考上將 CopyLocal 設定為 false- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="9a5e8-231">MSBuild 15 [#1937](https://github.com/NuGet/Home/issues/1937)的 nuget.exe 支援</span><span class="sxs-lookup"><span data-stu-id="9a5e8-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="9a5e8-232">的套件支援。`csproj`</span><span class="sxs-lookup"><span data-stu-id="9a5e8-232">Pack support for .`csproj`</span></span><span data-ttu-id="9a5e8-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="9a5e8-234">當正在執行使用者動作時停用使用者動作- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="9a5e8-235">NuGet 應該新增 `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)的支援</span><span class="sxs-lookup"><span data-stu-id="9a5e8-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="9a5e8-236">新增 NuGet 2.x 中遺失的 framework 相容性（已在2.x 中 (）) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="9a5e8-237">支援 fallback 封裝資料夾- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="9a5e8-238">設計和執行封裝類型的概念以支援工具套件- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="9a5e8-239">新增 API 以取得全域套件資料夾的路徑- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="9a5e8-240">在 pack- [#3356](https://github.com/NuGet/Home/issues/3356)中啟用 SemVer 2.0。0</span><span class="sxs-lookup"><span data-stu-id="9a5e8-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="9a5e8-241">DCR</span><span class="sxs-lookup"><span data-stu-id="9a5e8-241">DCRs</span></span>

* <span data-ttu-id="9a5e8-242">nuget.exe push-timeout 參數無法運作- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="9a5e8-243">封裝描述文字應為可選取- [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="9a5e8-244">啟用 nuget.exe 以產生 `.props` `.targets` `.nuproj` 專案 [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="9a5e8-245">新增擴充性 API 以使用 imports 進行比較- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="9a5e8-246">使用 #2486 時隱藏相依性選項 `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="9a5e8-247">在詳細的輸出中列印出 nuget.exe 版本標頭- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="9a5e8-248">NuGet 必須讓使用者知道以 dotnet tfm 為基礎的 PCL 進行升級/安裝可能會造成問題- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="9a5e8-249">針對專案的不正確安裝/升級發出警告/tfm = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="9a5e8-250">修正 ReShaper 和 NuGet for Update 的效能問題- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="9a5e8-251">新增 netcoreapp11 和 netstandard17 支援- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="9a5e8-252">利用 AssemblyMetadata 屬性進行 `.nuspec` 權杖取代- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="9a5e8-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
