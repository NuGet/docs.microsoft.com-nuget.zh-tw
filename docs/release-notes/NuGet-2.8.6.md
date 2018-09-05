---
title: NuGet 2.8.6 版本資訊
description: 版本資訊 NuGet 2.8.6 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546487"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 版本資訊

[NuGet 2.8.5 版本資訊](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 版本資訊](../release-notes/nuget-2.8.7.md)

發行 NuGet 2.8.6 2015 年 7 月 20 日做為我們 2.8.5 次要更新 VSIX 某些目標修正和改善，以支援 Windows 10 UWP 開發模型的支援可能會傳遞的封裝。

這個版本的 NuGet 套件管理員延伸模組提供只適用於 Visual Studio 2013 支援。

在此版本中，[NuGet 套件管理員] 對話方塊會有新增的支援：

* 導入了 UAP 目標 Framework Moniker，以支援 Windows 10 應用程式開發。
* NuGet 通訊協定第 3 版端點
* 支援[Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 屬性儲存機制來源。 預設值為"2"
* 正在回復到遠端存放庫如果在本機快取無法使用必要的套件版本