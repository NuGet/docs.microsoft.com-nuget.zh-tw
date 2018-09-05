---
title: NuGet 3.0 RC 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.0 RC 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551715"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="695e7-103">NuGet 3.0 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="695e7-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="695e7-104">[NuGet 3.0 Beta 版本資訊](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 版本資訊](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="695e7-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="695e7-105">NuGet 3.0 RC 於 2015 年 4 月 29 日發行 Visual Studio 2015 RC 版本。</span><span class="sxs-lookup"><span data-stu-id="695e7-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="695e7-106">此版本還有幾個重要的 bug 修正、 效能增強功能和更新以支援新的架構。</span><span class="sxs-lookup"><span data-stu-id="695e7-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="695e7-107">它只適用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="695e7-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="695e7-108">在效能上持續的關注</span><span class="sxs-lookup"><span data-stu-id="695e7-108">Continued Focus on Performance</span></span>

<span data-ttu-id="695e7-109">持續是熱門話題，我們會專注於穩定性和 NuGet 查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="695e7-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="695e7-110">此版本中，您應該開始查看非常快速的搜尋作業中的 NuGet UI 和網站。</span><span class="sxs-lookup"><span data-stu-id="695e7-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="695e7-111">我們正在監視的服務，並使用服務，以便我們可以繼續微調這些作業。</span><span class="sxs-lookup"><span data-stu-id="695e7-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="695e7-112">已解決的重要問題</span><span class="sxs-lookup"><span data-stu-id="695e7-112">Significant Issues Resolved</span></span>

<span data-ttu-id="695e7-113">穩定的 NuGet 用戶端，以便我們可以解決許多問題做為此版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="695e7-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="695e7-114">以下是只有一些更重要的問題已解決的簡短清單：</span><span class="sxs-lookup"><span data-stu-id="695e7-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="695e7-115">隨著 ASP.NET 5 的 K framework 的重新命名的詳細資訊，framework moniker 已更新，以處理 dnx 和 dnxcore[連結](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="695e7-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="695e7-116">從 Visual Studio UI 中的連結新增說明文件[連結](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="695e7-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="695e7-117">更妥善地處理複雜的參考中的`.nuspec`逗號分隔的 framework 參考[連結](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="695e7-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="695e7-118">已修正日文的文化特性的支援[連結](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="695e7-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="695e7-119">更新的用戶端，讓 ASP.NET 5 專案使用新的 v3 端點[連結](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="695e7-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="695e7-120">已更新為較佳的控制代碼與原始檔控制的 packages 資料夾[連結](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="695e7-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="695e7-121">已修正的附屬套件支援[連結](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="695e7-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="695e7-122">已更正的架構特定的內容檔案支援[連結](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="695e7-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="695e7-123">GitHub 存在變革</span><span class="sxs-lookup"><span data-stu-id="695e7-123">GitHub presence overhaul</span></span>

<span data-ttu-id="695e7-124">我們已進行一些變更以我們[原始程式碼儲存機制在 GitHub 上的](http://github.com/nuget/home)。</span><span class="sxs-lookup"><span data-stu-id="695e7-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="695e7-125">如果您有任何問題，與 Visual Studio 的 NuGet 用戶端、 Powershell 命令，或在命令列可執行檔可以記錄這些問題，並上監視其進度我們[首頁 GitHub 存放庫問題清單](http://github.com/nuget/home/issues)。</span><span class="sxs-lookup"><span data-stu-id="695e7-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="695e7-126">我們在追蹤中的資源庫的問題我們[GitHub NuGetGallery 存放庫](http://github.com/nuget/NuGetGallery/issues)。</span><span class="sxs-lookup"><span data-stu-id="695e7-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="695e7-127">敬請期待</span><span class="sxs-lookup"><span data-stu-id="695e7-127">Stay Tuned</span></span>

<span data-ttu-id="695e7-128">請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和 NuGet 3.0 公告 ！</span><span class="sxs-lookup"><span data-stu-id="695e7-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>