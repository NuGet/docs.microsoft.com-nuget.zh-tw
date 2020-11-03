---
title: NuGet 1.2 版本資訊
description: NuGet 1.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237178"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 版本資訊

[NuGet 1.0 和1.1 版本](../release-notes/nuget-1.1.md)  |  資訊[NuGet 1.3 版本](../release-notes/nuget-1.3.md)資訊

NuGet 1.2 已于2011年3月30日發行。

## <a name="new-features"></a>新功能

### <a name="framework-profile-support"></a>架構設定檔支援

從一開始，NuGet 支援的程式庫會以不同的架構為目標。 但現在套件可能包含以特定設定檔為目標的元件，例如 Windows Phone 設定檔。 若要以特定的架構設定檔為目標，請在設定檔縮寫後面附加虛線。 例如，若要以 Windows Phone 上執行的 SilverLight 為目標 (又稱為 Windows Phone 7) ，您可以將元件放在 sl3-wp 資料夾中，如下列螢幕擷取畫面所示。

![架構設定檔資料夾版面配置](./media/framework-profile-support.png)

您可能會問為什麼我們不只是選擇使用 "wp7" 做為標記。 在某些情況下，我們預期 Windows Phone 7 可能會在未來執行較新版的 Silverlight，在這種情況下，您可能需要更明確地瞭解您所瞄準的 framework 設定檔。

### <a name="automatically-add-binding-redirects"></a>自動新增系結重新導向

安裝具有強式名稱元件的封裝時，NuGet 現在可以偵測到專案需要將系結重新導向新增至設定檔的情況，以便讓專案自動進行編譯和新增。 David Ebbo 的第3部分，其 NuGet 版本設定為「透過系結重新[導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)」，涵蓋了這項功能在更多詳細資料中的用途。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>指定 (GAC) 的架構元件參考

在某些情況下，套件可能相依于 .NET Framework 中的元件。 嚴格來說，您的套件取用者不一定需要參考架構元件。 但在某些情況下，這一點很重要，例如，當開發人員需要針對該元件中的型別撰寫程式碼才能使用您的封裝時。 新 `frameworkAssemblies` 元素（中繼資料專案的子專案）可讓您指定一組 `frameworkAssembly` 指向 GAC 中 Framework 元件的元素。 請注意架構元件的重點。
這些元件不會包含在套件中，因為它們會假設在每部電腦上都是 .NET Framework 的一部分。 下表列出專案的屬性 `frameworkAssembly` 。


|屬性 |描述|
|----------------|-----------|
|**集**|*必要* 。 元件的名稱，例如 `System.Net` 。|
|**targetFramework**|*選擇項* 。 允許指定架構和設定檔名稱 (或) 此 framework 元件套用的別名，例如 "net40" 或 "sl4"。 使用 [支援多個目標 framework](../create-packages/supporting-multiple-target-frameworks.md)所述的相同格式。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 現在可以儲存 API 金鑰認證

使用 nuget.exe 命令列工具時，您現在可以使用 SetApiKey 命令來儲存您的 API 金鑰。 如此一來，您就不需要在每次推送套件時指定它。 如需有關使用 nuget.exe 儲存 API 金鑰的詳細資訊，請 [參閱發行封裝的相關檔](../nuget-org/publish-a-package.md)。

### <a name="package-explorer"></a>封裝 Explorer
套件瀏覽器已更新為支援 NuGet 1.2。 如需詳細資訊，請參閱 [套件瀏覽器版本](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)資訊。

## <a name="other-featuresfixes"></a>其他功能/修正

前一份清單最明顯的是我們所執行的許多功能，以及我們修正的 bug。 畢竟，我們已在此版本中執行/修正了 [59 工作專案](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) 。

## <a name="known-issues"></a>已知問題

* **1.2 套件不相容** ：以最新版本的命令列工具建立的套件，nuget.exe ( # A0 1.2) 將無法搭配舊版 NuGet 與增益集 (，例如 1.1) 。 如果您遇到錯誤訊息，說明不相容的架構，則表示您遇到此錯誤。 請將 NuGet 更新至最新版本。
* **Nuget. 伺服器不相容** ：如果您使用 nuget.exe 專案裝載內部 nuget 摘要，您必須使用最新版本的 nuget.exe 來更新該專案。
* 簽章 **不符錯誤** ：如果在升級期間發生錯誤，並顯示簽章不相符的訊息，您必須先卸載 NuGet，然後再安裝。 這會列在 [ [已知問題] 頁面](../release-notes/known-issues.md) 中，以提供更多詳細資料。 此問題只會影響執行 Visual Studio 2010 SP1 的版本，並已安裝不正確簽署的 NuGet 1.0 版本。 此版本僅可從 CodePlex 網站取得一小段時間，因此此問題不會影響太多人。