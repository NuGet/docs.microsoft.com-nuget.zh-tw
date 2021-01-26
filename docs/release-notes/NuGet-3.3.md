---
title: NuGet 3.3 版本資訊
description: NuGet 3.3 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776513"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 版本資訊

[NuGet 3.2.1 版本](../release-notes/nuget-3.2.1.md)  |  資訊[NuGet 3.4-RC 版本](../release-notes/nuget-3.4-RC.md)資訊

NuGet 3.3 已于2015年11月30日發行，具有大量的使用者介面更新和命令列功能，以及 NuGet 用戶端的實用修正集合。

## <a name="new-features"></a>新功能

* 引進了認證提供者，讓 NuGet 命令列用戶端能夠順暢地使用已驗證的摘要。 有關[如何安裝 Visual Studio Team Services 認證提供者](../reference/extensibility/nuget-exe-credential-providers.md)，以及設定 nuget 用戶端以使用它的指示，可在 nuget 檔上取得。

## <a name="new-user-interface-features"></a>新的消費者介面功能

* 個別的 [流覽]、[已安裝] 和 [更新] 索引標籤
* 更新可用徽章，指出具有可用更新的套件數目
* 套件清單中的套件徽章，指出封裝是否已安裝或有可用的更新
* 新增至套件清單的下載計數和作者
* 套件清單上的最高可用版本號碼和目前已安裝的版本號碼
* 允許從套件清單快速安裝、更新及卸載的動作按鈕
* 套件詳細資料面板上更清楚的動作按鈕
* 套件詳細資料面板上的套件更新日期
* 方案視圖中的合併面板
* 方案視圖上專案的可排序方格和已安裝的版本號碼

## <a name="new-command-line-features"></a>新的命令列功能

在此版本中，我們引進了 `add` 和 `init` 命令來初始化以資料夾為基礎的儲存機制，如 [nuget.exe 參考](../reference/nuget-exe-cli-reference.md)中所述。 使用此資料夾結構所建立和維護的存放庫，會 [提供重要的效能優勢](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) ，如我們的 blog 所述。

## <a name="contentfiles"></a>ContentFiles

`project.json`Managed 專案現在會透過新的 `contentFiles` 資料夾和 `.nuspec` `contentFiles` 元素標記法來支援內容。  封裝作者可以直接指定此內容，以便與專案系統互動。  如需有關如何在檔中設定 contentFiles 的詳細資訊， `.nuspec` 請參閱 [nuspec 參考](../reference/nuspec.md)。

## <a name="nuget-locals-cache-management"></a>NuGet 區域變數快取管理

已更新 NuGet 命令列，以包含如何在工作站上管理本機快取的相關資訊。  有關 [區域變數] 命令的詳細資訊可在 [NuGet 命令列參考](../reference/cli-reference/cli-ref-locals.md)中取得。

## <a name="fixed-issues"></a>已修正的問題

**值得注意的問題**

* NuGet 命令列還原支援在 Mono- [1543](https://github.com/NuGet/Home/issues/1543)上使用方案檔還原套件

3.3 版中所解決問題的完整清單可在 GitHub 的 [3.3 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)下找到。

3.3 命令列版本中修正的問題清單會記錄在 [3.3 Command-Line 里程碑](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)中。

## <a name="known-issues"></a>已知問題

我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)