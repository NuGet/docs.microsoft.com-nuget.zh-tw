---
title: NuGet 套件管理員 UI 參考
description: 使用 Visual Studio 中的 NuGet 套件管理員 UI，使用 NuGet 套件的指示。
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 1de6ddeca6295c621a90409807af198bc3c7a068
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981180"
---
# <a name="nuget-package-manager-ui"></a>NuGet 套件管理員 UI

在 Windows 上的 Visual Studio 中的 NuGet 套件管理員 UI 可讓您輕鬆地安裝、 解除安裝，並更新專案和方案中的 NuGet 套件。 在 Visual Studio for Mac 的體驗，請參閱 <<c0> [ 在專案中的包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。 找不到隨附於 Visual Studio Code 的套件管理員 UI。

本主題內容：

- [尋找及安裝套件 （瀏覽 索引標籤）](#finding-and-installing-a-package)
- [解除安裝套件 （已安裝 索引標籤）](#uninstalling-a-package)
- [更新套件 （已安裝和更新 索引標籤）](#updating-a-package) (包括[「 隱含參考的 sdk 」 或 「 自動 」 參考訊息](#implicit_reference))
- [管理解決方案套件](#managing-packages-for-the-solution)（在同一時間方式處理多個專案）。
- [套件來源](#package-sources)
- [套件管理員選項控制](#package-manager-options-control)

> [!Note]
> 如果您缺少的 NuGet 套件管理員，在 Visual Studio 2015，請檢查**工具 > 擴充功能和更新...** 並搜尋*NuGet 套件管理員*延伸模組。 如果您無法使用 Visual Studio 中的延伸模組安裝程式，請下載擴充功能直接從[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。
>
> 在 Visual Studio 2017，NuGet 和 NuGet 套件管理員會自動會與任何安裝。NET 相關的工作負載。 藉由選取個別安裝**個別元件 > 程式碼工具 > NuGet 套件管理員**Visual Studio 2017 安裝程式中的選項。

## <a name="finding-and-installing-a-package"></a>尋找和安裝封裝

1. 在 **方案總管**，以滑鼠右鍵按一下其中一個**參考**或專案，然後選取**管理 NuGet 套件...**.

    ![管理 NuGet 套件 功能表選項](media/ManagePackagesUICommand.png)

1. **瀏覽**索引標籤會顯示依熱門程度從目前所選來源的封裝 (請參閱[套件來源](#package-sources))。 搜尋特定的封裝，使用在左上方的搜尋方塊中。 選取封裝，從清單中，以顯示其資訊，也可讓**安裝**以及版本選取項目下拉式清單的按鈕。

    ![管理 NuGet 封裝對話方塊瀏覽 索引標籤](media/Search.png)

1. 從下拉式清單中選取所需的版本，然後選取**安裝**。 Visual Studio 會將封裝和其相依性安裝到專案。 系統可能會要求您接受授權條款。 新增的套件安裝完成時，出現在**已安裝** 索引標籤。套件也會列在**參考**節點的 方案總管 中，表示您可以在專案中有參考這些`using`陳述式。

    ![在 [方案總管] 中的參考](media/References.png)

> [!Tip]
> 若要在搜尋中，包含發行前版本，並發行前版本中提供版本下拉式清單，選取**包含發行前版本**選項。

## <a name="uninstalling-a-package"></a>解除安裝套件

1. 在 [**方案總管] 中**，以滑鼠右鍵按一下其中一個**參考**或所需的專案，然後選取**管理 NuGet 套件...**.
1. 選取 [**已安裝**] 索引標籤。
1. 選取要解除安裝 （使用搜尋來篩選清單，如有必要） 的封裝，然後選取**解除安裝**。

    ![解除安裝套件](media/UninstallPackage.png)

1. 請注意，**包括發行前版本**並**套件來源**解除安裝套件時，控制項沒有任何作用。

## <a name="updating-a-package"></a>更新套件

1. 在 [**方案總管] 中**，以滑鼠右鍵按一下其中一個**參考**或所需的專案，然後選取**管理 NuGet 套件...**.(在網站專案中，以滑鼠右鍵按一下**Bin**資料夾。)
1. 選取 [**更新**] 索引標籤，查看有可用的更新，從選取的封裝來源的封裝。 選取 **包含發行前版本**包含發行前版本的套件清單中的更新。
1. 選取要更新，從右邊的下拉式清單中選取所需的版本，並選取封裝**更新**。

    ![更新套件](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>某些封裝，如**更新**按鈕已停用，且會出現訊息指出，它會 「 隱含參考 SDK 」 （或 「 自動參考 」）。 此訊息表示封裝是較大的架構或 SDK 的一部分，而且不應獨立更新。 (這類套件會在內部標示與`<IsImplicitlyDefined>True</IsImplicitlyDefined>`。)比方說，`Microsoft.NETCore.App`屬於.NET Core SDK 和套件版本不相同的應用程式所使用的執行階段 framework 版本。 您需要[更新您的.NET Core 安裝](https://aka.ms/dotnet-download)來取得新版本的 ASP.NET Core 和.NET Core 執行階段。 [請參閱這份文件，如需詳細資訊，.NET Core 中繼套件和版本控制](/dotnet/core/packages)。 這適用於下列常用的套件：
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![範例封裝標示隱含參考或自動參考](media/PackageManagerUIAutoReferenced.png)

1. 若要更新為最新版本的多個封裝，選取清單中選取**更新**清單上方的按鈕。
1. 您也可以更新從個別封裝**已安裝** 索引標籤。在此情況下，封裝的詳細資料包含版本選擇器 (受**包括發行前版本**選項) 和**更新** 按鈕。

## <a name="managing-packages-for-the-solution"></a>管理解決方案套件

管理解決方案封裝是同時使用多個專案的便利方法。

1. 選取**工具 > NuGet 套件管理員 > 管理方案的 NuGet 套件...** 功能表命令，或以滑鼠右鍵按一下方案，然後選取**管理 NuGet 套件...**:

    ![管理解決方案的 NuGet 封裝](media/ManagePackagesSolutionUICommand.png)

1. 在管理解決方案的封裝時，UI 可讓您選取的專案，會受到作業：

    ![管理方案的套件時的專案選取器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>彙總索引標籤

開發人員通常認為不建議您在相同方案中的不同專案中使用相同的 NuGet 套件的不同版本。 當您選擇管理解決方案套件時，套件管理員 UI 提供**合併** 索引標籤您可以輕易看到方案中的不同專案，使用封裝名稱中有不同的版本號碼：

![套件管理員 UI 合併 索引標籤](media/ConsolidateTab.png)

在此範例中，而 ConsoleApp1 使用 EntityFramework 6.1.0 ClassLibrary1 專案時，會使用 EntityFramework 6.2.0。 若要彙總套件版本，執行下列作業：

- 選取 [專案] 清單中要更新的專案。
- 選取要使用所有這些專案中的版本**版本**控制項，例如 EntityFramework 6.2.0。
- 選取 [**安裝**] 按鈕。

封裝管理員會選取的封裝版本安裝到所有選取的專案之後，封裝不會再出現在**合併** 索引標籤。

## <a name="package-sources"></a>套件來源

若要變更 Visual Studio 將會從中取得封裝的來源，選取從來源選取器的其中一個：

![在 套件管理員 UI 中的封裝來源選取器](media/PackageSourceDropDown.png)

若要管理的套件來源：

1. 選取 **設定**套件管理員 UI 中的圖示如下所述，或使用**工具 > 選項**命令，然後捲動至**NuGet 套件管理員**:

    ![套件管理員 UI 設定圖示](media/PackageSourceSettings.png)

1. 選取 **套件來源**節點：

    ![封裝來源選項](media/options.png)

1. 若要新增為來源，請選取 **+** 、 編輯名稱、 輸入的路徑或 URL **來源** 控制項，然後選取 **更新** 。 來源現在會出現在選取器下拉式清單中。
1. 若要變更的套件來源，請選取它，進行中的編輯**名稱**並**來源**方塊中，然後選取**Update**。
1. 若要停用的套件來源，請清除方塊左邊的清單中的名稱。
1. 若要移除的套件來源，請選取它，然後按**X**  按鈕。
1. 使用向上和向下箭號按鈕以變更套件來源的優先順序。 還原專案的套件時，visual Studio 會搜尋這些來源中的優先順序。 如需詳細資訊，請參閱 <<c0> [ 套件還原](../consume-packages/package-restore.md)。

> [!Tip]
> 如果套件來源之後刪除它再次發生，表示它可能會列在電腦層級或使用者層級`NuGet.Config`檔案。 請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)這些檔案的位置，然後移除來源以手動方式編輯檔案，或使用[nuget 來源命令](../tools/nuget-exe-CLI-reference.md)。

## <a name="package-manager-options-control"></a>套件管理員選項控制

選取套件時，套件管理員 UI 會顯示一個小型的可展開**選項**下方 （如下所示同時摺疊和展開） 版本選擇器控制項。 請注意，某些專案類型，才**顯示預覽視窗**提供選項。

![套件管理員選項](media/PackageManagerUIOptions.png)

下列各節說明這些選項。

### <a name="show-preview-window"></a>顯示預覽視窗

選取時，強制回應視窗會顯示其所選套件的相依性之前安裝套件：

![範例預覽對話方塊](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Možnosti instalace a Aktualizace

（不適用所有專案類型）。

**相依性行為**設定 NuGet 如何決定要安裝的相依套件版本：

- *略過相依性*略過安裝任何相依性，這通常會中斷安裝封裝。
- *最低*[Default] 安裝相依性最低的版本號碼符合主要的所選套件的需求。
- *最高的修補程式*安裝的版本具有相同的主要和次要版本號碼，但最高的修補程式數目。 比方說，如果未指定版本 1.2.2 則開頭為 1.2 的最高版本將會安裝
- *最高次要*安裝的版本，使用相同的主要版本號碼，但最高次要號碼和修補程式數目。 如果指定 1.2.2 版，則會從 1 開始的最高版本將會安裝
- *最高*安裝封裝的最高可用版本。

**檔案衝突動作**指定 NuGet 應如何處理已經存在於專案或本機電腦的封裝：

- *提示*會指示 NuGet 詢問是否要保留或覆寫現有的封裝。
- *全部忽略*會指示 NuGet 略過覆寫任何現有的封裝。
- *覆寫所有*會指示 NuGet 覆寫任何現有的封裝。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>解除安裝選項

（不適用所有專案類型）。

**移除相依性**： 選取時，會移除任何相依的套件如果它們是在其他地方專案中未參考。

**強制解除安裝，即使它有相依性**： 選取時，解除安裝封裝即使仍在專案中參考。 這通常用於搭配**移除相依性**移除套件及任何相依性安裝它。 使用此選項可能，不過，會導致中斷的參考，專案中。 在此情況下，您可能需要[重新安裝這些其他套件](../consume-packages/reinstalling-and-updating-packages.md)。
