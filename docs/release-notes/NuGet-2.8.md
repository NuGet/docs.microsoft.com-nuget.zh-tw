---
title: NuGet 2.8 版本資訊
description: NuGet 2.8 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237011"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 版本資訊

[NuGet 2.7.2 版本](../release-notes/nuget-2.7.2.md)  |  資訊[NuGet 2.8.1 版本](../release-notes/nuget-2.8.1.md)資訊

NuGet 2.8 發行于2014年1月29日。

## <a name="acknowledgements"></a>通知

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie)) 
    - [#3466](https://nuget.codeplex.com/workitem/3466) -封裝封裝時，驗證相依性套件的識別碼。
2. [聖馬丁 Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw)) 
    - [#2379](https://nuget.codeplex.com/workitem/2379) -在 persistening 摘要認證時移除 $metadata 尾碼。
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks)) 
    - [#3538](http://nuget.codeplex.com/workitem/3538) -支援指定 nuget.exe update 命令的專案檔。
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -不以-IncludeReferencedProjects 傳遞的取代權杖。
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave)) 
    - [#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget。推送大型封裝時，推送擲回 OutOfMemoryException。
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -當專案參考另一個 CLI/c + + 專案時，修正不正確的目標路徑。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph)) 
    - [#3639](https://nuget.codeplex.com/workitem/3639) -預設允許將套件安裝為開發相依性
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl)) 
    - [#3717](https://nuget.codeplex.com/workitem/3717) -移除最新修補程式版本的隱含升級
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - NuGet. Server、nuget.exe 鏡像命令及其他專案的數個 bug 修正和改進。
    - 這項工作已在數個月內完成，且 Gregory 與我們合作，以正確的時機將其整合至2.8 的主要主機。

## <a name="patch-resolution-for-dependencies"></a>相依性的修補程式解析

在解析套件相依性時，NuGet 過去已實行一項策略，以選取符合套件相依性的最低主要和次要套件版本。 不過，與主要和次要版本不同的是，修補程式版本一律會解析為最高版本。 雖然行為的因為善意很好，但卻建立了不具決定性的方式來安裝具有相依性的套件。 請考慮下列範例：

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

在此範例中，即使安裝了 Developer1 和 Developer2 PackageA@1.0.0 ，每個都有不同的 PackageB 版本。 NuGet 2.8 會變更此預設行為，使修補程式版本的相依性解析行為與主要和次要版本的行為一致。 在上述範例中， PackageB@1.0.0 會安裝為安裝的結果， PackageA@1.0.0 而不考慮較新的修補程式版本。

## <a name="-dependencyversion-switch"></a>-DependencyVersion 參數

雖然 NuGet 2.8 變更瞭解析相依性的 _預設_ 行為，但也可透過套件管理員主控台中的-DependencyVersion 參數，更精確地控制相依性解析程式。 交換器可將相依性解析為最可能的版本 (預設行為) 、可能的最高版本，或是最高的次要或修補程式版本。  此參數只適用于 powershell 命令中的安裝套件。

![DependencyVersion 參數](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 屬性

除了上述的-DependencyVersion 參數之外，NuGet 也可讓您在定義預設值的 Nuget.Config 檔案中設定新屬性的功能，如果未在安裝套件的調用中指定-DependencyVersion 參數，則為。 任何安裝套件作業的 NuGet 封裝管理員對話方塊也會遵守此值。 若要設定此值，請將下列屬性新增至您的 Nuget.Config 檔案：

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>使用-whatif 預覽 NuGet 作業

有些 NuGet 套件可以有深度的相依性圖形，因此在安裝、卸載或更新作業期間，可能會有説明，以先查看將會發生什麼事。 NuGet 2.8 將標準的 PowerShell-whatif 交換器新增至安裝套件、卸載套件和更新套件命令，以啟用將套用命令的整個封裝的整個關閉。 例如， `install-package Microsoft.AspNet.WebApi -whatif` 在空白 ASP.NET Web 應用程式中執行時，會產生下列各項。

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

## <a name="downgrade-package"></a>降級套件

安裝發行前版本的套件，以調查新功能，然後決定復原到最後一個穩定版本並不常見。 在 NuGet 2.8 之前，這是一個多步驟的程式，可將發行前版本套件及其相依性卸載，然後再安裝較早的版本。 不過，使用 NuGet 2.8 時，更新套件現在將會回復整個封裝結束 (例如封裝的相依性樹狀結構) 至先前的版本。

## <a name="development-dependencies"></a>開發相依性

許多不同類型的功能都可以當做 NuGet 套件提供，包括用來將開發程式優化的工具。 這些元件在開發新封裝時，不應視為新封裝的相依性（當它稍後發佈時）。 NuGet 2.8 可讓套件以 developmentDependency 的形式將本身識別為檔案 `.nuspec` 。 安裝此中繼資料時，也會將此中繼資料加入至 `packages.config` 已安裝封裝的專案檔案中。 當該檔案 `packages.config` 稍後在中分析 NuGet 相依性時 `nuget.exe pack` ，將會排除標示為開發相依性的相依性。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>不同平臺的個別 packages.config 檔案

開發多個目標平臺的應用程式時，每個個別的組建環境通常會有不同的專案檔。 在不同的專案檔中使用不同的 NuGet 套件也是很常見的，因為套件具有不同平臺的不同層級支援。 NuGet 2.8 針對不同的平臺專屬專案檔建立不同的檔案，為此案例提供了更好的支援 `packages.config` 。

![多個 package.config 檔案](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>回到本機快取

雖然 NuGet 套件通常是從使用網路連線 [的「nuget](http://www.nuget.org/) 資源庫」之類的遠端資源庫取用，但在許多情況下，用戶端並未連線。 如果沒有網路連線，NuGet 用戶端就無法成功安裝套件，即使這些套件已在用戶端電腦上的本機 NuGet 快取中。 NuGet 2.8 會將自動快取回復新增至套件管理員主控台。 例如，中斷網路介面卡的連線並安裝 jQuery 時，主控台會顯示下列各項：

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

快取回復功能不需要任何特定的命令引數。 此外，快取回復目前只能在套件管理員主控台中運作-在 [封裝管理員] 對話方塊中，行為目前無法運作。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 用戶端更新

除了 NuGet 2.8，WebMatrix 的 NuGet 延伸模組也已更新，以包含 [nuget 2.5](../release-notes/nuget-2.5.md)提供的許多主要功能。 新功能包括「全部更新」、「最小 NuGet 版本」等功能，並允許覆寫內容檔。

若要更新 WebMatrix 3 中的 NuGet 封裝管理員延伸模組：

1. 開啟 WebMatrix 3
1. 按一下功能區中的延伸模組圖示
1. 選取 [更新] 索引標籤
1. 按一下以將 NuGet 封裝管理員更新為2.5。0
1. 關閉並重新啟動 WebMatrix 3

這是 NuGet 團隊首次發行版本的 NuGet 封裝管理員延伸模組。  Microsoft 最近將程式碼提供給開放原始碼 NuGet 專案。 先前，NuGet 整合已內建在 WebMatrix 中，無法從 WebMatrix 更新。  我們現在可以將它與 NuGet 用戶端工具的其餘部分一起更新。

## <a name="bug-fixes"></a>錯誤修正

更新套件-重新安裝命令的效能改進是所做的其中一個重大錯誤修正。

除了這些功能和上述的效能修正之外，此版本的 NuGet 也包含許多其他 bug 修正。 發行中已解決的問題總數為181。 如需 NuGet 2.8 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。
