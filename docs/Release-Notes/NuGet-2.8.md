---
title: "NuGet 2.8 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 77ba98d8-3d66-4126-b2b6-813ddd8ef192
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.8 的版本資訊。"
keywords: "NuGet 2.8 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 182e7d1e2224c431631cddd14fdbea8dd9e14278
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 版本資訊

[NuGet 2.7.2 版本資訊](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md)

NuGet 2.8 已於 2014 年 1 月 29 日發行。

## <a name="acknowledgements"></a>謝誌

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) -當壓縮封裝，驗證相依性套件的識別碼。
1. [馬頓 Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [# 2379年](https://nuget.codeplex.com/workitem/2379)-persistening 摘要認證時，移除 $metadata 後置詞。
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) -指定 nuget.exe 更新命令的專案檔的支援。
1. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -不會隨-IncludeReferencedProjects 取代語彙基元。
1. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 推入大型封裝時，擲回 OutOfMemoryException。
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -修正不正確的目標路徑的專案參考另一個 CLI/c + + 專案時。
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -允許依預設，做為開發相依性安裝的封裝
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -移除隱含升級至最新修補程式版本
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - 數個 bug 修正和增強功能 NuGet.Server、 nuget.exe 鏡像命令，以及其他等等。
    - 這項工作已完成 Gregory 我們努力右計時整合 2.8 主機幾個月。

## <a name="patch-resolution-for-dependencies"></a>修補程式解析的相依性

當解析封裝相依性，NuGet 在過去已實作選取最低的主要和次要的封裝版本能符合封裝上的相依性的策略。 不同於主要和次要版本中，不過，修補程式的版本是一定要解析為最高的版本。 雖然行為是本意良好，但，它會建立缺乏決定性具有相依性安裝封裝。 參考下列範例：

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

在此範例中，即使 Developer1 Developer2 安裝和PackageA@1.0.0、 每個結束向上 PackageB 的不同版本。 NuGet 2.8 變更此預設行為的修補程式版本的相依性解析行為是使用主要和次要版本的行為一致。 在上述範例中，然後PackageB@1.0.0會安裝安裝PackageA@1.0.0，不論修補程式的較新版本。

## <a name="-dependencyversion-switch"></a>-DependencyVersion 交換器

雖然 NuGet 2.8 變更_預設_行為對於解析相依項，它也會加入相依性解析程序，透過-DependencyVersion 交換器的更精確地控制封裝管理員主控台中。 參數可讓解析的相依性，以最低的可能版本 （預設行為），可能最高的版本，或最高次要或修補程式的版本。  這個參數僅適用於安裝套件中的 powershell 命令。

![DependencyVersion 交換器](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 屬性

除了以上詳述，能夠有也允許 NuGet 在 Nuget.Config 檔案中設定新的屬性-DependencyVersion 參數定義的預設值為何，如果未指定-DependencyVersion 交換器中的引動過程安裝套件。 這個值也會遵守任何安裝封裝作業的 [NuGet 套件管理員] 對話方塊。 若要設定此值，請先 Nuget.Config 檔案中加入以下屬性：

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>預覽 NuGet 作業與-whatif

部分 NuGet 封裝可以有深入的相依性圖形，而在這種情況，它可以在安裝期間會有幫助、 解除安裝或更新作業來第一次看到 會發生什麼事。 NuGet 2.8 將標準的 PowerShell-whatif 參數新增至安裝套件、 解除安裝套件和更新套件的命令，以啟用視覺化的封裝命令將套用的整個終止。 例如，執行`install-package Microsoft.AspNet.WebApi -whatif`空的 ASP.NET Web 應用程式會產生下列。

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

不常見的安裝套件的發行前版本，以便調查新的功能，然後決定要回復到最後一個穩定版本。 NuGet 2.8 之前，這是多重步驟的程序解除安裝發行前版本的封裝和其相依性，然後安裝較舊版本。 使用 NuGet 2.8，不過，更新套件現在會回復整個封裝封閉區段 （例如封裝的相依性樹狀目錄） 到之前的版本。

## <a name="development-dependencies"></a>開發相依性

許多不同類型的功能可以傳遞做為 NuGet 套件-包括用來最佳化開發程序的工具。 這些元件，雖然可以很有幫助開發新的封裝，而不應視為新的封裝的相依性更新版本發行時。 NuGet 2.8 可讓封裝本身中識別`.nuspec`developmentDependency 檔案。 安裝時，此中繼資料也會以新增`packages.config`到其中安裝封裝的專案檔。 時， `packages.config` NuGet 相依性，在稍後分析檔案`nuget.exe pack`，其中會排除標記為開發相依性的相依性。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>不同的平台的個別 packages.config 檔案

開發應用程式為多個目標平台，時，通常會有不同的專案檔的每個個別的建置環境。 它通常也可以使用不同的專案檔中的不同 NuGet 套件封裝有各種不同平台的支援層級。 NuGet 2.8 提供改善的支援此案例藉由建立不同`packages.config`不同的平台專屬專案檔的檔案。

![多個 package.config 檔案](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>後援至本機快取

雖然 NuGet 封裝通常使用從遠端組件庫例如[在 NuGet gallery](http://www.nuget.org/)使用網路連線，有許多用戶端無法連線的案例。 如果沒有網路連接，NuGet 用戶端無法成功安裝封裝-即使這些封裝工作已在本機的 NuGet 快取的用戶端電腦上。 NuGet 2.8 會將後援自動快取加入至封裝管理員主控台。 例如，當中斷連線的網路介面卡，安裝 jQuery 主控台顯示下列資訊：

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

快取後援功能不需要任何特定的命令列引數。 此外，後援的快取目前只適用於封裝管理員主控台-行為目前不適用於 [封裝管理員] 對話方塊。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 用戶端更新

NuGet 2.8 以及 for WebMatrix NuGet 延伸模組也已更新成包含許多傳遞時的主要功能[NuGet 2.5](../release-notes/nuget-2.5.md)。 新功能包括例如 '更新 All'、' 最低 NuGet 版本 ' 和允許的內容檔案的覆寫。

若要更新您在 WebMatrix 3 的 NuGet 套件管理員擴充功能：

1. 開啟 WebMatrix 3
1. 按一下功能區中的擴充功能圖示
1. 選取 [更新] 索引標籤
1. 按一下以更新 2.5.0 NuGet 封裝管理員
1. 關閉並重新啟動 WebMatrix 3

這是 NuGet 小組的第一版 NuGet 套件管理員擴充 WebMatrix。  Microsoft 最近已造成程式碼到 NuGet 開放原始碼專案。 先前，NuGet integration 已內建 WebMatrix，並且無法更新頻外方式從 WebMatrix。  我們現在有以進一步 NuGet 的用戶端工具的其餘部分一起更新它的功能。

## <a name="bug-fixes"></a>Bug 修正

有一個主要的 bug 修正進行已更新套件中的效能改進層重新安裝命令。

除了這些功能與前述效能修正程式，這個版本的 NuGet 也包含許多其他 bug 修正。 有一些版本中解決的 181 總問題。 如需完整清單的工作項目中修正 NuGet 2.8，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。
