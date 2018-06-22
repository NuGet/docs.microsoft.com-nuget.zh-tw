---
title: NuGet 2.7.2 版本資訊
description: 版本資訊包含 NuGet 2.7.2 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0cb99e4e1ae9238286dc4fab7b8d34e5b117ed64
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820231"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 版本資訊

[NuGet 2.7.1 版本資訊](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md)

NuGet 2.7.2 已於 2013 年 11 月 11 日發行。

## <a name="noteworthy-bug-fixes-and-features"></a>值得注意的錯誤修正和功能

### <a name="license-text"></a>授權文字
一段時間，Microsoft Visual Studio 中已包含幾個常用的開放原始碼程式庫的 Web 應用程式專案的預設範本一部分的 NuGet 套件。 jQuery 可能是這種類型的文件庫眾所皆知的範例。 支援協議與產品一起傳送的元件相關聯，因為封裝的指令碼檔案會包含比公用 nuget.org 的組件庫上找到的相同封裝中的指令碼檔案的不同授權文字。 文字的差異可避免造成有不同的內容雜湊值的指令碼檔案的不同授權文字區塊的結果繼續執行的封裝更新，並因此被視為在專案中修改。

若要減輕這個問題，NuGet 2.7.2 可讓指令碼作者，以包含授權文字區塊，看起來，如下所示的特殊標記區段內。

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

更新封裝的內容時檔案，其中包含這個區塊中，NuGet 不因素區塊的內容與在 NuGet gallery 上的版本比較可以因此刪除和更新內容檔案，就好像它會比對的原始複本。

此區塊是以文字"NUGET:: BEGIN 授權 」 和識別 「 NUGET:: END 授權文字 」 發生任何位置的開始和結束行。  沒有其他格式的需求存在時，它會讓這項功能，以用於任何類型的文字檔案，不論語言為何。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>將繫結重新導向的非 Framework 組件
對於屬於.NET Framework 的組件，NuGet 會略過加入繫結重新導向至應用程式的組態檔更新封裝時。 此修正位址 NuGet 2.7 藉此繫結重新導向未被加入針對某些組件，即使這些組件不在迴歸視為.NET Framework 的一部分。 NuGet 2.7.2 還原先前的 NuGet 2.5 和 2.6 行為，並加入繫結重新導向。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>利用 Xamarin 工具安裝中安裝可攜式程式庫
Xamarin 的開發工具的機器上安裝之後，他們會修改指定現有的目標 framework 組合和 Xamarin 架構之間的相容性支援的架構組態資料。 2.7.2 的版本，NuGet 是留意這些隱含的相容性規則，因此輕鬆 Xamarin 平台目標的開發人員套件中的這類安裝之 Xamarin 相容，但未明確標記為可攜式類別庫中繼資料本身。

### <a name="machine-wide-configuration-settings-honored"></a>接受的整部機器的組態設定
使用階層式 Nuget.Config 檔案時，repositoryPath 索引鍵不被接受 Nuget.Config 檔案的最接近方案根目錄。 在 Visual Studio 2013 中，NuGet 會安裝在 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config 自訂 Nuget.Config 檔案以加入 < Microsoft 和.NET 封裝來源。 如此一來，解決在方案中使用自訂的 repositoryPath 已刪除電腦層級 Nuget.Config-這也意味著移除 < Microsoft 和.NET 封裝來源。 使用階層式 Nuget.Config 檔案時，NuGet 2.7.2 現在會接受 repositoryPath 優先順序規則。

## <a name="all-changes"></a>所有的變更
如需完整的工作清單項目固定在 NuGet 2.7.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。
