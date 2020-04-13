---
title: 棄用nuget.org包
description: 有關棄用套件程序以及客戶端如何顯示此資訊的詳細說明
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096876"
---
# <a name="deprecating-packages"></a><span data-ttu-id="7e132-103">棄用包</span><span class="sxs-lookup"><span data-stu-id="7e132-103">Deprecating packages</span></span>

<span data-ttu-id="7e132-104">如果您不再維護包,或者希望鼓勵包的消費者轉到其他包,則可以棄用包。</span><span class="sxs-lookup"><span data-stu-id="7e132-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="7e132-105">包棄用不同於**取消列出**包,如下所述:</span><span class="sxs-lookup"><span data-stu-id="7e132-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="7e132-106">**取消列出**包會阻止其發現,因為它隱藏在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="7e132-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="7e132-107">**棄用**包可以讓包的現有消費者瞭解其是否在其專案中安裝或使用。</span><span class="sxs-lookup"><span data-stu-id="7e132-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="7e132-108">它還讓他們知道棄用的原因以及您指定的備用建議包(包發行者)。</span><span class="sxs-lookup"><span data-stu-id="7e132-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="7e132-109">棄用包不會取消列出包。</span><span class="sxs-lookup"><span data-stu-id="7e132-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="7e132-110">作為發行者,您可以選擇取消列出包和棄用包。</span><span class="sxs-lookup"><span data-stu-id="7e132-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="7e132-111">棄用工作流</span><span class="sxs-lookup"><span data-stu-id="7e132-111">Deprecation workflow</span></span>
1. <span data-ttu-id="7e132-112">要棄用套件,請轉到 **"管理包"** 並選擇 **「棄用**」 :</span><span class="sxs-lookup"><span data-stu-id="7e132-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![跳到棄用套件選項](media/deprecation-select-option.png)

2. <span data-ttu-id="7e132-114">選擇要棄用的版本。</span><span class="sxs-lookup"><span data-stu-id="7e132-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="7e132-115">如果要棄用所有版本,**請選擇「選擇所有版本**」選項。</span><span class="sxs-lookup"><span data-stu-id="7e132-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![選擇要棄用的套件版本](media/deprecation-select-version.png)

3. <span data-ttu-id="7e132-117">選擇棄用的原因。</span><span class="sxs-lookup"><span data-stu-id="7e132-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="7e132-118">如果包不再維護,請選擇 **「舊版」** 選項。</span><span class="sxs-lookup"><span data-stu-id="7e132-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="7e132-119">如果特定版本存在嚴重錯誤,請選擇 **「具有嚴重錯誤」** 選項。</span><span class="sxs-lookup"><span data-stu-id="7e132-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="7e132-120">出於任何其他原因,請選擇 **"其他**"。</span><span class="sxs-lookup"><span data-stu-id="7e132-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="7e132-121">您始終可以指定備用建議的包(和版本)和給擁有者的自定義消息。</span><span class="sxs-lookup"><span data-stu-id="7e132-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![選擇備用套件建議與自訂訊息的原因](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="7e132-123">自定義消息僅在nuget.org上顯示,但不顯示在用戶端。</span><span class="sxs-lookup"><span data-stu-id="7e132-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="7e132-124">目前,像和`dotnet.exe`NuGet 包管理器這樣的用戶端不顯示自訂訊息。</span><span class="sxs-lookup"><span data-stu-id="7e132-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="7e132-125">棄用套件的客戶端體驗</span><span class="sxs-lookup"><span data-stu-id="7e132-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="7e132-126">一旦包被棄用,就會以下列方式通知其消費者(取決於所使用的用戶端)。</span><span class="sxs-lookup"><span data-stu-id="7e132-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="7e132-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e132-127">Visual Studio</span></span> 
<span data-ttu-id="7e132-128">*可從 Visual Studio 2019 版本 16.3 開始*</span><span class="sxs-lookup"><span data-stu-id="7e132-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="7e132-129">Visual Studio`Installed`警告 選項卡上已棄用的包的使用。它將顯示包及其棄用資訊的警告(包括棄用的原因和備用包(如果存在)。如果存在, 則改為使用。</span><span class="sxs-lookup"><span data-stu-id="7e132-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![在安裝的「視覺工作室」選項卡上的已棄用包,選項卡上已安裝的包管理器](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="7e132-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="7e132-131">dotnet.exe</span></span>
<span data-ttu-id="7e132-132">*可從 .NET SDK 3.0 開始*</span><span class="sxs-lookup"><span data-stu-id="7e132-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="7e132-133">如果使用 dotnet.exe,則可以在解決方案或專案`dotnet list package --deprecated`資料夾 上執行該指令,以取得有關棄用套件的清單以及棄用資訊:</span><span class="sxs-lookup"><span data-stu-id="7e132-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
