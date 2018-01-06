---
title: "NuGet 1.2 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 48f23141-b2ad-4cdf-8d81-7bb6b9419aa6
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.2 的版本資訊。"
keywords: "NuGet 1.2 的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 79e82f19d2be96fee3832eeb24ebb443aebc2b64
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 的版本資訊

[NuGet 1.0 和 1.1 版本資訊](../release-notes/nuget-1.1.md) | [NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md)

NuGet 1.2 起已於 2011 年 3 月 30 日發行。

## <a name="new-features"></a>新功能

### <a name="framework-profile-support"></a>支援 framework 設定檔

從開始，NuGet 會支援具有程式庫以不同的架構為目標。 但現在封裝可能包含以特定的設定檔，例如 Windows Phone 設定檔為目標的組件。 若要以特定架構的設定檔為目標，附加破折號，後面接著的設定檔的縮寫。 例如，若要在 Windows Phone (也稱為 Windows Phone 7) 上執行的 SilverLight，您可以將組件 sl3 wp 資料夾如下列螢幕擷取畫面所示。

![Framework 設定檔資料夾版面配置](./media/framework-profile-support.png)

您可能會要求為什麼我們不只要選擇"wp7"做為 moniker。 部分，我們所預期，Windows Phone 7 可能在未來執行較新版的 Silverlight，在此情況下，您可能需要更特定的對您的 framework 設定檔是以。

### <a name="automatically-add-binding-redirects"></a>繫結重新導向自動加入

當強式名稱組件的安裝套件，NuGet 現在可以偵測專案需要繫結重新導向加入至編譯，並將其自動加入專案中的組態檔的情況。 第 3 部分 David Ebbo 部落格文章系列的 NuGet 版本控制標題為 「[透過繫結重新導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"涵蓋更多詳細資料中的這項功能的目的。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>指定 Framework 組件參考 (GAC)

在某些情況下，封裝可能取決於為.NET Framework 中的組件。 嚴格來說，它不一定需要取用者，您的封裝參考 framework 組件。 但在某些情況下，是很重要的例如，開發人員必須撰寫程式碼對該組件中的型別才能使用您的封裝。 新`frameworkAssemblies`項目，項目的子項目中繼資料，可讓您指定的一組`frameworkAssembly`Framework 組件在 GAC 中所指向的項目。 請注意在 Framework 組件上的強調。
假設為每部電腦上，.NET Framework 的一部分時，這些組件不會包含在封裝中。 下表列出的屬性`frameworkAssembly`項目。


|屬性 |描述|
|----------------|-----------|
|**assemblyName**|*需要*。 例如，組件名稱`System.Net`。|
|**targetFramework**|*選擇性*。 可讓您指定架構和設定檔名稱 （或別名），例如"net40"或"sl4"適用於這個 framework 組件。 使用相同的格式中所述[支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 現在是能夠將儲存 API 金鑰認證

使用 nuget.exe 命令列工具時，您現在可以使用 SetApiKey 命令來儲存您的 API 金鑰。 這樣一來，您不需要每次推送封裝，請指定它。 如需詳細資訊以 nuget.exe，儲存您的 API 金鑰[讀取發行套件的文件](../create-packages/publish-a-package.md)。

### <a name="package-explorer"></a>封裝總管
封裝總管 已更新為支援 NuGet 1.2。 如需詳細資訊，請參閱[封裝總管 的版本資訊](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。

## <a name="other-featuresfixes"></a>其他功能/修正

上述清單了許多我們實作的功能和我們已修正的 bug 最為明顯。 總而言之，我們實作/修正[59 工作項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)在此版本中。

## <a name="known-issues"></a>已知問題

* **1.2 封裝不相容**： 使用命令列工具的最新版本建立套件、 nuget.exe (> 1.2) 不適用於舊版的 NuGet VS 增益集 （例如 1.1)。 如果遇到錯誤訊息，說明不相容的結構描述相關的項目時，會發生這個錯誤。 請更新至最新版的 NuGet。
* **NuGet.Server 不相容**： 如果您正在裝載內部的 NuGet 摘要使用 NuGet.Server 專案，您必須使用最新版的 NuGet.Server 更新該專案。
* **簽章不相符錯誤**： 如果您使用簽章不相符，相關訊息升級期間執行時發生錯誤，您必須先解除安裝 NuGet，然後再進行安裝。 這會列在我們[已知問題頁面](../release-notes/Known-Issues.md)提供更多詳細資料。 問題只會影響這些執行 Visual Studio 2010 SP1，且有新版 NuGet 1.0 安裝未正確簽署。 這個版本只對可從 CodePlex 網站一小段時間無法讓此問題應該不會太多人的影響。