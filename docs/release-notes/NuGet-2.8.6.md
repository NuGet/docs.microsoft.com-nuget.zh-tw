---
title: NuGet 2.8.6 版本資訊
description: 版本資訊包含 NuGet 2.8.6 已知問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819714"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 版本資訊

[NuGet 2.8.5 版本資訊](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 版本資訊](../release-notes/nuget-2.8.7.md)

發行 NuGet 2.8.6 2015 年 7 月 20 日為我們 2.8.5 的次要更新，但有一些 VSIX 目標修正和增強功能支援 Windows 10 UWP 開發模型的支援可能會傳遞的套件。

這個版本的 NuGet 封裝管理員延伸模組會提供僅適用於 Visual Studio 2013 支援。

在此版本中，[NuGet 封裝管理員] 對話方塊會有新增的支援：

* 導入了 UAP 目標 Framework Moniker，以支援 Windows 10 應用程式開發。
* NuGet 的通訊協定第 3 版端點
* 支援[Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 屬性儲存機制來源。 預設值為"2"
* 回到遠端儲存機制如果在本機快取無法使用必要的套件版本