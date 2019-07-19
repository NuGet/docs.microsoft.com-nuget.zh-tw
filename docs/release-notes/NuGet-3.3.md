---
title: NuGet 3.3 版本資訊
description: NuGet 3.3 的版本資訊, 包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317033"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="f0526-103">NuGet 3.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="f0526-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="f0526-104">[Nuget 3.2.1 版本](../release-notes/nuget-3.2.1.md) | 資訊[nuget 3.4-RC 版本](../release-notes/nuget-3.4-RC.md)資訊</span><span class="sxs-lookup"><span data-stu-id="f0526-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="f0526-105">NuGet 3.3 已于2015年11月30日發行, 其中有大量的使用者介面更新和命令列功能, 以及對 NuGet 用戶端有用的修正集合。</span><span class="sxs-lookup"><span data-stu-id="f0526-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="f0526-106">新功能</span><span class="sxs-lookup"><span data-stu-id="f0526-106">New Features</span></span>

* <span data-ttu-id="f0526-107">已引進認證提供者, 可讓 NuGet 命令列用戶端能夠順暢地與已驗證的摘要搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f0526-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="f0526-108">有關[如何安裝 Visual Studio Team Services 認證提供者](../api/nuget-exe-credential-providers.md), 以及如何設定 nuget 用戶端來使用它的指示, 可在 nuget 檔中取得。</span><span class="sxs-lookup"><span data-stu-id="f0526-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="f0526-109">新的使用者介面功能</span><span class="sxs-lookup"><span data-stu-id="f0526-109">New User Interface Features</span></span>

* <span data-ttu-id="f0526-110">分隔 [流覽]、[已安裝] 和 [更新可用] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="f0526-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="f0526-111">更新可用的徽章, 指出有可用更新的套件數目</span><span class="sxs-lookup"><span data-stu-id="f0526-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="f0526-112">封裝清單中的套件徽章, 指出套件是否已安裝, 或是否有可用的更新</span><span class="sxs-lookup"><span data-stu-id="f0526-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="f0526-113">將下載計數和作者新增至套件清單</span><span class="sxs-lookup"><span data-stu-id="f0526-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="f0526-114">套件清單上的最高可用版本號碼和目前安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="f0526-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="f0526-115">允許從套件清單快速安裝、更新及卸載的動作按鈕</span><span class="sxs-lookup"><span data-stu-id="f0526-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="f0526-116">套件詳細資料面板上的動作按鈕更清楚</span><span class="sxs-lookup"><span data-stu-id="f0526-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="f0526-117">封裝詳細資料面板上的套件更新日期</span><span class="sxs-lookup"><span data-stu-id="f0526-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="f0526-118">解決方案視圖中的合併面板</span><span class="sxs-lookup"><span data-stu-id="f0526-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="f0526-119">解決方案視圖上專案的可排序方格和已安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="f0526-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="f0526-120">新的命令列功能</span><span class="sxs-lookup"><span data-stu-id="f0526-120">New Command-line Features</span></span>

<span data-ttu-id="f0526-121">在此版本中, 我們`add`引進`init`了和命令來初始化以資料夾為基礎的存放庫, 如[nuget.exe 參考](../reference/nuget-exe-cli-reference.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="f0526-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="f0526-122">使用此資料夾結構來建立和維護的存放庫, 將可[提供更明顯的效能優勢](http://blog.nuget.org/20150922/Accelerate-Package-Source.html), 如我們的 blog 所述。</span><span class="sxs-lookup"><span data-stu-id="f0526-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="f0526-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="f0526-123">ContentFiles</span></span>

<span data-ttu-id="f0526-124">`project.json`受控專案現在透過新`contentFiles`的資料夾和`.nuspec` `contentFiles`元素標記法支援內容。</span><span class="sxs-lookup"><span data-stu-id="f0526-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="f0526-125">封裝作者可以直接指定此內容, 以便與專案系統互動。</span><span class="sxs-lookup"><span data-stu-id="f0526-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="f0526-126">如需如何在`.nuspec`檔中設定 contentFiles 的詳細資訊, 請參閱[nuspec 參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="f0526-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="f0526-127">NuGet 區域變數快取管理</span><span class="sxs-lookup"><span data-stu-id="f0526-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="f0526-128">NuGet 命令列已更新為包含如何在工作站上管理本機快取的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f0526-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="f0526-129">有關 [區域變數] 命令的詳細資訊可在[NuGet 命令列參考](../reference/cli-reference/cli-ref-locals.md)中取得。</span><span class="sxs-lookup"><span data-stu-id="f0526-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="f0526-130">已修正問題</span><span class="sxs-lookup"><span data-stu-id="f0526-130">Fixed Issues</span></span>

<span data-ttu-id="f0526-131">**值得注意的問題**</span><span class="sxs-lookup"><span data-stu-id="f0526-131">**Notable Issues**</span></span>

* <span data-ttu-id="f0526-132">NuGet 命令列還原支援在 Mono- [1543](https://github.com/NuGet/Home/issues/1543)上使用方案檔還原套件</span><span class="sxs-lookup"><span data-stu-id="f0526-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="f0526-133">3\.3 版本中所解決問題的完整清單可在 GitHub 的[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)下找到。</span><span class="sxs-lookup"><span data-stu-id="f0526-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="f0526-134">3\.3 命令列版本中已修正的問題清單會記錄在[3.3 命令列里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)中。</span><span class="sxs-lookup"><span data-stu-id="f0526-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="f0526-135">已知問題</span><span class="sxs-lookup"><span data-stu-id="f0526-135">Known Issues</span></span>

<span data-ttu-id="f0526-136">我們會繼續追蹤 GitHub 問題清單的問題, 可以在下列位置找到:[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="f0526-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>