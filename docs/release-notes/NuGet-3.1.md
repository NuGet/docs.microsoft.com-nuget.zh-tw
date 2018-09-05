---
title: NuGet 3.1 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.1 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545343"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 版本資訊

[NuGet 3.0 版本資訊](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 版本資訊](../release-notes/nuget-3.1.1.md)

Visual Studio 2015 的 NuGet 3.1 已於 2015 年 7 月 27 日發行為通用 Windows 平台 SDK 的配套擴充功能。 我們提供此版本中的使用 Windows 平台 SDK，讓 Windows 開發經驗可以利用先前已啟動的 NuGet 跨平台工作。 這個 NuGet 擴充功能版本僅適用於 Visual Studio 2015。

我們建議開發人員可存取 Visual Studio 組件庫更新，可供使用，因為我們一律會發佈與 bug 修正和新功能更新為最新版本。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 擴充功能

問題與此版本中的功能都會標記與 GitHub 上[「 3.1 RTM UWP 轉移支援 」 里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)共有的情況下，我們會關閉 67 3.1 版本中的問題。

### <a name="new-features"></a>新功能

* `project.json` 支援 Windows UWP 和 ASP.NET 5 支援
* 可轉移套件安裝

描述與這些功能的定義位於其他地方文件。

### <a name="deprecated"></a>已被取代

下列功能已不再適用於 Visual Studio 2015:

* 可以不會再安裝方案層級套件

下列功能已不再適用於 Visual Studio 2015 和使用專案`project.json`規格

* `install.ps1` 和`uninstall.ps1`-這些指令碼套件安裝期間將會忽略、 還原、 更新及解除安裝
* 設定轉換將會被忽略
* 內容將會執行，但不是會複製到專案。
    * 小組正在致力於重新實作這項功能，請遵循討論並在進行中： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>已知問題

已有許多隨此版本的已知問題。

* Windows 10 sdk 3.1 版的安裝將會降級任何版本的先前已安裝的 NuGet 延伸模組

## <a name="nuget-command-line"></a>NuGet 命令列

NuGet 命令列可執行檔已更新，並移至新的可散布位置，因此歷程記錄的 nuget.exe 版本可以繼續可供使用。  您可以下載 nuget.exe 的 3.1 beta 版的 Windows 在： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

新的可散布位置位於 dist.nuget.org 主機上，使用此範本會遵循資料夾結構：

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>新功能

* nuget.exe，即可還原及套件安裝到使用專案`project.json`檔案。
* 可以連接到 nuget.exe，並使用在 NuGet v3 通訊協定： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>已知問題 ##

1.    無法執行組件針對`project.json`檔案- [928](https://github.com/NuGet/Home/issues/928)
2.    不支援 Mono- [1059年](https://github.com/NuGet/Home/issues/1059)
3.    未當地語系化- [1058年](https://github.com/NuGet/Home/issues/1058)， [1057年](https://github.com/NuGet/Home/issues/1057)
4.    未簽署，就像現存 http://nuget.org/nuget.exe  -  [1073年](https://github.com/NuGet/Home/issues/1073)
