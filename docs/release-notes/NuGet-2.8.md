---
title: NuGet 2.8 版本資訊
description: NuGet 2.8 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429049"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 版本資訊

[Nuget 2.7.2 版本](../release-notes/nuget-2.7.2.md)資訊 | [nuget 2.8.1 版本](../release-notes/nuget-2.8.1.md)資訊

NuGet 2.8 已于2014年1月29日發行。

## <a name="acknowledgements"></a>致謝

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) （[@leppie](https://twitter.com/leppie)）
    - [#3466](https://nuget.codeplex.com/workitem/3466) -封裝套件時，驗證相依性套件的識別碼。
2. [聖馬丁 Balliauw](https://www.codeplex.com/site/users/view/maartenba) （[@maartenballiauw](https://twitter.com/maartenballiauw)）
    - [#2379](https://nuget.codeplex.com/workitem/2379) -在 persistening 摘要認證時移除 $metadata 尾碼。
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) （[@foxtricks](https://twitter.com/foxtricks)）
    - [#3538](http://nuget.codeplex.com/workitem/3538) -支援指定 nuget.exe update 命令的專案檔。
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - 未隨-IncludeReferencedProjects 傳遞的[#3536](http://nuget.codeplex.com/workitem/3536)取代權杖。
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) （[@Sarkie_Dave](https://twitter.com/Sarkie_Dave)）
    - [#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget。推送大型套件時，發送擲回 OutOfMemoryException。
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -當專案參考另一個 CLI/C++專案時，修正不正確的目標路徑。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) （[@adamralph](https://twitter.com/adamralph)）
    - [#3639](https://nuget.codeplex.com/workitem/3639) -允許依預設將套件安裝為開發相依性
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) （[@davidfowl](https://twitter.com/davidfowl)）
    - [#3717](https://nuget.codeplex.com/workitem/3717) -移除對最新修補程式版本的隱含升級
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - NuGet. 伺服器、nuget.exe 鏡像命令及其他專案的數個 bug 修正和改善。
    - 這項工作已在數個月內完成，Gregory 與我們合作，以在適當的時機與我們整合到2.8 的主機。

## <a name="patch-resolution-for-dependencies"></a>相依性的修補程式解析

在解析套件相依性時，NuGet 過去已實行一種策略來選取符合封裝相依性的最低主要和次要套件版本。 但與主要和次要版本不同的是，修補程式版本一律會解析為最高版本。 雖然此行為是因為善意的，但它卻建立了安裝具有相依性之套件的不確定性。 請考慮下列範例：

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

在此範例中，即使已 PackageA@1.0.0安裝 Developer1 和 Developer2，每個都是以不同版本的 PackageB 來結束。 NuGet 2.8 會變更此預設行為，讓修補程式版本的相依性解析行為與主要和次要版本的行為一致。 在上述範例中，PackageB@1.0.0 會因為安裝 PackageA@1.0.0而安裝，而不論較新的修補程式版本為何。

## <a name="-dependencyversion-switch"></a>-DependencyVersion 參數

雖然 NuGet 2.8 會變更解析相依性的_預設_行為，但它也會透過套件管理員主控台中的-DependencyVersion 參數，更精確地控制相依性解析程式。 參數可讓您將相依性解析成最低可能版本（預設行為）、可能的最高版本，或最高的次要或修補程式版本。  此交換器僅適用于 powershell 命令中的安裝套件。

![DependencyVersion 參數](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 屬性

除了上面詳述的-DependencyVersion 參數外，NuGet 也可以在定義預設值的 Nuget.exe 檔案中設定新屬性（如果未在的調用中指定-DependencyVersion 參數）。install-package。 [NuGet 套件管理員] 對話方塊也會遵循此值，進行任何安裝封裝作業。 若要設定此值，請將下列屬性新增至您的 Nuget .Config 檔案：

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>使用-whatif 預覽 NuGet 作業

某些 NuGet 套件可以有深度相依性圖形，因此在安裝、卸載或更新作業時，可能會先瞭解會發生什麼事。 NuGet 2.8 將標準 PowerShell-whatif 參數新增至安裝套件、卸載套件和更新套件命令，以視覺化方式將套用命令的整個套件關閉。 例如，在空白 ASP.NET Web 應用程式中執行 `install-package Microsoft.AspNet.WebApi -whatif` 會產生下列結果。

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>降級封裝

安裝套件的搶鮮版，以調查新功能，然後決定復原到最後一個穩定版本，並不是很常見的情況。 在 NuGet 2.8 之前，這是卸載發行前版本套件及其相依性，然後再安裝舊版的多步驟程式。 不過，使用 NuGet 2.8，更新套件現在會將整個套件關閉（例如套件的相依性樹狀結構）復原到先前的版本。

## <a name="development-dependencies"></a>開發相依性

許多不同類型的功能可以做為 NuGet 套件提供，包括用來優化開發程式的工具。 這些元件雖然可能有助於開發新的套件，但在稍後發行時，不應將其視為新封裝的相依性。 NuGet 2.8 可讓套件在 `.nuspec` 檔案中將其本身識別為 developmentDependency。 安裝時，此中繼資料也會加入至已安裝封裝之專案的 `packages.config` 檔案。 稍後在 `nuget.exe pack`中分析 NuGet 相依性的 `packages.config` 檔案時，將會排除標示為開發相依性的相依性。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>不同平臺的個別封裝 .config 檔案

開發多個目標平臺的應用程式時，每個個別的組建環境都有不同的專案檔案。 在不同的專案檔中使用不同的 NuGet 套件也很常見，因為套件具有不同平臺的各種支援層級。 NuGet 2.8 為不同平臺特定的專案檔建立不同的 `packages.config` 檔案，為此案例提供了更好的支援。

![多個 package .config 檔案](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>回到本機快取

雖然 NuGet 套件通常是從使用網路連線的遠端資源庫（例如[nuget 資源庫](http://www.nuget.org/)）取用，但在許多情況下，用戶端並未連接。 如果沒有網路連線，NuGet 用戶端就無法成功安裝套件，即使這些套件已經在本機 NuGet 快取的用戶端電腦上也一樣。 NuGet 2.8 會將自動快取回溯新增至套件管理員主控台。 例如，當中斷網路介面卡的連線並安裝 jQuery 時，主控台會顯示下列內容：

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

快取回退功能不需要任何特定的命令引數。 此外，快取回退目前僅適用于套件管理員主控台-此行為目前無法在 [套件管理員] 對話方塊中運作。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 用戶端更新

除了 NuGet 2.8，適用于 WebMatrix 的 NuGet 延伸模組也已更新，以包含[nuget 2.5](../release-notes/nuget-2.5.md)提供的許多主要功能。 新功能包括「全部更新」、「最低 NuGet 版本」，並允許覆寫內容檔案。

若要更新 WebMatrix 3 中的 NuGet 套件管理員延伸模組：

1. 開啟 WebMatrix 3
1. 按一下功能區中的 [延伸模組] 圖示
1. 選取 [更新] 索引標籤
1. 按一下以將 NuGet 套件管理員更新為2.5。0
1. 關閉並重新啟動 WebMatrix 3

這是 NuGet 小組第一版的 NuGet 套件管理員延伸模組（適用于 WebMatrix）。  Microsoft 最近將此程式碼提供給開放原始碼 NuGet 專案。 先前，NuGet 整合已內建到 WebMatrix 中，無法從 WebMatrix 升級。  我們現在可以進一步將它與 NuGet 用戶端工具的其餘部分一起更新。

## <a name="bug-fixes"></a>錯誤修正

其中一個主要錯誤修正是在更新-封裝-重新安裝命令中改善效能。

除了這些功能和前述的效能修正之外，這一版的 NuGet 也包含其他許多 bug 修正。 發行中解決了181的總問題。 如需 NuGet 2.8 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。
