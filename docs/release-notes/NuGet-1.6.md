---
title: NuGet 1.6 版本資訊
description: NuGet 1.6 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777018"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="f6610-103">NuGet 1.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="f6610-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="f6610-104">[NuGet 1.5 版本](../release-notes/nuget-1.5.md)  |  資訊[NuGet 1.7 版本](../release-notes/nuget-1.7.md)資訊</span><span class="sxs-lookup"><span data-stu-id="f6610-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="f6610-105">NuGet 1.6 已于2011年12月13日發行。</span><span class="sxs-lookup"><span data-stu-id="f6610-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="f6610-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="f6610-106">Known Installation Issue</span></span>
<span data-ttu-id="f6610-107">如果您執行的是 VS 2010 SP1，如果您已安裝較舊的版本，可能會在嘗試升級 NuGet 時發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="f6610-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="f6610-108">解決方法是直接卸載 NuGet，然後從 VS 延伸模組資源庫安裝它。</span><span class="sxs-lookup"><span data-stu-id="f6610-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="f6610-109">如需相關資訊，請參閱 <https://support.microsoft.com/kb/2581019> 。</span><span class="sxs-lookup"><span data-stu-id="f6610-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="f6610-110">注意：如果 Visual Studio 不允許您卸載擴充功能 () 停用 [卸載] 按鈕，那麼您可能需要使用 [以系統管理員身分執行] 來重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f6610-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="f6610-111">功能</span><span class="sxs-lookup"><span data-stu-id="f6610-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="f6610-112">支援語義版本控制和發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="f6610-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="f6610-113">NuGet 1.6 引進 (SemVer) 的語義版本設定支援。</span><span class="sxs-lookup"><span data-stu-id="f6610-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="f6610-114">如需有關如何使用 SemVer 的詳細資訊，請參閱 [版本設定檔](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="f6610-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="f6610-115">在不簽入套件的情況下使用 NuGet (套件還原) </span><span class="sxs-lookup"><span data-stu-id="f6610-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="f6610-116">NuGet 1.6 現在具有工作流程的第一個類別支援，NuGet 封裝不會新增至原始檔控制，而是在組建時還原（如果遺失的話）。</span><span class="sxs-lookup"><span data-stu-id="f6610-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="f6610-117">如需詳細資訊，請閱讀 [使用 NuGet，而不將套件認可至原始檔控制](../consume-packages/packages-and-source-control.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="f6610-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="f6610-118">安裝 NuGet 套件的專案範本</span><span class="sxs-lookup"><span data-stu-id="f6610-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="f6610-119">為了支援預先安裝的 NuGet 套件來 Visual Studio 專案範本，NuGet 1.6 也加入了 Visual Studio 專案範本的支援。</span><span class="sxs-lookup"><span data-stu-id="f6610-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="f6610-120">專案範本可以具有在叫用範本時所安裝的相關聯 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="f6610-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="f6610-121">如需如何變更專案/專案範本以安裝 NuGet 套件的詳細資訊，請參閱 [Visual Studio 範本主題中的套件](../visual-studio-extensibility/visual-studio-templates.md) 。</span><span class="sxs-lookup"><span data-stu-id="f6610-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="f6610-122">支援停用套件來源</span><span class="sxs-lookup"><span data-stu-id="f6610-122">Support for disabling package sources</span></span>
<span data-ttu-id="f6610-123">當您設定多個套件來源時，NuGet 會在套件安裝期間和其相依性的套件中尋找套件。</span><span class="sxs-lookup"><span data-stu-id="f6610-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="f6610-124">基於某個原因而關閉的套件來源可能會嚴重降低 NuGet 的速度。</span><span class="sxs-lookup"><span data-stu-id="f6610-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="f6610-125">在 NuGet 1.6 之前，您可以移除套件來源，但是當您想要將它重新加入時，必須記住的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f6610-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="f6610-126">NuGet 1.6 允許取消核取套件來源以將它停用，但請將其保留。</span><span class="sxs-lookup"><span data-stu-id="f6610-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![停用封裝](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="f6610-128">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="f6610-128">Bug Fixes</span></span>
<span data-ttu-id="f6610-129">NuGet 1.6 總共修正了106個工作專案。</span><span class="sxs-lookup"><span data-stu-id="f6610-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="f6610-130">其中的95分類為 bug，而其中有10個是功能。</span><span class="sxs-lookup"><span data-stu-id="f6610-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="f6610-131">如需 NuGet 1.6 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="f6610-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
