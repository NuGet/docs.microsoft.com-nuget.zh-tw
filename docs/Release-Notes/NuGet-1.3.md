---
title: "NuGet 1.3 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.3。"
keywords: "NuGet 1.3 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 版的版本資訊

[NuGet 1.2 版本資訊](../release-notes/nuget-1.2.md) | [NuGet 1.4 版本資訊](../release-notes/nuget-1.4.md)

NuGet 1.3 已於 2011 年 4 月 25 日發行。

## <a name="new-features"></a>新功能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>簡化的封裝建立符號伺服器整合

NuGet 團隊在協助人員[SymbolSource.org](http://www.symbolsource.org/)提供真正簡易的方式以及您的套件中發佈您的來源和 PDB 的。 這可讓您的封裝的取用者逐步執行您在偵錯工具中的封裝的來源。 如需詳細資訊，請參閱[建立和發行符號套件](../create-packages/symbol-packages.md)簡單的方法發佈 NuGet 套件的來源。 您也可以觀看即時的示範這項功能的深度 NuGet 一部分在 Mix11 與互動。 這項功能會完全示範開始在 20 分鐘標記的視訊。

### <a name="open-packagepage-command"></a>`Open-PackagePage`命令

此命令讓您更容易取得來源的封裝，封裝管理員主控台內的 [專案] 頁面。 它也提供選項，以開啟 授權 URL 及報表濫用頁面封裝。
命令語法如下：

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru`選項用來傳回所指定 URL 的值。

例如：

    PM> Open-PackagePage Ninject

將瀏覽器開啟至 Ninject 封裝中指定的專案 URL。

    PM> Open-PackagePage Ninject -License

將瀏覽器開啟至 Ninject 封裝中指定的授權 URL。

    PM> Open-PackagePage Ninject -ReportAbuse

將瀏覽器開啟至目前用來回報不當使用，指定封裝的封裝來源的 URL。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

將授權 URL 指派給變數，$url，，而不需要在瀏覽器中開啟 URL。

### <a name="performance-improvements"></a>效能改善

NuGet 1.3 導入了許多效能改進。 NuGet 1.3 可避免多次下載相同版本的封裝，包含每個使用者的本機快取。 可以存取和透過 [封裝管理員設定] 對話方塊中清除快取：

![NuGet 套件快取設定的選項 對話方塊](./media/nuget-options.png)

其他效能改進功能包括支援的 HTTP 壓縮，並改善 Visual Studio 中的封裝安裝速度。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 和 nuget.exe 使用相同的封裝來源清單

NuGet 1.3 之前 nuget.exe 和 NuGet Visual Studio 增益集所使用的套件來源清單並未儲存在相同的位置。 NuGet 1.3 現在會在兩個位置使用相同的清單。 清單儲存在`NuGet.Config`並儲存在 [AppData] 資料夾。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 會忽略檔案和資料夾，以開頭 '。 ' 預設

為了讓適用於原始檔控制系統，這類 Subversion 和 Mercurial NuGet，nuget.exe 會忽略開頭的檔案和資料夾 '。 ' 字元建立封裝時。 這會覆寫使用兩個新旗標：

* __-NoDefaultExcludes__用來覆寫此設定，並包含所有的檔案。
* __-排除__用來將其他檔案/資料夾排除使用模式。 例如，若要排除 '.bak' 副檔名的所有檔案

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注意： 此模式不是遞迴的預設。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX 專案和.NET 微架構的支援

這點受惠社群投稿，NuGet 會包含 WiX 專案類型，以及.NET 微架構的支援。

## <a name="bug-fixes"></a>Bug 修正

如需完整的 bug 修正清單，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修正

* 與原始程式檔的封裝工作中兩個網站和 Web 應用程式專案中。
原始程式檔複製到網站，`App_Code`資料夾
