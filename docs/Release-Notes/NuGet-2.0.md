---
title: "NuGet 2.0 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.0 的版本資訊。"
keywords: "NuGet 2.0 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 版本資訊

[NuGet 1.8 版本資訊](../release-notes/nuget-1.8.md) | [NuGet 2.1 版本資訊](../release-notes/nuget-2.1.md)

NuGet 2.0 已於 2012 年 6 月 19 日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您正在執行 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您有安裝較舊的版本。

因應措施是只要解除安裝 NuGet，然後再從 VS 擴充功能庫進行安裝。  請參閱[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)如需詳細資訊，或[直接前往 VS hotfix](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕會停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。

## <a name="package-restore-consent-is-now-active"></a>封裝還原同意目前為作用中

中所述[格上的封裝還原同意](http://blog.nuget.org/20120518/package-restore-and-consent.html)，NuGet 2.0 現在會要求同意，有啟用上線並下載封裝的封裝還原。 請確認您提供同意透過封裝管理員的組態對話方塊或 EnableNuGetPackageRestore 環境變數。

## <a name="group-dependencies-by-target-frameworks"></a>群組的目標架構的相依性

從 2.0 版開始，封裝相依性可能會不同 framework 設定檔為基礎的目標專案。 這利用更新完成`.nuspec`結構描述。 `<dependencies>`項目現在可包含一組`<group>`項目。 每個群組包含零或多個`<dependency>`項目和`targetFramework`屬性。 如果目標 framework 與不相容的目標專案 framework 設定檔時，會同時安裝在群組內的所有相依性。 例如: 

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

請注意，一個群組可以包含**零**相依性。 在上述範例中，如果封裝安裝到專案為目標的 Silverlight 3.0 或更新版本，將會安裝沒有相依性。 如果封裝被安裝到專案的目標.NET 4.0 或更新版本，將會安裝兩個相依性、 jQuery 和 WebActivator。  如果套件安裝到這些 2 的架構或任何其他架構的最早的版本為目標的專案，將會安裝 RouteMagic 1.1.0。 群組之間沒有任何繼承。 如果專案的目標 framework 符合`targetFramework`將安裝的群組時，只有該群組內的相依性屬性。

封裝可以指定在兩種格式之一的封裝相依性： 一份舊有格式`<dependency>`項目或群組。 如果`<group>`格式，則無法安裝封裝在 2.0 之前的 NuGet 版本。

請注意，不允許混用兩種格式。 例如，下列程式碼片段是**無效**並且會拒絕 nuget。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>群組內容的檔案和 PowerShell 指令碼的目標 framework

除了組件參考，內容檔案與 PowerShell 指令碼可以也被分組目標架構。 相同的資料夾結構中找到`lib`指定目標架構的資料夾現在可套用至相同的方式`content`和`tools`資料夾。 例如: 

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

**請注意**： 因為`init.ps1`方案層級執行，且不相依於任何個別的專案，必須將它置正下方`tools`資料夾。 如果放在架構特定的資料夾內，將會忽略它。

此外，NuGet 2.0 中的新功能是 framework 資料夾可以是*空*，在此情況下，NuGet 會不加入組件參考、 加入內容的檔案或執行特定的架構版本的 PowerShell 指令碼。 在上述資料夾範例`content\net40`是空的。

## <a name="improved-tab-completion-performance"></a>改善的索引標籤完成的效能
Tab 鍵自動完成功能，NuGet 封裝管理員主控台中的已更新為大幅改善效能。 會有更少延遲，直到出現建議下拉式清單中，按下 tab 鍵的時間。

## <a name="bug-fixes"></a>Bug 修正
NuGet 2.0 包含封裝還原同意和效能，特別強調括許多錯誤修正。
如需完整的工作清單項目固定在 NuGet 2.0 中，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
