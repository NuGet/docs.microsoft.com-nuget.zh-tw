---
title: NuGet 2.8.5 版本資訊
description: NuGet 2.8.5 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780350"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 版本資訊

[NuGet 2.8.3 版本](../release-notes/nuget-2.8.3.md)  |  資訊[NuGet 2.8.6 版本](../release-notes/nuget-2.8.6.md)資訊

NuGet 2.8.5 已于2015年3月30日發行。 這是 2.8.3 VSIX 的次要更新，包含一些目標修正。

在此版本中，已針對 [DNX 目標 Framework 的名字](https://github.com/aspnet/dnx)已新增 NuGet 封裝管理員的支援對話方塊。  支援的新 framework 標記包括：

* **core50** -A ' base ' 目標 framework 標記 (TFM 與核心 CLR 相容的) 。
* **dnx452** -使用完整4.5.2 版架構的 DNX 型應用程式專用 TFM
* **dnx46** -使用完整4.6 版架構的 DNX 型應用程式專用 TFM
* **dnxcore50** -使用核心5.0 版架構的 DNX 型應用程式專用 TFM

修正了一個錯誤，導致套件無法正確安裝至 Fsharp.core 專案：

https://nuget.codeplex.com/workitem/4400