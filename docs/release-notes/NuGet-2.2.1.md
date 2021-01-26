---
title: NuGet 2.2.1 版本資訊
description: NuGet 2.2.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776808"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="f7b9c-103">NuGet 2.2.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="f7b9c-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="f7b9c-104">[NuGet 2.2 版本](../release-notes/nuget-2.2.md)  |  資訊[NuGet 2.5 版本](../release-notes/nuget-2.5.md)資訊</span><span class="sxs-lookup"><span data-stu-id="f7b9c-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="f7b9c-105">NuGet 2.2.1 發行于2013年2月15日。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="f7b9c-106">VS 延伸模組的版本號碼為2.2.40116.9051。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="f7b9c-107">當地語系化更新</span><span class="sxs-lookup"><span data-stu-id="f7b9c-107">Localization Refresh</span></span>
<span data-ttu-id="f7b9c-108">當 NuGet 隨附于 Visual Studio 2012 的一部分時，會完整地當地語系化為英文 + 13 種其他語言。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="f7b9c-109">從那時起，NuGet 2.1 和2.2 已出貨，但當地語系化尚未重新整理。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="f7b9c-110">NuGet 2.2.1 版本會更新我們的當地語系化。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="f7b9c-111">NuGet 的 UI 和 PowerShell 主控台會當地語系化成下列語言：</span><span class="sxs-lookup"><span data-stu-id="f7b9c-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="f7b9c-112">簡體中文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="f7b9c-113">繁體中文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="f7b9c-114">捷克文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-114">Czech</span></span>
1. <span data-ttu-id="f7b9c-115">英文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-115">English</span></span>
1. <span data-ttu-id="f7b9c-116">法文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-116">French</span></span>
1. <span data-ttu-id="f7b9c-117">德文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-117">German</span></span>
1. <span data-ttu-id="f7b9c-118">義大利文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-118">Italian</span></span>
1. <span data-ttu-id="f7b9c-119">日文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-119">Japanese</span></span>
1. <span data-ttu-id="f7b9c-120">韓文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-120">Korean</span></span>
1. <span data-ttu-id="f7b9c-121">波蘭文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-121">Polish</span></span>
1. <span data-ttu-id="f7b9c-122">葡萄牙文 (巴西)</span><span class="sxs-lookup"><span data-stu-id="f7b9c-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="f7b9c-123">俄文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-123">Russian</span></span>
1. <span data-ttu-id="f7b9c-124">西班牙文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-124">Spanish</span></span>
1. <span data-ttu-id="f7b9c-125">土耳其文</span><span class="sxs-lookup"><span data-stu-id="f7b9c-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="f7b9c-126">Visual Studio 範本支援多個預先安裝的套件存放庫</span><span class="sxs-lookup"><span data-stu-id="f7b9c-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="f7b9c-127">如果您產生 Visual Studio 範本，您可以使用 NuGet 將 [套件預先安裝](../visual-studio-extensibility/visual-studio-templates.md) 為範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="f7b9c-128">到目前為止，這項功能會限制所有需要來自相同來源的套件。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="f7b9c-129">不過，使用 NuGet 2.2.1，您可以從範本、VSIX 或登錄) 中定義之磁片上的資料夾中，安裝多個存放庫 (的套件。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="f7b9c-130">這項功能的主要案例是自訂的 ASP.NET 專案範本。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="f7b9c-131">內建的 ASP.NET 範本使用預先安裝的套件，從本機磁片提取套件。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="f7b9c-132">您現在可以建立自訂 ASP.NET 專案範本，以使用 ASP.NET 所安裝的現有套件，但是將額外的 NuGet 套件新增至您的範本。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="f7b9c-133">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="f7b9c-133">Bug Fixes</span></span>
<span data-ttu-id="f7b9c-134">NuGet 2.2.1 包含一些目標錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="f7b9c-135">如需 NuGet 2.2.1 中已修正的工作專案清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="f7b9c-136">已知問題</span><span class="sxs-lookup"><span data-stu-id="f7b9c-136">Known Issues</span></span>

<span data-ttu-id="f7b9c-137">如果您要擴充 ASP.NET 專案範本，所有預先安裝的套件存放庫都必須使用相同的 `isPreunzipped` 屬性值。</span><span class="sxs-lookup"><span data-stu-id="f7b9c-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
