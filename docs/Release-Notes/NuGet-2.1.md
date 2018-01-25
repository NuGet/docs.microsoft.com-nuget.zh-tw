---
title: "NuGet 2.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.1 版本資訊。"
keywords: "NuGet 2.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 05cdb898cc674ac7eadb238d41896638d8e3488c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 版本資訊

[NuGet 2.0 版本資訊](../release-notes/nuget-2.0.md) | [NuGet 2.2 版本資訊](../release-notes/nuget-2.2.md)

NuGet 2.1 已於 2012 年 10 月 4 日發行。

## <a name="hierarchical-nugetconfig"></a>階層式 Nuget.Config
NuGet 2.1 可讓您更大的彈性來控制透過以遞迴方式向上尋找的資料夾結構的 NuGet 設定`NuGet.Config`檔案，然後建置組態從所有找到的檔案集。  例如，假設其中團隊具有 CI 組建的其他內部的相依性內部的封裝儲存機制。 個別的專案的資料夾結構看起來可能如下所示：

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

此外，如果方案已啟用封裝還原，也會存在下列資料夾：

    C:\myteam\solution1\.nuget

為了有小組內部的封裝儲存機制適用於所有專案的小組，會在不讓它可供每個專案的電腦上，我們可以建立新的 Nuget.Config 檔案，並將它放在 c:\myteam 資料夾中。 沒有任何方法指定為每個專案的 packages 資料夾。

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

我們現在可以看到的來源已加入執行 'nuget.exe 來源' 命令，從任何資料夾下方 c:\myteam 如下所示：

![從父 nuget 組態的封裝來源](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config`搜尋檔案順序如下：

1. `.nuget\Nuget.Config`
2. 遞迴逐步來自專案資料夾根目錄
3. 全域`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)

組態設定是套用在非*反向順序*，亦即，取決於上述排序，全域 Nuget.Config 就會先套用，後面接著探索到的 Nuget.Config 檔案從根專案資料夾，再由`.nuget\Nuget.Config`。  這是非常重要，如果您使用`<clear/>`項目移除設定的一組項目。

## <a name="specify-packages-folder-location"></a>指定 'packages' 資料夾位置
在過去，NuGet 已找到方案根資料夾下的已知 'packages' 資料夾管理方案套件。  有許多不同的方案具有已安裝的 NuGet 封裝的開發團隊，這會導致在許多不同的地方，在檔案系統上安裝相同的封裝。

NuGet 2.1 提供更細微地控制透過 [packages] 資料夾的位置`repositoryPath`中的項目`NuGet.Config`檔案。  建立階層式 Nuget.Config 支援上述範例，假設我們想要擁有 C:\myteam\ 共用相同的封裝資料夾下的所有專案。  若要這麼做，只要加入下列項目以`c:\myteam\Nuget.Config`。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

在此範例中，共用`Nuget.Config`檔案會指定無論深度 C:\myteam，下方會建立每個專案的封裝共用的資料夾。 請注意，是否您有現有的封裝資料夾方案根目錄下，您必須將它刪除，NuGet 會將封裝放在新位置之前。

## <a name="support-for-portable-libraries"></a>可攜式程式庫支援
[可攜式類別庫](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)是可讓您建置組件，可以不需要修改不同 Microsoft 平台上，從.net Framework Windows Phone 和 Xbox 甚至的 silverlight 版本的.NET 4 第一次引進的功能360 （雖然在此階段中，NuGet 不支援 Xbox 可攜式程式庫目標）。  藉由擴充[封裝慣例](../create-packages/supporting-multiple-target-frameworks.md)framework 版本和設定檔，NuGet 2.1 現在支援可攜式程式庫，讓您建立封裝以將複合架構和設定檔目標`lib`資料夾。

例如，請考慮下列的可攜式類別庫提供的目標平台。

![可攜式程式庫建立對話方塊](./media/releasenotes-21-plib.png)

在建置之程式庫之後和命令`nuget.exe pack MyPortableProject.csproj`執行時，新的可攜式程式庫封裝的資料夾結構看藉由檢查產生的 NuGet 套件的內容。

![可攜式程式庫封裝配置](./media/releasenotes-21-plib-layout.png)

如您所見，可攜式程式庫資料夾名稱慣例遵循模式 '可攜式 {架構 1} + {framework n}' 的 framework 識別項遵循現有[架構名稱和版本慣例](../schema/target-frameworks.md)。 使用適用於 Windows Phone 的 framework 識別項中找到一個例外狀況的名稱和版本的慣例。  這個 moniker，應該使用的架構名稱 'wp' （wp7、 wp71 或 wp8）。 使用 ' silverlight-wp7'，例如，將會導致錯誤。

安裝時所建立從這個資料夾結構的套件，NuGet 可現在其架構和設定檔將規則套用至所指定的資料夾名稱中的多個目標。  後方 NuGet 的比對規則是 「 更特定的 「 目標將會優先 」 較不特定 」 的原則。  這表示，以特定平台為目標的 moniker 會一律透過慣用可攜式電腦如果它們都相容的專案。  此外，如果多個可移植的目標相容的專案，NuGet 會偏好平台支援一組 「 最靠近 」 專案參考封裝所在的一個。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>目標的 Windows 8 和 Windows Phone 8 專案
NuGet 2.1 除了新增目標可攜式程式庫專案的支援，Windows 8 市集和 Windows Phone 8 專案中，以及一些新的一般 moniker 的 Windows 市集和 Windows Phone 專案將會提供新的 framework moniker容易管理整個各自的平台的未來版本。

對於 Windows 8 市集應用程式中，識別項，看起來像這樣：

|2.0 及更早版本的 NuGet|NuGet 2.1|
|----------------|-----------|
|winRT45, .NETCore45|Windows，Windows8，win win8|

<br/>
Windows Phone 專案的識別項，看起來像這樣：

|Phone OS|2.0 及更早版本的 NuGet|NuGet 2.1
|----------------|-----------|-----------|
|Windows Phone 7|silverlight3-wp|wp，wp7，WindowsPhone WindowsPhone7|
|Windows Phone 7.5 (Mango)|silverilght4-wp71|wp71, WindowsPhone71|
|Windows Phone 8|（不支援）|wp8, WindowsPhone8|
<br/>
在所有上述變更，舊的架構名稱會繼續受到完整支援 NuGet 2.1。  起，新的名稱應該使用時，就能更穩定跨各平台的未來版本。 新的名稱會*不*是支援的 NuGet 2.1 之前的版本，不過，因此詳加規劃時，切換。

## <a name="improved-search-in-package-manager-dialog"></a>在封裝管理員 對話方塊中改進的搜尋
過去的數個反覆項目，透過變更已經引進來大幅提升速度及相關性的封裝搜尋在 NuGet gallery。  不過，這些增強功能只限於 nuget.org 的網站。  NuGet 2.1 改進的搜尋體驗可讓透過 [NuGet 封裝管理員] 對話方塊。  例如，假設您想要尋找 Windows Azure 快取預覽封裝。  合理的搜尋查詢，此套件可能是 「 Azure 快取 」。  在舊版的 [封裝管理員] 對話方塊中，所需的封裝會不甚至會列在結果的第一頁。  不過，在 NuGet 2.1 中，所需的套件現在會出現在搜尋結果的頂端。

![封裝管理員對話方塊搜尋](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>強制執行封裝的更新
之前 NuGet 2.1，NuGet 會略過更新封裝時不高的版本號碼。  此導入了人事某些案例 – 特別在建置或 CI 案例，小組不想增加每個組建編號的封裝版本。  所要的行為就是強制更新而定。  NuGet 2.1 可應付此 '重新安裝' 旗標。  例如，舊版的 NuGet 會產生下列時嘗試更新沒有較新的封裝版本的套件：

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

重新安裝旗標，封裝將會更新而不論是否有為較新版本。

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

重新安裝旗標可幫助證明另一種情況就是重新架構為目標。 變更目標 framework 的專案 （例如，從.NET 4 為.NET 4.5)，當更新封裝的重新安裝可以更新所有 NuGet 封裝在專案中安裝正確的組件的參考。

## <a name="edit-package-sources-within-visual-studio"></a>編輯 Visual Studio 中的封裝來源
在舊版的 NuGet 中，更新從套件來源中刪除並重新加入 [封裝來源所需的 Visual Studio 選項] 對話方塊。  NuGet 2.1 支援更新為第一級函式的組態使用者介面，以改善此工作流程。

![封裝管理員的組態對話方塊](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Bug 修正
NuGet 2.1 包含括許多錯誤修正。 如需完整的工作清單項目固定在 NuGet 2.0 中，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
