---
title: NuGet 1.7 版本資訊
description: NuGet 1.7 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777072"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="06aaa-103">NuGet 1.7 版本資訊</span><span class="sxs-lookup"><span data-stu-id="06aaa-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="06aaa-104">[NuGet 1.6 版本](../release-notes/nuget-1.6.md)  |  資訊[NuGet 1.8 版本](../release-notes/nuget-1.8.md)資訊</span><span class="sxs-lookup"><span data-stu-id="06aaa-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="06aaa-105">NuGet 1.7 發行于2012年4月4日。</span><span class="sxs-lookup"><span data-stu-id="06aaa-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="06aaa-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="06aaa-106">Known Installation Issue</span></span>
<span data-ttu-id="06aaa-107">如果您執行的是 VS 2010 SP1，如果您已安裝較舊的版本，可能會在嘗試升級 NuGet 時發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="06aaa-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="06aaa-108">解決方法是直接卸載 NuGet，然後從 VS 延伸模組資源庫安裝它。</span><span class="sxs-lookup"><span data-stu-id="06aaa-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="06aaa-109">如需相關資訊，請參閱 <https://support.microsoft.com/kb/2581019> 。</span><span class="sxs-lookup"><span data-stu-id="06aaa-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="06aaa-110">注意：如果 Visual Studio 不允許您卸載擴充功能 () 停用 [卸載] 按鈕，那麼您可能需要使用 [以系統管理員身分執行] 來重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="06aaa-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="06aaa-111">功能</span><span class="sxs-lookup"><span data-stu-id="06aaa-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="06aaa-112">支援在安裝後開啟 readme.txt 檔案</span><span class="sxs-lookup"><span data-stu-id="06aaa-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="06aaa-113">1.7 的新功能，如果您的套件在 `readme.txt` 套件的根目錄包含檔案，NuGet 會在完成安裝套件之後自動開啟此檔案。</span><span class="sxs-lookup"><span data-stu-id="06aaa-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="06aaa-114">在 [管理 NuGet 封裝] 對話方塊中顯示發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="06aaa-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="06aaa-115">[管理 NuGet 封裝] 對話方塊現在包含一個下拉式清單，其中提供了顯示發行前版本套件的選項。</span><span class="sxs-lookup"><span data-stu-id="06aaa-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![顯示發行前版本套件](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="06aaa-117">遺失套件檔案時顯示套件還原按鈕</span><span class="sxs-lookup"><span data-stu-id="06aaa-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="06aaa-118">當您開啟封裝管理員主控台或 [管理員 NuGet 套件] 對話方塊時，NuGet 會檢查目前的解決方案是否已啟用套件還原模式，以及資料夾中是否遺失任何封裝檔案 `packages` 。</span><span class="sxs-lookup"><span data-stu-id="06aaa-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="06aaa-119">如果符合這兩個條件，NuGet 將會通知您，而且會顯示方便的 [還原] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="06aaa-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="06aaa-120">按一下這個按鈕將會觸發 NuGet 來還原所有遺失的封裝。</span><span class="sxs-lookup"><span data-stu-id="06aaa-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![對話方塊上的 [封裝還原] 按鈕](./media/packagerestore-dialog.png)

![主控台上的 [封裝還原] 按鈕](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="06aaa-123">新增解決方案層級的 packages.config 檔案</span><span class="sxs-lookup"><span data-stu-id="06aaa-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="06aaa-124">在舊版的 NuGet 中，每個專案都有一個檔案， `packages.config` 可追蹤該專案中安裝的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="06aaa-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="06aaa-125">不過，方案層級沒有類似的檔案可追蹤解決方案層級的封裝。</span><span class="sxs-lookup"><span data-stu-id="06aaa-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="06aaa-126">因此，沒有辦法可以還原解決方案層級的封裝。</span><span class="sxs-lookup"><span data-stu-id="06aaa-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="06aaa-127">這項功能現在已在 NuGet 1.7 中執行。</span><span class="sxs-lookup"><span data-stu-id="06aaa-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="06aaa-128">解決方案層級檔案 `packages.config` 會放置在 [ `.nuget` 方案根目錄] 下的資料夾底下，而且只會儲存方案層級的封裝。</span><span class="sxs-lookup"><span data-stu-id="06aaa-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="06aaa-129">移除 New-Package 命令</span><span class="sxs-lookup"><span data-stu-id="06aaa-129">Remove New-Package command</span></span>
<span data-ttu-id="06aaa-130">由於使用量很低，因此已移除 New-Package 命令。</span><span class="sxs-lookup"><span data-stu-id="06aaa-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="06aaa-131">建議開發人員使用 nuget.exe 或方便的 NuGet 套件瀏覽器來建立封裝。</span><span class="sxs-lookup"><span data-stu-id="06aaa-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="06aaa-132">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="06aaa-132">Bug Fixes</span></span>
<span data-ttu-id="06aaa-133">NuGet 1.7 已修正套件還原工作流程和網路/原始檔控制案例的許多錯誤。</span><span class="sxs-lookup"><span data-stu-id="06aaa-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="06aaa-134">如需 NuGet 1.7 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="06aaa-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
