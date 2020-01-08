---
title: NuGet 2.0 版本資訊
description: NuGet 2.0 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383063"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 版本資訊

[Nuget 1.8 版本](../release-notes/nuget-1.8.md)資訊 | [nuget 2.1 版本](../release-notes/nuget-2.1.md)資訊

NuGet 2.0 已于2012年6月19日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行 VS 2010 SP1，如果您已安裝舊版，則嘗試升級 NuGet 時可能會發生安裝錯誤。

因應措施是直接卸載 NuGet，然後從 VS 延伸模組資源庫進行安裝。  如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>，或[直接移至 VS 提供程式](http://bit.ly/vsixcertfix)。

注意：如果 Visual Studio 不允許您卸載擴充功能（[卸載] 按鈕已停用），您可能需要使用 [以系統管理員身分執行] 重新開機 Visual Studio。

## <a name="package-restore-consent-is-now-active"></a>套件還原同意現已啟用

如這[篇關於封裝還原同意文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)中所述，NuGet 2.0 現在需要授與同意，才能讓套件還原上線並下載套件。 請確定您已透過 [套件管理員設定] 對話方塊或 EnableNuGetPackageRestore 環境變數提供同意。

## <a name="group-dependencies-by-target-frameworks"></a>依目標 framework 群組相依性

從2.0 版開始，封裝相依性可能會根據目標專案的 framework 設定檔而有所不同。 這項作業是使用已更新的 `.nuspec` 架構來完成。 `<dependencies>` 元素現在可以包含一組 `<group>` 元素。 每個群組都包含零個或多個 `<dependency>` 元素和一個 `targetFramework` 屬性。 如果目標 framework 與目標專案架構設定檔相容，則會同時安裝群組內的所有相依性。 例如：

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

請注意，群組可以包含**零個**相依性。 在上述範例中，如果將套件安裝到以 Silverlight 3.0 或更新版本為目標的專案中，則不會安裝任何相依性。 如果將封裝安裝到以 .NET 4.0 或更新版本為目標的專案中，將會安裝兩個相依性（jQuery 和 WebActivator）。  如果將封裝安裝到以這兩個架構的早期版本為目標的專案中，或任何其他架構，則會安裝 RouteMagic 1.1.0。 群組之間沒有任何繼承。 如果專案的目標 framework 符合群組的 `targetFramework` 屬性，則只會安裝該群組中的相依性。

封裝可以使用兩種格式的其中一種來指定封裝相依性： `<dependency>` 專案或群組之一般清單的舊格式。 如果使用 `<group>` 格式，套件就無法安裝在2.0 之前的 NuGet 版本中。

請注意，不允許混用這兩種格式。 例如，下列程式碼片段**無效**，NuGet 將會拒絕。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>依目標架構將內容檔案和 PowerShell 腳本分組

除了元件參考之外，也可以依目標 framework 將內容檔案和 PowerShell 腳本分組。 在用來指定目標 framework 的 `lib` 資料夾中找到的相同資料夾結構，現在可以用相同方式套用至 `content` 和 `tools` 資料夾。 例如：

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

**注意**：因為 `init.ps1` 是在方案層級執行，而且不相依于任何個別專案，所以必須直接放在 `tools` 資料夾底下。 如果放在架構特定的資料夾內，則會忽略它。

此外，NuGet 2.0 中的一項新功能是，架構資料夾可以是*空*的，在這種情況下，nuget 將不會新增元件參考、新增內容檔案或針對特定架構版本執行 PowerShell 腳本。 在上述範例中，`content\net40` 的資料夾是空的。

## <a name="improved-tab-completion-performance"></a>改良的 tab 鍵自動完成效能
NuGet 套件管理員主控台中的 tab 鍵自動完成功能已更新，可大幅改善效能。 按下 tab 鍵，直到出現 [建議] 下拉式清單時，才會有更少的延遲。

## <a name="bug-fixes"></a>Bug 修正
NuGet 2.0 包含許多 bug 修正，並著重于封裝還原同意和效能。
如需 NuGet 2.0 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
