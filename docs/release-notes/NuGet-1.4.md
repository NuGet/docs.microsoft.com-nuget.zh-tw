---
title: NuGet 1.4 版本資訊
description: NuGet 1.4 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777150"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 版本資訊

[NuGet 1.3 版本](../release-notes/nuget-1.3.md)  |  資訊[NuGet 1.5 版本](../release-notes/nuget-1.5.md)資訊

NuGet 1.4 已于2011年6月17日發行。

## <a name="features"></a>功能

### <a name="update-package-improvements"></a>Update-Package 改進
NuGet 1.4 對 Update-Package 命令引進了許多改進，讓您更輕鬆地在解決方案中的多個專案之間保持相同版本的套件。 例如，將封裝升級至最新版本時，您通常會想要將該套件安裝的所有專案更新為相同 verision。

`Update-Package`命令現在可讓您更輕鬆地：

#### <a name="update-all-packages-in-a-single-project"></a>更新單一專案中的所有套件

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a>更新所有專案中的封裝

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a>更新所有專案中的所有封裝

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a>對所有套件執行「安全」更新
旗標會 `-Safe` 限制只升級為具有相同主要和次要版本元件的版本。 例如，如果已安裝版本1.0.0 的封裝，且摘要中有版本1.0.1、1.0.2 和1.1，旗標就會將 `-Safe` 套件更新為1.0.2。 如果沒有旗標升級， `-Safe` 就會將套件升級為最新版本1.1。

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a>在解決方案層級管理套件
在 NuGet 1.4 之前，使用對話方塊將套件安裝至多個專案會很麻煩。 每個專案都需要啟動對話方塊一次。

NuGet 1.4 新增了同時在多個專案中安裝/卸載/更新套件的支援。 只要以滑鼠右鍵按一下方案，然後選取 [ **管理 NuGet 套件** ] 功能表選項，即可啟動。

![解決方案層級 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-solution-dialog.png)

請注意，在對話方塊的標題列中，會顯示方案的名稱，而不是專案的名稱。
封裝作業現在會提供核取方塊清單，其中包含應套用作業的專案清單。

![管理 NuGet 套件專案選取專案](./media/manage-nuget-packages-project-selection.png)

如需詳細資訊，請參閱 [管理解決方案套件](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)的主題。

### <a name="constraining-upgrades-to-allowed-versions"></a>將升級限制為允許的版本
根據預設，在 `Update-Package` 封裝上執行命令 (或使用對話方塊) 更新套件時，將會更新為摘要中的最新版本。 有了更新所有封裝的新支援，在某些情況下，您可能會想要將套件鎖定至特定版本範圍。 例如，您可能事先知道您的應用程式只會使用版本 2. * 的封裝，而不是3.0 或更新版本。 為了避免不小心將套件更新為3，NuGet 1.4 新增了支援，以限制可以升級套件的版本範圍，方法是 `packages.config` 使用新屬性手動編輯檔案 `allowedVersions` 。

例如，下列範例示範如何鎖定 `SomePackage` 套件版本範圍 2.0-3.0 (獨佔) 。
`allowedVersions`屬性接受使用[版本範圍格式](../concepts/package-versioning.md#version-ranges)的值。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

請注意，在1.4 中，鎖定特定版本範圍的套件必須是手動編輯的。 在 NuGet 1.5 中，我們計畫新增透過命令來放置此範圍的支援 `Install-Package` 。

### <a name="package-visualizer"></a>封裝視覺化
透過 [**工具**  ->  **庫封裝管理員** 套件視覺化檢視] 功能表選項啟動的新封裝視覺化檢視，可  ->  讓您輕鬆地視覺化方案內的所有專案及其套件相依性。

_**重要注意事項：** 這項功能會利用 Visual Studio 中的 DGML 支援。只有 Visual Studio Ultimate 才支援建立視覺效果。只有 Visual Studio Premium 或更高版本才支援查看 DGML 圖表。_

![封裝視覺化](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet 對話方塊的自動更新檢查
某些版本的 NuGet 引進了透過檔案表示的新功能， `.nuspec` 這些功能是舊版 NuGet 對話方塊無法理解的。
其中一個範例是 NuGet 1.4 中用來 [指定架構元件](../release-notes/nuget-1.2.md#framework-assembly-refs)的簡介。
因此，請務必使用最新版本的 NuGet，以確保您可以使用封裝，以利用最新的功能。
若要讓 NuGet 的更新更清楚，NuGet 對話方塊會包含可在有較新版本可用時醒目提示的邏輯。

_**注意**：只有在目前的會話中選取 [ **線上** ] 索引標籤時，才會進行檢查。_

![有新版本可用的 [管理 NuGet 套件] 對話方塊](./media/manage-nuget-packages-update-notification.png)

若要關閉自動檢查更新，請移至 [NuGet 設定] 對話方塊，並取消核取 [ **自動檢查更新**]。

![NuGet 設定](./media/nuget-settings.png)

這項功能實際上是新增在 NuGet 1.3 中，但在更新至1.3 之前（例如 NuGet 1.4），將不會顯示。

### <a name="package-manager-dialog-improvements"></a>封裝管理員對話方塊改進
* **改良的功能表名稱**：為了清楚起見，已重新命名啟動對話方塊的功能表選項。 功能表選項現在是 [ **管理 NuGet 套件**]。
* **詳細資料窗格會顯示最新的更新日期**：當選取 [ **線上** ] 或 [ **更新** ] 索引標籤時，NuGet 對話方塊會在套件的詳細資料窗格中顯示最新的更新日期。
* **顯示的標記清單**： Nuget 對話方塊會顯示標記。

### <a name="powershell-improvements"></a>Powershell 改進
* **已簽署的 powershell 腳本**： NuGet 包含已簽署的 powershell 腳本，以便在更嚴格的環境中使用。
* **提示支援**：封裝管理員主控台現在支援透過 `$host.ui.Prompt` 和命令的提示 `$host.ui.PromptForChoice` 。
* **封裝來源名稱**：使用旗標指定套件來源時，支援提供封裝來源的名稱 `-Source` 。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 命令列改進
* **NuGet 自訂命令**： nuget.exe 可透過使用 MEF 的自訂命令進行擴充。
* **建立符號套件的工作流程更簡單**： `-Symbols` 旗標可以套用至一般慣例式資料夾結構，只要在資料夾內包含來源和檔案，就可以建立符號套件 `.pdb` 。
* **指定多個來源**： `NuGet install` 命令支援使用分號做為分隔符號來指定多個來源，或是指定 `-Source` 多次。
* **Proxy 驗證支援**：當在需要驗證的 Proxy 後方使用 nuget 時，nuget 1.4 新增了提示使用者認證的支援。
* **nuget.exe 更新中斷變更**： `-Self` nuget.exe 必須有旗標才能自行更新。 `nuget.exe Update` 現在會取得檔案的路徑 `packages.config` ，並嘗試更新套件。 請注意，此更新的限制為不會： * * 更新、新增、移除專案檔中的內容。
* * 在封裝內執行 Powershell 腳本。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>使用 nuget.exe 推送套件的 NuGet 伺服器支援
NuGet 包含簡單的方法，可透過 nuget 套件裝載 [輕量 web 型 NuGet 存放庫](../hosting-packages/nuget-server.md) `NuGet.Server` 。 使用 NuGet 1.4，輕量伺服器支援使用 nuget.exe 來推送和刪除封裝。
的最新版本會 `NuGet.Server` 新增 `appSetting` 名為的新 `apiKey` 。 當索引鍵省略或保留空白時，就會停用將套件推送至摘要的功能。 將 apiKey 設定為值 (理想的強式密碼) 使用 nuget.exe 來推送套件。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>支援 Windows Phone Tools Mango Edition
Windows Phone Tools for Mango 的發行候選版本現在支援 NuGet。
Windows Phone 工具目前不支援 Visual Studio 的延伸模組管理員，因此若要安裝適用于 Windows Phone 工具的 NuGet，您可能需要手動下載並執行 VSIX。

若要卸載 Windows Phone 工具的 NuGet，請執行下列命令。

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.4 總共修正了88個工作專案。 這些標記為 bug 的71。

如需 NuGet 1.4 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>Bug 修正值得注意：

* [問題 603](http://nuget.codeplex.com/workitem/603)：指定特定套件來源時，跨不同存放庫的套件相依性可正確解析。
* [問題 1036](http://nuget.codeplex.com/workitem/1036)：新增 `NuGet Pack SomeProject.csproj` 到後置建立事件不再造成無限迴圈。
* [問題 961](http://nuget.codeplex.com/workitem/961)： `-Source` 旗標支援相對路徑。

## <a name="nuget-14-update"></a>NuGet 1.4 更新
在發行 NuGet 1.4 之後不久，我們發現有幾個重要的問題要修正。
此更新至1.4 的特定版本號碼為1.4.20615.9020。

### <a name="bug-fixes"></a>Bug 修正
* [問題 1220](http://nuget.codeplex.com/workitem/1220)： `install.ps1` / `uninstall.ps1` 當有一個以上的專案時，Update-Package 不會在所有專案中執行
* [問題 1156](http://nuget.codeplex.com/workitem/1156)：未安裝 Powershell 2 時，封裝管理員主控台卡在 W2K3/XP () 
