---
title: NuGet 3.1 版本資訊
description: NuGet 3.1 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776528"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 版本資訊

[NuGet 3.0 版本](../release-notes/nuget-3.0.0.md)  |  資訊[NuGet 3.1.1 版本](../release-notes/nuget-3.1.1.md)資訊

NuGet 3.1 已于2015年7月27日發行為通用 Windows 平臺 SDK 的配套延伸模組，可用於 Visual Studio 2015。 我們已透過 Windows Platform SDK 提供此版本，讓 Windows 開發體驗可以利用先前已啟動的 NuGet 跨平臺工作。 此 NuGet 擴充功能版本僅適用于 Visual Studio 2015。

我們建議可存取 Visual Studio 資源庫的開發人員更新為可用的最新版本，因為我們一律會發佈具有 bug 修正和新功能的更新。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 擴充功能

此版本中的問題和功能已在 GitHub 上標記為「 [3.1 RTM UWP 可轉移支援」里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  ，但我們已在3.1 版本中關閉67問題。

### <a name="new-features"></a>新功能

* `project.json` 支援 Windows UWP 和 ASP.NET 5 支援
* 可轉移的套件安裝

您可以在檔的其他位置找到這些功能的描述和定義。

### <a name="deprecated"></a>已被取代

下列功能不再適用于 Visual Studio 2015：

* 無法再安裝解決方案層級套件

下列功能不再適用于 Visual Studio 2015 和使用規格的專案 `project.json`

* `install.ps1` 和 `uninstall.ps1` -在套件安裝、還原、更新和卸載期間，將會忽略這些腳本。
* 將忽略設定轉換
* 將會攜帶內容，但不會複製到專案中。
    * 小組正致力於重新執行這項功能，請遵循下列討論和進度： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>已知問題

此版本提供一些已知問題。

* 使用 Windows 10 SDK 安裝3.1 版本將會降級先前安裝的任何 NuGet 擴充功能版本

## <a name="nuget-command-line"></a>NuGet 命令列

NuGet 命令列可執行檔已更新並移至新的可轉散發位置，讓 nuget.exe 的歷程記錄版本可繼續使用。  您可以在下列位置下載適用于 Windows 的 3.1 Beta 版 nuget.exe： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

新的可散發位置位於 dist.nuget.org 主機上，其資料夾結構會在此範本之後：

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>新功能

* nuget.exe 可以將封裝還原並安裝到使用檔案的專案 `project.json` 。
* nuget.exe 可以連線至下列位置並使用 NuGet v3 通訊協定： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>已知問題 ##

1.    無法針對檔案執行套件 `project.json` - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono- [1059](https://github.com/NuGet/Home/issues/1059)不支援
3.    未當地語系化- [1058](https://github.com/NuGet/Home/issues/1058)、   [1057](https://github.com/NuGet/Home/issues/1057)
4.    未簽署，就像現有的 http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)一樣
