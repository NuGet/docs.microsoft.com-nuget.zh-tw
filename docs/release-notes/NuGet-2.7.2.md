---
title: NuGet 2.7.2 版本資訊
description: NuGet 2.7.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776779"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 版本資訊

[NuGet 2.7.1 版本](../release-notes/nuget-2.7.1.md)  |  資訊[NuGet 2.8 版本](../release-notes/nuget-2.8.md)資訊

NuGet 2.7.2 已于2013年11月11日發行。

## <a name="noteworthy-bug-fixes-and-features"></a>值得注意的錯誤修正和功能

### <a name="license-text"></a>授權文字
Microsoft 針對 Visual Studio 中的 Web 應用程式專案的預設範本，包含了數個常用的開放原始碼程式庫的 NuGet 套件。 jQuery 可能是這種程式庫類型最知名的範例。 由於與產品一起傳遞的元件相關聯的支援合約，封裝的腳本檔案所含的授權文字，與公用 nuget.org 資源庫上相同套件中找到的指令檔不同。 這項文字差異可以防止套件更新因為不同的授權文字區塊而無法繼續，而導致腳本檔案 (不同的內容雜湊值，因此在專案) 內視為已修改。

為了減輕這個問題，NuGet 2.7.2 允許腳本作者在特別標示的區段內包含授權文字區塊，如下所示。

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

當使用包含此區塊的內容檔案來更新套件時，NuGet 不會將區塊的內容視為與 NuGet 資源庫上的版本進行比較，因此可以刪除和更新內容檔案，就好像它符合原始複本一樣。

此區塊是由文字「NUGET：開始授權文字」和「NUGET：結束授權文字」所識別，並在開頭和結尾行的任何位置發生。  不存在任何其他格式化需求，不論語言為何，都可以在任何類型的文字檔中使用這項功能。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>新增非架構元件的系結重新導向
針對屬於 .NET Framework 一部分的元件，NuGet 會在更新套件時，略過將系結重新導向新增至應用程式的設定檔。 這項修正可解決 NuGet 2.7 中的回歸，因為某些元件不會加入系結重新導向，即使這些元件不會被視為 .NET Framework 的一部分也一樣。 NuGet 2.7.2 會還原先前的 NuGet 2.5 和2.6 行為，並新增系結重新導向。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>安裝已安裝 Xamarin 工具的便攜程式庫
當 Xamarin 的開發工具安裝在電腦上時，它們會修改支援的架構設定資料，以指定現有目標 framework 組合和 Xamarin framework 之間的相容性。 使用版本2.7.2 時，NuGet 現在知道這些隱含相容性規則，因此可讓開發人員輕鬆地以 Xamarin 平臺為目標，以安裝 Xamarin 相容但未明確標示為套件中繼資料本身的便攜程式庫。

### <a name="machine-wide-configuration-settings-honored"></a>接受全電腦的設定
使用階層式 Nuget.Config 檔案時，不會針對最接近解決方案根目錄的 Nuget.Config 檔案接受 repositoryPath 金鑰。 在 Visual Studio 2013 中，NuGet 會在% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config 安裝自訂 Nuget.Config 檔案，以新增 "Microsoft 和 .NET" 套件來源。 因此，在解決方案中使用自訂 repositoryPath 的解決方法是刪除電腦層級的 Nuget.Config，也就是移除「Microsoft 和 .NET」套件來源。 在使用階層式 Nuget.Config 檔案時，NuGet 2.7.2 現在接受 repositoryPath 的優先順序規則。

## <a name="all-changes"></a>所有變更
如需 NuGet 2.7.2 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。
