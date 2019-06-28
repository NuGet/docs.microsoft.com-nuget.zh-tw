---
title: NuGet 1.2 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.2 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426195"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 版本資訊

[NuGet 1.0 和 1.1 版本資訊](../release-notes/nuget-1.1.md) | [NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md)

NuGet 1.2 於 2011 年 3 月 30 日發行。

## <a name="new-features"></a>新功能

### <a name="framework-profile-support"></a>Framework 設定檔支援

從開始時，NuGet 會支援具有程式庫為目標不同的架構。 但是現在套件可能會包含以特定的設定檔，例如 Windows Phone 設定檔為目標的組件。 若要以目標 framework 的特定設定檔，附加一個破折號後面的設定檔的縮寫。 比方說，若要在 Windows Phone (也稱為 Windows Phone 7) 上執行的 SilverLight 為目標，您可以將組件放在 sl3 wp 資料夾中，如下列螢幕擷取畫面所示。

![Framework 設定檔資料夾版面配置](./media/framework-profile-support.png)

您可能會問為什麼我們不只是選擇 「 wp7"做為 moniker。 中的情況下，我們會預期 Windows Phone 7 可能在未來執行較新版本的 Silverlight，在此情況下，您可能需要更明確了解您的架構設定檔就為目標的。

### <a name="automatically-add-binding-redirects"></a>自動新增繫結重新導向

當使用強式名稱組件安裝套件，NuGet 現在可以偵測表示專案需要繫結重新導向加入至專案，以編譯並自動新增它們的順序中的組態檔的情況。 第 3 部分 David Ebbo 的部落格文章系列的 NuGet 版本設定名為"[透過繫結重新導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"涵蓋更多詳細資料中的這項功能的目的。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>指定 Framework 組件參考 (GAC)

在某些情況下，封裝可能取決於.NET Framework 中的組件。 嚴格來說，它不一定需要取用者的您的套件參考的 framework 組件。 但在某些情況下，很重要的例如當開發人員必須針對該組件中的型別程式碼，才能使用您的套件。 新`frameworkAssemblies`項目，項目的子項目中繼資料，可讓您指定一組`frameworkAssembly`在 GAC 中的 Framework 組件所指向的項目。 請注意其重視 Framework 組件。
因為它們假設為每部電腦上，.NET Framework 的一部分，這些組件不會包含在套件中。 下表列出的屬性`frameworkAssembly`項目。


|屬性 |描述|
|----------------|-----------|
|**assemblyName**|*所需*。 這類的組件名稱`System.Net`。|
|**targetFramework**|*選擇性*。 可讓您指定架構和設定檔的名稱 （或別名），這個架構組件適用於 「 net40"或"sl4 」 等。 使用相同的格式中所述[支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 現在已能夠儲存 API 金鑰認證

使用 nuget.exe 命令列工具時，您現在可以使用 SetApiKey 命令來儲存您的 API 金鑰。 如此一來，您不需要指定它，每次您將封裝推送。 如需有關使用 nuget.exe，儲存您的 API 金鑰[閱讀相關文件發行套件](../nuget-org/publish-a-package.md)。

### <a name="package-explorer"></a>封裝總管
封裝總管 已更新為支援 NuGet 1.2。 如需詳細資訊，請參閱[封裝總管版本資訊](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。

## <a name="other-featuresfixes"></a>其他功能/修正程式

先前的清單是最明顯的許多我們實作的功能和我們已修正的 bug。 總而言之，我們實作/修正[59 工作項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)在此版本中。

## <a name="known-issues"></a>已知問題

* **1.2 封裝不相容**:使用命令列工具的最新版本建置的套件，nuget.exe (> 1.2) 不適用於舊版的 NuGet VS 增益集 （例如 1.1)。 如果您遇到錯誤訊息，說明不相容的結構描述相關的項目時，您遇到這個錯誤。 請更新至最新版的 NuGet。
* **NuGet.Server 不相容**:如果您正在裝載內部的 NuGet 摘要使用 NuGet.Server 的專案，您必須使用最新版的 NuGet.Server 更新該專案。
* **簽章不相符錯誤**:如果您使用相關的簽章不相符的訊息升級期間遇到錯誤，必須先解除安裝 NuGet，然後再進行安裝。 這會列在我們[已知問題頁面](../release-notes/known-issues.md)提供更多詳細資料。 此問題只會影響執行 Visual Studio 2010 SP1，且資料不正確地簽署 NuGet 1.0 一起安裝的版本。 此版本已僅能從 CodePlex 網站在短時間內讓此問題，應該不會影響太多人。