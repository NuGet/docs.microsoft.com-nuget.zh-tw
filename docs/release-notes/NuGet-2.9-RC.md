---
title: NuGet 2.9-RC 版本資訊
description: NuGet 2.9 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780314"
---
# <a name="nuget-29-rc-release-notes"></a>NuGet 2.9-RC 版本資訊

[NuGet 2.8.7 版本](../release-notes/nuget-2.8.7.md)  |  資訊[NuGet 3.0 Preview 版本](../release-notes/nuget-3.0-preview.md)資訊

NuGet 2.9 已于2015年9月10日發行為 Visual Studio 2012 和2013的 2.8.7 VSIX 更新。

### <a name="updates-in-this-release"></a>此版本中的更新

* 現在如果其包含的檔案格式不正確，則會略過處理套件 `.nuspec` - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* 修正了 \r\n for Unix/Linux 案例的 multipartwebrequest 處理- [776](https://github.com/NuGet/Home/issues/776)
* 修正 Visual Studio 2013 社區版本- [1180](https://github.com/NuGet/Home/issues/1180)中的組建事件整合


您可以在 GitHub 的[2.8.8 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)中找到此版本的完整修正清單
