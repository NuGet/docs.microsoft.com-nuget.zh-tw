---
title: NuGet 2.1 版本資訊
description: NuGet 2.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777033"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 版本資訊

[NuGet 2.0 版本](../release-notes/nuget-2.0.md)  |  資訊[NuGet 2.2 版本](../release-notes/nuget-2.2.md)資訊

NuGet 2.1 發行于2012年10月4日。

## <a name="hierarchical-nugetconfig"></a>階層式 Nuget.Config

NuGet 2.1 透過以遞迴方式流覽資料夾結構來尋找檔案 `NuGet.Config` ，然後從所有找到的檔案集中建立設定，讓您更有彈性地控制 NuGet 設定。  例如，假設某個小組具有其他內部相依性 CI 組建的內部套件存放庫。 個別專案的資料夾結構看起來可能如下所示：

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

此外，如果解決方案已啟用套件還原，下列資料夾也將存在：

```
C:\myteam\solution1\.nuget
```

若要讓小組的內部封裝存放庫可供小組使用的所有專案使用，但無法將它提供給電腦上的每個專案，我們可以建立新的 Nuget.Config 檔，並將它放在 c:\myteam 資料夾中。 沒有任何方法可指定每個專案的封裝資料夾。

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

現在，我們可以從 c:\myteam 下的任何資料夾執行 ' nuget.exe source ' 命令，以查看已新增來源，如下所示：

![從父 nuget 設定封裝來源](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 系統會以下列順序搜尋檔案：

1. `.nuget\Nuget.Config`
2. 從專案資料夾到根的遞迴逐步解說
3. 全域 `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`) 

這些設定會以 *相反順序* 套用，也就是說，根據上述順序，全域 Nuget.Config 會先套用，接著會先套用從根到專案資料夾的探索 Nuget.Config 檔案，接著是 `.nuget\Nuget.Config` 。  如果您要使用 `<clear/>` 元素從設定中移除一組專案，這點特別重要。

## <a name="specify-packages-folder-location"></a>指定 [套件] 資料夾位置

在過去，NuGet 已從方案根資料夾底下的已知「套件」資料夾管理解決方案的套件。  針對有許多不同方案已安裝 NuGet 套件的開發小組，這可能會導致在檔案系統上的許多不同位置中安裝相同的套件。

NuGet 2.1 透過檔案中的專案，讓您更精確地控制套件資料夾的位置 `repositoryPath` `NuGet.Config` 。  以階層式 Nuget.Config 支援的先前範例為基礎，假設我們想要讓 C:\myteam\ 下的所有專案共用相同的封裝資料夾。  若要完成這項工作，只要將下列專案加入至 `c:\myteam\Nuget.Config` 。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

在此範例中，共用檔案 `Nuget.Config` 會針對在 C:\myteam 底下建立的每個專案（不論深度）指定共用封裝資料夾。 請注意，如果您的解決方案根目錄底下有現有的套件資料夾，您必須先將其刪除，NuGet 才會將套件放在新的位置。

## <a name="support-for-portable-libraries"></a>支援可移植程式庫

[便攜程式庫](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 是 .net 4 首次引進的功能，可讓您建立可在不同的 Microsoft 平臺上執行的元件，從 the.NET Framework 的版本到 Silverlight，再 Windows Phone 甚至是 Xbox 360 (但目前 NuGet 並不支援 Xbox 便攜程式庫目標) 。  藉由擴充 framework 版本和設定檔的 [套件慣例](../create-packages/supporting-multiple-target-frameworks.md) ，NuGet 2.1 現在可讓您建立具有複合架構和設定檔目的檔案夾的封裝，藉此支援便攜程式庫 `lib` 。

例如，請考慮下列可移植類別庫的可用目標平臺。

![便攜程式庫建立對話方塊](./media/releasenotes-21-plib.png)

建立程式庫並執行命令之後 `nuget.exe pack MyPortableProject.csproj` ，您可以藉由檢查所產生 NuGet 套件的內容，來查看新的便攜程式庫套件資料夾結構。

![便攜程式庫套件配置](./media/releasenotes-21-plib-layout.png)

如您所見，便攜程式庫資料夾名稱慣例遵循模式 ' 便攜-{framework 1} + {framework n} '，其中的 framework 識別碼遵循現有的 [framework 名稱和版本慣例](../reference/target-frameworks.md)。 名稱和版本慣例有一個例外狀況，可在用於 Windows Phone 的 framework 識別碼中找到。  這個標記應使用架構名稱 ' wp ' (wp7、wp71 或 wp8) 。 例如，使用 ' silverlight-wp7 ' 將會產生錯誤。

安裝從此資料夾結構建立的封裝時，NuGet 現在可以將其架構和設定檔規則套用至多個目標，如資料夾名稱中所指定。  NuGet 比對規則背後的原則是「更明確的」目標優先于「較不明確」的目標。  這表示，如果以特定平臺為目標的名字，將一律優先于可移植的專案（如果它們兩者都與專案相容）。  此外，如果有多個可移植目標與某個專案相容，則 NuGet 會偏好一組支援的平臺「最接近」至參考封裝的專案。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>以 Windows 8 和 Windows Phone 8 專案為目標

除了新增以可移植程式庫專案為目標的支援之外，NuGet 2.1 還為 Windows 8 存放區和 Windows Phone 8 專案提供了新的架構名字，以及一些新的 Windows Store 和 Windows Phone 專案的一般名字標記，可讓您更輕鬆地在各平臺的未來版本中進行管理。

針對 Windows 8 存放區應用程式，識別碼看起來如下：

| NuGet 2.0 及更早版本 | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows、Windows8、win、win8 |

<br/>
針對 Windows Phone 專案，識別碼看起來會如下所示：

| 電話作業系統 | NuGet 2.0 及更早版本 | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | wp、wp7、WindowsPhone、WindowsPhone7 |
| Windows Phone 7.5 (Mango)  | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (不支援) | wp8、WindowsPhone8 |

<br/>
在上述所有變更中，NuGet 2.1 將繼續完整支援舊的架構名稱。  接下來，您應該使用新的名稱，因為它們在個別平臺的未來版本中將會更穩定。 不過，在2.1 之前的 NuGet 版本中將 *不* 支援新的名稱，因此請視需要規劃何時進行切換。

## <a name="improved-search-in-package-manager-dialog"></a>改善封裝管理員對話方塊中的搜尋

在過去幾個反復專案中，已引進 NuGet 資源庫的變更，以大幅提升封裝搜尋的速度和相關性。  不過，這些改良功能僅限於 nuget.org 網站。  NuGet 2.1 透過 [NuGet 套件管理員] 對話方塊，讓您獲得改良的搜尋體驗。  例如，假設您想要尋找 Windows Azure Caching Preview 套件。  此套件的合理搜尋查詢可能是「Azure 快取」。  在舊版的 [套件管理員] 對話方塊中，所需的套件甚至不會列在結果的第一頁。  不過，在 NuGet 2.1 中，所需的套件現在會顯示在搜尋結果的頂端。

![套件管理員對話方塊搜尋](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>強制更新套件

在 NuGet 2.1 之前，如果沒有較高的版本號碼，NuGet 會略過更新套件。  這對某些案例引進了一些衝突，特別是在組建或 CI 案例中，小組不想要將套件版本號碼與每個組建遞增。  所需的行為是強制進行更新，而不是。  NuGet 2.1 使用「重新安裝」旗標解決此情況。  例如，當您嘗試更新的套件版本不是較新的套件時，舊版的 NuGet 會導致下列情況：

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

使用 [重新安裝] 旗標時，無論是否有較新的版本，套件都會更新。

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

重新安裝旗標的另一個案例，是架構重新設為目標。 當您變更專案的目標 framework 時 (例如，從 .NET 4 到 .NET 4.5) ，Update-Package-重新安裝可以針對在專案中安裝的所有 NuGet 套件，更新正確元件的參考。

## <a name="edit-package-sources-within-visual-studio"></a>在 Visual Studio 中編輯套件來源

在舊版的 NuGet 中，從 [Visual Studio 選項] 對話方塊內更新套件來源需要刪除並重新加入套件來源。  NuGet 2.1 藉由支援 update 做為設定使用者介面的第一個類別功能，來改善此工作流程。

![套件管理員設定對話方塊](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Bug 修正

NuGet 2.1 包含許多 bug 修正。 如需 NuGet 2.0 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
