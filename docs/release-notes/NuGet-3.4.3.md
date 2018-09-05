---
title: NuGet 3.4.3 版本資訊
description: 版本資訊 NuGet 3.4.3 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549161"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="df76c-103">NuGet 3.4.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="df76c-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="df76c-104">[NuGet 3.4.2 版本資訊](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 版本資訊](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="df76c-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="df76c-105">NuGet 3.4.3 已發行於 2016 年 4 月 22 日解決 3.4 及後續版本中已識別的幾個問題。</span><span class="sxs-lookup"><span data-stu-id="df76c-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="df76c-106">您可以下載 VSIX 和 nuget.exe[此處](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="df76c-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="df76c-107">更新和增強功能</span><span class="sxs-lookup"><span data-stu-id="df76c-107">Updates and Improvements</span></span>

* <span data-ttu-id="df76c-108">改善 Visual Studio 的可靠性。</span><span class="sxs-lookup"><span data-stu-id="df76c-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="df76c-109">我們已修正一些問題造成損毀 Visual Studio 中的 nuget。</span><span class="sxs-lookup"><span data-stu-id="df76c-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="df76c-110">修正</span><span class="sxs-lookup"><span data-stu-id="df76c-110">Fixes</span></span>

* <span data-ttu-id="df76c-111">已修正一些授權問題受密碼保護的私用 nuget 摘要。</span><span class="sxs-lookup"><span data-stu-id="df76c-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="df76c-112">已修正的問題解決無法還原 PCL 的從`project.json`以指定的執行階段。</span><span class="sxs-lookup"><span data-stu-id="df76c-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="df76c-113">安裝套件時，某些客戶所遇到間歇性失敗。</span><span class="sxs-lookup"><span data-stu-id="df76c-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="df76c-114">這現在已修正在此版本中。</span><span class="sxs-lookup"><span data-stu-id="df76c-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="df76c-115">已修正的問題，導致還原失敗，在 C + + /cli 專案與`project.json`。</span><span class="sxs-lookup"><span data-stu-id="df76c-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="df76c-116">無法解壓縮正確當您使用 nuget 在 mono 中某些套件 (例如 ModernHttpClient)。</span><span class="sxs-lookup"><span data-stu-id="df76c-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="df76c-117">這現在已修正在此版本中。</span><span class="sxs-lookup"><span data-stu-id="df76c-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="df76c-118">如中此版本的修正和改善的完整清單，請參閱的問題清單[此處](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="df76c-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>