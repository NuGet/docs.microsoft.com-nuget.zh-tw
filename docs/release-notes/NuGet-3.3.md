---
title: NuGet 3.3 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.3 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546643"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 版本資訊

[NuGet 3.2.1 版本資訊](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 版本資訊](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 已發行 2015 年 11 月 30 日的大量的使用者介面更新和命令列功能，以及有助於修正 NuGet 用戶端的集合。

## <a name="new-features"></a>新功能

* 已引進，讓能夠完美搭配的已驗證摘要的 NuGet 命令列用戶端認證提供者。 [有關如何安裝 Visual Studio Team Services 的認證提供者](../api/nuget-exe-credential-providers.md)並設定 NuGet 使用的用戶端均可在 NuGet 文件。

## <a name="new-user-interface-features"></a>新的使用者介面功能

* 不同的瀏覽、 安裝和更新可用索引標籤
* 更新可用的徽章，表示封裝名稱中有可用的更新數目
* 表示如果封裝已安裝，或有可用更新的套件清單中的套件徽章
* 下載計數和作者新增至套件清單
* 最高可用的版本號碼和套件清單上的目前安裝的版本號碼
* 動作按鈕，以允許快速安裝、 更新及解除安裝的套件清單
* 封裝詳細資料 面板上更清楚的動作按鈕
* 封裝詳細資料 面板上的封裝更新日期
* 合併方案 檢視中的面板
* 可排序方格中的專案和方案 檢視的已安裝的版本號碼

## <a name="new-command-line-features"></a>命令列的新功能

此版本引進`add`並`init`命令，以初始化資料夾為基礎的存放庫中所述[nuget.exe 參考](../tools/nuget-exe-cli-reference.md)。 存放庫，建構和維護與此資料夾結構將會[提供效能優勢明顯](http://blog.nuget.org/20150922/Accelerate-Package-Source.html)我們的部落格上所述。

## <a name="contentfiles"></a>ContentFiles

現在支援內容`project.json`管理透過新的專案`contentFiles`資料夾並`.nuspec``contentFiles`元素標記法。  此內容也可以更直接指定由封裝作者與專案系統互動。  詳細資訊，有關如何設定中的 contentFiles`.nuspec`文件可在[.nuspec 參考](../reference/nuspec.md)。

## <a name="nuget-locals-cache-management"></a>NuGet 區域變數快取管理

NuGet 命令列已更新為包括如何管理的工作站上的本機快取的相關資訊。  Locals 命令的詳細資訊位於[NuGet 命令列參考](../tools/cli-ref-locals.md)。

## <a name="fixed-issues"></a>已修正的問題

**值得注意的問題**

* NuGet 命令列還原的支援還原套件在 Mono-方案檔[1543年](https://github.com/NuGet/Home/issues/1543)

3.3 版的版本中已解決的問題的完整清單可在 GitHub 上[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)。

3.3 的命令列版本中修正的問題的清單中會記錄[3.3 的命令列里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)。

## <a name="known-issues"></a>已知問題

我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)