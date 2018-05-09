---
title: 3.5 Beta2 前版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.5 Beta 2 版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="210dc-103">NuGet 3.5 Beta2 前版本資訊</span><span class="sxs-lookup"><span data-stu-id="210dc-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="210dc-104">[NuGet 3.5 Beta 版本資訊](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 版本資訊](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="210dc-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="210dc-105">Visual Studio 2013 和 nuget.exe NuGet 3.5 Beta 2 RTM 2016 年 6 月 27 日發行</span><span class="sxs-lookup"><span data-stu-id="210dc-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="210dc-106">完整的變更記錄</span><span class="sxs-lookup"><span data-stu-id="210dc-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="210dc-107">問題清單</span><span class="sxs-lookup"><span data-stu-id="210dc-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="210dc-108">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="210dc-108">Bug Fixes</span></span>

* <span data-ttu-id="210dc-109">更新的錯誤訊息至不支援在.NET Core 的已驗證的摘要-的密碼 decrpytion [# 2942年](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="210dc-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="210dc-110">封裝管理員主控台取得封裝失敗，則.NET Core 專案開啟- [# 2932年](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="210dc-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="210dc-111">NuGet 推入命令中修正不正確地處理 403 [# 2910年](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="210dc-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="210dc-112">請修正問題，在解除安裝 disableSourceControlIntegration 設定時，繫結至 TFS 原始檔控制的方案中的套件設為 true- [# 2739年](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="210dc-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="210dc-113">修正納入帳戶非目標的封裝-封裝更新[# 2724年](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="210dc-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="210dc-114">使用 MSBuild 的詳細資訊層級設定記錄器等級 Nuget 套件管理員的 UI 動作- [# 2705年](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="210dc-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="210dc-115">修正 NuGet 組態是無效的錯誤，在網站專案-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="210dc-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="210dc-116">修正從組件問題`.csproj`時所包含的內容檔案[# 2658年](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="210dc-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="210dc-117">在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 無法運作- [# 2653年](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="210dc-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="210dc-118">值不可為 null，在封裝建立-Nuget 3.4.3 版本中修正問題[# 2648年](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="210dc-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="210dc-119">還原會使用預存的認證 Nuget.Config，VSTS 摘要- [# 2647年](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="210dc-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="210dc-120">效能-使用版本 comparsion 程式碼中修正過度配置- [# 2632年](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="210dc-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="210dc-121">修正問題，當 nuget.exe 的多個執行個體嘗試安裝相同的封裝，以平行方式- [# 2628年](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="210dc-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="210dc-122">效能-快取相依性資訊的多個專案作業- [# 2619年](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="210dc-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="210dc-123">修正問題的來源清單是空的時，將會加入從設定的封裝來源無法[# 2617年](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="210dc-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="210dc-124">修正 Misleading 錯誤時嘗試安裝封裝相依於設計階段外貌- [# 2594年](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="210dc-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="210dc-125">設定"All"PackageManager 主控台從安裝封裝會嘗試第一個來源- [# 2557年](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="210dc-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="210dc-126">修正問題的封裝，寫入時間在未來使用的檔案 （單聲道）- [# 2518年](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="210dc-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="210dc-127">顯示例外狀況時失敗正在尋找專案中沒有更新命令- [# 2418年](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="210dc-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="210dc-128">從 nuget v3.3 + 安裝的套件摘要與引數時未正確地還原套件內容-NoCache 當封裝包含`.nupkg`檔案- [# 2354年](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="210dc-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="210dc-129">修正問題封裝 （所有來源） 時都安裝封裝遺漏來源 1- [# 2322年](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="210dc-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="210dc-130">如果單一來源授權-就會失敗，請安裝區塊[# 2034年](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="210dc-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="210dc-131">`.nuspec` 版本範圍應該覆寫-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="210dc-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="210dc-132">NuGet 3.3.0 更新無法使用 '...額外的條件約束中定義 packages.config 阻止了此作業。 '</span><span class="sxs-lookup"><span data-stu-id="210dc-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="210dc-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="210dc-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="210dc-134">此組件強式名稱和私用屬性，會卸除 nuget.exe 更新。</span><span class="sxs-lookup"><span data-stu-id="210dc-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="210dc-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="210dc-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="210dc-136">相對檔案路徑與修正問題，如"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="210dc-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="210dc-137">改善更新解析程式失敗的訊息- [# 1373年](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="210dc-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="210dc-138">功能與行為變更</span><span class="sxs-lookup"><span data-stu-id="210dc-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="210dc-139">nuget.exe 推送的逾時參數無法運作- [# 2785年](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="210dc-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="210dc-140">不會產生 nuget.exe 還原`.props`和`.targets`檔案`.nuproj`專案 （在 v3.4.3.855 迴歸）- [# 2711年](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="210dc-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="210dc-141">需要擴充性 API 來比較架構來使用匯入- [# 2633年](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="210dc-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="210dc-142">隱藏相依性的選項，當使用`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="210dc-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="210dc-143">列印出 nuget.exe 版本標頭中詳細的輸出- [# 1887年](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="210dc-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="210dc-144">NuGet 應該加入支援 /runtimes/ {刪除} /nativeassets/ {txm} /- [# 2782年](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="210dc-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>