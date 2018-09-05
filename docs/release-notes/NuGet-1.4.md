---
title: NuGet 1.4 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.4 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550627"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 的版本資訊

[NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md) | [NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md)

於 2011 年 6 月 17 日發行 NuGet 1.4。

## <a name="features"></a>功能

### <a name="update-package-improvements"></a>更新套件改善
NuGet 1.4 導入了許多增強功能讓您更輕鬆地保持相同的版本中的封裝，在方案中的多個專案的 [更新套件] 命令。 例如，升級為最新版本的封裝，時很常見，要更新為相同 verision 已安裝該套件的所有專案。

`Update-Package`命令現在可讓您更輕鬆地：

#### <a name="update-all-packages-in-a-single-project"></a>更新單一專案中的所有封裝

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>更新所有專案中的套件

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>更新所有專案中的所有封裝

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>所有封裝執行的 「 安全 」 的更新
`-Safe`旗標限制升級至具有相同的主要和次要版本元件的唯一版本。 例如，如果已安裝版本 1.0.0 的封裝，而有版本 1.0.1、 1.0.2 與 1.1 可用的摘要中`-Safe`旗標將此封裝更新至 1.0.2。 升級不含`-Safe`旗標會將套件升級為最新版本，也就是 1.1。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>方案層級的管理套件
在 NuGet 1.4 之前套件安裝至多個專案十分麻煩使用對話方塊。 您需要啟動每一次的專案 對話方塊。

NuGet 1.4 會新增多個專案中安裝/解除安裝/更新封裝的支援，在相同的時間。 只要啟動方案上按一下滑鼠右鍵，然後選取**管理 NuGet 套件**功能表選項。

![方案層級管理 NuGet 套件 對話方塊](./media/manage-nuget-packages-solution-dialog.png)

請注意，在對話方塊的標題列中，會顯示方案的名稱，而不是專案的名稱。
封裝作業現在會提供核取方塊的清單作業應該套用到專案的清單。

![管理 NuGet 封裝專案選取項目](./media/manage-nuget-packages-project-selection.png)

如需詳細資訊，請參閱主題[管理方案的套件](../tools/package-manager-ui.md#managing-packages-for-the-solution)。

### <a name="constraining-upgrades-to-allowed-versions"></a>限制升級至允許的版本
根據預設，當執行`Update-Package`命令封裝 （或更新套件，對話方塊），將會更新為最新的版本，摘要中。 更新所有封裝的新支援，可能情況下您想要鎖定在特定版本範圍內的封裝。 例如，您可能事先知道您的應用程式只會使用 2.* 版的封裝，但不是 3.0 或更新版本。 為了防止意外更新為 3 的套件，NuGet 1.4 新增對限制的封裝可以升級為，透過手動編輯的版本範圍`packages.config`檔案中，使用新`allowedVersions`屬性。

例如，下列範例顯示如何鎖定`SomePackage`套件版本範圍 2.0-3.0 （獨佔）。
`allowedVersions`屬性可接受的值使用[版本範圍格式](../reference/package-versioning.md#version-ranges-and-wildcards)。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

請注意，在 1.4，鎖定特定版本範圍封裝必須手動編輯。 我們計劃 NuGet 1.5 中加入此支援將透過此範圍`Install-Package`命令。

### <a name="package-visualizer"></a>封裝視覺化檢視
新的封裝視覺化檢視，透過啟動**工具** -> **程式庫套件管理員** -> **封裝視覺化檢視**功能表選項，可讓您輕鬆地以視覺化方式檢視所有專案和其解決方案中的封裝相依性。

_**重要事項：** 這項功能會利用 DGML 支援中的 Visual Studio。在 Visual Studio Ultimate 中才支援建立視覺效果。檢視 DGML 圖表僅適用於 Visual Studio Premium 或高等教育中。_

![封裝視覺化檢視](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>[NuGet] 對話方塊中的自動更新檢查
某些版本的 NuGet 引進新功能，透過表示`.nuspec`不了解舊版 NuGet 對話方塊的檔案。
其中一個範例是在 NuGet 1.4 的簡介[指定 framework 組件](../release-notes/nuget-1.2.md#framework-assembly-refs)。
基於這個原因，請務必使用最新版的 NuGet，以確保您可以使用套件利用最新的功能。
若要讓 NuGet 的更新更明顯可見，NuGet 對話方塊會包含更新的版本時反白顯示的邏輯。

_**附註**： 如果，才有核取**Online**目前工作階段中已選取索引標籤。_

![[管理 NuGet 套件] 對話方塊，可用的新版本](./media/manage-nuget-packages-update-notification.png)

若要關閉自動檢查更新，請移至 NuGet 的 [設定] 對話方塊，並取消核取**自動檢查更新**。

![NuGet 設定](./media/nuget-settings.png)

這項功能實際上已加入 NuGet 1.3，但就不會顯示，當然，1.3，例如 NuGet 1.4 的更新，所提供。

### <a name="package-manager-dialog-improvements"></a>套件管理員 對話方塊改良
* **改善的功能表名稱**： 為了清楚起見已重新命名功能表選項，以啟動對話方塊。 功能表選項現**管理 NuGet 套件**。
* **詳細資料 窗格會顯示最新的更新日期**: NuGet 對話方塊會顯示封裝的詳細資料窗格中的最新的更新的日期時**Online**或是**更新**選取索引標籤。
* **顯示的標記清單**: Nuget 對話方塊就會顯示標籤。

### <a name="powershell-improvements"></a>Powershell 增強功能
* **簽署的 PowerShell 指令碼**: NuGet 包含帶正負號的 Powershell 指令碼啟用更嚴格的環境中的使用量。
* **提示支援**: 套件管理員主控台現在支援透過提示`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令。
* **套件來源名稱**： 提供的套件來源的名稱指定套件來源使用時，支援`-Source`旗標。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 命令列改進功能
* **NuGet 的自訂命令**: nuget.exe 可透過使用 MEF 的自訂命令。
* **更簡單的工作流程建立符號套件**:`-Symbols`旗標可以用來建立符號套件僅包含來源的一般慣例為基礎資料夾結構和`.pdb`資料夾中的檔案。
* **指定多個來源**:`NuGet install`命令支援指定多個使用分號作為分隔符號，或藉由指定的來源`-Source`多次。
* **Proxy 驗證支援**: NuGet 1.4 新增對需要驗證的 proxy 後方使用 NuGet 時提示使用者提供認證。
* **nuget.exe 更新的重大變更**:`-Self`現在是旗標所需的 nuget.exe 更新本身。 `nuget.exe Update` 現在會採用的路徑`packages.config`檔案，並將嘗試更新套件。 請注意，這項更新限制，則不會: * * 更新，新增、 移除專案檔案中的內容。
* * 封裝內的執行 Powershell 指令碼。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>使用 nuget.exe 推送套件的 NuGet 伺服器支援
NuGet 包含簡單的方式來裝載[輕量 web 型 NuGet 存放庫](../hosting-packages/nuget-server.md)透過`NuGet.Server`NuGet 套件。 使用 NuGet 1.4 輕量級伺服器支援推送和刪除使用 nuget.exe 的封裝。
最新版`NuGet.Server`將新`appSetting`具名`apiKey`。 當索引鍵是省略或留白時，會停用將套件推送至摘要。 設定 apiKey 的值 （在理想情況下是強式密碼），可讓使用 nuget.exe 推送套件。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>適用於 Windows Phone 工具 Mango Edition 的支援
NuGet 現在支援 Windows Phone Mango 工具發行候選版本中。
目前，Windows Phone 工具並沒有 Visual Studio 擴充功能管理員，因此，若要安裝 Windows Phone 工具的 NuGet 支援，您可能需要下載並手動執行 VSIX。

若要解除安裝 NuGet for Windows Phone 工具，請執行下列命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.4 有工作項目固定為 88 總計。 這些 71 已標示為錯誤。

如需完整的工作清單項目固定在 NuGet 1.4，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的錯誤修正：

* [問題 603](http://nuget.codeplex.com/workitem/603)： 跨不同的存放庫的套件相依性時，可以解決正確地指定特定的套件來源。
* [問題 1036年](http://nuget.codeplex.com/workitem/1036)： 新增`NuGet Pack SomeProject.csproj`來建置後事件不會再造成無限迴圈。
* [問題 961](http://nuget.codeplex.com/workitem/961):`-Source`旗標支援相對路徑。

## <a name="nuget-14-update"></a>NuGet 1.4 更新
不久後 NuGet 1.4 的版本中，我們會發現幾個重要修正的問題。
這項更新 1.4 的特定版本號碼是 1.4.20615.9020。

### <a name="bug-fixes"></a>Bug 修正
* [問題 1220年](http://nuget.codeplex.com/workitem/1220)： 不會執行更新套件`install.ps1` / `uninstall.ps1`中有多個專案時的所有專案
* [問題 1156年](http://nuget.codeplex.com/workitem/1156): W2K3/XP 上 （未安裝 Powershell 第 2） 時停滯的套件管理員主控台
