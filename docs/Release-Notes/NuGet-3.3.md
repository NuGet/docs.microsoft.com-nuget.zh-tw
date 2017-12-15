---
title: "NuGet 3.3 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4110a36a-cffe-4038-8da4-e841bce6e94b
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.3 的版本資訊。"
keywords: "NuGet 3.3 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f35f7621db324957b0af8329cf9faa11493835e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 版本資訊

[NuGet 3.2.1 版本資訊](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 版本資訊](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 發行 2015 年 11 月 30 日與大量的使用者介面更新和命令列的功能，以及有助於修正 NuGet 用戶端的集合。

## <a name="new-features"></a>新功能

* 已引進，允許 NuGet 命令列用戶端可以緊密地與已驗證的摘要使用認證提供者。 [指示如何安裝 Visual Studio Team Services 認證提供者](../API/nuget-exe-Credential-Providers.md)及設定 NuGet 用戶端使用其可用的 NuGet 文件。

## <a name="new-user-interface-features"></a>新的使用者介面功能

* 個別的瀏覽、 安裝和更新可用索引標籤
* 更新可用徽章表示封裝名稱中有可用的更新數目
* 封裝徽章指出封裝是否已安裝的套件清單中或已有可用更新
* 下載計數和作者加入至封裝清單
* 最高可用的版本號碼和封裝清單目前安裝的版本號碼
* 動作按鈕，以允許快速安裝、 更新及解除安裝的套件清單
* 封裝詳細資料面板上更清楚的動作按鈕
* 封裝詳細資料面板上的套件更新日期
* 合併方案檢視中的面板
* 可排序方格中的專案和方案 檢視的已安裝的版本號碼

## <a name="new-command-line-features"></a>命令列的新功能

此版本引進`add`和`init`初始化資料夾為基礎儲存機制中所述的命令[nuget.exe 參考](../tools/nuget-exe-cli-reference.md)。 儲存機制，建構和維護與此資料夾結構將[提供效能優勢明顯](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我們的部落格上所述。

## <a name="contentfiles"></a>ContentFiles

內容現可支援`project.json`managed 透過新的專案`contentFiles`資料夾和`.nuspec``contentFiles`元素標記法。  此內容可以更直接指定由封裝作者提供專案系統互動。  有關如何設定中的 contentFiles 更多資訊`.nuspec`文件位於[.nuspec 參考](../schema/nuspec.md)。

## <a name="nuget-locals-cache-management"></a>NuGet 本機快取管理

NuGet 命令列已更新為包含有關如何管理在工作站上的本機快取的資訊。  [區域變數] 命令的詳細資訊可用於[NuGet 命令列參照](../tools/cli-ref-locals.md)。

## <a name="fixed-issues"></a>已修正的問題

**值得注意的問題**

* NuGet 的命令列還原的支援還原封裝與方案檔上 Mono- [1543年](https://github.com/NuGet/Home/issues/1543)

3.3 版本已解決的問題的完整清單可以在 GitHub 上找到[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。

在 3.3 命令列的版本中修正問題的清單會記錄在[3.3 命令列里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。

## <a name="known-issues"></a>已知問題

我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)