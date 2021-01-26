---
title: NuGet 3.4.3 版本資訊
description: NuGet 3.4.3 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776467"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="04707-103">NuGet 3.4.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="04707-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="04707-104">[NuGet 3.4.2 版本](../release-notes/nuget-3.4.2.md)  |  資訊[NuGet 3.4.4 版本](../release-notes/nuget-3.4.4.md)資訊</span><span class="sxs-lookup"><span data-stu-id="04707-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="04707-105">NuGet 3.4.3 已于2016年4月22日發行，以解決在3.4 和後續版本中識別的數個問題。</span><span class="sxs-lookup"><span data-stu-id="04707-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="04707-106">您可以在 [這裡](https://dist.nuget.org/index.html)下載 VSIX 和 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="04707-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="04707-107">更新和改進</span><span class="sxs-lookup"><span data-stu-id="04707-107">Updates and Improvements</span></span>

* <span data-ttu-id="04707-108">改善 Visual Studio 的可靠性。</span><span class="sxs-lookup"><span data-stu-id="04707-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="04707-109">我們已修正 NuGet 中導致 Visual Studio 損毀的一些問題。</span><span class="sxs-lookup"><span data-stu-id="04707-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="04707-110">修正</span><span class="sxs-lookup"><span data-stu-id="04707-110">Fixes</span></span>

* <span data-ttu-id="04707-111">修正了一些受密碼保護的私用 nuget 摘要的授權問題。</span><span class="sxs-lookup"><span data-stu-id="04707-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="04707-112">已修正無法從指定的執行時間還原 PCL 之的問題 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="04707-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="04707-113">某些客戶在安裝套件時遇到間歇性失敗。</span><span class="sxs-lookup"><span data-stu-id="04707-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="04707-114">這項功能現在已在此版本中修正。</span><span class="sxs-lookup"><span data-stu-id="04707-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="04707-115">修正在 c + +/CLI 專案中導致還原失敗的問題 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="04707-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="04707-116">某些套件 (例如，當您在 mono 中使用 nuget 時，未正確解壓縮的 ModernHttpClient) 。</span><span class="sxs-lookup"><span data-stu-id="04707-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="04707-117">這項功能現在已在此版本中修正。</span><span class="sxs-lookup"><span data-stu-id="04707-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="04707-118">如需此版本中的修正和增強功能的完整清單，請參閱 [此處](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)的問題清單。</span><span class="sxs-lookup"><span data-stu-id="04707-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>