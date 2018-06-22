---
title: NuGet 3.4.3 版本資訊
description: 版本資訊包含 NuGet 3.4.3 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820322"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="c772e-103">NuGet 3.4.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="c772e-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="c772e-104">[NuGet 3.4.2 版本資訊](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 版本資訊](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="c772e-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="c772e-105">NuGet 3.4.3 已發行於 2016 年 4 月 22 日解決幾個 3.4 及後續版本中已識別的問題。</span><span class="sxs-lookup"><span data-stu-id="c772e-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="c772e-106">您可以下載 VSIX 和 nuget.exe[這裡](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="c772e-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="c772e-107">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="c772e-107">Updates and Improvements</span></span>

* <span data-ttu-id="c772e-108">Visual Studio 可靠性。</span><span class="sxs-lookup"><span data-stu-id="c772e-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="c772e-109">我們已修正一些問題造成損毀 Visual Studio 中的 NuGet 中。</span><span class="sxs-lookup"><span data-stu-id="c772e-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="c772e-110">修正程式</span><span class="sxs-lookup"><span data-stu-id="c772e-110">Fixes</span></span>

* <span data-ttu-id="c772e-111">已修正一些授權問題受密碼保護的私用 nuget 摘要。</span><span class="sxs-lookup"><span data-stu-id="c772e-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="c772e-112">已修正的問題解決無法還原 PCL 的從`project.json`以指定的執行階段。</span><span class="sxs-lookup"><span data-stu-id="c772e-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="c772e-113">安裝封裝時，有些客戶已執行到斷斷續續地發生失敗。</span><span class="sxs-lookup"><span data-stu-id="c772e-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="c772e-114">這現在已在此版本中已修正。</span><span class="sxs-lookup"><span data-stu-id="c772e-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="c772e-115">已修正的問題導致還原失敗，在 C + + /CLI 專案與`project.json`。</span><span class="sxs-lookup"><span data-stu-id="c772e-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="c772e-116">其中無法解壓縮正確當您使用 nuget 中 mono 某些封裝 (例如 ModernHttpClient)。</span><span class="sxs-lookup"><span data-stu-id="c772e-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="c772e-117">這現在已在此版本中已修正。</span><span class="sxs-lookup"><span data-stu-id="c772e-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="c772e-118">如中這一版的修正和改善的完整清單，請參閱問題的清單[這裡](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="c772e-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>