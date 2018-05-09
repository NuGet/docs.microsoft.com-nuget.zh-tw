---
title: NuGet 1.4 版本資訊
description: 版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.4。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5e4c2a5f2db80b0ebc3fec7c653aecb8bcc4ab5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 版本資訊

[NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md) | [NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md)

NuGet 1.4 已於 2011 年 6 月 17 日發行。

## <a name="features"></a>功能

### <a name="update-package-improvements"></a>更新套件增強功能
NuGet 1.4 導入了許多增強功能輕鬆地保持在相同版本的封裝，跨多個專案方案中的 [更新套件] 命令。 例如，封裝升級至最新版本，時很常見，想要與相同 verision 更新已安裝該套件的所有專案。

`Update-Package`命令現在可讓您更輕鬆地：

#### <a name="update-all-packages-in-a-single-project"></a>更新單一專案中的所有套件

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>更新所有專案的封裝

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>更新所有專案中的所有套件

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>所有封裝執行的 「 安全 」 的更新
`-Safe`旗標限制只升級至具有相同主要和次要版本元件的唯一版本。 例如，若已安裝版本 1.0.0 的封裝，而摘要中有 1.0.1、 1.0.2 和 1.1 版`-Safe`旗標會將套件更新為 1.0.2。 升級，而`-Safe`旗標會將封裝升級至最新版本，也就是 1.1。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>管理方案層級的封裝
NuGet 1.4 之前安裝的套件分成多個專案問世使用對話方塊。 您需要啟動 [一次每個專案] 對話方塊。

NuGet 1.4 同時在多個專案新增安裝/解除安裝/更新封裝的支援。 只要啟動以滑鼠右鍵按一下方案並選取**管理 NuGet 封裝**功能表選項。

![方案層級管理 NuGet 套件對話方塊](./media/manage-nuget-packages-solution-dialog.png)

請注意，在對話方塊的標題列，會顯示方案的名稱，而不是專案的名稱。
封裝作業現在會提供一份核取方塊，包含作業應套用至專案的清單。

![管理 NuGet 封裝專案選取項目](./media/manage-nuget-packages-project-selection.png)

如需詳細資訊，請參閱主題[解決方案的管理套件](../tools/package-manager-ui.md#managing-packages-for-the-solution)。

### <a name="constraining-upgrades-to-allowed-versions"></a>條件約束至允許的版本升級
根據預設，當執行`Update-Package`命令封裝 （或更新套件，對話方塊），將會更新摘要中的最新版本。 更新所有封裝的新支援，可能情況下，您要鎖定的特定版本範圍封裝。 例如，您可能事先知道您的應用程式將只使用版本 2.*，但不是 3.0 和更新版本的封裝。 若要避免不小心更新為 3 的套件，NuGet 1.4 新增的條件約束可由手動編輯來升級封裝的版本範圍支援`packages.config`檔案使用新`allowedVersions`屬性。

例如，下列範例顯示如何鎖定`SomePackage`套件版本範圍 2.0 3.0 （獨佔）。
`allowedVersions`屬性接受的值使用[版本範圍格式](../reference/package-versioning.md#version-ranges-and-wildcards)。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

請注意，在 1.4，鎖定特定的版本範圍封裝必須手動編輯。 我們計劃 NuGet 1.5 中加入支援將透過此範圍`Install-Package`命令。

### <a name="package-visualizer"></a>封裝的視覺化檢視
新的封裝視覺化檢視，啟動透過**工具** -> **程式庫套件管理員** -> **封裝視覺化檢視**功能表選項，可讓您輕鬆地將所有專案與方案中的封裝相依性視覺化。

_**重要事項：**這項功能會利用 DGML 支援 Visual Studio 中。在 Visual Studio Ultimate 中才支援建立視覺效果。只支援在 Visual Studio Premium 或高階檢視 DGML 圖表。_

![封裝的視覺化檢視](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>自動更新檢查 NuGet 對話方塊
某些版本的 NuGet 導入新的功能，以表示透過`.nuspec`較舊版本的 NuGet 對話方塊不了解的檔案。
其中一個範例是簡介 > 中的 NuGet 1.4[指定 framework 組件](../release-notes/nuget-1.2.md#framework-assembly-refs)。
基於此原因，是使用最新版的 NuGet 以確保您可以使用套件利用最新的功能。
若要更新 NuGet 更明顯可見，NuGet 對話方塊會包含邏輯，以較新版本可用時，反白顯示。

_**請注意**： 檢查只會**線上**已選取目前的工作階段中的索引標籤。_

![管理與新的版本可用的 NuGet 套件 對話方塊](./media/manage-nuget-packages-update-notification.png)

若要關閉自動檢查更新，請移至 [NuGet 設定] 對話方塊，並取消選取**自動檢查更新**。

![NuGet 設定](./media/nuget-settings.png)

這項功能實際上已加入 NuGet 1.3 但不是會顯示，而且當然 1.3，例如 NuGet 1.4 更新之前，已提供。

### <a name="package-manager-dialog-improvements"></a>封裝管理員對話方塊改進
* **改善的功能表名稱**： 更清楚，所以已重新命名功能表選項，以啟動對話方塊。 功能表選項現在是**管理 NuGet 封裝**。
* **詳細資料 窗格會顯示最新的更新日期**: NuGet 對話方塊顯示封裝的詳細資料窗格中的最新的更新的日期時**線上**或**更新**選取索引標籤。
* **顯示的標記清單**: Nuget 對話方塊會顯示標籤。

### <a name="powershell-improvements"></a>Powershell 增強功能
* **簽署的 PowerShell 指令碼**: NuGet 包含帶正負號的 Powershell 指令碼啟用更嚴格的環境中的使用量。
* **提示支援**: Package Manager Console 現在支援透過提示`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令。
* **封裝來源名稱**： 時，指定封裝來源，使用提供的套件來源名稱支援`-Source`旗標。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 命令列增強功能
* **自訂的 NuGet 命令**: nuget.exe 是透過自訂的命令使用 MEF 可延伸。
* **更簡單的工作流程建立符號封裝**:`-Symbols`旗標可套用至建立符號封裝只包括來源的一般慣例為基礎資料夾結構和`.pdb`資料夾中的檔案。
* **指定多個來源**:`NuGet install`命令支援指定的分隔符號，或藉由指定使用分號分隔的多個來源`-Source`多次。
* **Proxy 驗證支援**: NuGet 1.4 新增支援使用 NuGet 需要驗證的 proxy 後面時，提示使用者提供認證。
* **nuget.exe 更新的重大變更**:`-Self`旗標現在是所需的 nuget.exe 自行更新。 `nuget.exe Update` 中的路徑現在採用`packages.config`檔案，並嘗試更新套件。 請注意，這項更新限制，則不會: * * 更新，新增、 移除內容中的專案檔。
* * 在封裝中的執行 Powershell 指令碼。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>使用 nuget.exe 推送封裝的 NuGet 伺服器支援
NuGet 包含簡單的方式來主機[輕量 web 型 NuGet 儲存機制](../hosting-packages/nuget-server.md)透過`NuGet.Server`NuGet 封裝。 使用 NuGet 1.4 輕量型伺服器支援推入和刪除使用 nuget.exe 的封裝。
最新版`NuGet.Server`加入新`appSetting`具名`apiKey`。 索引鍵是省略或保留空白，將封裝推送到摘要會停用。 設定 apiKey 的值 （最好是強式密碼），可讓使用 nuget.exe 推送的封裝。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone 工具 Mango 版本支援
NuGet 現在支援 Mango 的 Windows Phone 工具發行候選版本中。
目前，Windows Phone 工具並沒有支援的 Visual Studio 擴充功能管理員，因此若要安裝 Windows Phone 工具的 NuGet，您可能需要下載並手動執行 VSIX。

若要解除安裝 Windows Phone 工具的 NuGet，請執行下列命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.4 有工作項目固定 88 總數。 這些 71 已標示為錯誤。

如需完整的工作清單項目固定在 NuGet 1.4 中請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修正：

* [問題 603](http://nuget.codeplex.com/workitem/603)： 跨不同的儲存機制的封裝相依性時，可以解決正確地指定特定的封裝來源。
* [問題 1036年](http://nuget.codeplex.com/workitem/1036)： 加入`NuGet Pack SomeProject.csproj`來建置後事件不會再造成無限迴圈。
* [問題 961](http://nuget.codeplex.com/workitem/961):`-Source`旗標可支援相對路徑。

## <a name="nuget-14-update"></a>NuGet 1.4 更新
不久後 NuGet 1.4 版本中，我們可以發現幾個重要修正的問題。
這項更新 1.4 的特定版本號碼是 1.4.20615.9020。

### <a name="bug-fixes"></a>Bug 修正
* [問題 1220年](http://nuget.codeplex.com/workitem/1220)： 不會執行更新套件`install.ps1` / `uninstall.ps1`多個專案時，所有專案中
* [問題 1156年](http://nuget.codeplex.com/workitem/1156)： 封裝管理員主控台卡 W2K3/XP 上 （當未安裝 Powershell 2）
