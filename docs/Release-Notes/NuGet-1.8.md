---
title: NuGet 1.8 版本資訊 |Microsoft 文件
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.8 的版本資訊。
keywords: NuGet 1.8 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b94382f79143cac6bd5deccb5e5253ba8c6f60ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 版本資訊

[NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md) | [NuGet 2.0 版本資訊](../release-notes/nuget-2.0.md)

NuGet 1.8 已於 2012 月 23 日發行。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您正在執行 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您有安裝較舊的版本。

因應措施是只要解除安裝 NuGet，然後再從 VS 擴充功能庫進行安裝。  請參閱[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)如需詳細資訊，或[直接前往 VS hotfix](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕會停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 相容 Windows XP 中，發行的 hotfix

NuGet 1.8 很快發行之後，我們所了解密碼編譯中的變更 1.8 中斷使用者，在 Windows XP 上。

我們已因為已發行 hotfix，以解決此問題。  透過更新 Visual Studio 延伸模組組件庫中透過 NuGet，您會收到此 hotfix。

## <a name="features"></a>功能

### <a name="satellite-packages-for-localized-resources"></a>當地語系化資源的附屬項目封裝
NuGet 1.8 現在支援建立個別的封裝，當地語系化的資源，類似於.NET Framework 的附屬組件功能的能力。  加上一些慣例的任何其他 NuGet 封裝為相同的方式建立附屬項目封裝：

* 附屬項目封裝識別碼和檔案名稱應該包含符合其中一個標準的後置詞[文化特性使用的.NET Framework 字串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。
* 在其`.nuspec`檔案，附屬封裝應該定義語言項目具有相同識別碼中使用的文化特性字串
* 附屬項目封裝應該定義中的相依性及其`.nuspec`核心封裝，也就是減去語言尾碼相同的識別碼與封裝的檔案。  此核心套件必須能夠使用成功安裝的儲存機制中。

若要安裝當地語系化的資源的封裝，開發人員明確選取當地語系化的封裝儲存機制中。 目前，在 NuGet gallery 所提供的任何一種特殊處理，附屬封裝。

![與當地語系化 pacakges 封裝管理員 對話方塊](./media/dlg-w-loc-packs.png)

附屬項目封裝列出其核心封裝的相依性，因為附屬和核心封裝並提取到 [NuGet 封裝] 資料夾，因此安裝。

![當地語系化的封裝與封裝資料夾](./media/fldr-loc-packs.png)

此外，安裝附屬套件，NuGet 也能辨識的文化特性的字串命名慣例，而且，讓它可以由.NET Framework 中選取，然後將當地語系化的資源組件複製到核心封裝內的正確子資料夾。

![核心封裝資料夾與複製的資源資料夾](./media/fldr-copied-loc.png)

要注意與附屬封裝一個現有的 bug 會 NuGet 當地語系化的資源不會複製`bin`適用於網站專案的資料夾。  NuGet 的下一個版本中，將會修正此問題。

如需示範如何建立及使用附屬項目封裝的完整範例，請參閱[ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample)。

### <a name="package-restore-consent"></a>封裝還原同意
在 NuGet 1.8 我們打造支援來保護使用者隱私權的封裝還原的一個重要限制。 此條件約束需要開發人員在建置專案和方案用來明確地同意封裝還原封裝還原的上線從設定的封裝來源下載套件。

有 2 種方式來提供此同意。 第一個位於 [套件管理員設定] 對話方塊如下所示。  這個方法主要是用於開發人員電腦。

![封裝管理員的組態對話方塊](./media/pr-consent-configdlg.png)

第二種方法是將設定環境變數"EnableNuGetPackageRestore"值"true"。  這個方法適用於無人看管的電腦，例如 CI 或組建伺服器。

現在，如上所述，我們已於 NuGet 1.8 中只配置這項功能的基礎。  實際上，這表示，雖然我們新增了所有的邏輯，以啟用功能，它會目前未強制執行此版本中。 會啟用它，不過，在下一個版本的 NuGet，因此我們想要讓您知道它儘速使您可以適當地設定您的環境，並因此不會影響我們啟動時，強制使用同意條件約束。

如需詳細資訊，請參閱[小組部落格文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)這項功能。

### <a name="nugetexe-performance-improvements"></a>nuget.exe 的效能改進
藉由修改安裝命令，以下載並安裝封裝，以平行方式，NuGet 1.8 帶來重大的效能改進 nuget.exe – 和擴充功能封裝還原。  高的層級測試顯示 6 封裝安裝到專案的效能改善大約在 NuGet 1.8 35%。  增加到 25 的套件數目，顯示大約 60%的效能提高。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.8 包含很多 bug 修正，特別強調的封裝管理員主控台和封裝還原工作流程，特別是在關聯於封裝還原同意和 Windows 8 Express 整合。
如需完整的工作清單項目固定在 NuGet 1.8，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
