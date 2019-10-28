---
title: NuGet 用戶端 SDK
description: API 不斷演進，尚未記載，但範例可在 Dave Glick 的 blog 中取得。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924610"
---
# <a name="nuget-client-sdk"></a>NuGet 用戶端 SDK

*Nuget 用戶端 SDK*是指以[nuget. 命令](https://www.nuget.org/packages/NuGet.Commands)、 [nuget、封裝](https://www.nuget.org/packages/NuGet.Packaging)和[NuGet. 通訊協定](https://www.nuget.org/packages/NuGet.Protocol)為中心的 nuget 套件群組。 這些套件會取代先前的[NuGet. 核心](https://www.nuget.org/packages/NuGet.Core/)程式庫。

> [!Note]
>  如需 NuGet 伺服器通訊協定的相關檔，請參閱[Nuget 伺服器 API](~/api/overview.md)。

## <a name="source-code"></a>原始程式碼

原始程式碼發佈于 GitHub 上的專案[NuGet/nuget. 用戶端](https://github.com/NuGet/NuGet.Client)。

## <a name="third-party-documentation"></a>協力廠商檔

您可以在下列 blog 系列中找到一些 API 的範例和檔： Dave Glick，發佈的2016：

- [探索 NuGet v3 程式庫，第1部分：簡介和概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [探索 NuGet v3 程式庫，第2部分：搜尋封裝](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [探索 NuGet v3 程式庫，第3部分：安裝套件](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> 這些 blog 文章是在 NuGet 用戶端 SDK 套件的**3.4.3**版本發行後不久撰寫。
> 較新版本的套件可能與 blog 文章中的資訊不相容。

聖馬丁 Björkström 在 Dave Glick 的 blog 系列文章中，介紹了使用 NuGet 用戶端 SDK 來安裝 NuGet 套件的不同方法：

- [重新訪 NuGet v3 程式庫](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
