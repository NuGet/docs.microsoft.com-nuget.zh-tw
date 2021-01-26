---
title: NuGet 2.6 版本資訊
description: 適用于 WebMatrix 的 NuGet 2.6.1 版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 812a0e806e29c5a2141db4f2fbab4bf91b0983f9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776831"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 版本資訊

[NuGet 2.5 版本](../release-notes/nuget-2.5.md)  |  資訊[適用于 WebMatrix 的 NuGet 2.6.1 版本](../release-notes/nuget-2.6.1-for-webmatrix.md)資訊

NuGet 2.6 已于2013年6月26日發行。

## <a name="notable-features-in-the-release"></a>版本中的值得注意功能

### <a name="support-for-visual-studio-2013"></a>支援 Visual Studio 2013

NuGet 2.6 是提供 Visual Studio 2013 支援的第一個版本。 和 Visual Studio 2012 一樣，NuGet 封裝管理員擴充功能也包含在每一版的 Visual Studio 中。

為了提供 Visual Studio 2013 的最佳可能支援，同時同時支援 Visual Studio 2010 和 Visual Studio 2012，以及盡可能將延伸大小保持在最小的範圍，我們會為 Visual Studio 2013 產生個別的擴充功能，而原始延伸模組會繼續以 Visual Studio 2010 和2012為目標。

從 NuGet 2.6 開始，我們將發佈兩個擴充功能，如下所示：

1. [NuGet 封裝管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (適用于 Visual Studio 2010 和 2012) 
1. [適用于 Visual Studio 2013 的 NuGet 封裝管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

透過此分割， [nuget.org](https://nuget.org) 首頁的 [安裝 nuget] 按鈕會帶您前往 [ [正在安裝 nuget](../install-nuget-client-tools.md) ] 頁面，您可以在其中找到安裝不同 nuget 用戶端的詳細資訊。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 轉換支援

NuGet 用戶端最具高度要求的功能之一，就是使用 XDT 轉換引擎（用於 Visual Studio 組建設定轉換）來支援更強大的 XML 轉換。

在2013年4月，我們對 XDT 的 NuGet 支援提出兩個相關的大型宣告。 第一個是 XDT 程式庫本身本身是 [以 NuGet 套件的形式發行](https://nuget.org/packages/Microsoft.Web.Xdt) ，並 [在 CodePlex 上開放](http://xdt.codeplex.com/)原始碼。 此步驟已讓其他開放原始碼軟體（包括 NuGet 用戶端）可自由使用 XDT 引擎。 第二個宣告是在 NuGet 用戶端中支援使用 XDT 引擎進行轉換的計畫。 NuGet 2.6 包含這種整合。

#### <a name="how-it-works"></a>運作方式

為了充分利用 NuGet 的 XDT 支援，此機制看起來類似于目前的設定 [轉換功能](../create-packages/source-and-config-file-transformations.md)。
轉換檔案會新增至套件的內容資料夾。 不過，雖然設定轉換使用單一檔案進行安裝和卸載，但 XDT 轉換可讓您使用下列檔案，對這兩個處理常式進行細微的控制：

- Web.config 安裝. xdt
- Web.config 卸載. xdt

此外，NuGet 會使用檔案尾碼來判斷要針對轉換執行的引擎，因此使用現有 web.config 的封裝。轉換將繼續運作。 XDT 轉換也可以套用至任何 XML 檔案 (而不只是 web.config) ，所以您可以將此專案運用於專案中的其他應用程式。

#### <a name="what-you-can-do-with-xdt"></a>您可以使用 XDT 來做什麼

其中一個 XDT 的最大優點是它的 [簡單但功能強大的語法](/previous-versions/aspnet/dd465326(v=vs.110)) ，可操作 XML DOM 的結構。 XDT 會以各種不同的方式（從簡單的屬性名稱比對到完整的 XPath 支援）提供可比對專案的控制項，而不是直接將一個固定檔結構覆迭至另一個結構。 一旦找到相符的元素或一組元素，XDT 就會提供一組豐富的函式來操作專案，不論是加入、更新或移除屬性、將新專案放在特定位置，或是取代或移除整個元素及其子系。

### <a name="machine-wide-configuration"></a>Machine-Wide 設定

NuGet 最大的優點之一，就是將其他大型的可執行檔或程式庫分成一組可以整合的模組化元件，而且最重要的是獨立維護和建立版本。 不過，這項功能的其中一個副作用是產品或產品系列的傳統概念可能會更分散。
NuGet 的自訂套件來源功能提供一種組織套件的方式;不過，自訂套件來源無法自行探索。

NuGet 2.6 藉由搜尋路徑% ProgramData%/NuGet/Config. 下的資料夾階層，擴充設定 NuGet 的邏輯。產品安裝程式可以在此資料夾下新增自訂 NuGet 設定檔，以註冊其產品的自訂套件來源。 此外，資料夾結構也支援產品、版本，甚至是 IDE SKU 的語法。 這些目錄中的設定會以下列順序套用，並以「最後在 wins 中」優先順序策略來套用。

1. %ProgramData%\NuGet\Config \* .config
2. %ProgramData%\NuGet\Config \{ IDE} \* .config
3. %ProgramData%\NuGet\Config \{ IDE} \{ 版本} \* .config
4. %ProgramData%\NuGet\Config \{ IDE} \{ 版本} \{ SKU} \* .config

在此清單中，{IDE} 預留位置是 NuGet 執行所在的 IDE 專用，因此在 Visual Studio 的情況下，它將會是 "VisualStudio"。 IDE (提供 {Version} 和 {SKU} 預留位置，例如 "11.0" 和 "WDExpress"、"VWDExpress" 和 "Pro"，分別) 。 資料夾可以包含許多不同的 * .config 檔案。
因此，在其產品安裝程式中，您可以藉由建立下列檔案路徑來新增自訂套件來源，而此來源只能在 Visual Studio 2012 的 Professional 和旗艦版中看見：

% ProgramData% \NuGet\Config\VisualStudio\11.0\Pro\acme.config

雖然資料夾結構可讓軟體安裝程式之類的程式直接將整個電腦的套件來源新增至 NuGet 的設定，但 NuGet 設定對話方塊也已更新，以允許將套件來源註冊為使用者特定的 (例如在% AppData%/NuGet/NuGet.Config) 或整部電腦上註冊。

這項功能是由 Visual Studio 2013 所使用，檔案會安裝在下列位置：

% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

在此檔案中，會設定名為「.NET Framework 套件」的新套件來源。

![NuGet 設定檔電腦的整個設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>CoNtextualizing 搜尋

由於 NuGet 資源庫所提供的套件數目持續以指數的步調成長，因此在 NuGet 優先權清單的最上方會持續改善搜尋。 其中一個 NuGet 規劃的功能是內容搜尋，這表示 NuGet 將會使用您所使用之 Visual Studio 版本和 SKU 的相關資訊，以及您要建立的專案類型，作為判斷潛在搜尋結果相關性的準則。

從 NuGet 2.6 開始，每次安裝套件時，會將安裝內容記錄為安裝作業資料的一部分。  搜尋也會傳送相同的內容資訊，讓 NuGet 資源庫能夠依內容安裝趨勢來提升搜尋結果。  NuGet 資源庫的未來更新將會啟用這種與內容相關的相關性提升。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>追蹤直接安裝與相依性安裝的比較

套件作者更依賴 NuGet 資源庫上提供的 [套件統計資料](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) 。  作者要求的一項重要的資料點是直接安裝套件與相依性安裝之間的差異。  到目前為止，NuGet 用戶端不會傳送任何有關安裝作業的內容，不論開發人員是否直接安裝套件，或是是否已安裝以滿足相依性。
從 NuGet 2.6 開始，現在會針對安裝作業傳送該資料。  NuGet 資源庫上的套件統計資料會將該資料公開為個別的安裝作業，並具有「相依性」尾碼。

* 安裝
* Install-Dependency
* 更新
* Update-Dependency
* 重新安裝
* Reinstall-Dependency

除了不同的作業名稱之外，也會記錄相依的封裝識別碼以進行安裝。  NuGet 資源庫的未來更新將會在報表中公開該資料，讓套件作者完全瞭解開發人員安裝其套件的方式。

## <a name="bug-fixes"></a>Bug 修正

NuGet 2.6 也包含數個 bug 修正。 如需 NuGet 2.6 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。