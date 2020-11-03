---
title: NuGet 生態系統概觀
description: NuGet 生態系統中的完整資源，包含 NuGet 來源、非 Microsoft NuGet 專案、公用程式和訓練教材。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 165587fb64be5a5f4dbfdece7dc3a1e6402b733e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237422"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="bd138-103">NuGet 生態系統的概觀</span><span class="sxs-lookup"><span data-stu-id="bd138-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="bd138-104">NuGet 是在 2010 年引進，因此極有可能改善和自動化開發程序的不同層面。</span><span class="sxs-lookup"><span data-stu-id="bd138-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="bd138-105">因為 NuGet 是 [Apache v2 授權](http://choosealicense.com/licenses/apache/)許可的開放原始碼，所以其他專案可以利用 NuGet，而且公司可以在產品中建置其支援。</span><span class="sxs-lookup"><span data-stu-id="bd138-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="bd138-106">不論針對開放原始碼專案還是企業應用程式開發，NuGet 以及根據 NuGet 建置的其他應用程式都提供多種生態系統工具來改善軟體開發程序。</span><span class="sxs-lookup"><span data-stu-id="bd138-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="bd138-107">因為開發人員的參與，所有這些專案都可以創新。</span><span class="sxs-lookup"><span data-stu-id="bd138-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="bd138-108">就如同您參與 NuGet 本身一樣，也會透過報告缺失和新功能想法來參與這些專案，並提供意見、撰寫文件，同時盡可能提供程式碼。</span><span class="sxs-lookup"><span data-stu-id="bd138-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="bd138-109">.NET Foundation 專案</span><span class="sxs-lookup"><span data-stu-id="bd138-109">.NET Foundation projects</span></span>

<span data-ttu-id="bd138-110">NuGet 提供 Microsoft 開發平台的免費開放原始碼套件管理系統。</span><span class="sxs-lookup"><span data-stu-id="bd138-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="bd138-111">它包含一些用戶端工具，以及包含[正式 NuGet 資源庫](http://www.nuget.org)的服務集。</span><span class="sxs-lookup"><span data-stu-id="bd138-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="bd138-112">這些合併使用可以形成 [.NET Foundation](http://www.dotnetfoundation.org/) 所治理的 NuGet 專案。</span><span class="sxs-lookup"><span data-stu-id="bd138-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="bd138-113">NuGet 組織包含 GitHub 上的各種存放庫。</span><span class="sxs-lookup"><span data-stu-id="bd138-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="bd138-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) 提供所有存放庫的總覽，以及可在何處找到各種 NuGet 元件。</span><span class="sxs-lookup"><span data-stu-id="bd138-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="bd138-115">Microsoft 專案</span><span class="sxs-lookup"><span data-stu-id="bd138-115">Microsoft projects</span></span>

<span data-ttu-id="bd138-116">Microsoft 大量參與 NuGet 的開發。</span><span class="sxs-lookup"><span data-stu-id="bd138-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="bd138-117">Microsoft 員工所做的所有參與也是開放原始碼並捐獻 (包含著作權) 給 .NET Foundation。</span><span class="sxs-lookup"><span data-stu-id="bd138-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="bd138-118">非 Microsoft 專案</span><span class="sxs-lookup"><span data-stu-id="bd138-118">Non-Microsoft projects</span></span>

<span data-ttu-id="bd138-119">許多其他個人和公司都對 NuGet 生態系統有重大貢獻。</span><span class="sxs-lookup"><span data-stu-id="bd138-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="bd138-120">這裡所列之每個專案的授權可能會與核心 NuGet 元件不同，因此請確認授權條款可接受後再使用：</span><span class="sxs-lookup"><span data-stu-id="bd138-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="bd138-121">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="bd138-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="bd138-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="bd138-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="bd138-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="bd138-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="bd138-124">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="bd138-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="bd138-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="bd138-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="bd138-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="bd138-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="bd138-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="bd138-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="bd138-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="bd138-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="bd138-129">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="bd138-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="bd138-130">MyGet (或 NuGet-as-a-service)</span><span class="sxs-lookup"><span data-stu-id="bd138-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="bd138-131">NuGet 套件總管</span><span class="sxs-lookup"><span data-stu-id="bd138-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="bd138-132">NuGet 伺服器</span><span class="sxs-lookup"><span data-stu-id="bd138-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="bd138-133">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="bd138-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="bd138-134">Paket</span><span class="sxs-lookup"><span data-stu-id="bd138-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="bd138-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="bd138-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="bd138-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="bd138-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="bd138-137">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="bd138-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="bd138-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="bd138-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="bd138-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="bd138-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="bd138-140">Xamarin 和 MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="bd138-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="bd138-141">其他 NuGet 公用程式</span><span class="sxs-lookup"><span data-stu-id="bd138-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="bd138-142">這些是根據 NuGet 所建置的工具和公用程式：</span><span class="sxs-lookup"><span data-stu-id="bd138-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="bd138-143">[Glimpse 延伸模組](http://getglimpse.com/Packages) (外掛程式是套件)</span><span class="sxs-lookup"><span data-stu-id="bd138-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="bd138-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="bd138-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="bd138-145">[Orchard](http://www.orchardproject.net/) (CMS 模組是從 Orchard 資源庫中所裝載的 v1 NuGet 摘要中擷取)</span><span class="sxs-lookup"><span data-stu-id="bd138-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="bd138-146">NuGet 伺服器的 Java 實作</span><span class="sxs-lookup"><span data-stu-id="bd138-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="bd138-147">[NuGetLatest](https://twitter.com/NuGetLatest) (推出新套件發行集的 Twitter 機器人)</span><span class="sxs-lookup"><span data-stu-id="bd138-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="bd138-148">[DefinitelyTyped](http://definitelytyped.org/) ([自動](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript 類型 [發行至 NuGet 的定義](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="bd138-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="bd138-149">訓練教材和參考</span><span class="sxs-lookup"><span data-stu-id="bd138-149">Training materials and references</span></span>

<span data-ttu-id="bd138-150">使用新的工具或技術通常隨附學習曲線。</span><span class="sxs-lookup"><span data-stu-id="bd138-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="bd138-151">幸運的是，NuGet 沒有不合理的學習曲線！</span><span class="sxs-lookup"><span data-stu-id="bd138-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="bd138-152">事實上，任何人都可以快速[開始取用套件](../quickstart/install-and-use-a-package-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="bd138-152">In fact, anyone can [get started consuming packages](../quickstart/install-and-use-a-package-in-visual-studio.md) quickly.</span></span>

<span data-ttu-id="bd138-153">也就是說，撰寫套件 (尤其是不錯的套件) 以及在自動化建置和部署程序中包含 NuGet 時，需要花費較多時間在下列資源：</span><span class="sxs-lookup"><span data-stu-id="bd138-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="bd138-154">NuGet 部落格</span><span class="sxs-lookup"><span data-stu-id="bd138-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="bd138-155">Twitter 上的 NuGet 小組@nuget</span><span class="sxs-lookup"><span data-stu-id="bd138-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="bd138-156">書籍：</span><span class="sxs-lookup"><span data-stu-id="bd138-156">Books:</span></span>
  - [<span data-ttu-id="bd138-157">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="bd138-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="bd138-158">NuGet 2 Essentials</span><span class="sxs-lookup"><span data-stu-id="bd138-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="bd138-159">個別套件的文件</span><span class="sxs-lookup"><span data-stu-id="bd138-159">Documentation for individual packages</span></span>

<span data-ttu-id="bd138-160">[NuDoq](http://nudoq.org) 提供直接存取，以及 NuGet 套件的更新和文件。</span><span class="sxs-lookup"><span data-stu-id="bd138-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="bd138-161">NuDoq 會定期輪詢最新套件更新的 nuget.org 資源庫伺服器、解除封裝和處理程式庫文件檔案，並據以更新網站。</span><span class="sxs-lookup"><span data-stu-id="bd138-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="bd138-162">新增專案</span><span class="sxs-lookup"><span data-stu-id="bd138-162">Adding your project</span></span>

<span data-ttu-id="bd138-163">如果您的 NuGet 生態系統專案是此頁面的重要新增，則請提交編輯此頁面的提取要求。</span><span class="sxs-lookup"><span data-stu-id="bd138-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>