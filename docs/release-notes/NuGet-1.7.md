---
title: NuGet 1.7 版的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.7 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551463"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="1021b-103">NuGet 1.7 版的版本資訊</span><span class="sxs-lookup"><span data-stu-id="1021b-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="1021b-104">[NuGet 1.6 版版本資訊](../release-notes/nuget-1.6.md) | [NuGet 1.8 版本資訊](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="1021b-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="1021b-105">NuGet 1.7 已於 2012 年 4 月 4 日發行。</span><span class="sxs-lookup"><span data-stu-id="1021b-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="1021b-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="1021b-106">Known Installation Issue</span></span>
<span data-ttu-id="1021b-107">如果您執行的 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您已安裝較舊版本。</span><span class="sxs-lookup"><span data-stu-id="1021b-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="1021b-108">因應措施是只解除安裝 NuGet，然後再從 VS 延伸模組資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="1021b-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="1021b-109">請參閱 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1021b-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="1021b-110">注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕已停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。</span><span class="sxs-lookup"><span data-stu-id="1021b-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="1021b-111">功能</span><span class="sxs-lookup"><span data-stu-id="1021b-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="1021b-112">開啟 readme.txt 檔案，以在安裝後的支援</span><span class="sxs-lookup"><span data-stu-id="1021b-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="1021b-113">如果您的套件包含新 1.7，`readme.txt`完成安裝套件之後，檔案根目錄的套件，NuGet 會自動開啟此檔案。</span><span class="sxs-lookup"><span data-stu-id="1021b-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="1021b-114">在 [管理 NuGet 套件] 對話方塊中顯示發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="1021b-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="1021b-115">[管理 NuGet 套件] 對話方塊現在會包含在下拉式清單中提供選項，即可顯示發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="1021b-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![顯示發行前版本套件](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="1021b-117">遺漏封裝檔案時，顯示 [套件還原] 按鈕</span><span class="sxs-lookup"><span data-stu-id="1021b-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="1021b-118">當您開啟套件管理員主控台或的 Manager NuGet 套件 對話方塊，NuGet 會檢查目前的方案是否已啟用套件還原的模式和如果任何套件檔案中遺漏`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="1021b-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="1021b-119">如果這兩項條件都符合，NuGet 會通知您，並會顯示方便的 [還原] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1021b-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="1021b-120">按一下此按鈕，將會觸發 NuGet 還原所有遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="1021b-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![在對話方塊上的套件還原 按鈕](./media/packagerestore-dialog.png)

![在主控台上的套件還原 按鈕](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="1021b-123">新增方案層級 packages.config 檔案</span><span class="sxs-lookup"><span data-stu-id="1021b-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="1021b-124">在舊版的 NuGet 中，每個專案都`packages.config`以便持續追蹤哪些 NuGet 套件會安裝在該專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="1021b-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="1021b-125">不過，在解決方案層級来追蹤的方案層級套件時發生任何類似的檔案。</span><span class="sxs-lookup"><span data-stu-id="1021b-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="1021b-126">如此一來，沒有辦法還原方案層級套件。</span><span class="sxs-lookup"><span data-stu-id="1021b-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="1021b-127">這項功能現已實作在 NuGet 1.7。</span><span class="sxs-lookup"><span data-stu-id="1021b-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="1021b-128">方案層級`packages.config`檔案位於`.nuget`解決方案之下的資料夾的根目錄，並將儲存只有方案層級套件。</span><span class="sxs-lookup"><span data-stu-id="1021b-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="1021b-129">移除新增套件 命令</span><span class="sxs-lookup"><span data-stu-id="1021b-129">Remove New-Package command</span></span>
<span data-ttu-id="1021b-130">低使用量，因為已移除 [新增套件] 命令。</span><span class="sxs-lookup"><span data-stu-id="1021b-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="1021b-131">建議開發人員使用 nuget.exe 或方便的 NuGet 封裝總管 來建立封裝。</span><span class="sxs-lookup"><span data-stu-id="1021b-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="1021b-132">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="1021b-132">Bug Fixes</span></span>
<span data-ttu-id="1021b-133">NuGet 1.7 已修正許多 bug 有關於的套件還原工作流程與網路/原始檔控制的案例。</span><span class="sxs-lookup"><span data-stu-id="1021b-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="1021b-134">如需完整的工作清單項目中已修正 NuGet 1.7，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="1021b-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
