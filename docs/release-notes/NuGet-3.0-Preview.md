---
title: NuGet 3.0 Preview 版本資訊
description: NuGet 3.0 Preview 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780331"
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 Preview 版本資訊

[NuGet 2.9 RC 版本](../release-notes/nuget-2.9-rc.md)  |  資訊[NuGet 3.0 Beta 版注意事項](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 Preview 已于2014年11月12日發行，作為 Visual Studio 2015 Preview 版本的一部分。 我們已發行 NuGet 3.0 預覽版。 這是我們 (的大型版本，雖然預覽) ，但我們很高興能開始取得有關變更的意見反應。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

此 NuGet 3.0 預覽版包含在 Visual Studio 2015 Preview 中。 我們即將致力於取得 Visual Studio 2012 的預覽，並 Visual Studio 2013。 我們先前已分享我們的意圖，以 [停止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，而我們的確進行了這種困難的決策。

## <a name="brand-new-ui"></a>全新的 UI

您注意到 NuGet 3.0 Preview 的第一件事，就是全新的 UI。 它不再是強制回應對話方塊;現在是完整的 Visual Studio 文件視窗。 如此一來，您就可以開啟多個專案的 UI， (和/或方案) 一次，將視窗移到另一個監視器，並在您想要的情況下停駐）等等。

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

除了可用性差異，由於放棄強制回應對話方塊，我們也在新的 UI 中有許多新功能。

### <a name="version-selection"></a>版本選取專案

可能是最常要求的 UI 功能，是允許套件安裝和更新的版本選項--這現在已可供使用。

![套件版本選取專案](./media/NuGet-3.0-Preview/version-selection.png)

無論您是安裝或更新套件，[版本] 下拉式清單都可讓您查看套件可用的所有版本，而且有一些值得注意的版本會升級至清單頂端，以便方便選取。 您不再需要使用 PowerShell 主控台來取得不是最新版本的特定版本。

### <a name="combined-installedonlineupdates-workflows"></a>合併安裝/線上/更新工作流程

先前的 UI 有3個已安裝、線上和更新的索引標籤。 列出的套件是這些工作流程專屬的，而且可用的動作也是針對工作流程所特有。 雖然這似乎是合理的，但我們聽說過許多人通常會在這種情況下出現。

我們現在有結合的體驗，您可以在其中安裝、更新或卸載套件，而不論您如何選取套件。 為了協助特定的工作流程，我們現在有一個篩選下拉式清單，可讓您篩選出可以看見的封裝，但可供封裝使用的動作是一致的。

![卸載套件](./media/NuGet-3.0-Preview/uninstall-package.png)

藉由使用「已安裝」篩選器，您就可以輕鬆地查看已安裝的套件、哪些套件有可用的更新，然後您可以藉由變更版本選取專案來卸載或更新套件，以查看變更可用的動作。

![更新套件](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>版本匯總

通常會將相同的套件安裝至方案內的多個專案。 有時候，安裝在每個專案中的版本可能會脫離，而且必須合併使用中的版本。 NuGet 3.0 Preview 為此案例引進了一項新功能。

在解決方案上按一下滑鼠右鍵，然後選擇 [管理方案的 NuGet 套件]，即可存取 [方案層級封裝管理] 視窗。 從該處，如果您選取的封裝已安裝至多個專案，但使用不同的版本，則會出現新的「合併」動作。 在下方的螢幕擷取畫面中， `Newtonsoft.Json` 已安裝至 `SamplesClassLibrary` with 版本， `6.0.4` 並已安裝至 `SamplesConsoleApp` with version `5.0.4` 。

![合併版本](./media/NuGet-3.0-Preview/consolidate.png)

以下是合併到單一版本的工作流程。

1. 選取 `Newtonsoft.Json` 清單中的套件
1. `Consolidate`從 `Action` 下拉式清單中選擇
1. 使用 `Version` 下拉式清單來選取要合併的版本
1. 核取要合併到該版本之專案的方塊 (請注意，已在所選版本上的專案會呈現灰色) 
1. 按一下 `Consolidate` 按鈕以執行匯總

### <a name="operation-previews"></a>作業預覽

無論您正在執行哪一項作業（安裝/更新/卸載），新的 UI 現在都提供一種方式來預覽您的專案所做的變更。 此預覽會顯示將安裝的任何新封裝、將更新的套件，以及將卸載的封裝，以及作業期間不會變更的套件。

在下列範例中，我們可以看到安裝 SignalR 會導致對專案進行相當多的變更。

![預覽安裝 SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>安裝選項

使用 PowerShell 主控台，您可以控制幾個值得注意的安裝選項。 我們現在也將這些功能帶入 UI 中。 您現在可以控制如何選取相依性版本的相依性解析行為。

![相依性行為](./media/NuGet-3.0-Preview/dependency-behavior.png)

您也可以指定當套件中的內容檔案與已經在專案中的檔案衝突時，所要採取的動作。

![檔案衝突動作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>無限期滾動

我們在列出套件時，會在 UI 上取得具有滾動和分頁範例的大量意見反應。 很常見的情況是，您必須在簡短清單的底部按一下下一個頁碼，然後再次滾動。 在新的 UI 中，我們已在套件清單中執行無限期的滾動，因此您只需要滾動，就不需要再進行分頁。

![無限期滾動](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>使其正常運作，使其變得更快速，讓它變得很美觀

我們很高興能讓您試用這個新的 UI。在此預覽里程碑中，我們已遵循良好的舊」古訓「讓它正常運作，讓它變得相當快速」。 在此預覽中，我們已完成大部分的第一個目標，也就是可行的。 我們知道它的速度不夠快，而我們也知道它還不太棒。 相信我們將在現在和 RC 版本之間處理這些目標。 在此同時，我們很樂意聽到您對於新 UI *可用性* 的意見反應 *，也就* 是工作流程、作業，以及使用新 ui 的方式。

相較于舊的 UI，我們已移除一些函數。 其中一個是故意的，而另一個則不是在時間內完成。

#### <a name="searching-all-package-sources"></a>搜尋「所有」套件來源

舊的 UI 可讓您針對所有套件來源執行封裝搜尋。 我們已在 UI 中移除該功能，而不會將它重新開機。 這項功能是用來對您的所有套件來源執行搜尋作業、將結果結合在一起，然後根據您的排序選取專案嘗試排序結果。

我們發現搜尋相關性真的很難在一起。 您是否可以想像針對 Google 和 Bing 執行搜尋，並將結果統稱在一起？ 此外，這項功能的速度很慢、很容易不 *小心* 使用，而且我們認為這項功能很少會很有用。 由於這項功能所帶來的問題，我們收到了一些可能未曾修正的 bug 報告。

#### <a name="update-all"></a>全部更新

在舊的 UI 中，我們已使用新的 UI 中的 [全部更新] 按鈕。 我們會針對 RC 版本 resurrect 這項功能。

## <a name="new-clientserver-api"></a>新用戶端/伺服器 API

除了新套件管理 UI 中的所有新功能之外，我們也已經處理 NuGet 用戶端/伺服器通訊協定的一些執行詳細資料。 我們所做的工作是建立 NuGet 的「API v3」，這是針對重大案例（例如套件還原和安裝封裝）的高可用性而設計的。 新的 API 是以 REST 和超媒體為基礎，而且我們選取了 [JSON-LD](http://json-ld.org) 作為資源格式。

在 NuGet 3.0 預覽版本中，您會在 [套件來源] 下拉式清單中看到名為 "preview.nuget.org" 的新套件來源。 如果您選取該套件來源，我們將使用新的 API，而不是連接到 nuget.org。我們已將預覽來源提供給 UI，同時繼續測試、修改和改進新的 API。 在 NuGet 3.0 RC 中，這個新的 API v3 套件來源會取代 v2 型的 "nuget.org" 套件來源。

儘管我們將投入 API v3 的投資，我們也讓所有這些新功能都能與現有的 API v2 通訊協定搭配使用，這表示它們也會使用 nuget.org 以外的現有套件來源。

## <a name="new-features-coming"></a>即將推出新功能

除了您在 UI 中看到的內容之外，我們也會在現在和 3.0 RTM 之間處理一些基本的新 NuGet 功能。 以下是顯著的投資領域的簡短清單：

1. 我們與 Visual Studio 和 MSBuild 小組合作，讓 [NuGet 更深入地進入平臺](http://blog.nuget.org/20141014/in-the-platform.html)。
1. 我們正致力於放棄安裝階段套件慣例，並藉由引進新的「權威」 [套件資訊清單](http://blog.nuget.org/20141023/package-manifests.html)，在封裝時期套用這些慣例。
1. 我們致力於重構 NuGet 程式碼基底，讓用戶端和伺服器元件可在 Visual Studio 的套件管理之外的不同網域中重複使用。
1. 我們正在調查「私用相依性」的概念，其中套件可能會指出它相依于其他封裝的相依性，僅供執行詳細資料，而這些相依性不應該呈現為最上層的相依性。

## <a name="stay-tuned"></a>持續關注

請留意 [我們的 blog](http://blog.nuget.org) ，以取得更多 NuGet 3.0 的進度和公告！