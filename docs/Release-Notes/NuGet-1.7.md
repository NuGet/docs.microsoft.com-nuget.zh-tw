---
title: "NuGet 1.7 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.7 的版本資訊。"
keywords: "NuGet 1.7 的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="84a7e-104">NuGet 1.7 版版本資訊</span><span class="sxs-lookup"><span data-stu-id="84a7e-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="84a7e-105">[NuGet 1.6 版本資訊](../release-notes/nuget-1.6.md) | [NuGet 1.8 版本資訊](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="84a7e-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="84a7e-106">NuGet 1.7 已於 2012 年 4 月 4 日發行。</span><span class="sxs-lookup"><span data-stu-id="84a7e-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="84a7e-107">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="84a7e-107">Known Installation Issue</span></span>
<span data-ttu-id="84a7e-108">如果您正在執行 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您有安裝較舊的版本。</span><span class="sxs-lookup"><span data-stu-id="84a7e-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="84a7e-109">因應措施是只要解除安裝 NuGet，然後再從 VS 擴充功能庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="84a7e-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="84a7e-110">如需詳細資訊，請參閱 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。</span><span class="sxs-lookup"><span data-stu-id="84a7e-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="84a7e-111">注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕會停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。</span><span class="sxs-lookup"><span data-stu-id="84a7e-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="84a7e-112">功能</span><span class="sxs-lookup"><span data-stu-id="84a7e-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="84a7e-113">開啟安裝後的 readme.txt 檔案，以支援</span><span class="sxs-lookup"><span data-stu-id="84a7e-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="84a7e-114">如果您的封裝包含新 1.7，`readme.txt`它完成安裝程式套件後，檔案位於根目錄的套件，NuGet 會自動開啟此檔案。</span><span class="sxs-lookup"><span data-stu-id="84a7e-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="84a7e-115">在 [管理 NuGet 封裝] 對話方塊中顯示套件發行前版本</span><span class="sxs-lookup"><span data-stu-id="84a7e-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="84a7e-116">[管理 NuGet 封裝] 對話方塊現在包含下拉式清單會提供選項，以顯示套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="84a7e-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![顯示套件發行前版本](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="84a7e-118">遺漏封裝檔案時顯示封裝還原按鈕</span><span class="sxs-lookup"><span data-stu-id="84a7e-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="84a7e-119">當您開啟 [封裝管理員主控台或管理員 NuGet 封裝] 對話方塊，NuGet 會檢查目前的方案是否已啟用的封裝還原模式，如果任何封裝檔案中遺漏`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="84a7e-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="84a7e-120">如果這兩項條件都符合，NuGet 會通知您，並會顯示方便的 [還原] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84a7e-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="84a7e-121">按一下此按鈕將會觸發 NuGet 還原所有遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="84a7e-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![在對話方塊上的封裝還原按鈕](./media/packagerestore-dialog.png)

![在主控台上的封裝還原按鈕](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="84a7e-124">新增解決方案層級 packages.config 檔案</span><span class="sxs-lookup"><span data-stu-id="84a7e-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="84a7e-125">在舊版的 NuGet，每個專案有`packages.config`會追蹤哪些 NuGet 封裝會安裝在該專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="84a7e-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="84a7e-126">不過，在方案層級追蹤的方案層級封裝沒有類似檔。</span><span class="sxs-lookup"><span data-stu-id="84a7e-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="84a7e-127">如此一來，已沒有還原方案層級的封裝。</span><span class="sxs-lookup"><span data-stu-id="84a7e-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="84a7e-128">NuGet 1.7 現在實作這項功能。</span><span class="sxs-lookup"><span data-stu-id="84a7e-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="84a7e-129">方案層級`packages.config`檔案位於`.nuget`下的方案資料夾的根和只有方案層級封裝會儲存。</span><span class="sxs-lookup"><span data-stu-id="84a7e-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="84a7e-130">移除新增套件 命令</span><span class="sxs-lookup"><span data-stu-id="84a7e-130">Remove New-Package command</span></span>
<span data-ttu-id="84a7e-131">低使用量，因為已經移除 [新增套件] 命令。</span><span class="sxs-lookup"><span data-stu-id="84a7e-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="84a7e-132">開發人員建議使用 nuget.exe 或很方便的 NuGet 封裝總管 來建立封裝。</span><span class="sxs-lookup"><span data-stu-id="84a7e-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="84a7e-133">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="84a7e-133">Bug Fixes</span></span>
<span data-ttu-id="84a7e-134">NuGet 1.7 已修正許多 bug 周圍的封裝還原，工作流程和網路/原始檔控制案例。</span><span class="sxs-lookup"><span data-stu-id="84a7e-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="84a7e-135">如需完整的工作清單項目固定在 NuGet 1.7，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="84a7e-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
