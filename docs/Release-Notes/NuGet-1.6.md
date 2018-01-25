---
title: "NuGet 1.6 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.6 版的版本資訊。"
keywords: "NuGet 1.6 的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="7c124-104">NuGet 1.6 版的版本資訊</span><span class="sxs-lookup"><span data-stu-id="7c124-104">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="7c124-105">[NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md) | [NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="7c124-105">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="7c124-106">NuGet 1.6 已於 2011 年 12 月 13 日發行。</span><span class="sxs-lookup"><span data-stu-id="7c124-106">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="7c124-107">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="7c124-107">Known Installation Issue</span></span>
<span data-ttu-id="7c124-108">如果您正在執行 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您有安裝較舊的版本。</span><span class="sxs-lookup"><span data-stu-id="7c124-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="7c124-109">因應措施是只要解除安裝 NuGet，然後再從 VS 擴充功能庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="7c124-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="7c124-110">如需詳細資訊，請參閱 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。</span><span class="sxs-lookup"><span data-stu-id="7c124-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="7c124-111">注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕會停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。</span><span class="sxs-lookup"><span data-stu-id="7c124-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="7c124-112">功能</span><span class="sxs-lookup"><span data-stu-id="7c124-112">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="7c124-113">支援語意版本設定和套件發行前版本</span><span class="sxs-lookup"><span data-stu-id="7c124-113">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="7c124-114">NuGet 1.6 版引進了 (SemVer) 的語意版本設定的支援。</span><span class="sxs-lookup"><span data-stu-id="7c124-114">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="7c124-115">如需如何使用 SemVer 的詳細資訊，請參閱[版本控制文件](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="7c124-115">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="7c124-116">使用 NuGet 而不要簽入的封裝 （封裝還原）</span><span class="sxs-lookup"><span data-stu-id="7c124-116">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="7c124-117">NuGet 1.6 現在具有第一級支援工作流程中的 NuGet 封裝不會加入至原始檔控制，但改為會還原在建置階段遺失。</span><span class="sxs-lookup"><span data-stu-id="7c124-117">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="7c124-118">如需詳細資訊，請參閱[不認可封裝至原始檔控制使用的 NuGet](../consume-packages/packages-and-source-control.md)主題。</span><span class="sxs-lookup"><span data-stu-id="7c124-118">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="7c124-119">安裝 NuGet 封裝的項目範本</span><span class="sxs-lookup"><span data-stu-id="7c124-119">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="7c124-120">支援預先安裝的 NuGet 封裝加入 Visual Studio 專案範本的工作為基礎，NuGet 1.6 也新增支援 Visual Studio 項目範本。</span><span class="sxs-lookup"><span data-stu-id="7c124-120">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="7c124-121">項目範本可以有相關的叫用中的範本時所安裝的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="7c124-121">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="7c124-122">如需有關如何變更要安裝 NuGet 封裝的專案/項目範本的詳細資訊，請參閱[封裝在 Visual Studio 範本](../visual-studio-extensibility/visual-studio-templates.md)主題。</span><span class="sxs-lookup"><span data-stu-id="7c124-122">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="7c124-123">停用封裝來源的支援</span><span class="sxs-lookup"><span data-stu-id="7c124-123">Support for disabling package sources</span></span>
<span data-ttu-id="7c124-124">當多個封裝來源的設定時，NuGet 安裝封裝及其相依性時看起來中每個封裝。</span><span class="sxs-lookup"><span data-stu-id="7c124-124">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="7c124-125">已關閉的原因可以嚴重會拖慢 NuGet 套件來源。</span><span class="sxs-lookup"><span data-stu-id="7c124-125">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="7c124-126">NuGet 1.6 前您無法移除封裝來源，但您必須記住的詳細資料，為您想要將它新增回。</span><span class="sxs-lookup"><span data-stu-id="7c124-126">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="7c124-127">NuGet 1.6 可讓您取消核取 要停用，但保留周圍的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="7c124-127">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![停用封裝](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="7c124-129">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="7c124-129">Bug Fixes</span></span>
<span data-ttu-id="7c124-130">NuGet 1.6 有工作項目固定 106 總數。</span><span class="sxs-lookup"><span data-stu-id="7c124-130">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="7c124-131">這些 95 已分類為 bug 和 10，這些功能。</span><span class="sxs-lookup"><span data-stu-id="7c124-131">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="7c124-132">如需完整的工作清單項目固定在 NuGet 1.6，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="7c124-132">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
