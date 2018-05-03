---
title: NuGet 3.1 版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.1 版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 版本資訊

[NuGet 3.0 版本資訊](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 版本資訊](../release-notes/nuget-3.1.1.md)

NuGet 3.1 已發行於 2015 年 7 月 27 日做為通用 Windows 平台 SDK 配套擴充 Visual Studio 2015。 我們傳送與 Windows 平台 SDK 的這個版本中，Windows 程式開發體驗無法充分利用先前已啟動的 NuGet 跨平台工作。 此 NuGet 延伸模組版本只適用於 Visual Studio 2015。

這些開發人員可存取可供使用，我們一律會發佈具有 bug 修正和新功能更新為最新版本的 Visual Studio 組件庫更新建議。

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 擴充功能

問題和此版本功能會標記與 GitHub 上[「 3.1 RTM UWP 轉移支援 」 里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)總共我們關閉 67 3.1 版本中的問題。

### <a name="new-features"></a>新功能

* `project.json` 支援 Windows 適用 UWP 和 ASP.NET 5 支援
* 可轉移的套件安裝

描述與這些功能的定義可以找到其他地方文件中。

### <a name="deprecated"></a>已被取代

下列功能就不再適用於 Visual Studio 2015:

* 無法再安裝方案層級的套件

下列的功能就不再適用於 Visual Studio 2015 和使用的專案`project.json`規格

* `install.ps1` 和`uninstall.ps1`-這些指令碼封裝安裝期間將會忽略、 還原、 更新及解除安裝
* 設定轉換將會被忽略
* 內容將會執行，但是不會複製到專案。
    * 小組正在重新實作這項功能，請依照下列討論進度： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>已知問題

沒有傳遞此版本的已知問題的數字。

* 安裝與 Windows 10 SDK 3.1 版本將會降級任何版本的先前已安裝的 NuGet 延伸模組

## <a name="nuget-command-line"></a>NuGet 命令列

NuGet 命令列可執行檔已更新，並移至新的 「 可散布位置，如此 nuget.exe 歷史版本才能繼續可供使用。  您可以在 windows 下載 nuget.exe 3.1 beta 版： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

新的 「 可散布位置位於 dist.nuget.org 主機上，使用此範本會遵循資料夾結構：

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>新功能

* nuget.exe 可以還原，並將封裝安裝到使用專案`project.json`檔案。
* nuget.exe 可以連接及取用在 NuGet v3 通訊協定： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>已知問題 ##

1.    無法執行組件針對`project.json`檔案- [928](https://github.com/NuGet/Home/issues/928)
2.    不支援單聲道- [1059年](https://github.com/NuGet/Home/issues/1059)
3.    未當地語系化- [1058年](https://github.com/NuGet/Home/issues/1058)， [1057年](https://github.com/NuGet/Home/issues/1057)
4.    未簽署，就像現存http://nuget.org/nuget.exe- [1073年](https://github.com/NuGet/Home/issues/1073)
