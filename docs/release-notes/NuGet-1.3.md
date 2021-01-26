---
title: NuGet 1.3 版本資訊
description: NuGet 1.3 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777121"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="5b23c-103">NuGet 1.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="5b23c-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="5b23c-104">[NuGet 1.2 版本](../release-notes/nuget-1.2.md)  |  資訊[NuGet 1.4 版本](../release-notes/nuget-1.4.md)資訊</span><span class="sxs-lookup"><span data-stu-id="5b23c-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="5b23c-105">NuGet 1.3 已于2011年4月25日發行。</span><span class="sxs-lookup"><span data-stu-id="5b23c-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="5b23c-106">新功能</span><span class="sxs-lookup"><span data-stu-id="5b23c-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="5b23c-107">使用符號伺服器整合簡化套件建立</span><span class="sxs-lookup"><span data-stu-id="5b23c-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="5b23c-108">NuGet 團隊與 [SymbolSource.org](http://www.symbolsource.org/) 的人員合作，提供一種非常簡單的方式來發佈您的來源和 PDB 以及套件。</span><span class="sxs-lookup"><span data-stu-id="5b23c-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="5b23c-109">這可讓您封裝的取用者在偵錯工具中逐步執行封裝的來源。</span><span class="sxs-lookup"><span data-stu-id="5b23c-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="5b23c-110">如需更多詳細資料，請參閱 [建立和發佈符號套件](../create-packages/symbol-packages.md) 的簡易方式，可讓您輕鬆地發佈具有來源的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="5b23c-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="5b23c-111">您也可以觀看這項功能的實況示範，作為 NuGet 深入探討 Mix11 的一部分。</span><span class="sxs-lookup"><span data-stu-id="5b23c-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="5b23c-112">這項功能已從影片的20分鐘標示開始完整示範。</span><span class="sxs-lookup"><span data-stu-id="5b23c-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="5b23c-113">`Open-PackagePage` 命令</span><span class="sxs-lookup"><span data-stu-id="5b23c-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="5b23c-114">此命令可讓您輕鬆地從封裝管理員主控台中，取得封裝的 [專案] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5b23c-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="5b23c-115">它也提供選項來開啟封裝的授權 URL 和 [報告不當] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5b23c-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="5b23c-116">命令的語法為：</span><span class="sxs-lookup"><span data-stu-id="5b23c-116">The syntax for the command is:</span></span>

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

<span data-ttu-id="5b23c-117">`-PassThru`選項是用來傳回指定之 URL 的值。</span><span class="sxs-lookup"><span data-stu-id="5b23c-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="5b23c-118">範例：</span><span class="sxs-lookup"><span data-stu-id="5b23c-118">Examples:</span></span>

```
PM> Open-PackagePage Ninject
```

<span data-ttu-id="5b23c-119">將瀏覽器開啟至 Ninject 封裝中指定的專案 URL。</span><span class="sxs-lookup"><span data-stu-id="5b23c-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -License
```

<span data-ttu-id="5b23c-120">開啟瀏覽器至 Ninject 封裝中指定的授權 URL。</span><span class="sxs-lookup"><span data-stu-id="5b23c-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -ReportAbuse
```

<span data-ttu-id="5b23c-121">開啟瀏覽器，指向目前套件來源的 URL，此 URL 是用來報告指定封裝的濫用。</span><span class="sxs-lookup"><span data-stu-id="5b23c-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

<span data-ttu-id="5b23c-122">將授權 URL 指派給變數 $url，而不在瀏覽器中開啟 URL。</span><span class="sxs-lookup"><span data-stu-id="5b23c-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="5b23c-123">效能改進</span><span class="sxs-lookup"><span data-stu-id="5b23c-123">Performance Improvements</span></span>

<span data-ttu-id="5b23c-124">NuGet 1.3 引進了許多效能改進。</span><span class="sxs-lookup"><span data-stu-id="5b23c-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="5b23c-125">NuGet 1.3 包含本機的每個使用者快取，可避免多次下載相同版本的套件。</span><span class="sxs-lookup"><span data-stu-id="5b23c-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="5b23c-126">您可以透過 [封裝管理員設定] 對話方塊來存取和清除快取：</span><span class="sxs-lookup"><span data-stu-id="5b23c-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![具有套件快取設定的 NuGet 選項對話方塊](./media/nuget-options.png)

<span data-ttu-id="5b23c-128">其他效能改進包括新增 HTTP 壓縮的支援，以及改善 Visual Studio 內的套件安裝速度。</span><span class="sxs-lookup"><span data-stu-id="5b23c-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="5b23c-129">Visual Studio 和 nuget.exe 使用相同的套件來源清單</span><span class="sxs-lookup"><span data-stu-id="5b23c-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="5b23c-130">在 NuGet 1.3 之前，nuget.exe 和 NuGet Visual Studio Add-In 所使用的套件來源清單，不會儲存在相同的位置。</span><span class="sxs-lookup"><span data-stu-id="5b23c-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="5b23c-131">NuGet 1.3 現在會在這兩個位置中使用相同的清單。</span><span class="sxs-lookup"><span data-stu-id="5b23c-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="5b23c-132">此清單會儲存在中 `NuGet.Config` ，並儲存在 AppData 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5b23c-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="5b23c-133">nuget.exe 忽略以 '. ' 開頭的檔案和資料夾（預設值為 '. '）</span><span class="sxs-lookup"><span data-stu-id="5b23c-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="5b23c-134">為了讓 NuGet 可與原始檔控制系統（例如 Subversion 和 Mercurial）正常搭配運作，nuget.exe 會在建立封裝時忽略以 '. ' 字元開頭的資料夾和檔案。</span><span class="sxs-lookup"><span data-stu-id="5b23c-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="5b23c-135">您可以使用兩個新旗標來覆寫此內容：</span><span class="sxs-lookup"><span data-stu-id="5b23c-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="5b23c-136">__-NoDefaultExcludes__ 用來覆寫此設定並包含所有檔案。</span><span class="sxs-lookup"><span data-stu-id="5b23c-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="5b23c-137">__-Exclude__ 用來新增其他檔案/資料夾，以使用模式來排除。</span><span class="sxs-lookup"><span data-stu-id="5b23c-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="5b23c-138">例如，若要排除所有副檔名為 ' .bak ' 的檔案</span><span class="sxs-lookup"><span data-stu-id="5b23c-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="5b23c-139">_注意：模式預設並非遞迴。_</span><span class="sxs-lookup"><span data-stu-id="5b23c-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="5b23c-140">WiX 專案和 .NET 微架構的支援</span><span class="sxs-lookup"><span data-stu-id="5b23c-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="5b23c-141">由於有參與的投稿，NuGet 包含 WiX 專案類型和 .NET 微架構的支援。</span><span class="sxs-lookup"><span data-stu-id="5b23c-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="5b23c-142">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="5b23c-142">Bug Fixes</span></span>

<span data-ttu-id="5b23c-143">如需錯誤修正的完整清單，請參閱 [此版本的 NuGet 問題追蹤](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)程式。</span><span class="sxs-lookup"><span data-stu-id="5b23c-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="5b23c-144">Bug 修正值得注意</span><span class="sxs-lookup"><span data-stu-id="5b23c-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="5b23c-145">具有原始程式檔的套件可在網站和 Web 應用程式專案中運作。</span><span class="sxs-lookup"><span data-stu-id="5b23c-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="5b23c-146">針對網站，會將來源檔案複製到 `App_Code` 資料夾</span><span class="sxs-lookup"><span data-stu-id="5b23c-146">For Websites, source files are copied into the `App_Code` folder</span></span>
