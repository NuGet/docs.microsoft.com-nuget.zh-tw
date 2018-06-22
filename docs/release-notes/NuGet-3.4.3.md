---
title: NuGet 3.4.3 版本資訊
description: 版本資訊包含 NuGet 3.4.3 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820322"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 版本資訊

[NuGet 3.4.2 版本資訊](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 版本資訊](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 已發行於 2016 年 4 月 22 日解決幾個 3.4 及後續版本中已識別的問題。

您可以下載 VSIX 和 nuget.exe[這裡](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和增強功能

* Visual Studio 可靠性。 我們已修正一些問題造成損毀 Visual Studio 中的 NuGet 中。

## <a name="fixes"></a>修正程式

* 已修正一些授權問題受密碼保護的私用 nuget 摘要。
* 已修正的問題解決無法還原 PCL 的從`project.json`以指定的執行階段。
* 安裝封裝時，有些客戶已執行到斷斷續續地發生失敗。 這現在已在此版本中已修正。
* 已修正的問題導致還原失敗，在 C + + /CLI 專案與`project.json`。
* 其中無法解壓縮正確當您使用 nuget 中 mono 某些封裝 (例如 ModernHttpClient)。 這現在已在此版本中已修正。

如中這一版的修正和改善的完整清單，請參閱問題的清單[這裡](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。