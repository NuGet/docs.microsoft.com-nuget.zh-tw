---
title: NuGet 3.0 RC 版本資訊
description: NuGet 3.0 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776575"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="4864d-103">NuGet 3.0 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="4864d-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="4864d-104">[NuGet 3.0 Beta 版注意事項](../release-notes/nuget-3.0-beta.md)  | [NuGet 3.0 RC2 版本](../release-notes/nuget-3.0-RC2.md)資訊</span><span class="sxs-lookup"><span data-stu-id="4864d-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="4864d-105">NuGet 3.0 RC 已于2015年4月29日發行，Visual Studio 2015 RC 版本。</span><span class="sxs-lookup"><span data-stu-id="4864d-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="4864d-106">此版本有許多重要的 bug 修正、效能改進和更新，以支援新的架構。</span><span class="sxs-lookup"><span data-stu-id="4864d-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="4864d-107">它僅適用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="4864d-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="4864d-108">繼續專注于效能</span><span class="sxs-lookup"><span data-stu-id="4864d-108">Continued Focus on Performance</span></span>

<span data-ttu-id="4864d-109">NuGet 查詢的穩定性和效能會持續成為我們所關注的熱門主題。</span><span class="sxs-lookup"><span data-stu-id="4864d-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="4864d-110">在此版本中，您應該會開始在 NuGet UI 和網站中看到非常快速的搜尋作業。</span><span class="sxs-lookup"><span data-stu-id="4864d-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="4864d-111">我們正在監視服務以及您使用服務的方式，讓我們可以繼續調整這些作業。</span><span class="sxs-lookup"><span data-stu-id="4864d-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="4864d-112">已解決重大問題</span><span class="sxs-lookup"><span data-stu-id="4864d-112">Significant Issues Resolved</span></span>

<span data-ttu-id="4864d-113">為了穩定 NuGet 用戶端，我們在此版本中解決了許多問題。</span><span class="sxs-lookup"><span data-stu-id="4864d-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="4864d-114">以下是已解決的一些更重要問題的簡短清單：</span><span class="sxs-lookup"><span data-stu-id="4864d-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="4864d-115">在 ASP.NET 5 的 K 架構重新命名過程中，架構的名字標記已更新為可處理 dnx 和 dnxcore [連結](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="4864d-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="4864d-116">在 Visual Studio UI[連結](https://github.com/NuGet/Home/issues/232)中新增連結的說明文件</span><span class="sxs-lookup"><span data-stu-id="4864d-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="4864d-117">`.nuspec`使用以逗號分隔的架構參考[連結](https://github.com/NuGet/Home/issues/276)，更有效地處理中的複雜參考</span><span class="sxs-lookup"><span data-stu-id="4864d-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="4864d-118">已修正日文文化特性[連結](https://github.com/NuGet/Home/issues/253)的支援</span><span class="sxs-lookup"><span data-stu-id="4864d-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="4864d-119">已更新用戶端，以允許 ASP.NET 5 專案使用新的 v3 端點 [連結](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="4864d-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="4864d-120">已更新為使用原始檔控制[連結](https://github.com/NuGet/Home/issues/56)更妥善處理套件資料夾</span><span class="sxs-lookup"><span data-stu-id="4864d-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="4864d-121">已修正附屬套件[連結](https://github.com/NuGet/Home/issues/17)的支援</span><span class="sxs-lookup"><span data-stu-id="4864d-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="4864d-122">已更正架構特定內容檔案[連結](https://github.com/NuGet/Home/issues/18)的支援</span><span class="sxs-lookup"><span data-stu-id="4864d-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="4864d-123">GitHub 狀態檢驗</span><span class="sxs-lookup"><span data-stu-id="4864d-123">GitHub presence overhaul</span></span>

<span data-ttu-id="4864d-124">我們已對 [GitHub 上的原始程式碼存放庫](http://github.com/nuget/home)進行一些變更。</span><span class="sxs-lookup"><span data-stu-id="4864d-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="4864d-125">如果您有 NuGet Visual Studio 用戶端、Powershell 命令或命令列可執行檔的任何問題，您可以記錄這些問題，並在 [GitHub 首頁存放庫問題清單](http://github.com/nuget/home/issues)上監視其進度。</span><span class="sxs-lookup"><span data-stu-id="4864d-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="4864d-126">我們在 [GitHub NuGetGallery 存放庫](http://github.com/nuget/NuGetGallery/issues)中追蹤資源庫的問題。</span><span class="sxs-lookup"><span data-stu-id="4864d-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="4864d-127">持續關注</span><span class="sxs-lookup"><span data-stu-id="4864d-127">Stay Tuned</span></span>

<span data-ttu-id="4864d-128">請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多 NuGet 3.0 的進度和公告！</span><span class="sxs-lookup"><span data-stu-id="4864d-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>