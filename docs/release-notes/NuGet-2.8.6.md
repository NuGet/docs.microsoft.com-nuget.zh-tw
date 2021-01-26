---
title: NuGet 2.8.6 版本資訊
description: NuGet 2.8.6 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776698"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 版本資訊

[NuGet 2.8.5 版本](../release-notes/nuget-2.8.5.md)  |  資訊[NuGet 2.8.7 版本](../release-notes/nuget-2.8.7.md)資訊

NuGet 2.8.6 已于2015年7月20日發行為 2.8.5 VSIX 的次要更新，並提供一些目標修正和增強功能，以支援可透過 Windows 10 UWP 開發模型提供支援的封裝。

此版本的 NuGet 套件管理員延伸模組僅提供 Visual Studio 2013 的支援。

在此版本中，NuGet 封裝管理員對話方塊已新增下列功能的支援：

* 引進了 UAP 目標 Framework 的標記，以支援 Windows 10 應用程式開發。
* NuGet 通訊協定第3版端點
* 支援在存放庫來源上 [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 屬性。 預設值為 "2"
* 在本機快取中無法使用必要的套件版本時，回復至遠端存放庫