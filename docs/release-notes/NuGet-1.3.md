---
title: NuGet 1.3 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.3 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551347"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="41175-103">NuGet 1.3 的版本資訊</span><span class="sxs-lookup"><span data-stu-id="41175-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="41175-104">[NuGet 1.2 版本資訊](../release-notes/nuget-1.2.md) | [NuGet 1.4 版本資訊](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="41175-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="41175-105">於 2011 年 4 月 25 日發行 NuGet 1.3。</span><span class="sxs-lookup"><span data-stu-id="41175-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="41175-106">新功能</span><span class="sxs-lookup"><span data-stu-id="41175-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="41175-107">簡化的封裝建立符號伺服器整合</span><span class="sxs-lookup"><span data-stu-id="41175-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="41175-108">NuGet 小組合作的人一定[SymbolSource.org](http://www.symbolsource.org/)來提供一個非常簡單的方式，以及您的套件，發佈您的來源和 PDB。</span><span class="sxs-lookup"><span data-stu-id="41175-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="41175-109">這可讓您的套件的取用者，逐步執行偵錯工具在您套件的來源。</span><span class="sxs-lookup"><span data-stu-id="41175-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="41175-110">如需詳細資訊，請參閱[建立和發行符號套件](../create-packages/symbol-packages.md)發行 NuGet 套件來源使用簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="41175-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="41175-111">您也可以觀看的現場示範這項功能的一部分深入了解 NuGet 在 Mix11 討論。</span><span class="sxs-lookup"><span data-stu-id="41175-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="41175-112">這項功能是完整的 8:27 開始示範影片的 20 分鐘標記處。</span><span class="sxs-lookup"><span data-stu-id="41175-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="41175-113">`Open-PackagePage` 命令</span><span class="sxs-lookup"><span data-stu-id="41175-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="41175-114">此命令可讓您能夠輕鬆地在套件管理員主控台 內從封裝的專案頁面。</span><span class="sxs-lookup"><span data-stu-id="41175-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="41175-115">它也提供選項，以開啟 授權 URL 及報表內容粗俗的文章頁面，為套件。</span><span class="sxs-lookup"><span data-stu-id="41175-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="41175-116">命令的語法是：</span><span class="sxs-lookup"><span data-stu-id="41175-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="41175-117">`-PassThru`選項用來傳回所指定 URL 的值。</span><span class="sxs-lookup"><span data-stu-id="41175-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="41175-118">例如：</span><span class="sxs-lookup"><span data-stu-id="41175-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="41175-119">開啟瀏覽器並前往 Ninject 封裝中指定的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="41175-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="41175-120">開啟瀏覽器並前往 Ninject 封裝中指定的授權 URL。</span><span class="sxs-lookup"><span data-stu-id="41175-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="41175-121">將瀏覽器開啟至目前的封裝來源來指定封裝的 檢舉不當使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="41175-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="41175-122">指派給變數，也就是 $url，授權 URL，而不需要在瀏覽器中開啟 URL。</span><span class="sxs-lookup"><span data-stu-id="41175-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="41175-123">效能改善</span><span class="sxs-lookup"><span data-stu-id="41175-123">Performance Improvements</span></span>

<span data-ttu-id="41175-124">NuGet 1.3 導入了許多效能改善。</span><span class="sxs-lookup"><span data-stu-id="41175-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="41175-125">NuGet 1.3 以避免多次下載相同版本的封裝，包含的每個使用者的本機快取。</span><span class="sxs-lookup"><span data-stu-id="41175-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="41175-126">可以存取和透過 [套件管理員設定] 對話方塊中清除快取：</span><span class="sxs-lookup"><span data-stu-id="41175-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![NuGet 套件快取設定的選項 對話方塊](./media/nuget-options.png)

<span data-ttu-id="41175-128">其他效能改進功能包括新增支援 HTTP 壓縮，以及改善 Visual Studio 內的套件安裝速度。</span><span class="sxs-lookup"><span data-stu-id="41175-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="41175-129">Visual Studio 和 nuget.exe 會使用相同的套件來源清單</span><span class="sxs-lookup"><span data-stu-id="41175-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="41175-130">NuGet 1.3 之前的 nuget.exe 與 NuGet Visual Studio 增益集所使用的套件來源清單已不會儲存在相同的位置。</span><span class="sxs-lookup"><span data-stu-id="41175-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="41175-131">NuGet 1.3 現在會在兩個位置使用相同的清單。</span><span class="sxs-lookup"><span data-stu-id="41175-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="41175-132">清單儲存在`NuGet.Config`並儲存在 [AppData] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="41175-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="41175-133">nuget.exe 會忽略的檔案和資料夾，以開頭 '。 ' 預設</span><span class="sxs-lookup"><span data-stu-id="41175-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="41175-134">為了讓這類 Subversion 和 mercurial 都會處理與原始檔控制系統的 NuGet，nuget.exe 會忽略資料夾和檔案的開頭 '。 ' 字元建立封裝時。</span><span class="sxs-lookup"><span data-stu-id="41175-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="41175-135">這可以使用覆寫兩個新旗標：</span><span class="sxs-lookup"><span data-stu-id="41175-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="41175-136">__-NoDefaultExcludes__用來覆寫此設定，並包含所有檔案。</span><span class="sxs-lookup"><span data-stu-id="41175-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="41175-137">__-排除__用來新增其他檔案/資料夾排除使用模式。</span><span class="sxs-lookup"><span data-stu-id="41175-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="41175-138">例如，若要排除 '.bak' 副檔名的所有檔案</span><span class="sxs-lookup"><span data-stu-id="41175-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="41175-139">_注意： 模式不是預設的遞迴。_</span><span class="sxs-lookup"><span data-stu-id="41175-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="41175-140">WiX 專案和.NET Micro Framework 支援</span><span class="sxs-lookup"><span data-stu-id="41175-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="41175-141">由於社群貢獻，NuGet 會包含 WiX 專案類型，以及.NET Micro Framework 的支援。</span><span class="sxs-lookup"><span data-stu-id="41175-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="41175-142">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="41175-142">Bug Fixes</span></span>

<span data-ttu-id="41175-143">Bug 修正的完整清單，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="41175-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="41175-144">值得注意的錯誤修正</span><span class="sxs-lookup"><span data-stu-id="41175-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="41175-145">與原始程式檔的套件運作在這兩個網站和 Web 應用程式專案中。</span><span class="sxs-lookup"><span data-stu-id="41175-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="41175-146">原始程式檔複製到網站，`App_Code`資料夾</span><span class="sxs-lookup"><span data-stu-id="41175-146">For Websites, source files are copied into the `App_Code` folder</span></span>
