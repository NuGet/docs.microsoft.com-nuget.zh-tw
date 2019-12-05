---
title: NuGet 1.3 版本資訊
description: NuGet 1.3 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825258"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 版本資訊

[Nuget 1.2 版本](../release-notes/nuget-1.2.md)資訊 | [nuget 1.4 版本](../release-notes/nuget-1.4.md)資訊

NuGet 1.3 已于2011年4月25日發行。

## <a name="new-features"></a>新功能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>使用符號伺服器整合簡化封裝建立

NuGet 團隊與[SymbolSource.org](http://www.symbolsource.org/)的人員合作，提供一種簡單的方式來發佈您的來源和 PDB 以及您的套件。 這可讓您封裝的取用者在偵錯工具中逐步執行封裝的來源。 如需更多詳細資料，請閱讀[建立和發佈符號套件](../create-packages/symbol-packages.md)簡單的方式來發佈具有來源的 NuGet 套件。 您也可以觀賞這項功能的實況示範，做為 NuGet 的一部分，Mix11 的深度討論。 這項功能會從影片的20分鐘標記開始完整示範。

### <a name="open-packagepage-command"></a>`Open-PackagePage` 命令

此命令可讓您輕鬆地從套件管理員主控台中取得封裝的專案頁面。 它也會提供選項，以開啟封裝的 [授權 URL] 和 [報告濫用] 頁面。
此命令的語法為：

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` 選項是用來傳回指定之 URL 的值。

範例：

    PM> Open-PackagePage Ninject

將瀏覽器開啟至 Ninject 封裝中指定的專案 URL。

    PM> Open-PackagePage Ninject -License

將瀏覽器開啟至 Ninject 套件中指定的授權 URL。

    PM> Open-PackagePage Ninject -ReportAbuse

將瀏覽器開啟至目前封裝來源上用來報告指定封裝之不當使用的 URL。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

將授權 URL 指派給變數，$url，而不在瀏覽器中開啟 URL。

### <a name="performance-improvements"></a>效能改善

NuGet 1.3 引進了許多效能改進。 NuGet 1.3 藉由包含本機個別使用者快取，避免多次下載相同版本的套件。 您可以透過 [套件管理員設定] 對話方塊來存取和清除快取：

![具有套件快取設定的 NuGet 選項對話方塊](./media/nuget-options.png)

其他效能改進包括新增 HTTP 壓縮的支援，以及改善 Visual Studio 內的封裝安裝速度。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 和 nuget.exe 會使用相同的套件來源清單

在 NuGet 1.3 之前，nuget.exe 和 NuGet Visual Studio 增益集所使用的套件來源清單不會儲存在相同的位置。 NuGet 1.3 現在會在這兩個位置中使用相同的清單。 此清單會儲存在 `NuGet.Config` 中，並儲存在 AppData 資料夾中。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 預設會忽略以 '. ' 開頭的檔案和資料夾

為了讓 NuGet 適用于 Subversion 和 Mercurial 等原始檔控制系統，nuget.exe 會在建立封裝時，忽略以 '. ' 字元開頭的資料夾和檔案。 這可以使用兩個新旗標來覆寫：

* __-NoDefaultExcludes__是用來覆寫此設定並包含所有檔案。
* __-Exclude__是用來新增其他檔案/資料夾，以使用模式來排除。 例如，排除所有副檔名為 ' .bak ' 的檔案

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注意：根據預設，模式不是遞迴的。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>支援 WiX 專案和 .NET 微架構

由於有了社區投稿，NuGet 包含 WiX 專案類型和 .NET 微架構的支援。

## <a name="bug-fixes"></a>Bug 修正

如需錯誤修正的完整清單，請參閱[此版本的 NuGet 問題追蹤](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)器。

## <a name="bug-fixes-worth-noting"></a>Bug 修正值得注意

* 具有來源檔案的封裝可在網站和 Web 應用程式專案中使用。
針對網站，會將原始程式檔複製到 `App_Code` 資料夾
