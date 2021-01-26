---
title: NuGet 1.3 版本資訊
description: NuGet 1.3 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777121"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 版本資訊

[NuGet 1.2 版本](../release-notes/nuget-1.2.md)  |  資訊[NuGet 1.4 版本](../release-notes/nuget-1.4.md)資訊

NuGet 1.3 已于2011年4月25日發行。

## <a name="new-features"></a>新功能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>使用符號伺服器整合簡化套件建立

NuGet 團隊與 [SymbolSource.org](http://www.symbolsource.org/) 的人員合作，提供一種非常簡單的方式來發佈您的來源和 PDB 以及套件。 這可讓您封裝的取用者在偵錯工具中逐步執行封裝的來源。 如需更多詳細資料，請參閱 [建立和發佈符號套件](../create-packages/symbol-packages.md) 的簡易方式，可讓您輕鬆地發佈具有來源的 NuGet 套件。 您也可以觀看這項功能的實況示範，作為 NuGet 深入探討 Mix11 的一部分。 這項功能已從影片的20分鐘標示開始完整示範。

### <a name="open-packagepage-command"></a>`Open-PackagePage` 命令

此命令可讓您輕鬆地從封裝管理員主控台中，取得封裝的 [專案] 頁面。 它也提供選項來開啟封裝的授權 URL 和 [報告不當] 頁面。
命令的語法為：

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

`-PassThru`選項是用來傳回指定之 URL 的值。

範例：

```
PM> Open-PackagePage Ninject
```

將瀏覽器開啟至 Ninject 封裝中指定的專案 URL。

```
PM> Open-PackagePage Ninject -License
```

開啟瀏覽器至 Ninject 封裝中指定的授權 URL。

```
PM> Open-PackagePage Ninject -ReportAbuse
```

開啟瀏覽器，指向目前套件來源的 URL，此 URL 是用來報告指定封裝的濫用。

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

將授權 URL 指派給變數 $url，而不在瀏覽器中開啟 URL。

### <a name="performance-improvements"></a>效能改進

NuGet 1.3 引進了許多效能改進。 NuGet 1.3 包含本機的每個使用者快取，可避免多次下載相同版本的套件。 您可以透過 [封裝管理員設定] 對話方塊來存取和清除快取：

![具有套件快取設定的 NuGet 選項對話方塊](./media/nuget-options.png)

其他效能改進包括新增 HTTP 壓縮的支援，以及改善 Visual Studio 內的套件安裝速度。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 和 nuget.exe 使用相同的套件來源清單

在 NuGet 1.3 之前，nuget.exe 和 NuGet Visual Studio Add-In 所使用的套件來源清單，不會儲存在相同的位置。 NuGet 1.3 現在會在這兩個位置中使用相同的清單。 此清單會儲存在中 `NuGet.Config` ，並儲存在 AppData 資料夾中。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 忽略以 '. ' 開頭的檔案和資料夾（預設值為 '. '）

為了讓 NuGet 可與原始檔控制系統（例如 Subversion 和 Mercurial）正常搭配運作，nuget.exe 會在建立封裝時忽略以 '. ' 字元開頭的資料夾和檔案。 您可以使用兩個新旗標來覆寫此內容：

* __-NoDefaultExcludes__ 用來覆寫此設定並包含所有檔案。
* __-Exclude__ 用來新增其他檔案/資料夾，以使用模式來排除。 例如，若要排除所有副檔名為 ' .bak ' 的檔案

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注意：模式預設並非遞迴。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX 專案和 .NET 微架構的支援

由於有參與的投稿，NuGet 包含 WiX 專案類型和 .NET 微架構的支援。

## <a name="bug-fixes"></a>Bug 修正

如需錯誤修正的完整清單，請參閱 [此版本的 NuGet 問題追蹤](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)程式。

## <a name="bug-fixes-worth-noting"></a>Bug 修正值得注意

* 具有原始程式檔的套件可在網站和 Web 應用程式專案中運作。
針對網站，會將來源檔案複製到 `App_Code` 資料夾
