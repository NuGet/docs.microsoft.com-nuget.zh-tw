---
title: NuGet 3.4.4 版本資訊
description: NuGet 3.4.4 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780224"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="9489d-103">NuGet 3.4.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="9489d-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="9489d-104">[NuGet 3.4.3 版本](../release-notes/nuget-3.4.3.md)  |  資訊[NuGet 3.5-Beta 版注意事項](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="9489d-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="9489d-105">此版本的主要焦點在於改善 nuget.exe 3.4.3 版本的品質，並提供 Visual Studio 擴充功能的一些修正。</span><span class="sxs-lookup"><span data-stu-id="9489d-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="9489d-106">您可以在 [這裡](https://dist.nuget.org/index.html)下載 VSIX 和 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="9489d-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="9489d-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19) </span><span class="sxs-lookup"><span data-stu-id="9489d-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="9489d-108">完整變更記錄</span><span class="sxs-lookup"><span data-stu-id="9489d-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="9489d-109">問題清單</span><span class="sxs-lookup"><span data-stu-id="9489d-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="9489d-110">變更</span><span class="sxs-lookup"><span data-stu-id="9489d-110">Changes</span></span>

- <span data-ttu-id="9489d-111">封裝改進：套件符號的改進、封裝 `project.json` 和其他[ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="9489d-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="9489d-112">當在 update 命令 [605] 中尋找專案失敗時顯示例外狀況 \# (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="9489d-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="9489d-113">從輸入讀取套件類型 `.nuspec` ，以及 `project.json` 在封裝[ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)時讀取</span><span class="sxs-lookup"><span data-stu-id="9489d-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="9489d-114">建立 NuGet。共用不是專案。</span><span class="sxs-lookup"><span data-stu-id="9489d-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="9489d-115">\#602</span><span class="sxs-lookup"><span data-stu-id="9489d-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="9489d-116">使用推送超時作為 HTTP 回應超時[ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="9489d-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="9489d-117">未來時間的套件檔案不會使用其時間[ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="9489d-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="9489d-118">將 `NuGet.Core.dll` 版本更新為2.12.0 以修正 XML 問題[ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="9489d-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="9489d-119">支援。/NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="9489d-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="9489d-120">在沒有 `project.json` 或 `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)的情況下還原顯示錯誤</span><span class="sxs-lookup"><span data-stu-id="9489d-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="9489d-121">修正必要版本時的相依性版本[ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="9489d-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>