---
title: NuGet 2.6 版本資訊
description: 適用于 WebMatrix 的 NuGet 2.6.1 版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384120"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 版本資訊

[Nuget 2.5 版本](../release-notes/nuget-2.5.md)資訊 | [Nuget 2.6.1 for WebMatrix 版本](../release-notes/nuget-2.6.1-for-webmatrix.md)資訊

NuGet 2.6 已于2013年6月26日發行。

## <a name="notable-features-in-the-release"></a>版本中值得注意的功能

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 的支援

NuGet 2.6 是提供 Visual Studio 2013 支援的第一版。 和 Visual Studio 2012 一樣，NuGet 套件管理員延伸模組會包含在每個 Visual Studio 版本中。

為了提供 Visual Studio 2013 的最佳支援，同時仍然支援 Visual Studio 2010 和 Visual Studio 2012，並盡可能縮小擴充大小，我們會為 Visual Studio 2013 產生個別的延伸模組，原始延伸模組會繼續以 Visual Studio 2010 和2012為目標。

從 NuGet 2.6 開始，我們將發佈兩個延伸模組，如下所示：

1. [NuGet 套件管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)（適用于 Visual Studio 2010 和2012）
1. [Visual Studio 2013 的 NuGet 套件管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

在此分割中， [nuget.org](https://nuget.org)首頁的 [安裝 nuget] 按鈕會帶您前往 [[正在安裝 nuget](../install-nuget-client-tools.md) ] 頁面，您可以在其中找到有關安裝不同 nuget 用戶端的詳細資訊。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 轉換支援

NuGet 用戶端最常要求的功能之一，就是使用用於 Visual Studio 組建設定轉換的 XDT 轉換引擎，支援更強大的 XML 轉換。

我們在2013年4月提出有關 XDT 的 NuGet 支援的兩個重大公告。 第一種是 XDT 程式庫本身本身是[以 NuGet 套件的形式發行](https://nuget.org/packages/Microsoft.Web.Xdt)，並[開放在 CodePlex 上](http://xdt.codeplex.com/)。 此步驟已啟用可供其他開放原始碼軟體免費使用的 XDT 引擎，包括 NuGet 用戶端。 第二個宣告是在 NuGet 用戶端中支援使用 XDT 引擎進行轉換的計畫。 NuGet 2.6 包括此整合。

#### <a name="how-it-works"></a>運作方式

若要利用 NuGet 的 XDT 支援，此機制看起來類似于目前的設定[轉換功能](../create-packages/source-and-config-file-transformations.md)。
轉換檔案會新增至封裝的 content 資料夾。 不過，雖然設定轉換使用單一檔案進行安裝和卸載，但 XDT 轉換會使用下列檔案，對這兩個處理常式進行細微的控制：

- Web.config. install. xdt
- Web.config. xdt

此外，NuGet 會使用檔案尾碼來判斷要針對轉換執行的引擎，因此使用現有 web.config 的封裝將會繼續運作。 XDT 轉換也可以套用至任何 XML 檔案（而不只是 web.config），因此您可以針對專案中的其他應用程式運用此功能。

#### <a name="what-you-can-do-with-xdt"></a>您可以使用 XDT 執行的動作

其中一個 XDT 最大的優點是，它是[簡單但功能強大的語法](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110))，用於操作 XML DOM 的結構。 XDT 會以各種不同的方式，從簡單的屬性名稱比對到完整的 XPath 支援，而不只是將一個固定的檔結構覆迭至另一個結構。 一旦找到相符的元素或一組元素，XDT 就會提供一組豐富的函式來操作專案，不論是要加入、更新或移除屬性、在特定位置放置新專案，或是取代或移除整個元素及其子系。

### <a name="machine-wide-configuration"></a>全電腦設定

NuGet 的其中一個絕佳優點，就是將某個大型的可執行檔或程式庫細分成一組可整合的模組化元件，而且最重要的是獨立維護和設定版本。 不過，這一點的副作用是，產品或產品系列的傳統概念可能會更分散。
NuGet 的自訂套件來源功能提供了一種組織套件的方式;不過，自訂套件來源無法自行探索。

NuGet 2.6 藉由搜尋路徑% ProgramData%/NuGet/Config. 下的資料夾階層，擴充設定 NuGet 的邏輯。產品安裝程式可以在此資料夾下新增自訂的 NuGet 設定檔案，以註冊其產品的自訂套件來源。 此外，資料夾結構也支援產品、版本，甚至是 IDE SKU 的語義。 這些目錄中的設定會依照下列順序套用，並具有「最後一個勝出」優先順序策略。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{版本}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{版本}\{SKU}\*.config

在這份清單中，{IDE} 預留位置專屬於 NuGet 執行所在的 IDE，因此在 Visual Studio 的情況下，它將會是 "VisualStudio"。 IDE 會提供 {Version} 和 {SKU} 預留位置（例如分別為 "11.0" 和 "WDExpress"、"VWDExpress" 和 "Pro"）。 該資料夾可以包含許多不同的 * .config 檔案。
因此，ACME component company 可以做為其產品安裝程式的一部分，藉由建立下列檔案路徑來新增自訂套件來源，只有在 Professional 和旗艦版的 Visual Studio 2012 中才會顯示：

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

雖然資料夾結構可讓軟體安裝程式之類的程式直接將電腦範圍的套件來源新增至 NuGet 的設定，但 NuGet 設定對話方塊也已更新，可允許以使用者特定的方式（例如在% AppData%/NuGet/NuGet.Config 中註冊）或整部電腦來註冊套件來源。

這項功能是由 Visual Studio 2013 所使用，其中檔案安裝在：

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

在此檔案中，已設定稱為「.NET Framework 封裝」的新封裝來源。

![NuGet 設定檔電腦範圍設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>CoNtextualizing 搜尋

由於 NuGet 資源庫所服務的套件數目會繼續以指數步調成長，因此改善搜尋會一直出現在 NuGet 優先順序清單的頂端。 NuGet 的其中一個規劃功能是內容性搜尋，這表示 NuGet 會使用您所使用之 Visual Studio 版本和 SKU 的相關資訊，以及您要建立的專案類型，做為判斷潛在搜尋相關性的準則更.

從 NuGet 2.6 開始，每次安裝套件時，安裝的內容都會記錄為安裝作業資料的一部分。  搜尋也會傳送相同的內容資訊，讓 NuGet 資源庫可透過內容相關的安裝趨勢來提升搜尋結果。  NuGet 資源庫的未來更新將會啟用此內容相關的相關性提升。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>追蹤直接安裝與相依性安裝

套件作者會依賴 NuGet 資源庫上提供的[套件統計資料](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)。  作者所要求的一個重要的資料點，是直接套件安裝和相依性安裝之間的差異。  到目前為止，NuGet 用戶端不會在安裝作業前後傳送任何內容，不論開發人員是否直接安裝套件，或是安裝它以滿足相依性。
從 NuGet 2.6 開始，現在會針對安裝作業傳送該資料。  NuGet 資源庫上的套件統計資料會以個別的安裝作業（具有「相依性」尾碼）公開該資料。

* 安裝
* 安裝-相依性
* 更新
* 更新-相依性
* 重新安裝
* 重新安裝-相依性

除了不同的作業名稱之外，也會記錄相依封裝識別碼以供安裝。  NuGet 資源庫的未來更新將會在報表中公開該資料，讓套件作者能夠完全瞭解開發人員安裝其套件的方式。

## <a name="bug-fixes"></a>Bug 修正

NuGet 2.6 也包含數個 bug 修正。 如需 NuGet 2.6 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。