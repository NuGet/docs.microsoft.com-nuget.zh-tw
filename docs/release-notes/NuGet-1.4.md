---
title: NuGet 1.4 版本資訊
description: NuGet 1.4 的版本資訊, 包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5f1d3ed6a1b20fb07437f1718faafaac0a193773
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488701"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 版本資訊

[Nuget 1.3 版本](../release-notes/nuget-1.3.md) | 資訊[nuget 1.5 版本](../release-notes/nuget-1.5.md)資訊

NuGet 1.4 已于2011年6月17日發行。

## <a name="features"></a>功能

### <a name="update-package-improvements"></a>更新-套件改良功能
NuGet 1.4 引進了許多更新封裝命令的改良功能, 讓您更輕鬆地在解決方案中的多個專案之間保持相同版本的套件。 例如, 將套件升級至最新版本時, 要將安裝該套件的所有專案更新為相同的 verision, 是很常見的情況。

`Update-Package`命令現在可讓您更輕鬆地執行下列作業:

#### <a name="update-all-packages-in-a-single-project"></a>更新單一專案中的所有封裝

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>更新所有專案中的封裝

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>更新所有專案中的所有封裝

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>對所有套件執行「安全」更新
`-Safe`旗標會限制只能升級至具有相同主要和次要版本元件的版本。 例如, 如果已安裝版本1.0.0 的封裝, 而摘要中有版本1.0.1、1.0.2 和 1.1, `-Safe`旗標就會將套件更新為1.0.2。 升級時若`-Safe`沒有旗標, 會將套件升級至最新版本1.1。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>在解決方案層級管理封裝
在 NuGet 1.4 之前, 使用對話方塊將封裝安裝到多個專案會很麻煩。 每個專案都必須啟動對話方塊一次。

NuGet 1.4 加入了在多個專案中同時安裝/卸載/更新套件的支援。 只要以滑鼠右鍵按一下方案, 然後選取 [**管理 NuGet 套件**] 功能表選項, 即可啟動。

![解決方案層級的 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-solution-dialog.png)

請注意, 在對話方塊的標題列中, 會顯示方案的名稱, 而不是專案的名稱。
封裝作業現在提供具有作業應套用之專案清單的核取方塊清單。

![管理 NuGet 套件專案選擇](./media/manage-nuget-packages-project-selection.png)

如需詳細資訊, 請參閱[管理解決方案的封裝](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)主題。

### <a name="constraining-upgrades-to-allowed-versions"></a>限制升級為允許的版本
根據預設, 在封裝上`Update-Package`執行命令 (或使用對話方塊更新封裝) 時, 它會更新為摘要中的最新版本。 有了更新所有封裝的新支援, 您可能會想要將封裝鎖定至特定版本範圍。 例如, 您可能事先知道, 您的應用程式只會使用版本 2. * 的套件, 而不是3.0 和更新版本。 為了避免不小心將套件更新為 3, NuGet 1.4 加入了限制封裝可升級的版本的支援, 方法是使用新`packages.config` `allowedVersions`的屬性手動編輯該檔案。

例如, 下列範例示範如何鎖定`SomePackage`版本範圍 2.0-3.0 (獨佔) 的套件。
屬性會接受使用[版本範圍格式](../concepts/package-versioning.md#version-ranges-and-wildcards)的值。 `allowedVersions`

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

請注意, 在1.4 中, 必須手動編輯特定版本範圍的封裝。 在 NuGet 1.5 中, 我們打算新增透過`Install-Package`命令來放置此範圍的支援。

### <a name="package-visualizer"></a>封裝視覺化
新的封裝視覺化檢視會透過 [**工具** -> ] [程式庫] [**套件管理員** -> **封裝**] 功能表選項來啟動, 讓您可以輕鬆地將所有專案及其在中的套件相依性視覺化解.

_**重要注意事項:** 這項功能會利用 Visual Studio 中的 DGML 支援。只有在 Visual Studio Ultimate 中才支援建立視覺效果。只有 Visual Studio Premium 或更高版本才支援視圖 DGML 圖表。_

![封裝視覺化](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet 對話的自動更新檢查
某些版本的 nuget 會導入透過檔案所`.nuspec`表示的新功能, 而舊版的 nuget 對話並不瞭解。
其中一個範例是 NuGet 1.4 中用來[指定架構元件](../release-notes/nuget-1.2.md#framework-assembly-refs)的簡介。
因此, 請務必使用最新版本的 NuGet, 以確保您可以使用可利用最新功能的套件。
若要讓 NuGet 的更新更可見, NuGet 對話方塊會包含在有較新版本可用時反白顯示的邏輯。

_**注意**:只有在目前的會話中選取 [**線上**] 索引標籤時, 才會進行檢查。_

![提供新版本的 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-update-notification.png)

若要關閉自動檢查更新, 請移至 [NuGet 設定] 對話方塊, 並取消核取 [**自動檢查更新**]。

![NuGet 設定](./media/nuget-settings.png)

這項功能實際上是在 NuGet 1.3 中新增, 但是在更新至 1.3 (例如 NuGet 1.4) 之前, 並不會顯示。

### <a name="package-manager-dialog-improvements"></a>套件管理員對話方塊改善
* **改良的功能表名稱**:為了清楚起見, 啟動對話方塊的功能表選項已重新命名。 [功能表] 選項現在是 [**管理 NuGet 封裝**]。
* [**詳細資料] 窗格會顯示最新的更新日期**:當選取 [**線上**] 或 [**更新**] 索引標籤時, [NuGet] 對話方塊會在封裝的詳細資料窗格中顯示最新更新的日期。
* **顯示的標記清單**:Nuget 對話方塊會顯示標記。

### <a name="powershell-improvements"></a>Powershell 改良功能
* **已簽署的 PowerShell 腳本**:NuGet 包含已簽署的 Powershell 腳本, 讓您在更嚴格的環境中使用。
* **提示支援**:套件管理員主控台現在支援透過`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令的提示。
* **套件來源名稱**:使用`-Source`旗標指定封裝來源時, 支援提供封裝來源的名稱。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 命令列改良功能
* **Nuget 自訂命令**: nuget.exe 可透過使用 MEF 的自訂命令進行擴充。
* **更簡單地建立符號套件的工作流程**:旗標可以套用至一般慣例式資料夾結構, 只需包含資料夾中的來源和`.pdb`檔案, 即可建立符號套件。 `-Symbols`
* **指定多個來源**:命令支援使用分號做為分隔符號, 或指定`-Source`多次來指定多個來源。 `NuGet install`
* **Proxy 驗證支援**:在需要驗證的 proxy 後方使用 NuGet 時, NuGet 1.4 新增了提示輸入使用者認證的支援。
* **Nuget.exe 更新中斷性變更**:現在需要有旗標, nuget.exe 才會自行更新。 `-Self` `nuget.exe Update`現在會採用檔案的路徑`packages.config` , 並嘗試更新套件。 請注意, 這項更新的限制在於, 它不會: * * 更新、新增、移除專案檔中的內容。
\* * 在封裝內執行 Powershell 腳本。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>NuGet 伺服器支援使用 nuget.exe 推送套件
Nuget 包含一個簡單的方式, 可透過`NuGet.Server` NuGet 套件裝載[輕量的 web 型 NuGet 存放庫](../hosting-packages/nuget-server.md)。 使用 NuGet 1.4, 輕量伺服器支援使用 nuget.exe 推送和刪除套件。
的最新版本`NuGet.Server`會新增名`appSetting`為`apiKey`的新。 當省略金鑰或保留空白時, 會停用將套件推送至摘要的功能。 將 apiKey 設定為值 (最好是強式密碼), 可以使用 nuget.exe 來推送套件。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone Tools Mango Edition 的支援
Windows Phone Tools for Mango 的發行候選版本現在支援 NuGet。
Windows Phone 工具目前不支援 Visual Studio 延伸模組管理員, 因此若要安裝適用于 Windows Phone 工具的 NuGet, 您可能需要手動下載並執行 VSIX。

若要卸載 Windows Phone 工具的 NuGet, 請執行下列命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>錯誤修正
NuGet 1.4 總共已修正88個工作專案。 71的已標示為 bug。

如需 NuGet 1.4 中已修正之工作專案的完整清單, 請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>錯誤修正值得注意:

* [問題 603](http://nuget.codeplex.com/workitem/603):指定特定封裝來源時, 跨不同存放庫的套件相依性會正確解析。
* [問題 1036](http://nuget.codeplex.com/workitem/1036):新增`NuGet Pack SomeProject.csproj`至後置組建事件不會再造成無限迴圈。
* [問題 961](http://nuget.codeplex.com/workitem/961): `-Source`旗標支援相對路徑。

## <a name="nuget-14-update"></a>NuGet 1.4 更新
在 NuGet 1.4 發行之後不久, 我們發現有幾個重要的問題要修正。
此更新至1.4 的特定版本號碼為1.4.20615.9020。

### <a name="bug-fixes"></a>錯誤修正
* [問題 1220](http://nuget.codeplex.com/workitem/1220):當有一個以上的`install.ps1`專案時, 更新套件不會在所有專案中執行/ `uninstall.ps1`
* [問題 1156](http://nuget.codeplex.com/workitem/1156):套件管理員主控台卡在 W2K3/XP 上 (未安裝 Powershell 2 時)
