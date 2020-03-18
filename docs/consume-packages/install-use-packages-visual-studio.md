---
title: 在 Visual Studio 中安裝和管理 NuGet 套件
description: 使用 Visual Studio 中的 NuGet 套件管理員 UI 來處理 NuGet 套件的指示。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428692"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>在 Visual Studio 中，使用 NuGet 套件管理員來安裝和管理套件

Visual Studio 中的 NuGet 套件管理員 UI 可讓您在專案和解決方案中，輕鬆地安裝、解除安裝和更新 NuGet 套件。 如需 Visual Studio for Mac 中的體驗，請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)。 套件管理員 UI 未隨附於 Visual Studio Code。

> [!NOTE]
> 如果您在 Visual Studio 2015 中遺漏 NuGet 套件管理員，請查看 [工具] > [擴充功能和更新]，然後搜尋「NuGet 套件管理員」擴充功能。 如果您無法在 Visual Studio 中使用擴充功能安裝程式，請直接從 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) \(英文\) 下載擴充功能。
>
> 從 Visual Studio 2017 開始，NuGet 和 NuGet 套件管理員會隨任何 .NET 相關的工作負載自動安裝。 若要個別地安裝，請在 Visual Studio 安裝程式中選取 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 選項。

## <a name="find-and-install-a-package"></a>尋找並安裝套件

1. 在 [方案總管] 中，以滑鼠右鍵按一下 [參考] 或專案，然後選取 [管理 NuGet 套件]。

    ![[管理 NuGet 套件] 功能表選項](media/ManagePackagesUICommand.png)

1. [瀏覽] 索引標籤會依熱門度顯示目前所選來源的套件 (請參閱[套件來源](#package-sources))。 使用左上方的搜尋方塊來搜尋特定套件。 從清單中選取套件以顯示其資訊，這也會啟用 [安裝] 按鈕和版本選擇下拉式清單。

    ![管理 NuGet 套件對話方塊 [瀏覽] 索引標籤](media/Search.png)

1. 從下拉式清單選取所需的版本然後選取 [安裝]。 Visual Studio 會將套件及其相依性安裝到專案中。 系統可能會要求您接受授權條款。 安裝完成時，新增的封裝會出現在 [**已安裝**] 索引標籤上。套件也會列在方案總管的 [**參考**] 節點中，表示您可以在專案中使用 `using` 的語句來參考它們。

    ![方案總管中的 [參考]](media/References.png)

> [!Tip]
> 若要在搜尋中包含發行前版本，並且讓發行前版本可在 [版本] 下拉式清單中取得，請選取 [包含發行前版本] 選項。

> [!Note]
> NuGet 有兩種格式，可供專案使用封裝： [`PackageReference`](package-references-in-project-files.md)和[`packages.config`](../reference/packages-config.md)。 [預設值可以在 Visual Studio 的 [選項] 視窗中設定](Package-Restore.md#choose-default-package-management-format)。

## <a name="uninstall-a-package"></a>解除安裝套件

1. 在 [方案總管] 中，以滑鼠右鍵按一下 [參考] 或所需的專案，然後選取 [管理 NuGet 套件]。
1. 選取 [已安裝] 索引標籤。
1. 選取要解除安裝的套件 (如有必要，請使用搜尋功能篩選清單)，然後選取 [解除安裝]。

    ![將套件解除安裝](media/UninstallPackage.png)

1. 請注意，將套件解除安裝時，[包含發行前版本] 和 [套件來源] 控制項沒有任何影響。

## <a name="update-a-package"></a>更新套件

1. 在**方案總管**中，以滑鼠右鍵按一下 [**參考**] 或所需的專案，然後選取 [**管理 NuGet 套件 ...** ]。（在網站專案中，以滑鼠右鍵按一下 [ **Bin** ] 資料夾）。
1. 選取 [更新] 索引標籤，以查看在所選套件來源有可用更新的套件。 選取 [包含發行前版本]，以在更新清單中包含發行前版本套件。
1. 選取要更新的套件、從右邊的下拉式清單選取所需的版本，然後選取 [更新]。

    ![更新套件](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>對於某些套件，其 [更新] 按鈕已停用，並顯示訊息指出該套件「由 SDK 隱含參考」(或 "AutoReferenced")。 此訊息表示套件是較大架構或 SDK 的一部分，不應獨立更新。 （這類套件會在內部以 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`標示）。例如，`Microsoft.NETCore.App` 是 .NET Core SDK 的一部分，而封裝版本與應用程式所使用的執行時間架構版本不同。 您必須[更新 .NET Core 安裝](https://aka.ms/dotnet-download) \(英文\)，以取得新版本 ASP.NET Core 和 .Net Core 執行階段。 [如需 .NET Core 中繼套件和版本控制的詳細資料，請參閱此文件](/dotnet/core/packages)。 這適用於下列常用的套件：
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![標示為隱含參考或 AutoReferenced 的範例套件](media/PackageManagerUIAutoReferenced.png)

1. 若要將多個套件更新為最新版本，請在清單中選取它們，然後選取清單上方的 [更新] 按鈕。
1. 您也可以從 [**已安裝**] 索引標籤更新個別的封裝。在此情況下，封裝的詳細資料包含版本選取器（受限於 [**包含發行**前版本] 選項）和 [**更新**] 按鈕。

## <a name="manage-packages-for-the-solution"></a>管理解決方案的套件

管理解決方案的套件可讓同時處理多個專案更方便。

1. 選取 [工具] > [NuGet 套件管理員] > [管理解決方案的 NuGet 套件] 功能表命令，或以滑鼠右鍵按一下解決方案並選取 [管理 NuGet 套件]：

    ![管理解決方案的 NuGet 套件](media/ManagePackagesSolutionUICommand.png)

1. 在管理解決方案的套件時，UI 可讓您選取受作業影響的專案：

    ![管理解決方案套件時的專案選取器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>[合併] 索引標籤

開發人員通常會認為在相同的解決方案中，跨不同專案使用同一個 NuGet 套件的不同版本是不好的做法。 當您要管理解決方案的套件時，套件管理員 UI 提供 [合併] 索引標籤，您可以在其中輕鬆地查看解決方案中有哪些不同專案使用的套件具有不同版本號碼：

![套件管理員 UI [合併] 索引標籤](media/ConsolidateTab.png)

在此範例中，ClassLibrary1 專案使用 EntityFramework 6.2.0，而 ConsoleApp1 使用 EntityFramework 6.1.0。 若要合併套件版本，請執行下列動作：

- 在 [專案] 清單中選取要更新的專案。
- 在 [版本] 控制項中選取要在所有這些專案中使用的版本，例如，EntityFramework 6.2.0。
- 選取 [安裝] 按鈕。

套件管理員會將選取的套件版本安裝到所有已選取的專案中，之後套件就不會再出現在 [合併] 索引標籤上。

## <a name="package-sources"></a>套件來源

若要變更 Visual Studio 取得套件的來源，請從來源選取器中選取：

![套件管理員 UI 中的 [套件來源] 選取器](media/PackageSourceDropDown.png)

若要管理套件來源：

1. 選取底下所示套件管理員 UI 中的 [設定] 圖示，或使用 [工具] > [選項] 命令，並捲動至 [NuGet 套件管理員]：

    ![套件管理員 UI 設定圖示](media/PackageSourceSettings.png)

1. 選取 [套件來源] 節點：

    ![[套件來源] 選項](media/options.png)

1. 若要新增來源，請選取 **+** 、編輯名稱、在 [來源] 控制項中輸入 URL 或路徑，然後選取 [更新]。 來源現在會顯示在選取器下拉式清單中。
1. 若要變更套件來源，請選取套件、在 [名稱] 和 [來源] 方塊中編輯，然後選取 [更新]。
1. 若要停用套件來源，請取消選取清單中名稱左邊的方塊。
1. 若要移除套件來源，請選取它，然後選取 [X] 按鈕。
1. 使用向上和向下箭號按鈕不會變更套件來源的優先順序。 Visual Studio 會忽略套件來源的順序，而使用任一個最先回應要求的來源。 如需詳細資訊，請參閱[套件還原](../consume-packages/package-restore.md)。

> [!Tip]
> 如果套件來源在刪除後重新出現，它可能是列在電腦層級或使用者層級的 `NuGet.Config` 檔案中。 請參閱[常用的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)，以了解這些檔案的位置，然後手動編輯這些檔案或使用 [nuget sources 命令](../reference/nuget-exe-CLI-reference.md)將來源移除。

## <a name="package-manager-options-control"></a>套件管理員 [選項] 控制項

選取套件時，套件管理員 UI 會在版本選取器下方顯示一個小型、可展開的 [選項] 控制項 (在此顯示摺疊和展開的狀態)。 請注意，某些專案類型只提供 [顯示預覽視窗] 選項。

![套件管理員選項](media/PackageManagerUIOptions.png)

下列各節會說明這些選項。

### <a name="show-preview-window"></a>顯示預覽視窗

選取此選項時，系統會在安裝套件之前顯示強制回應視窗，顯示所選套件的相依性：

![範例預覽對話方塊](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>安裝和更新選項

(並非所有專案類型都適用)。

[相依性行為] 會設定 NuGet 如何決定要安裝的相依套件版本：

- [忽略相依性] 會略過安裝任何相依性，這通常會使安裝的套件無法運作。
- [最低] [預設] 會使用符合主要所選套件需求的最小版本號碼來安裝相依性。
- [最高修補程式] 會使用相同的主要和次要版本號碼 (但有最高的修補程式號碼) 來安裝版本。 例如，如果指定 1.2.2 版則會安裝開頭為 1.2 的最高版本
- [最高次要] 會使用相同的主要版本號碼，但最高的次要號碼和修補程式號碼來安裝版本。 如果指定 1.2.2 版，則會安裝開頭為 1 的最高版本
- [最高] 會安裝套件的最高可用版本。

[檔案衝突動作] 會指定 NuGet 應如何處理已存在於專案或本機電腦中的套件：

- [提示] 會指示 NuGet 詢問要保留或覆寫現有套件。
- [全部忽略] 會指示 NuGet 略過覆寫任何現有套件。
- [全部覆寫] 會指示 NuGet 覆寫任何現有套件。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>解除安裝選項

(並非所有專案類型都適用)。

[移除相依性]：選取此選項時，系統會移除未在專案中其他位置參考的任何相依性套件。

[即使有相依性仍強制解除安裝]：選取時，即使專案中仍有項目參考該套件，也會將該套件解除安裝。 這通常與 [移除相依性] 結合使用，以移除套件和它所安裝的任何相依性。 不過，使用這個選項可能會導致專案中的參考無法運作。 在此情況下，您可能必須[重新安裝其他套件](../consume-packages/reinstalling-and-updating-packages.md)。
