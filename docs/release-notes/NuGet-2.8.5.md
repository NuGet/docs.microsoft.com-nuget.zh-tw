---
title: NuGet 2.8.5 版本資訊
description: 版本資訊包含 NuGet 2.8.5 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 版本資訊

[NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 版本資訊](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 2015 年 3 月 30 日發行。 它是次要更新某些 VSIX 設為我們 2.8.3 目標修正程式。

在本版中的 NuGet 封裝管理員 新增的支援[DNX 目標 Framework Moniker](https://github.com/aspnet/dnx)。  這些新的 framework moniker 的支援包括：

* **core50** -'base' 的目標 framework moniker (TFM) 和核心 CLR 相容。
* **dnx452** -使用完整 4.5.2 TFM DNX 為基礎的特定應用程式的 framework 版本
* **dnx46** -使用 framework 完整 4.6 版 TFM DNX 為基礎的特定應用程式
* **dnxcore50** -A TFM DNX 為基礎的特定應用程式使用 framework Core 5.0 版

一個 bug 已修正無法正確安裝到 FSharp 專案無法在封裝：

https://nuget.codeplex.com/workitem/4400