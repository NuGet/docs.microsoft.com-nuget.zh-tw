---
title: NuGet 3.0 版的 Preview 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.0 Preview 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546461"
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 版的 Preview 版本資訊

[NuGet 2.9 RC 版本資訊](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta 版本資訊](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 Preview 於 2014 年 11 月 12 日 Visual Studio 2015 Preview 版本發行。 我們發行了 NuGet 3.0 預覽。 這是大型的發表，我們 （雖然預覽中），和我們很高興能夠開始取得意見反應，我們變更。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

這個 NuGet 3.0 預覽包含在 Visual Studio 2015 Preview 中。 我們正努力取得預覽卸除 Visual Studio 2012 和 Visual Studio 2013 推出。 我們之前告訴大家我們試圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，但未將該相當困難的決定。

## <a name="brand-new-ui"></a>全新的 UI

您會注意到關於 NuGet 3.0 預覽第一件事是我們全新的 UI。 它不再是強制回應對話方塊;它現在是完整的 Visual Studio 文件視窗。 這可讓您一次開啟多個專案 （和/或解決方案） 的 UI、 的視窗切割到另一個監視器、 將它停駐，不過，您會願意等等。

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

超過使用性的差異，因為放棄強制回應對話方塊，我們也有許多新功能在新的 UI 中。

### <a name="version-selection"></a>版本選取項目

最可能是要求 UI 功能可讓版本選取項目套件安裝和更新，這是立即可用。

![套件版本選取項目](./media/NuGet-3.0-Preview/version-selection.png)

是否要安裝或更新套件，[版本] 下拉式清單可讓您查看所有具有某些值得注意的版本升級為簡單的選取清單的頂端提供套件的版本。 您不再需要使用 PowerShell 主控台，以取得不是最新的特定版本。

### <a name="combined-installedonlineupdates-workflows"></a>合併的安裝/連線/更新工作流程

我們先前的 UI 有上線，已安裝和更新的 3 個索引標籤。 列出的套件所特有的工作流程和可用的動作所特有的工作流程。 雖然看似合理的我們聽到許多您通常會取得挫敗由這種區隔。

我們現在有合併的體驗，您可以用它來安裝、 更新，或解除安裝的封裝，不論您如何取得選取的封裝。 為了協助特定的工作流程，我們現在可以篩選下拉式清單，可讓您篩選可見，封裝，但適用於封裝的動作則一致。

![解除安裝套件](./media/NuGet-3.0-Preview/uninstall-package.png)

藉由使用 「 安裝 」 篩選條件，您就可以輕鬆地觀察哪些有可用的更新，您已安裝的封裝，然後您可以解除安裝或變更版本選取項目，以查看更新的封裝變更可用的動作。

![更新的套件](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>版本彙總

通常會有相同的套件安裝到您的方案中的多個專案。 有時安裝到每個專案的版本可以相隔漂移，就必須彙總中使用的版本。 NuGet 3.0 Preview 引進了新的功能，只要在此案例。

方案層級套件的 管理 視窗可以存取方案上按一下滑鼠右鍵，然後選擇 管理方案的 NuGet 套件。 在這裡，如果您選取 封裝安裝到多個專案，但使用不同的版本，在使用中，新的 「 合併 」 動作會變成可用。 在下列螢幕擷取畫面，`Newtonsoft.Json`已安裝到`SamplesClassLibrary`版`6.0.4`，並已安裝到`SamplesConsoleApp`版本`5.0.4`。

![彙總版本](./media/NuGet-3.0-Preview/consolidate.png)

以下是合併到單一版本的工作流程。

1. 選取`Newtonsoft.Json`清單中的封裝
1. 選擇`Consolidate`從`Action`下拉式清單中
1. 使用`Version`下拉式清單，選取要合併到的版本
1. 核取方塊的專案，應該會合併到該版本 （請注意，已在選取的版本上的專案會呈現灰色）
1. 按一下 `Consolidate`按鈕以執行彙總

### <a name="operation-previews"></a>作業預覽

不論您執行-哪一個作業安裝/更新/解除安裝-新的 UI 現在提供一種方式預覽變更，將對您的專案。 此預覽會顯示任何新的套件，將安裝套件，將會更新，並將它封裝，將會解除安裝，以及將會在作業期間維持不變的封裝。

在下列範例中，我們可以看到，安裝 Microsoft.AspNet.SignalR 會導致相當多的變更至專案。

![安裝 SignalR 的預覽](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>安裝選項

使用 PowerShell 主控台中，您有幾個值得注意的安裝選項的控制權。 我們現在已經納入 UI 也加入這些功能。 您現在可以控制如何選取版本的相依性的相依性解析行為。

![相依性的行為](./media/NuGet-3.0-Preview/dependency-behavior.png)

您也可以指定要從封裝的內容檔案發生衝突的檔案已在您的專案時所採取的動作。

![Akce při Konfliktu Souborů](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>無限捲動

我們用來取得相當的意見反應，我們的 ui 讓這兩個捲動和列出封裝時，分頁典範。 它是很常見的捲動到底部的簡短清單，按一下 [下一步] 的頁面數目，然後再次捲動。 有新的 UI 中，我們已實作無限捲動套件清單中，您只需要捲動，沒有更多的分頁。

![無限捲動](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>使其工作、 快速，讓它很

我們很興奮地一定要記得這個新的 UI 讓您試用。在此預覽的里程碑，我們已經遵循的良好的古訓 「 保持運作、 進行快速、 加強美化。 」 在此預覽中，我們已經完成大部分的第一個目標，它的運作方式。 我們知道它尚未相當快速，我們知道它尚未相當相當。 我們將努力於這些目標現在與 RC 版本之間的信任。 在此同時，我們很希望聽聽您的意見反應的相關*可用性*的新 UI--工作流程、 作業，以及它*感覺*若要使用新的 UI。

有幾個相較於舊版的 UI，我們已移除的函式。 其中一種是特意的與另一個只是未完成的時間。

#### <a name="searching-all-package-sources"></a>搜尋 「 全部 」 的套件來源

舊版 UI 可讓您執行封裝的搜尋，針對所有套件來源。 我們已移除該功能在 UI 中，我們將不會被帶回來。 用來執行搜尋作業，針對所有套件來源，這項功能會組織在一起，結果，並嘗試排列取決於您選擇的排序結果。

我們發現搜尋相關性是很難組織在一起。 您可以想像執行對 Google、 Bing 搜尋，並一起編排結果嗎？ 此外，這項功能已變慢、 容易*意外*以及我們認為很少是真的很實用。 因為發生問題的功能導入，我們收到數目可能永遠不會有已修正的 bug 報告在其上。

#### <a name="update-all"></a>全部更新

我們用來在尚未有新的 UI 中將舊版 UI 的 [全部更新] 按鈕。 我們將會重新啟動這項功能，我們的 RC 版本。

## <a name="new-clientserver-api"></a>新用戶端/伺服器 API

除了我們新的套件管理 UI 中的新功能，我們也一直在處理某些 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。 我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。 新的 API 以 REST 為基礎，並已選取超媒體和我們[JSON-LD](http://json-ld.org)為我們資源的格式。

在 NuGet 3.0 Preview 位元為單位，您會看到新的封裝來源的封裝來源下拉式清單中稱為 「 preview.nuget.org"。 如果您選取該套件來源，我們將使用我們的新 API，而是要連接到 nuget.org。我們已進行預覽來源可在 UI 中，同時會持續測試、 修訂和提高新的 API。 在 NuGet 3.0 RC 中，這個新的 API v3 套件來源將會取代 v2 為基礎的"nuget.org"套件來源。

儘管我們正在將放入 API v3 的投資，我們已進行所有這些新功能也適用於我們現有 API v2 通訊協定，這表示它們會使用現有的套件來源，以及 nuget.org 以外。

## <a name="new-features-coming"></a>即將推出的新功能

現在開始到 3.0 的 RTM，我們也正在一些基本以外的新 NuGet 功能，在 UI 中看到的內容。 以下是一份主要投資領域：

1. 我們合作，使用 Visual Studio 和 MSBuild 小組以取得[平台更深層的 NuGet](http://blog.nuget.org/20141014/in-the-platform.html)。
1. 我們正在放棄安裝階段套件慣例，並改為在藉由引進新的封裝時套用這些慣例 「 授權 」[封裝資訊清單](http://blog.nuget.org/20141023/package-manifests.html)。
1. 我們正在努力的重構 NuGet 程式碼基底進行 Visual Studio 中的套件管理之外的不同網域中的可重複使用的用戶端和伺服器元件。
1. 我們正積極研究概念的 「 私用相依性 」，封裝可能表示它具有相依於其他封裝的實作詳細資料，以及這些相依性不應該顯示為最上層相依性。

## <a name="stay-tuned"></a>敬請期待

請留意[我們的部落格](http://blog.nuget.org)如需詳細的進度和 NuGet 3.0 公告 ！