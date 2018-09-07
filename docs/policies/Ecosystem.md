---
title: NuGet 生態系統概觀
description: NuGet 生態系統中的完整資源，包含 NuGet 來源、非 Microsoft NuGet 專案、公用程式和訓練教材。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548140"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet 生態系統的概觀

NuGet 是在 2010 年引進，因此極有可能改善和自動化開發程序的不同層面。

因為 NuGet 是 [Apache v2 授權](http://choosealicense.com/licenses/apache/)許可的開放原始碼，所以其他專案可以利用 NuGet，而且公司可以在產品中建置其支援。 不論針對開放原始碼專案還是企業應用程式開發，NuGet 以及根據 NuGet 建置的其他應用程式都提供多種生態系統工具來改善軟體開發程序。

因為開發人員的參與，所有這些專案都可以創新。 就如同您參與 NuGet 本身一樣，也會透過報告缺失和新功能想法來參與這些專案，並提供意見、撰寫文件，同時盡可能提供程式碼。

## <a name="net-foundation-projects"></a>.NET Foundation 專案

NuGet 提供 Microsoft 開發平台的免費開放原始碼套件管理系統。 它包含一些用戶端工具，以及包含[正式 NuGet 資源庫](http://www.nuget.org)的服務集。 這些合併使用可以形成 [.NET Foundation](http://www.dotnetfoundation.org/) 所治理的 NuGet 專案。

NuGet 組織包含 GitHub 上的各種存放庫。 [https://github.com/Nuget/Home](https://github.com/Nuget/Home) 概述所有存放庫以及可尋找各種 NuGet 元件的位置。

## <a name="microsoft-projects"></a>Microsoft 專案

Microsoft 大量參與 NuGet 的開發。 Microsoft 員工所做的所有參與也是開放原始碼並捐獻 (包含著作權) 給 .NET Foundation。

## <a name="non-microsoft-projects"></a>非 Microsoft 專案

許多其他個人和公司都對 NuGet 生態系統有重大貢獻。 這裡所列之每個專案的授權可能會與核心 NuGet 元件不同，因此請確認授權條款可接受後再使用：

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (或 NuGet-as-a-service)](http://www.myget.org/)
- [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet 伺服器](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin 和 MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>其他 NuGet 公用程式

這些是根據 NuGet 所建置的工具和公用程式：

- [Glimpse 延伸模組](http://getglimpse.com/Packages) (外掛程式是套件)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (CMS 模組是從 Orchard 資源庫中所裝載的 v1 NuGet 摘要中擷取)
- [NuGet 伺服器的 Java 實作](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (推出新套件發行集的 Twitter 機器人)
- [DefinitelyTyped](http://definitelytyped.org/) ([自動](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript 類型 [發行至 NuGet 的定義](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>訓練教材和參考

使用新的工具或技術通常隨附學習曲線。 幸運的是，NuGet 沒有不合理的學習曲線！ 事實上，任何人都可以快速[開始取用套件](../quickstart/use-a-package.md)。

也就是說，撰寫套件 (尤其是不錯的套件) 以及在自動化建置和部署程序中包含 NuGet 時，需要花費較多時間在下列資源：

- [NuGet 部落格](http://blog.nuget.org/)
- [Twitter 上的 NuGet 小組@nuget](http://twitter.com/nuget)
- 書籍：
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>個別套件的文件

[NuDoq](http://nudoq.org) 提供直接存取，以及 NuGet 套件的更新和文件。

NuDoq 會定期輪詢最新套件更新的 nuget.org 資源庫伺服器、解除封裝和處理程式庫文件檔案，並據以更新網站。

## <a name="adding-your-project"></a>新增專案

如果您的 NuGet 生態系統專案是此頁面的重要新增，則請提交編輯此頁面的提取要求。
