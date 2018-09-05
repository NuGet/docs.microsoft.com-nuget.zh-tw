---
title: NuGet 2.1 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.1 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548593"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 版本資訊

[NuGet 2.0 版本資訊](../release-notes/nuget-2.0.md) | [NuGet 2.2 版本資訊](../release-notes/nuget-2.2.md)

NuGet 2.1 已於 2012 年 10 月 4 日發行。

## <a name="hierarchical-nugetconfig"></a>階層式 Nuget.Config

NuGet 2.1 可讓您更大的彈性來控制 NuGet 設定，透過以遞迴方式向上瀏覽資料夾結構以尋找`NuGet.Config`檔案，然後再建立 找到的所有檔案組的組態。  例如，假設小組有 CI 組建的其他內部的相依性的內部套件存放庫的位置。 個別專案的資料夾結構看起來可能如下所示：

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

此外，如果方案已啟用套件還原，也會存在下列資料夾：

    C:\myteam\solution1\.nuget

為了有小組的內部套件存放庫可供所有專案的小組處理，而不讓它可用於每個專案的電腦上，我們可以建立新的 Nuget.Config 檔案，並將它放在 c:\myteam 資料夾中。 沒有任何方法指定為每個專案的 packages 資料夾。

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

我們現在可以看到來源已執行 「 nuget.exe 來源 」 命令，從任何資料夾下方 c:\myteam，如下所示：

![從父 nuget 組態的封裝來源](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 搜尋檔案順序如下：

1. `.nuget\Nuget.Config`
2. 遞迴逐步從專案資料夾根
3. 全域`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)

設定是套用在非*反向順序*，表示要根據上述的順序，全域的 Nuget.Config 就會先套用，後面接著探索到的 Nuget.Config 檔案從根專案資料夾，再接著藉由`.nuget\Nuget.Config`。  這是特別重要，如果您使用`<clear/>`從設定中移除的項目集的項目。

## <a name="specify-packages-folder-location"></a>指定 [套件] 資料夾位置

在過去，NuGet 已管理解決方案的根資料夾下的一個已知的 [套件] 資料夾的方案套件。  有許多不同的解決方案具有已安裝的 NuGet 套件的開發小組，這會導致相同的封裝中許多不同的位置，在檔案系統上安裝。

NuGet 2.1 提供更細微地控制透過 [packages] 資料夾的位置`repositoryPath`中的項目`NuGet.Config`檔案。  為建置基礎的階層式 Nuget.Config 支援上例，假設我們想要有 C:\myteam\ 共用相同的封裝資料夾下的所有專案。  若要達成此目的，只是下列項目新增至`c:\myteam\Nuget.Config`。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

在此範例中，共用`Nuget.Config`檔案會指定無論深度 C:\myteam，下方會建立每個專案共用的 packages 資料夾。 請注意，如果您有現有的 [封裝] 資料夾底下您方案的根目錄時，需要刪除之前 NuGet 會將套件放在新的位置。

## <a name="support-for-portable-libraries"></a>可攜式程式庫的支援

[可攜式程式庫](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)是第一次引進可讓您建置組件，可以不需修改不同的 Microsoft 平台，從舊版.net Framework silverlight Windows Phone 和甚至是 Xbox 上的.NET 4 的功能360 （雖然在此階段中，NuGet 不支援 Xbox 可攜式程式庫目標）。  藉由擴充[封裝慣例](../create-packages/supporting-multiple-target-frameworks.md)framework 版本和設定檔，NuGet 2.1 現在支援可攜式程式庫，可讓您建立複合的架構和設定檔目標的套件`lib`資料夾。

例如，請考慮下列的可攜式類別庫提供的目標平台。

![可攜式程式庫建立對話方塊](./media/releasenotes-21-plib.png)

程式庫建立之後的命令`nuget.exe pack MyPortableProject.csproj`執行時，新的可攜式程式庫封裝的資料夾結構可以藉由檢查產生的 NuGet 套件的內容。

![可攜式程式庫套件配置](./media/releasenotes-21-plib-layout.png)

如您所見，可攜式程式庫資料夾名稱慣例會遵循模式 '可攜式 {架構，1} + {framework n}' 的 framework 識別項遵循現有[架構的名稱和版本的慣例](../reference/target-frameworks.md)。 使用適用於 Windows Phone 的 framework 識別項中找到的名稱和版本的慣例的例外狀況。  這個 moniker 應該使用的架構名稱 'wp' （wp7、 wp71 或 wp8）。 使用 ' silverlight-wp7'，比方說，將會導致錯誤。

安裝時建立此資料夾結構中的封裝，NuGet 現在可以套用其架構和設定檔的規則所指定的資料夾名稱中的多個目標。  後置 NuGet 的比對規則是 「 更特定的 「 目標將會優先"較不特定 」 的原則。  這表示，以在特定平台為目標的 moniker 會一律透過慣用可攜式電腦如果它們都與專案相容。  此外，如果多個可移植的目標是相容的專案，NuGet 會偏好其中組支援的平台是 「 最靠近 」 參考封裝專案。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>目標的 Windows 8 和 Windows Phone 8 專案

NuGet 2.1 除了新增針對可攜式程式庫專案的支援，Windows 8 市集和 Windows Phone 8 專案，以及一些新的一般 moniker，Windows 市集和 Windows Phone 專案將會提供新的 framework moniker若您更輕鬆地在未來的版本，個別的平台的管理。

Windows 8 市集應用程式中，識別碼看起來像這樣：

| 2.0 及更早版本的 NuGet | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows，Windows8，win win8 |

<br/>
Windows Phone 專案識別碼看起來像這樣：

| Phone OS | 2.0 及更早版本的 NuGet | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | wp wp7，w WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71 WindowsPhone71 |
| Windows Phone 8 | （不支援） | wp8 WindowsPhone8 |

<br/>
在所有上述變更，舊的架構名稱仍受到完整支援 NuGet 2.1。  接下來，新的名稱應該使用它們將會更穩定的個別平台的未來版本。 新的名稱將會*不*是支援在 2.1 之前的 NuGet 版本，不過，因此據此進行規劃時若要切換。

## <a name="improved-search-in-package-manager-dialog"></a>在 [套件管理員] 對話方塊中的改進的搜尋

過去的幾個反覆項目，透過已引進的變更至 NuGet 資源庫，大幅提升速度及套件搜尋的相關性。  不過，這些增強功能僅限於 nuget.org 網站。  NuGet 2.1 可讓您可透過 [NuGet 套件管理員] 對話方塊改良的搜尋體驗。  例如，假設您想要尋找 Windows Azure 快取預覽封裝。  此套件的合理的搜尋查詢可能是 「 Azure 快取 」。  在舊版的 [套件管理員] 對話方塊中，所需的套件會不甚至會列在結果的第一頁。  不過，在 NuGet 2.1 中，所需的套件現在會出現在頂端的搜尋結果。

![套件管理員對話方塊中搜尋](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>強制執行封裝的更新

之前 NuGet 2.1，NuGet 會略過更新套件時不高的版本號碼。  這引進了適用於特定案例 – 特別是在組建或 CI 案例，小組不想要遞增套件版本編號，以每個組建的摩擦。  所要的行為是強制更新不論。  NuGet 2.1 可應付這 '重新安裝' 旗標。  比方說，舊版的 NuGet，會導致下列時嘗試更新沒有較新的封裝版本的套件：

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

重新安裝旗標，將更新的套件不論是否有較新版本。

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

重新安裝旗標可幫助證明的另一個案例是 framework 重新目標。 變更 （例如，從.NET 4 中為.NET 4.5)，專案的目標 framework 時 Update-package-重新安裝可更新所有的 NuGet 套件安裝在專案的正確的組件的參考。

## <a name="edit-package-sources-within-visual-studio"></a>編輯 Visual Studio 內的套件來源

在舊版的 NuGet 中，更新從套件來源，在 Visual Studio 選項對話方塊中所需刪除並重新加入 套件來源。  NuGet 2.1 支援更新為第一級函式的組態使用者介面改善這個工作流程。

![套件管理員 設定對話方塊](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Bug 修正

NuGet 2.1 還包含括許多錯誤修正。 如需完整的工作清單項目中已修正 NuGet 2.0，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
