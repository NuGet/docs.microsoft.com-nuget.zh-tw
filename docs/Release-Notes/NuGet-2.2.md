---
title: "NuGet 2.2 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.2 版本資訊。"
keywords: "NuGet 2.2 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 63a1ae2315ea0c26fb5d26507ac0bcba8567aa9a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="9821f-104">NuGet 2.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="9821f-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="9821f-105">[NuGet 2.1 版本資訊](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 版本資訊](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="9821f-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="9821f-106">NuGet 2.2 已於 2012 年 12 月 12 日發行。</span><span class="sxs-lookup"><span data-stu-id="9821f-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="9821f-107">Visual Studio 快速啟動</span><span class="sxs-lookup"><span data-stu-id="9821f-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="9821f-108">其中一個 Visual Studio 2012 中已加入的新功能是[快速啟動對話方塊](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。</span><span class="sxs-lookup"><span data-stu-id="9821f-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="9821f-109">NuGet 2.2 擴充這個對話方塊中，讓它可以在 快速啟動中輸入搜尋詞彙以初始化 封裝管理員 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9821f-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="9821f-110">搜尋符合 'jquery' 的 NuGet 封裝在結果中，輸入 'jquery' 在快速啟動中，現在包含，例如的選項。</span><span class="sxs-lookup"><span data-stu-id="9821f-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![在 Visual Studio 快速啟動中的 NuGet](./media/quick-launch.png)

<span data-ttu-id="9821f-112">選取此選項將會啟動的標準 NuGet 封裝管理員搜尋體驗的詞彙 'jquery'。</span><span class="sxs-lookup"><span data-stu-id="9821f-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![預先填入的 NuGet 封裝管理員 對話方塊](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="9821f-114">指定封裝內容的整個資料夾</span><span class="sxs-lookup"><span data-stu-id="9821f-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="9821f-115">NuGet 2.2 現在可讓您指定在整個資料夾`<file>`元素`.nuspec`檔案以包含所有該資料夾的內容。</span><span class="sxs-lookup"><span data-stu-id="9821f-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="9821f-116">例如，下列會使所有指令碼封裝的指令碼資料夾中要加入至 contents\scripts 資料夾，當封裝安裝到專案。</span><span class="sxs-lookup"><span data-stu-id="9821f-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="9821f-117">**更新 6/24/16： 安裝封裝時，會忽略空的資料夾 [內容] 資料夾中。**</span><span class="sxs-lookup"><span data-stu-id="9821f-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="9821f-118">已知問題</span><span class="sxs-lookup"><span data-stu-id="9821f-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="9821f-119">使用封裝管理員主控台時，套件安裝失敗的 F # 專案</span><span class="sxs-lookup"><span data-stu-id="9821f-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="9821f-120">將 NuGet 封裝安裝到使用封裝管理員主控台的 F # 專案時，會擲回 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="9821f-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="9821f-121">目前正積極努力與 F # 小組解決問題，但在此同時，因應措施是將 NuGet 封裝安裝到 F # 專案中透過 NuGet 的封裝管理員 對話方塊，而不是主控台。</span><span class="sxs-lookup"><span data-stu-id="9821f-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="9821f-122">[詳細的資訊已 CodePlex 上提供](http://nuget.codeplex.com/workitem/2873)。</span><span class="sxs-lookup"><span data-stu-id="9821f-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="9821f-123">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="9821f-123">Bug Fixes</span></span>
<span data-ttu-id="9821f-124">NuGet 2.2 包含括許多錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="9821f-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="9821f-125">如需完整的工作清單項目中修正 NuGet 2.2，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="9821f-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
