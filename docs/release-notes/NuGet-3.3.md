---
title: NuGet 3.3 版本資訊
description: NuGet 3.3 的版本資訊, 包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317033"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 版本資訊

[Nuget 3.2.1 版本](../release-notes/nuget-3.2.1.md) | 資訊[nuget 3.4-RC 版本](../release-notes/nuget-3.4-RC.md)資訊

NuGet 3.3 已于2015年11月30日發行, 其中有大量的使用者介面更新和命令列功能, 以及對 NuGet 用戶端有用的修正集合。

## <a name="new-features"></a>新功能

* 已引進認證提供者, 可讓 NuGet 命令列用戶端能夠順暢地與已驗證的摘要搭配使用。 有關[如何安裝 Visual Studio Team Services 認證提供者](../api/nuget-exe-credential-providers.md), 以及如何設定 nuget 用戶端來使用它的指示, 可在 nuget 檔中取得。

## <a name="new-user-interface-features"></a>新的使用者介面功能

* 分隔 [流覽]、[已安裝] 和 [更新可用] 索引標籤
* 更新可用的徽章, 指出有可用更新的套件數目
* 封裝清單中的套件徽章, 指出套件是否已安裝, 或是否有可用的更新
* 將下載計數和作者新增至套件清單
* 套件清單上的最高可用版本號碼和目前安裝的版本號碼
* 允許從套件清單快速安裝、更新及卸載的動作按鈕
* 套件詳細資料面板上的動作按鈕更清楚
* 封裝詳細資料面板上的套件更新日期
* 解決方案視圖中的合併面板
* 解決方案視圖上專案的可排序方格和已安裝的版本號碼

## <a name="new-command-line-features"></a>新的命令列功能

在此版本中, 我們`add`引進`init`了和命令來初始化以資料夾為基礎的存放庫, 如[nuget.exe 參考](../reference/nuget-exe-cli-reference.md)中所述。 使用此資料夾結構來建立和維護的存放庫, 將可[提供更明顯的效能優勢](http://blog.nuget.org/20150922/Accelerate-Package-Source.html), 如我們的 blog 所述。

## <a name="contentfiles"></a>ContentFiles

`project.json`受控專案現在透過新`contentFiles`的資料夾和`.nuspec` `contentFiles`元素標記法支援內容。  封裝作者可以直接指定此內容, 以便與專案系統互動。  如需如何在`.nuspec`檔中設定 contentFiles 的詳細資訊, 請參閱[nuspec 參考](../reference/nuspec.md)。

## <a name="nuget-locals-cache-management"></a>NuGet 區域變數快取管理

NuGet 命令列已更新為包含如何在工作站上管理本機快取的相關資訊。  有關 [區域變數] 命令的詳細資訊可在[NuGet 命令列參考](../reference/cli-reference/cli-ref-locals.md)中取得。

## <a name="fixed-issues"></a>已修正問題

**值得注意的問題**

* NuGet 命令列還原支援在 Mono- [1543](https://github.com/NuGet/Home/issues/1543)上使用方案檔還原套件

3\.3 版本中所解決問題的完整清單可在 GitHub 的[3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)下找到。

3\.3 命令列版本中已修正的問題清單會記錄在[3.3 命令列里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)中。

## <a name="known-issues"></a>已知問題

我們會繼續追蹤 GitHub 問題清單的問題, 可以在下列位置找到:[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)