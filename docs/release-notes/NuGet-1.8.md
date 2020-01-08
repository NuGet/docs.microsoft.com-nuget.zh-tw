---
title: NuGet 1.8 版本資訊
description: NuGet 1.8 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 973a2d010cb75eeeb383be94baf2fb17a999dd7c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383457"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 版本資訊

[Nuget 1.7 版本](../release-notes/nuget-1.7.md)資訊 | [nuget 2.0 版本](../release-notes/nuget-2.0.md)資訊

NuGet 1.8 已于2012年5月23日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行 VS 2010 SP1，如果您已安裝舊版，則嘗試升級 NuGet 時可能會發生安裝錯誤。

因應措施是直接卸載 NuGet，然後從 VS 延伸模組資源庫進行安裝。  如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>，或[直接移至 VS 提供程式](http://bit.ly/vsixcertfix)。

注意：如果 Visual Studio 不允許您卸載擴充功能（[卸載] 按鈕已停用），您可能需要使用 [以系統管理員身分執行] 重新開機 Visual Studio。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 與 Windows XP 不相容，已發行的修補程式

在 NuGet 1.8 發行後不久，我們已瞭解1.8 中的密碼編譯變更會中斷 Windows XP 上的使用者。

我們已發行解決此問題的修正程式。  藉由 Visual Studio 延伸模組資源庫來更新 NuGet，您會收到此修補程式。

## <a name="features"></a>功能

### <a name="satellite-packages-for-localized-resources"></a>當地語系化資源的附屬套件
NuGet 1.8 現在支援針對當地語系化的資源建立個別的封裝，類似于 .NET Framework 的附屬元件功能。  附屬套件的建立方式與任何其他 NuGet 套件相同，並加入幾個慣例：

* 附屬套件識別碼和檔案名應包含尾碼，以符合 .NET Framework 所使用的其中一個標準[文化特性字串](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。
* 在它的 `.nuspec` 檔案中，附屬套件應使用識別碼中所用的相同文化特性字串來定義語言元素。
* 附屬套件應定義其 `.nuspec` 檔案中的相依性至其核心套件，這只是識別碼減去語言尾碼的套件。  核心套件必須在存放庫中提供，才能成功安裝。

若要安裝具有當地語系化資源的套件，開發人員會從存放庫明確選取當地語系化的封裝。 目前，NuGet 資源庫不會對附屬套件提供任何一種特殊的處理方式。

![具有當地語系化套件的 [套件管理員] 對話方塊](./media/dlg-w-loc-packs.png)

因為附屬套件會列出其核心套件的相依性，所以附屬和核心套件都會提取至 NuGet 套件資料夾並安裝。

![具有當地語系化套件的封裝資料夾](./media/fldr-loc-packs.png)

此外，在安裝附屬套件時，NuGet 也會辨識文化特性字串命名慣例，然後將當地語系化的資源元件複製到核心套件中正確的子資料夾，以供 .NET Framework 挑選。

![已複製資源資料夾的核心封裝資料夾](./media/fldr-copied-loc.png)

要注意的附屬套件有一個現有的錯誤，就是 NuGet 不會將當地語系化的資源複製到網站專案的 `bin` 資料夾。  此問題將在下一版的 NuGet 中修正。

如需示範如何建立和使用附屬套件的完整範例，請參閱[https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)。

### <a name="package-restore-consent"></a>套件還原同意
在 NuGet 1.8 中，我們已為支援封裝還原的重要條件約束奠定基礎，以保護使用者隱私權。 此條件約束需要開發人員建立專案和解決方案，使用套件還原來明確同意封裝還原上線，以從設定的套件來源下載套件。

有2種方式可提供這種同意。 第一個可在 [套件管理員設定] 對話方塊中找到，如下所示。  這個方法主要是供開發人員機器。

![[套件管理員設定] 對話方塊](./media/pr-consent-configdlg.png)

第二種方法是將環境變數 "EnableNuGetPackageRestore" 設定為值 "true"。  此方法適用于自動機器，例如 CI 或組建伺服器。

如先前所述，我們只在 NuGet 1.8 中為這項功能奠定了基礎。  實際上，這表示雖然我們已新增所有邏輯來啟用此功能，但目前並不會在此版本中強制執行。 不過，它會在下一版的 NuGet 中啟用，因此我們想要讓您儘快知道它，以便您可以適當地設定環境，並在我們開始強制執行同意條件約束時不會受到影響。

如需詳細資訊，請參閱這項功能的[小組博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)。

### <a name="nugetexe-performance-improvements"></a>nuget.exe 效能改進
藉由修改 install 命令來以平行方式下載和安裝套件，NuGet 1.8 針對 nuget.exe –和擴充套件還原帶來了顯著的效能改進。  高階測試顯示將6個套件安裝到專案中的效能，在 NuGet 1.8 中可改善大約35%。  將封裝數目增加為25會顯示大約60% 的效能提升。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.8 包含很多 bug 修正，著重于套件管理員主控台和套件還原工作流程，特別是與套件還原同意和 Windows 8 Express 整合相關。
如需 NuGet 1.8 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
