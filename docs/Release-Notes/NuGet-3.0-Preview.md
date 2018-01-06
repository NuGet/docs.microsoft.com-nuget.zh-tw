---
title: "NuGet 3.0 Preview 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6762b6f8-82b7-4bab-a1f0-cd25e5dc1fb4
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.0 預覽的版本資訊。"
keywords: "NuGet 3.0 預覽的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ae137af6f9722c454458fdcb4f20760c08d6e8bb
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 的預覽版本資訊

[NuGet 2.9 RC 版本資訊](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta 版本資訊](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 預覽版本已發行於 2014 年 11 月 12 日在 Visual Studio 2015 Preview 版本。 我們發行了 NuGet 3.0 預覽。 這是我們大發行 （雖然預覽中），以及我們很高興能夠開始取得意見反應，我們變更。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

此 NuGet 3.0 預覽隨附於 Visual Studio 2015 Preview。 我們正努力預覽卸除的 Visual Studio 2012 和 Visual Studio 2013 很快。 我們先前共用我們意圖[中止更新適用於 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，我們沒有做出的決策，困難。

## <a name="brand-new-ui"></a>全新的 UI

您會發現有關 NuGet 3.0 預覽第一件事是我們新的 UI。 它不再是強制回應對話方塊。它現在是完整的 Visual Studio 文件視窗。 這可讓您在一次開啟多個專案 （和/或方案） 的使用者介面、 分離出來視窗至另一個監視器、 將它停駐，不過就像 like 等等。

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

超過使用性的差異，因為放棄強制回應對話方塊，我們也有許多新功能的新 UI 中。

### <a name="version-selection"></a>版本選取項目

最可能要求 UI 功能可讓版本選取項目套件安裝和更新-這是立即可用。

![套件版本選取項目](./media/NuGet-3.0-Preview/version-selection.png)

是否要安裝或更新的封裝，[版本] 下拉式清單可讓您查看所有可用的封裝，版本具有某些值得注意的版本升級為簡單的選取清單的頂端。 您不再需要使用來取得特定版本，不是最新的 PowerShell 主控台。

### <a name="combined-installedonlineupdates-workflows"></a>結合安裝/線上/更新工作流程

我們先前 UI 必須上線，已安裝和更新的 3 個索引標籤。 封裝列出特定的工作流程，而且可用的動作所特有的工作流程。 雖然看似邏輯，我們聽到許多您通常會取得這項分隔的錯誤。

我們現在有合併的體驗，您可以在其中安裝、 更新或解除安裝封裝，不論您如何到達所選取的封裝。 為了協助的特定工作流程，我們現在有篩選下拉式清單中，可讓您篩選封裝可見的但然後封裝可用動作一致。

![解除安裝封裝](./media/NuGet-3.0-Preview/uninstall-package.png)

藉由使用 「 安裝 」 篩選器，您可以輕鬆地看見有何者有可用的更新，您已安裝的封裝，並接著您可以解除安裝，或藉由變更版本選取項目，以查看更新的封裝變更可用的動作。

![更新的套件](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>版本彙總

通常會有相同的封裝安裝到您的方案中的多個專案。 有時候安裝到每個專案的版本可以分開漂移，則需要彙總中使用的版本。 NuGet 3.0 Preview 引進的新功能，只要在此案例。

方案層級封裝的 管理 視窗可以存取方案上按一下滑鼠右鍵，然後選擇 管理方案的 NuGet 套件。 從該處，如果您選取的封裝安裝到多個專案，但具有不同的版本，在使用中，新的 「 合併 」 動作會變成可用。 在下列螢幕擷取畫面，`Newtonsoft.Json`安裝`SamplesClassLibrary`版本`6.0.4`且已安裝到`SamplesConsoleApp`版本`5.0.4`。

![合併版本](./media/NuGet-3.0-Preview/consolidate.png)

以下是將合併到單一版本的工作流程。

1. 選取`Newtonsoft.Json`清單中的封裝
1. 選擇`Consolidate`從`Action`下拉式清單
1. 使用`Version`下拉式清單來選取要合併到的版本
1. 核取方塊，應合併到該版本 （請注意，已在選取的版本上的專案會呈現灰色） 的專案
1. 按一下`Consolidate`按鈕來執行彙總

### <a name="operation-previews"></a>作業預覽

不論哪一項作業在執行-安裝/更新/解除安裝-新的使用者介面現在提供一種方式預覽變更，將對您的專案。 這個預覽會顯示新的封裝將安裝的封裝將會更新，並將封裝將會解除安裝，以及將會在作業期間維持不變的封裝。

在下列範例中，我們可以看到，安裝 Microsoft.AspNet.SignalR 時會產生極多的變更至專案。

![安裝 SignalR 的預覽](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>安裝選項

使用 PowerShell 主控台，您有幾個值得注意的安裝選項的控制權。 現在我們已將這些功能帶入 UI。 您現在可以控制如何選取版本的相依性的相依性解析行為。

![相依性的行為](./media/NuGet-3.0-Preview/dependency-behavior.png)

您也可以指定要從套件內容檔案衝突的檔案已在您的專案時所採取的動作。

![檔案 [衝突] 動作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>無限捲動

我們用來取得稍微的意見反應，我們的 ui 讓這兩個捲動及列出封裝時，分頁開發架構。 它是非常普遍能夠捲動的簡短清單底部，按一下 下一步的頁面數字，然後再一次捲動。 使用新的 UI 中，我們已實作無限捲動封裝清單中，因此您只需要捲動-沒有更多的分頁。

![無限捲動](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>讓工作，使其快速，使其美觀

我們很高興能夠讓您試用努力這個新的 UI。在此預覽里程碑，我們都遵循的良好俗話說 「 保持運作、 進行快速、 加強美化。 」 在此預覽中，我們已經完成大部分的該第一個目標-它的運作方式。 我們知道它尚未相當快速，我們已經知道它尚未相當相當。 我們會努力這些目標的 RC 版本之間的信任。 在此同時，我們很希望聽聽您的意見反應的相關*可用性*的新 ui-工作流程、 作業，以及它*感覺*若要使用新的 UI。

有幾個函式，我們便移除了相較於舊的 UI。 下列其中一種有意，和另一個只未完成的時間。

#### <a name="searching-all-package-sources"></a>搜尋 「 全部 」 封裝來源

舊的 UI 可讓您執行封裝，針對您的封裝來源的所有搜尋。 我們已移除該功能，在 UI 中，我們將不會使其傳回。 這項功能，用來執行搜尋作業，針對您的封裝來源的所有組織在一起，，結果，並嘗試根據您排序選取結果。

我們發現搜尋相關性是很難組織在一起。 您可以想像執行針對 Google 和 Bing 搜尋，並一起 weaving 結果嗎？ 此外，這項功能已慢速又容易*意外*以及我們認為很少是實際的有用。 因為發生問題的功能導入，我們收到無法從未已獲得修正的 bug 報告在其上的數的字。

#### <a name="update-all"></a>更新所有

我們使用舊尚有無法在新的 UI 中的 UI 中有 [更新全部] 按鈕。 我們會重新啟動這項功能，我們的 RC 版本。

## <a name="new-clientserver-api"></a>新用戶端/伺服器應用程式開發介面

除了所有我們新的封裝管理 UI 中的新功能，我們已也已在處理某些 NuGet 的用戶端/伺服器通訊協定的實作詳細資料。 我們已完成的工作是建立 「 API v3"nuget，專為高可用性的重要案例，例如封裝還原和安裝封裝。 新的應用程式開發介面以 REST 為基礎和超，我們已選取[JSON LD](http://json-ld.org)為我們的資源格式。

在 NuGet 3.0 預覽位元為單位，您會看到稱為"preview.nuget.org"的套件來源下拉式清單中的新封裝來源。 如果您選取的套件來源，我們將使用新 API，而是要連接到 nuget.org。我們已可供預覽來源在 UI 中我們繼續測試、 修訂和改善的新 API。 在 NuGet 3.0 RC 中，這個新的 API v3 為基礎的套件來源將會取代 v2 為基礎的 」 nuget.org"的套件來源。

儘管我們正在將放入 API v3 的投資，我們已經讓我們現有 API v2 通訊協定，這表示將使用現有的封裝來源，以及 nuget.org 以外也使用所有這些新功能。

## <a name="new-features-coming"></a>推出的新功能

之間 3.0 RTM，我們也正在一些基本 NuGet 以外新功能，您會看到在 UI 中。 以下是主要的投資領域的簡短清單：

1. 我們正在合作與 Visual Studio 和 MSBuild 小組以取得[更深入的平台的 NuGet](http://blog.nuget.org/20141014/in-the-platform.html)。
1. 我們正努力放棄安裝階段封裝慣例，並改為在封裝階段套用這些慣例，藉由引進新的 「 系統授權 」[封裝資訊清單](http://blog.nuget.org/20141023/package-manifests.html)。
1. 我們正努力的重構 NuGet 程式碼在 Visual Studio 中的封裝管理以外的不同網域中進行用戶端和伺服器元件可重複使用基底。
1. 我們正在調查概念的 「 私用相依性 」 封裝可以在其中表示它具有的實作詳細資料，其他套件相依性和這些相依性不應該顯示為最上層的相依性。

## <a name="stay-tuned"></a>敬請期待

請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及針對 NuGet 3.0 公告 ！