---
title: NuGet 1.2 版本資訊
description: NuGet 1.2 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429084"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 版本資訊

[Nuget 1.0 和1.1 版本](../release-notes/nuget-1.1.md)資訊 | [nuget 1.3 版本](../release-notes/nuget-1.3.md)資訊

NuGet 1.2 已于2011年3月30日發行。

## <a name="new-features"></a>新功能

### <a name="framework-profile-support"></a>架構設定檔支援

從一開始，NuGet 支援的程式庫以不同的架構為目標。 但現在封裝可能包含以特定設定檔（例如 Windows Phone 設定檔）為目標的元件。 若要以架構的特定設定檔為目標，請在設定檔縮寫後面附加一個破折號。 例如，若要以 Windows Phone 上執行的 SilverLight （也稱為 Windows Phone 7）為目標，您可以將元件放在 sl3-wp 資料夾中，如下列螢幕擷取畫面所示。

![架構設定檔資料夾版面配置](./media/framework-profile-support.png)

您可能會問，為什麼我們並未直接選擇使用 "wp7" 做為名字。 在某些情況下，我們預期 Windows Phone 7 可能會在未來執行較新版本的 Silverlight，在此情況下，您可能需要更明確地瞭解您所瞄準的架構設定檔。

### <a name="automatically-add-binding-redirects"></a>自動加入系結重新導向

安裝具有強式命名元件的套件時，NuGet 現在可以偵測到專案需要將系結重新導向新增至設定檔的情況，讓專案能夠自動進行編譯及新增。 David Ebbo 的第3部分：關於 NuGet 版本設定的「透過系結重新[導向進行統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)」，涵蓋此功能的目的。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>指定架構元件參考（GAC）

在某些情況下，封裝可能相依于 .NET Framework 中的元件。 嚴格來說，您的套件取用者不一定需要參考架構元件。 但在某些情況下，這一點很重要，例如，開發人員必須針對該元件中的型別撰寫程式碼，才能使用您的封裝。 新的 `frameworkAssemblies` 專案（metadata 元素的子專案）可讓您指定一組指向 GAC 中之架構元件的 `frameworkAssembly` 元素。 請注意架構元件的重點。
這些元件不會包含在您的套件中，因為它們會被視為 .NET Framework 中的每一部電腦上。 下表列出 `frameworkAssembly` 元素的屬性。


|屬性 |描述|
|----------------|-----------|
|**assemblyName**|*必要*。 元件的名稱，例如 `System.Net`。|
|**targetFramework**|*選擇性*。 允許指定此架構元件所適用的架構和設定檔名稱（或別名），例如 "net40" 或 "sl4"。 使用[支援多個目標 framework](../create-packages/supporting-multiple-target-frameworks.md)中所述的相同格式。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 現在能夠儲存 API 金鑰認證

使用 nuget.exe 命令列工具時，您現在可以使用 SetApiKey 命令來儲存您的 API 金鑰。 如此一來，您就不需要在每次推送封裝時指定它。 如需有關使用 nuget.exe 來儲存 API 金鑰的詳細資訊，請[參閱發行封裝的相關檔](../nuget-org/publish-a-package.md)。

### <a name="package-explorer"></a>封裝瀏覽器
Package Explorer 已更新為支援 NuGet 1.2。 如需詳細資訊，請參閱[Package Explorer 版本](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)資訊。

## <a name="other-featuresfixes"></a>其他功能/修正程式

前一份清單是我們所實行的許多功能和我們修正的 bug 中最明顯的一項。 畢竟，我們已在此版本中執行/修正[59 工作專案](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。

## <a name="known-issues"></a>已知問題

* **1.2 套件不相容**：使用最新版本的命令列工具所建立的套件，nuget.exe （> 1.2）將無法使用舊版 Nuget VS 增益集（例如1.1）。 如果您遇到錯誤訊息，指出有關不相容架構的問題，則表示您遇到此錯誤。 請將 NuGet 更新為最新版本。
* **Nuget. 伺服器不相容**：如果您要使用 nuget.exe 專案裝載內部 NuGet 摘要，則必須使用最新版的 Nuget. 伺服器來更新該專案。
* 簽章**不相符錯誤**：如果您在升級期間遇到錯誤，但有簽章不相符的訊息，您必須先卸載 NuGet，然後再進行安裝。 這會列在我們的「[已知問題」頁面](../release-notes/known-issues.md)中，其中提供更多詳細資料。 此問題只會影響執行 Visual Studio 2010 SP1 且安裝了不正確簽署之 NuGet 1.0 版本的作業。 這個版本只會在 CodePlex 網站上提供一小段時間，因此此問題不會影響太多人。