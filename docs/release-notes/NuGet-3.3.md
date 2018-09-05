---
title: NuGet 3.3 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.3 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546643"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="63c54-103">NuGet 3.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="63c54-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="63c54-104">[NuGet 3.2.1 版本資訊](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 版本資訊](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="63c54-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="63c54-105">NuGet 3.3 已發行 2015 年 11 月 30 日的大量的使用者介面更新和命令列功能，以及有助於修正 NuGet 用戶端的集合。</span><span class="sxs-lookup"><span data-stu-id="63c54-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="63c54-106">新功能</span><span class="sxs-lookup"><span data-stu-id="63c54-106">New Features</span></span>

* <span data-ttu-id="63c54-107">已引進，讓能夠完美搭配的已驗證摘要的 NuGet 命令列用戶端認證提供者。</span><span class="sxs-lookup"><span data-stu-id="63c54-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="63c54-108">[有關如何安裝 Visual Studio Team Services 的認證提供者](../api/nuget-exe-credential-providers.md)並設定 NuGet 使用的用戶端均可在 NuGet 文件。</span><span class="sxs-lookup"><span data-stu-id="63c54-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="63c54-109">新的使用者介面功能</span><span class="sxs-lookup"><span data-stu-id="63c54-109">New User Interface Features</span></span>

* <span data-ttu-id="63c54-110">不同的瀏覽、 安裝和更新可用索引標籤</span><span class="sxs-lookup"><span data-stu-id="63c54-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="63c54-111">更新可用的徽章，表示封裝名稱中有可用的更新數目</span><span class="sxs-lookup"><span data-stu-id="63c54-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="63c54-112">表示如果封裝已安裝，或有可用更新的套件清單中的套件徽章</span><span class="sxs-lookup"><span data-stu-id="63c54-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="63c54-113">下載計數和作者新增至套件清單</span><span class="sxs-lookup"><span data-stu-id="63c54-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="63c54-114">最高可用的版本號碼和套件清單上的目前安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="63c54-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="63c54-115">動作按鈕，以允許快速安裝、 更新及解除安裝的套件清單</span><span class="sxs-lookup"><span data-stu-id="63c54-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="63c54-116">封裝詳細資料 面板上更清楚的動作按鈕</span><span class="sxs-lookup"><span data-stu-id="63c54-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="63c54-117">封裝詳細資料 面板上的封裝更新日期</span><span class="sxs-lookup"><span data-stu-id="63c54-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="63c54-118">合併方案 檢視中的面板</span><span class="sxs-lookup"><span data-stu-id="63c54-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="63c54-119">可排序方格中的專案和方案 檢視的已安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="63c54-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="63c54-120">命令列的新功能</span><span class="sxs-lookup"><span data-stu-id="63c54-120">New Command-line Features</span></span>

<span data-ttu-id="63c54-121">此版本引進`add`並`init`命令，以初始化資料夾為基礎的存放庫中所述[nuget.exe 參考](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="63c54-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="63c54-122">存放庫，建構和維護與此資料夾結構將會[提供效能優勢明顯](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我們的部落格上所述。</span><span class="sxs-lookup"><span data-stu-id="63c54-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="63c54-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="63c54-123">ContentFiles</span></span>

<span data-ttu-id="63c54-124">現在支援內容`project.json`管理透過新的專案`contentFiles`資料夾並`.nuspec``contentFiles`元素標記法。</span><span class="sxs-lookup"><span data-stu-id="63c54-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="63c54-125">此內容也可以更直接指定由封裝作者與專案系統互動。</span><span class="sxs-lookup"><span data-stu-id="63c54-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="63c54-126">詳細資訊，有關如何設定中的 contentFiles`.nuspec`文件可在[.nuspec 參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="63c54-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="63c54-127">NuGet 區域變數快取管理</span><span class="sxs-lookup"><span data-stu-id="63c54-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="63c54-128">NuGet 命令列已更新為包括如何管理的工作站上的本機快取的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="63c54-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="63c54-129">Locals 命令的詳細資訊位於[NuGet 命令列參考](../tools/cli-ref-locals.md)。</span><span class="sxs-lookup"><span data-stu-id="63c54-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="63c54-130">已修正的問題</span><span class="sxs-lookup"><span data-stu-id="63c54-130">Fixed Issues</span></span>

<span data-ttu-id="63c54-131">**值得注意的問題**</span><span class="sxs-lookup"><span data-stu-id="63c54-131">**Notable Issues**</span></span>

* <span data-ttu-id="63c54-132">NuGet 命令列還原的支援還原套件在 Mono-方案檔[1543年](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="63c54-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="63c54-133">3.3 版的版本中已解決的問題的完整清單可在 GitHub 上[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="63c54-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="63c54-134">3.3 的命令列版本中修正的問題的清單中會記錄[3.3 的命令列里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。</span><span class="sxs-lookup"><span data-stu-id="63c54-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="63c54-135">已知問題</span><span class="sxs-lookup"><span data-stu-id="63c54-135">Known Issues</span></span>

<span data-ttu-id="63c54-136">我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="63c54-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>