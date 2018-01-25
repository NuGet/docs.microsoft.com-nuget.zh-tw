---
title: "NuGet 2.8.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含 NuGet 2.8.1 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.8.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="b64b6-104">NuGet 2.8.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="b64b6-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="b64b6-105">[NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 版本資訊](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="b64b6-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="b64b6-106">NuGet 2.8.1 已於 2014 年 4 月 2 日發行。</span><span class="sxs-lookup"><span data-stu-id="b64b6-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="b64b6-107">在版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="b64b6-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="b64b6-108">Windows Phone 8.1 專案的支援</span><span class="sxs-lookup"><span data-stu-id="b64b6-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="b64b6-109">此版本現在支援下列新目標 framework moniker 用於目標 Windows Phone 8.1 專案：</span><span class="sxs-lookup"><span data-stu-id="b64b6-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="b64b6-110">WindowsPhone81 / WP81 （適用於 silverlight 的 Windows Phone 專案）</span><span class="sxs-lookup"><span data-stu-id="b64b6-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="b64b6-111">WindowsPhoneApp81 / WPA81 （適用於 WinRT 為基礎的 Windows Phone 應用程式專案）</span><span class="sxs-lookup"><span data-stu-id="b64b6-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="b64b6-112">更新 NuGet WebMatrix 擴充</span><span class="sxs-lookup"><span data-stu-id="b64b6-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="b64b6-113">這個版本會更新 NuGet 用戶端到 WebMatrix 中找到[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，並使它 XDT 轉換等的功能。</span><span class="sxs-lookup"><span data-stu-id="b64b6-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="b64b6-114">更重要的是，2.6.1 核心更新可以讓 WebMatrix 用戶端安裝 NuGet 封裝，其中包含較新版本`.nuspec`結構描述，包括 ASP.NET NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="b64b6-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="b64b6-115">如需 WebMatrix 的擴充功能更新的詳細資訊，請參閱這些特定[版本資訊](../release-notes/nuget-2.6.1-for-WebMatrix.md)。</span><span class="sxs-lookup"><span data-stu-id="b64b6-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="b64b6-116">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="b64b6-116">Bug Fixes</span></span>
<span data-ttu-id="b64b6-117">除了這些功能，這個版本的 NuGet 會包括其他 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="b64b6-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="b64b6-118">有一些版本中解決的 16 總問題。</span><span class="sxs-lookup"><span data-stu-id="b64b6-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="b64b6-119">如需完整清單的工作項目固定在 NuGet 2.8.1，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="b64b6-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="b64b6-120">Reshipping 與 Visual Studio"14"CTP</span><span class="sxs-lookup"><span data-stu-id="b64b6-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="b64b6-121">在 Visual Studio"14"CTP 3 2014 年 6 月發行中，NuGet 2.8.1 是箱子運送。</span><span class="sxs-lookup"><span data-stu-id="b64b6-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="b64b6-122">它支援那些功能仍會在長條上方與其他 2.8.1 VSIXes，例如 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="b64b6-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
