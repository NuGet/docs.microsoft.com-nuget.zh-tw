---
title: NuGet 2.8 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.8 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547455"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 版本資訊

[NuGet 2.7.2 版本資訊](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md)

NuGet 2.8 已於 2014 年 1 月 29 日發行。

## <a name="acknowledgements"></a>謝誌

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) -當封裝套件，驗證相依性套件的識別碼。
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [# 2379年](https://nuget.codeplex.com/workitem/2379)-persistening 摘要認證時，移除 $metadata 後置詞。
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) -指定專案檔的 nuget.exe 更新命令的支援。
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) --IncludeReferencedProjects 與失敗的取代權杖。
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 推送大型封裝時，擲回 OutOfMemoryException。
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -專案參考另一個的 CLI/c + + 專案時，修正不正確的目標路徑。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -允許依預設，做為開發相依性安裝封裝
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -移除隱含升級至最新的修補程式版本
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - 數個 bug 修正和改善的 NuGet.Server、 nuget.exe 鏡像命令和其他項目。
    - 這項工作已完成幾個月，Gregory 正確的時機與我們合作，將整合到 2.8 的主要。

## <a name="patch-resolution-for-dependencies"></a>修補程式解決相依性

當解析套件相依性，NuGet 已在過去實作選取最低的主要和次要封裝版本符合封裝上的相依性的策略。 不同於主要和次要版本，不過，修補程式版本已一律解決的最高版本。 行為是用意良好，但它會建立決定性具有相依性安裝套件的缺乏。 參考下列範例：

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

在此範例中，即使 Developer1 和 Developer2 安裝PackageA@1.0.0、 每個結束向上 PackageB 的不同版本。 NuGet 2.8 會變更此預設行為，因此修補程式版本的相依性解析行為會與主要和次要版本的行為一致。 在上述範例中，然後PackageB@1.0.0由於安裝會安裝PackageA@1.0.0，而不論較新的修補程式版本。

## <a name="-dependencyversion-switch"></a>-DependencyVersion 參數

雖然變更 NuGet 2.8_預設_行為解析相依性，它也會加入更精確地控制相依性解析程序-DependencyVersion 參數透過套件管理員主控台中。 參數可讓您解析的相依性，以最低的可能版本 （預設行為）、 最高的可能版本，或最高次要或修補程式版本。  此參數僅適用於安裝套件中的 powershell 命令。

![DependencyVersion 參數](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 屬性

除了以上詳述，NuGet 也可讓提供的能力的 Nuget.Config 檔案中設定新的屬性-DependencyVersion 參數定義的預設值為何，如果未指定-DependencyVersion 參數中的引動過程安裝套件。 此值也會遵守任何安裝封裝作業的 [NuGet 套件管理員] 對話方塊。 若要設定此值，請先 Nuget.Config 檔案中加入以下屬性：

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>預覽 NuGet 作業，與-whatif

部分 NuGet 套件可以有深入的相依性圖形，而此情況下，它可以在安裝期間會有幫助、 解除安裝或更新作業，先查看 會發生什麼事。 NuGet 2.8 會將標準的 PowerShell-whatif 參數新增至安裝套件、 解除安裝套件和更新套件的命令，來啟用視覺化整個 closure 的封裝將會套用命令。 例如，執行`install-package Microsoft.AspNet.WebApi -whatif`在空的 ASP.NET Web 應用程式會產生下列結果。

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

不常見安裝套件的發行前版本，以便調查的新功能，但後來回復到最新穩定版本。 NuGet 2.8 以前這會是多重步驟的程序解除安裝發行前版本套件和其相依性，然後安裝 先前的版本。 使用 NuGet 2.8，不過，更新套件現在會回復整個封裝結束 （例如套件的相依性樹狀結構） 到之前的版本。

## <a name="development-dependencies"></a>開發相依性

許多不同類型的功能可能會傳送為 NuGet 套件-包括用來最佳化開發過程的工具。 這些元件，雖然也很有幫助開發新封裝時，不應視為新的封裝相依性更新版本發行時。 NuGet 2.8 可讓封裝本身中識別`.nuspec`為 developmentDependency 的檔案。 安裝時，此中繼資料也會加入至`packages.config`封裝已安裝所在的專案檔案。 時， `packages.config` NuGet 相依性期間稍後分析檔案`nuget.exe pack`，它會排除這些標示為開發相依性的相依性。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>適用於不同平台的個別 packages.config 檔案

在開發用於多個目標平台的應用程式時，常會每個個別的建置環境有不同的專案檔。 它也很常見使用不同的 NuGet 封裝，在不同的專案檔中，因為套件會有各種不同平台的支援層級。 NuGet 2.8 可改進支援此案例藉由建立不同`packages.config`不同的平台專屬專案檔的檔案。

![多個 package.config 檔案](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>切換回本機快取

雖然 NuGet 套件通常都是從遠端資源庫這類[在 NuGet gallery](http://www.nuget.org/)使用網路連線，有許多用戶端未連接的案例。 沒有網路連線，NuGet 用戶端無法成功安裝封裝-，即使這些套件已在本機 NuGet 快取的用戶端的電腦上。 NuGet 2.8 會將套件管理員主控台中的自動後援的快取。 比方說，當中斷連線的網路介面卡，並安裝 jQuery、 在主控台顯示下列資訊：

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

快取後援功能不需要任何特定的命令列引數。 此外，快取後援目前只適用於套件管理員主控台-行為目前不適用於 [套件管理員] 對話方塊。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 用戶端更新

NuGet 2.8 以及 WebMatrix 的 NuGet 擴充功能也已更新為包含的許多主要的功能隨附於[NuGet 2.5](../release-notes/nuget-2.5.md)。 新功能包括例如 '更新 All'、' 最低 NuGet 版本 ' 和允許的內容檔案的覆寫。

若要更新您在 WebMatrix 3 中的 NuGet 套件管理員延伸模組：

1. 開啟 WebMatrix 3
1. 按一下功能區中的延伸模組圖示
1. 選取 [更新] 索引標籤
1. 按一下以更新 2.5.0 NuGet 套件管理員
1. 關閉並重新啟動 WebMatrix 3

這是 NuGet 小組的第一版的 NuGet 套件管理員延伸模組 WebMatrix。  Microsoft 最近被提供程式碼到開放原始碼 NuGet 專案。 先前，NuGet 整合內建在 WebMatrix 中，並無法更新超出訊號範圍從 WebMatrix。  我們現在有可進一步與 NuGet 的用戶端工具的其餘部分一起更新它的功能。

## <a name="bug-fixes"></a>Bug 修正

其中一個所做的重大錯誤修正已更新套件中的效能改進-重新安裝命令。

除了這些功能和修正上述的效能，這一版的 NuGet 也會包含其他許多 bug 修正。 發生在版本中解決的 181 總問題。 如需完整的工作清單項目中已修正 NuGet 2.8，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。
