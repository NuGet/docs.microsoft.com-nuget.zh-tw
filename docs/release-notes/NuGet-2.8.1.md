---
title: NuGet 2.8.1 版本資訊
description: NuGet 2.8.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776762"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="1a234-103">NuGet 2.8.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="1a234-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="1a234-104">[NuGet 2.8 版本](../release-notes/nuget-2.8.md)  |  資訊[NuGet 2.8.2 版本](../release-notes/nuget-2.8.2.md)資訊</span><span class="sxs-lookup"><span data-stu-id="1a234-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="1a234-105">NuGet 2.8.1 發行于2014年4月2日。</span><span class="sxs-lookup"><span data-stu-id="1a234-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="1a234-106">版本中的值得注意功能</span><span class="sxs-lookup"><span data-stu-id="1a234-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="1a234-107">支援 Windows Phone 8.1 專案</span><span class="sxs-lookup"><span data-stu-id="1a234-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="1a234-108">此版本現在支援下列新的目標 framework 名字標記，可用來將 Windows Phone 8.1 專案設為目標：</span><span class="sxs-lookup"><span data-stu-id="1a234-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="1a234-109">以 Silverlight 為基礎的 Windows Phone 專案的 WindowsPhone81/WP81 () </span><span class="sxs-lookup"><span data-stu-id="1a234-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="1a234-110">以 WinRT 為基礎 Windows Phone 應用程式專案的 WindowsPhoneApp81/WPA81 () </span><span class="sxs-lookup"><span data-stu-id="1a234-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="1a234-111">NuGet WebMatrix 擴充功能的更新</span><span class="sxs-lookup"><span data-stu-id="1a234-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="1a234-112">此版本會將 WebMatrix 中找到的 NuGet 用戶端更新為 [nuget.exe](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，並引進 XDT 轉換等 it 功能。</span><span class="sxs-lookup"><span data-stu-id="1a234-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="1a234-113">更重要的是，2.6.1 core 更新可讓 WebMatrix 用戶端安裝 NuGet 套件，其中包含最新版本的 `.nuspec` 架構，包括 ASP.NET NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="1a234-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="1a234-114">如需有關 WebMatrix 擴充功能更新的詳細資訊，請參閱這些特定的 [版本](../release-notes/nuget-2.6.1-for-WebMatrix.md)資訊。</span><span class="sxs-lookup"><span data-stu-id="1a234-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="1a234-115">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="1a234-115">Bug Fixes</span></span>
<span data-ttu-id="1a234-116">除了這些功能之外，此版本的 NuGet 還包含其他 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="1a234-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="1a234-117">發行中已解決16個問題。</span><span class="sxs-lookup"><span data-stu-id="1a234-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="1a234-118">如需 NuGet 2.8.1 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="1a234-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="1a234-119">Visual Studio "14" CTP 的 Reshipping</span><span class="sxs-lookup"><span data-stu-id="1a234-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="1a234-120">在2014年6月3日發行的 Visual Studio "14" CTP 中，NuGet 2.8.1 隨附于 box。</span><span class="sxs-lookup"><span data-stu-id="1a234-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="1a234-121">It 支援的功能與其他 2.8.1 VSIXes （例如 Visual Studio 2013）保持不變。</span><span class="sxs-lookup"><span data-stu-id="1a234-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
