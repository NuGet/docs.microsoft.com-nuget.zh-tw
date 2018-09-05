---
title: NuGet 2.7.2 版本資訊
description: 版本資訊 NuGet 2.7.2 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550066"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 版本資訊

[NuGet 2.7.1 版本資訊](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md)

NuGet 2.7.2 已於 2013 年 11 月 11 日發行。

## <a name="noteworthy-bug-fixes-and-features"></a>值得注意的錯誤修正和功能

### <a name="license-text"></a>授權文字
好一段時間，Microsoft 已在 Visual Studio 中包含數個熱門的開放原始碼程式庫的 Web 應用程式專案的預設範本一部分的 NuGet 套件。 jQuery 可能是眾所皆知的這種類型的程式庫範例。 因為傳遞以及產品的元件相關聯的支援協議的情況下，封裝的指令碼檔案會包含比公用 nuget.org 資源庫上找到的相同封裝中的指令碼檔案的不同授權文字。 在文字中的這項差異可以避免繼續進行，因為造成有不同的內容雜湊值的指令碼檔案的不同授權文字區塊的套件更新 （也因此被視為在專案中修改）。

若要解決這個問題，NuGet 2.7.2 可讓指令碼作者包括授權文字區塊，這看起來像這樣的特殊標記區段內。

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

更新內容套件時檔案包含這個區塊中，NuGet 不會不納入與 NuGet 資源庫上的版本比較區塊的內容和可以因此刪除和更新內容檔案，就好像它會比對的原始複本。

識別此區塊文字 「 NUGET:: BEGIN 授權文字 」 和 「 NUGET:: END 授權文字 」 發生任何一處開始和結束行。  沒有其他格式的需求存在時，它會允許在任何類型的文字檔案，不論語言為何要使用這項功能。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>新增繫結重新導向的非 Framework 組件
對於屬於.NET Framework 的組件，NuGet 會略過新增繫結重新導向至應用程式的組態檔更新套件時。 此修正位址的迴歸，藉此繫結重新導向不新增針對某些組件，即使這些組件不是 NuGet 2.7 中視為.NET Framework 的一部分。 NuGet 2.7.2 還原先前的 NuGet 2.5 和 2.6 的行為，並新增繫結重新導向。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>使用已安裝 Xamarin 工具來安裝可攜式程式庫
當在機器上安裝 Xamarin 的開發工具時，它們會修改支援的架構的組態資料，以指定現有的目標架構組合和 Xamarin 架構之間的相容性。 2.7.2 的版本，NuGet 會知道這些隱含的相容性規則，並因此可方便 Xamarin 平台為目標的開發人員套件中，因此安裝與 Xamarin 相容，但未明確標示的可攜式程式庫中繼資料本身。

### <a name="machine-wide-configuration-settings-honored"></a>接受的整部電腦的組態設定
使用階層式 Nuget.Config 檔案時，repositoryPath 金鑰未被接受的最接近方案根目錄的 Nuget.Config 檔案。 在 Visual Studio 2013 中，NuGet 會安裝自訂 Nuget.Config 檔於 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config，才能夠加入 「 Microsoft 和.NET 」 套件來源。 如此一來，因應措施在解決方案中使用自訂的 repositoryPath 已刪除的電腦層級 Nuget.Config-這也意味著移除 「 Microsoft 和.NET 」 套件來源。 使用階層式 Nuget.Config 檔案時，NuGet 2.7.2 現在會接受 repositoryPath 的優先順序規則。

## <a name="all-changes"></a>所有的變更
如需完整的工作清單項目中已修正 NuGet 2.7.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。
