---
title: "NuGet 2.6 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.6 版本資訊。"
keywords: "NuGet 2.6 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2df9721e6941c110948af1a2d4ec4b7aeb476dd
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 版本資訊

[NuGet 2.5 版本資訊](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 WebMatrix 版本資訊](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 已於 2013 年 6 月 26 日發行。

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 的支援

NuGet 2.6 是第一次釋放所提供的 Visual Studio 2013 的支援。 和 Visual Studio 2012，像是 NuGet 套件管理員擴充功能隨附於每個版本的 Visual Studio。

為了提供最佳的可能支援 Visual Studio 2013，同時仍然支援 Visual Studio 2010 和 Visual Studio 2012，並保持越小越好的延伸大小，我們會產生個別的擴充功能時的 Visual Studio 2013原始副檔名會繼續以 Visual Studio 2010 和 2012年為目標。

從 NuGet 2.6 開始，我們將發佈兩個擴充功能，如下所示：

1. [NuGet 套件管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)（適用於 Visual Studio 2010 和 2012年）
1. [Visual Studio 2013 的 NuGet 封裝管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

此分割中， [nuget.org](https://nuget.org)首頁的 「 安裝 NuGet"按鈕會帶您前往[安裝 NuGet](../install-nuget-client-tools.md)頁面上，您可以在何處安裝不同的 NuGet 用戶端的相關資訊。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 轉換的支援

其中一個最高要求 NuGet 用戶端功能已支援使用 XDT 轉換引擎用於 Visual Studio 建置組態轉換功能更強大的 XML 轉換。

在 2013 年 4 月中，我們所做的有關 XDT NuGet 支援兩個大公告。 第一個已 XDT 程式庫本身已被本身[以 NuGet 套件形式發行](https://nuget.org/packages/Microsoft.Web.Xdt)和[開啟來源 CodePlex 上](http://xdt.codeplex.com/)。 此步驟中啟用 XDT 引擎，可供自由其他開放原始碼軟體，包括 NuGet 用戶端。 第二個宣告已計劃來支援 XDT 引擎使用 NuGet 用戶端中的轉換。 NuGet 2.6 包含這項整合。

#### <a name="how-it-works"></a>它的運作方式

若要充分利用 NuGet 的 XDT 支援，機制尋找類似的[目前組態轉換功能](../create-packages/source-and-config-file-transformations.md)。
轉換檔案會新增至套件的內容資料夾。 不過，設定轉換會使用單一檔案的安裝和解除安裝，而 XDT 轉換可讓更細微的控制這兩個這些處理程序使用下列檔案：

- Web.config.install.xdt
- Web.config.uninstall.xdt

此外，NuGet 會使用檔案後置字元來判斷哪些引擎來執行轉換，以便使用現有 web.config.transforms 封裝將會繼續運作。 XDT 可以也將轉換套用至任何 XML 檔案 (不只是 web.config)，因此您可以利用這其他應用程式專案中。

#### <a name="what-you-can-do-with-xdt"></a>您可以使用達成 XDT

XDT 的最大優點的其中一個是其[簡單但強大的語法](http://msdn.microsoft.com/library/dd465326.aspx)管理結構的 XML dom。 XDT 會提供用於比對中以各種方式，從簡單的屬性名稱比對的完整 XPath 支援的項目控制項而不是只覆疊拖曳至另一個結構的一個固定格式文件結構。 一旦找到相符的項目或項目集，XDT 提供一組豐富的函式操作項目，而不論其所指新增、 更新或移除屬性，將新的項目放在特定位置，或取代或移除整個元素和其子系。

### <a name="machine-wide-configuration"></a>整部機器組態

NuGet 的優點是它細分否則大型可執行檔或程式庫至一組可整合，以及最重要的是維護和版本建立個別的模組化元件。 不過，它的一個副作用，會是產品或產品系列的傳統的做法可能會變得愈來愈分散。
NuGet 的自訂封裝來源功能提供一個方式來組織封裝，不過，自訂封裝來源不是可自行探索。

NuGet 2.6 延伸設定 NuGet 搜尋路徑 %programdata%/nuget/config 下的資料夾階層的邏輯。產品安裝程式可以將此登錄其產品的自訂封裝來源 資料夾下的自訂 NuGet 組態檔案。 此外，資料夾結構支援語意的產品、 版本和 IDE 的甚至 SKU。 依下列順序使用的 「 上一次在 wins"優先順序策略會套用這些目錄中的設定。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

在此清單中，以便在 Visual Studio 中，它將會是"VisualStudio"，為特定 NuGet 執行中，在 IDE {IDE} 預留位置。 {版本} 和 {SKU} 預留位置 （例如提供 IDE"11.0"和"WDExpress"、"VWDExpress 」 和 「 Pro"，分別)。 資料夾可以再包含許多不同的 *.config 檔案。
因此，ACME 元件公司可以其產品安裝程式的過程中，加入自訂的套件來源將會是檢視只能在 Visual Studio 2012 Professional 和 Ultimate 版本中建立下列檔案路徑：

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

NuGet 組態對話方塊時的資料夾結構可讓您可以直接軟體安裝程式，將整個電腦的封裝來源新增至 NuGet 的設定類似的程式，也允許做為封裝來源註冊更新其中一個特定使用者 （例如註冊 %appdata%/nuget/nuget.config 中） 或整部機器。

Visual Studio 2013 中，檔案會安裝在使用這項功能：

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

在這個檔案中，新的封裝來源，稱為 「.NET Framework 套件 」 設定。

![NuGet 組態檔的電腦的各種設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing 搜尋

由在 NuGet gallery 的封裝數目仍指數的速度成長，改善搜尋會保持為曾經 NuGet 優先順序清單的頂端。 NuGet 的計劃功能之一是搜尋的專案的內容中搜尋，這表示 NuGet 將使用做為準則的版本與 SKU 的 Visual Studio 所使用，以及您要建置類型的相關資訊來判斷可能相關性結果。

從 NuGet 2.6 開始，已安裝封裝，每次安裝內容會記錄為安裝操作資料的一部分。  搜尋也會傳送相同的內容資訊，可在 NuGet Gallery，提高內容安裝趨勢的搜尋結果。  在 NuGet Gallery 的未來更新會啟用此內容相關的相關性提高。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>追蹤直接安裝 vs。相依性安裝

封裝的作者越來越多依賴在[封裝統計資料](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)在 NuGet Gallery 上提供。  其中一個重要的遺漏資料點作者需要的是直接的封裝會安裝與相依性安裝之間的差異。  到目前為止，NuGet 用戶端未傳送任何內容周圍是否開發人員直接安裝封裝，或如果在安裝滿足相依性的安裝作業。
從 NuGet 2.6，現在會將資料傳送為安裝操作。  封裝在 NuGet Gallery 上的統計資料會公開做為個別的安裝作業，該資料與 「-相依性"後置詞。

* 安裝
* Install-Dependency
* 更新
* Update-Dependency
* 重新安裝
* Reinstall-Dependency

除了不同的作業名稱，也會針對安裝記錄相依的套件識別碼。  在 NuGet Gallery 的未來更新將會公開在報表中，可讓封裝作者以充分了解如何開發人員要安裝其封裝資料。

## <a name="bug-fixes"></a>Bug 修正

NuGet 2.6 也包含數個 bug 修正。 如需完整的工作清單項目固定在 NuGet 2.6，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。