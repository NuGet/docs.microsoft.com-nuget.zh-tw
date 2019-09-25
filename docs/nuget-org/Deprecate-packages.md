---
title: Nuget.org 上的淘汰套件
description: 淘汰封裝程式的詳細描述，以及用戶端如何顯示此資訊
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248894"
---
# <a name="deprecating-packages"></a><span data-ttu-id="868f0-103">淘汰套件</span><span class="sxs-lookup"><span data-stu-id="868f0-103">Deprecating packages</span></span>

<span data-ttu-id="868f0-104">如果您不再維護封裝，或想要鼓勵套件的取用者移至另一個套件，您可以取代套件。</span><span class="sxs-lookup"><span data-stu-id="868f0-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="868f0-105">套件取代與**取消列出**您的套件不同，如下所述：</span><span class="sxs-lookup"><span data-stu-id="868f0-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="868f0-106">**取消列出**套件會防止其探索，因為它會隱藏在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="868f0-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="868f0-107">**淘汰**封裝可讓您的套件現有取用者瞭解其是否已在其專案中安裝或使用。</span><span class="sxs-lookup"><span data-stu-id="868f0-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="868f0-108">它也會讓他們知道取代的原因，以及您所指定的替代建議套件（封裝發行者）。</span><span class="sxs-lookup"><span data-stu-id="868f0-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="868f0-109">淘汰封裝不會取消列出套件。</span><span class="sxs-lookup"><span data-stu-id="868f0-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="868f0-110">身為發行者，您可以選擇取消列出和取代套件。</span><span class="sxs-lookup"><span data-stu-id="868f0-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="868f0-111">淘汰工作流程</span><span class="sxs-lookup"><span data-stu-id="868f0-111">Deprecation workflow</span></span>
1. <span data-ttu-id="868f0-112">若要取代封裝，請移至 [**管理套件**]，**然後選取 [** 淘汰]：</span><span class="sxs-lookup"><span data-stu-id="868f0-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![移至取代封裝選項](media/deprecation-select-option.png)

2. <span data-ttu-id="868f0-114">選取您想要取代的版本。</span><span class="sxs-lookup"><span data-stu-id="868f0-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="868f0-115">如果您想要取代所有版本，請選擇 [**選取所有版本**] 選項。</span><span class="sxs-lookup"><span data-stu-id="868f0-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![選取要取代的套件版本](media/deprecation-select-version.png)

3. <span data-ttu-id="868f0-117">選擇取代的原因。</span><span class="sxs-lookup"><span data-stu-id="868f0-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="868f0-118">如果不再維護封裝，請選擇 [**舊版**] 選項。</span><span class="sxs-lookup"><span data-stu-id="868f0-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="868f0-119">如果特定版本有重大錯誤，請選擇 [**有重大錯誤**] 選項。</span><span class="sxs-lookup"><span data-stu-id="868f0-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="868f0-120">基於任何其他原因，請選取 [**其他**]。</span><span class="sxs-lookup"><span data-stu-id="868f0-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="868f0-121">您一律可以為擁有者指定替代的建議套件（和版本）和自訂訊息。</span><span class="sxs-lookup"><span data-stu-id="868f0-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![選取原因替代套件建議和自訂訊息](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="868f0-123">自訂訊息只會顯示在 nuget.org 上，但不會顯示在用戶端上。</span><span class="sxs-lookup"><span data-stu-id="868f0-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="868f0-124">目前， `dotnet.exe`和 NuGet 套件管理員之類的用戶端不會顯示自訂訊息。</span><span class="sxs-lookup"><span data-stu-id="868f0-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="868f0-125">已淘汰套件的用戶端體驗</span><span class="sxs-lookup"><span data-stu-id="868f0-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="868f0-126">一旦套件已淘汰，其取用者會以下列方式收到通知（視使用的用戶端而定）。</span><span class="sxs-lookup"><span data-stu-id="868f0-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="868f0-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="868f0-127">Visual Studio</span></span> 
<span data-ttu-id="868f0-128">*從 Visual Studio 2019 版本16.3 開始提供*</span><span class="sxs-lookup"><span data-stu-id="868f0-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="868f0-129">Visual Studio 警告索引標籤上`Installed`已淘汰的套件使用方式。它會將您導向封裝及其取代資訊（包括已淘汰的原因，以及要改用的替代封裝，如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="868f0-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab.It will lead you to the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![套件管理員 Visual Studio 已安裝 索引標籤上的已淘汰套件](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="868f0-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="868f0-131">dotnet.exe</span></span>
<span data-ttu-id="868f0-132">*從 .NET SDK 3.0 開始提供*</span><span class="sxs-lookup"><span data-stu-id="868f0-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="868f0-133">如果您使用 dotnet，您可以在方案或專案資料夾`dotnet list package --deprecated`上執行命令，以取得已淘汰的套件清單以及取代資訊：</span><span class="sxs-lookup"><span data-stu-id="868f0-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
