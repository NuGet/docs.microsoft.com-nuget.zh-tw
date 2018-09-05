---
title: NuGet 1.3 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.3 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551347"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 的版本資訊

[NuGet 1.2 版本資訊](../release-notes/nuget-1.2.md) | [NuGet 1.4 版本資訊](../release-notes/nuget-1.4.md)

於 2011 年 4 月 25 日發行 NuGet 1.3。

## <a name="new-features"></a>新功能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>簡化的封裝建立符號伺服器整合

NuGet 小組合作的人一定[SymbolSource.org](http://www.symbolsource.org/)來提供一個非常簡單的方式，以及您的套件，發佈您的來源和 PDB。 這可讓您的套件的取用者，逐步執行偵錯工具在您套件的來源。 如需詳細資訊，請參閱[建立和發行符號套件](../create-packages/symbol-packages.md)發行 NuGet 套件來源使用簡單的方法。 您也可以觀看的現場示範這項功能的一部分深入了解 NuGet 在 Mix11 討論。 這項功能是完整的 8:27 開始示範影片的 20 分鐘標記處。

### <a name="open-packagepage-command"></a>`Open-PackagePage` 命令

此命令可讓您能夠輕鬆地在套件管理員主控台 內從封裝的專案頁面。 它也提供選項，以開啟 授權 URL 及報表內容粗俗的文章頁面，為套件。
命令的語法是：

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru`選項用來傳回所指定 URL 的值。

例如：

    PM> Open-PackagePage Ninject

開啟瀏覽器並前往 Ninject 封裝中指定的專案 URL。

    PM> Open-PackagePage Ninject -License

開啟瀏覽器並前往 Ninject 封裝中指定的授權 URL。

    PM> Open-PackagePage Ninject -ReportAbuse

將瀏覽器開啟至目前的封裝來源來指定封裝的 檢舉不當使用的 URL。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

指派給變數，也就是 $url，授權 URL，而不需要在瀏覽器中開啟 URL。

### <a name="performance-improvements"></a>效能改善

NuGet 1.3 導入了許多效能改善。 NuGet 1.3 以避免多次下載相同版本的封裝，包含的每個使用者的本機快取。 可以存取和透過 [套件管理員設定] 對話方塊中清除快取：

![NuGet 套件快取設定的選項 對話方塊](./media/nuget-options.png)

其他效能改進功能包括新增支援 HTTP 壓縮，以及改善 Visual Studio 內的套件安裝速度。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 和 nuget.exe 會使用相同的套件來源清單

NuGet 1.3 之前的 nuget.exe 與 NuGet Visual Studio 增益集所使用的套件來源清單已不會儲存在相同的位置。 NuGet 1.3 現在會在兩個位置使用相同的清單。 清單儲存在`NuGet.Config`並儲存在 [AppData] 資料夾中。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 會忽略的檔案和資料夾，以開頭 '。 ' 預設

為了讓這類 Subversion 和 mercurial 都會處理與原始檔控制系統的 NuGet，nuget.exe 會忽略資料夾和檔案的開頭 '。 ' 字元建立封裝時。 這可以使用覆寫兩個新旗標：

* __-NoDefaultExcludes__用來覆寫此設定，並包含所有檔案。
* __-排除__用來新增其他檔案/資料夾排除使用模式。 例如，若要排除 '.bak' 副檔名的所有檔案

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注意： 模式不是預設的遞迴。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX 專案和.NET Micro Framework 支援

由於社群貢獻，NuGet 會包含 WiX 專案類型，以及.NET Micro Framework 的支援。

## <a name="bug-fixes"></a>Bug 修正

Bug 修正的完整清單，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的錯誤修正

* 與原始程式檔的套件運作在這兩個網站和 Web 應用程式專案中。
原始程式檔複製到網站，`App_Code`資料夾
