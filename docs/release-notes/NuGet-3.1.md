---
title: NuGet 3.1 版本資訊
description: NuGet 3.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776528"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="6df05-103">NuGet 3.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="6df05-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="6df05-104">[NuGet 3.0 版本](../release-notes/nuget-3.0.0.md)  |  資訊[NuGet 3.1.1 版本](../release-notes/nuget-3.1.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="6df05-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="6df05-105">NuGet 3.1 已于2015年7月27日發行為通用 Windows 平臺 SDK 的配套延伸模組，可用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="6df05-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="6df05-106">我們已透過 Windows Platform SDK 提供此版本，讓 Windows 開發體驗可以利用先前已啟動的 NuGet 跨平臺工作。</span><span class="sxs-lookup"><span data-stu-id="6df05-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="6df05-107">此 NuGet 擴充功能版本僅適用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="6df05-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="6df05-108">我們建議可存取 Visual Studio 資源庫的開發人員更新為可用的最新版本，因為我們一律會發佈具有 bug 修正和新功能的更新。</span><span class="sxs-lookup"><span data-stu-id="6df05-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="6df05-109">NuGet Visual Studio 擴充功能</span><span class="sxs-lookup"><span data-stu-id="6df05-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="6df05-110">此版本中的問題和功能已在 GitHub 上標記為「 [3.1 RTM UWP 可轉移支援」里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  ，但我們已在3.1 版本中關閉67問題。</span><span class="sxs-lookup"><span data-stu-id="6df05-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="6df05-111">新功能</span><span class="sxs-lookup"><span data-stu-id="6df05-111">New Features</span></span>

* <span data-ttu-id="6df05-112">`project.json` 支援 Windows UWP 和 ASP.NET 5 支援</span><span class="sxs-lookup"><span data-stu-id="6df05-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="6df05-113">可轉移的套件安裝</span><span class="sxs-lookup"><span data-stu-id="6df05-113">Transitive package installation</span></span>

<span data-ttu-id="6df05-114">您可以在檔的其他位置找到這些功能的描述和定義。</span><span class="sxs-lookup"><span data-stu-id="6df05-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="6df05-115">已被取代</span><span class="sxs-lookup"><span data-stu-id="6df05-115">Deprecated</span></span>

<span data-ttu-id="6df05-116">下列功能不再適用于 Visual Studio 2015：</span><span class="sxs-lookup"><span data-stu-id="6df05-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="6df05-117">無法再安裝解決方案層級套件</span><span class="sxs-lookup"><span data-stu-id="6df05-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="6df05-118">下列功能不再適用于 Visual Studio 2015 和使用規格的專案 `project.json`</span><span class="sxs-lookup"><span data-stu-id="6df05-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="6df05-119">`install.ps1` 和 `uninstall.ps1` -在套件安裝、還原、更新和卸載期間，將會忽略這些腳本。</span><span class="sxs-lookup"><span data-stu-id="6df05-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="6df05-120">將忽略設定轉換</span><span class="sxs-lookup"><span data-stu-id="6df05-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="6df05-121">將會攜帶內容，但不會複製到專案中。</span><span class="sxs-lookup"><span data-stu-id="6df05-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="6df05-122">小組正致力於重新執行這項功能，請遵循下列討論和進度： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="6df05-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="6df05-123">已知問題</span><span class="sxs-lookup"><span data-stu-id="6df05-123">Known Issues</span></span>

<span data-ttu-id="6df05-124">此版本提供一些已知問題。</span><span class="sxs-lookup"><span data-stu-id="6df05-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="6df05-125">使用 Windows 10 SDK 安裝3.1 版本將會降級先前安裝的任何 NuGet 擴充功能版本</span><span class="sxs-lookup"><span data-stu-id="6df05-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="6df05-126">NuGet 命令列</span><span class="sxs-lookup"><span data-stu-id="6df05-126">NuGet Command-line</span></span>

<span data-ttu-id="6df05-127">NuGet 命令列可執行檔已更新並移至新的可轉散發位置，讓 nuget.exe 的歷程記錄版本可繼續使用。</span><span class="sxs-lookup"><span data-stu-id="6df05-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="6df05-128">您可以在下列位置下載適用于 Windows 的 3.1 Beta 版 nuget.exe： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="6df05-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="6df05-129">新的可散發位置位於 dist.nuget.org 主機上，其資料夾結構會在此範本之後：</span><span class="sxs-lookup"><span data-stu-id="6df05-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="6df05-130">新功能</span><span class="sxs-lookup"><span data-stu-id="6df05-130">New Features</span></span>

* <span data-ttu-id="6df05-131">nuget.exe 可以將封裝還原並安裝到使用檔案的專案 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="6df05-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="6df05-132">nuget.exe 可以連線至下列位置並使用 NuGet v3 通訊協定： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="6df05-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6df05-133">已知問題</span><span class="sxs-lookup"><span data-stu-id="6df05-133">Known Issues</span></span> ##

1.    <span data-ttu-id="6df05-134">無法針對檔案執行套件 `project.json` - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="6df05-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="6df05-135">Mono- [1059](https://github.com/NuGet/Home/issues/1059)不支援</span><span class="sxs-lookup"><span data-stu-id="6df05-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="6df05-136">未當地語系化- [1058](https://github.com/NuGet/Home/issues/1058)、   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="6df05-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="6df05-137">未簽署，就像現有的 http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)一樣</span><span class="sxs-lookup"><span data-stu-id="6df05-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
