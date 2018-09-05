---
title: NuGet 2.8.5 版本資訊
description: 版本資訊 NuGet 2.8.5 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548621"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 版本資訊

[NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 版本資訊](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 釋放 2015 年 3 月 30 日。 它是次要更新到我們 2.8.3 VSIX 某些目標修正。

在此版本中，NuGet 套件管理員 對話方塊的支援已針對[DNX 目標 Framework Moniker](https://github.com/aspnet/dnx)。  這些新的 framework moniker 的支援包括：

* **core50** -'base' 的目標 framework moniker (TFM) 與核心 CLR 相容。
* **dnx452** -使用完整 4.5.2 TFM 特定 DNX 型應用程式的 framework 版本
* **dnx46** -使用完整 4.6 版本的 framework TFM 特定 DNX 型應用程式
* **dnxcore50** -使用 framework Core 5.0 版的 TFM 特定 DNX 型應用程式

一個 bug 已修正導致無法正確地安裝到 FSharp 專案封裝：

https://nuget.codeplex.com/workitem/4400