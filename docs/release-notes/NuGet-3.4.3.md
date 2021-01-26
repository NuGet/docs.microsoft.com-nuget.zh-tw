---
title: NuGet 3.4.3 版本資訊
description: NuGet 3.4.3 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776467"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 版本資訊

[NuGet 3.4.2 版本](../release-notes/nuget-3.4.2.md)  |  資訊[NuGet 3.4.4 版本](../release-notes/nuget-3.4.4.md)資訊

NuGet 3.4.3 已于2016年4月22日發行，以解決在3.4 和後續版本中識別的數個問題。

您可以在 [這裡](https://dist.nuget.org/index.html)下載 VSIX 和 nuget.exe。

## <a name="updates-and-improvements"></a>更新和改進

* 改善 Visual Studio 的可靠性。 我們已修正 NuGet 中導致 Visual Studio 損毀的一些問題。

## <a name="fixes"></a>修正

* 修正了一些受密碼保護的私用 nuget 摘要的授權問題。
* 已修正無法從指定的執行時間還原 PCL 之的問題 `project.json` 。
* 某些客戶在安裝套件時遇到間歇性失敗。 這項功能現在已在此版本中修正。
* 修正在 c + +/CLI 專案中導致還原失敗的問題 `project.json` 。
* 某些套件 (例如，當您在 mono 中使用 nuget 時，未正確解壓縮的 ModernHttpClient) 。 這項功能現在已在此版本中修正。

如需此版本中的修正和增強功能的完整清單，請參閱 [此處](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)的問題清單。