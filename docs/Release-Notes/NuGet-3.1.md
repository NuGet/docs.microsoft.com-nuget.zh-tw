---
title: "NuGet 3.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.1 版本資訊。"
keywords: "NuGet 3.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="49a47-104">NuGet 3.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="49a47-104">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="49a47-105">[NuGet 3.0 版本資訊](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 版本資訊](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="49a47-105">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="49a47-106">NuGet 3.1 已發行於 2015 年 7 月 27 日做為通用 Windows 平台 SDK 配套擴充 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="49a47-106">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="49a47-107">我們傳送與 Windows 平台 SDK 的這個版本中，Windows 程式開發體驗無法充分利用先前已啟動的 NuGet 跨平台工作。</span><span class="sxs-lookup"><span data-stu-id="49a47-107">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="49a47-108">此 NuGet 延伸模組版本只適用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="49a47-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="49a47-109">這些開發人員可存取可供使用，我們一律會發佈具有 bug 修正和新功能更新為最新版本的 Visual Studio 組件庫更新建議。</span><span class="sxs-lookup"><span data-stu-id="49a47-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="49a47-110">NuGet Visual Studio 擴充功能</span><span class="sxs-lookup"><span data-stu-id="49a47-110">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="49a47-111">問題和此版本功能會標記與 GitHub 上[「 3.1 RTM UWP 轉移支援 」 里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)總共我們關閉 67 3.1 版本中的問題。</span><span class="sxs-lookup"><span data-stu-id="49a47-111">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="49a47-112">新功能</span><span class="sxs-lookup"><span data-stu-id="49a47-112">New Features</span></span>

* <span data-ttu-id="49a47-113">`project.json`支援 Windows 適用 UWP 和 ASP.NET 5 支援</span><span class="sxs-lookup"><span data-stu-id="49a47-113">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="49a47-114">可轉移的套件安裝</span><span class="sxs-lookup"><span data-stu-id="49a47-114">Transitive package installation</span></span>

<span data-ttu-id="49a47-115">描述與這些功能的定義可以找到其他地方文件中。</span><span class="sxs-lookup"><span data-stu-id="49a47-115">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="49a47-116">已被取代</span><span class="sxs-lookup"><span data-stu-id="49a47-116">Deprecated</span></span>

<span data-ttu-id="49a47-117">下列功能就不再適用於 Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="49a47-117">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="49a47-118">無法再安裝方案層級的套件</span><span class="sxs-lookup"><span data-stu-id="49a47-118">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="49a47-119">下列的功能就不再適用於 Visual Studio 2015 和使用的專案`project.json`規格</span><span class="sxs-lookup"><span data-stu-id="49a47-119">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="49a47-120">`install.ps1`和`uninstall.ps1`-這些指令碼封裝安裝期間將會忽略、 還原、 更新及解除安裝</span><span class="sxs-lookup"><span data-stu-id="49a47-120">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="49a47-121">設定轉換將會被忽略</span><span class="sxs-lookup"><span data-stu-id="49a47-121">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="49a47-122">內容將會執行，但是不會複製到專案。</span><span class="sxs-lookup"><span data-stu-id="49a47-122">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="49a47-123">小組正在重新實作這項功能，請依照下列討論進度： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="49a47-123">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="49a47-124">已知問題</span><span class="sxs-lookup"><span data-stu-id="49a47-124">Known Issues</span></span>

<span data-ttu-id="49a47-125">沒有傳遞此版本的已知問題的數字。</span><span class="sxs-lookup"><span data-stu-id="49a47-125">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="49a47-126">安裝與 Windows 10 SDK 3.1 版本將會降級任何版本的先前已安裝的 NuGet 延伸模組</span><span class="sxs-lookup"><span data-stu-id="49a47-126">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="49a47-127">NuGet 命令列</span><span class="sxs-lookup"><span data-stu-id="49a47-127">NuGet Command-line</span></span>

<span data-ttu-id="49a47-128">NuGet 命令列可執行檔已更新，並移至新的 「 可散布位置，如此 nuget.exe 歷史版本才能繼續可供使用。</span><span class="sxs-lookup"><span data-stu-id="49a47-128">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="49a47-129">您可以下載 Windows 上 nuget.exe 3.1 beta 版： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="49a47-129">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="49a47-130">新的 「 可散布位置位於 dist.nuget.org 主機上，使用此範本會遵循資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="49a47-130">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="49a47-131">新功能</span><span class="sxs-lookup"><span data-stu-id="49a47-131">New Features</span></span>

* <span data-ttu-id="49a47-132">nuget.exe 可以還原，並將封裝安裝到使用專案`project.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="49a47-132">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="49a47-133">nuget.exe 可以連接及取用在 NuGet v3 通訊協定： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="49a47-133">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="49a47-134">已知問題</span><span class="sxs-lookup"><span data-stu-id="49a47-134">Known Issues</span></span> ##

1.    <span data-ttu-id="49a47-135">無法執行組件針對`project.json`檔案- [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="49a47-135">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="49a47-136">不支援單聲道- [1059年](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="49a47-136">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="49a47-137">未當地語系化- [1058年](https://github.com/NuGet/Home/issues/1058)， [1057年](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="49a47-137">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="49a47-138">未簽署，就像現存的 http://nuget.org/nuget.exe- [1073年](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="49a47-138">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
