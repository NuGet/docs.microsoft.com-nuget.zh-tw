---
title: NuGet 2.6 版本資訊
description: Webmatrix 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.6.1 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551939"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 版本資訊

[NuGet 2.5 版本資訊](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix 版本資訊](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 已於 2013 年 6 月 26 日發行。

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 的支援

NuGet 2.6 是第一個版本所提供的 Visual Studio 2013 的支援。 例如 Visual Studio 2012，NuGet 套件管理員延伸模組包含在每個版本的 Visual Studio 中。

為了提供可行的最佳支援 Visual Studio 2013 同時支援 Visual Studio 2010 和 Visual Studio 2012 和保留的延伸模組大小越小越好，我們會產生另外的延伸模組時的 Visual Studio 2013原始副檔名會繼續以 Visual Studio 2010 和 2012年為目標。

從 NuGet 2.6 開始，我們將發佈兩個延伸模組，如下所示：

1. [NuGet 套件管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)（適用於 Visual Studio 2010 和 2012年）
1. [Visual Studio 2013 的 NuGet 套件管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

此分割中， [nuget.org](https://nuget.org)首頁的 「 安裝 NuGet"按鈕會帶您前往[安裝 NuGet](../install-nuget-client-tools.md)頁面上，您可以在其中找到安裝不同的 NuGet 用戶端的詳細資訊。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 轉換的支援

NuGet 用戶端的最高要求的功能之一就是支援更強大的 XML 轉換使用 XDT 轉換引擎會在 Visual Studio 組建組態轉換。

在 2013 年 4 月中，我們所做的有關 XDT 的 NuGet 支援的兩個大公告。 第一是 XDT 程式庫本身正在被本身[NuGet 套件形式發行](https://nuget.org/packages/Microsoft.Web.Xdt)並[CodePlex 上的開放原始碼](http://xdt.codeplex.com/)。 此步驟中啟用 XDT 引擎，可供自由其他開放原始碼軟體，包括 NuGet 用戶端。 第二個宣告是要支援 NuGet 用戶端中的轉換使用 XDT 引擎的計劃。 NuGet 2.6 包含這項整合。

#### <a name="how-it-works"></a>它的運作方式

若要充分利用 NuGet 的 XDT 支援，機制看起來類似[目前的組態轉換功能](../create-packages/source-and-config-file-transformations.md)。
轉換檔案新增至套件的內容資料夾。 不過，雖然組態轉換會使用單一檔案的安裝和解除安裝，XDT 轉換就會啟用更細微的控制這兩個這些處理程序，使用下列檔案：

- Web.config.install.xdt
- Web.config.uninstall.xdt

此外，NuGet 會使用檔案後置字元來判斷哪些引擎來執行轉換，以便使用現有的 web.config.transforms 封裝將會繼續運作。 XDT 轉換也可以套用至任何 XML 檔案 (不只是 web.config)，讓您可以對其他應用程式中利用這，在您的專案。

#### <a name="what-you-can-do-with-xdt"></a>您可以執行含有 XDT

其中一個 XDT 的最大優點是其[簡單但功能強大的語法](http://msdn.microsoft.com/library/dd465326.aspx)來操作 XML DOM 的結構 而不是直接覆疊一個固定格式文件結構到另一個結構，XDT 會提供控制項，可比對各種不同的方式，從簡單的屬性名稱比對完整 XPath 支援的項目。 一旦找到相符的項目或項目集，XDT 提供一組豐富的函式操作項目，而不論其是指新增、 更新或移除屬性，將新的項目放在特定位置，或取代或移除整個元素和其子系。

### <a name="machine-wide-configuration"></a>整部機器組態

NuGet 的優點之一是，它會細分否則大型的可執行檔或程式庫的模組化元件都可以獨立整合，以及最重要的是維護與已建立版本的一組。 其中一項副作用，不過，是傳統的產品或產品系列概念可能變得更分散。
NuGet 的自訂套件來源功能提供的其中一種組織封裝，不過，自訂套件來源並不會自行探索。

NuGet 2.6 延伸來設定 NuGet 搜尋路徑 %programdata%/nuget/config 下的資料夾階層的邏輯。產品安裝程式可以加入自訂的 NuGet 組態檔，在此資料夾中註冊他們的產品的自訂套件來源。 此外，資料夾結構支援語意的產品、 版本和甚至是 SKU 的 IDE。 依下列順序 「 後進先 「 優先順序策略會套用這些目錄中的設定。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

在此清單中，以便在 Visual Studio 中，案例中，它會是"VisualStudio 」，是針對 IDE 中執行 NuGet，{IDE} 預留位置。 {Version} 和 {SKU} 預留位置所提供的 IDE （例如："11.0"和"WDExpress"、"VWDExpress 」 和 「 專業 」，分別)。 資料夾可以則包含許多不同的 *.config 檔案。
因此，ACME 元件公司，其產品安裝程式的過程中，新增將只會出現在 Visual Studio 2012 Professional 和 Ultimate 版本建立下列檔案路徑的自訂套件來源：

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

雖然資料夾結構，並直接將整部電腦的套件來源新增至 NuGet 組態的軟體安裝程式 」 等方案，NuGet 組態對話方塊也已經更新，以便為套件來源的註冊其中一個特定使用者 （例如登錄 %appdata%/nuget/nuget.config 中） 或整部電腦。

這項功能會利用 Visual Studio 2013，在安裝檔案的位置：

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

在此檔案中，新的封裝來源，稱為 「.NET Framework 封裝 」 設定。

![NuGet 組態檔機器的各種設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>內容化搜尋

因為 NuGet 資源庫所提供的套件數目持續迅速成長，改善搜尋會保持為曾經 NuGet 優先順序清單的頂端。 NuGet 的計劃的功能之一是搜尋的專案的內容相關式搜尋，也就是說，NuGet 會使用版本和 SKU 的 Visual Studio，您會使用和您要建置類型相關資訊作為準則來判斷潛在相關性結果。

從 NuGet 2.6 開始，安裝套件時，每次安裝的內容會記錄安裝作業資料的一部分。  搜尋也會傳送相同的內容資訊，這可讓 NuGet 資源庫，來提升搜尋結果的內容安裝趨勢。  未來的更新至 NuGet 資源庫會啟用此內容相關的關聯性的提升。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>追蹤直接安裝 vs。相依性安裝

套件作者可以依賴越來越[封裝的統計資料](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)在 NuGet Gallery 上提供。  其中一個重要的遺漏資料點的作者，提出的要求是直接的套件會安裝與相依性安裝之間的差異。  到目前為止，NuGet 用戶端未傳送任何開發人員是否直接安裝套件，或如果在安裝符合相依性安裝作業的內容。
從開始，使用 NuGet 2.6 中現在會將資料傳送為安裝操作。  封裝在 NuGet Gallery 上的統計資料會公開為個別的安裝作業，該資料與 「-相依性"後置詞。

* 安裝
* 安裝相依性
* 更新
* 更新相依性
* 重新安裝
* 重新安裝相依性

除了不同的作業名稱，也會記錄相依的套件識別碼進行安裝。  在 NuGet Gallery 的未來更新會公開該報表，讓套件作者將全面了解如何開發人員要安裝其套件內的資料。

## <a name="bug-fixes"></a>Bug 修正

NuGet 2.6 也包含數個 bug 修正。 如需完整的工作清單項目中已修正 NuGet 2.6，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。