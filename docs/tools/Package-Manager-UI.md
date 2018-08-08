---
title: NuGet 封裝管理員 UI 參考
description: 使用 NuGet 封裝，使用 Visual Studio 中的 NuGet 封裝管理員 UI 的指示。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 307416908aff5db12fbf6f419e20acc6e0a9b241
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818837"
---
# <a name="nuget-package-manager-ui"></a>NuGet 封裝管理員 UI

在 Windows 上的 Visual Studio 中的 NuGet 封裝管理員 UI 可讓您輕鬆地安裝、 解除安裝，及更新在專案和方案的 NuGet 套件。 Visual Studio 中適用於 Mac 的經驗，請參閱[您的專案中包括的 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。 「 封裝管理員 」 UI 未隨附於 Visual Studio 程式碼。

本主題內容：

- [尋找和安裝封裝 （瀏覽 索引標籤）](#finding-and-installing-a-package)
- [解除安裝封裝 （已安裝 索引標籤）](#uninstalling-a-package)
- [更新封裝 （已安裝與更新索引標籤）](#updating-a-package) (包括["隱含參考 sdk"或"AutoReferenced 」 訊息](#implicit_reference))
- [管理解決方案套件](#managing-packages-for-the-solution)（在同一時間方式處理多個專案）。
- [封裝來源](#package-sources)
- [封裝管理員選項 控制項](#package-manager-options-control)

> [!Note]
> 如果您遺漏的 NuGet 封裝管理員 Visual Studio 2015 中，檢查**工具 > 擴充功能和更新...** 並搜尋*NuGet 套件管理員*延伸模組。 如果您無法使用 Visual Studio 中的擴充功能安裝程式，下載擴充功能直接從[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。
>
> 在 Visual Studio 2017，NuGet 和 NuGet 套件管理員自動安裝任何。網路相關的工作負載。 選取個別安裝**個別元件 > 程式碼工具 > NuGet 套件管理員**選項在 Visual Studio 2017 安裝程式。

## <a name="finding-and-installing-a-package"></a>尋找和安裝封裝

1. 在**方案總管] 中**，以滑鼠右鍵按一下 [**參考**或專案，然後選取**管理 NuGet 封裝...**.

    ![管理 NuGet 封裝 功能表選項](media/ManagePackagesUICommand.png)

1. **瀏覽**索引標籤會顯示受歡迎情況看出從目前選取的來源封裝 (請參閱[封裝來源](#package-sources))。 搜尋特定的封裝，使用在左上方的 [搜尋] 方塊。 封裝從清單選取以顯示其資訊，也可讓**安裝**版本選取項目下拉式清單以及按鈕。

    ![管理 NuGet 套件對話方塊瀏覽 索引標籤](media/Search.png)

1. 從下拉式清單選取所需的版本，然後選取**安裝**。 Visual Studio 會將封裝和其相依性安裝到專案。 系統可能會要求您接受授權條款。 已加入的套件安裝完成時，出現在**已安裝** 索引標籤。封裝也會列在**參考**節點的 方案總管 中，表示您可以在專案中有參考它們`using`陳述式。

    ![在 [方案總管] 的參考](media/References.png)

> [!Tip]
> 若要在搜尋中，包含發行前版本，而且建立發行前版本版本中提供下拉式清單，請選取**包含發行前版本**選項。

## <a name="uninstalling-a-package"></a>解除安裝封裝

1. 在**方案總管] 中**，以滑鼠右鍵按一下 [**參考**或所需的專案，然後選取**管理 NuGet 封裝...**.
1. 選取**已安裝** 索引標籤。
1. 選取要解除安裝 （使用搜尋來篩選清單，如有必要） 的套件，然後選取**解除安裝**。

    ![解除安裝封裝](media/UninstallPackage.png)

1. 請注意，**包含發行前版本**和**套件來源**解除安裝封裝時，控制項沒有任何作用。

## <a name="updating-a-package"></a>更新封裝

1. 在**方案總管] 中**，以滑鼠右鍵按一下 [**參考**或所需的專案，然後選取**管理 NuGet 封裝...**.(在網站專案中，以滑鼠右鍵按一下**Bin**資料夾。)
1. 選取**更新**索引標籤，查看所選取的封裝來源中有可用的更新。 選取**包含發行前版本**要在更新清單中包含套件發行前版本。
1. 選取要更新，在右側下拉式清單中選取所需的版本，並選取封裝**更新**。

    ![更新封裝](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>針對某些封裝，**更新**按鈕會停用，而且會出現訊息指出，它 「 隱含由參考 SDK"（或 「 AutoReferenced"）。 訊息會指出封裝，例如 Microsoft.NETCore.App 或 Microsoft.NETStandard.Library，是較大的架構或 SDK 的一部分，而且不應該獨立更新。 (這類封裝會在內部標示`<IsImplicitlyDefined>True</IsImplicitlyDefined>`。)若要更新封裝，更新的 SDK 所屬，推斷包含 SDK 來源封裝名稱。 例如，像 Microsoft.NETCore.App 封裝是.NET Core SDK 的一部分，因此您需要將.NET Core SDK 安裝更新。

    ![範例封裝標示為隱含參考或 AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. 若要為其最新版本更新多個封裝，選取這些清單並選取**更新**清單上方的按鈕。
1. 您也可以更新從個別封裝**已安裝** 索引標籤。在此情況下，封裝的詳細資料包含版本選取器 (受**包含發行前版本**選項) 和**更新** 按鈕。

## <a name="managing-packages-for-the-solution"></a>管理方案套件

管理方案套件是方便的方法，來同時使用多個專案。

1. 選取**工具 > NuGet 套件管理員 > 管理方案的 NuGet 封裝...** 功能表命令時，或以滑鼠右鍵按一下方案並選取**管理 NuGet 封裝...**:

    ![管理方案的 NuGet 封裝](media/ManagePackagesSolutionUICommand.png)

1. 當管理解決方案的封裝時，UI 可讓您選取受作業影響的專案：

    ![管理方案的封裝時的專案選取器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>彙總索引標籤

開發人員通常人認為非常不建議您在相同方案中的不同專案中使用不同版本的相同的 NuGet 封裝。 當您選擇管理解決方案的封裝時，封裝管理員 UI 提供**合併彙算**所在您很容易其中封裝名稱中有不同的版本號碼由不同專案方案中的索引標籤：

![封裝管理員 UI 合併索引標籤](media/ConsolidateTab.png)

在此範例中，而 ConsoleApp1 使用 EntityFramework 6.1.0 ClassLibrary1 專案時，使用 EntityFramework 6.2.0。 彙總套件版本，執行下列作業：

- 選取要更新專案清單中的專案。
- 選取要使用所有這些專案中的版本**版本**控制權，例如 EntityFramework 6.2.0。
- 選取**安裝** 按鈕。

封裝管理員安裝到所有選取的專案，在其後封裝不會再出現在選取的封裝版本**合併彙算** 索引標籤。

## <a name="package-sources"></a>封裝來源

若要變更 Visual Studio 將會從中取得封裝的來源，請選取從來源選取器的其中一個：

![封裝管理員 UI 中的 封裝來源選取器](media/PackageSourceDropDown.png)

若要管理的封裝來源：

1. 選取**設定**封裝管理員 UI 中的圖示如下所述，或使用**工具 > 選項**命令，然後捲動至**NuGet 套件管理員**:

    ![封裝管理員 UI 設定圖示](media/PackageSourceSettings.png)

1. 選取**封裝來源**節點：

    ![封裝來源選項](media/options.png)

1. 若要新增為來源，請選取 **+** 、 編輯名稱、 輸入的路徑或 URL **來源** 控制項，然後選取 **更新** 。 來源現在會出現在選取器下拉式清單中。
1. 若要變更的封裝來源，請選取它，進行中的編輯**名稱**和**來源**方塊，然後選取**更新**。
1. 若要停用封裝來源，請清除方塊左邊的清單中的名稱。
1. 若要移除的封裝來源，加以選取，然後選取**X**  按鈕。
1. 使用向上和向下箭號按鈕以變更的封裝來源的優先順序。 還原專案的封裝時，visual Studio 會搜尋這些來源中的優先順序。 如需詳細資訊，請參閱[封裝還原](../consume-packages/package-restore.md)。

> [!Tip]
> 如果套件來源再次出現之後刪除它，它可能會列在電腦層級或使用者層級`NuGet.Config`檔案。 請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)針對這些檔案的位置，然後移除來源以手動方式編輯檔案，或使用[nuget 來源命令](../tools/nuget-exe-CLI-reference.md)。

## <a name="package-manager-options-control"></a>封裝管理員選項 控制項

選取封裝時，「 封裝管理員 」 UI 會顯示小，可展開**選項**下方 （如下所示同時摺疊和展開） 版本選擇器控制項。 請注意，某些專案類型，才**顯示預覽視窗**提供選項。

![封裝管理員選項](media/PackageManagerUIOptions.png)

下列各節說明這些選項。

### <a name="show-preview-window"></a>顯示預覽視窗

選取時，強制回應視窗會顯示其中所選封裝的相依性套件之前，先：

![範例預覽對話方塊](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>安裝及更新選項

（不適用的所有專案類型）。

**相依性行為**設定 NuGet 如何決定要安裝的相依套件版本：

- *忽略的相依性*略過安裝任何相依性，這通常會中斷所安裝的套件。
- *最低*[Default] 安裝相依性以符合需求的主要的所選套件的最小的版本號碼。
- *最高的修補程式*安裝的版本具有相同主要和次要版本號碼，而最高的修補程式數目。 比方說，如果已指定版本 1.2.2 然後開頭 1.2 最高的版本將會安裝
- *最高次要*安裝的版本具有相同主要版本號碼，但最高次要號碼和修補程式數目。 如果指定 1.2.2 版本，然後以 1 為開頭的最高版本將會安裝
- *最高*安裝封裝的最新可用版本。

**檔案衝突 動作**指定 NuGet 應該如何處理已經存在於專案或本機電腦的封裝：

- *提示*指示 NuGet 詢問是否要保留或覆寫現有的封裝。
- *忽略以上所有*指示 NuGet 略過覆寫任何現有的封裝。
- *覆寫所有*指示 NuGet 覆寫任何現有的封裝。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>解除安裝選項

（不適用的所有專案類型）。

**移除依存性**： 選取時，移除任何相依的套件如果它們未參考其他地方專案中。

**強制解除安裝，即使相依於它也是**： 選取時，會解除安裝封裝即使仍在專案中參考。 這通常用於搭配**移除相依性**移除封裝和任何相依性安裝它。 使用此選項可能，不過，會導致中斷的參考專案中。 在這種情況下，您可能需要[重新安裝這些其他封裝](../consume-packages/reinstalling-and-updating-packages.md)。
