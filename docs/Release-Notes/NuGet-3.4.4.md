---
title: "NuGet 3.4.4 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f0aa9bb-75e5-429d-9954-3cb41a909c14
description: "版本資訊包含 NuGet 3.4.4 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 3.4.4 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 51ddb918d2269990588e9cba4d15ffeb878de5f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="f14aa-104">NuGet 3.4.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="f14aa-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="f14aa-105">[NuGet 3.4.3 版本資訊](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta 版本資訊](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="f14aa-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="f14aa-106">此版本的主要焦點在於已 3.4.3 品質的改良版本與 Visual Studio 擴充功能的幾個修正 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="f14aa-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="f14aa-107">您可以下載 VSIX 和 nuget.exe[這裡](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="f14aa-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="f14aa-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) （2016年-05-19 版）</span><span class="sxs-lookup"><span data-stu-id="f14aa-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="f14aa-109">完整的變更記錄</span><span class="sxs-lookup"><span data-stu-id="f14aa-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="f14aa-110">問題的清單</span><span class="sxs-lookup"><span data-stu-id="f14aa-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="f14aa-111">變更</span><span class="sxs-lookup"><span data-stu-id="f14aa-111">Changes</span></span>

- <span data-ttu-id="f14aa-112">組件的改進： 改進符號，封裝的功能與封裝`project.json`多[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="f14aa-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="f14aa-113">尋找專案中更新命令失敗時所顯示的例外狀況 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="f14aa-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="f14aa-114">從輸入讀取封裝類型`.nuspec`和`project.json`時封裝[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="f14aa-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="f14aa-115">請 NuGet.Shared 非專案。</span><span class="sxs-lookup"><span data-stu-id="f14aa-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="f14aa-116">\#602</span><span class="sxs-lookup"><span data-stu-id="f14aa-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="f14aa-117">推入逾時做為 HTTP 回應逾時[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="f14aa-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="f14aa-118">未來的時間與封裝檔案並不會使用其時間[ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="f14aa-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="f14aa-119">更新`NuGet.Core.dll`版本來修正 XML 問題 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="f14aa-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="f14aa-120">支援./NuGet.CommandLine.XPlat v\<詳細等級\>\<模式\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="f14aa-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="f14aa-121">顯示而不還原錯誤`project.json`或`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="f14aa-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="f14aa-122">當所需的版本不同時修復相依性版本[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="f14aa-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>