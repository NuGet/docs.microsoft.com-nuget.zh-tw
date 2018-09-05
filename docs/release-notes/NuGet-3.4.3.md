---
title: NuGet 3.4.3 版本資訊
description: 版本資訊 NuGet 3.4.3 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549161"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 版本資訊

[NuGet 3.4.2 版本資訊](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 版本資訊](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 已發行於 2016 年 4 月 22 日解決 3.4 及後續版本中已識別的幾個問題。

您可以下載 VSIX 和 nuget.exe[此處](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和增強功能

* 改善 Visual Studio 的可靠性。 我們已修正一些問題造成損毀 Visual Studio 中的 nuget。

## <a name="fixes"></a>修正

* 已修正一些授權問題受密碼保護的私用 nuget 摘要。
* 已修正的問題解決無法還原 PCL 的從`project.json`以指定的執行階段。
* 安裝套件時，某些客戶所遇到間歇性失敗。 這現在已修正在此版本中。
* 已修正的問題，導致還原失敗，在 C + + /cli 專案與`project.json`。
* 無法解壓縮正確當您使用 nuget 在 mono 中某些套件 (例如 ModernHttpClient)。 這現在已修正在此版本中。

如中此版本的修正和改善的完整清單，請參閱的問題清單[此處](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。