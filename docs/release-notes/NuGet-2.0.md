---
title: NuGet 2.0 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.0 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547571"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 版本資訊

[NuGet 1.8 版本資訊](../release-notes/nuget-1.8.md) | [NuGet 2.1 版本資訊](../release-notes/nuget-2.1.md)

NuGet 2.0 已於 2012 年 6 月 19 日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行的 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您已安裝較舊版本。

因應措施是只解除安裝 NuGet，然後再從 VS 延伸模組資源庫進行安裝。  請參閱[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)如需詳細資訊，或[直接前往 VS hotfix](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕已停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。

## <a name="package-restore-consent-is-now-active"></a>套件還原同意目前為作用中

在此所述[將張貼在套件還原同意](http://blog.nuget.org/20120518/package-restore-and-consent.html)，NuGet 2.0 現在會要求同意要提供給啟用套件還原回到線上，並下載套件。 請確定您已提供同意透過套件管理員的組態對話方塊中或 EnableNuGetPackageRestore 環境變數。

## <a name="group-dependencies-by-target-frameworks"></a>依目標架構的群組相依性

從 2.0 版開始，相依性可能會不同的封裝會根據目標專案的 framework 設定檔。 這利用更新完成`.nuspec`結構描述。 `<dependencies>`項目現在可包含一組`<group>`項目。 每個群組包含零或多個`<dependency>`項目和`targetFramework`屬性。 如果目標架構與目標專案的 framework 設定檔相容時，會同時安裝在群組內的所有相依性。 例如: 

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

請注意，群組可以包含**零**相依性。 在上述範例中，如果封裝會安裝至專案目標 Silverlight 3.0 或更新版本，會不安裝任何相依性。 如果封裝被安裝至專案目標.NET 4.0 或更新版本，將會安裝兩個相依性，jQuery 和 WebActivator。  如果封裝已安裝至這些 2 的架構或任何其他架構的最早的版本為目標的專案中，將會安裝 RouteMagic 1.1.0。 群組之間沒有任何繼承。 如果專案的目標架構符合`targetFramework`群組，只有該群組內的相依性屬性將會安裝。

封裝可以指定兩種格式之一的封裝相依性： 舊格式的一般清單的`<dependency>`項目或群組。 如果`<group>`格式時，無法安裝此套件，NuGet 的版本早於 2.0。

請注意，不允許混用兩種格式。 例如，下列程式碼片段是**無效**和 nuget 將會遭到拒絕。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>群組的內容檔案和 PowerShell 指令碼，以依目標架構

除了組件參考，內容檔案和 PowerShell 指令碼可以也會依目標 framework。 相同的資料夾結構中找到`lib`資料夾，用於指定目標 framework 現在可套用至相同的方式`content`和`tools`資料夾。 例如: 

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**附註**： 因為`init.ps1`方案層級執行，且不相依於任何個別的專案，它必須放在正下方`tools`資料夾。 如果用來放置架構特有資料夾內，將會忽略它。

此外，NuGet 2.0 中的新功能是可以在架構資料夾*空*，在此情況下，NuGet 不會新增組件參考、 加入內容的檔案或執行特定的 framework 版本的 PowerShell 指令碼。 在範例中，資料夾`content\net40`是空的。

## <a name="improved-tab-completion-performance"></a>改善的索引標籤完成效能
已更新 NuGet 套件管理員主控台中的索引標籤完成功能以大幅改善效能。 會從建議下拉式清單中出現之前按下 tab 鍵的時間少很多延遲。

## <a name="bug-fixes"></a>Bug 修正
NuGet 2.0 包含套件還原同意和效能，特別強調的許多錯誤修正。
如需完整的工作清單項目中已修正 NuGet 2.0，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
