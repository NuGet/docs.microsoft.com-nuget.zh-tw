---
title: NuGet 2.2.1 版本資訊
description: 版本資訊 NuGet 2.2.1 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550694"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="b87a7-103">NuGet 2.2.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="b87a7-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="b87a7-104">[NuGet 2.2 版本資訊](../release-notes/nuget-2.2.md) | [NuGet 2.5 版本資訊](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="b87a7-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="b87a7-105">NuGet 2.2.1 已於 2013 年 2 月 15 日發行。</span><span class="sxs-lookup"><span data-stu-id="b87a7-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="b87a7-106">VS 擴充功能版本號碼是 2.2.40116.9051。</span><span class="sxs-lookup"><span data-stu-id="b87a7-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="b87a7-107">當地語系化的重新整理</span><span class="sxs-lookup"><span data-stu-id="b87a7-107">Localization Refresh</span></span>
<span data-ttu-id="b87a7-108">NuGet 隨附於 Visual Studio 2012，當它已完全當地語系化成英文 + 其他 13 種語言。</span><span class="sxs-lookup"><span data-stu-id="b87a7-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="b87a7-109">從那時起，NuGet 2.1 和 2.2 已出貨，但當地語系化有未重新整理。</span><span class="sxs-lookup"><span data-stu-id="b87a7-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="b87a7-110">NuGet 2.2.1 版本重新整理我們的當地語系化。</span><span class="sxs-lookup"><span data-stu-id="b87a7-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="b87a7-111">NuGet 的 UI 和 PowerShell 主控台會當地語系化成下列語言版本：</span><span class="sxs-lookup"><span data-stu-id="b87a7-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="b87a7-112">中文 (簡體)</span><span class="sxs-lookup"><span data-stu-id="b87a7-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="b87a7-113">和 SharePoint 2010 顯示的</span><span class="sxs-lookup"><span data-stu-id="b87a7-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="b87a7-114">捷克文</span><span class="sxs-lookup"><span data-stu-id="b87a7-114">Czech</span></span>
1. <span data-ttu-id="b87a7-115">英文</span><span class="sxs-lookup"><span data-stu-id="b87a7-115">English</span></span>
1. <span data-ttu-id="b87a7-116">法文</span><span class="sxs-lookup"><span data-stu-id="b87a7-116">French</span></span>
1. <span data-ttu-id="b87a7-117">德文</span><span class="sxs-lookup"><span data-stu-id="b87a7-117">German</span></span>
1. <span data-ttu-id="b87a7-118">義大利文</span><span class="sxs-lookup"><span data-stu-id="b87a7-118">Italian</span></span>
1. <span data-ttu-id="b87a7-119">日文</span><span class="sxs-lookup"><span data-stu-id="b87a7-119">Japanese</span></span>
1. <span data-ttu-id="b87a7-120">韓文</span><span class="sxs-lookup"><span data-stu-id="b87a7-120">Korean</span></span>
1. <span data-ttu-id="b87a7-121">波蘭文</span><span class="sxs-lookup"><span data-stu-id="b87a7-121">Polish</span></span>
1. <span data-ttu-id="b87a7-122">葡萄牙文 (巴西)</span><span class="sxs-lookup"><span data-stu-id="b87a7-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="b87a7-123">俄文</span><span class="sxs-lookup"><span data-stu-id="b87a7-123">Russian</span></span>
1. <span data-ttu-id="b87a7-124">西班牙文</span><span class="sxs-lookup"><span data-stu-id="b87a7-124">Spanish</span></span>
1. <span data-ttu-id="b87a7-125">土耳其文</span><span class="sxs-lookup"><span data-stu-id="b87a7-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="b87a7-126">Visual Studio 範本支援多個預先安裝的套件儲存機制</span><span class="sxs-lookup"><span data-stu-id="b87a7-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="b87a7-127">如果您產生 Visual Studio 範本，您可以使用 NuGet[預先安裝套件](../visual-studio-extensibility/visual-studio-templates.md)為範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="b87a7-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="b87a7-128">到目前為止，這項功能有一項限制的所有封裝，需要來自相同的來源。</span><span class="sxs-lookup"><span data-stu-id="b87a7-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="b87a7-129">使用 NuGet 2.2.1，您可以從多個 （範本、 在 VSIX 中或登錄中所定義的磁碟上的資料夾） 內的存放庫安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="b87a7-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="b87a7-130">這項功能的主要案例是自訂的 ASP.NET 專案範本。</span><span class="sxs-lookup"><span data-stu-id="b87a7-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="b87a7-131">內建的 ASP.NET 範本會使用預先安裝的套件，提取本機磁碟中的套件。</span><span class="sxs-lookup"><span data-stu-id="b87a7-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="b87a7-132">您現在可以建立自訂的 ASP.NET 專案範本使用 ASP.NET 所安裝的現有套件，但將額外的 NuGet 套件新增到您的範本。</span><span class="sxs-lookup"><span data-stu-id="b87a7-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b87a7-133">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="b87a7-133">Bug Fixes</span></span>
<span data-ttu-id="b87a7-134">NuGet 2.2.1 包含幾個目標的 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="b87a7-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="b87a7-135">如需工作的清單項目中已修正 NuGet 2.2.1，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="b87a7-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="b87a7-136">已知問題</span><span class="sxs-lookup"><span data-stu-id="b87a7-136">Known Issues</span></span>

<span data-ttu-id="b87a7-137">如果您要擴充 ASP.NET 專案範本，所有預先安裝的套件存放庫必須使用相同的值`isPreunzipped`屬性。</span><span class="sxs-lookup"><span data-stu-id="b87a7-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
