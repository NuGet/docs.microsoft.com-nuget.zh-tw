---
title: 3.5 Beta2 版本資訊
description: NuGet 3.5 Beta 2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776390"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="a3b39-103">NuGet 3.5 Beta2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a3b39-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="a3b39-104">[NuGet 3.5-Beta 版注意事項](../release-notes/nuget-3.5-Beta.md)  | [NuGet 3.5-RC 版本](../release-notes/nuget-3.5-RC.md)資訊</span><span class="sxs-lookup"><span data-stu-id="a3b39-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="a3b39-105">NuGet 3.5 Beta 2 RTM 發行于2016年6月27日，Visual Studio 2013 和 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a3b39-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="a3b39-106">完整變更記錄</span><span class="sxs-lookup"><span data-stu-id="a3b39-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="a3b39-107">問題清單</span><span class="sxs-lookup"><span data-stu-id="a3b39-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="a3b39-108">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="a3b39-108">Bug Fixes</span></span>

* <span data-ttu-id="a3b39-109">已更新錯誤訊息，以在 .NET Core 中缺少密碼 decrpytion 的支援以進行驗證的摘要- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="a3b39-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="a3b39-110">如果 .NET Core 專案為開啟[#2932](https://github.com/NuGet/Home/issues/2932) ，封裝管理員主控台 Get-Package 會失敗</span><span class="sxs-lookup"><span data-stu-id="a3b39-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="a3b39-111">修正 NuGet push 命令[#2910](https://github.com/NuGet/Home/issues/2910)中不正確的403處理</span><span class="sxs-lookup"><span data-stu-id="a3b39-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="a3b39-112">修正將 disableSourceControlIntegration 設為 true 時，在系結至 TFS 原始檔控制的解決方案中卸載封裝的問題- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="a3b39-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="a3b39-113">修正套件更新以將非目標套件納入考慮- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="a3b39-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="a3b39-114">使用 MSBuild 詳細資訊層級來設定 Nuget 套件管理員 UI 動作的記錄器層級- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="a3b39-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="a3b39-115">修正 NuGet 設定在網站專案中是不正確錯誤-VS 2015 VSIX (v 3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="a3b39-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="a3b39-116">修正套件中 `.csproj` 包含內容檔案時的問題- [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="a3b39-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="a3b39-117">`NuGetDefaults.Config` () 中 `ProgramData\NuGet` 的 DefaultPushSource 無法運作- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="a3b39-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="a3b39-118">修正在套件建立時，Nuget 3.4.3 版本值不能是 null 的問題- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="a3b39-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="a3b39-119">Restore 會使用 VSTS 摘要 Nuget.Config 的預存認證- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="a3b39-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="a3b39-120">效能-修正版本比較程式碼中的過度配置- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="a3b39-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="a3b39-121">修正多個 nuget.exe 實例嘗試以平行方式安裝相同套件時的問題 [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="a3b39-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="a3b39-122">效能-快取多專案作業的相依性資訊- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="a3b39-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="a3b39-123">修正來源清單空白時，無法從設定新增套件來源的問題- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="a3b39-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="a3b39-124">修正嘗試安裝相依于設計階段 facade 之套件時的誤導錯誤- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="a3b39-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="a3b39-125">從 >packagemanager 主控台安裝具有「全部」設定的封裝，只會嘗試第一個來源 [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="a3b39-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="a3b39-126">修正套件的問題，這些封裝在未來 (Mono) 的檔案有寫入時間 [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="a3b39-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="a3b39-127">當在 update 命令中尋找專案失敗時顯示例外狀況- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="a3b39-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="a3b39-128">當套件包含檔案時，從 nuget v1.0 + 摘要安裝套件時，無法正確還原套件內容 `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354) -NoCache</span><span class="sxs-lookup"><span data-stu-id="a3b39-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="a3b39-129">修正套件安裝 (所有來源) 當套件從1個來源[#2322](https://github.com/NuGet/Home/issues/2322)遺失時的問題</span><span class="sxs-lookup"><span data-stu-id="a3b39-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="a3b39-130">如果單一來源失敗授權，請安裝區塊- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="a3b39-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="a3b39-131">`.nuspec` 版本範圍應覆寫-IncludeReferencedProjects 版本- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="a3b39-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="a3b39-132">NuGet 3.3.0 更新失敗，並出現「額外的條件約束 .。。在 packages.config 中定義會防止這項作業。</span><span class="sxs-lookup"><span data-stu-id="a3b39-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="a3b39-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="a3b39-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="a3b39-134">nuget.exe 更新會卸載元件強式名稱和私用屬性。</span><span class="sxs-lookup"><span data-stu-id="a3b39-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="a3b39-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="a3b39-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="a3b39-136">修正 "DefaultPushSource" 的相對檔案路徑問題- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="a3b39-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="a3b39-137">改善更新解析程式失敗訊息- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="a3b39-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="a3b39-138">功能與行為變更</span><span class="sxs-lookup"><span data-stu-id="a3b39-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="a3b39-139">nuget.exe push-timeout 參數無法運作- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="a3b39-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="a3b39-140">nuget.exe restore 不會產生 `.props` 專案的檔案，也不會 `.targets` `.nuproj` (3.4.3.855) 中的回歸 [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="a3b39-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="a3b39-141">需要擴充性 API 來比較具有 imports 的架構 [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="a3b39-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="a3b39-142">使用 #2486 時隱藏相依性選項 `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="a3b39-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="a3b39-143">在詳細的輸出中列印出 nuget.exe 版本標頭- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="a3b39-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="a3b39-144">NuGet 應該新增/runtimes/{rid}/nativeassets/{txm}/的支援- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="a3b39-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>