---
title: "NuGet 2.2.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 39ceaeb3-2d33-4b1c-b195-eba36c6cbf9a
description: "版本資訊包含 NuGet 2.2.1 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.2.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c31150572b4b6e066643ebcf0d92be16b25c6e19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="77f3c-104">NuGet 2.2.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="77f3c-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="77f3c-105">[NuGet 2.2 版本資訊](../release-notes/nuget-2.2.md) | [NuGet 2.5 版本資訊](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="77f3c-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="77f3c-106">NuGet 2.2.1 已於 2013 年 2 月 15 日發行。</span><span class="sxs-lookup"><span data-stu-id="77f3c-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="77f3c-107">VS 擴充功能版本號碼是 2.2.40116.9051。</span><span class="sxs-lookup"><span data-stu-id="77f3c-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="77f3c-108">當地語系化的重新整理</span><span class="sxs-lookup"><span data-stu-id="77f3c-108">Localization Refresh</span></span>
<span data-ttu-id="77f3c-109">NuGet 隨附的 Visual Studio 2012，當它已完全當地語系化成英文 + 13 其他語言。</span><span class="sxs-lookup"><span data-stu-id="77f3c-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="77f3c-110">從那時起，NuGet 2.1 和 2.2 已出貨，但當地語系化有尚未重新整理。</span><span class="sxs-lookup"><span data-stu-id="77f3c-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="77f3c-111">NuGet 2.2.1 版本重新整理我們當地語系化。</span><span class="sxs-lookup"><span data-stu-id="77f3c-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="77f3c-112">NuGet 的 UI 及 PowerShell 主控台會當地語系化成下列語言：</span><span class="sxs-lookup"><span data-stu-id="77f3c-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="77f3c-113">中文 (簡體)</span><span class="sxs-lookup"><span data-stu-id="77f3c-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="77f3c-114">和 SharePoint 2010 顯示的</span><span class="sxs-lookup"><span data-stu-id="77f3c-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="77f3c-115">捷克文</span><span class="sxs-lookup"><span data-stu-id="77f3c-115">Czech</span></span>
1. <span data-ttu-id="77f3c-116">英文</span><span class="sxs-lookup"><span data-stu-id="77f3c-116">English</span></span>
1. <span data-ttu-id="77f3c-117">法文</span><span class="sxs-lookup"><span data-stu-id="77f3c-117">French</span></span>
1. <span data-ttu-id="77f3c-118">德文</span><span class="sxs-lookup"><span data-stu-id="77f3c-118">German</span></span>
1. <span data-ttu-id="77f3c-119">義大利文</span><span class="sxs-lookup"><span data-stu-id="77f3c-119">Italian</span></span>
1. <span data-ttu-id="77f3c-120">日文</span><span class="sxs-lookup"><span data-stu-id="77f3c-120">Japanese</span></span>
1. <span data-ttu-id="77f3c-121">韓文</span><span class="sxs-lookup"><span data-stu-id="77f3c-121">Korean</span></span>
1. <span data-ttu-id="77f3c-122">波蘭文</span><span class="sxs-lookup"><span data-stu-id="77f3c-122">Polish</span></span>
1. <span data-ttu-id="77f3c-123">葡萄牙文 (巴西)</span><span class="sxs-lookup"><span data-stu-id="77f3c-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="77f3c-124">俄文</span><span class="sxs-lookup"><span data-stu-id="77f3c-124">Russian</span></span>
1. <span data-ttu-id="77f3c-125">西班牙文</span><span class="sxs-lookup"><span data-stu-id="77f3c-125">Spanish</span></span>
1. <span data-ttu-id="77f3c-126">土耳其文</span><span class="sxs-lookup"><span data-stu-id="77f3c-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="77f3c-127">Visual Studio 範本可支援多個預先安裝的封裝儲存機制</span><span class="sxs-lookup"><span data-stu-id="77f3c-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="77f3c-128">如果您產生 Visual Studio 範本，您可以使用 NuGet[預先安裝套件](../visual-studio-extensibility/visual-studio-templates.md)做為範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="77f3c-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="77f3c-129">到目前為止，這項功能有一項限制的所有封裝需要來自相同的來源。</span><span class="sxs-lookup"><span data-stu-id="77f3c-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="77f3c-130">隨 NuGet 2.2.1，您可以從多個 （範本、 在 VSIX 中或在登錄中定義的磁碟上的資料夾） 內的儲存機制安裝套件。</span><span class="sxs-lookup"><span data-stu-id="77f3c-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="77f3c-131">這項功能的主要案例是自訂的 ASP.NET 專案範本。</span><span class="sxs-lookup"><span data-stu-id="77f3c-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="77f3c-132">內建 ASP.NET 範本使用預先安裝的套件，提取從本機磁碟的封裝。</span><span class="sxs-lookup"><span data-stu-id="77f3c-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="77f3c-133">您現在可以建立自訂 ASP.NET 專案範本使用 asp.net 安裝現有的封裝，但將額外的 NuGet 封裝加入至您的範本。</span><span class="sxs-lookup"><span data-stu-id="77f3c-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="77f3c-134">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="77f3c-134">Bug Fixes</span></span>
<span data-ttu-id="77f3c-135">NuGet 2.2.1 包含幾個目標的 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="77f3c-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="77f3c-136">如需工作的清單項目固定在 NuGet 2.2.1，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="77f3c-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="77f3c-137">已知問題</span><span class="sxs-lookup"><span data-stu-id="77f3c-137">Known Issues</span></span>

<span data-ttu-id="77f3c-138">如果您要擴充 ASP.NET 專案範本，所有預先安裝的封裝儲存機制必須使用相同的值`isPreunzipped`屬性。</span><span class="sxs-lookup"><span data-stu-id="77f3c-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
