---
title: "NuGet 3.3 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.3 的版本資訊。"
keywords: "NuGet 3.3 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c83f87231497e14c36f1b8100b7bec720bb63b1c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="cafac-104">NuGet 3.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="cafac-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="cafac-105">[NuGet 3.2.1 版本資訊](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 版本資訊](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="cafac-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="cafac-106">NuGet 3.3 發行 2015 年 11 月 30 日與大量的使用者介面更新和命令列的功能，以及有助於修正 NuGet 用戶端的集合。</span><span class="sxs-lookup"><span data-stu-id="cafac-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="cafac-107">新功能</span><span class="sxs-lookup"><span data-stu-id="cafac-107">New Features</span></span>

* <span data-ttu-id="cafac-108">已引進，允許 NuGet 命令列用戶端可以緊密地與已驗證的摘要使用認證提供者。</span><span class="sxs-lookup"><span data-stu-id="cafac-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="cafac-109">[指示如何安裝 Visual Studio Team Services 認證提供者](../API/nuget-exe-Credential-Providers.md)及設定 NuGet 用戶端使用其可用的 NuGet 文件。</span><span class="sxs-lookup"><span data-stu-id="cafac-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../API/nuget-exe-Credential-Providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="cafac-110">新的使用者介面功能</span><span class="sxs-lookup"><span data-stu-id="cafac-110">New User Interface Features</span></span>

* <span data-ttu-id="cafac-111">個別的瀏覽、 安裝和更新可用索引標籤</span><span class="sxs-lookup"><span data-stu-id="cafac-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="cafac-112">更新可用徽章表示封裝名稱中有可用的更新數目</span><span class="sxs-lookup"><span data-stu-id="cafac-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="cafac-113">封裝徽章指出封裝是否已安裝的套件清單中或已有可用更新</span><span class="sxs-lookup"><span data-stu-id="cafac-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="cafac-114">下載計數和作者加入至封裝清單</span><span class="sxs-lookup"><span data-stu-id="cafac-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="cafac-115">最高可用的版本號碼和封裝清單目前安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="cafac-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="cafac-116">動作按鈕，以允許快速安裝、 更新及解除安裝的套件清單</span><span class="sxs-lookup"><span data-stu-id="cafac-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="cafac-117">封裝詳細資料面板上更清楚的動作按鈕</span><span class="sxs-lookup"><span data-stu-id="cafac-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="cafac-118">封裝詳細資料面板上的套件更新日期</span><span class="sxs-lookup"><span data-stu-id="cafac-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="cafac-119">合併方案檢視中的面板</span><span class="sxs-lookup"><span data-stu-id="cafac-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="cafac-120">可排序方格中的專案和方案 檢視的已安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="cafac-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="cafac-121">命令列的新功能</span><span class="sxs-lookup"><span data-stu-id="cafac-121">New Command-line Features</span></span>

<span data-ttu-id="cafac-122">此版本引進`add`和`init`初始化資料夾為基礎儲存機制中所述的命令[nuget.exe 參考](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="cafac-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="cafac-123">儲存機制，建構和維護與此資料夾結構將[提供效能優勢明顯](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我們的部落格上所述。</span><span class="sxs-lookup"><span data-stu-id="cafac-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="cafac-124">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="cafac-124">ContentFiles</span></span>

<span data-ttu-id="cafac-125">內容現可支援`project.json`managed 透過新的專案`contentFiles`資料夾和`.nuspec``contentFiles`元素標記法。</span><span class="sxs-lookup"><span data-stu-id="cafac-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="cafac-126">此內容可以更直接指定由封裝作者提供專案系統互動。</span><span class="sxs-lookup"><span data-stu-id="cafac-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="cafac-127">有關如何設定中的 contentFiles 更多資訊`.nuspec`文件位於[.nuspec 參考](../schema/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="cafac-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../schema/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="cafac-128">NuGet 本機快取管理</span><span class="sxs-lookup"><span data-stu-id="cafac-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="cafac-129">NuGet 命令列已更新為包含有關如何管理在工作站上的本機快取的資訊。</span><span class="sxs-lookup"><span data-stu-id="cafac-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="cafac-130">[區域變數] 命令的詳細資訊可用於[NuGet 命令列參照](../tools/cli-ref-locals.md)。</span><span class="sxs-lookup"><span data-stu-id="cafac-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="cafac-131">已修正的問題</span><span class="sxs-lookup"><span data-stu-id="cafac-131">Fixed Issues</span></span>

<span data-ttu-id="cafac-132">**值得注意的問題**</span><span class="sxs-lookup"><span data-stu-id="cafac-132">**Notable Issues**</span></span>

* <span data-ttu-id="cafac-133">NuGet 的命令列還原的支援還原封裝與方案檔上 Mono- [1543年](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="cafac-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="cafac-134">3.3 版本已解決的問題的完整清單可以在 GitHub 上找到[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="cafac-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="cafac-135">在 3.3 命令列的版本中修正問題的清單會記錄在[3.3 命令列里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。</span><span class="sxs-lookup"><span data-stu-id="cafac-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="cafac-136">已知問題</span><span class="sxs-lookup"><span data-stu-id="cafac-136">Known Issues</span></span>

<span data-ttu-id="cafac-137">我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="cafac-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>