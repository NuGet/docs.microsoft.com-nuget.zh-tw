---
title: NuGet 1.8 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.8 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546617"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 的版本資訊

[NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md) | [NuGet 2.0 版本資訊](../release-notes/nuget-2.0.md)

NuGet 1.8 已於 2012 5 月 23 日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行的 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您已安裝較舊版本。

因應措施是只解除安裝 NuGet，然後再從 VS 延伸模組資源庫進行安裝。  請參閱[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)如需詳細資訊，或[直接前往 VS hotfix](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕已停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 相容 Windows xp 中，發行的 hotfix

NuGet 1.8 發行不久之後，我們已了解 1.8 的密碼編譯變更中斷使用者，在 Windows XP 上。

我們因為已發行 hotfix 來解決此問題。  藉由更新透過 Visual Studio 延伸模組組件庫的 NuGet，您會收到此 hotfix。

## <a name="features"></a>功能

### <a name="satellite-packages-for-localized-resources"></a>當地語系化資源的附屬套件
NuGet 1.8 現在支援建立個別的封裝，如需當地語系化的資源，類似於.NET Framework 的附屬組件功能的能力。  附屬套件會在相同的方式，加上一些慣例的任何其他 NuGet 套件的形式建立：

* 附屬套件識別碼和檔案名稱應包含符合標準的其中一個尾碼[文化特性 .NET Framework 所使用字串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。
* 在其`.nuspec`檔案，附屬套件應該定義語言項目具有相同識別碼使用的文化特性字串
* 附屬套件應該定義中的相依性及其`.nuspec`其核心封裝，也就是只要使用相同的識別碼，減去語言字尾封裝的檔案。  核心封裝必須可成功安裝的儲存機制中。

若要將套件安裝當地語系化的資源，開發人員明確選取當地語系化的套件儲存機制中。 目前，NuGet 資源庫不會提供任何一種特殊處理，就可以附屬套件。

![使用當地語系化 pacakges 套件管理員 對話方塊](./media/dlg-w-loc-packs.png)

附屬套件列出其核心封裝的相依性，因為在附屬和核心套件會提取至 NuGet 套件資料夾，並安裝。

![封裝資料夾中，使用當地語系化的套件](./media/fldr-loc-packs.png)

此外，在安裝附屬套件，NuGet 也會辨識的文化特性的字串命名慣例，然後將當地語系化的資源組件複製到核心封裝內的正確子資料夾，以便它可以挑選由.NET Framework。

![核心封裝資料夾中，使用複製的資源資料夾](./media/fldr-copied-loc.png)

一個現有的 bug，要特別注意的附屬套件是 NuGet 不會複製至的當地語系化的資源`bin`適用於網站專案的資料夾。  在 NuGet 的下一個版本中，將會修正此問題。

如需示範如何建立和使用附屬套件的完整範例，請參閱 < [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample)。

### <a name="package-restore-consent"></a>套件還原同意
在 NuGet 1.8 中，我們打造出支援套件還原以保護使用者隱私權的一個重要限制。 此條件約束需要開發人員在建置專案和方案明確地同意套件還原用套件還原的上線設定的套件來源下載套件。

有 2 種方式可提供此同意。 第一個可在 [套件管理員設定] 對話方塊，如下所示。  這個方法主要是供開發人員電腦。

![套件管理員 設定對話方塊](./media/pr-consent-configdlg.png)

第二種方法是將環境變數"EnableNuGetPackageRestore 」 設為值"true"。  這個方法適用於無人看管的電腦，例如 CI 或組建伺服器。

現在，如上所述，我們有只打造出這項功能在 NuGet 1.8。  實際上，這表示，雖然我們已新增所有的邏輯，以啟用功能，它目前未強制執行在此版本。 將會啟用，不過，在下一個版本的 NuGet，因此我們想要讓您知道它儘速，以便您可以適當地設定您的環境，並因此不會影響我們啟動時強制使用同意條件約束。

如需詳細資訊，請參閱[小組部落格文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)這項功能。

### <a name="nugetexe-performance-improvements"></a>nuget.exe 的效能改進
藉由修改安裝命令，下載及並行安裝套件，NuGet 1.8 會提供大幅的效能增強功能 nuget.exe-to 和 by 延伸模組套件還原。  高的層級測試顯示為 6 的套件安裝至專案的效能改善在 NuGet 1.8 約 35%。  增加到 25 的套件數目，顯示約 60%的效能提高。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.8 會包含相當多的 bug 修正，並強調的套件管理員主控台和套件還原工作流程，特別是與封裝還原同意與 Windows 8 Express 整合。
如需完整的工作清單項目中已修正 NuGet 1.8，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
