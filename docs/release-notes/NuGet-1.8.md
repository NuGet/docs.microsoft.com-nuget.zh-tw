---
title: NuGet 1.8 版本資訊
description: NuGet 1.8 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9d55534ffe765137731b7fbf4be4bbaa618c769c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236829"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 版本資訊

[NuGet 1.7 版本](../release-notes/nuget-1.7.md)  |  資訊[NuGet 2.0 版本](../release-notes/nuget-2.0.md)資訊

NuGet 1.8 發行于2012年5月23日。

## <a name="known-installation-issue"></a>已知的安裝問題
如果您執行的是 VS 2010 SP1，如果您已安裝較舊的版本，可能會在嘗試升級 NuGet 時發生安裝錯誤。

解決方法是直接卸載 NuGet，然後從 VS 延伸模組資源庫安裝它。  <https://support.microsoft.com/kb/2581019>如需詳細資訊，請參閱，或[直接移至 VS 修正程式](http://bit.ly/vsixcertfix)。

注意：如果 Visual Studio 不允許您卸載擴充功能 () 停用 [卸載] 按鈕，那麼您可能需要使用 [以系統管理員身分執行] 來重新開機 Visual Studio。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 與 Windows XP 不相容，已發行的修正程式

在發行 NuGet 1.8 之後不久，我們瞭解1.8 中的密碼編譯變更在 Windows XP 中斷。

我們已發行可解決此問題的修正程式。  藉由透過 Visual Studio 擴充功能庫更新 NuGet，您會收到此修正程式。

## <a name="features"></a>功能

### <a name="satellite-packages-for-localized-resources"></a>當地語系化資源的附屬套件
NuGet 1.8 現在支援針對當地語系化的資源建立個別套件的功能，類似于 .NET Framework 的附屬元件功能。  附屬套件的建立方式與任何其他 NuGet 套件的方式相同，另外還有幾個慣例：

* 附屬套件識別碼和檔案名應包含符合 .NET Framework 所使用的其中一個標準文化特性 [字串](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)的尾碼。
* 在其檔案中 `.nuspec` ，附屬套件應使用識別碼中所使用的相同文化特性字串來定義語言元素
* 附屬套件應該在其核心封裝的檔案中定義相依性 `.nuspec` ，而這只是識別碼減去語言尾碼的套件。  您必須在存放庫中提供核心套件，才能成功安裝。

若要安裝具有當地語系化資源的套件，開發人員可從存放庫明確地選取當地語系化的封裝。 目前，NuGet 資源庫不會對附屬套件提供任何一種特殊處理方式。

![具有當地語系化套件的套件管理員對話方塊](./media/dlg-w-loc-packs.png)

由於附屬套件會列出其核心套件的相依性，因此會將附屬和核心套件提取到 NuGet 套件資料夾並安裝。

![具有當地語系化套件的封裝資料夾](./media/fldr-loc-packs.png)

此外，在安裝附屬套件時，NuGet 也會辨識文化特性字串命名慣例，然後將當地語系化的資源元件複製到核心封裝內的正確子資料夾，以便 .NET Framework 加以挑選。

![包含已複製資源資料夾的核心封裝資料夾](./media/fldr-copied-loc.png)

使用附屬套件時要注意的一個現有 bug 是，NuGet 不會將當地語系化的資源複製到 `bin` 網站專案的資料夾中。  下一版的 NuGet 將會修正此問題。

如需示範如何建立和使用附屬套件的完整範例，請參閱 [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) 。

### <a name="package-restore-consent"></a>封裝還原同意
在 NuGet 1.8 中，我們奠定了在套件還原上支援重要條件約束以保護使用者隱私權的基礎。 此條件約束需要開發人員建立使用套件還原的專案和方案，以明確同意封裝還原上線，以便從設定的套件來源下載套件。

有兩種方式可以提供此同意。 第一個可在 [套件管理員設定] 對話方塊中找到，如下所示。  這個方法主要適用于開發人員電腦。

![套件管理員設定對話方塊](./media/pr-consent-configdlg.png)

第二種方法是將環境變數 "EnableNuGetPackageRestore" 設定為 "true" 值。  此方法適用于自動機器，例如 CI 或組建伺服器。

如上所述，我們僅針對 NuGet 1.8 中的這項功能奠定基礎。  實際上，這表示，雖然我們已新增所有邏輯來啟用此功能，但目前並不會在此版本中強制執行。 不過，它將會在下一版的 NuGet 中啟用，因此我們想要儘快讓您知道它的設定，以便您可以適當地設定環境，因此當我們開始強制執行同意條件約束時，就不會受到影響。

如需詳細資訊，請參閱這項功能的 [小組 blog 文章](http://blog.nuget.org/20120518/package-restore-and-consent.html) 。

### <a name="nugetexe-performance-improvements"></a>nuget.exe 效能改進
藉由修改 install 命令，以平行方式下載並安裝套件，NuGet 1.8 對 nuget.exe 以及延伸模組套件還原帶來大幅的效能改進。  高階測試顯示將6個套件安裝至專案的效能，可透過 NuGet 1.8 中的35% 來改善。  將套件數目增加至25會顯示大約60% 的效能提升。

## <a name="bug-fixes"></a>錯誤修正
NuGet 1.8 包含許多 bug 修正，並著重于套件管理員主控台和套件還原工作流程，特別是與套件還原同意和 Windows 8 快速整合有關。
如需 NuGet 1.8 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。