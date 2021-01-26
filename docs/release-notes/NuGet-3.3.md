---
title: NuGet 3.3 版本資訊
description: NuGet 3.3 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776513"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="42db7-103">NuGet 3.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="42db7-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="42db7-104">[NuGet 3.2.1 版本](../release-notes/nuget-3.2.1.md)  |  資訊[NuGet 3.4-RC 版本](../release-notes/nuget-3.4-RC.md)資訊</span><span class="sxs-lookup"><span data-stu-id="42db7-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="42db7-105">NuGet 3.3 已于2015年11月30日發行，具有大量的使用者介面更新和命令列功能，以及 NuGet 用戶端的實用修正集合。</span><span class="sxs-lookup"><span data-stu-id="42db7-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="42db7-106">新功能</span><span class="sxs-lookup"><span data-stu-id="42db7-106">New Features</span></span>

* <span data-ttu-id="42db7-107">引進了認證提供者，讓 NuGet 命令列用戶端能夠順暢地使用已驗證的摘要。</span><span class="sxs-lookup"><span data-stu-id="42db7-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="42db7-108">有關[如何安裝 Visual Studio Team Services 認證提供者](../reference/extensibility/nuget-exe-credential-providers.md)，以及設定 nuget 用戶端以使用它的指示，可在 nuget 檔上取得。</span><span class="sxs-lookup"><span data-stu-id="42db7-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="42db7-109">新的消費者介面功能</span><span class="sxs-lookup"><span data-stu-id="42db7-109">New User Interface Features</span></span>

* <span data-ttu-id="42db7-110">個別的 [流覽]、[已安裝] 和 [更新] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="42db7-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="42db7-111">更新可用徽章，指出具有可用更新的套件數目</span><span class="sxs-lookup"><span data-stu-id="42db7-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="42db7-112">套件清單中的套件徽章，指出封裝是否已安裝或有可用的更新</span><span class="sxs-lookup"><span data-stu-id="42db7-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="42db7-113">新增至套件清單的下載計數和作者</span><span class="sxs-lookup"><span data-stu-id="42db7-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="42db7-114">套件清單上的最高可用版本號碼和目前已安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="42db7-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="42db7-115">允許從套件清單快速安裝、更新及卸載的動作按鈕</span><span class="sxs-lookup"><span data-stu-id="42db7-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="42db7-116">套件詳細資料面板上更清楚的動作按鈕</span><span class="sxs-lookup"><span data-stu-id="42db7-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="42db7-117">套件詳細資料面板上的套件更新日期</span><span class="sxs-lookup"><span data-stu-id="42db7-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="42db7-118">方案視圖中的合併面板</span><span class="sxs-lookup"><span data-stu-id="42db7-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="42db7-119">方案視圖上專案的可排序方格和已安裝的版本號碼</span><span class="sxs-lookup"><span data-stu-id="42db7-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="42db7-120">新的命令列功能</span><span class="sxs-lookup"><span data-stu-id="42db7-120">New Command-line Features</span></span>

<span data-ttu-id="42db7-121">在此版本中，我們引進了 `add` 和 `init` 命令來初始化以資料夾為基礎的儲存機制，如 [nuget.exe 參考](../reference/nuget-exe-cli-reference.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="42db7-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="42db7-122">使用此資料夾結構所建立和維護的存放庫，會 [提供重要的效能優勢](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) ，如我們的 blog 所述。</span><span class="sxs-lookup"><span data-stu-id="42db7-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="42db7-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="42db7-123">ContentFiles</span></span>

<span data-ttu-id="42db7-124">`project.json`Managed 專案現在會透過新的 `contentFiles` 資料夾和 `.nuspec` `contentFiles` 元素標記法來支援內容。</span><span class="sxs-lookup"><span data-stu-id="42db7-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="42db7-125">封裝作者可以直接指定此內容，以便與專案系統互動。</span><span class="sxs-lookup"><span data-stu-id="42db7-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="42db7-126">如需有關如何在檔中設定 contentFiles 的詳細資訊， `.nuspec` 請參閱 [nuspec 參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="42db7-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="42db7-127">NuGet 區域變數快取管理</span><span class="sxs-lookup"><span data-stu-id="42db7-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="42db7-128">已更新 NuGet 命令列，以包含如何在工作站上管理本機快取的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="42db7-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="42db7-129">有關 [區域變數] 命令的詳細資訊可在 [NuGet 命令列參考](../reference/cli-reference/cli-ref-locals.md)中取得。</span><span class="sxs-lookup"><span data-stu-id="42db7-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="42db7-130">已修正的問題</span><span class="sxs-lookup"><span data-stu-id="42db7-130">Fixed Issues</span></span>

<span data-ttu-id="42db7-131">**值得注意的問題**</span><span class="sxs-lookup"><span data-stu-id="42db7-131">**Notable Issues**</span></span>

* <span data-ttu-id="42db7-132">NuGet 命令列還原支援在 Mono- [1543](https://github.com/NuGet/Home/issues/1543)上使用方案檔還原套件</span><span class="sxs-lookup"><span data-stu-id="42db7-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="42db7-133">3.3 版中所解決問題的完整清單可在 GitHub 的 [3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)下找到。</span><span class="sxs-lookup"><span data-stu-id="42db7-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="42db7-134">3.3 命令列版本中修正的問題清單會記錄在 [3.3 Command-Line 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)中。</span><span class="sxs-lookup"><span data-stu-id="42db7-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="42db7-135">已知問題</span><span class="sxs-lookup"><span data-stu-id="42db7-135">Known Issues</span></span>

<span data-ttu-id="42db7-136">我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="42db7-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>