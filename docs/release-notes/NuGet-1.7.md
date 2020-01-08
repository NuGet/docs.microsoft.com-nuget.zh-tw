---
title: NuGet 1.7 版本資訊
description: NuGet 1.7 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383315"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="4f581-103">NuGet 1.7 版本資訊</span><span class="sxs-lookup"><span data-stu-id="4f581-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="4f581-104">[Nuget 1.6 版本](../release-notes/nuget-1.6.md)資訊 | [nuget 1.8 版本](../release-notes/nuget-1.8.md)資訊</span><span class="sxs-lookup"><span data-stu-id="4f581-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="4f581-105">NuGet 1.7 已于2012年4月4日發行。</span><span class="sxs-lookup"><span data-stu-id="4f581-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="4f581-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="4f581-106">Known Installation Issue</span></span>
<span data-ttu-id="4f581-107">如果您執行 VS 2010 SP1，如果您已安裝舊版，則嘗試升級 NuGet 時可能會發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="4f581-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="4f581-108">因應措施是直接卸載 NuGet，然後從 VS 延伸模組資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="4f581-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="4f581-109">如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>。</span><span class="sxs-lookup"><span data-stu-id="4f581-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="4f581-110">注意：如果 Visual Studio 不允許您卸載擴充功能（[卸載] 按鈕已停用），您可能需要使用 [以系統管理員身分執行] 重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4f581-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="4f581-111">功能</span><span class="sxs-lookup"><span data-stu-id="4f581-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="4f581-112">支援在安裝後開啟 readme.txt 檔案</span><span class="sxs-lookup"><span data-stu-id="4f581-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="4f581-113">1\.7 的新功能，如果您的套件在套件的根目錄包含 `readme.txt` 檔案，NuGet 會在完成封裝的安裝後自動開啟此檔案。</span><span class="sxs-lookup"><span data-stu-id="4f581-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="4f581-114">[管理 NuGet 封裝] 對話方塊中的 [顯示發行前版本套件]</span><span class="sxs-lookup"><span data-stu-id="4f581-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="4f581-115">[管理 NuGet 封裝] 對話方塊現在包含一個下拉式清單，其中提供可顯示發行前版本套件的選項。</span><span class="sxs-lookup"><span data-stu-id="4f581-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![顯示發行前版本套件](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="4f581-117">遺失套件檔案時顯示封裝還原按鈕</span><span class="sxs-lookup"><span data-stu-id="4f581-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="4f581-118">當您開啟 [套件管理員主控台] 或 [管理員 NuGet 套件] 對話方塊時，NuGet 會檢查目前的解決方案是否已啟用封裝還原模式，以及是否有任何封裝檔案從 `packages` 資料夾中遺失。</span><span class="sxs-lookup"><span data-stu-id="4f581-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="4f581-119">如果符合這兩個條件，NuGet 將會通知您，而且會顯示方便的 [還原] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4f581-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="4f581-120">按一下此按鈕會觸發 NuGet，以還原所有遺失的封裝。</span><span class="sxs-lookup"><span data-stu-id="4f581-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![對話方塊上的 [封裝還原] 按鈕](./media/packagerestore-dialog.png)

![主控台上的 [封裝還原] 按鈕](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="4f581-123">新增方案層級的封裝 .config 檔案</span><span class="sxs-lookup"><span data-stu-id="4f581-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="4f581-124">在舊版的 NuGet 中，每個專案都有一個 `packages.config` 檔案，可追蹤該專案中安裝的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="4f581-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="4f581-125">不過，解決方案層級沒有類似的檔案可以追蹤解決方案層級的封裝。</span><span class="sxs-lookup"><span data-stu-id="4f581-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="4f581-126">因此，沒有任何方法可以還原解決方案層級的封裝。</span><span class="sxs-lookup"><span data-stu-id="4f581-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="4f581-127">這項功能現在已在 NuGet 1.7 中執行。</span><span class="sxs-lookup"><span data-stu-id="4f581-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="4f581-128">解決方案層級的 `packages.config` 檔案會放在 [方案根目錄] 底下的 [`.nuget`] 資料夾底下，而且只會儲存解決方案層級的封裝。</span><span class="sxs-lookup"><span data-stu-id="4f581-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="4f581-129">移除新的-封裝命令</span><span class="sxs-lookup"><span data-stu-id="4f581-129">Remove New-Package command</span></span>
<span data-ttu-id="4f581-130">由於使用量過低，已移除新的-Package 命令。</span><span class="sxs-lookup"><span data-stu-id="4f581-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="4f581-131">建議開發人員使用 nuget.exe 或方便的 NuGet 套件瀏覽器來建立封裝。</span><span class="sxs-lookup"><span data-stu-id="4f581-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4f581-132">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="4f581-132">Bug Fixes</span></span>
<span data-ttu-id="4f581-133">NuGet 1.7 已針對套件還原工作流程和網路/原始檔控制案例，修正許多 bug。</span><span class="sxs-lookup"><span data-stu-id="4f581-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="4f581-134">如需 NuGet 1.7 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="4f581-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
